# Zurvan Linux: Technical Specification & Architecture Document
**Version:** 1.0 (Phase 1)  
**Status:** Approved  
**Target Architecture:** 64-bit PC (`amd64`)  
**Base Distribution:** Debian Stable  

---

## 1. Project Overview
Zurvan Linux is an open-source, community-driven operating system designed for Persian-speaking users and developers. Named after *Zurvan*, the ancient Iranian deity of infinite time and stability, the distribution is built upon the rock-solid foundation of Debian Stable. 

The project aims to deliver a modern, visually compelling desktop environment utilizing **KDE Plasma (latest stable)**, featuring out-of-the-box hardware compatibility, robust Persian localization, seamless Flatpak integration, modular network-bypass tools tailored for developers in restricted network environments, and reproducible distribution/update tooling via GitHub Actions and Cloudflare.

---

## 2. Core System Architecture

### 2.1 Base System
*   **Upstream Base:** Debian Stable.
*   **CPU Architecture (Phase 1):** `amd64` (64-bit Intel/AMD PCs). *Note: `arm64` (AArch64) support is planned for Phase 2.*
*   **Init System:** `systemd` (default Debian configuration).
*   **Bootloader:** GRUB 2 with dual-boot (UEFI and Legacy BIOS) support.

### 2.2 Kernel & Driver Stack
*   **System Kernel:** Debian Stable default Linux kernel, with optional automated migration to the Debian Backports kernel for newer hardware enablement (HWE).
*   **Hardware Firmware:** The `contrib`, `non-free`, and `non-free-firmware` repository areas are enabled by default. The following firmware packages are pre-installed in the ISO:
  * `firmware-linux`, `firmware-linux-nonfree`
  * `firmware-iwlwifi` (Intel Wireless support)
  * `firmware-realtek`, `firmware-atheros`, `firmware-b43`, `firmware-brcm80211`
  * `linux-firmware` (common device firmware for network, GPU, and peripheral hardware)
*   **Graphics Stack:** 
    *   Mesa drivers for open-source Intel and AMD GPU acceleration.
    *   Integrated `nvidia-detect` utility to assist users in installing proprietary NVIDIA drivers.

---

## 3. Desktop Environment & UI/UX

### 3.1 Graphical Interface
*   **Desktop Environment:** KDE Plasma (latest stable) — Wayland session by default, with X11 fallback.
*   **Display Manager:** SDDM (Simple Desktop Display Manager) with a customized, branded dark theme.
*   **Window Manager:** KWin (configured with hardware-accelerated blur, desktop effects, and smooth transitions).

### 3.2 Typography & Localization
*   **Default System Font:** **Vazirmatn** (Open Font License) set as the default sans-serif font system-wide, including the desktop interface and web browsers.
*   **Monospace Font:** **Vazirmatn UI FD** (Farsi Digits version) for terminal emulation and coding environments.
*   **Language & Input:** 
    *   RTL (Right-to-Left) layout support natively optimized in the Plasma desktop settings.
    *   Pre-configured dual-language keyboard layouts: US English (`us`) and Standard Persian (`ir`) with standard shortcut keys (e.g., `Alt+Shift` or `Super+Space`) for layout toggling.

---

## 4. Package & Software Management

### 4.1 Native Package Manager (APT)
*   The primary package management relies on Debian's standard `apt` toolset.
*   Custom repository hosting for Zurvan-specific packages (hosted on GitHub Pages, proxied via Cloudflare).

### 4.2 Flatpak & Flathub Integration
*   `flatpak` runtime and the native `plasma-discover-backend-flatpak` are installed out-of-the-box.
*   The **Flathub** repository is pre-configured and enabled globally. Users can search, install, and update modern sandboxed applications directly from **KDE Discover**.

---

## 5. Multimedia & Graphics Support

### 5.1 Comprehensive Codec Integration
To ensure out-of-the-box playback for all common media formats without additional configuration, the following packages are pre-installed:
*   **System Frameworks:** `ffmpeg`, `libavcodec-extra`.
*   **GStreamer Plugins:** `gstreamer1.0-libav`, `gstreamer1.0-plugins-good`, `gstreamer1.0-plugins-bad`, `gstreamer1.0-plugins-ugly`.
*   **Hardware Acceleration:** `gstreamer1.0-vaapi`, `intel-media-va-driver`, `mesa-va-drivers`, `vdpau-driver-all`.

### 5.2 Default Applications
*   **File Manager:** Dolphin (KDE default).
*   **Video Player:** **Haruna** (modern, MPV-based GUI player with hardware acceleration) and **VLC** as a stable fallback.
*   **Audio Player:** Elisa (KDE music player).

---

## 6. Project Identity Package (`zurvan-base-files`)
A small project-built package layered into the live image to carry distributor
metadata used by GRUB and the installer:
- `/etc/os-release` distributor ID / name / version.
- GRUB distributor hook so the bootloader labels the entry "Zurvan Linux"
  instead of the upstream Debian string.

This package is built in CI by `iso-builder` and staged locally during image
assembly. It is not yet published to the custom APT repo.

---

## 7. Iranian Localization & Developer Utilities

### 6.1 Modular Network Bypass (`zurvan-dns-bypass`)
A custom, optional meta-package developed under the Zurvan project to mitigate access restrictions and sanctions on global developer tools (e.g., Docker Hub, Android SDK, Google Developers).
*   **Structure:** A lightweight script/utility that securely modifies DNS resolution settings.
*   **Configurations:** Toggles between:
    1.  *Sanction Bypass Mode:* Uses localized, trusted DNS servers (such as Shecan or Begazar).
    2.  *Gaming/Low-Latency Mode:* Uses Radar Game DNS configurations.
    3.  *Default Mode:* Automatically restores local ISP DNS or global public DNS (e.g., Cloudflare `1.1.1.1`).

---

## 8. Installation Framework

### 7.1 Graphical Installer
*   **Framework:** **Calamares Installer** (customized brand-matching styling).
*   **Local Configurations:** Automatically detects and suggests the Tehran timezone (`Asia/Tehran`) and configures RTL languages based on geolocation or user choice during step-by-step setup.
*   **Slideshow:** Customized presentation slides highlighting Zurvan Linux features, community forums, and guide pages.
