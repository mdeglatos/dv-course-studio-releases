# DV Course Studio — Releases

Signed release artifacts and the auto-updater manifest for **DV Course Studio**, a
local-first desktop course studio for Windows (Tauri 2 + React 19).

> This repository holds **published build artifacts only** — the application source lives
> in a separate, private repository. Releases here are produced by the project's release
> pipeline (see `RELEASING.md` in the app repo).

## Download & install

Get the latest installer from the **[Releases](../../releases/latest)** page:

- `DV.Course.Studio_<version>_x64-setup.exe` — Windows (NSIS) installer

Run it to install. WebView2 is fetched automatically if it isn't already present.

## Auto-updates

The app checks this repo for updates via the [Tauri updater](https://v2.tauri.app/plugin/updater/).
Every release includes three assets:

| Asset | Purpose |
|-------|---------|
| `*_x64-setup.exe` | The installer / update payload |
| `*_x64-setup.exe.sig` | Detached minisign signature of the installer |
| `latest.json` | The update manifest the app polls |

The app polls **`releases/latest/download/latest.json`** and compares its `version` field
to the running version. A newer version is downloaded and its signature verified against a
minisign **public key baked into the app** — anything that doesn't verify is rejected
(fail-closed). The private signing key never appears in this repository.

### `latest.json` shape

```json
{
  "version": "0.1.0",
  "notes": "…",
  "pub_date": "2026-07-10T18:43:38Z",
  "platforms": {
    "windows-x86_64": {
      "signature": "<contents of the .sig file>",
      "url": "https://github.com/mdeglatos/dv-course-studio-releases/releases/download/v<version>/DV.Course.Studio_<version>_x64-setup.exe"
    }
  }
}
```

## Publishing a new version

Bump the version, build + sign the installer, and publish it together with an updated
`latest.json` under a new `v<version>` tag. The full procedure — including the
empty-password signing gotcha and the CI options — is documented in `RELEASING.md` in the
application repository.
