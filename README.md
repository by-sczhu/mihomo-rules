# Mihomo Rulesets

这是一个专为 Mihomo (Clash Meta) 内核定制的高性能分流规则集仓库。
本仓库的所有规则均通过 `raw.githubusercontent.com` 提供直接订阅，无须等待 Release 发布，确保规则更新能够以最快速度同步至客户端。

## 🚀 特性

- **极速直连**：全面采用 GitHub Raw 直连地址，适合配合各类加速代理或定时更新任务。
- **精细化 PT 分流**：
  - 针对常见 PT（Private Tracker）站点与公网 PT Tracker 进行精准拦截/直连配置。
  - **DNS 与 NTP 优化**：针对时间同步等高频且敏感的域名进行特殊直连优化，建议配合 `fake-ip-filter` 使用。

## 📂 规则集订阅列表

| 规则集名称 | 类型 | 说明 | Raw 直连订阅地址 | 建议策略 |
| :--- | :--- | :--- | :--- | :--- |
| **direct_custom** | `domain` / `ipcidr` | 私有种子站点及相关域名/IP | `https://raw.githubusercontent.com/by-sczhu/mihomo-rules/main/direct_custom.mrs` | `DIRECT` |
| **proxy_custom** | `domain` | 自定义直连（DNS 与 NTP 优化 | `https://raw.githubusercontent.com/by-sczhu/mihomo-rules/main/proxy_custom.mrs` | `Proxy` |

## 🛠️ 配置示例 (config.yaml)

在您的 Mihomo 配置文件中，引入本仓库 Raw 规则集的标准写法如下：

rule-providers:

  direct_custom:
    type: http
    behavior: domain
    url: "https://raw.githubusercontent.com/by-sczhu/mihomo-rules/main/direct_custom.mrs"
    interval: 86400

  proxy_custom:
    type: http
    behavior: domain
    url: "https://raw.githubusercontent.com/by-sczhu/mihomo-rules/main/proxy_custom.mrs"
    interval: 86400

rules:
  # 优先处理direct_custom
  - RULE-SET,direct_custom,DIRECT
  - RULE-SET,proxy_custom,Proxy
