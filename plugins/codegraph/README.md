# Codegraph（ZCode 插件）

把本机安装的 codegraph CLI（代码知识图谱工具，`codegraph --version` 可查版本）作为 MCP server 接入 ZCode。与在 MCP 设置里手写 `codegraph serve --mcp` 完全等价，插件只是便于按项目/按会话启停管理。

## 功能

一次 `codegraph_explore` 调用即可拿到**相关符号的源码 + 它们之间的调用路径**（Read 等价的源码片段与调用链），替代反复"搜索→读文件"的循环，显著节省上下文。支持自然语言问题、符号名/文件名组合查询。

## 前置条件

1. **本机已安装 codegraph CLI（≥ 1.6）且在 PATH 中**：

   ```bash
   codegraph --version
   ```

2. **目标项目已建索引**（插件不负责建索引，在项目根目录执行一次）：

   ```bash
   codegraph init          # 建索引（生成项目内 .codegraph/）
   codegraph sync          # 后续增量同步
   ```

   无索引的项目中调用工具会得到相应提示。

## 工具

| 工具 | 作用 |
|---|---|
| `codegraph_explore` | 查询符号/文件/自然语言问题，返回相关源码与调用路径；`maxFiles` 控制来源文件数（默认 12） |

## 配置

`.mcp.json` 保持与直配一致：`codegraph serve --mcp`（stdio），`timeoutMs: 30000`。升级 codegraph CLI 与插件互不影响。
