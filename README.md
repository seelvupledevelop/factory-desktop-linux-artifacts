# Factory Desktop 0.187.0 — Linux build artifacts (PRIVATE)

Unofficial Linux packaging of **Factory Desktop 0.187.0**, built from Factory's
official macOS DMG using the
[factory-desktop-linux](https://github.com/seelvupledevelop/factory-desktop-linux)
port builder. Not affiliated with or supported by Factory. Official source:
[factory.ai](https://factory.ai).

> ⚠️ Private mirror of build outputs. Do not redistribute. For personal use only.

## Artifacts — v0.187.0 (CI-built 2026-09-30, run 36774904364)

| File | Size | SHA-256 |
|---|---|---|
| `factory-desktop_0.187.0_amd64.deb` | 258,584,498 B | `477c61da938feaa147509e7ea75b2ae6fa8427f3576db21f8048662afa0879a6` |
| `Factory-0.187.0.AppImage` | 257,969,263 B | `a9a0baca154ba301c44841a4ff58e37e7e7ca1926253fe49fe4ded32cbd51c67` |

> Rebuilt twice on 2026-09-30: first locally with the `MimeType=x-scheme-handler/factory-desktop` fix (electron-builder had been silently dropping scheme registration — broke browser sign-in on cold starts), then by CI on the public repo (`Release` workflow). Both artifacts ship the fix; hashes above are the CI build, identical on the public release.

Verify: `sha256sum -c checksums-0.187.0.txt`

The `.deb`, `.AppImage`, and `checksums-0.187.0.txt` are attached to the
[private release v0.187.0](https://github.com/seelvupledevelop/factory-desktop-linux-artifacts/releases/tag/v0.187.0)
(git cannot carry files over 100 MB; GitHub Releases allow up to 2 GB each).

**Direct downloads** (private — require repo access):

- [factory-desktop_0.187.0_amd64.deb](https://github.com/seelvupledevelop/factory-desktop-linux-artifacts/releases/download/v0.187.0/factory-desktop_0.187.0_amd64.deb)
- [Factory-0.187.0.AppImage](https://github.com/seelvupledevelop/factory-desktop-linux-artifacts/releases/download/v0.187.0/Factory-0.187.0.AppImage)
- [checksums-0.187.0.txt](https://github.com/seelvupledevelop/factory-desktop-linux-artifacts/releases/download/v0.187.0/checksums-0.187.0.txt)

GitHub's release-asset digests confirm integrity: the uploaded files hash
exactly to the SHA-256 values in the table above (`477c61da…` / `a9a0baca…`).

## Install

```sh
# Debian/Ubuntu/Mint (.deb — installs to /opt/Factory, adds desktop entry + user services)
sudo apt install ./factory-desktop_0.187.0_amd64.deb

# AppImage (portable)
chmod +x Factory-0.187.0.AppImage
./Factory-0.187.0.AppImage
```

Requires the global `droid` CLI on PATH (`~/.local/bin/droid` works too); the
app installs it via Factory's official installer if missing.

## Provenance & build verification

Built with `node dist/cli.js build-all --factory-version 0.187.0 --targets deb,appimage`
from the `factory-desktop-linux` port at commit `3ac56f3`.

- Source DMG: official `Factory-0.187.0-x64.dmg` from `app.factory.ai/api/desktop`
  (S3: `downloads.factory.ai/factory-desktop/releases/0.187.0/darwin/x64/`)
- Upstream `app.asar` SHA-256: `9df8956c7023fa6dd3df02cffae95fd275a27f7e5f4f2772bce7f89ed0882b0f`
- Patch markers verified in the built app: daemon transport patch present,
  user daemon on 127.0.0.1:37643, Linux keytar ELF (no macOS binary),
  Rust `factory-update-manager` staged, **no bundled droid binary**
- Packaging toolchain: electron-builder 25.1.8, Electron 42.3.3, 7-Zip 26.01
