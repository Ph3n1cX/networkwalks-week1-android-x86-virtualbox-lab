# Networkwalks Week 1 — Android-x86 VirtualBox Lab

A practical lab running Android-x86 9.0 alongside Kali Linux in VirtualBox, using a shared NAT Network and static IPv4 addressing.

**Author:** Faisol Daud  
**Program:** Networkwalks Cybersecurity — Week 1 Extra Project

## Lab Setup

| Component | Configuration |
|---|---|
| Hypervisor | Oracle VirtualBox |
| Android guest | Android-x86 9.0 — `10.0.0.9/24` |
| Kali Linux guest | `10.0.0.2/24` |
| Network | VirtualBox NAT Network |
| Gateway | `10.0.0.1` |
| DNS | `8.8.8.8` |

Both VMs are attached to the same NAT Network so they can communicate with each other and access the internet.

## Network Topology

```text
              Internet
                 |
       VirtualBox NAT Network
            10.0.0.0/24
             /        \
        Kali Linux   Android-x86
        10.0.0.2     10.0.0.9
```

## Connectivity Tests

The lab included connectivity checks in both directions and an outbound internet check.

| Test | Command | Purpose |
|---|---|---|
| Android → Kali | `ping 10.0.0.2` | Verify guest-to-guest connectivity |
| Kali → Android | `ping 10.0.0.9` | Verify connectivity in the reverse direction |
| Android → Internet | `ping 8.8.8.8` | Check outbound IP connectivity |

## Screenshots

### Android VM in VirtualBox
![Android-x86 VM running in VirtualBox](01-virtualbox-android-vm.png)

### Android network configuration
![Android static IP settings](02-android-network-settings.png)

### Android ping to Kali Linux
![Android ping to Kali Linux](03-android-ping-kali.png)

### Android internet connectivity test
![Android ping to 8.8.8.8](04-android-ping-internet.png)

### Kali ping to Android-x86
![Kali Linux ping to Android-x86](05-kali-ping-android.png)

## Key Takeaways

- Configured Android-x86 as a VirtualBox guest.
- Connected two guest VMs through a shared NAT Network.
- Applied static IPv4 network settings.
- Tested connectivity between guests and to an external IP address.

## Setup Notes

See [Android-x86 Setup Notes](docs/android-x86-setup-notes.md) for the installation steps and configuration details.

## References

- [Android-x86](https://www.android-x86.org/)
- [Android-x86 9.0 releases](https://sourceforge.net/projects/android-x86/files/Release%209.0/)
- [Oracle VirtualBox](https://www.virtualbox.org/)
- [Networkwalks sample lab repository](https://github.com/waqaskarimccie/NETWORKWALKS-B082-WK1-PM1-CYBERSECURITY-LAB-SETUP-SAMPLE)

Thanks to Sir Waqas Karim (CCIE) and the Networkwalks team for their guidance.
