# 第三章：Git & GitHub —— 版本控制从入门到实用

> 本章系统介绍 Git 的核心概念、安装配置、日常命令、分支管理，以及 GitHub 的使用，帮助你建立规范的代码管理习惯。

---

## 3.1 为什么需要版本控制

### 3.1.1 没有版本控制的痛苦

你有没有遇到过这些情况：

- 修改了文件，发现改错了，但"撤销"已经不够用了
- 存了一堆"最终版.docx"、"最终版2.docx"、"最终版_真的最终.docx"
- 和同学合作项目，互相覆盖对方的修改
- 想找到一周前某个功能还好用时的代码，找不到了

**版本控制就是为了解决这些问题而生的。**

### 3.1.2 Git 是什么

Git 是目前全球最流行的**分布式版本控制系统**，由 Linux 内核的作者 Linus Torvalds 于 2005 年创建。

它能做到：
- **记录每一次修改**：谁、什么时间、改了什么
- **随时回退**：任意回到历史上的某个版本
- **多人协作**：多人同时修改同一项目，不互相冲突
- **分支实验**：新功能在分支上开发，不影响主线

### 3.1.3 GitHub 是什么

GitHub 是全球最大的代码托管平台，基于 Git 构建。可以把它理解为：

> Git = 工具（本地使用）  
> GitHub = 云盘（把 Git 仓库存在网上，方便备份和分享）

---

## 3.2 Git 的核心概念

在开始操作之前，先理解几个关键词：

### 3.2.1 三个区域

```
工作区（Working Directory）
    ↓ git add
暂存区（Staging Area / Index）
    ↓ git commit
本地仓库（Local Repository）
    ↓ git push
远程仓库（Remote Repository，如 GitHub）
```

| 区域 | 说明 |
|------|------|
| 工作区 | 你直接编辑的文件夹，肉眼能看到的文件 |
| 暂存区 | 准备提交的文件"候选区"，git add 后进入 |
| 本地仓库 | 正式的历史记录库，git commit 后进入 |
| 远程仓库 | GitHub 上的仓库，git push 后同步 |

### 3.2.2 提交（Commit）

每次 `git commit` 就是一个"存档点"，包含：
- 本次修改的内容
- 提交时间
- 提交人
- 提交说明（你写的 message）

这些存档点串成一条时间线，就是项目的完整历史。

### 3.2.3 分支（Branch）

分支就像平行宇宙：主线（main）正常运行，你在另一条分支上做实验，不影响主线。实验成功后再合并回来。

```
main:    A → B → C → F（合并后）
                  ↘
feature:           D → E
```

---

## 3.3 安装与配置

### 3.3.1 安装 Git（Windows）

```powershell
winget install --id Git.Git -e --source winget
```

安装完成后验证：

```powershell
git --version
# 输出类似：git version 2.x.x
```

### 3.3.2 配置用户信息

安装后必须配置姓名和邮箱，这些信息会出现在每次提交记录里：

```powershell
git config --global user.name "你的名字"
git config --global user.email "你的邮箱@example.com"
```

查看已有配置：

```powershell
git config --list
```

### 3.3.3 配置默认编辑器（可选）

```powershell
# 设置为 VS Code 或 Cursor
git config --global core.editor "code --wait"
```

### 3.3.4 生成 SSH 密钥（连接 GitHub 用）

SSH 是一种安全的连接方式，配置一次后推送代码不需要每次输密码。

```powershell
# 第一步：生成密钥
ssh-keygen -t ed25519 -C "你的邮箱@example.com"
# 一路按回车，使用默认路径

# 第二步：查看公钥内容（复制这段内容）
cat ~/.ssh/id_ed25519.pub

# 第三步：把公钥添加到 GitHub
# 登录 GitHub → 右上角头像 → Settings → SSH and GPG keys → New SSH key
# 粘贴公钥内容，保存

# 第四步：测试连接
ssh -T git@github.com
# 成功会显示：Hi 你的用户名! You've successfully authenticated.
```

---

## 3.4 创建第一个仓库

### 3.4.1 方式一：本地初始化，再推到 GitHub

```powershell
# 新建文件夹并进入
mkdir my-project
cd my-project

# 初始化 Git 仓库
git init

# 创建一个文件
echo "# 我的项目" > README.md

# 添加到暂存区
git add .

# 提交
git commit -m "第一次提交"

# 关联 GitHub 远程仓库（先在 GitHub 上手动创建空仓库，复制 SSH 地址）
git remote add origin git@github.com:你的用户名/仓库名.git

# 推送
git branch -M main
git push -u origin main
```

### 3.4.2 方式二：从 GitHub 克隆到本地

```powershell
git clone git@github.com:你的用户名/仓库名.git
cd 仓库名
```

---

## 3.5 日常使用命令

### 3.5.1 查看状态与历史

```powershell
git status                  # 查看哪些文件修改了，哪些已暂存
git diff                    # 查看具体修改了什么内容
git log                     # 查看完整提交历史
git log --oneline           # 简洁版历史（一行一条）
git log --oneline --graph   # 带分支图的历史
```

### 3.5.2 标准提交流程

```powershell
git add .                   # 把所有修改加入暂存区
git add 文件名               # 只暂存某个文件
git commit -m "本次修改说明"  # 提交，写清楚做了什么
git push                    # 推送到 GitHub
```

**写好 commit message 的原则：**
- 说明"做了什么"，而不是"改了代码"
- 好的示例：`添加用户登录功能`、`修复首页图片加载失败的问题`
- 差的示例：`update`、`fix`、`改了一些东西`

### 3.5.3 从远程同步

```powershell
git pull            # 拉取远程最新内容并自动合并（= fetch + merge）
git fetch           # 只拉取，不合并，需要手动 merge
```

### 3.5.4 忽略不需要追踪的文件

在项目根目录创建 `.gitignore` 文件，写入不想被 Git 追踪的文件/文件夹：

```gitignore
# 示例 .gitignore

node_modules/       # Node.js 依赖包（很大，不需要上传）
.env                # 环境变量文件（含密码，不能上传！）
*.log               # 所有日志文件
dist/               # 编译输出目录
.DS_Store           # macOS 系统文件
Thumbs.db           # Windows 缩略图缓存
```

---

## 3.6 分支管理

### 3.6.1 基本分支操作

```powershell
git branch                  # 查看所有本地分支（当前分支前有 *）
git branch 分支名            # 创建新分支
git checkout 分支名          # 切换到某个分支
git checkout -b 分支名       # 创建并立即切换（常用）
git branch -d 分支名         # 删除分支（已合并才能删）
git branch -D 分支名         # 强制删除分支
```

### 3.6.2 合并分支

```powershell
# 先切换到目标分支（比如 main）
git checkout main

# 把另一个分支合并进来
git merge feature/登录功能
```

### 3.6.3 处理合并冲突

当两个分支修改了同一行代码，合并时会出现冲突：

```
<<<<<<< HEAD
这是 main 分支的内容
=======
这是 feature 分支的内容
>>>>>>> feature/登录功能
```

解决方法：
1. 手动编辑文件，删除 `<<<<<<<`、`=======`、`>>>>>>>` 标记，留下正确内容
2. `git add 冲突文件`
3. `git commit -m "解决合并冲突"`

### 3.6.4 推荐的分支命名规范

| 前缀 | 用途 | 示例 |
|------|------|------|
| `main` / `master` | 主分支，稳定版本 | `main` |
| `feature/` | 新功能开发 | `feature/用户登录` |
| `fix/` | Bug 修复 | `fix/首页加载问题` |
| `docs/` | 文档更新 | `docs/更新README` |

---

## 3.7 撤销与回退

### 3.7.1 撤销工作区修改（未 add）

```powershell
git restore 文件名           # 撤销某个文件的修改（恢复到上次 commit 的状态）
git restore .               # 撤销所有未暂存的修改
```

### 3.7.2 撤销暂存区（已 add，未 commit）

```powershell
git restore --staged 文件名  # 把文件从暂存区移出（不删除修改内容）
```

### 3.7.3 回退到历史版本

```powershell
git log --oneline           # 先查看历史，找到目标 commit 的 ID（如 abc1234）

git revert abc1234          # 安全回退：新建一个"撤销提交"（推荐，不破坏历史）

git reset --hard abc1234    # 强制回退：直接回到那个版本（会丢失之后的提交，谨慎使用）
```

### 3.7.4 暂存当前工作（Stash）

当你正在开发，突然需要去修复另一个 bug，但当前代码还没写完不想提交：

```powershell
git stash               # 把当前修改暂存起来，工作区恢复干净
git stash list          # 查看所有 stash
git stash pop           # 取出最近一次 stash，恢复修改
git stash drop          # 删除最近一次 stash
```

---

## 3.8 GitHub 使用指南

### 3.8.1 创建仓库

1. 登录 GitHub，点击右上角 `+` → New repository
2. 填写仓库名、描述，选择公开（Public）或私有（Private）
3. 可勾选"Add a README file"自动初始化
4. 点击 Create repository

### 3.8.2 README.md 的重要性

README 是别人看到你仓库时第一眼看到的文件，好的 README 包含：

```markdown
# 项目名称

一句话描述这个项目是做什么的。

## 安装方式
## 使用方法
## 目录结构
## 作者
```

### 3.8.3 Issues（问题追踪）

Issues 用于记录待办事项、bug、功能建议：

- 点击仓库页面的 `Issues` 标签
- 点击 `New issue` 新建
- 可以打标签（bug、enhancement、question 等）
- 解决后关闭 Issue

### 3.8.4 Pull Request（PR）

PR 是多人协作的核心流程：

```
1. Fork 别人的仓库（复制一份到自己账号下）
2. clone 到本地，创建新分支
3. 修改代码，push 到自己的 fork
4. 在 GitHub 上发起 Pull Request
5. 原作者审核，同意后合并到主仓库
```

### 3.8.5 GitHub Pages（免费发布网页）

可以把仓库直接变成一个网站：

1. 仓库里放 `index.html`
2. 仓库 Settings → Pages
3. 选择 main 分支，保存
4. 几分钟后访问 `https://你的用户名.github.io/仓库名`

---

## 3.9 常见问题与解决

### 提示 "dubious ownership"（安全警告）

```powershell
git config --global --add safe.directory 你的目录路径
# 示例：
git config --global --add safe.directory E:/practice
```

### push 时提示权限拒绝

原因：SSH 密钥没有配置好，或远程地址用的是 HTTPS 而不是 SSH。

```powershell
# 查看当前远程地址
git remote -v

# 改为 SSH 地址
git remote set-url origin git@github.com:用户名/仓库名.git
```

### 提交后发现 commit message 写错了

```powershell
# 修改最近一次提交的说明（前提是还没有 push）
git commit --amend -m "正确的说明"
```

### 误删文件，想找回来

```powershell
# 恢复已删除但未提交的文件
git restore 文件名

# 找回之前某次提交里的文件
git checkout 提交ID -- 文件名
```

---

## 3.10 工作流总结

### 个人项目日常流程

```
修改文件
  → git status（查看改了什么）
  → git add .（暂存）
  → git commit -m "说明"（提交）
  → git push（同步到 GitHub）
```

### 多人协作流程

```
git pull（先同步最新代码）
  → git checkout -b feature/新功能（创建分支）
  → 写代码
  → git add . && git commit -m "说明"
  → git push origin feature/新功能
  → 在 GitHub 上发起 Pull Request
  → 同事 Review 后合并
```

---

## 3.11 本章小结

| 要点 | 内容 |
|------|------|
| Git 是什么 | 版本控制工具，记录文件修改历史 |
| 三个区域 | 工作区 → 暂存区 → 本地仓库 → 远程仓库 |
| 核心命令 | add / commit / push / pull / branch / merge |
| 撤销回退 | restore / revert / reset / stash |
| GitHub | 代码云托管 + 协作平台，免费无限公开仓库 |
| 好习惯 | 勤 commit、写清楚 message、用 .gitignore |
