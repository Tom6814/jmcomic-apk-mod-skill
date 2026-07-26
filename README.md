# JMComic3 APK 逆向修改 Skill

[![Skill](https://img.shields.io/badge/AI-Skill-blue)](https://github.com/Tom6814/jmcomic-apk-mod-skill)
[![JMComic3](https://img.shields.io/badge/JMComic3-v2.0.29-orange)](https://github.com/Tom6814/JMComic3-APK-NO-Ads)

一个**面向 AI 编程工具的 Skill 包**，用于自动化完成 JMComic3 Android APK 的逆向修改任务：去除广告、移除游戏/电影板块。

---

## 这是什么

这是一个 **AI Skill 文件**——一份系统化的指令和知识文档，接入支持 Skill 机制的大语言模型（LLM）或 AI 编程工具后，可以让 AI 自动完成以下工作：

- 分析 JMComic3 APK 的 Webpack 分块结构
- 定位并清除所有广告代码（banner、闪屏、插屏、文字链接）
- 移除游戏和电影板块的路由、Tab 入口、孤儿 chunk
- 削减 APK 体积、防止误删、验证核心功能

**逆向修改一个 APK 通常需要耗费数小时的人力**——追踪 minified JS 中的广告链路、逐 chunk 修补、反复测试验证。通过这个 Skill，AI 可以在几分钟内完成同样的工作。

---

## 适用场景

| 模式 | 说明 |
|------|------|
| **分支 A：仅去广告** | 清除所有应用内广告，保留游戏/电影板块 |
| **分支 B：去广告 + 去板块** | 在 A 基础上彻底剔除游戏/电影功能 |

---

## 快速开始

### 方式一：在 AI 编程工具中直接调用（推荐）

1. 将此仓库克隆到本地：

```bash
git clone https://github.com/Tom6814/jmcomic-apk-mod-skill.git
```

2. 将 `jmcomic-apk-mod/SKILL.md` 放入你的 AI 编程工具（如 Trae、Cursor 等）的 Skill 目录

3. 将 JMComic3 APK 解包到工作目录

4. 在 AI 工具中调用 `jmcomic-apk-mod` Skill，按提示操作

### 方式二：手动参考技能文档

即使不使用 AI 辅助，`SKILL.md` 本身也是一份**完整的逆向修改手册**（800+ 行），包含：

- 广告链路追踪方法论（Module 8038 → adKey → Module 8284 → first_links）
- Webpack chunk 依赖分析与孤儿代码清理
- 5 个真实踩坑记录与避坑指南
- 6 类绝对不能触碰的核心功能区域（Cookie、暗色模式、阅读器等）
- 批量精确字符串替换的 Python 脚本模板
- 从 minified JS 中提取路由表、组件映射、广告位清单的排查脚本

---

## 工作原理

```
Skill 文件（结构化知识）
        ↓
    AI / LLM 解析
        ↓
  读取 APK 解包后的 JS chunk 文件
        ↓
  识别 Webpack 分块系统（n.e / n.bind）
        ↓
  追踪广告链路（adKey → Module 8038/8284）
        ↓
  精确字符串替换 + 孤儿 chunk 清理
        ↓
  验证（路由跳转、搜索功能、暗色模式、登录态）
```

---

## 安全性

Skill 内置了严格的误伤防护机制：

- **禁止触碰区域清单**：Cookie/登录态、亮暗色模式、漫画阅读器、Android 原生桥、网络请求层
- **操作安全守则**：修改前 grep 验证上下文、不删模棱两可的 chunk、每步提交 git
- **验证 Checklist**：分支 A 含 9 项检查、分支 B 含 8 项检查
- **删除前双重确认**：用 `n.e(CHUNK_ID)` 和 `n.bind(n, CHUNK_ID)` 验证无残留引用

---

## 背景

本 Skill 来源于 [JMComic3-APK-NO-Ads](https://github.com/Tom6814/JMComic3-APK-NO-Ads) 项目的实战经验。JMComic3 是一个基于 React + Webpack 的漫画阅读 Android 应用，对其进行逆向修改需要：

- 解包 APK，在数万行 minified JS 中追踪广告链路
- 逐个 Webpack chunk 修补，全量搜索防止遗漏
- 反复构建测试，排查白屏等误删问题

一次完整的去广告修改通常需要 **3-5 小时的密集排查和验证**。本 Skill 将整个过程系统化、自动化，降低到 **分钟级别**。

### 为什么是独立仓库

Skill 和 APK 源码是不同的产物，面向不同的受众：

- **[JMComic3-APK-NO-Ads](https://github.com/Tom6814/JMComic3-APK-NO-Ads)**（28MB+）— 给想要下载成品 APK 或研究具体代码的用户
- **本仓库**（18KB）— 给想要自己动手修改、适配新版本的用户

将 Skill 独立出来的理由与 `react-devtools` 独立于 `react` 仓库相同：**不同受众，不同仓库**。

---

## 目录结构

```
jmcomic-apk-mod-skill/
├── README.md
└── jmcomic-apk-mod/
    └── SKILL.md          # 核心 Skill 文件（805 行）
```

---

## 相关项目

- [JMComic3-APK-NO-Ads](https://github.com/Tom6814/JMComic3-APK-NO-Ads) — 修改后的 JMComic3 去广告版 APK 源码仓库，本 Skill 的实战来源

---

## 许可

本项目仅用于学习和研究目的。请勿将修改后的 APK 用于盈利或商业分发。
