# Fork 维护工作流

本文档记录个人版本与原作者仓库之间的同步方式。

## 当前配置

| 名称 | 地址 | 用途 |
| --- | --- | --- |
| `origin` | `https://github.com/somindev/lj-skills.git` | 个人 fork |
| `upstream` | `git@github.com:lijigang/ljg-skills.git` | 原作者仓库 |

分支职责：

- `master`：始终跟随 `upstream/master`，不放个人修改。
- `my-version`：保存个人修改，日常开发在此分支进行。

## 首次推送个人分支

```bash
git switch my-version
git push -u origin my-version
```

设置跟踪关系后，日常提交可以直接推送：

```bash
git push
```

## 同步原作者更新

先更新本地 `master`：

```bash
git fetch upstream
git switch master
git merge --ff-only upstream/master
git push origin master
```

再把个人修改应用到最新 `master`：

```bash
git switch my-version
git rebase master
git push --force-with-lease
```

`--force-with-lease` 会在远端分支出现未知更新时拒绝覆盖，比 `--force` 更安全。

## 处理 Rebase 冲突

查看冲突文件：

```bash
git status
```

修改冲突文件后继续：

```bash
git add <文件>
git rebase --continue
```

放弃本次 rebase，恢复到开始前：

```bash
git rebase --abort
```

## 多人协作时

如果其他人也在使用 `my-version`，不要 rebase 已共享的提交。改用 merge：

```bash
git switch my-version
git merge master
git push
```

## 检查仓库状态

```bash
git remote -v
git status --short --branch
git branch -vv
git log --oneline --graph --decorate --all -20
```
