# Git 常用命令

## 查看 Git 版本

```bash
git --version
```

## 克隆远程仓库

```bash
git clone git@bitbucket.org:tctt/wmp.git wmp
```

## 从远程仓库拉取

```bash
git pull
```

## 将所有修改过的工作文件提交暂存区

```bash
git add .
```

## 提交已经被 add 进来的改动

```bash
git commit -m "the commit message"
```

## push 所有分支

```bash
git push
```

## 用代码库中的文件完全覆盖本地工作版本

```bash
git reset --hard
git pull
```

## 检出指定分支，并与本地当前分支合并

```bash
git pull origin wmp-dev
```

## 检出指定分支，并切换到检出的分支

```bash
git fetch origin wmp-dev
git checkout wmp-dev
```
