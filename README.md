# 🚀 n8n AI 自动化工作流

基于 **n8n** + **DeepSeek** 的 AI 自动化工作流集合，用于提升工作效率。目前已包含 **岗位 JD 分析** 和 **AI 内容运营助手** 两个工作流。

---

## 📋 工作流介绍

### 1. 岗位 JD 分析 `岗位JD.json`

> 🤖 自动分析招聘岗位描述（JD），生成面试题、简历建议等，结果自动写入 Google Sheets。

**🔄 工作流程：**

```
Webhook 接收 POST 请求
    ↓
DeepSeek AI 分析岗位JD
    ↓
解析 AI 返回的 JSON 结果
    ↓
整理字段并写入 Google Sheets
    ↓
返回分析结果 JSON
```

**📥 输入参数：**

| 参数 | 类型 | 说明 |
|------|------|------|
| `JD` | string | 岗位描述文本 |

**📤 返回内容：**

| 字段 | 说明 |
|------|------|
| `top_5_skills` | 最重要的 5 项硬技能 |
| `experience_level` | 岗位等级（初级 / 中级 / 高级） |
| `interview_questions` | 10 个高频面试题（含类型和考察目的） |
| `resume_optimization` | 简历优化建议（技能匹配、经历优化、关键词、避坑要点） |
| `summary` | 岗位核心职责总结 |

**🔧 调用示例：**

```bash
curl -X POST https://<你的n8n地址>/webhook/job-analyzer \
  -H "Content-Type: application/json" \
  -d '{"JD": "岗位职责：1. 负责公司核心产品的后端开发..."}'
```

---

### 2. AI 内容运营助手 `AI内容运营助手.json`

> 📱 输入新闻内容，一键生成小红书标题、公众号标题、短视频脚本和话题标签。

**🔄 工作流程：**

```
Webhook 接收 POST 请求
    ↓
DeepSeek AI 分析新闻内容
    ↓
解析 AI 返回的 JSON 结果
    ↓
整理字段并写入 Google Sheets
    ↓
返回生成的运营素材 JSON
```

**📥 输入参数：**

| 参数 | 类型 | 说明 |
|------|------|------|
| `news` | string | 新闻原文 / 需要运营的内容 |

**📤 返回内容：**

| 字段 | 说明 |
|------|------|
| `xiaohongshu_titles` | 3 个小红书风格标题 |
| `wechat_titles` | 3 个公众号风格标题 |
| `short_video_script` | 短视频脚本（开头钩子 + 正文 + 结尾引导） |
| `hashtags` | 5 个推荐话题标签 |

**🔧 调用示例：**

```bash
curl -X POST https://<你的n8n地址>/webhook/data \
  -H "Content-Type: application/json" \
  -d '{"news": "某公司今日发布了新一代 AI 芯片..."}'
```

---

## 🛠 技术栈

| 组件 | 用途 |
|------|------|
| [n8n](https://n8n.io/) | 工作流编排引擎 |
| [DeepSeek](https://www.deepseek.com/) | AI 大语言模型 |
| [Google Sheets](https://www.google.com/sheets/) | 数据存储 & 结果记录 |
| Webhook | API 触发入口 |

---

## 📦 如何导入到你的 n8n

1. 打开你的 n8n 管理界面
2. 点击右上角 **"Import from File"**（或从文件导入）
3. 选择 `岗位JD.json` 或 `AI内容运营助手.json`
4. 导入后，重新配置以下凭据：
   - 🔑 **DeepSeek API Key** — 在 DeepSeek Chat Model 节点中配置
   - 📊 **Google Sheets 认证** — 在 Google Sheets 节点中重新授权
5. 点击 **"Active"** 开关激活工作流
6. 🎉 开始使用！

---

## ⚠️ 导入后必做配置

| 配置项 | 所在节点 | 说明 |
|--------|----------|------|
| DeepSeek API Key | DeepSeek Chat Model | 填入你的 DeepSeek API 密钥 |
| Google Sheets 授权 | Append row in sheet | 重新连接你的 Google 账号 |
| Google Sheets 文档 ID | Append row in sheet | 替换为你自己的 Google Sheets 文档 |

---

## 📁 文件结构

```
├── .gitignore              # Git 忽略规则
├── README.md               # 项目说明（本文件）
├── 岗位JD.json             # 岗位分析工作流
└── AI内容运营助手.json     # 内容运营工作流
```

---

## 🔒 安全提示

- ⚠️ 工作流 JSON 中已移除 API 密钥等敏感信息
- ⚠️ 导入后请自行配置 DeepSeek API Key
- ⚠️ 不要将包含真实凭据的 JSON 文件上传到公开仓库
- ⚠️ Google Sheets 文档 ID 如有敏感数据请替换

---

## 🧑‍💻 作者

- **GitHub**: [nna567](https://github.com/nna567)
- **邮箱**: Jiewen595@gmail.com

---

<p align="center">⭐ 如果对你有帮助，欢迎 Star！</p>
