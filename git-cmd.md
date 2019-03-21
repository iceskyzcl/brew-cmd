# Git cheat sheet

代码符号说明：
- [] - 可选参数
- <> - 必填参数


## 参考

[ProGit](https://git-scm.com/book/zh) - Git官网上的电子书

[GitHub Help](https://help.github.com) - GitHub官网帮助页面


## 安装

参见 [ProGit](https://git-scm.com/book/zh) 1.5节-安装Git


## 配置

**Git 配置变量存储在三个不同的位置：**

1. `/etc/gitconfig` 文件: 包含系统上每一个用户及他们仓库的通用配置。 `git config` 使用 `--system` 选项会从此文件读写配置变量。

2. `~/.gitconfig` 或 `~/.config/git/config` 文件：只针对当前用户。 `git config` 使用 `--global` 选项会从此文件读写配置变量。

3. 当前使用仓库的 Git 目录中的 config 文件（即 `.git/config`）：针对该仓库。

每一个级别覆盖上一级别的配置。

**使用 Git 前需先配置用户信息：**

```
git config --global user.name "John Doe"
git config --global user.email "johndoe@example.com"
```

> Git 通过 `user.name` 来关联提交 commit 的身份。修改 `user.name` 只对今后提交 commit 产生影响。

> GitHub 通过 `user.email` 来关联提交 push 的用户账号。修改 `user.email` 只对今后提交 push 产生影响。

**查看配置信息：**

`git config --list`

**Git 帮助命令：**

`git help [cmd]`


## 创建仓库

有两种取得 Git 项目仓库的方法：

**1. 在当前目录创建仓库：**

`git init`

> 该命令将创建一个名为 `.git` 的子目录，包含初始化的 Git 仓库中所有的必须文件。

**2. 下载一个项目以及它所有的版本历史：**

`git clone <url>`

> 该命令会创建一个以 `项目名` 为名称的目录，并在这个目录下初始化一个 `.git` 子目录。

> 推荐使用 `https://` 协议。


## 修改文件

> 文件的3个区域：工作区，暂存区，仓库。

> 文件的4种状态：未跟踪， 已修改， 已暂存，已提交。

**列出所有未提交的文件：**

`git status [-s]`

> 选项 `-s` 简短显示：
> - `??` 未跟踪
> - `A` 新添加到暂存区
> - `M`左 修改并暂存
> - 右`M` 修改但未暂存

**查看修改内容：**

`git diff`

> 此命令比较 工作区 和 暂存区 之间的差异。

`git diff --staged`

> 此命令比较 暂存区 和 最新版本 之间到差异。

**将文件添加到暂存区：**

`git add <file>`

**提交commit：**

`git commit [-m "message"]`

> 此命令把 暂存区 作为新版本提交。

`git commit -am "message"`

> 选项 `-a` 把所有已跟踪的文件暂存起来一并提交，从而跳过 `git add` 步骤。

**修改本地最近一次提交的注释：**

`git commit --amend`

**忽略跟踪：**

常用 `.gitignore` 文件列表参见 GitHub 的 [gitignore](https://github.com/github/gitignore) 项目。

## 删除和移动文件

**从暂存区移除并删除工作区中的文件：**

`git rm <file>`

**从暂存区移除但保留工作区中的文件：**

`git rm --cached <file>`

**重命名并准备commit：**

`git mv <file-original> <file-renamed>`


## 查看提交历史

**列出当前分支的版本历史：**

`git log [-p] [--oneline] [--graph]`

> 选项 `-p` 显示每次提交的差异。

**列出指定文件的版本历史：**

`git log --follow <file>`

> 包括文件重命名和移动。

**列出本地仓库的HEAD引用历史：**

`git reflog`

> 等效于 `git log -g --oneline`。

**查看提交简报:**

`git shortlog`

> 类似changelog文档。


## 恢复与重置

**从 指定版本 恢复到 暂存区：**

`git reset [commit-id] <file>`

> [commit-id] 默认为 HEAD。

**从 暂存区 恢复到 工作区：**

`git checkout -- <file>`

**变基当前分支引用指向 指定版本，并重置暂存区：**

`git reset [--hard] <commit-id>`

> 选项 `--hard` 同时重置工作区。

**切换到指定版本：**

`git checkout <commit-id>`

> `checkout` 命令会重置 暂存区 并改变 工作区 文件。

**批量修改历史提交：**

`git filter-branch --index-filter 'git rm --cached --ignore-unmatch <file>' -- --all`

> `filter-branch` 命令会改变hash值。
> 参见 [ProGit](https://git-scm.com/book/zh) 10.7节-维护与数据恢复。


## 分支

> 分支本质上仅仅是指向 commit 对象的可变指针。

**创建分支：**

`git branch <branch-name>`

> 仅创建分支，不自动切换。

**切换到指定分支：**

`git checkout <brench-name>`

> `checkout` 命令会重置 暂存区 并改变 工作区 文件。

**创建并切换分支：**

`git checkout -b <brench-name> [remote-name/branch-name]`

> 选项 `[remote-name/branch-name]` 以远程分支为上游创建本地分支。

**列出所有分支：**

`git branch [-vv] [--merged|--no-merged]`

> 选项 `-vv` 显示分支跟踪信息（基于已下载的数据）。

> 选项 `--merged` 或 `--no-merged` 显示已合并或未合并到当前分支的分支。

**合并指定分支到当前分支：**

`git merge [remote-name/]<branch-name>`

> 当 `git merge` 遇到冲突时，Git 做了合并，但没有自动创建一个新的合并提交。此时输入 `git status` 查看未合并的文件，修改文件后手动提交。

**合并遇到冲突时终止合并：**

`git merge --abort`

**删除指定分支：**

`git branch -d <branch-name>`


## 远程仓库

> GitHub远程仓库推送前先设置 [GitHub personal access token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line) 以获得权限。

**列出所有远程仓库地址：**

`git remote [-v]`

**添加远程仓库：**

`git remote add <remote-name> <url>`

**下载远程仓库的历史数据：**

`git fetch [remote-name|--all]`

**设置当前分支跟踪远程分支：**

`git branch -u <remote-name/branch-name>`

**下载当前分支所跟踪的远程分支，并自动合并到当前分支：**

`git pull`

> `clone` 和 `checkout` 命令会自动建立跟踪。

**将指定分支推送到远程分支：**

`git push [remote-name] [branch-name][:remote-branch-name]`

**查看远程仓库信息：**

`git remote show [remote-name]`

**移除远程仓库：**

`git remote rm [remote-name]`


## 标签

标签有两种类型：轻量标签（lightweight）与附注标签（annotated）。

**1. 添加轻量标签：**

`git tag <tagname> [commit-id]`

> 轻量标签是特定commit的引用。[commit-id] 默认为 HEAD。

**2. 添加附注标签：**

`git tag -a <tagname> -m <message> [commit-id]`

> 附注标签是一个包含个人信息的可校验对象。[commit-id] 默认为 HEAD。

**列出已有的标签：**

`git tag`

**显示指定标签：**

`git show <tagname>`

**删除标签：**

`git tag -d <tagname>`

**推送标签至远程仓库：**

`git push [remote-name] --tags`


## 临时存储

**临时存储所有修改的已跟踪文件：**

`git stash`

**取回并删除最新stash：**

`git stash pop`

**列出stash列表：**

`git stash list`

**应用指定stash：**

`git stash apply [stash@{n}]`

> 使用 `apply` 命令前应确认工作区状态干净，否则可能产生合并冲突。

> 默认为最新stash。

**删除指定stash：**

`git stash drop [stash@{n}]`

> 默认为最新stash。


## 选择提交区间

**沿当前分支回溯第n个提交：**

`git show HEAD~[n]`

> n=数字，默认=1。

**双点语法：**

`git log <commit-not>..<commit-in>`

查看在 commit-in分支 而不在 commit-not分支 的提交。

> 等价于 `git log ^<commit-not> <commit-in>`。

**三点语法：**

`git log [--left-right] <commitA>...<commitB>`

查看在 commitA分支 *异或* commitB分支 的提交。

> 选项 `--left-right` 标注提交位于哪一侧分支。


## 搜索

**在指定提交中搜索：**

`git grep [-n] <string> [commit-id]`

> 选项 `-n` 显示行号。默认搜索工作区。

**在提交历史中搜索：**

`git log -S<string>`

**查看每一行最后一次修改的提交信息：**

`git blame [-C] [-L [startline],[endline]] <file>`

> 选项 `-L` 限定起止行号。

> 选项 `-C` 检索每一行的原始文件出处（如复制/移动）。

**二分查找调试：**

```
git bisect start [new-commit] [old-commit]
git bisect run <test.sh>  #脚本运行old-commit返回0
git bisect reset [commit-id]
```

> 参见 [ProGit](https://git-scm.com/book/zh) 7.10节-使用 Git 调试。
