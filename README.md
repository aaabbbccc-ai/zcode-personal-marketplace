# ZCode 个人插件市场

个人常用的 ZCode 插件集合。在任意一台电脑上把本仓库添加为插件市场，就能安装这里收录的插件。仓库是公开的，只包含插件清单和 Apache-2.0 技能文档，不含账号、Cookie 或密钥。

## 在另一台电脑上使用

ZCode Desktop：

1. 打开 **设置 → 插件 → 发现**（Plugin Marketplace）。
2. 点右上角 **+ → 添加插件市场**。
3. 填入 `aaabbbccc-ai/zcode-personal-marketplace`（公开仓库，新机器无需登录 GitHub）。
4. 在 **Personal → zisu-personal** 下找到需要的插件，点 **安装**。

ZCode CLI：

```bash
zcode plugins marketplace add aaabbbccc-ai/zcode-personal-marketplace
zcode plugins install chrome-devtools@zisu-personal
```

安装完成后新开一个会话生效。

## 收录插件

### chrome-devtools

Google 官方 [chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp) 的打包，附带官方 7 个技能文档：

| 技能 | 用途 |
| --- | --- |
| `chrome-devtools` | MCP 工具总览与标准操作流程 |
| `chrome-devtools-cli` | 不通过 MCP、直接用 CLI 操作浏览器 |
| `cookie-debugging` | Cookie、会话、登录态与 SameSite 排查 |
| `a11y-debugging` | 无障碍语义、焦点、对比度审计 |
| `debug-optimize-lcp` | LCP / Core Web Vitals 分析与优化 |
| `memory-leak-debugging` | 堆快照抓取、对比与内存泄漏定位 |
| `troubleshooting` | 连接失败、页面目标异常排查 |

MCP 启动参数默认是：

```text
npx -y chrome-devtools-mcp@1.11.0 --autoConnect
```

`--autoConnect` 会接管你当前登录着的 Chrome（Chrome 144+），而不是另起一个没有登录态的浏览器。使用前需要在该 Chrome 里打开 `chrome://inspect/#remote-debugging` 并允许调试连接；首次连接 Chrome 还会弹一次授权框。用完记得回到该页面关闭，开着等于任何本机程序都能控制这个浏览器。

如果只想让 MCP 自己启动一个独立 Chrome（不需要登录态，也不会弹授权框），把 `.zcode-plugin/plugin.json` 里 `args` 的 `--autoConnect` 去掉，重新安装或更新插件即可。

插件本身不保存任何账号、Cookie 或密钥。浏览器内容和操作结果会进入当前 ZCode 会话上下文，注意不要在不可信的页面里暴露敏感信息。

## 更新

修改插件后同步提升两处版本号，保持一致：

- `plugins/chrome-devtools/.zcode-plugin/plugin.json` 的 `version`
- `.claude-plugin/marketplace.json` 中对应条目的 `version`

然后提交并推送。其他机器执行 `zcode plugins marketplace update zisu-personal`，再 `zcode plugins update chrome-devtools@zisu-personal`。

## 目录结构

```text
.
├── .claude-plugin/
│   └── marketplace.json
└── plugins/
    └── chrome-devtools/
        ├── .zcode-plugin/plugin.json
        ├── LICENSE
        └── skills/
```

## 许可

`chrome-devtools` 插件中的技能文档与 `LICENSE` 来自 Google 的
[chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp)，遵循 Apache-2.0。
