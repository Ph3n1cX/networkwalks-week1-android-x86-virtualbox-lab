# NETWORKWALKS — Week 1 Extra Project: Android-x86 Lab

A practical lab documenting the installation of **Android-x86 9.0 in Oracle VirtualBox**, connection to the same NAT Network as Kali Linux, static IPv4 configuration, and connectivity checks.

> **Program:** Cybersecurity at Networkwalks  
> **Week:** 01 — Extra Project (WK1-PMx)  
> **Author:** Faisol Daud  
> **GitHub:** [Ph3n1cX](https://github.com/Ph3n1cX)

---

## 📌 Project Overview

This extra project involved deploying Android-x86 9.0 as a virtual machine, connecting it to the existing Kali Linux lab network, configuring a static IP address, and testing communication between the two guest systems and the internet.

## 🎯 Objectives

- Download Android-x86 9.0 from the official project release source.
- Create and install an Android-x86 VM in VirtualBox.
- Connect Android and Kali Linux to the same VirtualBox NAT Network.
- Configure Android with a static IPv4 address.
- Test Android-to-Kali and Kali-to-Android connectivity.
- Check outbound internet connectivity from Android.
- Document the configuration and lessons learned.

## 🖥️ Lab Environment

| Component | Configuration |
|---|---|
| Hypervisor | Oracle VirtualBox |
| Android guest OS | Android-x86 9.0 |
| Existing lab VM | Kali Linux |
| Virtual network | VirtualBox NAT Network |
| Network subnet | `10.0.0.0/24` |
| Default gateway | `10.0.0.1` |
| DNS server | `8.8.8.8` |
| Android IP | `10.0.0.9/24` |
| Kali Linux IP | `10.0.0.2/24` |

Host operating system and exact VirtualBox version are not listed because they have not been confirmed.

## 🌐 Network Topology

```text
                         Internet
                            |
                   VirtualBox NAT Network
                      10.0.0.0/24
                            |
                 +----------+----------+
                 |                     |
             Kali Linux             Android-x86
             10.0.0.2/24            10.0.0.9/24
                 |                     |
                 +--- Bidirectional ---+
                     connectivity tests
```

Both VMs must be attached to the **same NAT Network**. VirtualBox's regular per-VM NAT adapter is different from a shared NAT Network.

## ⚙️ Implementation Steps

### 1. Download Android-x86

The supplied Networkwalks guide points to the official Android-x86 website and its linked SourceForge release directory. For a 64-bit VM, the guide specifies `android-x86_64-9.0-r2.iso`.

- [Android-x86 official website](https://www.android-x86.org/)
- [Android-x86 9.0 release files](https://sourceforge.net/projects/android-x86/files/Release%209.0/)

### 2. Create the VirtualBox VM

The supplied guide recommends these baseline settings:

| Setting | Value |
|---|---|
| VM name | `Android9-Lab` |
| Type | Linux |
| Version | Other Linux (64-bit), for a 64-bit ISO |
| RAM | 2048 MB |
| Virtual disk | VDI, dynamically allocated |
| Disk capacity | At least 10 GB |

### 3. Install Android-x86

Attach the ISO under **Settings → Storage**. The guide recommends at least 64 MB of video memory and enabling 3D acceleration. Boot the ISO and choose **Installation – Install Android-x86 to harddisk**. Create or modify the partition, select ext4, install GRUB, allow the system to be writable, and reboot after installation.

### 4. Connect to the NAT Network

Under **VirtualBox → VM Settings → Network**:

- Set **Attached to** to `NAT Network`.
- Select the same NAT Network used by Kali Linux.
- Restart the VM after applying the settings.

### 5. Configure Android's static IP

Open Android's network settings and locate the Ethernet or virtual network configuration. Menu paths can vary by Android-x86 build.

| Setting | Value |
|---|---|
| IPv4 address | `10.0.0.9` |
| Subnet mask | `255.255.255.0` |
| Gateway | `10.0.0.1` |
| DNS | `8.8.8.8` |

Confirm that `10.0.0.9` is not already in use on the lab subnet.

## 🔎 Connectivity Verification

The project update reports that connectivity was tested between Android and Kali Linux and from Android to the internet. The following commands document the checks.

### Android → Kali Linux

Run from an Android terminal or terminal emulator:

```sh
ping 10.0.0.2
```

### Android → Internet

```sh
ping 8.8.8.8
```

### Kali Linux → Android

Run from a Kali terminal:

```bash
ping 10.0.0.9
```

> **Evidence note:** Upload screenshots of the actual command output. Commands and expected results document the procedure; they do not replace evidence from the lab. A failed ping can also result from ICMP filtering.

## 📸 Lab Screenshots

The screenshots below are stored in the repository root and show evidence from the lab.

### 1. Android-x86 running in VirtualBox

![Android VM running in VirtualBox](01-virtualbox-android-vm.png)

### 2. Android static IP configuration

![Android network settings](02-android-network-settings.png)

### 3. Android ping to Kali Linux

![Android ping to Kali Linux at 10.0.0.2](03-android-ping-kali.png)

### 4. Android ping to the internet

![Android ping to 8.8.8.8](04-android-ping-internet.png)

### 5. Kali Linux ping to Android-x86

![Kali Linux ping to Android at 10.0.0.9](05-kali-ping-android.png)


## 🧰 Troubleshooting

| Problem | What to check |
|---|---|
| VMs cannot ping each other | Confirm both adapters use the same NAT Network rather than separate standard NAT adapters. |
| Android cannot reach the gateway | Check the IP, subnet mask, gateway, and VM network attachment. |
| Internet test fails | Check outbound connectivity and DNS; ICMP may be filtered. |
| Static IP fails | Confirm the address is not duplicated and the Android network interface is active. |
| No terminal app is available | Use an appropriate terminal emulator if available for the lab. |

## 💡 What I Learned

- How VirtualBox supports a non-standard guest OS such as Android-x86.
- Why guest VMs need the same NAT Network for direct guest-to-guest communication.
- How static IPv4 configuration uses an address, subnet mask, gateway, and DNS server.
- How to verify connectivity from both endpoints.
- How to distinguish guest-to-guest tests from outbound internet tests.
- The value of reproducible technical documentation and authentic evidence.

## 📚 References

- [Android-x86 official website](https://www.android-x86.org/)
- [Android-x86 9.0 release files — SourceForge](https://sourceforge.net/projects/android-x86/files/Release%209.0/)
- [Oracle VirtualBox](https://www.virtualbox.org/)
- [Networkwalks sample repository](https://github.com/waqaskarimccie/NETWORKWALKS-B082-WK1-PM1-CYBERSECURITY-LAB-SETUP-SAMPLE)

## 🙏 Acknowledgements

Thanks to **Sir Waqas Karim (CCIE)** and the **Networkwalks team** for the guidance and support.

## ⚠️ Disclaimer

This repository documents an educational virtual lab. Use lab systems responsibly and test only systems you own or are explicitly authorised to assess.
