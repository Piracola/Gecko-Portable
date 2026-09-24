<div align="center">

# Gecko-Portable

Shared builder for Firefox-family portable browsers

[![Validate][badge-validate]][link-validate]
[![libportable sync][badge-sync]][link-sync]
[![libportable][badge-libportable]][link-libportable]
[![License][badge-license]][link-license]

**Language / 语言:** [简体中文](README.md) · **English**

[Browser packages](#browser-packages) · [Docs](./docs/usage.md) · [Add a browser](./docs/extend.md)

</div>

This repository is the build engine behind the Firefox-family portable packages. It is not aimed at end users — download a finished build from one of the browser repositories below.

## Browser packages

| Project | Repository | Latest | Downloads | Star |
| --- | --- | --- | --- | --- |
| **Firefox Portable** | [Firefox-Portable][link-firefox] | [![][badge-firefox-release]][link-firefox] | [![][badge-firefox-downloads]][link-firefox] | [![][badge-firefox-stars]][link-firefox] |
| **Floorp Portable** | [Floorp_portable][link-floorp] | [![][badge-floorp-release]][link-floorp] | [![][badge-floorp-downloads]][link-floorp] | [![][badge-floorp-stars]][link-floorp] |
| **Zen Portable** | [Zen-Portable][link-zen] | [![][badge-zen-release]][link-zen] | [![][badge-zen-downloads]][link-zen] | [![][badge-zen-stars]][link-zen] |

> Browser repositories only carry configuration and a launcher. Download, verification, injection and packaging all happen here.

## How the repositories are split

| Layer | Contents |
| --- | --- |
| **Gecko-Portable** (this repo) | `build.py`, injection binaries in `bin/`, the reusable workflow, upstream sync tooling |
| **Browser repositories** | Just `portable/portable.ini`, `开始.bat`, and a short workflow that calls the reusable one |

Change the build process in one place and every browser picks it up.

## Quick start (maintainers)

```powershell
# Requirements: Python 3.10+, 7-Zip
pip install -r requirements.txt

# Smoke check: resolve the version only
python build.py --browser firefox --auto-version --check-only

# Full build
python build.py --browser firefox --auto-version `
  --portable ..\Firefox-Portable\portable `
  --launcher ..\Firefox-Portable\开始.bat
```

See [docs/usage.md](./docs/usage.md) for the full pipeline and CLI reference.

## Adding a browser

Any modern Gecko browser with `mozglue.dll` can plug in. Steps: [docs/extend.md](./docs/extend.md). Candidate list: [docs/gecko-browsers.md](./docs/gecko-browsers.md).

## License

MIT — see [LICENSE](LICENSE).

The binaries under `bin/` come from [libportable][link-libportable] and are covered by its own license: [bin/LICENSE-libportable.txt](bin/LICENSE-libportable.txt).

---

<div align="center">

<sub>Built and maintained by</sub>

**Piracola**

</div>

[badge-validate]: https://img.shields.io/github/actions/workflow/status/Piracola/Gecko-Portable/validate.yml?branch=main&style=flat-square&color=2ea043&label=Validate
[badge-sync]: https://img.shields.io/github/actions/workflow/status/Piracola/Gecko-Portable/sync-libportable.yml?branch=main&style=flat-square&color=2f81f7&label=libportable%20sync
[badge-libportable]: https://img.shields.io/badge/libportable-v9.0.10-blue?style=flat-square
[badge-license]: https://img.shields.io/github/license/Piracola/Gecko-Portable?style=flat-square&color=6e7681&label=License

[link-validate]: https://github.com/Piracola/Gecko-Portable/actions/workflows/validate.yml
[link-sync]: https://github.com/Piracola/Gecko-Portable/actions/workflows/sync-libportable.yml
[link-libportable]: https://github.com/adonais/libportable/releases/tag/v9.0.10
[link-license]: https://github.com/Piracola/Gecko-Portable/blob/main/LICENSE

[badge-firefox-release]: https://img.shields.io/github/v/release/Piracola/Firefox-Portable?display_name=tag&style=flat-square&color=d8653f&label=
[badge-firefox-downloads]: https://img.shields.io/github/downloads/Piracola/Firefox-Portable/total?style=flat-square&color=2ea043&label=
[badge-firefox-stars]: https://img.shields.io/github/stars/Piracola/Firefox-Portable?style=flat-square&color=2f81f7&label=
[link-firefox]: https://github.com/Piracola/Firefox-Portable

[badge-floorp-release]: https://img.shields.io/github/v/release/Piracola/Floorp_portable?display_name=tag&style=flat-square&color=3b82f6&label=
[badge-floorp-downloads]: https://img.shields.io/github/downloads/Piracola/Floorp_portable/total?style=flat-square&color=2ea043&label=
[badge-floorp-stars]: https://img.shields.io/github/stars/Piracola/Floorp_portable?style=flat-square&color=2f81f7&label=
[link-floorp]: https://github.com/Piracola/Floorp_portable

[badge-zen-release]: https://img.shields.io/github/v/release/Piracola/Zen-Portable?display_name=tag&style=flat-square&color=6366f1&label=
[badge-zen-downloads]: https://img.shields.io/github/downloads/Piracola/Zen-Portable/total?style=flat-square&color=2ea043&label=
[badge-zen-stars]: https://img.shields.io/github/stars/Piracola/Zen-Portable?style=flat-square&color=2f81f7&label=
[link-zen]: https://github.com/Piracola/Zen-Portable
