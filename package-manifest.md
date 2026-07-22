# Zurvan Linux: Package Manifest & Software Manifest
**Version:** 1.0 (Phase 1)  
**Target OS Base:** Debian Stable `amd64`  
**Desktop Environment:** KDE Plasma (latest stable)

**Debian Stable / Plasma 6 substitutions** (from `iso-builder`):
- `plasma-workspace-wayland` → folded into `plasma-workspace` in Plasma 6.
- `khotkeys` → removed in Plasma 6; global shortcuts now use KDE's built-in accel.
- `spectacle` → renamed to `kde-spectacle` in current Debian Stable.
- `fonts-vazirmatn` "Vazirmatn UI FD" monospace → **divergence:** Debian package ships only proportional Vazirmatn; monospace variant deferred to Phase 2 (`branding-assets` M2.1).
- `zurvan-dns-bypass` → **divergence:** custom Phase 2 package; commented in live-build until built and published.

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

## 2. Command Line Utilities
Essential terminal-based tools for scripting, administration, troubleshooting, and developer workflows.

| Package Name | Function / Description |
|---|---|
| `git` | Distributed version control system |
| `curl` | Command-line data transfer tool |
| `wget` | Non-interactive network downloader |
| `htop` | Interactive process viewer |
| `btop` | Modern process viewer with graphs and system overview |
| `tree` | Directory tree display |
| `fastfetch` | Fast system information display tool |
| `vim` | Powerful terminal text editor |
| `nano` | Lightweight terminal text editor |
| `rsync` | Fast incremental file transfer and synchronization |
| `zip` | Zip archive creation tool |
| `unzip` | Zip archive extraction tool |
| `ca-certificates` | HTTPS trust store for TLS connections |
| `gnupg` | Encryption, signing, and APT repo verification |
| `openssh-client` | SSH client for secure remote access |
| `ksshaskpass` | KDE SSH password prompt for GUI passphrase entry |
| `tzdata` | Timezone data for correct system time |
| `man-db` | Manual pages and documentation viewer |
| `net-tools` | Legacy networking tools including ifconfig and netstat |
| `iproute2` | Modern networking utilities including ip, ss, and tc |
| `iw` | Wireless configuration and diagnostics tool |
| `ufw` | Uncomplicated firewall configuration tool |
| `udisks2` | Disk service for mounting and ejection from CLI |
| `smartmontools` | SMART disk health monitoring and diagnostics |
| `parted` | Partition manipulation from the command line |
| `iotop` | I/O usage monitor per process |
| `ncdu` | Interactive disk usage analyzer |
| `bat` | Syntax-highlighting `cat` replacement; installed binary is `batcat` on Debian due to name conflict |

---

## 3. Shell & Terminal Productivity
Shell configuration, autocomplete, fuzzy finding, and prompt enhancements for interactive terminal use.

| Package Name | Function / Description |
|---|---|
| `bash-completion` | Tab completion for common CLI tools in bash |
| `zsh` | Advanced shell with improved scripting and interactive features |
| `zsh-autosuggestions` | Inline history suggestions as you type in zsh |
| `zsh-syntax-highlighting` | Real-time syntax highlighting for the command line |
| `fzf` | Interactive fuzzy finder for history, files, and processes |
| `zoxide` | Smart cd replacement (*requires debian-backports; optionally installed via post-install script*) |
| `starship` | Cross-shell prompt (*installed via upstream installer script; not in Debian Stable main archive*) |
| `unicode` | Command-line Unicode character lookup (*installed via upstream installer; not packaged for Debian Stable*) |

---

## 4. Display Manager & Login Interface
These components manage user authentication and the initial graphical login screen.

| Package Name | Function / Description |
|---|---|
| `sddm` | Simple Desktop Display Manager (graphical login) |
| `sddm-theme-breeze` | Default Breeze theme for SDDM (custom-skinned for Zurvan) |
| `plymouth` | Graphical boot animation framework |
| `plymouth-themes` | Boot-screen themes for Plymouth |

---

## 5. KDE Plasma Desktop Environment
The core desktop environment packages, applets, and session managers.

| Package Name | Function / Description |
|---|---|
| `plasma-desktop` | Core KDE Plasma desktop shell |
| `plasma-workspace` | Workspace shell and Wayland session provider |
| `plasma-nm` | System tray applet for Network Manager |
| `plasma-pa` | System tray applet for PulseAudio/PipeWire volume control |
| `kscreen` | Display configuration and multi-monitor management |
| `powerdevil` | Power management daemon and UI configurations |
| `kde-style-breeze` | Default Breeze widget style and window decorations |
| `bluedevil` | KDE Bluetooth device manager and integration |
| `kde-inotify-survey` | Warns when apps are using all inotify watches and prompts the user to raise it |
| `bluedevil` | KDE Bluetooth device manager and integration |
| `kde-inotify-survey` | Warns when apps are using all inotify watches and prompts the user to raise it |

---

## 6. Essential Desktop Applications
Native desktop utilities configured with optimized Persian layout settings.

| Package Name | Function / Description |
|---|---|
| `dolphin` | Highly customizable file manager |
| `konsole` | Advanced terminal emulator |
| `systemsettings` | KDE system configuration panel |
| `kde-spectacle` | Screenshot and screen capture utility |
| `ark` | Archive compression and extraction manager |
| `kwrite` | Lightweight text editor |
| `kcalc` | Scientific graphical calculator |
| `firefox` | Latest Firefox via Flathub (`org.mozilla.Firefox`) |
| `thunderbird` | Latest Thunderbird via Flathub (`org.mozilla.Thunderbird`) |
| `libreoffice` | Latest LibreOffice via Flathub (`org.libreoffice.LibreOffice`) |
| `khelpcenter` | KDE application handbooks and offline documentation |
| `kdeconnect-kde` | Remote mobile phone control and integration |
| `gparted` | Graphical partition editor for disk management |
| `okular` | KDE-native PDF, EPUB, and DjVu viewer with annotation support |

---

## 7. KDE Integration & Productivity Add-ons
Add-ons, extensions, and tools that improve the completeness of the Plasma desktop session.

| Package Name | Function / Description |
|---|---|
| `ffmpegthumbs` | Video thumbnailing plugin for Dolphin and Gwenview |
| `kimageformats` | AVIF, JXL, and other image format preview support |
| `kio-extras` | Thumbnailing engine and KIO protocol support for remote and special file access |
| `xdg-desktop-portal-gtk` | GTK app integration with KDE portals for file picker and screenshots |
| `xsettingsd` | GTK theme sync and HiDPI scaling for GTK apps without restart |
| `qt-imageformats` | WebP and other image format support in Qt applications |
| `unrar` | RAR archive extraction support for Ark |

---

## 8. Hardware Support & System Services
Hardware detection, firmware, input, and peripheral support packages.

| Package Name | Function / Description |
|---|---|
| `firmware-iwlwifi` | Intel WiFi firmware |
| `firmware-realtek` | Realtek WiFi and Ethernet firmware |
| `firmware-atheros` | Atheros WiFi firmware |
| `firmware-b43` | Broadcom B43 wireless firmware |
| `firmware-brcm80211` | Broadcom 802.11 wireless firmware |
| `upower` | Power management and battery monitoring service |
| `bluez` | Bluetooth protocol stack and system service |
| `fprintd` | Fingerprint authentication with PAM integration |
| `fwupd` | Firmware updating via Discover |
| `geoclue` | Location services for Night Color and geo-aware features |
| `iio-sensor-proxy` | Allows automatic screen rotation on Wayland for tablets and 2-in-1s |
| `power-profiles-daemon` | Enables power profile switching in the Plasma UI |
| `switcheroo-control` | Provides proper hybrid and multi-GPU detection |
| `system-config-printer-applet` | Notifier for directly connected printers requiring specific drivers |
| `system-config-printer-dbus-service` | Enables printer device discovery and recommended driver selection |
| `thermald` | Better thermal management and performance on recent Intel CPUs |
| `xserver-xorg-input-libinput` | Default input driver for touchpad, mouse, and tablet devices |
| `pipewire` | Modern audio server replacing PulseAudio |
| `wireplumber` | PipeWire session manager |
| `alsa-utils` | ALSA sound card configuration utilities |
| `linux-firmware` | Common device firmware for network, GPU, and peripheral hardware |
| `intel-microcode` | Intel CPU microcode updates for stability and security |
| `amd-microcode` | AMD CPU microcode updates for stability and security |
| `libwacom` | Wacom and graphics tablet device identification library |
| `xserver-xorg-input-wacom` | Wacom and tablet input driver for Xorg/Xwayland |
| `acpi` | ACPI battery, AC, and thermal state reporting |
| `lm-sensors` | Hardware sensor and fan speed monitoring |
| `usbutils` | USB device listing and diagnostics |
| `pciutils` | PCI device listing and diagnostics |
| `mesa-vulkan-drivers` | Vulkan driver support for AMD and Intel GPUs |
| `nvidia-detect` | Recommends the appropriate NVIDIA proprietary driver package |

**Optional vendor-specific packages:**
- `i8kutils` — Dell laptop fan control, BIOS info, and hotkeys
- `thinkpad-acpi-dkms` — ThinkPad ACPI driver for battery thresholds and hotkeys
- `tp-smapi-dkms` — ThinkPad SMAPI driver for battery and HDAPS support

---

## 9. File System Support
Filesystem drivers and tools for reading and writing non-Linux filesystems on removable media and shared partitions.

| Package Name | Function / Description |
|---|---|
| `ntfs-3g` | Read and write NTFS filesystem support |
| `exfatprogs` | exFAT filesystem creation and repair utilities |
| `dosfstools` | FAT and VFAT filesystem utilities |
| `btrfs-progs` | Btrfs filesystem utilities |
| `xfsprogs` | XFS filesystem utilities |

---

## 10. Universal Multimedia Codecs & HW Acceleration
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

## 11. Default Multimedia Players
Pre-configured multimedia software interfaces.

| Package Name | Function / Description |
|---|---|
| `haruna` | Modern KDE media player utilizing MPV as a backend |
| `vlc` | Latest VLC via Flathub (`org.videolan.VLC`) |
| `elisa` | Native KDE music player and library organizer |

---

## 12. Flatpak & Software Store Integration
This infrastructure integrates the Discover Software Center with the global Flathub database.
**Note:** Apps listed here as "via Flathub" are available on-demand through Discover; they are not pre-installed in the live ISO build tree unless explicitly listed elsewhere for apt-based installation.

| Package Name | Function / Description |
|---|---|
| `flatpak` | Universal sandboxed package management runtime |
| `plasma-discover` | KDE graphical software center |
| `plasma-discover-backend-flatpak` | Flatpak integration backend for Discover |


---

## 13. Typography
Provides optimized rendering for Persian (Farsi), Arabic, and Latin text layouts.

| Package Name | Function / Description |
|---|---|
| `fonts-vazirmatn` | Default open-source Persian/Latin variable font stack |
| `fontconfig` | Font configuration and customization utility |
| `noto-color-emoji` | Color emoji font support |
| `fonts-unifont` | Comprehensive fallback font covering a broad Unicode range |

**Divergence from earlier spec drafts:** The spec also calls for "Vazirmatn UI FD" (Farsi-Digits monospace) for terminal/editor use. On current Debian Stable, `fonts-vazirmatn` ships only the proportional family; forcing it into `monospace` would break terminal grid alignment. Monospace is therefore left at the system default, and the Vazirmatn UI FD variant is deferred to Phase 2 (`branding-assets` M2.1).

---

## 14. Custom Zurvan Utilities
Modular tools developed specifically to enhance the user experience in localized environments.

| Package Name | Function / Description |
|---|---|
| `zurvan-base-files` | Project identity package (release version, distributor strings, branding metadata). |
| `zurvan-dns-bypass` | Modular DNS switcher package (allows easy toggle for Shecan, Radar, and default ISP DNS resolving). |

**Phase note:** `zurvan-dns-bypass` is a custom package built in Phase 2 and published to the Zurvan APT repo. It is not available in the M1.x baseline and is commented in the live-build package list until M2.2 lands it in `repo.zurvanlinux.org`.

---

## 15. Installer Framework
The deployment engine used to copy the live environment to the user's local disk.

| Package Name | Function / Description |
|---|---|
| `calamares` | System independent installer framework |
| `calamares-settings-debian` | Debian-specific default modules for Calamares |

(End of file)
