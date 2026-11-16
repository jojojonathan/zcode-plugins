# Yuanbao Websearch（ZCode 插件）

把腾讯元宝的 MCP 搜索端点（SearchPro）接入 ZCode。与在 MCP 设置里手写 HTTP server 配置等价，插件只是便于按项目/按会话启停管理。

## ⚠️ 需要先设置 API Key

出于安全，插件**不内置** API key（本仓库公开，硬编码会泄漏）。`.mcp.json` 通过环境变量 `YUANBAO_API_KEY` 透传：

```powershell
# PowerShell，设置用户级环境变量（用你自己的 key）
setx YUANBAO_API_KEY "sk-你的key"
```

设置后**重启 ZCode** 生效。未设置该变量时，server 鉴权会失败、工具不可用。

## 功能

中文、中英混合、实时数据（金价/股价/天气等）联网搜索，走元宝 SearchPro。相对 Firecrawl 等英文搜索引擎，中文信源质量更好。

## 工具

| 工具 | 作用 |
|---|---|
| `SearchPro` | 联网搜索。`Query` 必填（UTF-8 ≤1500 字节）；`Mode` 0=公开网页 / 1=垂直权威信源（实时数据用，英文技术查询会返回空）/ 2=混合；`Freshness` 时效（如 `d7`/`m3`/`y1`）；`Cnt` 条数 10–50；`Site` 限站（如 `zhihu.com`）；`Industry` 垂直领域 `news/acad/finance/gov` |

## 配置

`.mcp.json` 为 HTTP 型 MCP：

```json
{
  "type": "http",
  "url": "https://api.wsa.cloud.tencent.com/Mcp",
  "headers": { "Authorization": "Bearer ${YUANBAO_API_KEY}" },
  "alwaysLoad": true
}
```

`${YUANBAO_API_KEY}` 由 ZCode 在启动 server 时从环境变量展开（与官方插件对 API key 的处理方式一致）。
