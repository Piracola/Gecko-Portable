# Gecko 衍生浏览器候选清单

统计时间：2026-09。目标是给 `build.py` 扩展更多 Gecko 内核衍生浏览器的便携版支持。

## 接入标准

| 维度 | 要求 |
| --- | --- |
| 内核 | 现代 Gecko，加载 `mozglue.dll`（libportable 注入载体） |
| 安装包 | 有 Windows x64 的 `.exe` 安装包（优于 zip）；7-Zip 可解 |
| 自动化 | 版本号可脚本解析（GitHub Releases / 稳定 JSON API / 可预测 URL） |
| 校验 | 最好有官方 SHA256/SHA512 |
| 结构 | 解包后主目录里有主 exe + `mozglue.dll`，接近 Firefox |
| 许可 | 允许分发「注入后」的成品 |

---

## 一、优先推荐（结构接近 Firefox，接入成本低）

| 浏览器 | 内核 | 上游 / 发布 | 主 exe | 建议标识 | 难度 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| **Firefox ESR** | Gecko | Mozilla 官方 CDN | `firefox.exe` | `firefox-esr` | ★☆☆ | 与现有 firefox 解析几乎相同，只是版本表字段不同 |
| **Firefox Developer Edition** | Gecko | Mozilla 官方 CDN | `firefox.exe` | `firefox-deved` | ★☆☆ | 同上，渠道不同 |
| **Firefox Nightly** | Gecko | Mozilla 官方 CDN | `firefox.exe` | `firefox-nightly` | ★☆☆ | 同上；版本号带 `a1` 后缀 |
| **Firefox Beta** | Gecko | Mozilla 官方 CDN | `firefox.exe` | `firefox-beta` | ★☆☆ | 可用 `firefox_versions.json` 的 `LATEST_FIREFOX_DEVEL_VERSION` |
| **Mercury** | Gecko | [Alex313031/Mercury](https://github.com/Alex313031/Mercury) | `mercury.exe` | `mercury` | ★★☆ | Releases 有 `*_installer.exe`；存在 AVX / SSE3 / SSE4 多构建，默认建议 AVX2 或给出选择 |
| **Waterfox** | Gecko | [BrowserWorks/Waterfox](https://github.com/BrowserWorks/Waterfox) + waterfox.net | `waterfox.exe` | `waterfox` | ★★☆ | GitHub 近期 Releases 无 asset，需改从官网 CDN/更新 API 取包 |
| **LibreWolf** | Gecko | GitLab / Codeberg（非 GitHub 主仓） | `librewolf.exe` | `librewolf` | ★★★ | 隐私增强分支；Windows 有安装包；社区已有 [librewolf-portable](https://github.com/ltguillaume/librewolf-portable) 可对照结构 |

## 二、值得做，但需要额外处理

| 浏览器 | 内核 | 上游 / 发布 | 建议标识 | 难度 | 阻塞点 |
| --- | --- | --- | --- | --- | --- |
| **Mullvad Browser** | Gecko (ESR) | [mullvad/mullvad-browser](https://github.com/mullvad/mullvad-browser) | `mullvad` | ★★★★ | 有 `mullvad-browser-windows-x86_64-*.exe`，但目录是 Tor 式多层布局（`Browser/`），自带启动器；smoke test 与解包逻辑要改 |
| **Tor Browser** | Gecko (ESR) | torproject（官网/镜像） | `tor` | ★★★★★ | 同上；且有多语言、渠道（stable/alpha）、自带便携逻辑，与 libportable 职责重叠 |
| **FireDragon** | Gecko (LibreWolf 系) | [garuda-linux/firedragon](https://github.com/garuda-linux/firedragon)（GitLab 镜像） | `firedragon.exe` | ★★★☆ | 主打 Linux；Windows 发布渠道不稳定，需先确认官方 Windows 包 |
| **GNU IceCat** | Gecko | [tmiland/GNU-IceCat](https://github.com/tmiland/GNU-IceCat) 等社区构建 | `icecat.exe` | ★★★★ | GNU 官方 Windows 包不完整，多靠第三方构建，溯源链弱 |
| **Ghostery Private Browser** | Gecko | ghostery 各仓库 | `ghostery.exe` | ★★★★ | 产品形态多变（Dawn / Ghostery），发布渠道需逐一确认 |
| **Betterbird** | Gecko (Thunderbird) | [Betterbird](https://www.betterbird.eu/) | `betterbird.exe` | ★★★☆ | 是邮件客户端不是浏览器；结构同 Firefox，`mozglue` 注入理论可行 |
| **SeaMonkey** | Gecko（旧） | seamonkey-project.org | `seamonkey.exe` | ★★★★ | 套件（浏览器+邮件）；Gecko 偏旧，`mozglue` 路径可能变化 |

## 三、Goanna（Pale Moon 系，非 Gecko）

libportable 历史上支持 Iceweasel / Pale Moon 系，但注入载体与现代 Firefox 不同，必须单独验证。

| 浏览器 | 内核 | 上游 | 建议标识 | 难度 | 备注 |
| --- | --- | --- | --- | --- | --- |
| **Pale Moon** | Goanna | palemoon.org | `palemoon` | ★★★★ | 有 Windows 安装包；需确认注入目标模块 |
| **Basilisk** | Goanna | Basilisk-Development-Team | `basilisk` | ★★★★ | 同上 |
| **New Moon / Mypal 等第三方编译** | Goanna | 分散 | — | ★★★★★ | 来源分散，不建议作为正式产品线 |

## 四、已支持的同系变体（脚本改动极小）

| 浏览器 | 说明 | 成本 |
| --- | --- | --- |
| Floorp | 已支持 | — |
| Zen | 已支持 | — |
| Firefox | 已支持 | — |
| Zen Twilight / Zen Beta | 同一仓库的预览渠道 | 解析 URL / asset 名即可 |
| Floorp One / Floorp 11 | 同系旧版或皮肤分支 | 看是否仍有独立安装包 |
| Iceweasel（第三方 Firefox 构建） | 与 libportable 同源社区 | 按具体构建发布方式接入 |

## 五、不建议接入（非 Gecko）

| 浏览器 | 原因 |
| --- | --- |
| Midori | 已转向 Chromium |
| Ghost Browser | Chromium |
| qutebrowser | Qt WebEngine |
| Chrome / Edge / Helium | Chromium，已在 [ChromiumPortable](https://github.com/Piracola/ChromiumPortable) 体系 |

---

## 建议接入顺序

```text
1. firefox-esr / firefox-beta / firefox-deved   （复用现有解析，立刻能扩渠道）
2. mercury                                      （GitHub Releases 有 installer.exe）
3. waterfox                                     （先搞定官网下载/校验源）
4. librewolf                                    （GitLab 发布 + 对照社区便携方案）
5. mullvad                                      （Tor 式布局，单独做解包适配）
```

## 实现提示

每增加一个浏览器，工作量大致是：

1. `BROWSERS` 加 4 行配置
2. `resolve_version_and_url` 加一个分支（约 5–20 行）
3. 新建浏览器仓库：`portable/portable.ini` + `开始.bat` + 工作流
4. `validate.yml` 的浏览器列表加上新标识
5. 跑一遍 `--check-only` 与完整构建 + 便携性实测

详细步骤见 [extend.md](./extend.md)。
