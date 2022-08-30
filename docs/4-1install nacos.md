# 4-1Nacos 的配置与安装
------------

### Nacos 单机版本

*   文件路径 /Users/brzha12/brzha\_imooc/micro\_service\_solution/soft
*   下载地址 [https://github.com/alibaba/nacos/releases](https://github.com/alibaba/nacos/releases)

```bash 
# 解压
tar -xzvf nacos-server-2.0.0.tar.gz

# 单机模式启动
./startup.sh -m standalone

```

*   访问路径：[http://127.0.0.1:8848/nacos/index.html](http://127.0.0.1:8848/nacos/index.html)
*   默认的账号密码都是 nacos, 使用无痕模式吧

### 给 Nacos 配置自定义的 MySQL 持久化

``` 
### If use MySQL as datasource:
spring.datasource.platform=mysql

### Count of DB:
db.num=1

### Connect URL of DB:
db.url.0=jdbc:mysql://127.0.0.1:3306/nacos_config?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useUnicode=true&useSSL=false&serverTimezone=UTC
db.user.0=root
db.password.0=root

```

### Nacos 集群部署方式

```
# 进入到 /Users/brzha12/brzha_imooc/micro_service_solution/soft/nacos/conf, 新建 cluster.conf 文件, 并填充内容

172.16.3.41:8848
172.16.3.41:8858
172.16.3.41:8868

# 集群必须要使用 MySQL(可以是 PG 或者是其他的数据源)作为持久化的方式, 因为需要能够访问到同一个数据源

# 复制出来三份 Nacos
➜  soft cp -p -r ./nacos nacos-8848
➜  soft cp -p -r ./nacos nacos-8858
➜  soft cp -p -r ./nacos nacos-8868

# 修改端口号
vim nacos-8848/conf/application.properties
vim nacos-8858/conf/application.properties
vim nacos-8868/conf/application.properties

# 启动三个 nacos, 不带任何参数标识集群启动
./nacos-8848/bin/startup.sh
```
