# Proxifier + Antigravity（Clash Verge）稳定代理教程

本仓库提供 **Windows 上 Antigravity 走代理** 的完整配置说明，适用于国内网络环境中出现的“加载模型卡顿/报错/超时”等问题。

## 适用场景

- Antigravity 经常卡在 “Loading models…”
- 发消息时报错或长时间无响应
- 已开代理但仍像在直连（部分进程未走代理）

## 你需要准备

- Clash Verge 正常可用
- 已安装 Proxifier

## 快速指引（精简版）

1. 在 Clash Verge 看端口：`设置 -> 端口配置`（优先用 Mixed Port）
2. 在 Proxifier 添加代理服务器（127.0.0.1 + 你的端口，协议选 SOCKS5）
3. 在 Proxifier 添加规则：
   - `Antigravity.exe`
   - `language_server_windows_x64.exe`
   - Action 选你的代理
4. 把规则放在 Default 之上
5. 验证：Proxifier Connections 里 Rule 显示 Antigravity 而非 Direct

> Clash Verge 必须保持运行，否则 Proxifier 的转发无效。

## 完整教程

请查看：
- [Proxifier_Antigravity.MD](./Proxifier_Antigravity.MD)

## 常见问题

- **无限循环提示（verge-mihomo.exe）**：让它直连（Direct）即可
- **DNS 直连导致卡顿**：在 Proxifier 的 Name Resolution 勾选 “Resolve hostnames through proxy”
- **只想让 Antigravity 走代理**：把 Default 改成 Direct

---

如需补充更多场景（Gemini CLI、WSL 等），可提 Issue 或继续扩展文档。
