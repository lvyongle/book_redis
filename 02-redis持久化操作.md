# redis持久化操作

### 持久化操作简介

- 数据快照方式-RDB
- 过程日志方式-AOF



### RDB方式存储方式

- 指令方式
  - `save`  : 执行一次,保存一次
  - 查看文件位置  `CONFIG GET DIR`
- save指令相关配置
  - `dbfilename` 
    - 保存文件名
    - 默认 `dump.rdb`
    - 通常设置 `dump[-端口号].rdb`
  - `dir`
    - 存储 `.rdb` 文件的路径
    - 通常使用最大盘
  - `rdbcompression` 
    - 设置存储本地数据库时是否压缩数据,默认 `yes` ,采用 `LZF` 压缩
    - 通常默认开启,如果设置为 `no` ,可节省 ` cpu ` 性能,但会使文件变得巨大
  - `rdbchecksum`
    - 校验 ` RDB ` 文件
    - 每次变更操作都会降低性能,但是建议打开



