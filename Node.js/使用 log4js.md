# 使用 log4js

## 安装

```
npm i log4js --save
```

## 使用

```
var log4js = require('log4js');
var logger = log4js.getLogger();
logger.level = 'debug';
logger.debug("Some debug messages");
```

## 配置

```
const log4js = require('log4js');
log4js.configure({
  appenders: { cheese: { type: 'file', filename: 'cheese.log' } },
  categories: { default: { appenders: ['cheese'], level: 'error' } }
});
 
const logger = log4js.getLogger('cheese');
logger.trace('Entering cheese testing');
logger.debug('Got cheese.');
logger.info('Cheese is Gouda.');
logger.warn('Cheese is quite smelly.');
logger.error('Cheese is too ripe!');
logger.fatal('Cheese was breeding ground for listeria.');
```

## 更多信息

* https://github.com/log4js-node/log4js-node
* https://blog.csdn.net/u012712261/article/details/52095712
* https://www.jb51.net/article/91414.htm
