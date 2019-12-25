# docker配置

### docker安装

 卸载旧版本

``````shell
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
``````



安装所需的软件包。yum-utils 提供了 yum-config-manager ，并且 device mapper 存储驱动程序需要 device-mapper-persistent-data 和 lvm2

``````
yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
``````

(不必要)使用以下命令来设置稳定的仓库。注:版改用国内镜像

``````
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
``````

安装

``````
yum install docker-ce docker-ce-cli containerd.io
``````

### docker配置

1 更换国内镜像

需要在/etc/docker下创建daemon.json文件:

{
  "registry-mirrors": ["https://7a571b6z.mirror.aliyuncs.com"]
}

### docker启动所有

``````
 docker restart $(docker ps -a -q)
``````

则需要启动docker服务，执行：

```
service docker start
```



## tomcat安装配置



不挂载启动

``````
dockerrun -p 8080:8080 --name tomcat -d tomcat
``````





## nginx安装配置

1 进入容器拷贝配置文件

``````shell
docker exec -it ngx_demo /bin/bash
docker cp ngx_demo:/etc/nginx/nginx.conf /usr/docker/nginx81/nginx.conf
``````

2 挂载启动

``````shell
docker run -p 80:80 --name ngx_demo -v /usr/docker/nginx81/nginx.conf:/etc/nginx/nginx.conf:ro -d nginx 
``````

3 关闭

``````shell
docker rm -f ngx_demo 
``````

## mysql安装配置

1 Mysql8.0配置:

``````sql
GRANT ALL ON . TO 'root'@'%';
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
flush privileges;
``````

2 挂载启动

``````shell
docker run -p 3306:3306 --name mysql -v /usr/docker/mysql/conf:/etc/mysql/conf.d -v /usr/docker/mysql/logs:/logs -v /usr/docker/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql
``````

3 关闭

``````shell
docker rm -f mysql 
``````

------

```shell
docker run -d -p 1984:1984 oddrationale/docker-shadowsocks -s 0.0.0.0 -p 1984 -k $SSPASSWORD -m aes-256-cfb
```

