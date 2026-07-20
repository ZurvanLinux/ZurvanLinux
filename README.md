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

**Phase 1 — specification only.** Documents are evolving; implementation begins once the spec set stabilizes. If prose in a document conflicts with what the codebase eventually does in another repo, trust the codebase but flag the divergence here.

## Licensing

All content in this repository is licensed under **[Creative Commons Attribution-ShareAlike 4.0 International](./LICENSE)** (CC-BY-SA-4.0).
