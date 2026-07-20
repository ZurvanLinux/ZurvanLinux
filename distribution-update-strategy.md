# Zurvan Linux: Distribution & Update Strategy
**Version:** 1.0 (Phase 1)  
**Infrastructure Base:** GitHub & Cloudflare  
**Target OS Base:** Debian Stable `amd64`  

---

## 1. ISO Image Distribution Strategy
Because of the large size of Linux installation ISOs (typically 2GB–3.5GB), traditional web hosting is not cost-effective. Zurvan Linux implements a hybrid distribution model utilizing **Cloudflare R2** (ISO storage), **GitHub Releases** (release notes + checksums), and **Cloudflare** (delivery) for optimized, zero-cost delivery.

### 1.1 Infrastructure Configuration
*   **Storage Host (ISO binary):** A public **Cloudflare R2** bucket under the Zurvan Linux Cloudflare account. R2 provides **zero-egress** object storage (downloads cost nothing, which matters for users on restricted/limited networks) and has **no per-file size cap**. This replaces an earlier plan to use GitHub Releases for the ISO itself — GitHub caps a single release asset at **2 GB**, which a full KDE ISO exceeds.
*   **Release metadata:** **GitHub Releases** holds the per-version release notes and the `SHA256SUMS` file, and its body links to the R2 download URL. It is *not* used for the ISO binary.
*   **Routing & Delivery:** A dedicated subdomain (`download.zurvanlinux.org`) is bound to the R2 bucket as a **Cloudflare custom domain**; Cloudflare serves the object directly (HTTP range + resumable downloads).
*   **Cloudflare Configuration:** Cloudflare's free tier limits cached files to 512 MB, so ISO binaries (>512 MB) are **not** edge-cached — they stream from the R2 origin on each request. Because R2 egress is free, this incurs no cost. The download page and small metadata are cached at the edge as usual.

---

## 2. Custom APT Package Repository Architecture
For custom packages developed specifically for Zurvan Linux (such as `zurvan-dns-bypass`, visual assets, and configuration tweaks), a custom APT repository is hosted directly on GitHub Pages.

```
                           ┌───► Cloudflare R2 (Hosts raw system ISO files; zero-egress)
                           │
User ───► Cloudflare ─────┼───► GitHub Releases (Release notes + SHA256SUMS; links to R2)
                           │
                           ├───► GitHub Pages (Hosts custom APT repo - deb files & indices)
                           │
                           └───► GitHub Pages (Hosts static project landing page)
```

### 2.1 Repository Hosting Configuration
*   **Host Platform:** GitHub Pages (configured as a static website repository under the organization).
*   **Domain:** `https://repo.zurvanlinux.org`
*   **Caching & Optimization via Cloudflare:**
    *   Cloudflare acts as a reverse proxy for the static GitHub Pages site.
    *   All package metadata (`Packages.gz`, `InRelease`) and standard `.deb` packages (which are usually under 100MB) are aggressively cached on Cloudflare's Edge servers.
    *   This setup minimizes data transit to GitHub, avoids rate-limiting, and guarantees high-speed `apt update` and `apt upgrade` execution for users in Iran, bypassing local ISP routing issues or global throttling.

---

## 3. Repository Integrity & Cryptographic Security
To maintain standard Debian security policies, the package repository is cryptographically signed.

*   **Signing Key:** A dedicated 4096-bit GPG key is generated and managed by the core Zurvan development team.
*   **Metadata Verification:** Every repository update automatically signs the `Release` file, creating `Release.gpg` (detached signature) and `InRelease` (clear-signed) files.
*   **Public Key Distribution:** The public GPG key is hosted at `https://repo.zurvanlinux.org/public.key`. During installation, the Calamares installer automatically registers this key in the user's system keyring (`/etc/apt/keyrings/zurvan-archive-keyring.gpg`) to prevent unsigned repository warnings.

---

## 4. Upstream Mirror Optimization (Iranian Networks)
Upstream packages (standard Debian packages) must be downloaded with minimal latency. 

*   **Auto-Redirector:** By default, Zurvan Linux utilizes `deb.debian.org` in `/etc/apt/sources.list`. This service automatically redirects the user's system to the geolocally nearest Debian mirror.
*   **Alternative Local Mirrors:** For advanced configurations, the custom Welcome Screen will feature a toggle allowing users to easily switch their main Debian sources to trusted local university and ISP mirrors inside Iran (such as Iranserver, Tabriz University, or other high-bandwidth mirrors) to ensure high-speed package updates during network disruptions.

---

## 5. Software Updates via KDE Discover & Flatpak
Zurvan Linux provides a dual-layer graphical update experience to keep user applications secure and up-to-date.

### 5.1 System & APT Updates
*   KDE Discover is configured to check the native APT repositories for core system upgrades and security patches regularly.
*   Users receive standard desktop notifications when system package updates are released.

### 5.2 Application Updates (Flathub)
*   By pre-integrating Flathub, user applications (such as browsers, communication clients, and office software) are updated independently of the Debian base.
*   Flatpak updates are managed seamlessly inside Discover, ensuring users always run the latest stable versions of desktop applications without compromising the underlying system stability.
