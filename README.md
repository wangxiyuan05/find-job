# Find Job — 🎯 个人求职全流程管理系统

> 本项目基于 [boss-agent-cli](https://github.com/can4hou6joeng4/boss-agent-cli)（MIT License）开发，继承其 BOSS 直聘 CLI 核心能力。
> 
> 在此之上，针对个人求职需求定制了多平台协作流程、面经调研、Pipeline 追踪等完整工作流。
>
> 部分代码由 AI 辅助生成。

[![Python](https://img.shields.io/badge/Python-%E2%89%A53.10-3776AB?logo=python&logoColor=white)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

---

## 🎯 求职方向

| 方向 | 目标 |
|------|------|
| 🌍 **海外出海品牌增长/运营** | 品牌出海类岗位 |
| 📊 **互联网产品运营/数据运营** | 大厂/中厂运营岗 |
| 🏭 **快消/新能源海外市场实习生** | 实业出海方向实习 |

---

## ✨ 功能特性

### 继承自原项目的基础能力

| 类别 | 功能 |
|------|------|
| 🔍 职位搜索 | 关键词搜索、城市/薪资/经验多维过滤、福利筛选（双休/五险一金等）|
| 👋 主动触达 | 查看详情、打招呼、批量打招呼、投递 |
| 📊 流程追踪 | Pipeline 状态管理、跟进提醒、每日摘要、转化漏斗 |
| 👀 增量监控 | 搜索预设、定时运行、新职位标记、收藏夹管理 |
| 💬 聊天管理 | 聊天列表、消息历史、摘要、标签、联系方式交换 |
| 🤖 AI 辅助 | JD 分析、简历润色、定向优化、模拟面试、聊天指导 |
| 🔐 登录链路 | Cookie 提取 → CDP 登录 → HTTP 二维码 → patchright 浏览器 |

### 本项目的定制增强

| 新增内容 | 说明 |
|---------|------|
| 📁 `pipeline/` | 求职全流程数据管理目录（职位池/面经/简历/追踪/内推）|
| 📋 `pipeline/求职流程模拟.md` | 完整操作流程文档，三个方向的详细命令示例 |
| 📊 职业方向筛选预设 | 针对海外品牌增长/数据运营/快消新能源的搜索策略 |
| 🌐 OpenCLI 协作流程 | 集成知乎/小红书/脉脉等平台进行面经调研和内推获取 |
| 🧠 AI 简历策略 | 按不同方向定制简历优化和面试准备流程 |

---

## 🔧 工具链

| 工具 | 用途 |
|------|------|
| **boss-agent-cli** | BOSS 直聘职位搜索、投递、追踪、AI 优化 |
| **OpenCLI** | 知乎/小红书/脉脉/B站等社交平台信息收集 |
| **qiaomu-opencli-skills** | Claude Code 直接调用 OpenCLI 的 Skill 封装 |

---

## 🚀 快速开始

```bash
# 1. 登录（从 Chrome 提取 Cookie）
boss login --cookie-source chrome

# 2. 查看状态
boss status

# 3. 搜索 —— 海外品牌增长方向
boss search "海外品牌增长" --city 上海 --welfare "双休,五险一金"

# 4. 搜索 —— 数据运营方向
boss search "数据运营" --city 上海 --salary "15k-30k"

# 5. 搜索 —— 快消新能源实习
boss search "新能源 海外市场 实习" --city 上海
```

---

## 📁 项目结构

```
find-job/
├── pipeline/                     ← 🆕 求职数据中枢（本项目的核心新增）
│   ├── 职位池/                    # boss search 结果 + 候选池
│   ├── 面经/                      # OpenCLI 收集的各平台面经
│   ├── 简历/                      # 各方向定制简历
│   ├── 内推/                      # 社交平台获取的内推信息
│   ├── 追踪/                      # Pipeline 状态
│   └── 求职流程模拟.md             # 完整操作文档
│
├── src/boss_agent_cli/           # ← 继承自原项目
│   ├── ai/         # AI 服务
│   ├── api/        # BOSS 直聘 API
│   ├── auth/       # 认证模块
│   ├── commands/   # CLI 命令
│   └── resume/     # 简历管理
│
├── LICENSE                       # MIT License（含原项目 + 本人版权）
├── README.md
└── CLAUDE.md                     # AI 助手配置
```

---

## 💡 日常操作流程

详见 [`pipeline/求职流程模拟.md`](pipeline/求职流程模拟.md)，核心步骤：

```
早上  →  boss search → 发现新职位 → 加入候选池
白天  →  看详情 → AI 分析 JD → 简历优化
      →  opencli 搜面经 → 收集信息
晚上  →  boss stats → 看统计数据
      →  boss ai interview-prep → 面试准备
```

---

## 🙏 致谢

### 原项目

本项目基于 [can4hou6joeng4/boss-agent-cli](https://github.com/can4hou6joeng4/boss-agent-cli)（MIT License）开发。

继承自原项目的模块：
- `src/boss_agent_cli/` 核心框架及所有子模块
- `tests/` 测试用例
- `docs/` 文档
- `skills/` + `mcp-server/` 集成配置

### 本项目的增量

- `pipeline/` — 求职流程管理目录及文档
- `README.md` — 重写，聚焦个人求职场景
- `LICENSE` — 追加版权声明
- `CLAUDE.md` — AI 助手协作配置

### AI 辅助

本项目的增量部分的代码和文档由 AI 辅助生成，人工审核后合并。

---

## 📄 许可证

MIT License。详见 [LICENSE](LICENSE)。

Copyright (c) 2026 can4hou6joeng4  
Copyright (c) 2026 wangxiyuan05
