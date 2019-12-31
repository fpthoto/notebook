# [Docker配置远程访问](https://www.cnblogs.com/yangshaox/p/11594828.html)



*近来学习Docker部署微服务,需要配置Docker的远程访问,由于实际环境和学习资料有出入,尝试着根据网上搜索的一些相关资料进行配置,未能成功.最终通过自己摸索,成功配置Docker远程访问.现和大家分享一下:*

------

**环境介绍:**

　　**操作系统版本:** 

　　CentOS Linux release 7.7.1908 (Core)

　　***docker版本:***

　　Docker version 19.03.2, build 6a30dfc

**操作方法:**

　　1, 访问并修改Docker配置文件  *vi /lib/systemd/system/docker.service*　

  　*![img](..\docker配置\image\1817484-20190926214747673-507823979.png)*

　　2, 修改daemon.json  *vi /etc/docker/daemon.json*

　　*添加键值对*  "hosts": ["0.0.0.0:2375","unix:///var/run/docker.sock"]

　　*![img](..\docker配置\image\1817484-20190926224044817-2131152622.png)*　　

　　3, 刷新配置并重启服务

　　　　systemctl daemon‐reload

　　　　systemctl restart docker

　　***大功告成!***