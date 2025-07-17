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
| 查看远程和本地仓库                        | `git remote -v`                        |
| 推送所有标签                              | `git push origin --tags`               |
| 推送单个标签                              | `git push origin v1.0.0`               |

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

### 八、git忽略提交

#### **1. 从 Git 中移除文件（保留本地文件）**

bash

复制

```bash
git rm --cached <文件名或路径>
```

- 

  作用

  ：

  - 从 Git 版本控制中移除该文件
  - 本地文件会保留在磁盘中（不会被删除）
  - 文件会变为 **未跟踪（Untracked）** 状态

#### **2. 提交变更**

bash

复制

```bash
git commit -m "chore: 从 Git 中移除 <文件名>（保留本地文件）"
```

- 这一步会正式从 Git 历史中删除该文件的跟踪记录。

#### **3. 重新添加文件（可选）**

如果后续想重新让 Git 跟踪该文件（比如修改了 `.gitignore` 后）：

bash

复制

```bash
git add <文件名或路径>
git commit -m "chore: 重新跟踪 <文件名>"
```

------

### **常见使用场景**

1. **误提交了敏感文件（如 `.env`、`node_modules`）**

   - 用 `git rm --cached` 移除，并添加到 `.gitignore` 避免再次误提交。

2. **停止跟踪某个大文件/中间文件**

   - 保留本地文件，但不再纳入版本控制。

3. **清理 Git 历史中的垃圾文件**

   - 彻底从 Git 历史中删除文件（需配合 `git filter-branch` 或 `BFG`）。

     git

     ## **.gitignore 基本用法**

     ### **1. 创建 `.gitignore` 文件**

     在项目根目录下创建 `.gitignore` 文件：

     bash

     复制

     ```bash
     touch .gitignore
     ```

     或者直接编辑：

     bash

     复制

     ```bash
     vim .gitignore
     ```

     ------

     ### **2. 语法规则**

     |    语法    |       示例       |              说明               |
     | :--------: | :--------------: | :-----------------------------: |
     |  `文件名`  |    `temp.txt`    |    忽略所有 `temp.txt` 文件     |
     | `目录名/`  |     `build/`     |      忽略整个 `build` 目录      |
     | `*.扩展名` |     `*.log`      |      忽略所有 `.log` 文件       |
     |  `!例外`   | `!important.log` |     不忽略 `important.log`      |
     |  `# 注释`  |   `# 这是注释`   |       注释行，Git 会忽略        |
     |   `**/`    |    `**/tmp/`     | 递归匹配所有子目录的 `tmp` 目录 |

     ------

     ### **3. 常用示例**

     #### **忽略特定文件**

     复制

     ```markdown
     # 忽略本地配置文件
     .env
     config.ini
     ```

     #### **忽略特定目录**

     复制

     ```markdown
     # 忽略编译输出目录
     bin/
     build/
     dist/
     ```

     #### **忽略特定扩展名**

     复制

     ```markdown
     # 忽略日志文件
     *.log
     *.tmp
     ```

     #### **忽略所有子目录下的某个目录**

     复制

     ```markdown
     # 忽略所有 node_modules 目录
     **/node_modules/
     ```

     #### **例外规则（不忽略某些文件）**

     复制

     ```markdown
     # 忽略所有 .txt 文件，但不包括 important.txt
     *.txt
     !important.txt
     ```

     ------

     ### **4. 生效方式**

     - **新文件**：`.gitignore` 对新创建的文件立即生效。

     - 

       已跟踪的文件

       ：如果文件已经被 Git 跟踪（

       ```
       git add
       ```

        

       过），需要先移除：

       bash

       复制

       ```bash
       git rm --cached <文件名>  # 从 Git 移除，但保留本地文件
       git commit -m "停止跟踪 <文件名>"
       ```

     ------

     ### **5. 全局 `.gitignore`（适用于所有项目）**

     如果你想 **全局忽略某些文件**（如 IDE 配置文件），可以配置全局 `.gitignore`：

     bash

     复制

     ```bash
     git config --global core.excludesfile ~/.gitignore_global
     ```

     然后在 `~/.gitignore_global` 里添加规则（如 `.DS_Store`、`.vscode/`）。

     ------

     ### **6. 检查哪些文件被忽略**

     bash

     复制

     ```bash
     git status --ignored  # 查看被忽略的文件
     ```

     