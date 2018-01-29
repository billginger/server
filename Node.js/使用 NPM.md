# 使用 NPM

## 初始化项目

```
npm init
```

## 查看全局安装过的包

```
npm list -g --depth 0
```

## 全局安装权限问题

```
sudo npm i -g express-generator
```

## 卸载

```
sudo npm un -g express-generator
```

## 目录权限问题

Warning "root" does not have permission to access the dev dir...

先删除 node_modules 目录，再执行：

```
npm install --unsafe-perm
```
