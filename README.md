# Windows 11 Installation Guide

A comprehensive guide for clean Windows 11 installation and development environment setup.

## Table of Contents

1. [Bootable USB Creation](#bootable-usb-creation)
2. [Windows 11 Installation](#windows-11-installation)
3. [Windows 11 Setup](#windows-11-setup)
4. [Development Environment](#development-environment)

---

## Bootable USB Creation

### Download Windows 11 ISO

1. Download Windows 11 ISO from [Microsoft's official site](https://www.microsoft.com/software-download/windows11)
   - **Product Language**: `en-us`
   - **Verify ISO integrity** using PowerShell:
     ```powershell
     Get-FileHash path\to\windows11.iso
     ```

### Rufus Configuration

Use the following Rufus settings for optimal Windows experience:

![Rufus settings](https://github.com/DovLozys/win-install-guide/assets/755086/7b13c307-7127-4329-b55b-aae4448c97f9)

**Key Settings:**
- Partition scheme: GPT
- Target system: UEFI (non CSM)
- File system: FAT32
- Remove Windows 11 hardware requirements
- Disable data collection (Windows 11)
- Create local account with same name as this user's

---

## Windows 11 Installation

### Initial Setup

1. **Boot from USB** and change **Time and currency format** to `English (World)`
   - This disables the Microsoft Store and prevents installation of unnecessary apps

2. **Select Installation Type**
   - Choose **Windows edition** → **Custom: Install Windows only**
   - Delete all existing partitions
   - Install to **Unallocated Space**

3. **Post-Installation Boot Configuration**
   - After file copying completes, restart into BIOS
   - Verify boot order priority has the fresh Windows drive first

### OOBE (Out-of-Box Experience)

1. When encountering **OOBEREGION error**, skip it
2. Select **"I don't have internet"**
3. Choose **"Continue with limited setup"**
4. Complete installation

---

## Windows 11 Setup

### Initial System Configuration

#### Regional Settings
- **Region** → **Country or region** → `United Kingdom`
- **Regional format** → `United Kingdom`
- **Time zone** → `London`

#### System Settings
- **System** → **About** → **Rename this PC**

### Driver Installation

Install device drivers in the following order (restart as required):

1. **Chipset drivers**
2. **WiFi drivers**
3. **Bluetooth drivers**
4. **Integrated graphics drivers**
5. **Dedicated graphics drivers**
6. **Audio drivers**

> **Note**: If you encounter a PieExtension error during WiFi driver installation, copy the `.exe` file to the Extensions folder.

### System Optimization

1. **Enable internet connection**

2. **Run Chris Titus Tech Windows Utility**
   ```powershell
   # Run in Admin PowerShell
   irm "https://christitus.com/win" | iex
   ```
   - Navigate to **Tweaks** → **Standard** → **Run Tweaks**
   - Run **OOSU10** for additional privacy settings

3. **Update System**
   - Run Microsoft Store updates
   - Install all Windows Updates
   - Repeat until no more updates are available

### Essential Software

Download and install the following:
- **Microsoft Visual C++ Redistributable** (msvcredist)
- **DirectX Web Installer** (dxwebinstall)

---

## Development Environment

### WSL (Windows Subsystem for Linux)

#### Installation
```powershell
wsl --install
```

#### Git Configuration

1. **Generate SSH Key**
   ```bash
   ssh-keygen -t ed25519 -C "your-email@example.com"
   ```

2. **Export Public Key** (for GitHub authentication)
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```

3. **Configure Git**
   ```bash
   git config --global user.email "your-email@example.com"
   git config --global user.name "Your Name"
   git config --global commit.gpgsign true
   git config --global gpg.format ssh
   git config --global user.signingkey ~/.ssh/id_ed25519.pub
   ```

### Visual Studio Code

#### Essential Settings

Add the following to your `settings.json`:

```json
{
  "telemetry.telemetryLevel": "off",
  "window.restoreWindows": "none"
}
```

#### Required Extensions

- [Remote Development Extension Pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)

---

*Last updated: Check commit history for latest changes*
