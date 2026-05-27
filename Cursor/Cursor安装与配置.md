# Cursor 学习记录：安装与中文设置（2026-05-28）

## 目标

- **界面中文（经典编辑器窗口）**：让顶部菜单显示为“文件/编辑/查看”。
- **AI 永远中文**：不管我用英文提问，AI 也用中文回答。
- **启动即经典模式**：双击桌面快捷方式只打开经典编辑器，不进入 Glass。

---

## 一、安装中文语言包（经典编辑器窗口用）

### 安装命令（在 Cursor 内置终端执行）

```powershell
cursor --install-extension MS-CEINTL.vscode-language-pack-zh-hans
```

### 如何确认安装成功

- 在用户扩展清单里能看到：`ms-ceintl.vscode-language-pack-zh-hans`
  - 例如：`C:\Users\Administrator\.cursor\extensions\extensions.json`
- 语言包索引里有 `zh-cn`：
  - 例如：`C:\Users\Administrator\AppData\Roaming\Cursor\languagepacks.json`

> 重要：语言包主要影响 **经典编辑器窗口**（VS Code workbench），不一定影响 Glass/Agent 界面。

---

## 二、为什么有时仍显示英文 “File”

### 结论

- **Glass / Agent 主界面**：菜单通常仍是英文（比如显示 `File`）。这是界面自身限制，**不是语言包失效**。
- **经典编辑器窗口**：会显示中文菜单（比如 `文件`），说明语言包正常。

### 快速自检

- 如果你能看到顶部菜单是 **“文件”**：说明中文语言包已经生效。
- 如果仍是 **“File”**：要么你在 Glass，要么经典窗口没有切换成功。

---

## 三、强制显示语言（可选）

如果需要强制指定中文，可以设置：

### 1) 用户语言文件

路径：

`C:\Users\Administrator\AppData\Roaming\Cursor\User\locale.json`

内容：

```json
{
  "locale": "zh-cn"
}
```

### 2) argv 参数（应用级）

路径：

`C:\Users\Administrator\.cursor\argv.json`

加入（或确认存在）：

```json
{
  "locale": "zh-cn"
}
```

> 注意：即使这些配置存在，Glass 界面仍可能显示英文菜单。

---

## 四、让 AI 永远用中文回答（全局生效）

### 验证方式（最快）

新开一个对话，发送：

`reply with one word`

如果 AI 回了中文（例如“好”），说明“永远中文”规则已生效。

### 推荐设置位置（UI）

在 Cursor 设置里添加 **User Rules**：

- Rules → User Rules
- 添加规则：

```text
Always respond in Simplified Chinese (简体中文).
```

---

## 五、启动即经典模式（桌面快捷方式）

### 已验证可用的参数组合

桌面快捷方式目标（Target）示例：

```text
E:\软件\cursor\Cursor.exe --classic --open-editor
```

说明：

- `--open-editor`：打开经典编辑器窗口
- `--classic`：只进入经典模式（不进 Glass）

### 排错要点

- 如果仍出现 Glass：先完全退出 Cursor（任务管理器结束所有 `Cursor.exe`），再用该快捷方式启动。

---

## 六、最终结果（今天已完成）

- **中文语言包已安装**：经典编辑器窗口菜单显示为“文件”。
- **AI 永远中文**：新对话英文测试触发中文回复，规则生效。
- **启动只进经典**：桌面快捷方式参数生效，Glass 不再自动打开。

