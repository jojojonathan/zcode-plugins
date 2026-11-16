# Tencent Docs（ZCode 插件）

把腾讯文档官方 MCP 端点接入 ZCode。HTTP 型，与你自己在 MCP 设置里配置该端点等价，插件只是便于按项目/按会话启停管理。

## ⚠️ 需要先设置 Token

腾讯文档 MCP 需要个人 Token 鉴权（无 Token 时所有请求返回 401 `Bearer token required`）：

1. 浏览器登录腾讯文档后访问 **https://docs.qq.com/open/document/mcp/get-token/** 复制你的 Token
2. 设置用户级环境变量并**重启 ZCode**：

   ```powershell
   setx TENCENT_DOCS_TOKEN "你的Token"
   ```

`.mcp.json` 中以 `Authorization: Bearer ${TENCENT_DOCS_TOKEN}` 透传（仓库不保存 Token）。若鉴权仍失败，把 `.mcp.json` 里该行的 `Bearer ` 前缀去掉（部分文档写的是裸 Token 形式）再重载插件试试。

## 功能（官方 MCP，约 224 个工具，以 tools/list 实际返回为准）

| 类别 | 代表工具 |
|---|---|
| 创建文档 | `create_smartcanvas_by_markdown`（智能文档，首选，MDX/Markdown 兼容）、`create_word_by_markdown`、`create_excel_by_markdown`、`create_slide_by_markdown`、`create_mind_by_markdown`、`create_flowchart_by_mermaid` |
| 读取/搜索 | `get_content`（读文档内容）、`search_space_file`（搜空间内文件）、`query_space_node`（空间节点树） |
| 空间与文件管理 | `create_space_node`、`manage.*`（重命名/移动/复制/删除/导入导出/权限） |
| 结构化编辑 | `smartsheet.*`（智能表格）、`sheet.*`（Excel）、`doc.*`（Word 精细编辑） |
| 其他 | `ocr.*`（图片转 Word/Excel）、网页剪藏、本地文件上云 |

## 使用示例

> 在我的腾讯文档里新建一篇智能文档，把这份会议纪要整理进去

> 搜索我空间里文件名带"预算"的表格，读出第二列为空的行

## 配置

`.mcp.json` 为 HTTP 型 MCP：

```json
{
  "type": "http",
  "url": "https://docs.qq.com/openapi/mcp",
  "headers": { "Authorization": "Bearer ${TENCENT_DOCS_TOKEN}" }
}
```

`${TENCENT_DOCS_TOKEN}` 由 ZCode 在连接时从环境变量展开。Token 失效后回到 get-token 页重新获取并更新环境变量即可。
