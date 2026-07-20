# Zurvan Linux: UI/UX & Localization Plan
**Version:** 1.0 (Phase 1)  
**Target Desktop Environment:** KDE Plasma 6.7  
**Language Focus:** Persian (Farsi) & English (Bilingual)  

---

## 1. Design Philosophy & UI/UX Goals
The design philosophy of **Zurvan Linux** is to combine the robustness of Debian with a modern, elegant, and Persian-centric visual experience. To compete directly with the aesthetic appeal of Ubuntu and Linux Mint, Zurvan Linux leverages the extensive customization capabilities of **KDE Plasma 6.7**.

The user interface is crafted to feel natural for Persian-speaking users through optimized Right-to-Left (RTL) mirroring, crisp typography, and unified system-wide branding, while maintaining a clean, familiar layout for global users.

---

## 2. Typography & Font Stack
Legibility is the foundation of a great desktop experience. Zurvan Linux replaces default fallback fonts with the open-source **Vazirmatn** font family, ensuring sharp, balanced rendering across all resolutions.

### 2.1 Font Specifications
*   **Default System Interface Font:** `Vazirmatn` (Regular, 10pt) — Used for menus, window titles, panels, and desktop widgets.
*   **Document & Reading Font:** `Vazirmatn` (Regular, 11pt) — Default for text editors, office suites, and system documentation.
*   **Monospace (Terminal) Font:** `Vazirmatn UI FD` (Fixed Digits, 10pt) — Tailored specifically for Konsole (the terminal emulator) and text editors to ensure Persian numbers and characters align with standard terminal grid layouts.

### 2.2 Fontconfig Implementation
To enforce this typography globally (including in web browsers like Firefox/Chrome and GTK applications), a custom fontconfig XML (`50-zurvan-fonts.conf`) is deployed in the `/etc/fonts/local.conf` system path.

---

## 3. Right-to-Left (RTL) Layout Strategy
KDE Plasma 6.7 provides robust native support for RTL rendering. Zurvan Linux configures locale settings to automatically mirror the workspace when the Persian language is selected.

*   **Taskbar & Panels:** When Farsi is active, the panel mirrors automatically: the Application Menu (Start Menu) aligns to the bottom-right corner, and the System Tray (clock, network, volume) moves to the bottom-left.
*   **Window Decorations:** Window title text aligns to the right side of the title bar, and window control buttons (Close, Maximize, Minimize) adapt to standard RTL patterns.
*   **Application Mirroring:** Native Qt and KDE applications dynamically adapt their layouts to RTL structure without breaking graphical components.

---

## 4. Keyboard Layouts & Input Configuration
A seamless bilingual typing experience is vital for Persian developers and users. Zurvan Linux configures standard input parameters during build time.

*   **Keyboard Layouts:**
    1.  **US English (`us`):** Default layout.
    2.  **Persian (`ir`):** Configured according to the **ISIRI 9147** national standard, ensuring standard placement of Persian characters and easy access to the Zero-Width Non-Joiner (ZWNJ / نیم‌فاصله) via `Shift+Space`.
*   **Layout Toggling Shortcut:** Pre-configured globally to use `Alt+Shift` (standard for many users migrating from Windows/macOS) or `Super+Space` as an alternative.
*   **Visual Indicator:** A clean keyboard layout flags widget is added to the system tray for easy switching and status viewing.

---

## 5. Regional Settings, Date & Calendar
*   **System Timezone:** Defaulted to `Asia/Tehran` for local users, with automatic Network Time Protocol (NTP) synchronization enabled.
*   **Jalali (Solar Hijri) Calendar:** Integrated natively into the Plasma clock/calendar applet. Zurvan Linux configures regional locale formats so the digital clock can display Persian calendar dates, weekdays, and times natively.

---

## 6. Branding & Aesthetic Customization (The Visual Identity)
To compete with leading distributions, Zurvan Linux establishes a consistent, professional visual identity across all stages of user interaction.

### 6.1 Plymouth Boot Splash Screen
*   **Description:** A clean, dark boot animation that hides standard kernel log text.
*   **Design:** Features a central, glowing **Zurvan Linux logo** with a minimal loading animation beneath it, replacing the default Debian spiral logo.

### 6.2 SDDM Login Screen
*   **Theme:** A customized variant of the Breeze SDDM theme.
*   **Layout:** A centered login form with a blurred background of the active system desktop wallpaper, sharp Vazirmatn typography, and prominent Zurvan branding.

### 6.3 Global Workspace Theme (Zurvan Dark & Light)
*   **Primary Accent Color:** A custom color scheme featuring deep slate greys as the background, paired with a vibrant, glowing **Teal/Aqua** accent color (to symbolize the cosmic, time-themed identity of "Zurvan").
*   **Widget Style:** Rounded corners on active windows, with clean, subtle drop-shadows and Wayland-powered translucent blur effects (where supported by the graphics hardware).
*   **Icon Theme:** **Papirus-Dark** customized with Zurvan-colored folders, ensuring modern, flat, vector-based icons for all applications.

### 6.4 Wallpaper Collection
*   The default desktop wallpaper features a custom abstract design representing "infinite time" and cosmic geometry, utilizing the Teal/Dark Slate color palette.
*   A pre-installed collection of alternative high-resolution wallpapers is included, highlighting Iranian architecture, historical landmarks, geometric Islamic tile-art, and Iranian landscapes.
