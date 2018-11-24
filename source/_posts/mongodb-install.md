---
title: 在 Mac 上安装并配置 MongoDB
date: 2018-11-12 23:30:58
tags: 
 - mongodb
categories: MacOS
---

### 下载并安装 MongoDB
- 直接下载安装

MongoDB 提供了 OSX 平台上 64 位的安装包，你可以在官网下载安装包。

```
下载地址：https://www.mongodb.com/download-center#community
```
- 通过mac自带的curl安装

```shell
# 进入 /usr/local
cd /usr/local

# 下载
sudo curl -O https://fastdl.mongodb.org/osx/mongodb-osx-ssl-x86_64-4.0.3.tgz

# 解压
sudo tar -zxvf mongodb-osx-ssl-x86_64-4.0.3.tgz

# 重命名为 mongodb 目录

sudo mv mongodb-osx-ssl-x86_64-4.0.3 mongodb
```

- 通过 brew 安装

```shell
sudo brew install mongodb
```
安装中需要稍等一会儿，完成后输入下列命令

```shell
mongod --version
mongo --version
```

出现下列提示，则表示可以使用 mongod 和 mongo 命令

```shell
db version v4.0.3
git version: 7ea530946fa7880364d88c8d8b6026bbc9ffa48c
allocator: system
modules: none
build environment:
    distarch: x86_64
    target_arch: x86_64
```
```shell
MongoDB bush version v4.0.3
git version: 7ea530946fa7880364d88c8d8b6026bbc9ffa48c
allocator: system
modules: none
build environment:
    distarch: x86_64
    target_arch: x86_64
```
否则，要配置环境变量

```shell
cd ~
vim .bash_profile
```

将下列代码复制粘贴进去，保存后即可。

```bash
export MONGO_PATH=/usr/local/Cellar/mongodb
export PATH=$PATH:$MONGO_PATH/bin
```

### 配置 MongoDB

新建数据库存放路径、配置文件和日志文件

```shell
#进入 mac 根目录
cd /

#新建文件夹 mongoData
mkdir mongoData

#新建三个文件夹分别是 db(存放数据库数据)，etc(mongodb配置文件)，logs(日志文件)
mkdir db etc logs

在etc和log下分别创建配置文件和日志文件
cd etc
touch mongo.conf
cd logs 
touch mongo.log

```

接下来修改 mongodb 的配置文件

```shell
#vim编辑配置文件
vim mongo.conf
```

mongdb的配置，参考链接 [Run-time Database Configuration](https://docs.mongodb.com/manual/administration/configuration/)

```bash
  #日志输出文件路径
logpath=/mongoData/logs/mongo.log

#错误日志采用追加模式，配置这个选项后mongodb的日志会追加到现有的日志文件，而不是从新创建一个新文件
logappend=true

#启用日志文件，默认启用
journal=true

#这个选项可以过滤掉一些无用的日志信息，若需要调试使用请设置为false
quiet=false

#是否后台启动，有这个参数，就可以实现后台运行
fork=true

#端口号 默认为27017
port=27017

#指定存储引擎（默认不需要指定）
#storageEngine=mmapv1

#开启认证
auth = true
```

将上面的配置字段复制进去并且保存

### 启动mongodb

```shell
#通过配置文件的方式启动mongdb
mongod -f /mongoData/etc/mongo.conf
```

如果出现 successfully, 则表示成功

```shell
2018-11-24T17:17:03.968+0800 I CONTROL  [main] Automatically disabling TLS 1.0, to force-enable TLS 1.0 specify --sslDisabledProtocols 'none'
about to fork child process, waiting until server is ready for connections.
forked process: 2299
child process started successfully, parent exiting
```

### 配置超级用户和用户

```shell
#进入mongodb
mongo

#使用admin数据库
use admin

#查看有所有数据库
show dbs
```

不出意外的话会提示没有权限，因为我们是以配置文件启动的mongodb，并且配置文件中我们开启了认证将auth字段设置成了true

这个时候我们就应该开始配置用户

- 创建超级管理员用户

```shell
use admin
db.createUser({user:"admin",pwd:"password",roles:["root"]}) //admin这个数据库是系统自带的数据库，他的用户可以访问任何其他数据库的数据，也叫做超级管理员

db.auth("admin","password") // => 1 表示验证通过 0表示验证失败

show dbs //=>admin   0.000GB blog    0.000GB config  0.000GB 
```

这样就展示出所有的数据库了

- 创建普通用户（某个数据库的用户）

```shell
use admin //=>进入admin数据库

db.auth("admin","password") //=> 通过超级管理员验证

use blog

db.createUser({user: "blog", pwd: "password", roles: [{ role: "dbOwner", db: "blog" }]})

show dbs => admin   0.000GB    blog    0.000GB    config  0.000GB    local   0.000GB
```

这样就创建了单独关于blog这个数据库的账户了，账号是blog，密码是password
这里我们要注意一点，给创建普通数据库用户的时候要是在超级管理员验证完之后创建

原文链接: https://segmentfault.com/a/1190000014740252