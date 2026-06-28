# CCPM + Ralph 本地化工作流指南

> **完全本地化的项目管理方案** - 无需 GitHub，基于本地 git 和文件系统

---

## 🎯 核心理念

**本地优先，远程可选** - 90% 的功能可以在本地完成！

```
本地需求 (CCPM) → 本地规划 (CCPM) → 本地执行 (Ralph) → 本地提交 (Git) → 本地跟踪 (CCPM)
```

### GitHub 依赖分析

| 功能阶段 | CCPM | Ralph | GitHub依赖 | 可本地化 |
|---------|------|-------|-----------|---------|
| **需求规划** | ✅ 主导 | - | ❌ 无需 | ✅ 100% |
| **技术设计** | ✅ 主导 | - | ❌ 无需 | ✅ 100% |
| **任务分解** | ✅ 主导 | - | ❌ 无需 | ✅ 100% |
| **GitHub同步** | ✅ 主导 | - | ✅ **必需** | ❌ 0% |
| **代码执行** | - | ✅ 主导 | ❌ 无需 | ✅ 100% |
| **进度跟踪** | ✅ 主导 | ✅ 辅助 | ⚠️ 部分 | ✅ 80% |
| **代码提交** | - | ✅ 主导 | ❌ 无需 | ✅ 100% |

**结论**：除了 CCPM 的 Sync 阶段，所有功能都可以在本地完成！

---

## 🔄 本地化工作流

### 完全本地流程

```
阶段1: 本地需求规划 (CCPM)
  ↓
阶段2: 本地技术设计 (CCPM)  
  ↓
阶段3: 本地任务分解 (CCPM)
  ↓
【跳过】阶段4: GitHub同步 (CCPM) ← 本地工作流跳过此步骤
  ↓
阶段5: 本地自主执行 (Ralph)
  ↓
阶段6: 本地进度跟踪 (CCPM + Ralph)
  ↓
阶段7: 本地完成交付 (CCPM)
```

---

## 📋 详细本地工作步骤

### 阶段1: 本地需求规划 (CCPM主导)

**完全本地化，无需 GitHub**

```bash
# 用户输入
"我要为项目添加用户认证功能"

# CCPM 本地执行
✅ 分析需求并提问
✅ 创建本地 PRD: .claude/prds/user-authentication.md
✅ 所有操作基于本地文件系统
```

**输出结构**:
```markdown
.claude/prds/user-authentication.md
---
name: user-authentication
description: "实现用户注册、登录和权限管理"
status: backlog
created: 2025-01-15T10:00:00Z
---

# PRD: 用户认证系统
## 问题陈述
## 用户故事  
## 功能需求
...
```

### 阶段2: 本地技术设计 (CCPM主导)

**完全本地化，无需 GitHub**

```bash
# 用户输入
"把 user-authentication PRD 转换为 Epic"

# CCPM 本地执行
✅ 读取本地 PRD 文件
✅ 分析技术可行性
✅ 创建本地 Epic: .claude/epics/user-authentication/epic.md
```

**输出结构**:
```markdown
.claude/epics/user-authentication/
├── epic.md                    # 技术设计文档
├── 001.md                     # 任务文件
├── 002.md
└── 003.md
```

### 阶段3: 本地任务分解 (CCPM主导)

**完全本地化，无需 GitHub**

```bash
# 用户输入
"分解 user-authentication Epic"

# CCPM 本地执行
✅ 读取本地 epic.md
✅ 创建任务文件: 001.md, 002.md, 003.md
✅ 设置本地依赖关系
✅ 识别并行化机会
```

### 【跳过】阶段4: GitHub同步

**本地工作流跳过此阶段**

```bash
# ❌ 不执行 GitHub 同步
# "同步到 GitHub"  ← 本地工作流跳过

# ✅ 替代方案：本地任务跟踪
echo "任务已准备就绪，可以开始本地执行"
```

**本地替代方案**:
- ❌ 不创建 GitHub Issues
- ❌ 不使用 gh CLI
- ✅ 保留本地任务文件
- ✅ 使用本地 git 分支
- ✅ 基于文件名的任务跟踪

### 阶段5: 本地自主执行 (Ralph主导)

**完全本地化，无需 GitHub**

```bash
# 用户输入
ralph --monitor

# Ralph 本地执行
✅ 读取本地 .ralph/PROMPT.md
✅ 分析本地任务文件
✅ 执行代码开发
✅ 提交到本地 git
✅ 更新本地状态文件
```

**Ralph 本地配置**:
```bash
# 不使用 GitHub 相关参数
ralph --monitor              # ✅ 本地监控
ralph --calls 50             # ✅ 本地API限制
ralph --live                 # ✅ 本地实时输出

# 不使用这些参数（需要GitHub）
# ralph --github-issue 123   # ❌ 跳过GitHub集成
# ralph --create-pr          # ❌ 跳过GitHub PR
```

### 阶段6: 本地进度跟踪 (混合模式)

**大部分本地化，无需 GitHub**

```bash
# 用户输入
"用户认证项目的进度如何？"

# CCPM 本地执行
✅ 读取本地任务文件: .claude/epics/*/00*.md
✅ 检查本地 git 状态
✅ 分析本地文件修改
✅ 生成本地进度报告
```

### 阶段7: 本地完成交付 (CCPM主导)

**完全本地化，无需 GitHub**

```bash
# 用户输入
"用户认证功能完成了？"

# CCPM 本地执行
✅ 验证所有本地任务完成状态
✅ 检查本地 git 提交历史
✅ 运行本地测试套件
✅ 合并本地分支
✅ 生成本地交付报告
```

---

## 🛠️ 实际本地使用示例

### 示例1: 完全本地化的新功能开发

```bash
# 1. CCPM 本地规划
"我要为项目添加批量图片生成功能"

# CCPM 本地执行
✅ 创建: .claude/prds/batch-generation.md
✅ 不需要任何网络连接

# 2. CCPM 本地技术设计
"把 batch-generation PRD 转换为 Epic"

# CCPM 本地执行  
✅ 创建: .claude/epics/batch-generation/epic.md
✅ 纯本地文件操作

# 3. CCPM 本地任务分解
"分解 batch-generation Epic"

# CCPM 本地执行
✅ 创建任务文件: 001.md, 002.md, 003.md
✅ 设置本地依赖关系

# 4. 【跳过】GitHub同步
# 不执行任何GitHub相关操作

# 5. Ralph 本地执行
ralph --monitor

# Ralph 本地执行
✅ 读取: .ralph/PROMPT.md
✅ 分析: .claude/epics/batch-generation/001.md
✅ 执行: 代码开发
✅ 提交: 本地git commit
✅ 更新: .ralph/status.json

# 6. CCPM 本地进度跟踪
"批量图片生成功能的进度如何？"

# CCPM 本地执行
✅ 读取: .claude/epics/batch-generation/local-status.md
✅ 检查: 本地git状态
✅ 生成: 本地进度报告
```

### 示例2: 大型ML项目本地开发

```bash
# 1. 初始化本地项目
mkdir ml-large-project && cd ml-large-project
git init
ralph-enable

# 2. 配置大文件处理
cat > .gitignore << 'EOF'
*.pth                  # 模型文件
*.bin                  # 二进制文件
data/datasets/         # 数据集
models/checkpoints/    # 检查点
.cache/                # 缓存
EOF

# 3. CCPM 本地规划
"我要实现一个大型语言模型训练系统"

# CCPM 本地执行
✅ 创建PRD: .claude/prds/llm-training.md
✅ 创建Epic: .claude/epics/llm-training/epic.md
✅ 分解任务: 001.md到020.md (20个任务)

# 4. Ralph 本地执行大项目
ralph --calls 200 --monitor

# Ralph 处理大项目
✅ 自动识别大文件策略
✅ 智能git提交 (跳过大文件)
✅ 本地状态跟踪
✅ 不需要上传到GitHub

# 5. 本地进度跟踪
"大模型训练项目的进度？"

# CCPM 本地报告
📊 大型项目本地进度: 45% (9/20任务)
💾 本地磁盘使用: 45GB / 100GB
🎯 下一步: 优化数据加载管道
```

---

## 🔧 本地化配置

### 项目目录结构

```
project/
├── .claude/              # CCPM 本地工作区
│   ├── prds/             # 本地PRD文档
│   ├── epics/            # 本地Epic和任务
│   └── context/          # 本地上下文
├── .ralph/               # Ralph 本地工作区
│   ├── PROMPT.md         # 本地开发提示
│   ├── fix_plan.md       # 本地任务清单
│   ├── status.json       # 本地实时状态
│   └── logs/             # 本地日志
├── .git/                 # 本地git仓库
└── src/                  # 项目源代码
```

### 本地任务跟踪

**替代 GitHub Issues 的方案**:

```markdown
## local-status.md (本地状态文件)
---
last_updated: 2025-01-15T14:30:00Z
total_tasks: 5
completed_tasks: 3
progress_percentage: 60
---

# 本地任务状态

## 任务清单
- [x] [001] 数据库用户表设计 ✅
- [x] [002] JWT认证实现 ✅  
- [x] [003] 前端登录组件 ✅
- [ ] [004] 集成测试 🔄 进行中
- [ ] [005] 部署文档 ⏸ 待开始
```

### 本地Git工作流

```bash
# 创建本地任务分支
git checkout -b task/001-database-schema
# Ralph 在此分支开发
# 完成后合并到feature分支
git checkout feature/user-auth
git merge task/001-database-schema

# 功能分支合并
git checkout main
git merge feature/user-auth
```

---

## 💡 本地化最佳实践

### 大文件处理策略

```bash
# .gitignore 配置
# 大模型文件
*.pth
*.bin
*.safetensors

# 数据集
data/datasets/
data/raw/

# 缓存文件
.cache/
__pycache__/
*.pyc

# 环境配置
.env
secrets/
```

### 本地备份策略

```bash
# 定期本地备份
git commit -m "本地备份点"
git tag v1.0-backup-$(date +%Y%m%d)

# 使用git bundle打包
git bundle create /backup/project-$(date +%Y%m%d).git HEAD

# 压缩项目目录
tar -czf /backup/project-$(date +%Y%m%d).tar.gz ./
```

---

## 📊 本地化 vs 远程化对比

### 功能对比

| 功能 | 本地工作流 | GitHub工作流 | 差异说明 |
|------|-----------|-------------|---------|
| **需求规划** | ✅ 完整 | ✅ 完整 | 无差异 |
| **技术设计** | ✅ 完整 | ✅ 完整 | 无差异 |
| **任务分解** | ✅ 完整 | ✅ 完整 | 无差异 |
| **代码执行** | ✅ 完整 | ✅ 完整 | 无差异 |
| **进度跟踪** | ✅ 80% | ✅ 100% | 缺少团队协作 |
| **大文件处理** | ✅ 无限制 | ⚠️ 受限制 | 本地更优 |
| **网络依赖** | ✅ 离线 | ❌ 联网 | 本地更灵活 |
| **隐私安全** | ✅ 完全控制 | ⚠️ 依赖GitHub | 本地更安全 |

### 适用场景

**选择本地工作流**:
- ✅ 个人项目
- ✅ 大型项目（上传慢）
- ✅ 敏感项目（不适合公开）
- ✅ 离线开发环境
- ✅ 快速原型开发

**选择远程工作流**:
- ✅ 多人协作团队
- ✅ 开源项目
- ✅ 需要远程访问
- ✅ 需要团队审查

---

## 🔌 混合模式推荐

**最佳方案：本地开发 + 选择性同步**

```bash
# 阶段1: 本地开发 (90%时间)
- CCPM本地规划
- Ralph本地执行
- 本地git提交
- 本地进度跟踪

# 阶段2: 选择性同步 (10%时间)
- 重要里程碑同步到GitHub
- 发布版本时创建GitHub Release
- 需要协作时同步特定分支
```

---

## 🚀 本地化快速开始

### 第一次本地使用

```bash
# 1. 创建本地项目
mkdir my-local-project && cd my-local-project
git init
ralph-enable

# 2. 开始本地规划
"我要实现用户认证功能"  # CCPM本地工作

# 3. 开始本地开发
ralph --monitor          # Ralph本地执行

# 4. 查看本地进度
"项目进度如何？"          # CCPM本地报告
```

---

## 📚 总结

### 本地工作流的核心优势

1. **✅ 完全控制** - 所有数据和代码都在本地
2. **✅ 无网络依赖** - 完全离线工作
3. **✅ 无大小限制** - 处理超大项目
4. **✅ 更快速度** - 无网络延迟
5. **✅ 隐私安全** - 敏感代码不外泄

### 核心结论

**CCPM + Ralph 的本地工作流不仅可行，而且在很多方面更优秀！**

- ✅ 90%的功能完全本地化
- ✅ 保留了所有核心开发能力
- ✅ 去除了不必要的网络依赖
- ✅ 提供了更好的性能和控制

**记住**：GitHub 是可选的增强功能，不是必需的基础依赖！