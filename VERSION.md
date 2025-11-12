# Version Management

## Single Source of Truth

The app version is maintained in **three synchronized locations**:

1. **`src-tauri/tauri.conf.json`** - Primary source for Tauri app metadata
2. **`src-tauri/Cargo.toml`** - Rust package version
3. **`package.json`** - Node/npm package version

## How It Works

The version is **automatically pulled from `Cargo.toml`** at runtime:

- Backend: Rust uses `env!("CARGO_PKG_VERSION")` to read from Cargo.toml
- Frontend: JavaScript calls `get_app_version()` Tauri command
- Display: Version is dynamically injected into the header on startup

## Updating the Version

To update the version number:

1. Update `src-tauri/tauri.conf.json`:
   ```json
   {
     "version": "0.3.0"
   }
   ```

2. Update `src-tauri/Cargo.toml`:
   ```toml
   [package]
   version = "0.3.0"
   ```

3. Update `package.json`:
   ```json
   {
     "version": "0.3.0"
   }
   ```

**The HTML no longer needs manual updates!** The version is loaded automatically.

## Why Multiple Files?

- **tauri.conf.json**: Used by Tauri build system for app metadata and installers
- **Cargo.toml**: Standard Rust package version, used at compile-time
- **package.json**: Node.js ecosystem standard, used by npm/Vite tooling

All three should be kept in sync for consistency across the build toolchain.
