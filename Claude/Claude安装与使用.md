# Claude 学习记录：安装与使用（2026-05-27）

## 目标

- 在 Windows 上安装 Claude 桌面应用（PWA）
- 安装 Claude Code CLI（命令行版）
- 了解两者的基本使用方式

---

## 一、Claude 是什么

Claude 是 Anthropic 开发的 AI 助手。主要有两种使用方式：

| 方式 | 适合场景 |
|------|----------|
| Claude 网页/桌面应用 | 日常对话、写作、问答 |
| Claude Code CLI | 编程辅助、在终端里直接对话代码 |

---

## 二、安装 Claude 桌面应用（PWA 方式）

### 什么是 PWA

PWA（Progressive Web App）是把网页"安装"成桌面应用，打开后像普通软件一样有独立窗口，不显示浏览器地址栏。

### 安装步骤

1. 用 Chrome 浏览器打开 [https://claude.ai](https://claude.ai)
2. 登录账号（可用 Google 账号）
3. 点击 Chrome 地址栏右侧的 **安装图标**（或菜单 → 更多工具 → 创建快捷方式 → 勾选"在窗口中打开"）
4. 点击"安装"，桌面出现 Claude 快捷方式

### 验证安装成功

- 桌面出现 Claude 图标
- 双击打开后是独立窗口（没有地址栏）

> 也可以直接下载官方安装包：访问 claude.ai 后页面会提示下载桌面版（`Claude Setup.exe`），运行后自动完成安装。

---

## 三、安装 Claude Code（命令行版）

Claude Code 是在终端里使用的 Claude，可以直接读取代码文件、帮你写代码。

### 前置条件

需要先安装 Node.js（Claude Code 依赖它运行）：

```powershell
winget install OpenJS.NodeJS
```

### 安装命令

```powershell
npm install -g @anthropic-ai/claude-code
```

### 验证安装

```powershell
claude --version
```

### 启动使用

```powershell
# 在任意项目文件夹下启动
cd E:\practice
claude
```

---

## 四、Claude Code 基本用法

| 操作 | 方式 |
|------|------|
| 直接提问 | 在提示符后输入问题 |
| 让它读文件 | 直接说"帮我看一下 xxx.md" |
| 让它写代码 | 描述需求，它会自动创建/修改文件 |
| 退出 | 输入 `/exit` 或按 `Ctrl+C` |
| 查看帮助 | 输入 `/help` |

---

## 五、今天已完成

- **Claude 桌面应用**：通过 `Claude Setup.exe` 安装完成，桌面有快捷方式。
- **Claude Code CLI**：已安装并可在终端正常使用。
- **仓库归档**：学习笔记已推送到 GitHub（GYJ-1 仓库）。
