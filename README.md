# DockerSutdy  

### learn for docker

<https://docs.docker.com/engine/install/centos/>
官方文档查看安装

# 1.Start Docker

```shel
sudo syetemctl start docker
```

## 补充

**linux切换root用户**

```shell
 su 密码
```





# 2.Docker的常用指令

## 帮助指令

```shell
docker version	 # 显示docker的版本信息
docker info     # 显示docker的系统信息，包括镜像和容器的数量
docker 命令  --help # 帮助命令
```

帮助文档的地址：[Reference documentation | Docker Documentation](https://docs.docker.com/reference/)



## 镜像命令

**docker images**查看本地所有主机的镜像

```shell
[root@localhost tyb]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    feb5d9fea6a5   14 months ago   13.3kB

#解释
REPOSITORY 镜像的仓库源
TAG 		镜像的标签
IMAGE ID 	镜像的id
CREATED 	镜像的创建时间
SIZE      	镜像的大小

#可选项
  -a, --all             Show all images (default hides intermediate images) #列出所有的镜像 
  -q, --quiet           Only show image IDs #只显示镜像的id

```

**docker search 搜索镜像**

```shell
[root@localhost tyb]# docker search mysql
NAME                            DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql                           MySQL is a widely used, open-source relation…   13513     [OK]       
mariadb                         MariaDB Server is a high performing open sou…   5157      [OK]       

#可选项 通过搜收藏来过滤
--filter=STARS=3000 #搜索出来的镜像就是START>3000的
[root@localhost tyb]# docker search mysql --filter=STARS=3000
NAME      DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql     MySQL is a widely used, open-source relation…   13513     [OK]       
mariadb   MariaDB Server is a high performing open sou…   5157      [OK] 
```

**docker pull** 下载镜像

```shell
# 下载镜像 docker pull镜像名 [:tag]版本号
[root@localhost tyb]# docker pull mysql
Using default tag: latest #如果不写 tag，默认就是 latest
latest: Pulling from library/mysql
72a69066d2fe: Pull complete  #分层下载，docker image的核心 联合文件系统
93619dbc5b36: Pull complete 
99da31dd6142: Pull complete 
626033c43d70: Pull complete 
37d5d7efb64e: Pull complete 
ac563158d721: Pull complete 
d2ba16033dad: Pull complete 
688ba7d5c01a: Pull complete 
00e060b6d11d: Pull complete 
1c04857f594f: Pull complete 
4d7cfa90e6ea: Pull complete 
e0431212d27d: Pull complete 
Digest: sha256:e9027fe4d91c0153429607251656806cc784e914937271037f7738bd5b8e7709 #签名
Status: Downloaded newer image for mysql:latest 
docker.io/library/mysql:latest #真实地址

#等价与它
docker pull mysql
docker .io/library/mysql:latest

[root@localhost tyb]#   docker pull mysql:5.7
5.7: Pulling from library/mysql
72a69066d2fe: Already exists 
93619dbc5b36: Already exists 
99da31dd6142: Already exists 
626033c43d70: Already exists 
37d5d7efb64e: Already exists 
ac563158d721: Already exists 
d2ba16033dad: Already exists 
0ceb82207cd7: Pull complete 
37f2405cae96: Pull complete 
e2482e017e53: Pull complete 
70deed891d42: Pull complete 
Digest: sha256:f2ad209efe9c67104167fc609cca6973c8422939491c9345270175a300419f94
Status: Downloaded newer image for mysql:5.7
docker.io/library/mysql:5.7

```

**docker rmi** 删除镜像

```shell
[root@localhost tyb]#  docker rmi -f 镜像id  # 删除指定的容器
[root@localhost tyb]#  docker rmi -f 镜像id 镜像id 镜像id 镜像id  #删除多个容器
[root@localhost tyb]#  docker rmi -f $(docker images -aq) #删除全部的容器
```



## 容器命令

说明：我们有了镜像才可以创建容器，linux，下载一个centos镜像来测试学习

```shell
docker pull centos
```

**新建容器并启动**

```shell
 docker run [可选参数] image
 
 #参数说明
 --name="Name" 容器名字 tomcat01 tomcat02，来区分容器
 -d 			后台方式运行
 -it			使用交互方式运行，进入容器内查看内容
 -p				指定容器的端口 -p 8080:8080
 	-p ip;主机端口：容器端口
 	-p 主机端口：容器端口 （常用）
 	-p 容器端口
 	容器端口
 -P				随机指定端口
 
 #测试，启动并进入容器
[root@localhost tyb]# docker run -it centos /bin/bash
[root@a577be7d0f66 /]# ls  #查看容器内的centos，基础都是不完善的
bin  etc   lib	  lost+found  mnt  proc  run   srv  tmp  var
dev  home  lib64  media       opt  root  sbin  sys  usr

#从容器中退回主机
[root@a577be7d0f66 /]# exit
exit
[root@localhost /]# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

```

**列出所有的运行的容器**

```shell
#docker ps 命令
-a #列出当前正在运行的容器+带出历史运行过的容器 （all）

[root@localhost /]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@localhost /]# docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED         STATUS                     PORTS     NAMES
a577be7d0f66   centos        "/bin/bash"   6 minutes ago   Exited (0) 3 minutes ago             nifty_chandrasekhar
b239193c61a7   hello-world   "/hello"      18 hours ago    Exited (0) 18 hours ago              beautiful_hawking
```



































