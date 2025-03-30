# MultiBoot-USB

**MultiBoot USB** is a 31 GB USB drive configured to boot three operating systems: **Kali Linux (ARM64)**, **Kali Linux (x86_64)**, and **Tails (x86_64)**. This project is designed for users who want a portable multi-boot device compatible with both ARM architectures and x86_64 architectures, requiring no additional hardware beyond the USB drive itself. The setup uses **rEFInd** as the bootloader to manage the systems.

## Description
This USB drive was designed for:
- **Kali Linux (ARM64)**: For penetration testing on ARM devices, such as the MacBook M3.
- **Kali Linux (x86_64)**: For penetration testing on x86_64 PCs, such as a Lenovo with Windows 11.
- **Tails (x86_64)**: For privacy and anonymity on x86_64 hardware.
The project avoids using Ventoy, opting instead for dedicated, physically installed partitions managed by rEFInd.

## Requirements
- **Hardware**:
  - 31 GB USB drive (or larger).
  - MacBook M3 (to configure and install Kali ARM64).
  - PC with Windows 11 (e.g., Lenovo) to install Kali x86_64 and Tails.

## USB Drive Structure
| Partition | Name            | Size       | Filesystem | Content           |
|-----------|-----------------|------------|------------|-------------------|
| disk4s1   | EFI             | 209.7 MB   | FAT32      | Bootloader (rEFInd) |
| disk4s2   | Kali_ARM64      | 10 GB      | ext4       | Kali Linux ARM64  |
| disk4s3   | Kali_x86        | 10 GB      | ext4       | Kali Linux x86_64 |
| disk4s4   | Tails_x86       | 10 GB      | ext4/raw   | Tails x86_64      |
