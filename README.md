# MultiBoot Project

## Introduction
"MultiBoot" is a personal project born from my curiosity to explore alternative operating systems like Tails and Kali Linux. The goal is to create a bootable USB drive with multiple operating systems, usable on two different devices:
- **MacBook with an ARM64 chip** (ARM architecture).
- **PC with Windows 11** (x86_64 architecture).

The USB drive contains:
- **Kali Linux ARM**: for Macs with ARM64 chips.
- **Kali Linux x86_64**: for Macs with Intel chips and the PC with Windows.
- **Tails x86_64**: for Macs with Intel chips and the PC with Windows.

I used **Ventoy** to manage the multiboot setup, a tool that allows copying multiple ISO files onto a USB drive and selecting which one to boot from a menu at startup. This README documents the process, challenges encountered, and results. Thanks to the compatibility of Kali Linux and Tails with both architectures (ARM64 for newer Macs and x86_64 for Intel-based Macs), the project covers 100% of macOS devices.

## Tools and Requirements
- **Hardware**:
  - 64GB USB drive (USB 3.0 recommended for speed).
  - MacBook with an ARM64 chip.
  - PC with Windows 11.
- **Software**:
  - Ventoy (latest version downloaded from [ventoy.net](https://www.ventoy.net)).
  - ISO files:
    - `kali-linux-2024.x-arm64.iso` (for ARM64).
    - `kali-linux-2024.x-installer-amd64.iso` (for x86_64).
    - `tails-amd64-6.x.iso` (for x86_64).

## Steps

### 1. Preparing the USB Drive with Ventoy
1. **Downloading Ventoy**:
   - Downloaded `ventoy-1.x.x-windows.zip` from [ventoy.net](https://www.ventoy.net) on the PC with Windows.
   - Extracted the contents into a folder.
2. **Installing Ventoy**:
   - Connected the 64GB USB drive to the PC with Windows.
   - Opened `Ventoy2Disk.exe` and selected the USB drive.
   - In the options:
     - Chose **GPT** (GUID Partition Table) for UEFI compatibility.
     - Enabled **Secure Boot** to support modern systems.
   - Clicked "Install" and confirmed the formatting of the USB drive.
   - Result: Two partitions created (a small one for booting, a larger one for ISOs).

### 2. Downloading the ISO Files
- **Kali Linux ARM**:
  - Downloaded from [kali.org/get-kali](https://www.kali.org/get-kali/), "Kali ARM" section.
  - File: `kali-linux-2024.x-arm64.iso`.
  - Renamed to `kali-linux-arm64.iso`.
- **Kali Linux x86_64**:
  - Downloaded from [kali.org/get-kali](https://www.kali.org/get-kali/), "Installer" version.
  - File: `kali-linux-2024.x-installer-amd64.iso`.
  - Renamed to `kali-linux-x86_64.iso`.
- **Tails x86_64**:
  - Downloaded from [tails.net/install](https://tails.net/install/), ISO version (not IMG).
  - File: `tails-amd64-6.x.iso`.
  - Renamed to `tails-x86_64.iso`.

**Note**: Initially, I downloaded Tails as an `.img` file, but I switched to the ISO for better compatibility with Ventoy.

### 3. Copying the ISO Files to the USB Drive
1. **Issue with macOS**:
   - I copied the ISO files from the USB drive connected to the MacBook.
   - On Windows, I noticed hidden 4KB files (e.g., `._kali-linux-arm64.iso`) created by macOS as metadata.
2. **Solution**:
   - On the PC with Windows, revealed hidden files in File Explorer (View > Show hidden files).
   - Manually deleted the `._filename.iso` files.
   - Verified that only the original ISO files remained.
3. **Final Copy**:
   - Copied the three files to the main partition of the USB drive:
     - `kali-linux-arm64.iso`
     - `kali-linux-x86_64.iso`
     - `tails-x86_64.iso`

### 4. Testing on Devices
#### On the PC with Windows 11
1. Connected the USB drive.
2. Restarted the PC and pressed **F12**, **F2**, or **DEL** (depending on the model) to access the boot menu.
3. Selected the USB drive ("Ventoy").
4. In the Ventoy menu:
   - Booted `kali-linux-x86_64.iso`: works in Live mode.
   - Booted `tails-x86_64.iso`: starts successfully.
   - Ignored `kali-linux-arm64.iso` (not compatible with x86_64).

#### On the MacBook with an ARM64 Chip
1. Connected the USB drive.
2. Restarted the Mac while holding down the **Power button** or **Option (Alt)** key to access the boot menu.
3. Selected the USB drive ("EFI Boot").
4. In the Ventoy menu:
   - Booted `kali-linux-arm64.iso`: should work (to be tested).
   - Ignored `kali-linux-x86_64.iso` and `tails-x86_64.iso` (compatible only with Intel-based Macs).

**Note**: On Macs with Intel chips, `kali-linux-x86_64.iso` and `tails-x86_64.iso` would be bootable, ensuring full coverage for macOS devices.

## Expected Results
- **PC with Windows**:
  - Kali Linux x86_64: functional.
  - Tails: functional.
- **MacBook with ARM64**:
  - Kali Linux ARM: functional (to be confirmed).
  - Kali Linux x86_64 and Tails: not compatible (only for Intel-based Macs).
- **Mac with Intel**:
  - Kali Linux x86_64: functional.
  - Tails: functional.

## Issues and Solutions
1. **Hidden 4KB Files**:
   - **Cause**: Copying files from macOS to an exFAT USB drive.
   - **Solution**: Manually deleted from Windows.
   - **Prevention**: Copy files directly from the PC with Windows in the future.
2. **Secure Boot**:
   - If Kali or Tails fail to boot on the PC with Windows, disable Secure Boot in the BIOS.
3. **Compatibility with MacBook ARM64**:
   - If the USB drive doesn’t appear, reduce the security level in Settings > Startup Disk.
