# 🧬 Skill Factory - AI自进化技能工厂

> AI Agent 发现现有 Skills 无法完成新任务时，自动制造所需技能的闭环系统。

## 核心价值

当 AI 遇到新任务时，传统做法是"人工告诉AI缺什么技能"。本系统实现**全自动**：

```
用户给任务
    ↓
AI 判断：现有 Skills 是否覆盖？
    ↓ 能 → 直接执行
    ↓ 不能 → 自动派子Agent → 制造新Skill → 同步回来 → 执行
```

---

## 📁 仓库结构

```
skill-factory/
├── README.md                    # 本文件
├── VERSION_A_MULTI_SERVER/      # 版本A：多服务器架构
│   ├── README.md
│   ├── scripts/
│   │   ├── skill_factory.py     # 核心脚本
│   │   └── wireguard_setup.sh   # VPN一键配置
│   └── configs/
│       └── template.json        # 配置模板
│
├── VERSION_B_SINGLE_SERVER/     # 版本B：单机脚本版
│   ├── README.md
│   ├── scripts/
│   │   └── skill_judge.py       # 判断+创造一体化脚本
│   └── configs/
│       └── skills_template/     # Skill规范模板
│
└── docs/
    ├── ARCHITECTURE.md           # 详细架构设计
    ├── SECURITY.md              # 安全规范
    └── WEBHOOK_INTEGRATION.md   # Webhook集成指南
```

---

## 🔍 版本对比

| 特性 | 版本A（多服务器） | 版本B（单机） |
|------|------------------|--------------|
| 架构 | 主Agent + 新加坡Skill工厂 | 单机判断+创造 |
| 同步方式 | WireGuard VPN + Git | 直接写入本地 |
| 适用场景 | 算力分散、多Agent协作 | 单Agent快速部署 |
| 部署难度 | ⭐⭐⭐⭐ | ⭐ |
| 响应速度 | ~30秒（含网络延迟） | ~5秒 |

---

## 🚀 快速开始

### 版本B（单机）- 推荐新手

```bash
# 克隆本仓库
git clone https://github.com/YuchenKuney/skill-factory.git
cd skill-factory/VERSION_B_SINGLE_SERVER

# 一键部署
bash setup.sh

# 测试
python3 scripts/skill_judge.py "帮我做XX市场调研"
```

### 版本A（多服务器）- 进阶用户

见 `VERSION_A_MULTI_SERVER/README.md`

---

## 🔒 安全规范

**无论哪个版本，都必须遵守：**

1. ❌ 禁止创建金融/支付/银行类 Skill
2. ❌ 禁止创建社交通讯类 Skill
3. ❌ 禁止创建任何涉及密钥/凭证的 Skill
4. ✅ 只创建数据处理/分析/自动化类 Skill
5. ✅ 所有 Skill 必须经过审计才能使用

**脱敏规范：**
- 所有 IP/域名替换为占位符
- 所有 Token/Key 替换为环境变量引用
- 配置通过环境变量注入，不硬编码

---

## 📡 Webhook 集成

所有操作都会推送 Webhook 卡片给用户：

```python
# 进度推送示例
python3 scripts/feishu_progress.py \
    "Step 2/5: 制造 Skill" \
    "✅ competitor_analyzer 已创建" \
    "blue"
```

支持飞书、企业微信、DingTalk 等平台。

---

## 📜 许可证

MIT License

---

_Last updated: 2026-04-24_
