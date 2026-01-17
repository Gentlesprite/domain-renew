# 域名自动续期脚本

自动续期 digitalplat.org 免费域名 (us.kg, pp.ua, eu.org 等)。

## 功能

- 支持多账号批量处理
- 自动发现账号下所有域名
- 智能判断是否在续期窗口内 (180天)
- 自动处理 Cloudflare 验证
- 会话持久化
- Telegram 通知支持

## 青龙面板使用

### 1. 添加订阅

在青龙面板的「订阅管理」中添加：

- **名称**: domain-renew
- **链接**: `https://github.com/donma033x/domain-renew.git`
- **分支**: main
- **定时规则**: `0 8 * * *`

### 2. 配置环境变量

在青龙面板的「环境变量」中添加：

| 变量名 | 说明 | 示例 |
|--------|------|------|
| `ACCOUNTS_DOMAIN` | 账号配置 | `邮箱:密码,邮箱2:密码2` |
| `TELEGRAM_BOT_TOKEN` | TG机器人Token | (可选) |
| `TELEGRAM_CHAT_ID` | TG聊天ID | (可选) |

**账号格式**: `邮箱:密码`，多账号用逗号分隔

### 3. 安装依赖

在青龙面板的「依赖管理」→「Python3」中安装：

```
playwright
requests
```

### 4. 系统依赖

需要在容器中安装 xvfb:

```bash
apt-get update && apt-get install -y xvfb xauth
```

### 5. 定时任务

建议每季度执行一次:
- 定时规则: `0 8 1 1,4,7,10 *` (1月、4月、7月、10月的1号 8:00)

## 手动运行

```bash
export ACCOUNTS_DOMAIN="your@email.com:password"
xvfb-run python3 do_renew.py
```

## 许可

MIT License
