# Git 命令速查

## 每天都会用的

| 命令 | 作用 |
|---|---|
| `git status` | 看当前状态（最该多按的一条） |
| `git add -A` | 把所有改动放进暂存区 |
| `git add <文件>` | 只暂存某个文件 |
| `git commit -m "说明"` | 提交暂存区的内容 |
| `git push` | 推到远端 |
| `git pull` | 拉远端最新（先 pull 再 push 是好习惯） |
| `git log --oneline --graph` | 看提交历史图 |

## 看历史

```bash
git log --oneline -10            # 最近 10 条，一行一条
git log --oneline --graph --all  # 带分支图
git show <提交号>                # 看某次提交改了什么
git diff                         # 工作区还没暂存的改动
git diff --staged                # 已暂存待提交的改动
```

## 撤销与后悔

| 场景 | 命令 |
|---|---|
| 改坏了某个文件，想还原成上次提交的样子 | `git restore <文件>` |
| 已经 `git add` 了，想撤出暂存区 | `git restore --staged <文件>` |
| 刚提交完，发现信息写错了（还没推送） | `git commit --amend -m "新说明"` |
| 刚提交完，想撤销这次提交但保留改动 | `git reset --soft HEAD~1` |
| 想彻底丢掉上次提交和改动（危险） | `git reset --hard HEAD~1` |

## 分支

```bash
git branch                       # 列出本地分支
git switch -c 新分支名            # 新建并切换
git switch main                  # 切回 main
git merge 分支名                  # 把某分支合并进当前分支
git branch -d 分支名              # 删除已合并的分支
```

## 远端

```bash
git remote -v                    # 看远端地址
git remote set-url origin 新地址  # 换远端地址
git fetch --prune                # 拉取远端信息并清理已删分支
git push -u origin main          # 第一次推送并绑定上游
```

## 冲突怎么解

`git pull` 或 `git merge` 后出现冲突时，文件里会长出这样的标记：

```
<<<<<<< HEAD
本地这一版
=======
远端那一版
>>>>>>> origin/main
```

处理步骤：

1. 打开冲突文件，把 `<<<<<<<`、`=======`、`>>>>>>>` 三行删掉
2. 留下你想要的内容（可以两版都留、都改、或重写）
3. `git add <冲突文件>`
4. `git commit`（Git 会给你一条预填好的合并说明，直接保存即可）
5. `git push`

想中途放弃这次合并：`git merge --abort`

## 有用的设置

```bash
git config --global --list                  # 看全部全局配置
git config --global core.quotepath false    # 中文文件名不转义（本机已设）
git config --global init.defaultBranch main # 新仓库默认 main（本机已设）
git config --global core.editor notepad     # 默认编辑器（本机已设）
```

## 本机特有提醒

- 远端地址必须用 `git@github.com:288288/xxx.git` 这种 SSH 形式，**不要用 https://**：这台机器到 github.com 的 443 端口是超时的
- 如果推送报 `Permission denied (publickey)`，说明密钥没被 GitHub 认，先跑 `ssh -T git@github.com` 自检
