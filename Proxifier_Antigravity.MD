# Proxifier + Antigravity 配置教程（Clash Verge）

本文面向 Windows 用户，目标是让 **Antigravity** 稳定走代理，避免直连导致的卡顿/报错。示例基于 Clash Verge + Proxifier。

## 一、准备条件

- 已安装 **Clash Verge** 并能正常联网
- 已安装 **Proxifier**

> 建议保持 Clash Verge 常驻运行，因为 Proxifier 只是把流量转发到本地代理端口。

## 二、确认 Clash Verge 端口

在 Clash Verge：`设置 -> 端口配置`

- **混合代理端口 (Mixed Port)**：如果开启，优先用它
- **SOCKS 代理端口**：若只开了 SOCKS，就用 SOCKS 端口
- **HTTP(S) 代理端口**：若只开了 HTTP/HTTPS，就用 HTTP(S) 端口

示例（以 Mixed Port 为例）：

- Address：`127.0.0.1`
- Port：`7897`
- Protocol：`SOCKS5`

## 三、在 Proxifier 添加代理服务器

`Profile -> Proxy Servers -> Add`

- Address：`127.0.0.1`
- Port：填 Clash Verge 的端口（例如 `7897`）
- Protocol：优先选 **SOCKS5**（Mixed Port 兼容）
- Authentication：一般不需要

点击 **Check** 测试成功后保存。

## 四、添加 Antigravity 规则（关键）

`Profile -> Proxification Rules -> Add`

- Name：`Antigravity`
- Applications：添加以下进程（建议使用 Browse 选择完整路径）
  - `Antigravity.exe`
  - `language_server_windows_x64.exe`
- Action：选择刚刚添加的代理（如 `127.0.0.1:7897 SOCKS5`）
- Target hosts：`Any`
- Target ports：`Any`

保存后将该规则**拖到 Default 之上**。

### 如何找到 language_server_windows_x64.exe

1. 打开 Antigravity
2. 任务管理器 -> 找到 `language_server_windows_x64.exe`
3. 右键 -> `打开文件位置`

常见路径示例：

```
C:\Users\<用户名>\.antigravity-server\bin\<版本号>\extensions\antigravity\bin\language_server_windows_x64.exe
```

## 五、避免“代理代理自己”的死循环

当 Proxifier 提示 **verge-mihomo.exe 无限循环** 时：

- 选择 “Apply suggested changes automatically”
- 或手动添加规则：
  - Application：`verge-mihomo.exe`
  - Action：`Direct`
  - 放在规则最上方

## 六、DNS 走代理（推荐）

`Profile -> Name Resolution`

- 取消勾选 `Detect DNS settings automatically`
- 勾选 `Resolve hostnames through proxy`

这样可以避免 DNS 直连导致的卡顿或解析失败。

## 七、验证是否生效

1. 打开 Antigravity，触发一次请求
2. 回到 Proxifier -> `Connections`
3. 看到 `Rule` 为 `Antigravity`，且不是 `Direct` 即表示成功

## 常见问题排查

- **Check 失败**：确认 Clash Verge 在运行、端口正确、未被占用
- **依然卡顿**：看 Proxifier 里是否命中规则；必要时用完整路径
- **别的软件不想走代理**：把 Proxifier 的 `Default` 改成 `Direct`

---

完成以上步骤后，Antigravity 会稳定走代理，避免直连导致的报错或长时间无响应。
