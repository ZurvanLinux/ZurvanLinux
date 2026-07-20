# AGENTS.md — Zurvan Linux

Guidance for AI agents (Kilo, Claude Code, Copilot, etc.) working in this repo.

## Project status: spec-only (Phase 1)

This repository currently contains **only specification/planning documents**. There is no source code, no `live-build` config tree, no scripts, no `Makefile`, no CI, and **no git history**. Do not assume any of these exist — do not invent paths, build commands, or test runners. If asked to implement something, create the structure described in the spec docs rather than guessing from defaults.

## Authoritative documents

The five root-level `.md` files are the source of truth for scope and behavior. Read them before any work:

- `technical-spec-architecture.md` — system architecture, kernel/driver stack, desktop environment, Calamares installer.
- `package-manifest.md` — exact pre-installed package list (apt + flatpak + codecs + fonts + custom utils).
- `ui-ux-localization-plan.md` — Vazirmatn typography, RTL layout, Persian keyboard (ISIRI 9147), branding.
- `distribution-update-strategy.md` — ISO delivery (Cloudflare R2 + Cloudflare; GitHub Releases holds notes + SHA256), custom APT repo, GPG signing.
- `testing-qa-checklist.md` — release-validation checklist (boot, installer, localization, hardware, repos).

If prose in a doc conflicts with what the codebase eventually does, trust the codebase — but flag the divergence.

## Toolchain (when implementation begins)

- **ISO build:** Debian `live-build` (explicitly stated in `package-manifest.md`). The eventual tree will be `auto/`, `config/` (package-lists, hooks, includes.chroot), built with `lb build` on a Debian Stable host.
- **Custom APT repo:** hosted on GitHub Pages at `repo.zurvanlinux.org`, proxied via Cloudflare, GPG-signed with a 4096-bit key. Public key at `/public.key`, registered on installed systems at `/etc/apt/keyrings/zurvan-archive-keyring.gpg`.
- **Installer:** Calamares with Debian settings modules + custom Zurvan branding.

## Hard constraints from the spec

Do not deviate from these without explicit approval — they are core product decisions, not implementation details:

- **Base:** Debian Stable. **Phase 1 arch: `amd64` only.** `arm64` is explicitly deferred to Phase 2.
- **Desktop:** KDE Plasma (latest stable), **Wayland by default with X11 fallback** (not the reverse).
- **Repositories enabled by default:** `contrib`, `non-free`, and `non-free-firmware` (firmware-iwlwifi, firmware-realtek, firmware-atheros, etc. must be pre-installed).
- **Fonts:** `fonts-vazirmatn` is the system-wide default; `Vazirmatn UI FD` (Farsi Digits) for Konsole/editors. Enforced via a custom fontconfig at `/etc/fonts/local.conf`.
- **Input:** Persian layout per **ISIRI 9147**; ZWNJ on `Shift+Space`; layout toggle `Alt+Shift` / `Super+Space`; layouts `us` + `ir`.
- **Locale/region:** Default timezone `Asia/Tehran`, Jalali (Solar Hijri) calendar in the clock applet, RTL mirroring when Persian is active.
- **Bootloader:** GRUB 2, supporting both UEFI (incl. Secure Boot) and Legacy BIOS.
- **Init:** `systemd` (Debian default config).

## Custom in-house components

- `zurvan-dns-bypass` — modular DNS switcher (Shecan / Radar / default ISP). Built and shipped via the custom APT repo.
- Branding assets: Plymouth splash, custom SDDM Breeze variant, "Zurvan Dark/Light" color scheme (teal accent on dark slate), Papirus-Dark icons with Zurvan-colored folders.

## Verification & release

Per `testing-qa-checklist.md`, every build must pass checks in **both** VMs (VirtualBox, QEMU/KVM) and on physical hardware, covering: BIOS/UEFI/Secure-Boot boot, Calamares partitioning (auto + manual), Tehran-timezone detection, Vazirmatn/RTL/ZWNJ rendering, VA-API/VDPAU decoding, NVIDIA detection, Flathub in Discover, and clean `apt update` (no GPG warnings). Treat that doc as the release gate.

## Conventions to follow

- Keep documents bilingual-aware: Persian terminology may appear (e.g. نیم‌فاصله = ZWNJ). Preserve it when editing.
- New spec decisions belong in the relevant `.md` file, not in commit messages or scattered notes.
- This project targets users in restricted-network regions (Iran) — DNS-bypass, local-mirror selection, and Flathub availability are intentional features, not bugs to "fix."
