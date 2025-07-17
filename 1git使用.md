# git使用

## 一、Git 基础配置（首次使用）

```
bash复制编辑git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

查看配置：

```
bash
复制编辑
git config --list
设置公钥和私钥
ssh-keygen -t rsa -b 4096 -C "994277989xin@gmail.com"
```

------

将公钥添加到 GitHub

1. 登录 GitHub，进入：
    `Settings` → `SSH and GPG keys` → `New SSH key`
    👉 链接：https://github.com/settings/keys
2. 填写标题（如“我的电脑SSH密钥”）
3. 粘贴刚刚复制的公钥内容
4. 点击保存





## 🏗️ 二、常用 Git 操作流程

### 1. 创建/初始化本地仓库

```
bash复制编辑mkdir my_project       # 创建目录
cd my_project          # 进入目录
git init               # 初始化为 Git 仓库
```

### 2. 添加文件并提交

```
bash复制编辑touch README.md        # 创建一个文件
git add README.md      # 添加到暂存区
git commit -m "第一次提交"  # 提交到本地仓库
```

> 🔹`git add` 是“准备提交”，`git commit` 是“正式提交”。

### 3. 查看仓库状态

```
bash


复制编辑
git status
```

### 4. 查看提交记录

```
bash


复制编辑
git log
```

------

## 🛰️ 三、连接远程仓库（如 GitHub）

### 1. 先去 GitHub 创建一个仓库（网址：https://github.com）

### 2. 绑定远程仓库地址

```
bash


复制编辑
git remote add origin https://github.com/用户名/仓库名.git
```

### 3. 推送到远程仓库

```
bash


复制编辑
git push -u origin main
```

> ⚠️ 默认分支可能是 `master` 或 `main`，用 `git branch` 查看。

------

## 🔁 四、日常开发常用命令

| 操作                                     | 命令                              |
| ---------------------------------------- | --------------------------------- |
| 添加修改                                 | `git add 文件名`                  |
| 提交                                     | `git commit -m "说明"`            |
| 查看状态                                 | `git status`                      |
| 查看历史                                 | `git log`                         |
| 查看分支                                 | `git branch`                      |
| 新建分支                                 | `git branch 分支名`               |
| 切换分支                                 | `git checkout 分支名`             |
| 合并分支                                 | `git merge 分支名`                |
| 拉取远程代码                             | `git pull`                        |
| 推送代码                                 | `git push`                        |
| 查看工作区和暂存区之间的差异（未 `add`） | `git diff`                        |
| 拉取远程仓库                             | 'git fetch'或者'git fetch 分支名' |
| 合并到当前分支                           | git merge                         |



------

## 🧹 五、恢复与撤销

| 场景           | 命令                     |
| -------------- | ------------------------ |
| 撤销 add       | `git reset 文件名`       |
| 撤销 commit    | `git reset --soft HEAD^` |
| 撤销工作区修改 | `git checkout -- 文件名` |
| 删除文件       | `git rm 文件名`          |

##       六、git打标签

| 操作     | 推荐方式                       |
| -------- | ------------------------------ |
| 提交顺序 | 先 `add` → `commit` → 再 `tag` |
| 标签类型 | 使用 `-a` 附注标签，便于描述   |
| 推送顺序 | `push` 代码 → 再 `push` 标签   |
| 避免问题 | 不要在未提交时打标签！         |

------

------

### 🧱 第一步：修改代码

修改你需要提交的代码文件。

------

### 🗃️ 第二步：暂存并提交

```
bash复制编辑git add .
git commit -m "feat: 增加 xxx 功能"
```

或者按文件选择提交：

```
bash复制编辑git add src/main.c
git commit -m "fix: 修复 xxx bug"
```

------

### 🔖 第三步：打标签

#### 💡 建议使用**附注标签（annotated tag）**

```
bash


复制编辑
git tag -a v1.0.0 -m "Release version 1.0.0"
```

这个标签就打在你刚刚提交的那个 commit 上。

## 🧪 七、简单实战流程举例

```
bash复制编辑# 创建一个项目目录并初始化 Git
mkdir demo
cd demo
git init

# 新建文件并提交
echo "Hello Git" > hello.txt
git add hello.txt 
git commit -m "添加 hello.txt"

# 创建 GitHub 仓库后添加远程地址
git remote add origin https://github.com/你的用户名/demo.git
git push -u origin main
```

git commit 提交本地仓库

git push 从本地到远程仓库

git pull 从远程仓库拉到本地来