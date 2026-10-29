# Android-x86 9.0 Setup Notes

These notes summarise the supplied **WK1-PMx — Week 1 Extra Projects: How to Setup Android-x86 in VirtualBox** guide.

## Requirements from the guide

- VirtualBox installed and already used for the Kali Linux VM.
- At least 10 GB of free disk space.
- At least 2 GB of RAM available for the Android VM.
- Existing Kali Linux VM configured on a NAT Network with IP `10.0.0.2`.

## Network summary

| Setting | Value |
|---|---|
| Network type | VirtualBox NAT Network |
| Kali Linux | `10.0.0.2/24` |
| Android-x86 9.0 | `10.0.0.9/24` |
| Gateway | `10.0.0.1` |
| DNS | `8.8.8.8` |

## Setup sequence

1. Download Android-x86 9.0 from the [official project website](https://www.android-x86.org/) or its [linked SourceForge release directory](https://sourceforge.net/projects/android-x86/files/Release%209.0/).
2. Create a VirtualBox VM named `Android9-Lab`, using Linux / Other Linux (64-bit) for the 64-bit ISO, 2048 MB RAM, and a dynamically allocated VDI of at least 10 GB.
3. Attach the ISO in Storage settings. The guide recommends video memory of at least 64 MB and enabling 3D acceleration.
4. Boot the ISO and select the hard-disk installation option. Create or modify partitions, select ext4, install GRUB, allow the system to be writable, and reboot when installation finishes.
5. In VM Network settings, choose `NAT Network` and select the same network used by Kali Linux.
6. Configure Android with static IP `10.0.0.9`, subnet mask `255.255.255.0`, gateway `10.0.0.1`, and DNS `8.8.8.8`.
7. From Android, test `ping 10.0.0.2` and `ping 8.8.8.8`.
8. From Kali Linux, test `ping 10.0.0.9`.
9. Capture screenshots of the actual successful connectivity tests for project evidence.

## Notes

- Android-x86 menu paths can vary between builds.
- A terminal emulator may be needed if no terminal is included.
- Ensure the static address is not already in use.
- A ping failure is not always proof that all network access is unavailable; ICMP may be filtered.
- Keep screenshots authentic and avoid exposing unrelated personal or host information.
