# CCPM + Ralph 集成工作流指南

> **目标**: 让 Claude Code 清楚理解如何结合使用 CCPM 和 Ralph 进行项目管理

---

## 🎯 核心概念

**CCPM 和 Ralph 是互补的工具，不是竞争关系！**

```
CCPM (大脑) → Ralph (双手) → CCPM (眼睛) → Ralph (持续改进)
```

### 工具定位

| 维度 | CCPM | Ralph |
|------|------|-------|
| **角色** | **项目规划师** | **自主开发者** |
| **主要用途** | 项目规划和任务分解 | 自主代码开发循环 |
| **工作方式** | 规范驱动 (PRD → Epic → Tasks) | 迭代驱动 (循环直到完成) |
| **输入** | 用户需求、想法 | GitHub Issues、任务描述 |
| **输出** | 结构化文档、GitHub Issues | 实际代码、git提交 |
| **适用阶段** | 需求分析、架构设计 | 功能实现、bug修复 |
| **GitHub集成** | 深度集成 (创建Issues) | 轻量集成 (跟踪进度) |
| **团队协作** | 强 (共享文档、Issues) | 弱 (单人开发循环) |
| **思维模式** | **结构化规划** | **持续执行** |

---

## 🔄 完整集成工作流

### 标准开发流程

```
阶段1: 需求规划 (CCPM)
  ↓
阶段2: 技术设计 (CCPM)  
  ↓
阶段3: 任务分解 (CCPM)
  ↓
阶段4: GitHub同步 (CCPM)
  ↓
阶段5: 自主执行 (Ralph)
  ↓
阶段6: 进度跟踪 (CCPM + Ralph)
  ↓
阶段7: 完成交付 (CCPM)
```

---

## 📋 详细工作步骤

### 阶段1: 需求规划 (CCPM主导)

**触发**: 用户有新功能想法或需求

```bash
# 用户输入示例
"我要为项目添加用户认证功能"
"我想优化数据库查询性能"
"需要实现实时消息推送"
```

**CCPM执行**:
1. 引导式需求收集
2. 创建 PRD 文档: `.claude/prds/<feature-name>.md`
3. 包含问题陈述、用户故事、功能需求、成功标准

### 阶段2: 技术设计 (CCPM主导)

**触发**: PRD 已创建

```bash
# 用户输入
"把 user-authentication PRD 转换为 Epic"
"解析用户认证 PRD"
```

**CCPM执行**:
1. 分析 PRD 技术可行性
2. 创建技术 Epic: `.claude/epics/<feature-name>/epic.md`
3. 包含架构决策、技术方案、实现策略

### 阶段3: 任务分解 (CCPM主导)

**触发**: Epic 已创建

```bash
# 用户输入
"分解 user-authentication Epic"
"把用户认证Epic分解成任务"
```

**CCPM执行**:
1. 识别并行化机会
2. 创建任务文件: `.claude/epics/<feature-name>/001.md`, `002.md`...
3. 设置依赖关系和并行标志

**输出示例**:
```bash
.claude/epics/user-authentication/
├── epic.md
├── 001.md  # [环境配置] 并行任务
├── 002.md  # [数据库设计] 并行任务
├── 003.md  # [认证API] 依赖002
├── 004.md  # [前端组件] 并行任务
└── 005.md  # [集成测试] 依赖003,004
```

### 阶段4: GitHub同步 (CCPM主导)

**触发**: 任务已分解完成

```bash
# 用户输入
"同步 user-authentication Epic 到 GitHub"
"推送用户认证任务到 GitHub"
```

**CCPM执行**:
1. 创建 Epic Issue (主任务)
2. 创建子 Issue (各个任务)
3. 设置标签、依赖关系
4. 创建 git worktree

**输出示例**:
```bash
# GitHub Issues 创建
✅ Epic Issue #123: "Epic: 用户认证系统"
✅ Task Issue #124: "数据库用户表设计"
✅ Task Issue #125: "JWT认证实现"
✅ Task Issue #126: "前端登录组件"
✅ Task Issue #127: "集成测试"
```

### 阶段5: 自主执行 (Ralph主导)

**触发**: GitHub Issues 已创建

```bash
# 用户输入
ralph --github-issue 124 --monitor
# 或
ralph --github-issue 125 --calls 50 --live
```

**Ralph执行**:
1. **分析阶段**: 读取 GitHub Issue 详细需求
2. **规划阶段**: 制定实现计划
3. **编码循环**: 
   - 阅读 `.ralph/PROMPT.md` 开发指导
   - 执行代码编写
   - 运行测试验证
   - 提交代码到 git
   - 更新 GitHub Issue 进度
4. **完成检测**: 智能判断任务是否完成
5. **自动标记**: 更新 Issue 状态为完成

### 阶段6: 进度跟踪 (混合模式)

**CCPM进度跟踪**:

```bash
# 用户输入
"用户认证项目的进度如何？"
"我们的 standup 状态？"
```

**CCPM执行**:
1. 读取所有任务状态
2. 生成进度报告
3. 识别阻塞问题
4. 显示下一步行动

### 阶段7: 完成交付 (CCPM主导)

**触发**: 所有任务完成

```bash
# 用户输入
"合并 user-authentication Epic"
"用户认证功能完成了？"
```

**CCPM执行**:
1. 验证所有任务完成状态
2. 运行完整测试套件
3. 合并 worktree 到主分支
4. 关闭所有相关 Issues
5. 归档 Epic 文档

---

## 🛠️ 实际使用示例

### 示例1: 新功能开发 (完整流程)

```bash
# 1. CCPM 规划
"我想为 SDXLTurbo 项目添加批量图片生成功能"

# CCPM 自动执行:
✅ 创建 PRD: batch-image-generation.md
✅ 引导需求收集 (用户故事、技术约束)
✅ 生成结构化需求文档

# 2. CCPM 技术设计
"把 batch-image-generation PRD 转换为 Epic"

# CCPM 自动执行:
✅ 创建技术 Epic: .claude/epics/batch-image-generation/epic.md
✅ 分析技术可行性 (StreamDiffusion批量推理)
✅ 设计架构方案

# 3. CCPM 任务分解
"分解 batch-image-generation Epic"

# CCPM 自动执行:
✅ 创建任务文件:
  - 001.md: 批量推理接口设计 [并行]
  - 002.md: 内存优化策略 [并行]
  - 003.md: 进度条UI组件 [并行]
  - 004.md: 批量处理逻辑 [依赖001]
  - 005.md: 性能测试 [依赖002,004]

# 4. CCPM GitHub同步
"同步 batch-image-generation 到 GitHub"

# CCPM 自动执行:
✅ 创建 Epic Issue #140
✅ 创建子 Issues: #141, #142, #143, #144, #145
✅ 设置标签: epic, batch, feature
✅ 创建 worktree: ../epic-batch-image-generation/

# 5. Ralph 执行
cd ../epic-batch-image-generation/
ralph --github-issue 141 --monitor

# Ralph 自动执行:
✅ 读取 Issue #141 需求
✅ 分析现有代码结构
✅ 实现批量推理接口
✅ 编写单元测试
✅ git commit -m "Issue #141: 实现批量推理接口"
✅ 更新 GitHub Issue #141 进度
✅ 智能检测完成并标记

# 6. 继续下一个任务
ralph --github-issue 142 --monitor
# 重复执行直到所有任务完成

# 7. CCPM 进度跟踪
"批量图片生成功能的进度如何？"

# CCPM 自动报告:
📊 Epic: 批量图片生成 总进度: 40% (2/5 任务完成)
```

### 示例2: Bug修复流程

```bash
# 1. CCPM 记录Bug
"发现 StreamDiffusion 推理时内存泄漏，每推理10张图片内存增长1GB"

# CCPM 自动执行:
✅ 创建 Bug 任务: .claude/epics/sdxlturbo-streamdiffusion/bug-memory-leak.md
✅ 分析Bug影响范围
✅ 设置优先级: P0 (高)

# 2. GitHub同步
"同步内存泄漏Bug到 GitHub"

# CCPM 自动执行:
✅ 创建 Bug Issue #150: "Bug: StreamDiffusion内存泄漏"
✅ 设置标签: bug, memory, P0

# 3. Ralph修复
ralph --github-issue 150 --monitor

# Ralph 自动执行:
✅ 分析内存泄漏原因 (tensor未释放)
✅ 实现修复方案 (添加gc.collect())
✅ 编写回归测试
✅ 验证修复效果
✅ 提交代码
✅ 关闭 Issue #150
```

---

## 🔧 配置和设置

### CCPM 配置结构

```
.claude/
├── prds/                           # 产品需求文档
├── epics/                          # 技术史诗和任务
│   ├── user-authentication/
│   │   ├── epic.md                # 技术设计文档
│   │   ├── 001.md                 # 任务1
│   │   ├── github-mapping.md      # Issue映射关系
│   │   └── updates/               # 进度更新
└── context/                        # 项目上下文
```

### Ralph 配置结构

```
.ralph/
├── PROMPT.md                       # 主开发提示
├── fix_plan.md                     # 任务清单
├── AGENT.md                        # 构建运行说明
├── status.json                      # 实时状态
└── logs/                          # 执行日志
```

---

## 💡 最佳实践

### 1. 明确的工具选择

| 使用场景 | 推荐工具 | 理由 |
|---------|----------|------|
| **需求分析** | CCPM | 结构化需求收集，团队共享 |
| **架构设计** | CCPM | 技术决策文档，依赖关系管理 |
| **任务分解** | CCPM | 并行化识别，优先级排序 |
| **GitHub Issues** | CCPM | 批量创建，标签管理 |
| **代码实现** | Ralph | 自主编码，智能完成检测 |
| **Bug修复** | Ralph | 快速定位，自动测试 |
| **进度报告** | CCPM | 多项目视图，团队共享 |

### 2. 工作流优化

**小型项目 (1-3天)**:
```bash
# 简化流程
1. "我要实现功能X" → CCPM快速PRD
2. Ralph直接执行 → ralph --prompt "功能X"
3. 手动GitHub更新
```

**中型项目 (1-2周)**:
```bash
# 标准流程
1. CCPM完整规划 (PRD → Epic → Tasks)
2. CCPM GitHub同步
3. Ralph逐个执行任务
4. CCPM进度跟踪
```

**大型项目 (1个月+)**:
```bash
# 完整流程 + 阶段性检查
1. CCPM详细规划
2. CCPM阶段性Epic (按模块分解)
3. Ralph并行执行 (多Issue)
4. CCPM每周standup
5. CCPM里程碑验证
```

### 3. 集成命令速查

```bash
# CCPM规划阶段
"创建 {功能名} 的PRD"
"把 {PRD名} 转换为Epic"
"分解 {Epic名}"
"同步 {Epic名} 到GitHub"

# Ralph执行阶段
ralph --github-issue <issue_number>
ralph --monitor                    # 带监控面板
ralph --calls 50 --live            # 实时输出

# CCPM跟踪阶段
"项目状态如何？"
"运行standup"
"什么被阻塞了？"
"下一步做什么？"
```

---

## 🚀 快速开始

### 第一次使用

```bash
# 1. 确认环境
gh auth status          # 检查GitHub认证
ralph --help            # 确认Ralph安装

# 2. 创建项目
cd my-project
ralph-enable            # 启用Ralph

# 3. 开始规划
"我要实现用户认证功能"  # CCPM开始工作

# 4. 执行开发
ralph --github-issue 123 --monitor  # Ralph开始工作
```

---

## 📚 总结

**核心原则**:

1. **CCPM = 项目大脑**: 负责规划、设计、分解、跟踪
2. **Ralph = 开发双手**: 负责编码、测试、优化、执行
3. **GitHub = 协作桥梁**: Issues作为数据交换中心
4. **Git = 版本控制**: 代码提交和分支管理

**成功关键**:

- ✅ **明确分工**: 规划用CCPM，执行用Ralph
- ✅ **数据同步**: GitHub Issues作为单一数据源
- ✅ **渐进采用**: 从简单流程开始，逐步完善
- ✅ **团队共识**: 所有成员理解工具定位

**避免混淆**:

- ❌ 不要用Ralph做需求规划 (它不擅长结构化思考)
- ❌ 不要用CCPM写代码 (它不是自主开发工具)
- ❌ 不要跳过GitHub同步 (失去团队协作基础)
- ❌ 不要混合使用不同项目管理工具 (造成数据混乱)

---

**记住**: CCPM和Ralph是**伙伴工具**，不是替代关系！正确结合使用可以极大提升开发效率。

*下次Claude Code看到这个文档时，应该清楚理解：*
- *什么时候用CCPM*
- *什么时候用Ralph* 
- *如何让它们协同工作*
- *完整的项目管理流程*