# MongoDB 常用命令

## 查询

### 按日期查询

```
db.message.find({ createdAt: { $gte: new Date('2017-8-1 11:51:00') } })
```

> 备注：gt大于，lt小于，gte大于等于，lte小于等于

### 按条件统计数量

```
db.message.find({ CreateTime: { $lt: 1504680640, $gt: 1504679775 } }).count()
```

### 排序

```
db.message.find().sort({ _id: -1 })
```

### 指定最大记录数

```
db.getCollection('message').find({}).limit(161355)
```

## 导出数据库

### 本地，指定端口，打包成 gz 文件

```
mongodump --gzip --db wpm --archive=/root/bill/site/wpm/db/wpm.gz --port=27082
```

### 阿里云，打包成 gz 文件

```
mongodump -h id.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase admin -u root -p password -d wmp --gzip --archive=/data/backup/wmp.gz
```

### 阿里云，按集合打包成 gz 文件，导出到指定目录

```
mongodump -h id.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase admin -u root -p password -d wpm -o /data/backup --gzip
```

## 导入数据库

### 本地，指定端口

```
mongorestore --gzip --archive=/home/bill/site/wpm/db/wpm.gz --port=27082
```

### 阿里云，导入时指定库名

```
mongorestore -h id.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase admin -u root -p password -d wmp2 --gzip --archive=/data/backup/wmp.gz
```

### 阿里云，导入指定目录的 gz 文件

```
mongorestore -h id.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase admin -u root -p password -d wpm2 /data/backup/wpm --gzip
```

### 3.4 版本以后，需使用 --nsFrom 和 --nsTo 在导入时重命名库名

```
mongorestore --gzip --archive=/Users/bill/node/backup/wmp.gz --nsFrom 'wmp.*' --nsTo 'wmp2.*'
```

## 跨库移动集合

```
use admin
db.runCommand({ renameCollection: "[oldDbName].[collectionName]", to: "[newDbName].[collectionName]" })
```
