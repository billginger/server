# Git 常用命令

## 查看 Git 版本

```
git --version
```

## 克隆远程仓库

```
git clone git@bitbucket.org:tctt/wmp.git wmp
```

## 从远程仓库拉取

```
git pull
```

## 将所有修改过的工作文件提交暂存区

```
git add .
```

## 提交已经被 add 进来的改动

```
git commit -m "the commit message"
```

## push 所有分支

```
git push
```

## 用代码库中的文件完全覆盖本地工作版本

```
git reset --hard
git pull
```

## 合并某分支到当前分支

```
git merge <name>
```

## 检出指定分支，并与本地当前分支合并

```
git pull origin wmp-dev
```

## 检出指定分支，并切换到检出的分支

```
git fetch origin wmp-dev
git checkout wmp-dev
```

## 查看代码更新记录

```
git log
```

## 代码回滚（切到之前的某个版本）

```
git checkout 6f7aa97
```
