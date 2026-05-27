# Git & GitHub 基础

学习日期：2026-05-27

---

## 一、Git 是什么

Git 是一个版本控制工具，用来记录文件的修改历史，方便多人协作和代码管理。  
GitHub 是一个托管 Git 仓库的网站，可以把本地代码上传到云端保存和分享。

---

## 二、安装与配置

### 安装 Git
```powershell
winget install --id Git.Git -e --source winget
```

### 配置用户信息（只需配置一次）
```powershell
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的邮箱"
```

### 生成 SSH 密钥（绑定 GitHub 账号）
```powershell
# 生成密钥
ssh-keygen -t ed25519 -C "你的邮箱"

# 查看公钥（复制后添加到 GitHub Settings -> SSH keys）
cat ~/.ssh/id_ed25519.pub

# 测试连接是否成功
ssh -T git@github.com
```

---

## 三、创建本地仓库并推送到 GitHub

```powershell
git init                                        # 初始化本地仓库
git add .                                       # 添加所有文件到暂存区
git commit -m "提交说明"                         # 提交到本地仓库
git branch -M main                              # 将分支重命名为 main
git remote add origin git@github.com/仓库地址   # 关联远程仓库
git push -u origin main                         # 第一次推送
```

---

## 四、日常使用命令

### 查看状态
```powershell
git status          # 查看当前文件状态
git log             # 查看提交历史
git log --oneline   # 简洁查看提交历史
```

### 提交更新
```powershell
git add .                   # 添加所有修改的文件
git add 文件名               # 只添加某个文件
git commit -m "说明内容"     # 提交
git push                    # 推送到远程仓库
```

### 从远程仓库获取
```powershell
git pull                    # 拉取远程最新内容并合并
git clone 仓库地址           # 克隆远程仓库到本地
```

### 分支操作
```powershell
git branch                  # 查看所有分支
git branch 分支名            # 创建新分支
git checkout 分支名          # 切换分支
git merge 分支名             # 合并分支到当前分支
```

---

## 五、常见问题

### 提示 "dubious ownership"
```powershell
git config --global --add safe.directory 你的目录路径
```

### 撤销未提交的修改
```powershell
git checkout -- 文件名      # 撤销某个文件的修改
git reset HEAD 文件名       # 从暂存区移除某个文件
```

---

## 六、工作流程总结

```
修改文件 → git add . → git commit -m "说明" → git push
```
