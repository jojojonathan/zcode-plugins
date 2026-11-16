# Next AI Drawio（ZCode 插件）

将 [DayuanJiang/next-ai-draw-io](https://github.com/DayuanJiang/next-ai-draw-io) 项目的 MCP server（npm 包 [`@next-ai-drawio/mcp-server`](https://www.npmjs.com/package/@next-ai-drawio/mcp-server)）打包为 ZCode 插件。

安装后，AI 可以在**浏览器实时画布**上绘制 draw.io 图表：AI 的改动会高亮描边、一条 Ctrl+Z 即可撤销，你随时可以和 AI 轮流编辑同一张图。draw.io 编辑器内置于 npm 包中，离线可用。

## 功能

- **从项目画图**：AI 读取你的代码与文档后直接绘制；已有的 `.drawio` / `.drawio.svg` 文件可用 `load_diagram` 打开继续编辑
- **共享画布**：AI 的改动自动描边提示（导出图不含描边），Ctrl+Z 回退；你在浏览器里的手动编辑会被 AI 读取，选中的图形可通过 `get_selection` 用"这些"指代
- **真实图标**：内置 AWS、Azure、GCP、Kubernetes、Cisco 等形状库，AI 使用真实图标名
- **自动排版**：时序图、泳道图、用例图有专属绘制指南与服务器端布局；其他新图的连线会自动绕开图形与文字
- **自查修正**：AI 可对渲染结果截图检查并修正重叠（`screenshot_diagram`）
- **版本与页面**：最近 20 个版本可恢复/对比；多页（标签页）支持
- **导出**：`.drawio`、`.png`、`.svg`、`.drawio.svg`

## 工具一览

| 工具 | 作用 |
|---|---|
| `start_session` | 打开预览画布并返回绘制指南；`session_id` 可继续已保存的图 |
| `create_new_diagram` | 用 `mxCell` XML 画一张新图 |
| `edit_diagram` | 按 id 增、改、删 cell，全有或全无 |
| `get_diagram` | 取当前 XML（含浏览器中的手动编辑） |
| `get_selection` | 取你在预览中选中的图形 |
| `screenshot_diagram` | 对某页截图，供 AI 检查 |
| `load_diagram` / `export_diagram` | 打开 `.drawio` / `.drawio.svg`；保存为 `.drawio` `.png` `.svg` `.drawio.svg` |
| `restore_version` | 回到更早的版本，仍可 redo |
| `list_saved_diagrams` | 列出之前会话保存的图（新→旧） |
| `get_drawing_guide` / `get_shape_library` | 绘制规则 / 某形状库（如 `aws4`）的图标样式 |
| `list_pages` / `add_page` / `rename_page` / `delete_page` | 页面（标签页）管理 |

## 使用

安装启用后直接说，例如：

> 读一下这个仓库，画出它的架构图

AI 会先调 `start_session`，浏览器自动打开预览画布（默认 `http://127.0.0.1:6002`，占用时自动向上找空闲端口），图随画随显。

图表保存在 `~/.next-ai-drawio/<session-id>.drawio`（保留最新 50 张）；`~/.next-ai-drawio/instructions.md` 可写自定义绘图规则（前 5000 字符生效，即时生效无需重启）。

## 配置（可选）

插件默认使用上游全部默认值。如需定制，编辑本插件 `.mcp.json`，在服务器条目中加 `env`（详见[上游 README](https://github.com/DayuanJiang/next-ai-draw-io/tree/main/packages/mcp-server#configuration)）：

| 变量 | 默认 | 说明 |
|---|---|---|
| `PORT` | `6002` | 预览端口，被占用时向上探测到 6020 |
| `DRAWIO_LANG` | 跟随 | 固定语言：`en` `zh` `zh-tw` `ja` `de` 等 |
| `DRAWIO_DARK` | `auto` | `1` 深色 / `0` 浅色 / `auto` 跟随系统 |
| `DRAWIO_UI` | 跟随 | 固定主题：`kennedy` `atlas` `dark` `min` `sketch` `simple` |
| `BROWSER` | 自动打开 | `none` 时不自动开浏览器，`start_session` 仍返回 URL |
| `DRAWIO_DATA_DIR` | `~/.next-ai-drawio` | 保存目录；`off` 关闭保存 |
| `DRAWIO_AUTO_SCREENSHOT` | 关 | `true` 每次创建/编辑都附带截图（每次 2–10 s） |

## 版本

- 插件版本 `0.1.x`：本打包的版本号
- 上游 MCP server 版本：**0.4.15**（`.mcp.json` 通过 `@latest` 锁定最新，npm 发布新版后重装/重启插件即可用上）

## 致谢与许可

上游项目 [DayuanJiang/next-ai-draw-io](https://github.com/DayuanJiang/next-ai-draw-io)（Apache-2.0），作者 DayuanJiang。本仓库仅为 ZCode 平台的打包层，插件功能全部来自上游。
