# DigitalPlat 免费域名自动续期脚本

自动续期 DigitalPlat (dash.domain.digitalplat.org) 的免费域名。

## 功能

- 支持多账号
- 自动登录
- 自动处理 Cloudflare 验证
- 自动续期即将到期的域名
- 保存会话供下次使用
- Telegram 通知

## 安装

```bash
# 安装依赖
pip install -r requirements.txt

# 安装 Playwright 浏览器
playwright install chromium
```

## 配置

```bash
# 复制配置文件
cp .env.example .env

# 编辑配置
vim .env
```

配置项说明:

```env
# YesCaptcha API Key (可选，用于解决验证码)
YESCAPTCHA_API_KEY=your_api_key

# 账号配置 (格式: email:password)
# 多个账号用逗号分隔
ACCOUNTS=email1@example.com:password1,email2@example.com:password2

# Telegram 通知 (可选)
TELEGRAM_BOT_TOKEN=your_bot_token
TELEGRAM_CHAT_ID=your_chat_id
```

## 运行

```bash
# 在有显示器的环境
python3 domain_renew.py

# 在无头服务器环境 (headless)
xvfb-run python3 domain_renew.py
```

## 定时任务

使用 cron 定期执行:

```bash
# 每周执行一次 (周日凌晨 3 点)
0 3 * * 0 cd /home/exedev/domain-renew && xvfb-run python3 domain_renew.py >> /var/log/domain-renew.log 2>&1
```

## 目录结构

```
domain-renew/
├── domain_renew.py    # 主脚本
├── .env               # 配置文件
├── .env.example       # 配置模板
├── requirements.txt   # Python 依赖
├── sessions/          # 会话存储
└── README.md          # 说明文档
```

## 注意事项

1. 免费域名通常有效期为 1 年，需要在到期前续期
2. 建议每周或每月执行一次，避免忽略到期域名
3. 如果 Cloudflare 验证失败，可以配置 YesCaptcha API Key
