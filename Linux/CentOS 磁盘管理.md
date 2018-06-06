# CentOS 磁盘管理

## 查看各分区使用情况

```
df -h
```

## 查看磁盘

```
fdisk -l
```

## 格式化磁盘

```
mkfs.ext4 /dev/vdb
```

## 挂载磁盘

```
mkdir /data
mount /dev/vdb /data
```

## 启动时自动挂载磁盘

```
echo '/dev/vdb /data ext4 defaults 0 0' >> /etc/fstab
cat /etc/fstab
```
