# Lab 02 — Proxmox and Ubuntu network foundation

**Status:** historical configuration, troubleshooting and administration results reported by the owner; original configurations and screenshots pending.

**Anonymized examples:** infrastructure addresses and hostnames use consistent RFC 5737 replacements, not actual deployed values. Loopback names/addresses retain their standard meaning. Commands below are explanatory examples, not instructions to connect to real infrastructure.

## Objective and baseline

Separate physical management from two virtual test segments and explain how the LAN endpoint, firewall and simulated WAN communicate. Full [addressing and resources](../architecture.md) are recorded centrally.

| Bridge | Historical role |
| --- | --- |
| vmbr0 | hypervisor-example management 192.0.2.50/24; Lenovo USB-Ethernet uplink to Cisco Gi1/0/1, access VLAN 10 |
| vmbr1 | Isolated LAN; no physical uplink; initially no host IP; VLAN-aware disabled |
| vmbr2 | Isolated simulated WAN; no physical uplink; host IP and VLAN-awareness setting not supplied |

VM 101 `lan-client-example` is Ubuntu Server with 2 vCPU, 2 GiB RAM, 20 GiB disk and an untagged VirtIO NIC on vmbr1, using `198.51.100.10/24`. VM 102 `lan-client2-example` was planned/configured on vmbr1 at `198.51.100.20/24`; its final verified deployment is unconfirmed.

VM 103 `wan-test-example` is attached to vmbr2 at `203.0.113.1/30`. VM 200 `firewall-example` has two VirtIO NICs: vtnet1 LAN on vmbr1 and vtnet0 WAN on vmbr2. Proxmox and Ubuntu release versions were not supplied.

## Troubleshooting case — VM 101 would not start

| Stage | Historical finding |
| --- | --- |
| Symptom | VM 101 failed to start |
| Configuration mismatch | VM NIC had VLAN tag 20 while vmbr1 was not VLAN-aware |
| Correction | Removed tag 20 from the VM NIC |
| Outcome | VM startup succeeded, according to the owner's training audit |
| Evidence limitation | Original error text, task log and screenshots not supplied |

The fix kept the virtual LAN untagged; it did not enable a trunk or integrate Cisco VLAN 20. The subnet number alone does not set an Ethernet VLAN tag.

## Secure administration case — local SSH forwarding

Historical path:

```text
Windows 192.0.2.10
  -> SSH to Proxmox 192.0.2.50:22
  -> host-originated TCP connection to OPNsense 198.51.100.1:443
```

The Proxmox host temporarily received a LAN-side address, represented here as `198.51.100.254/24`, on vmbr1 so it could reach the GUI target. Anonymized equivalent of the historical Windows command, provided for documentation rather than automatic execution:

```powershell
ssh -N -L 8443:198.51.100.1:443 root@192.0.2.50
```

- `-N` requests forwarding without running a remote command.
- `-L` forwards local TCP port 8443 through SSH to the named destination from the Proxmox side.
- `root@192.0.2.50` identifies the historical SSH destination/account; no password or key is included.
- The GUI was reached at `https://localhost:8443`, according to the owner.

This is local SSH TCP forwarding, not general IP routing between vmbr0 and vmbr1. It exposes the selected service through the SSH connection; it does not make all LAN hosts directly reachable from Windows. An explicit `127.0.0.1:8443` bind can constrain a future forwarding command to IPv4 loopback instead of relying on client defaults. The historical root login is not presented as a least-privilege administration design.

After administration, terminate the tunnel and remove the temporary host address from vmbr1, including any persistent network entry if one was added. **Removal is required housekeeping, not a completed action evidenced by this report.** No cleanup command was executed during this documentation update.

## Historical verification

| Check | Reported observation | Evidence status |
| --- | --- | --- |
| LAN/WAN bridge assignments | Mapped as above | Historical configuration report |
| VM 101 startup after tag removal | Succeeded | Owner report; original task log pending |
| GUI via localhost:8443 | Reached successfully | Owner report; original screenshot pending |
| VM 102 final deployment | Unconfirmed | Planned/configured during training |
| Temporary address removed | Not established | Cleanup evidence pending |

For future bridge changes, retain console access and a private backup before altering management connectivity. No live reconfiguration or new isolation tests were performed for this report.

Reference: [OpenSSH local forwarding options](https://man.openbsd.org/ssh#L).
