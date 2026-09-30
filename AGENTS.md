# AGENTS.md — mvision-privacy 开发规则

## 项目基本准则
1. **最小侵入原则 (Minimal Invasion)**：只修改与当前问题直接相关的代码，不随意破坏已有稳定逻辑。
2. **禁止自动提交**：修改、调试、修复代码后，严禁自动执行 `git commit` 或 `git push`。
3. **中文沟通**：所有回复、文档与日志必须使用中文。

<!-- REPOMIX_START -->
## 🤖 AI 上下文分析与 Repomix 规范 (AI Context & Repomix Policy)

本模块已全面接入 Repomix 自动化代码上下文体系，深度适配 **Gemini（1.5 Pro / 2.0 / Advanced）** 1M~2M 超大长上下文模型，支持无损进行全架构审视、跨工程功能迁移与缺陷排查。

### 1. 核心分析包路径
- 📄 **全量源码包**：`output_repomix/mvision-privacy-full.xml`（包含完整代码实现，适合功能重构、查 Bug 与深度推演）
- 🦴 **骨架结构包**：`output_repomix/mvision-privacy-structure.xml`（剥离函数实现体，仅保留类型、协议与接口签名，节省 70% Token，适合宏观架构推演）

### 2. 新功能刷新与同步机制
当本模块完成新功能开发、核心逻辑重构或发布前，**必须执行刷新以确保 AI 认知与代码 100% 同步**：
```bash
# 在工作区根目录下执行：
./analyze.sh mvision-privacy          # 刷新本模块分析包
./analyze.sh mvision-privacy --copy   # 刷新并将全量代码放入剪贴板 (Gemini 网页直接 Cmd+V)
./analyze.sh mvision-privacy --sync   # 刷新分析包并同步更新本开发规则
./analyze.sh all --sync      # 一键全量刷新全部子模块
```

### 3. 上下文与工程隔离准则
- 🚫 **严禁 Git 污染**：打包产生的 XML 文件严禁提交至 Git 仓库（已在根目录 `.gitignore` 隔离）。
- 🚫 **禁止自动提交**：任何代码修改完成后直接告知用户，由用户手动提交或明确要求后再进行 commit，严禁自动执行 `git commit` 或 `git push`。
- 🕒 **最新分析同步时间**：2026-09-28 09:39:44
<!-- REPOMIX_END -->

---

## 🧩 全矩阵公共组件库规范 (CommonComponents Integration)

本项目作为全矩阵子模块，必须深度复用工作区根目录的公共组件库 `CommonComponents/`。
新增特性或重构页面时，**必须首先读取公共组件开发指南，严禁重复造轮子**：
👉 **[`CommonComponents 全矩阵公共组件库统一开发指南`](../CommonComponents/README.md)**

### 现有核心公共组件（必须优先使用）：
1. **`GlassBackground`** ([`CommonComponents/GlassBackground/GlassBackgroundView.swift`](../CommonComponents/GlassBackground/GlassBackgroundView.swift))
   - 支持 `tvOS 26.0+` 系统原生 `UIGlassEffect` 液态高透玻璃、`visionOS` 空间计算原生玻璃与低版本三层超薄毛玻璃降级。
   - 标准调用：`.glassPanelBackground(cornerRadius: 24, style: .automatic)` / `.glassBackGroundIfAvailable(...)`。
2. **`MAppStore`** ([`CommonComponents/MAppStore/MAppStoreView.swift`](../CommonComponents/MAppStore/MAppStoreView.swift))
   - Apple 黄金比例详情页、大图轮播、焦点闭环双向穿透与 TestFlight 专属弹窗。
3. **`ActivationGuard`** ([`CommonComponents/ActivationGuard/`](../CommonComponents/ActivationGuard/))
   - 本地 HTTP 免责激活防护与局域网服务。

> **动态感知机制**：后续当公共组件库在 `CommonComponents/` 扩展新增播放器、网络或大屏 UI 组件时，请直接查阅上方 `CommonComponents/README.md` 指南进行无缝集成与代码平替。

