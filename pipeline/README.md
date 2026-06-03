# Find Job — AI 驱动的求职辅助 CLI

> 本项目基于 [boss-agent-cli](https://github.com/can4hou6joeng4/boss-agent-cli) 开发，原项目采用 **MIT License**。
>
> 部分代码由 AI 辅助生成。

[![Python](https://img.shields.io/badge/Python-%E2%89%A53.10-3776AB?logo=python&logoColor=white)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![GitHub](https://img.shields.io/badge/GitHub-wangxiyuan05%2Ffind--job-blue)](https://github.com/wangxiyuan05/find-job)

---

## 📖 项目简介

**Find Job** 是一款专为 AI Agent（Claude、Codex、Cursor 等）设计的本地求职辅助 CLI 工具，目前支持 **BOSS 直聘**平台。它帮助求职者在终端中完成职位搜索、福利筛选、流程追踪，并通过 AI 进行简历优化和面试准备。

**设计理念：**
- 本地辅助 · 只读优先 · 用户主动触发
- 不规避风控 · 不批量触达 · 不抓取平台数据
- 所有涉及投递、沟通等敏感操作默认回到官网手动完成

---

## ✨ 功能特性

### 原项目提供的基础能力

| 类别 | 功能 |
|------|------|
| 🔍 职位搜索 | 关键词搜索、城市/薪资/经验多维过滤、福利筛选（`--welfare "双休,五险一金"`） |
| 👋 主动触达 | 查看详情、打招呼、批量打招呼（限 10 个）、一键投递 |
| 📊 流程追踪 | Pipeline 状态管理、跟进提醒、每日摘要、转化漏斗统计 |
| 👀 增量监控 | 搜索预设保存、定时运行、新职位标记、收藏夹管理 |
| 💬 聊天管理 | 聊天列表、消息历史、结构化摘要、标签管理、联系方式交换 |
| 🤖 AI 辅助 | JD 分析、简历润色、定向优化、模拟面试、聊天指导 |
| 👔 招聘方功能 | 候选人管理、回复消息、职位上下架 |
| 🔐 登录链路 | 4 层降级策略：Cookie 提取 → CDP 登录 → HTTP 二维码 → patchright 浏览器 |

### 本项目的改进与扩展

> *（请在此处列举你对原项目所做的修改，示例如下）*

- **[示例] 新增 xxx 模块**：实现了 xxx 功能，用于 xxx 场景
- **[示例] 重构 xxx 模块**：优化了 xxx 逻辑，提升了 xxx 性能
- **[示例] 适配 xxx 平台**：新增对 xxx 平台的支持
- *（请根据实际修改情况补充）*

---

## 🛠 技术栈

| 层级 | 技术选型 |
|------|---------|
| 语言 | Python ≥ 3.10 |
| CLI 框架 | Click |
| HTTP 客户端 | httpx |
| 浏览器自动化 | patchright（Playwright 反检测 Fork）|
| 加密 | cryptography（Fernet + PBKDF2）|
| 数据存储 | SQLite3（WAL 模式）|
| AI 服务 | OpenAI / Anthropic Chat Completions API |
| 测试 | pytest（1000+ 测试用例）|

---

## 📦 安装

### 前置条件

- Python ≥ 3.10
- Chrome 浏览器（用于登录态复用）

### 安装步骤

```bash
# 1. 克隆仓库
git clone https://github.com/wangxiyuan05/find-job.git
cd find-job

# 2. 安装依赖（推荐使用虚拟环境）
python -m venv .venv
source .venv/bin/activate  # Linux/Mac
# .venv\Scripts\activate   # Windows

# 3. 安装包
pip install .

# 4. 安装 patchright 浏览器
patchright install chromium
```

---

## 🚀 快速开始

```bash
# 1. 登录（推荐从 Chrome 提取 Cookie）
boss login --cookie-source chrome

# 2. 查看登录状态
boss status

# 3. 搜索职位
boss search "产品运营" --city 上海 --welfare "双休,五险一金"

# 4. 查看详情
boss detail <security_id>

# 5. 加入候选池
boss shortlist add <security_id> <job_id>

# 6. 查看统计
boss stats
```

### AI 辅助功能

```bash
# 分析 JD
boss ai analyze-jd --jd job_description.txt

# 优化简历
boss ai polish --target "海外运营" --resume resume.md

# 面试准备
boss ai interview-prep --jd job_description.txt
```

### 登录方式

支持 4 种登录方式（自动降级）：
1. **Cookie 提取** — 从 Chrome/Firefox/Edge 本地提取（推荐）
2. **CDP 登录** — 通过 `--remote-debugging-port` 复用浏览器会话
3. **HTTP 二维码** — 纯 HTTP 扫码，无需浏览器
4. **patchright** — 反检测 Chromium 兜底

---

## 📁 项目结构

```
find-job/
├── src/
│   └── boss_agent_cli/
│       ├── ai/              # AI 服务（JD 分析、简历优化等）
│       ├── api/             # BOSS 直聘 API 封装
│       ├── auth/            # 认证模块（Cookie 提取、Token 管理）
│       ├── bridge/          # 浏览器桥接
│       ├── cache/           # 本地缓存
│       ├── commands/        # CLI 命令实现
│       │   ├── recruiter/   # 招聘方功能
│       │   └── ...
│       ├── platforms/       # 多平台抽象（zhipin/zhilian）
│       └── resume/          # 简历管理
├── tests/                   # 测试用例
├── docs/                    # 文档
├── skills/                  # Claude Code Skills
├── mcp-server/              # MCP 服务器
├── LICENSE
└── README.md
```

---

## 🔗 AI Agent 集成

支持 4 种集成方式：

| 方式 | 说明 |
|------|------|
| **Skills 安装** | `npx skills add wangxiyuan05/find-job` |
| **子进程调用** | 直接执行 `boss <command>` |
| **MCP 服务器** | 通过 `boss-mcp` 启动 MCP 服务 |
| **Python SDK** | `from boss_agent_cli import ...` |

---

## 🙏 致谢

### 原项目

本项目基于 [can4hou6joeng4/boss-agent-cli](https://github.com/can4hou6joeng4/boss-agent-cli)（MIT License）开发。

原项目提供了以下核心能力：
- `src/boss_agent_cli/` — 完整的 BOSS 直聘 CLI 框架
- `src/boss_agent_cli/api/` — BOSS 直聘 API 封装
- `src/boss_agent_cli/auth/` — 认证与登录链路
- `src/boss_agent_cli/commands/` — CLI 命令实现
- `src/boss_agent_cli/ai/` — AI 辅助服务
- `src/boss_agent_cli/resume/` — 简历管理
- `src/boss_agent_cli/cache/` — 本地缓存
- `src/boss_agent_cli/bridge/` — 浏览器桥接
- `src/boss_agent_cli/platforms/` — 多平台抽象
- `tests/` — 测试用例
- `docs/` — 文档
- `skills/` — Claude Code Skills
- `mcp-server/` — MCP 服务器

### 本项目的修改

> *（请在此处列出你对原项目代码的修改，格式示例：）*
>
> - `src/boss_agent_cli/xxx.py` — 新增功能 xxx，用于 xxx
> - `src/boss_agent_cli/yyy.py` — 重构了 yyy 逻辑，优化了 xxx
> - `src/boss_agent_cli/zzz.py` — 修复了 zzz 问题
> - `新文件.py` — 新增模块

### AI 辅助

本项目的部分修改和文档由 AI 辅助生成，人工审核后合并。

### 开源社区

感谢 [can4hou6joeng4](https://github.com/can4hou6joeng4) 创建了优秀的原项目，以及所有开源贡献者的付出。

---

## 📄 许可证

本项目延续原项目的 **MIT License** 开源协议。详见 [LICENSE](LICENSE)。

Copyright (c) 2026 can4hou6joeng4  
Copyright (c) 2026 wangxiyuan05
