<p align="center">
  <img src="logo.png" alt="Cleora Logo" width="112" />
</p>

<h1 align="center">Cleora</h1>

<p align="center">
  <strong>See what fills your disk, and clean it up safely.</strong><br />
  Offline-first, cross-platform personal storage advisor, desktop software auditor, and safe cleanup engine by <strong>Aur Labs</strong>.
</p>

<p align="center">
  <strong>Latest Release:</strong> <code>v0.1.0</code> · <strong>Platforms:</strong> Linux (Arch, Ubuntu, Debian, Fedora, openSUSE) · Windows · macOS
</p>

---

## Overview

Cleora is built on the philosophy that a system cleaner should be a **careful, transparent advisor**, never a blind cleaner. At runtime, Cleora automatically detects your operating system, Linux distribution, and installed package managers, then adapts its storage audit, cleanup commands, drive-offloading scripts, and software uninstaller to match your machine.

### Key Features

- **Home & System Space Audit:** Plain-English breakdown of your biggest space users (package caches, browser & tool caches, Gradle, Cargo, Pub/Dart, Android SDK, Docker, Flatpak, Snap, Xcode DerivedData, and `Desktop` / `Downloads` large files & installers).
- **Runtime OS & Package Manager Detection:** Automatically detects `Arch/Pacman`, `Ubuntu/Debian APT`, `Fedora DNF`, `openSUSE Zypper`, `Flatpak`, `Snap`, `Windows PowerShell + Winget`, and `macOS Homebrew`, generating native commands for your system.
- **Desktop Installed Software Audit & Complete Uninstaller:** Discovers installed desktop apps across Flatpak, Snap, Pacman, APT/DPKG, DNF/RPM, standalone `/opt` or user apps, Windows `winget`, and macOS `/Applications` + Homebrew Cask. Calculates total footprint (app binary + user config/cache/sandbox data) and provides one-click uninstall plus step-by-step complete removal commands.
- **Safe 1-Click Tool Cleanups & Quick Win Script:** Executes strictly allow-listed cleanup actions (moving safe caches to OS Trash or invoking official package cache cleaners) and generates a copyable Quick Win script.
- **Secondary Drive Mover (Symlink / Junction Offloading):** Safely moves heavy directories (`~/Android`, `~/.gradle`, `~/.cargo`, `~/.var`) to a secondary drive with verified symbolic links (or Windows junctions) and one-click undo/restore.
- **Interactive Storage Map & Duplicate Files Finder:** Treemap visualization of folder sizes and byte-for-byte BLAKE3 cryptographic duplicate detection that always preserves a primary copy.
- **Reversible Trash & Recovery History:** File cleanups move items to OS Trash or same-volume recovery vaults with conflict-safe restoration and local SQLite audit logs.
- **System Tray Integration:** Runs cleanly with a native system tray icon (`Show Cleora` / `Quit Cleora`) and low-disk notifications.

---

## Key Safety Invariants

1. **No Automated Blind Deletion:** No file, directory, or software package is ever removed automatically based on age or pattern heuristics.
2. **Cryptographic Proof for Duplicates:** Identical files are proven byte-for-byte using streaming BLAKE3 hashing, preserving at least one authoritative copy in every duplicate set.
3. **Source Code & System Inviolability:** Directories like `src/`, `lib/`, `tests/`, `.git`, and core OS paths are strictly protected (`Risk Level R0`).
4. **Honest Space Accounting:** Moving items to OS Trash or recovery vaults is reported transparently; immediate disk capacity is only freed when Trash is emptied.
5. **Conflict-Safe Restoration:** Restoring a file never overwrites an existing file silently.
6. **100% Offline & Private:** Zero accounts, zero telemetry, zero analytics tracking.

---

## Installation (v0.1.0)

### Linux (All Distributions)
- **Universal AppImage (Arch, Ubuntu, Debian, Fedora, openSUSE, Mint):**
  ```bash
  chmod +x Cleora_0.1.0_amd64.AppImage
  ./Cleora_0.1.0_amd64.AppImage
  ```
- **Debian / Ubuntu / Linux Mint / Pop!_OS (`.deb`):**
  ```bash
  sudo apt install ./Cleora_0.1.0_amd64.deb
  ```
- **Fedora / RHEL / openSUSE (`.rpm`):**
  ```bash
  sudo dnf install ./Cleora-0.1.0-1.x86_64.rpm
  ```

### Windows
- Download `cleora.exe` and run it directly on Windows 10 / 11 (uses the built-in Microsoft Edge WebView2 Runtime).

---

## Architecture & Technology Stack

- **Desktop Shell:** Tauri 2 (native packaging, system tray, secure sandboxed IPC)
- **Core Engine:** Rust (`cleora-core`, `cleora-platform`, `cleora-db`, `cleora-policy`, `cleora-test-fixtures`)
- **Frontend UI:** React 19 + TypeScript + Vite + Tailwind CSS
- **Local Persistence:** Embedded SQLite in WAL mode with foreign-key constraints
- **Platform Integrations:** Linux (Freedesktop Trash, `statvfs`, `pkexec`), Windows (Recycle Bin, PowerShell, `winget`), macOS (`~/.Trash`, `osascript`, Homebrew)

---

## Workspace Structure

```text
Cleora/
├── Cargo.toml                      # Root Cargo workspace (v0.1.0)
├── package.json                    # Frontend dependencies & scripts (v0.1.0)
├── icon.png                        # Master application icon
├── logo.png                        # Master application logo
├── docs/                           # Architecture specifications & charters
├── crates/
│   ├── cleora-core/                # Space hog advisor, scanner, duplicates, classification, mover, recovery
│   ├── cleora-platform/            # Volumes, OS trash, multi-OS tool runner, software inventory
│   ├── cleora-db/                  # SQLite connection, migrations, repositories
│   ├── cleora-policy/              # R0-R4 risk levels, rules engine, protected path denylists
│   └── cleora-test-fixtures/       # Mock polyglot project fixtures & synthetic trees
├── src-tauri/                      # Tauri 2 app configuration, system tray, typed commands
└── src/                            # React 19 UI
```

---

## Building from Source

### Prerequisites
- **Rust:** `1.90+` (`rustup update stable`)
- **Node.js:** `v20+`
- **pnpm:** `v10+`
- **Linux System Libraries:** `webkit2gtk-4.1`, `libappindicator3` / `libayatana-appindicator3`, `libssl-dev`, `build-essential`

### Commands

```bash
# Install frontend dependencies
pnpm install

# Run development app
pnpm tauri dev

# Run full verification suite
pnpm build
cargo test --workspace
cargo clippy --workspace -- -D warnings

# Build Linux packages (.AppImage, .deb, .rpm)
pnpm tauri build

# Cross-compile Windows .exe from Linux (requires cargo-xwin + lld)
pnpm tauri build --runner cargo-xwin --target x86_64-pc-windows-msvc --no-bundle
```

---

## License

Dual-licensed under either of:
- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE))
- MIT license ([LICENSE-MIT](LICENSE-MIT))

at your option.
