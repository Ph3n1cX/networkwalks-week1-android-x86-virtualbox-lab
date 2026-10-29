# Android-x86 VirtualBox Setup Notes

These notes are based on the three-page `WK1-PMx - Android VirtualBox Guide v1.pdf` provided for the Networkwalks Week 1 extra project. They summarize the prescribed setup, not a claim that every menu label is identical across Android-x86 builds.

## Requirements listed in the guide

- VirtualBox installed and already used for the Kali VM
- At least 10 GB free disk space
- At least 2 GB RAM available for the VM
- Existing Kali VM on a NAT Network at `10.0.0.2`

## Network summary

| Setting | Value |
|---|---|
| Network type | VirtualBox NAT Network |
| Kali Linux IP | `10.0.0.2/24` |
| Android 9.0 IP | `10.0.0.9/24` |
| Gateway | `10.0.0.1` |
| DNS | `8.8.8.8` |

## Procedure from the guide

1. Download the Android-x86 9.0 ISO from the official Android-x86 page or its linked SourceForge release directory.
2. Create a VirtualBox VM named `Android9-Lab`, using Linux / Other Linux (64-bit) for the 64-bit ISO, 2048 MB RAM, and a dynamically allocated VDI of at least 10 GB.
3. Attach the ISO. Set video memory to at least 64 MB and enable 3D acceleration as directed by the guide.
4. Boot the ISO and choose the hard-disk installation option. Create/modify partitions, use ext4, install GRUB, allow the system to be writable, and reboot after installation.
5. In VM network settings, choose `NAT Network` and select the same network as Kali.
6. In Android's Ethernet settings, configure static IP `10.0.0.9`, mask `255.255.255.0`, gateway `10.0.0.1`, DNS `8.8.8.8`.
7. Test from Android with `ping 10.0.0.2` and `ping 8.8.8.8`; test from Kali with `ping 10.0.0.9`.
8. Capture screenshots showing successful pings for submission.

## Official sources listed by the guide

- https://www.android-x86.org/
- https://sourceforge.net/projects/android-x86/files/Release%209.0/

## Notes

- Android-x86 menu paths can vary slightly by build.
- A terminal emulator may be needed if the installed image does not provide a terminal.
- Keep screenshots authentic to your own lab and avoid publishing sensitive host information.
