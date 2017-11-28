# 使用 NPM

## 初始化项目

```
npm init
```

## 权限问题

Warning "root" does not have permission to access the dev dir...

先删除 node_modules 目录，再执行：

```
npm install --unsafe-perm
```
