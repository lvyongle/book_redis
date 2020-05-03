# 	redis安装单机板

单机版安装,使用[<<redis中文网>>](http://www.redis.cn/download.html)

### 安装

下载,解压,编译  `Redis`

```shell
$ wget http://download.redis.io/releases/redis-5.0.5.tar.gz
$ tar xzf redis-5.0.5.tar.gz
$ cd redis-5.0.5
$ make
```



进入到解压后的 `src` 目录，通过如下命令启动Redis:

```shell
$ src/redis-server [--port=6380]
```



使用内置客户端进行交互

```shell
$ src/redis-cli      [-p6380]
redis> set foo bar
OK
redis> get foo
"bar"
```



- 注意:centos7下出现编译redis6.0错误,注意升级 `gcc` 版本

  ```shell
  In file included from server.c:30:0:
  server.h:1022:5: error: expected specifier-qualifier-list before ‘_Atomic’
       _Atomic unsigned int lruclock; /* Clock for LRU eviction */
  ```

  ```shell
  sudo yum install centos-release-scl
  sudo yum install devtoolset-7-gcc*
  scl enable devtoolset-7 bash
  ```

- 报错: `/bin/sh: cc: 未找到命令`

  ```shell
  yum install gcc-c++ -y
  ```

- 报错 `zmalloc.h:50:31: 致命错误：jemalloc/jemalloc.h：没有那个文件或目录`

  ```shell
  make MALLOC=libc
  ```

- 外部连接需要修改保护模式,启动时还要指定配置参数或者配置文件

  ```shell
  #protected-mode yes
  protected-mode no
  
  # By default Redis does not run as a daemon. Use 'yes' if you need it.
  # Note that Redis will write a pid file in /var/run/redis.pid when daemonized.
  daemonize yes
  
  # requirepass foobared
  requirepass foot
  ```

  ```shell
  $ redis-server /usr/local/redis/redis.conf
  ```

  

### 指定端口启动服务

```shell
daemonize yes
logfile '6479.log'
dir /redis/data1
port 6380
```



