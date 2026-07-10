# DV Course Studio

**Design, build, and ship interactive online courses — with AI agents doing the heavy lifting.**

DV Course Studio is a local-first desktop app (Windows) for producing rich, interactive
learning experiences. You plan an academy and its courses, and the studio helps you turn
each chapter into self-contained, interactive HTML "experiences" — complete with voice
narration, imagery, and a consistent visual theme. Work stays on your machine and syncs to
the cloud per course, so it can also appear in the companion web app.

> ⬇️ **[Download the latest installer →](../../releases/latest)**
> &nbsp;•&nbsp; `DV.Course.Studio_<version>_x64-setup.exe` (Windows)

---

## What it does

- **AI-assisted authoring, end to end.** Generate an academy strategy, courses, book
  structure, chapters, and interactive experiences — then refine them with guided prompts.
- **40+ interactive experience types.** Each experience is built as self-contained HTML
  (data → presentation → behavior) with a knowledge checklist, screens, and I18N support.
- **Two build engines, one set of conventions.**
  - *Direct API* — the studio calls AI services to generate content step by step.
  - *Local coding agent* — delegate a whole course to an embedded terminal running a coding
    agent (**Claude Code** or **Antigravity**), which autonomously builds and QAs each
    experience while you watch.
- **Voice & visuals.** Per-experience narration (TTS) and generated imagery, tied into a
  **visual theme system** (10 built-in themes + custom).
- **Local-first, cloud-optional.** Every course is either **Synced** (cloud-canonical via
  the web app, cross-device) or **Local-only** (private, offline). Content-hash
  last-writer-wins sync, an offline queue, and an agent-run lock keep things consistent.
- **Signed auto-updates.** New versions download and verify against a baked-in public key
  before installing (fail-closed).

## Install

1. Download `DV.Course.Studio_<version>_x64-setup.exe` from the
   **[latest release](../../releases/latest)**.
2. Run it. WebView2 is fetched automatically if it isn't already present.
3. On first launch, pick a workspace folder and connect an agent (or continue without one).

## Updates

The app polls this repository at **`releases/latest/download/latest.json`** and compares
its `version` to the running version; a newer, signature-verified build installs itself.
Each release ships three assets:

| Asset | Purpose |
|-------|---------|
| `*_x64-setup.exe` | Installer / update payload |
| `*_x64-setup.exe.sig` | Detached minisign signature |
| `latest.json` | Update manifest the app polls |

<details>
<summary><code>latest.json</code> shape</summary>

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
</details>

---

*This repository distributes **build artifacts only** — the application source is
maintained privately. Releases are produced by the project's release pipeline
(`RELEASING.md` in the app repo).*
