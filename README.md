# docker-lnmp

#### 介绍
docker环境下搭建的lnmp开发环境，让我们专注于程序开发，而不是环境搭建。

#### 安装

1. git clone https://gitee.com/lai390701/docker-lnmp.git
2. cd docker-lnmp
3. cp .env.example .env
4. vim .env (APP_CODE_PATH_HOST= 项目目录的相对路径，如：../../webroot)
5. docker-compose up -d --build nginx mysql redis mongo(耐心等待~)

#### 部署项目

1. cd docker-lnmp/nginx/sites
2. cp laravel.conf.example 项目名称.conf(如blog.conf）
3. vim blog.conf (修改server_name，如：blog.test；root=/var/www/你的项目名称（如blog）/public)
4. 配置系统hosts文件，加上:127.0.0.1 项目域名（如blog.test）
5. 打开浏览器输入http://blog.test即可访问你的项目（适用于大部分PHP项目）

#### 连接数据库
1. 配置my.conf(在mysql文件夹下)，在[mysqld]下增加:default-authentication-plugin=mysql_native_password
3. 如果是项目中链接数据库，需要将DB_HOST的值设置为：mysql
3. laravel中使用 artisan 导入数据的时候需要将 DB_HOST的值设置为：127.0.0.1
4. 如果是工具连接mysql则需要做如下操作:

```bash
$ docker-compose exec mysql bash # 以终端方式进入MySQL容器
$ mysql -root -proot # 建立MySQL
$ create user 'user'@'%' identified by '123456'; # 创建外网访问用户
$ grant all privileges on *.* to 'user'@'%' with grant option; # 授权
$ flush privileges; # 刷新权限
$ exit # 退出数据库
$ exit # 退出容器
```
#### 安装的容器说明

1. HAProxy: 是一款提供高可用性、负载均衡以及基于TCP（第四层）和HTTP（第七层）应用的代理软件，支持虚拟主机，它是免费、快速并且可靠的一种解决方案。
2. laravel-horizon:是由 Laravel 框架的核心开发人员开发的一个开源系统，为 Laravel 的 Redis 队列提供了强大的队列监控解决方案。 Horizon 可以帮助你轻松实现对 Redis 队列系统的一些关键指标的监控，例如作业吞吐量，运行时间等。
3. memcached:是一套分布式的快取系统，与redis相似。
4. mongo-webui:mongodb的web端管理工具
5. mysql:是一个关系型数据库管理系统，由瑞典MySQL AB 公司开发，目前属于 Oracle 旗下产品。MySQL 是最流行的关系型数据库管理系统之一，在 WEB 应用方面，MySQL是最好的 RDBMS (Relational Database Management System，关系数据库管理系统) 应用软件之一。
6. nginx:是一个高性能的HTTP和反向代理web服务器，同时也提供了IMAP/POP3/SMTP服务。
7. php-fpm:是一个PHPFastCGI管理器
8. portainer:是Docker的图形化管理工具，提供状态显示面板、应用模板快速部署、容器镜像网络数据卷的基本操作（包括上传下载镜像，创建容器等操作）、事件日志显示、容器控制台操作、Swarm集群和服务等集中管理和操作、登录用户管理和控制等功能。功能十分全面，基本能满足中小型单位对容器管理的全部需求。
9. postgres:是一种特性非常齐全的自由软件的对象-关系型数据库管理系统（ORDBMS），是以加州大学计算机系开发的POSTGRES，4.2版本为基础的对象关系型数据库管理系统。
10. rabbitmq:是实现了高级消息队列协议（AMQP）的开源消息代理软件（亦称面向消息的中间件）。
11. redis:是一个开源的使用ANSI C语言编写、支持网络、可基于内存亦可持久化的日志型、Key-Value数据库，并提供多种语言的API。
12. redis-webui:redis的web端管理工具
13. sonarqube:是一款用于代码质量管理的开源工具，它主要用于管理源代码的质量。 通过插件形式，可以支持众多计算机语言，比如 java, C#, go，C/C++, PL/SQL, Cobol, JavaScrip, Groovy 等。
14. varnish:可以有效降低web服务器的负载，提升访问速度。根据官方的说法，Varnish是一个cache型的HTTP反向代理。

### 说明
 本项目是基于laradock，删减了一些不常用的插件和配置，此项目完全可以在开发环境或者生产环境中部署，解决了项目因为环境不同导致的问题。


