$ cat "/home/user/GYJ-1/ClaudeCode/ClaudeCode制作网站.md"

# 第四章：用 Claude Code 制作网站

> 本章从零开始，带你用 Claude Code 在终端里指挥 AI 完成一个完整的个人主页网站，涵盖项目初始化、页面开发、样式美化，以及发布到 GitHub Pages 全流程。

---

## 4.1 准备工作

### 4.1.1 环境确认

在开始之前，确认以下工具已安装：

```powershell
node --version      # 需要 v18 或更高
git --version       # 需要 2.x
claude --version    # Claude Code 已安装
```

如果 Claude Code 还没安装，执行：

```powershell
npm install -g @anthropic-ai/claude-code
```

### 4.1.2 创建项目文件夹

```powershell
# 在你喜欢的位置新建项目文件夹
mkdir my-website
cd my-website

# 初始化 Git 仓库
git init

# 启动 Claude Code
claude
```

---

## 4.2 让 Claude Code 初始化项目

进入 Claude Code 后，直接用中文告诉它你要做什么：

```
> 帮我创建一个个人主页网站，包含：首页、关于我、项目展示三个页面，用纯 HTML + CSS 实现，不需要任何框架
```

Claude Code 会自动：
1. 创建 `index.html`（首页）
2. 创建 `about.html`（关于我）
3. 创建 `projects.html`（项目展示）
4. 创建 `style.css`（样式文件）

### 4.2.1 查看生成的文件结构

```
> 帮我列出当前文件夹的所有文件
```

标准项目结构如下：

```
my-website/
├── index.html        ← 首页
├── about.html        ← 关于我
├── projects.html     ← 项目展示
├── style.css         ← 全局样式
└── README.md         ← 项目说明
```

---

## 4.3 开发首页（index.html）

### 4.3.1 让 Claude Code 生成首页内容

```
> 帮我完善 index.html，包含：
> 1. 顶部导航栏，链接到三个页面
> 2. 居中的英雄区，显示姓名和一句话简介
> 3. 底部版权信息
> 风格简洁现代，配色用深色主题
```

Claude Code 会直接修改文件，你只需要在浏览器里刷新查看效果。

### 4.3.2 用浏览器实时预览

```powershell
# 方法一：直接双击 index.html 用浏览器打开
# 方法二：用 VS Code / Cursor 的 Live Server 插件
# 方法三：用 Python 启动本地服务器
python -m http.server 8080
# 然后浏览器访问 http://localhost:8080
```

### 4.3.3 修改内容

在 Claude Code 里直接说：

```
> 把首页的姓名改成"张三"，简介改成"前端开发者 | 热爱开源"
```

```
> 导航栏的链接颜色改成白色，鼠标悬停时变成浅蓝色
```

---

## 4.4 开发"关于我"页面

```
> 帮我完善 about.html，包含：
> 1. 个人头像区（用一个圆形的占位图代替）
> 2. 自我介绍段落，150 字左右
> 3. 技能列表，展示 HTML、CSS、JavaScript、Git 四项技能，用进度条样式显示
```

### 4.4.1 添加技能进度条

如果对效果不满意，可以继续调整：

```
> 技能进度条改成圆环样式，每个技能用不同颜色
```

```
> 在技能部分下面添加一个"学习历程"时间轴，从 2024 年开始
```

---

## 4.5 开发"项目展示"页面

```
> 帮我完善 projects.html，包含：
> 1. 网格布局，每行显示 3 个项目卡片
> 2. 每张卡片包含：项目名称、简短描述、技术标签、GitHub 链接按钮
> 3. 卡片鼠标悬停时有轻微上浮动画效果
> 4. 先放 3 个示例项目作为占位
```

### 4.5.1 添加筛选功能

```
> 在项目网格上方添加筛选按钮，可以按技术标签筛选项目，用纯 JavaScript 实现
```

---

## 4.6 美化全局样式

### 4.6.1 让 Claude Code 优化整体视觉

```
> 帮我优化 style.css：
> 1. 字体改用 Google Fonts 的 "Inter" 字体
> 2. 添加页面滚动时导航栏固定在顶部的效果
> 3. 所有页面切换时添加淡入动画
> 4. 移动端适配，手机上导航变成汉堡菜单
```

### 4.6.2 响应式设计检查

```
> 帮我检查三个页面的响应式布局，确保在手机（375px）、平板（768px）、桌面（1280px）三种宽度下都能正常显示
```

---

## 4.7 让 Claude Code 审查和优化代码

### 4.7.1 代码质量检查

```
> 帮我检查所有 HTML 文件，找出语义化标签使用不规范的地方并修复
```

```
> 帮我检查 style.css，删除重复的样式规则，合并可以复用的部分
```

### 4.7.2 性能优化

```
> 帮我优化网站性能：
> 1. 检查图片是否有 alt 属性
> 2. CSS 和 JS 文件是否放在正确位置
> 3. 给 <head> 添加必要的 meta 标签（viewport、description、keywords）
```

### 4.7.3 用 /review 命令审查改动

Claude Code 内置了审查命令：

```
> /review
```

它会列出本次所有修改，确认没有引入问题。

---

## 4.8 提交代码到 Git

### 4.8.1 让 Claude Code 帮你提交

在 Claude Code 里可以直接说：

```
> 帮我把所有改动提交到 Git，提交说明写"完成个人主页基础版本"
```

Claude Code 会自动执行：

```powershell
git add .
git commit -m "完成个人主页基础版本"
```

### 4.8.2 手动提交（推荐养成习惯）

也可以自己操作，保持对 Git 的掌控感：

```powershell
git status                          # 查看改动
git add .                           # 暂存所有文件
git commit -m "完成个人主页基础版本"  # 提交
```

---

## 4.9 发布到 GitHub Pages

### 4.9.1 在 GitHub 创建仓库

1. 登录 GitHub，点击右上角 `+` → New repository
2. 仓库名填写：`my-website`（或你喜欢的名字）
3. 选择 **Public**（公开，GitHub Pages 免费版需要公开仓库）
4. **不要**勾选初始化 README（本地已有）
5. 点击 Create repository

### 4.9.2 推送代码到 GitHub

```powershell
# 关联远程仓库（把下面的地址换成你的）
git remote add origin git@github.com:你的用户名/my-website.git

# 推送
git branch -M main
git push -u origin main
```

或者让 Claude Code 帮你：

```
> 帮我把代码推送到 GitHub，仓库地址是 git@github.com:你的用户名/my-website.git
```

### 4.9.3 开启 GitHub Pages

1. 进入 GitHub 仓库页面
2. 点击 **Settings**（设置）
3. 左侧菜单找到 **Pages**
4. Source 选择 **Deploy from a branch**
5. Branch 选择 `main`，文件夹选 `/ (root)`
6. 点击 **Save**

等待约 1~2 分钟，页面顶部会出现你的网站地址：

```
https://你的用户名.github.io/my-website
```

### 4.9.4 让 Claude Code 更新网站

以后每次修改完，让 Claude Code 提交并推送：

```
> 帮我提交并推送最新改动，说明是"更新项目展示页面"
```

GitHub Pages 会在几分钟内自动更新。

---

## 4.10 进阶：让 Claude Code 添加更多功能

### 4.10.1 添加暗黑/明亮模式切换

```
> 在导航栏右侧添加一个明暗模式切换按钮，点击后切换整个网站的配色，并把用户的选择保存到 localStorage
```

### 4.10.2 添加联系表单

```
> 在 index.html 底部添加一个联系表单，包含姓名、邮箱、留言三个字段，提交时用 JavaScript 做表单验证
```

### 4.10.3 添加平滑滚动和返回顶部

```
> 给所有页面内链接添加平滑滚动效果，并在右下角添加一个"返回顶部"按钮，滚动超过 300px 后才显示
```

### 4.10.4 添加加载动画

```
> 给网站添加一个页面加载完成前的 loading 动画，加载完成后淡出消失
```

---

## 4.11 与 Claude Code 高效协作的技巧

### 4.11.1 描述要具体

**模糊的要求（效果差）：**
```
> 让网站好看一些
```

**具体的要求（效果好）：**
```
> 把所有按钮的圆角改为 8px，背景色改为 #3b82f6，悬停时加深 10%，添加 0.2s 的过渡动画
```

### 4.11.2 分步骤迭代

不要一次提太多要求，一步一步来：

```
第一步：先把首页布局搭好
第二步：（看效果后）调整颜色和字体
第三步：（满意后）再做响应式适配
```

### 4.11.3 让 Claude Code 解释它做了什么

```
> 你刚才修改了哪些文件？每个改动的原因是什么？
```

这样可以学习 Claude Code 的实现思路，不只是得到结果。

### 4.11.4 遇到问题时的处理方式

如果网站出现样式错乱或 JS 报错：

```
> 浏览器控制台报错：Uncaught TypeError: Cannot read property 'style' of null
> 帮我找出原因并修复
```

```
> 在手机上导航栏重叠了，截图是这样的：[描述现象]
> 帮我排查 CSS 问题
```

---

## 4.12 常用命令速查

### Claude Code 内常用指令

| 指令 | 说明 |
|------|------|
| `/help` | 查看所有可用命令 |
| `/clear` | 清空对话上下文，重新开始 |
| `/review` | 审查当前所有改动 |
| `/init` | 为项目生成 CLAUDE.md 说明文件 |
| `/exit` | 退出 Claude Code |

### 网站开发常用 Git 命令

```powershell
git status                  # 查看哪些文件有改动
git diff                    # 查看具体改动内容
git add .                   # 暂存所有改动
git commit -m "说明"         # 提交
git push                    # 推送到 GitHub（自动更新 Pages）
git log --oneline           # 查看提交历史
```

---

## 4.13 本章小结

| 要点 | 内容 |
|------|------|
| 项目初始化 | 新建文件夹 → `git init` → 启动 `claude` |
| 开发方式 | 用自然语言描述需求，Claude Code 直接修改文件 |
| 预览方式 | 浏览器直接打开 / `python -m http.server 8080` |
| 代码审查 | 用 `/review` 命令，或直接问 Claude Code |
| 发布方式 | 推送到 GitHub → 开启 GitHub Pages |
| 高效技巧 | 具体描述 + 分步迭代 + 让 AI 解释改动 |
| 核心理念 | Claude Code 负责写代码，你负责提需求和把关质量 |
