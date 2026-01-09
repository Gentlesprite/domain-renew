# DigitalPlat 免费域名自动续期脚本

自动续期 DigitalPlat (dash.domain.digitalplat.org) 的免费域名。

## ⚠️ 免责声明

本项目仅供学习网页自动化技术使用。使用本脚本可能违反相关网站的服务条款，包括但不限于：
- 禁止使用自动化工具访问
- 禁止绕过安全验证措施

**使用本项目的风险由用户自行承担**，包括但不限于账号被封禁、服务被终止等后果。请在使用前仔细阅读相关网站的服务条款。

## 功能

- 支持多账号
- 自动登录
- 自动处理 Cloudflare 验证
- 自动续期即将到期的域名
- 保存会话供下次使用
- Telegram 通知

## 安装

```bash
# 安装系统依赖
sudo apt install xvfb  # Debian/Ubuntu
# sudo yum install xorg-x11-server-Xvfb  # CentOS/RHEL

# 安装 uv
curl -LsSf https://astral.sh/uv/install.sh | sh

# 安装项目依赖
uv sync

# 安装 Playwright 浏览器
uv run playwright install chromium
```

## 配置

```bash
cp .env.example .env
vim .env
```

```env
# 账号配置 (格式: email:password，多账号逗号分隔)
ACCOUNTS=email@example.com:password

# Telegram 通知 (可选)
TELEGRAM_BOT_TOKEN=your_bot_token
TELEGRAM_CHAT_ID=your_chat_id
```

## 运行

```bash
xvfb-run uv run python do_renew.py
```

## 定时任务

免费域名有效期较长，建议每 3 个月运行一次即可。

```bash
crontab -e

# 每季度 1 号凌晨 3 点运行 (1月、4月、7月、10月)
0 3 1 1,4,7,10 * cd /path/to/domain-renew && xvfb-run /home/user/.local/bin/uv run python do_renew.py >> /tmp/domain-renew.log 2>&1
```
