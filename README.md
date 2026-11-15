# hello-git-test

第一个 Git 练习仓库，用来验证「本地 → GitHub」的完整链路。

## 目录结构

```
hello-git-test/
├── README.md              本文件
├── .gitignore             忽略规则（Windows / 编辑器 / Python / Node）
├── docs/
│   └── git-cheatsheet.md  常用命令速查
└── templates/
    └── README.template.md 新项目 README 骨架
```

## 我用过的命令

```bash
git init                       # 初始化仓库（默认分支 main）
git status                     # 看当前状态
git add .                      # 把改动放进暂存区
git commit -m "说明"           # 提交
git remote add origin git@github.com:288288/hello-git-test.git
git push -u origin main        # 第一次推送，并绑定上游
```

## 日常三件套

```bash
git add -A && git commit -m "改了什么"
git push
git pull
```

## 版本

v0.1 初始版本

## 备注

- 认证走 SSH，不走 HTTPS（本机到 github.com 的 443 是超时的）
- 中文文件名能正常显示，因为设了 `core.quotepath=false`
- 新项目从这里复制：`templates/README.template.md` + 本仓库的 `.gitignore`
