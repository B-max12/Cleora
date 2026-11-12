# Cleora v0.1.0 Release Notes

**Release Date:** 2026-11-13  
**Tag:** `v0.1.0`

Welcome to the initial public release of **Cleora**, an offline-first, cross-platform storage advisor, desktop software auditor, and safe cleanup engine by **Aur Labs**.

---

## Highlights in v0.1.0

### 1. Runtime OS & Package Manager Auto-Detection
Cleora automatically detects your operating system, Linux distribution, and installed package managers at runtime, adapting its probes, cleanup commands, drive move commands, and software uninstaller automatically:
- **Linux:** Arch Linux (`Pacman`), Ubuntu / Debian / Mint (`APT / DPKG`), Fedora / RHEL (`DNF / RPM`), openSUSE (`Zypper`), `Flatpak`, `Snap`, and `systemd` journal logs.
- **Windows:** PowerShell commands, `%LOCALAPPDATA%` / `%APPDATA%` cache probes, `Clear-RecycleBin`, NTFS directory junctions (`mklink /J`), and `winget` software management.
- **macOS:** `~/Library/Caches`, `~/Library/Developer/Xcode/DerivedData`, Homebrew (`brew cleanup`), `~/.Trash`, and `/Applications` + Homebrew Cask auditing.

### 2. Desktop Installed Software Audit & Complete Uninstaller
- Scans installed desktop software across **Flatpak**, **Snap**, **Pacman**, **APT/DPKG**, **DNF/RPM**, standalone `/opt` or user `.desktop` apps, **Windows Winget**, and **macOS Applications / Homebrew Cask**.
- Computes **total disk footprint** (`App Size + User Config, Cache, and Sandbox Data`) so you can see the real space an app uses.
- Provides one-click uninstallation for supported package managers plus a **Complete Uninstall Guide** with copyable commands and associated user data paths.

### 3. Home & System Space Audit + Clean Up Hub
- Inspects high-impact space consumers (`~/.gradle`, `~/.cargo`, `~/.pub-cache`, `~/Android`, `~/.android`, `~/.var`, `~/.cache`, `/var/cache/pacman`, `/var/cache/apt/archives`, `/var/cache/dnf`, `/var/lib/flatpak`, `/var/log/journal`, OS Trash, and large/old files in `Desktop` and `Downloads`).
- Includes one-click allow-listed cache cleanups, a copyable **Quick Win Script**, and safe secondary-drive offloading via verified symbolic links with one-click undo.

### 4. Interactive Storage Map, BLAKE3 Duplicates & Safe Recovery
- **Storage Map:** Interactive treemap and folder drill-down for any directory.
- **Duplicate Files Finder:** Byte-for-byte BLAKE3 hash verification that always keeps one primary copy protected.
- **Reversible Trash & History:** Tracks cleanup operations in local SQLite and supports conflict-safe restoration.

### 5. Branding, System Tray & Cross-Platform Packaging
- Integrated official Cleora app icon (`icon.png`) and logo (`logo.png`) across the UI, window titlebar, installer bundles, and native **System Tray** (`Show Cleora` / `Quit Cleora`).
- Clean, non-overlapping table and header badges across all screen sizes.

---

## Download & Install Assets

| Platform | Artifact | Notes |
| --- | --- | --- |
| **Linux (All Distros)** | `Cleora_0.1.0_amd64.AppImage` | Portable AppImage (`chmod +x` and run) |
| **Debian / Ubuntu / Mint** | `Cleora_0.1.0_amd64.deb` | Install via `sudo apt install ./Cleora_0.1.0_amd64.deb` |
| **Fedora / RHEL / openSUSE** | `Cleora-0.1.0-1.x86_64.rpm` | Install via `sudo dnf install ./Cleora-0.1.0-1.x86_64.rpm` |
| **Windows (x64)** | `cleora.exe` | Standalone executable for Windows 10 / 11 (requires WebView2 Runtime, pre-installed on Windows 11) |

---

## Verification Summary
- `pnpm build` (`tsc && vite build`): Passed
- `cargo test --workspace`: 30/30 unit tests passed (`cleora-core`, `cleora-db`, `cleora-platform`, `cleora-policy`)
- `cargo clippy --workspace -- -D warnings`: Passed with 0 warnings

