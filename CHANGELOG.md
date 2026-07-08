# 发布说明

## 1.0.3

- Windows 安装包更新到 1.0.3，导入 Key 后启用 cc-switch 本地转发链路。
- 客户端自身请求和本地转发出去的 Codex / Claude API 请求会使用“网络配置”中选中的连接方式。
- macOS Apple Silicon 与 Intel 安装包构建通过 GitHub Actions，并同步到下载仓库。
- macOS 当前为未公证安装包，首次打开需要右键选择“打开”。
- 下载仓库 SHA256SUMS 已合并 Windows、macOS arm64、macOS x64 文件校验值。

## 1.0.2

- 取消 Codex 聊天记录恢复前的 Windows 原生确认弹窗。
- 点击“立即恢复”后直接进入自动备份和恢复流程，并保留恢复中的顶部提示。
- 撤回本次恢复仍保留确认，避免误操作。
- 本版本继续只更新 Windows x64 安装包。

## 1.0.1

- 修正客户端标题栏误用 CC Switch 图标的问题。
- 前端标题栏图标与 Windows 安装包、任务栏图标统一为解忧 AI 图标。
- 本版本继续只更新 Windows x64 安装包。

## 1.0.0

- 发布 Windows 正式第一版安装包。
- 网络配置未扫描到本机连接方式时，明确提示用户先打开系统代理或 VPN 软件后重新扫描。
- 顶部标题栏新增解忧 AI 桌面助手应用图标。
- 保留已验证通过的网页登录、Key 选择、Codex / Claude Code / Claude Desktop 配置、Codex 聊天记录安全扫描与恢复能力。
- 本版本继续只更新 Windows x64 安装包。

## 0.2.0-beta.15

- 修复部分 Windows 客户端点击“恢复聊天记录”的安全扫描时失败的问题。
- 根因是打包后资源路径可能被转换为 Windows verbatim 格式，传给内置 Node 运行 codex-provider-sync wrapper 时会触发 `EISDIR: illegal operation on a directory, lstat 'C:'`。
- 现在在调用内置 Node 前会把 `\\?\` 路径转换为 Node 兼容的普通 Windows 路径，不改变 codex-provider-sync 的扫描和恢复逻辑。
- 本版本继续只更新 Windows x64 安装包。

## 0.2.0-beta.14

- 软件配置中心的“重新读取”现在会显示加载状态和顶部结果提示。
- 通过“导入并启用当前 Key”写入的 Provider 名称固定为 `JieYou API`，不再拼接 Key 名称。
- 删除软件配置中心里的 API/Provider 时，改为先确认，确认后再删除。
- 保持 Windows x64 安装方式不变，本版本用于客户继续测试。

## 0.2.0-beta.9

- 新增 Claude Desktop 配置入口，底层复用 cc-switch 的 Claude Desktop 3P profile 写入与切换逻辑。
- Codex、Claude Code、Claude Desktop 现在可在同一配置流程中选择。
- Claude Desktop 配置成功后提示用户完全退出并重新打开 Claude Desktop。
- 授权登录网页 UI 已优化，更适合普通客户理解当前步骤。
- 保留原有 Windows x64 安装方式，本版本用于客户测试。

## 0.2.0-beta.2

- 修复“创建 Key”按钮跳转到错误路由的问题，现在打开中转站可用的 Key 页面。
- 网络配置扫描补充常见端口 `7897`、`7899`、`20171`、`2080`，并提高本机端口检测容错时间。
- 中转站账户里的今日 Token 改为 `K`、`M`、`B` 单位显示。
- 更换应用图标，避免继续使用 cc-switch 默认图标。

## 0.2.0-beta.1

- 基于 cc-switch 底座重构客户版客户端。
- 复用 cc-switch ProviderService 完成 Codex / Claude Code 配置新增、更新和切换。
- 只接入解忧中转 Key，不再暴露多 Provider 管理入口给普通客户。
- 网页登录后读取账户和 Key 列表，前端不保存完整 Key。
- 配置 Codex 成功后自动扫描聊天记录状态。
- 集成固定版本 codex-provider-sync，支持安全扫描、立即恢复、自动备份和撤回本次恢复。
- 修复 codex-provider-sync 空输出时显示 EOF 的问题，改为可读错误。
- 打包内置 Windows Node runtime，聊天记录恢复不依赖客户电脑已安装 Node。
- 关闭继承自 cc-switch 的自动更新产物生成和上游更新端点。
- 当前仅发布 Windows x64 安装包；macOS 包后续单独构建验证。

## 0.1.0-beta.1

- Windows a974b76 构建：Codex/Claude Code 配置写入改为 cc-switch 等效逻辑。
- Codex 写入 `config.toml` 的 `experimental_bearer_token` 和 `cc-switch-model-catalog.json`，不覆盖 `auth.json`。
- Claude Code 写入 `settings.json` 的 `ANTHROPIC_AUTH_TOKEN`，移除旧 `apiKeyHelper` 路径。
- 支持 Windows x64 安装包。
- 支持 macOS Apple Silicon 和 macOS Intel 测试安装包。
- 首次使用强制网页登录，不再提供旧的手动 Key 登录入口。
- 新增三步教程引导：网络配置、选择 Key 并配置软件、恢复聊天记录。
- 配置成功和聊天记录恢复成功会弹出明确结果提示。
- 聊天记录恢复入口改为“立即恢复聊天记录”，并在恢复前自动完成检查与备份。
- 优化 codex-provider-sync 输出解析，空输出不再显示 EOF 解析错误，并兼容带运行时噪声的 JSON 输出。
- 优化浅色界面下的选中、下拉、弹窗和左侧教程样式。
- macOS 原生验证已通过 GitHub Actions，当前安装包为未公证测试包。
