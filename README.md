# zcode-plugins

[jojojonathan](https://github.com/jojojonathan) 的个人 ZCode 插件市场。仓库本身即市场：在 ZCode 桌面客户端 **插件市场 → 添加 → 添加插件市场** 中填入本仓库地址（`https://github.com/jojojonathan/zcode-plugins`）或本地目录即可安装其中的插件。

## 插件

| 插件 | 版本 | 说明 |
|---|---|---|
| [Next AI Drawio](plugins/next-ai-drawio/) | 0.1.0 | AI 在浏览器实时画布上绘制 draw.io 图表，可人机轮流编辑、导出 `.drawio`/`.png`/`.svg`。封装上游 [`@next-ai-drawio/mcp-server`](https://github.com/DayuanJiang/next-ai-draw-io/tree/main/packages/mcp-server)（Apache-2.0） |
| [Codegraph](plugins/codegraph/) | 0.1.0 | 代码知识图谱：一次 `codegraph_explore` 调用返回相关符号源码与调用路径。封装本机 codegraph CLI（`codegraph serve --mcp`），需本机装 codegraph ≥1.6 且项目已 `codegraph init` |
| [Yuanbao Websearch](plugins/yuanbao-websearch/) | 0.1.0 | 腾讯元宝 MCP 端点联网搜索（中文/混合/实时数据）。需设置环境变量 `YUANBAO_API_KEY` |
| [Tencent Docs](plugins/tencent-docs/) | 0.1.0 | 腾讯文档官方 MCP：创建/读取/搜索在线文档（智能文档、Word、Excel、PPT、思维导图、流程图）、空间管理、OCR。需设置环境变量 `TENCENT_DOCS_TOKEN`（[获取 Token](https://docs.qq.com/open/document/mcp/get-token/)） |

## 布局

```text
zcode-plugins/
  marketplace.json            # 市场目录（ZCode / Claude 插件格式）
  plugins/
    <plugin-name>/
      .zcode-plugin/plugin.json
      ...                     # 插件自身文件
```

新增插件时：在 `plugins/` 下建目录，写好 `.zcode-plugin/plugin.json`，再在 `marketplace.json` 的 `plugins` 数组中登记（`source` 为相对市场根的路径）。

## 说明

- 本仓库只做 ZCode 平台的打包层，各插件功能与许可见其目录内 README 及上游项目
- MCP 型插件通过 `npx` 从 npm 拉取上游包（`@latest`），上游发布新版后重装/重启插件即可更新
