# 使用 PM2

## 全局安装

```
npm install pm2 -g
```

## 进程文件

```json
{
	"apps" : [{
		"name": "http",
		"script": "./http/index.js",
		"watch": true,
		"log_date_format": "YYYY-MM-DD HH:mm:ss",
		"error_file": "./pm2logs/http_err.log",
		"out_file": "./pm2logs/http_out.log"
	}, {
		"name": "sale",
		"script": "./sale/index.js",
		"cwd": "./sale/",
		"watch": true,
		"log_date_format": "YYYY-MM-DD HH:mm:ss",
		"error_file": "./pm2logs/sale_err.log",
		"out_file": "./pm2logs/sale_out.log"
	}]
}
```

## 常用命令

* pm2 start apps.json
* pm2 list
* pm2 monit
* pm2 logs
* pm2 kill

## 传参

```
pm2 start npm -- start -- --host 0.0.0.0 --disable-host-check --compress --no-inline
```
