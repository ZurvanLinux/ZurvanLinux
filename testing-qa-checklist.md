# Zurvan Linux: Testing & Quality Assurance (QA) Checklist
**Version:** 1.0 (Phase 1)  
**Target Platform:** 64-bit PC (`amd64`)  
**Base Distribution:** Debian 13 (Trixie)  
**Desktop Environment:** KDE Plasma 6.7  

This document serves as the standard operational checklist for testing and validating each build of the **Zurvan Linux** installation ISO image. All checks must be verified in both virtualized environments (e.g., VirtualBox, QEMU/KVM) and on physical hardware before a release is promoted to public status.

---

## 1. Boot & Live Environment Verification
These checks ensure the ISO image successfully boots and initiates the desktop environment on different hardware profiles.

*   [ ] **BIOS/Legacy Boot:** Verify that the live system boots successfully on older, non-UEFI motherboard configurations.
*   [ ] **UEFI Boot (Secure Boot Disabled):** Confirm standard UEFI boot functionality.
*   [ ] **UEFI Boot (Secure Boot Enabled):** Verify if the bootloader is correctly recognized when Secure Boot is active.
*   [ ] **Live Desktop Loading:** Confirm the KDE Plasma desktop loads completely without system service crashes or kernel panic warnings.
*   [ ] **System Integrity Check:** Check `/var/log/syslog` for any core system faults or failing services during the initial live session boot.

---

## 2. Graphical Installer (Calamares) Validation
These checks verify the reliability of the deployment engine during disk partitioning, user creation, and bootloader installation.

*   [ ] **Automatic Partitioning:** Test the "Erase Disk" option to verify that automated partition layout, filesystem creation, and mount points (including SWAP) are generated correctly.
*   [ ] **Manual Partitioning:** Test advanced manual partitioning schemes (e.g., separating `/home` and `/` or configuring dedicated EFI system partitions).
*   [ ] **Tehran Timezone Detection:** Verify Calamares detects or accurately suggests the default Tehran timezone (`Asia/Tehran`) based on system language/locale.
*   [ ] **User Creation & Privileges:** Verify that the primary user account is created with correct `sudo` privileges and administrative group memberships.
*   [ ] **Bootloader Installation:** Confirm that GRUB is successfully written to the correct partition (ESP for UEFI, or MBR for Legacy BIOS).
*   [ ] **Post-Installation Boot:** Verify the newly installed system boots successfully from the local hard drive after removing the live USB media.

---

## 3. UI/UX, Typography, and Localization Quality Checks
These checks validate the visual integration, font rendering, and bilingual input mechanics.

*   [ ] **Font Rendering (Vazirmatn):** Open Dolphin, Konsole, and System Settings to verify that the **Vazirmatn** font stack renders legibly without clipped characters or incorrect spacing.
*   [ ] **Monospace Font in Terminal:** Open Konsole and text editors to confirm that `Vazirmatn UI FD` is active and renders numerical displays and terminal characters correctly.
*   [ ] **RTL Workspace Mirroring:** Set the system language to Persian and verify that the global layout (panels, menus, calendar, window decorations) mirrors properly.
*   [ ] **Bilingual Input Toggling:** Verify that layout switching between English (US) and Persian (IR) is mapped to the standard shortcuts (`Alt+Shift` or `Super+Space`).
*   [ ] **Zero-Width Non-Joiner (ZWNJ):** Test typing in KWrite to ensure `Shift+Space` successfully inputs the non-joiner (`نیم‌فاصله`) without rendering extra spaces.
*   [ ] **Jalali Calendar Accuracy:** Click the system clock and confirm the Jalali (Solar Hijri) calendar dates, month names, and weekdays align accurately with the official Iranian calendar.

---

## 4. Hardware & Driver Compatibility
These checks ensure the distribution successfully supports network and multimedia hardware configurations out-of-the-box.

*   [ ] **Wired Networking:** Confirm automatic DHCP address assignment over Ethernet connection.
*   [ ] **Wireless Networking:** Test standard Wi-Fi adapters (Intel, Realtek, Atheros) to ensure the pre-installed firmware connects successfully to local access points.
*   [ ] **NVIDIA Driver Detection:** Run `nvidia-detect` to ensure the proprietary card detection utility executes correctly and displays the correct recommended driver package.
*   [ ] **Audio Output/Input:** Verify that PipeWire/PulseAudio recognizes the system soundcard, and test audio playback on both analog and HDMI channels.
*   [ ] **Hardware Video Acceleration (VA-API/VDPAU):** Play high-definition videos in **Haruna** and **VLC** while monitoring CPU usage to confirm GPU hardware decoding is active.

---

## 5. Software & Repository Integration
These checks confirm that custom utilities and the software backends are correctly integrated.

*   [ ] **KDE Discover Software Center:** Launch Discover and verify that the local APT cache is synchronized successfully.
*   [ ] **Flatpak & Flathub Connection:** Search for popular flatpak applications (e.g., Firefox, Discord) inside Discover to ensure Flathub is connected and functioning.
*   [ ] **Zurvan DNS Bypass (`zurvan-dns-bypass`):** Run the custom DNS switcher utility to verify successful toggling between Shecan, Radar, and default ISP DNS servers.
*   [ ] **GPG Key Validation:** Verify that no "unsigned repository" or "missing GPG key" warnings are thrown when executing `sudo apt update`.
