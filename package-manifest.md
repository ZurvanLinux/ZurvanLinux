# Zurvan Linux: Package Manifest & Software Manifest
**Version:** 1.0 (Phase 1)  
**Target OS Base:** Debian 13 (Trixie) `amd64`  
**Desktop Environment:** KDE Plasma 6.7  

This document details the curated list of pre-installed system packages, desktop environment components, multimedia libraries, and custom utilities included in the default ISO image of **Zurvan Linux**. These packages are configured to build via Debian’s `live-build` utility.

---

## 1. Core System & Base Utilities
These packages establish the underlying system framework, hardware recognition, and network management.

| Package Name | Function / Description |
|---|---|
| `xserver-xorg` | Core X11 display server (fallback) |
| `xwayland` | X11 compatibility layer for Wayland sessions |
| `network-manager` | Network connection management daemon |
| `user-setup` | Live-system user generation tool |
| `sudo` | Administrative privilege escalation utility |
| `eject` | CD/DVD/USB drive ejection utility |
| `locales` | System localization and language generation |

---

## 2. Display Manager & Login Interface
These components manage user authentication and the initial graphical login screen.

| Package Name | Function / Description |
|---|---|
| `sddm` | Simple Desktop Display Manager (graphical login) |
| `sddm-theme-breeze` | Default Breeze theme for SDDM (custom-skinned for Zurvan) |
| `plymouth` | Graphical boot animation framework |
| `plymouth-themes` | Boot-screen themes for Plymouth |

---

## 3. KDE Plasma 6.7 Desktop Environment
The core desktop environment packages, applets, and session managers.

| Package Name | Function / Description |
|---|---|
| `plasma-desktop` | Core KDE Plasma desktop shell |
| `plasma-workspace-wayland` | Wayland display server workspace session |
| `plasma-nm` | System tray applet for Network Manager |
| `plasma-pa` | System tray applet for PulseAudio/PipeWire volume control |
| `kscreen` | Display configuration and multi-monitor management |
| `powerdevil` | Power management daemon and UI configurations |
| `kde-style-breeze` | Default Breeze widget style and window decorations |
| `khotkeys` | Global keyboard shortcut manager |

---

## 4. Essential Desktop Applications
Native desktop utilities configured with optimized Persian layout settings.

| Package Name | Function / Description |
|---|---|
| `dolphin` | Highly customizable file manager |
| `konsole` | Advanced terminal emulator |
| `systemsettings` | KDE system configuration panel |
| `spectacle` | Screenshot and screen capture utility |
| `ark` | Archive compression and extraction manager |
| `kwrite` | Lightweight text editor |
| `kcalc` | Scientific graphical calculator |

---

## 5. Universal Multimedia Codecs & HW Acceleration
This subsystem ensures native, out-of-the-box decoding for almost all proprietary and open-source media formats.

| Package Name | Function / Description |
|---|---|
| `ffmpeg` | Core multimedia conversion and playback framework |
| `libavcodec-extra` | Patent-encumbered and extra audio/video codecs |
| `gstreamer1.0-libav` | FFmpeg-based GStreamer plugin (crucial for native players) |
| `gstreamer1.0-plugins-base` | Essential open-source GStreamer plugins |
| `gstreamer1.0-plugins-good` | High-quality open-source GStreamer plugins |
| `gstreamer1.0-plugins-bad` | Less common or unfinished GStreamer plugins |
| `gstreamer1.0-plugins-ugly` | Patent-restricted GStreamer plugins (e.g., MP3, DVD, AMR) |
| `gstreamer1.0-vaapi` | Hardware-accelerated video decoding via VA-API |
| `intel-media-va-driver` | Hardware acceleration driver for Intel HD/UHD graphics |
| `mesa-va-drivers` | Hardware acceleration drivers for AMD Radeon graphics |
| `vdpau-driver-all` | VDPAU drivers for various graphics chipsets |

---

## 6. Default Multimedia Players
Pre-configured multimedia software interfaces.

| Package Name | Function / Description |
|---|---|
| `haruna` | Modern KDE media player utilizing MPV as a backend |
| `vlc` | Universal, highly compatible fallback media player |
| `elisa` | Native KDE music player and library organizer |

---

## 7. Flatpak & Software Store Integration
This infrastructure integrates the Discover Software Center with the global Flathub database.

| Package Name | Function / Description |
|---|---|
| `flatpak` | Universal sandboxed package management runtime |
| `plasma-discover` | KDE graphical software center |
| `plasma-discover-backend-flatpak` | Flatpak integration backend for Discover |

---

## 8. Typography
Provides optimized rendering for Persian (Farsi), Arabic, and Latin text layouts.

| Package Name | Function / Description |
|---|---|
| `fonts-vazirmatn` | Default open-source Persian/Latin variable font stack |
| `fontconfig` | Font configuration and customization utility |

---

## 9. Custom Zurvan Utilities
Modular tools developed specifically to enhance the user experience in localized environments.

| Package Name | Function / Description |
|---|---|
| `zurvan-dns-bypass` | Modular DNS switcher package (allows easy toggle for Shecan, Radar, and default ISP DNS resolving) |

---

## 10. Installer Framework
The deployment engine used to copy the live environment to the user's local disk.

| Package Name | Function / Description |
|---|---|
| `calamares` | System independent installer framework |
| `calamares-settings-debian` | Debian-specific default modules for Calamares |
