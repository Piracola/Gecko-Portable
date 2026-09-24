# 新增浏览器支持

Firefox 系（Gecko）的浏览器基本都能直接接入。前提是：

1. 基于现代 Gecko，进程会加载 `mozglue.dll`（注入载体）
2. 有可用的 Windows x64 安装包，且能被 7-Zip 解开
3. 允许在许可证范围内重新分发「注入后的」成品

## 接入步骤

在 `build.py` 里补两处：

1. **`BROWSERS` 字典**：加上可执行文件名、成品目录名、显示名。

```python
"waterfox": {
    "display": "Waterfox",
    "exe_name": "waterfox.exe",
    "folder_name": "Waterfox",
    "supports_lang": False,
},
```

2. **`resolve_version_and_url`**：补上版本和安装包地址的解析方式。已有两个通用解析器：

- `_resolve_firefox()`：Mozilla 官方版本表 + CDN 安装包（含多语言）
- `_resolve_github_release_asset()`：GitHub Releases + 指定 asset 文件名（Floorp / Zen 在用）

若上游有稳定的 JSON API 或可预测的下载 URL，可以仿照 `_resolve_firefox` 新写一个解析函数。

## 新建浏览器仓库

浏览器专属配置不要塞进本仓库。新建一个仓库，放进三样东西：

```text
portable/portable.ini     便携化配置（可从兄弟仓库复制后微调）
开始.bat                  创建快捷方式的启动脚本
.github/workflows/*.yml   调用可复用工作流
```

工作流示例：

```yaml
jobs:
  build:
    permissions:
      contents: write
      actions: write
    uses: Piracola/Gecko-Portable/.github/workflows/build-portable.yml@main
    with:
      browser: waterfox
      release-notes-url: 'https://github.com/BrowserWorks/Waterfox/releases/tag/{version}'
```

| 输入参数 | 默认值 | 说明 |
| --- | --- | --- |
| `browser` | 必填 | `BROWSERS` 里的标识 |
| `lang` | `en-US` | 安装包语言（仅 `supports_lang` 的浏览器有效） |
| `release-notes-url` | 空 | 上游发行说明地址，`{version}` 会被替换成版本号 |
| `builder-ref` | `main` | 检出构建器的分支或标签 |
| `python-version` | `3.10` | 构建用的 Python 版本 |
| `keep-workflow-runs` | `10` | 保留的历史运行记录条数 |

想要完全可复现的构建，把 `uses:` 的引用和 `builder-ref` 同时指向同一个 tag：

```yaml
    uses: Piracola/Gecko-Portable/.github/workflows/build-portable.yml@v1
    with:
      browser: waterfox
      builder-ref: v1
```

（可复用工作流内部拿不到自身所在的提交，`github.job_workflow_sha` 在这个场景下是空的，所以需要显式传一次。）

## 验收清单

新浏览器上线前至少确认：

- [ ] `--check-only` 能解析出正确的版本和安装包 URL
- [ ] 安装包能被 7-Zip 解开，且能找到 `exe_name`
- [ ] 注入后 PE 导入表校验通过
- [ ] 便携性实测通过（`Profiles/` 有数据，`%APPDATA%` 没被写入）
- [ ] 若上游公布了哈希，已接入安装包校验
- [ ] 已写好 `portable.ini` 与 `开始.bat`
- [ ] 已在 `validate.yml` 的版本解析循环里加上新标识

## 候选浏览器清单

哪些 Gecko 衍生浏览器值得接入、难度如何，见 [gecko-browsers.md](./gecko-browsers.md)。
