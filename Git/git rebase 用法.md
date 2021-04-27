# git rebase 用法

## 合并多次提交：

* 切换到开发分支
* `git rebase -i HEAD~2` 合并提交，2表示合并两个
* 按 i 键进行编辑
* 在想要保留的 commit 前面使用 pick 或 p
* 在想要合并的 commit 前面使用 fixup 或 f
* 按 Esc 键退出编辑
* 按 : 键，然后输入 wq 保存退出
* `git push --force`

## 更新开发分支代码：

建议在更新开发分支代码前先合并多次提交，以减少解决冲突的次数。

* 本地更新 master 分支
* 切换到开发分支
* `git rebase master`
* 如果有冲突 -> 解决冲突
* 暂存所有合并更改
* `git rebase --continue`
* `git push --force`
