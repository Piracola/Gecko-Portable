<div align="center">

# Gecko-Portable

Firefox 系列便携浏览器的通用构建器

[![自检][badge-validate]][link-validate]
[![libportable 同步][badge-sync]][link-sync]
[![libportable][badge-libportable]][link-libportable]
[![许可证][badge-license]][link-license]

**语言 / Language:** **简体中文** · [English](README.en.md)

[浏览器成品](#浏览器成品) · [开发文档](./docs/usage.md) · [新增浏览器](./docs/extend.md)

</div>

本仓库是 Firefox 系便携版的构建引擎，不直接面向普通用户。想下载浏览器，请去下面的成品仓库。

## 浏览器成品

| 项目 | 仓库 | 最新版本 | 累计下载 | Star |
| --- | --- | --- | --- | --- |
| **Firefox 便携版** | [Firefox-Portable][link-firefox] | [![][badge-firefox-release]][link-firefox] | [![][badge-firefox-downloads]][link-firefox] | [![][badge-firefox-stars]][link-firefox] |
| **Floorp 便携版** | [Floorp_portable][link-floorp] | [![][badge-floorp-release]][link-floorp] | [![][badge-floorp-downloads]][link-floorp] | [![][badge-floorp-stars]][link-floorp] |
| **Zen 便携版** | [Zen-Portable][link-zen] | [![][badge-zen-release]][link-zen] | [![][badge-zen-downloads]][link-zen] | [![][badge-zen-stars]][link-zen] |

> 各仓库只保存配置和启动脚本；下载、校验、注入、打包全部集中在本仓库完成。

## 仓库分工

| 层级 | 内容 |
| --- | --- |
| **Gecko-Portable**（本仓库） | `build.py`、注入二进制 `bin/`、可复用工作流、上游同步工具 |
| **浏览器仓库** | 仅 `portable/portable.ini`、`开始.bat`、调用可复用工作流的配置 |

改构建流程只需要改本仓库一处，全部浏览器同时生效。

## 快速开始（维护者）

```powershell
# 依赖：Python 3.10+、7-Zip
pip install -r requirements.txt

# 冒烟检查：只解析版本，不下载
python build.py --browser firefox --auto-version --check-only

# 完整构建
python build.py --browser firefox --auto-version `
  --portable ..\Firefox-Portable\portable `
  --launcher ..\Firefox-Portable\开始.bat
```

更多参数与流程说明见 [docs/usage.md](./docs/usage.md)。

## 新增浏览器

Firefox 系（Gecko + `mozglue.dll`）基本都能接入。步骤见 [docs/extend.md](./docs/extend.md)，候选清单见 [docs/gecko-browsers.md](./docs/gecko-browsers.md)。

## 许可证

本仓库采用 MIT 许可证，详见 [LICENSE](LICENSE)。

`bin/` 中的二进制来自 [libportable][link-libportable]，遵循其自身许可证，见 [bin/LICENSE-libportable.txt](bin/LICENSE-libportable.txt)。

---

<div align="center">

<sub>Built and maintained by</sub>

**Piracola**

</div>

<!-- 徽标定义：中文标签需 percent-encode，否则 shields.io 无法解析。 -->
[badge-validate]: https://img.shields.io/github/actions/workflow/status/Piracola/Gecko-Portable/validate.yml?branch=main&style=flat-square&color=2ea043&label=%E8%87%AA%E6%A3%80
[badge-sync]: https://img.shields.io/github/actions/workflow/status/Piracola/Gecko-Portable/sync-libportable.yml?branch=main&style=flat-square&color=2f81f7&label=libportable%20%E5%90%8C%E6%AD%A5
[badge-libportable]: https://img.shields.io/badge/libportable-v9.0.10-blue?style=flat-square
[badge-license]: https://img.shields.io/github/license/Piracola/Gecko-Portable?style=flat-square&color=6e7681&label=%E8%AE%B8%E5%8F%AF%E8%AF%81

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
