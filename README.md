# Zurvan Linux — Specification & Architecture

> Authoritative specification documents for the Zurvan Linux distribution.

This repository holds the **source-of-truth specification** for Zurvan Linux — a Debian Stable–based, Persian-first desktop distribution running KDE Plasma (latest stable) on Wayland. No source code, build artifacts, or packages live here; this is the planning and design home that all other repositories in the [`ZurvanLinux`](https://github.com/ZurvanLinux) org implement against.

## Documents

| Document | Scope |
|----------|-------|
| [`technical-spec-architecture.md`](./technical-spec-architecture.md) | System architecture: kernel/driver stack, desktop environment, Calamares installer, bootloader, init |
| [`package-manifest.md`](./package-manifest.md) | Exact pre-installed package list (apt + flatpak + codecs + fonts + custom utils) |
| [`ui-ux-localization-plan.md`](./ui-ux-localization-plan.md) | Vazirmatn typography, RTL layout, Persian keyboard (ISIRI 9147), branding |
| [`distribution-update-strategy.md`](./distribution-update-strategy.md) | ISO delivery (GitHub Releases + Cloudflare), custom APT repo, GPG signing |
| [`testing-qa-checklist.md`](./testing-qa-checklist.md) | Release-validation checklist (boot, installer, localization, hardware, repos) |
| [`AGENTS.md`](./AGENTS.md) | Working agreement for AI agents editing this repository |

## Status

**M1.1b — ISO build pipeline live.** The `iso-builder` repo has a complete `live-build` + GitHub Actions pipeline producing a KDE Plasma baseline on Debian Stable. Pre-releases are tagged `v0.2.0-pre.N`.

**M1.2 — APT repo publish pipeline live.** The `apt-repository` repo publishes signed indices to GitHub Pages at `https://repo.zurvanlinux.org`.

**M1.3 — Website deployed.** The `website` repo is deployed to GitHub Pages at `https://zurvanlinux.org`.

**Remaining P0 prerequisites (blocking first stable release):**
- Cloudflare R2 bucket + `download.zurvanlinux.org` custom-domain binding.
- GitHub Actions secrets for R2 upload.
- Cloudflare HTTPS enforcement for `zurvanlinux.org`.
- QA boot-test gate: QEMU/KVM + VirtualBox (BIOS + UEFI).

Documents still contain a small number of flagged divergences where the current
Debian Stable package set does not match the original spec assumptions. Those are
documented inline in `package-manifest.md`.

## Licensing

All content in this repository is licensed under **[Creative Commons Attribution-ShareAlike 4.0 International](./LICENSE)** (CC-BY-SA-4.0).
