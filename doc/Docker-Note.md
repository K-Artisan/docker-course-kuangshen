[TOC]

# 资源

[视频教程](https://www.bilibili.com/video/BV1og4y1q7M4?p=1)

[Docker官网](https://www.docker.com/)

[Docker文档](https://docs.docker.com/docker-for-windows/install/)

[Docker仓储](https://hub.docker.com/)

[Docker 教程](https://www.runoob.com/docker/docker-architecture.html)



# Docker学习大纲

- Docker概述
- Docker安装
- Docker命令
  - 镜像命令
  - 容器命令
  - 操作命令
  - ......
- Docker镜像
- 容器数据卷
- IDEA整合Docker
- Docker Compose
- Docker  Swarm
- CI\CD jenkins

# Docker概述

## Docker为什么会出现

一款产品：开发-上线 两套环境、应用欢迎、应用环境

开发与运维的问题：两套环境引发各种问题

Docker根据以上问题，提出了解决方案：

java-apk-发布应用商店-使用apk--安装应用

java-jar（环境）--打包项目带上环境（镜像）--Docker仓库：商店--下载我们发布的镜像--直接运行即可

隔离:Docker的核心思想

Docker通过隔离机制，可将服务器利用用到极致

在容器技术之前，我们都是使用虚拟技术

虚拟机：在windows中安装一个Vmare，通过这个软件我们可以虚拟出一台或多台电脑，笨重

### docker的特点：

- 隔离

- 小巧

  镜像（最核心的环境4m）十分小巧，运行镜像即可，几个M，秒级启动

  虚拟机 几个G, 启动几分钟



## Docker的历史

2013年Docker开源

2014年4月9日，Docker1.0发布



## Docker能干什么

### 虚拟技术的确定：

- 资源占用十分多；
- 冗余步骤多；
- 启动很慢

### 容器技术

容器技术不是模拟一个完整的操作系统，

每个容器间都是相互隔离的，每个容器都有一个属于自己的文件系统，互不影响

### DevOPS（开发运维一体化）

- 应用更快捷的交付和部署

​      传统：一堆帮助文档，安装程序

​      Docker：打包镜像，发布测试，一件运维

- 更便捷的升级和扩缩容

  使用Docker后，项目打包为一个就镜像，

- 更简单的系统运维

  在容器化之后，开发、运维、测试都是高度一致

- 更高效的计算资源利用

  Docker的内核级别的虚拟化，可以在一个物理机上运行很多个容器实例，服务器的性能可以被利用到极致

  



## Docker的基本组成

- **镜像（Image）**：Docker 镜像（Image），就相当于是一个 root 文件系统。比如官方镜像 ubuntu:16.04 就包含了完整的一套 Ubuntu16.04 最小系统的 root 文件系统。

- **容器（Container）**：镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。

  容器可以被创建、启动、停止、删除、暂停等（相当于一个简易的Linux系统）。

- **仓库（Repository）**：仓库可看成一个代码控制中心，用来保存镜像。

  可分为公有仓库和私有服务

Docker 使用客户端-服务器 (C/S) 架构模式，使用远程API来管理和创建Docker容器。

Docker 容器通过 Docker 镜像来创建。

容器与镜像的关系类似于面向对象编程中的对象与类。

![u=3715698682,4278914997&fm=26&gp](images/Docker-Note/u=3715698682,4278914997&fm=26&gp.jpg)



## 安装Docker

### CentOS安装

https://docs.docker.com/engine/install/centos/



- 卸载旧版本

  ```shell
  yum remove docker \
                    docker-client \
                    docker-client-latest \
                    docker-common \
                    docker-latest \
                    docker-latest-logrotate \
                    docker-logrotate \
                    docker-engine
  ```

  

- 在线下载并安装 yum-util

   Install the `yum-utils` package (which provides the `yum-config-manager` utility) and set up the **stable** repository. 

  ```shell
  yum install -y yum-util
  ```



- 设置镜像仓库

  默认是国外的，下载很慢

  ```she
  yum-config-manager \
      --add-repo \
      https://download.docker.com/linux/centos/docker-ce.repo
  ```

​       使用国内镜像，比如：阿里

      ```shell
   yum-config-manager \
        --add-repo \
        http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
      ```

 

- 更新yum 软件包的索引

  ```shell
  yum makecache fast
  ```

  

- 安装Docker

Docker-ce 社区版本

Docker-ee 企业版本

**安装最新版本**

```shell
yum install docker-ce docker-ce-cli containerd.io
```



**安装指定版本**

```shell
yum list docker-ce --showduplicates | sort -r
yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io
```



- 启动Docker

  ```shell
  systemctl start docker
  ```

  

- 测试Docker

  ```shell
  # 测试是否安装成功
  docker version
  ```

  测试helloword

  ```shell
  [root@centos7 ~]# docker run hello-world
  Unable to find image 'hello-world:latest' locally
  latest: Pulling from library/hello-world
  b8dfde127a29: Pull complete 
  Digest: sha256:308866a43596e83578c7dfa15e27a73011bdd402185a84c5cd7f32a88b501a24
  Status: Downloaded newer image for hello-world:latest
  
  Hello from Docker!
  This message shows that your installation appears to be working correctly.
  
  To generate this message, Docker took the following steps:
   1. The Docker client contacted the Docker daemon.
   2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
      (amd64)
   3. The Docker daemon created a new container from that image which runs the
      executable that produces the output you are currently reading.
   4. The Docker daemon streamed that output to the Docker client, which sent it
      to your terminal.
  
  To try something more ambitious, you can run an Ubuntu container with:
   $ docker run -it ubuntu bash
  
  Share images, automate workflows, and more with a free Docker ID:
   https://hub.docker.com/
  
  For more examples and ideas, visit:
   https://docs.docker.com/get-started/
  
  ```

  

- 查看镜像

```shell
[root@centos7 ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    d1165f221234   12 days ago   13.3kB
```

#### 卸载

1. Uninstall the Docker Engine, CLI, and Containerd packages:

   删除docker依赖

   ```
   $ sudo yum remove docker-ce docker-ce-cli containerd.io
   ```

2. Images, containers, volumes, or customized configuration files on your host are not automatically removed. To delete all images, containers, and volumes:

   删除docker资源

   ```
   $ sudo rm -rf /var/lib/docker
   $ sudo rm -rf /var/lib/containerd
   ```







### Window10 安装



## 检查安装

检查安装是否成功：

```powershell

```





## Run的运行和原理

```powershell
PS C:\Users\wei> docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete
Digest: sha256:95ddb6c31407e84e91a986b004aee40975cb0bda14b5949f6faac5d2deadb4b9
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

<img src="images/Docker-Note/1614134987148.png" alt="1614134987148" style="zoom:80%;" />





## 配置镜像源

### 阿里云镜像加速

https://blog.csdn.net/u011700186/article/details/109452566



### 其它源

参考资料：

​     https://blog.csdn.net/zzk437367083/article/details/108769956

​     https://www.cnblogs.com/yyee/p/12827767.html



 常用的几个国内源 

```powershell
Docker官方中国仓库：https://registry.docker-cn.com
中科大USTC: https://docker.mirrors.ustc.edu.cn
网易163镜像：http://hub-mirror.c.163.com
```



#### Docker Desktop 的配置

Windos 10系统： Docker Desktop

<img src="images/Docker-Note/1614182160197.png" alt="1614182160197" style="zoom:80%;" />



```json
{
  "registry-mirrors": [],
  "insecure-registries": [],
  "debug": false,
  "experimental": false,
  "features": {
    "buildkit": true
  }
}
```

修改为：

```json
{
  "registry-mirrors": [
   "https://registry.docker-cn.com",
   "http://hub-mirror.c.163.com",
   "https://docker.mirrors.ustc.edu.cn"
   ],
  "insecure-registries": [],
  "debug": false,
  "experimental": false,
  "features": {
    "buildkit": true
  }
}

```

点击【Apply&Restart】





# 底层原理

##   Docker是怎么工作的？

Docker是一个Client-server 结构的系统，Docker的守护进程运行在主机上，通过Socketcon从客户端访问，

DockerServer接收到Docker-Client的指令，就会执行这个命名

<img src="images/Docker-Note/1614137268132.png" alt="1614137268132" style="zoom:80%;" />



## Docker 为什么比VM快？

<img src="images/Docker-Note/docker%20vs%20vm.jpg"  />

1. Docker有比虚拟机更少的抽象层
2. Docker利用的是宿主机的内核，VM需要的是Guest OS



所以说，新建一个容器的时候，docker不需要像虚拟机一样重新加载一个操作系统，避免引导。

虚拟机是加载Guest OS（分钟级别的）

Docker是利用宿主机的操作系统，省略 了这个复杂的过程，秒级的

<img src="images/Docker-Note/docker%E6%80%A7%E8%83%BD.jpg" style="zoom:80%;" />



# Docker的常用命令



## 帮助命令

```powershell
docker version     #显示docker的版本信息
docker info        # docker的系统信息，包括镜像和容器的数量
docker 命令 --help  # 帮助命令
```

帮助文档：

https://docs.docker.com/engine/reference/commandline/cli/



## 镜像命令

### docker images 查看镜像

#### **查看所有本地的主机上的镜像**

```powershell
> docker images --help

Usage:  docker images [OPTIONS] [REPOSITORY[:TAG]]

List images

Options:
  -a, --all             Show all images (default hides intermediate images)
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print images using a Go template
      --no-trunc        Don't truncate output
  -q, --quiet           Only show image IDs
```



```powershell
> docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    bf756fb1ae65   13 months ago   13.3kB
```

- REPOSITORY： 镜像的仓储源

- TAG：镜像的标签

- IMAGE：镜像的ID

- CREATED: 镜像的创建时间

- SIZE：镜像的大小



#### **全部的images的ID**

```powershell
PS C:\Users\wei> docker images -aq
2933adc350f3
bf756fb1ae65
```





### docker search 搜索镜像

搜索镜像

```powershell
> docker search --help

Usage:  docker search [OPTIONS] TERM

Search the Docker Hub for images

Options:
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print search using a Go template
      --limit int       Max number of search results (default 25)
      --no-trunc        Don't truncate output
```



搜索mysql

```powershell
>docker search mysql
```

<img src="images/Docker-Note/1614141342274.png" alt="1614141342274" style="zoom:80%;" />



#### 搜索 `STARS `大于3000的镜像

```powershell
docker search mysql --filter=STARS=700
```

 



### docker pull 下载镜像

#### 下载镜像

```powershell
>docker pull --help

Usage:  docker pull [OPTIONS] NAME[:TAG|@DIGEST]

Pull an image or a repository from a registry

Options:
  -a, --all-tags                Download all tagged images in the repository
      --disable-content-trust   Skip image verification (default true)
      --platform string         Set platform if server is multi-platform
                                capable
  -q, --quiet                   Suppress verbose output
```



下载镜像：mysql

```powershell
# 下载镜像 docker pull 镜像名[:tag]
PS C:\Users\wei> docker pull mysql
Using default tag: latest    # 如果不写tag，默认就是lastest
latest: Pulling from library/mysql
45b42c59be33: Pull complete  # 分层下载，docker image的核心，联合文件系统
b4f790bd91da: Pull complete
325ae51788e9: Pull complete
adcb9439d751: Pull complete
174c7fe16c78: Pull complete
698058ef136c: Pull complete
4690143a669e: Pull complete
f7599a246fd6: Pull complete
35a55bf0c196: Pull complete
790ac54f4c47: Pull complete
18602acc97e1: Pull complete
365caa3500d0: Pull complete
Digest: sha256:b1cc887ed32cc6c2f217b12703bd05f503f2037892c8bb226047fe5dff85a109 #签名
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest # 真实地址
```



真实地址：

```powershell
docker pull mysql
```

 等价于

```powershell
docker pull docker.io/library/mysql:latest
```



#### 指定版本

指定的版本必须是官网存在的

比如：mysql https://hub.docker.com/_/mysql  指明了支持的版本

```C#
Supported tags and respective Dockerfile links
8.0.23, 8.0, 8, latest
5.7.33, 5.7, 5
5.6.51, 5.6
```

下载5.7版本

```powershell
PS C:\Users\wei> docker pull mysql:5.7
5.7: Pulling from library/mysql
45b42c59be33: Already exists
b4f790bd91da: Already exists
325ae51788e9: Already exists
adcb9439d751: Already exists
174c7fe16c78: Already exists
698058ef136c: Already exists
4690143a669e: Already exists
66676c1ab9b3: Pull complete
25ebf78a38b6: Pull complete
349a839d5e27: Pull complete
40b03e3e5980: Pull complete
Digest: sha256:853105ad984a9fe87dd109be6756e1fbdba8b003b303d88ac0dda6b455f36556
Status: Downloaded newer image for mysql:5.7
docker.io/library/mysql:5.7
```

注意到：

```powershell
45b42c59be33: Already exists
b4f790bd91da: Already exists
325ae51788e9: Already exists
adcb9439d751: Already exists
174c7fe16c78: Already exists
698058ef136c: Already exists
4690143a669e: Already exists
```

已经存在，这就是Docker的联合文件系统，`5.7`版本与之前我们下载最新版本公用分层

```powershell
PS C:\Users\wei> docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
mysql         5.7       5f47254ca581   2 weeks ago     449MB
mysql         latest    2933adc350f3   2 weeks ago     546MB
hello-world   latest    bf756fb1ae65   13 months ago   13.3kB
```



### 删除镜像

```powershell
PS C:\Users\wei> docker rmi --help

Usage:  docker rmi [OPTIONS] IMAGE [IMAGE...]

Remove one or more images

Options:
  -f, --force      Force removal of the image
      --no-prune   Do not delete untagged parents
```

可通过镜像的 IMAGE ID ，删除多个的Images时候， Id用空格间隔

```powershell
docker rmi 5f47254ca581               # 单个删除
docker rmi 5f47254ca581 bf756fb1ae65  # 多个删除
docker rmi -f $(docker images -a)     # 全部删除
```



示例1：单个删除

```powershell
PS C:\Users\wei> docker rmi 5f47254ca581
Untagged: mysql:5.7
Untagged: mysql@sha256:853105ad984a9fe87dd109be6756e1fbdba8b003b303d88ac0dda6b455f36556
Deleted: sha256:5f47254ca5817f99cdd387ce7345d43e770e0682a4c81b62776f3347551b1d85
Deleted: sha256:63f5d2725ff0ecffe0a7345e749d39b269a8cef04984661f0f4e752869b9fbb1
Deleted: sha256:acbe85abff4e7bbdd75a1f56ee9a095a72fcba4c226d0194d46b9a8471b1fe18
Deleted: sha256:b851a484b18c5d3d25497260c111631ae3adf924eb10baa533b2a5b03b339d1a
Deleted: sha256:b5133b076285236e7fd98c42c1f18f57e2b4ed98daaed7b0afb3b98b804d6f25

PS C:\Users\wei> docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
mysql         latest    2933adc350f3   2 weeks ago     546MB
hello-world   latest    bf756fb1ae65   13 months ago   13.3kB
```



示例2：全部删除

```powershell
PS C:\Users\wei> docker rmi -f $(docker images -a)
Error response from daemon: invalid reference format: repository name must be lowercase
Error response from daemon: invalid reference format: repository name must be lowercase
Error response from daemon: invalid reference format: repository name must be lowercase
PS C:\Users\wei> docker rmi -f $(docker images -aq)
Untagged: mysql:latest
Untagged: mysql@sha256:b1cc887ed32cc6c2f217b12703bd05f503f2037892c8bb226047fe5dff85a109
Deleted: sha256:2933adc350f3b62c05a66f700fba68ef93997d67263121250ec7848c50dcf3f5
Deleted: sha256:78b6531a3acdad2154a839ac1ec9ae2677632cc834bd996e75317f6e35717834
Deleted: sha256:f0c1c423000a6848e30ae3249c25b16f678167e56b4bb3013445b2ad1d179e8c
Deleted: sha256:4386f82820992c927b924177ed3e4c2ffd477d4db7a63539ac76fd09ee36cd89
Deleted: sha256:d7494c9168a11444d8b13558068409ace7393452f08f878686eec45122ee56c1
Deleted: sha256:08dbcab3fe630e39bbabaa9f0ae72ec6d100bf1e400ebb4b7f04151b18bca89c
Deleted: sha256:c3f78dcd6bcc4c156554296323e0eed74a4d2d93b304be15f55c1ef62dd06e0a
Deleted: sha256:f89b66495a65489290c8edb71e0dbf9e3d0d6213b82cebc2554b271599f2f99d
Deleted: sha256:1918839317d9988ff5e0168e336717e32820af1e77c3121297efc73a387ecdc5
Deleted: sha256:1d2bcd52664a92805e5f49d94d3649323dd0f5682ae3e1380fa07b7a54d6ceb0
Deleted: sha256:787de05fee96c7ba99e49f17d72aec68769a7373a8881a27917bdbf83dca58e8
Deleted: sha256:eb82f9a2fbd7a4a0fdfbe40b5e77a995ccf73ab91364d90f4db820fd59dbf63b
Deleted: sha256:9eb82f04c782ef3f5ca25911e60d75e441ce0fe82e49f0dbf02c81a3161d1300
Untagged: hello-world:latest
Untagged: hello-world@sha256:95ddb6c31407e84e91a986b004aee40975cb0bda14b5949f6faac5d2deadb4b9
Deleted: sha256:bf756fb1ae65adf866bd8c456593cd24beb6a0a061dedf42b26a993176745f6b

PS C:\Users\wei> docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE

```

其中,

- `$(docker images -a)` ：

`docker images -a`:获取所有镜像的ID

`$`:作为参数传递，可查看：https://www.cnblogs.com/chengd/p/7803664.html



- 被装载的镜像也会被删除，使用该镜像的容器还会继续运行



## 容器命令

> 说明：我们有了镜像才能创建容器



现在下载一个**Centons**镜像来测试学习

```powershell
PS C:\Users\wei> docker pull centos
Using default tag: latest
latest: Pulling from library/centos
7a0437f04f83: Pull complete
Digest: sha256:5528e8b1b1719d34604c87e11dcd1c0a20bedf46e83b5632cdeac91b8c04efc1
Status: Downloaded newer image for centos:latest
docker.io/library/centos:latest

PS C:\Users\wei> docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
centos       latest    300e315adb2f   2 months ago   209MB
```



### 新建容器并启动

```powershell
docker run [可选项] image [COMMAND] [ARG...]
```

- 可选项：

  **-- name="Name"**  :容器的名字，tomcat01, tomcat02， 用于区分容器

  **-d**:后台方式运行

  **-it**:使用交互方式运行，进入容器查看内容

  -**p**:指定容器的端口 ，-p 8080:8080  

     -p IP:主机端口:容器端口

  ​    -p 主机端口:容器端口 （常用）

  ​    -p 容器端口



```powershell
docker run -it centos /bin/bash
```

` /bin/bash`命名是Linux系统下的控制台程序。

<img src="images/Docker-Note/1614145593464.png" alt="1614145593464" style="zoom:80%;" />

看到主机名变了，`@1b5b876a7037`

```powershell
# 测试，启动并进入容器
PS C:\Users\wei> docker run -it centos /bin/bash
[root@1b5b876a7037 /]# ls # 查看容器内Centos,基础版本，很多命名都不完善
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

# 从容器中退回主机
[root@1b5b876a7037 /]# exit
exit
PS C:\Users\wei>

```



> 在容器中输入：exit
>
> 退出容器，并且容器停止运行



### 查看容器

**docker ps**

​         列出当前正在运行的容器

**-a** ：列出所有的容器，包括：当前正在运行的容器、历史运行过容器

**-n=?**：显示最近创建的容器，比如：-n=10 显示最近创建的10个容器

**-q**：显示ID



```powershell
PS C:\Users\wei> docker ps # 查看运行中容器
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
 
PS C:\Users\wei> docker ps -a # 查看曾经运行（已经退出）的容器
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS                     PORTS     NAMES
1b5b876a7037   centos         "/bin/bash"   10 minutes ago   Exited (0) 7 minutes ago             relaxed_wing
c86e09381431   bf756fb1ae65   "/hello"      3 hours ago      Exited (0) 3 hours ago               happy_snyder

PS C:\Users\wei> docker ps -n=10
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS                      PORTS     NAMES
1b5b876a7037   centos         "/bin/bash"   29 minutes ago   Exited (0) 25 minutes ago             relaxed_wing
c86e09381431   bf756fb1ae65   "/hello"      3 hours ago      Exited (0) 3 hours ago                happy_snyder

PS C:\Users\wei> docker ps -aq #显示所有容器的ID
1b5b876a7037
c86e09381431
```

 



### 退出容器

#### 容器退出并停止

```powershell
exit
```

示例：

<img src="images/Docker-Note/1614147960039.png" alt="1614147960039" style="zoom: 80%;" />





#### 容器退出不停止

```
Ctrl + P + Q
```

示例：

<img src="images/Docker-Note/1614148096413.png" alt="1614148096413" style="zoom:80%;" />





### 删除容器

```powershell
docker rm 容器ID                 # 删除指定的容器
docker rm -f $(docker ps -aq)   # 删除所有的容器
docker ps -a -q|xargs docker rm # 删除所有的容器(看下Linux管道)
```

运行中的容器不能删除



**示例：删除容器**

```powershell
PS C:\Users\wei> docker ps -a
CONTAINER ID   IMAGE          COMMAND       CREATED              STATUS                          PORTS     NAMES
9a1ba404016c   centos         "/bin/bash"   22 seconds ago       Up 21 seconds                             mystifying_haslett
8b3a69b39c57   centos         "/bin/bash"   About a minute ago   Exited (0) About a minute ago             heuristic_taussig
1b5b876a7037   centos         "/bin/bash"   38 minutes ago       Exited (0) 34 minutes ago                 relaxed_wing
c86e09381431   bf756fb1ae65   "/hello"      4 hours ago          Exited (0) 4 hours ago                    happy_snyder

PS C:\Users\wei> docker rm 9a1ba404016c # 运行中的容器不能删除
Error response from daemon: You cannot remove a running container 9a1ba404016c07663efc3e557e79ecdee9242dcfa25ebc5cc96a7a6e91ab33b0. Stop the container before attempting removal or force remove

PS C:\Users\wei> docker rm 1b5b876a7037 # 删除指定的容器
1b5b876a7037

```



### 启动和停止

```powershell
docker start 容器ID       # 启动容器
docker restart 容器ID     # 重启容器
docker stop 容器ID        # 停止当前正在运行的容器
docker kill 容器ID        # 强制停止当前容器
```





# 常用其它命令



## 后台启动容器

后台方式启动容器

```powershell
docker run -d centos
```

```powershell
PS C:\Users\wei> docker run -d centos
f3a64b6496d3d6fa5902513b27e876a838b7f39e1183842badab896b037c03e9
PS C:\Users\wei> docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
PS C:\Users\wei>
```

从上面运行的情况，可以看到：

`centos`容器是停止的，

这是比较常见的坑，容器使用后后台运行，必须要有一个前台进程，**docker发现被没用使用，就会自动停止**，

比如:nginx容器启动后，发现自己没有提供服务，就会自动停止。



## 查看日志

```powershell
PS C:\Users\wei> docker logs --help

Usage:  docker logs [OPTIONS] CONTAINER

Fetch the logs of a container

Options:
      --details        Show extra details provided to logs
  -f, --follow         Follow log output
      --since string   Show logs since timestamp (e.g.
                       2013-01-02T13:23:37Z) or relative (e.g. 42m for 42
                       minutes)
  -n, --tail string    Number of lines to show from the end of the logs
                       (default "all")
  -t, --timestamps     Show timestamps
      --until string   Show logs before a timestamp (e.g.
                       2013-01-02T13:23:37Z) or relative (e.g. 42m for 42
                       minutes)
```





**示例1：查看全部日志**

**注意，如果日志还有写入，查看日志显示是会同步更新在界面上的**

```powershell
PS C:\Users\wei> docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS     NAMES

c86e09381431   bf756fb1ae65   "/hello"                 4 hours ago      Exited (0) 4 hours ago                happy_snyder

PS C:\Users\wei> docker start c86e09381431
c86e09381431
PS C:\Users\wei> docker logs c86e09381431

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
.......


Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
 
```



**示例2：最新10条日志**

```powershell
PS C:\Users\wei> docker logs --tail 10  c86e09381431
2021-02-24T07:12:10.228036800Z
2021-02-24T07:12:10.228043600Z To try something more ambitious, you can run an Ubuntu container with:
2021-02-24T07:12:10.228047300Z  $ docker run -it ubuntu bash
2021-02-24T07:12:10.228051400Z
2021-02-24T07:12:10.228056200Z Share images, automate workflows, and more with a free Docker ID:
2021-02-24T07:12:10.228070100Z  https://hub.docker.com/
2021-02-24T07:12:10.228080200Z
2021-02-24T07:12:10.228083100Z For more examples and ideas, visit:
2021-02-24T07:12:10.228085600Z  https://docs.docker.com/get-started/
2021-02-24T07:12:10.228089000Z
```



## 查看容器内部进程信息

```powershell
 docker top CONTAINER [ps OPTIONS]
```



**示例**：

```powershell
PS C:\Users\wei> docker run -it centos /bin/bash
[root@57f4ef66e9d4 /]#
PS C:\Users\wei> docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED             STATUS          PORTS     NAMES
57f4ef66e9d4   centos    "/bin/bash"   10 seconds ago      Up 8 seconds              stoic_feistel

# docker top 容器ID
PS C:\Users\wei> docker top 57f4ef66e9d4
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                1688                1667                0                   07:40               ?                   00:00:00            /bin/bash
PS C:\Users\wei>
```

<img src="images/Docker-Note/1614152515626.png" alt="1614152515626" style="zoom:80%;" />





## 查看镜像元数据

```powershell
PS C:\Users\wei> docker inspect --help

Usage:  docker inspect [OPTIONS] NAME|ID [NAME|ID...]

Return low-level information on Docker objects

Options:
  -f, --format string   Format the output using the given Go template
  -s, --size            Display total file sizes if the type is container
      --type string     Return JSON for specified type
```





示例：

```powershell
PS C:\Users\wei> docker inspect 57f4ef66e9d4
[
    {
        "Id": "57f4ef66e9d4aef0cf9c5eb81c74b1f74058d9f4a470f3f196bbdbe345d263f4",
        "Created": "2021-02-24T07:40:17.8754651Z",
        "Path": "/bin/bash",
        "Args": [],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 1688,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2021-02-24T07:40:18.3484599Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:300e315adb2f96afe5f0b2780b87f28ae95231fe3bdd1e16b9ba606307728f55",
        "ResolvConfPath": "/var/lib/docker/containers/57f4ef66e9d4aef0cf9c5eb81c74b1f74058d9f4a470f3f196bbdbe345d263f4/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/57f4ef66e9d4aef0cf9c5eb81c74b1f74058d9f4a470f3f196bbdbe345d263f4/hostname",
        "HostsPath": "/var/lib/docker/containers/57f4ef66e9d4aef0cf9c5eb81c74b1f74058d9f4a470f3f196bbdbe345d263f4/hosts",
        "LogPath": "/var/lib/docker/containers/57f4ef66e9d4aef0cf9c5eb81c74b1f74058d9f4a470f3f196bbdbe345d263f4/57f4ef66e9d4aef0cf9c5eb81c74b1f74058d9f4a470f3f196bbdbe345d263f4-json.log",
        "Name": "/stoic_feistel",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                49,
                205
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/752ca041a862e4ee189cbcfed5386158e87940640296821516a6b468369f8901-init/diff:/var/lib/docker/overlay2/ebdf0f4e10318a6431e9b9642b087e88f7d69e6e105250230d968231cc244bae/diff",
                "MergedDir": "/var/lib/docker/overlay2/752ca041a862e4ee189cbcfed5386158e87940640296821516a6b468369f8901/merged",
                "UpperDir": "/var/lib/docker/overlay2/752ca041a862e4ee189cbcfed5386158e87940640296821516a6b468369f8901/diff",
                "WorkDir": "/var/lib/docker/overlay2/752ca041a862e4ee189cbcfed5386158e87940640296821516a6b468369f8901/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "57f4ef66e9d4",
            "Domainname": "",
            "User": "",
            "AttachStdin": true,
            "AttachStdout": true,
            "AttachStderr": true,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": true,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20201204",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "eb0a3e801021c091b00a4db99bdc64b9b9fe326950f76ed3f74bcc105d49a093",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/eb0a3e801021",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "817060ec873b77e0e729865ec7ee97f082191182de757f46acf22851d029169e",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.3",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:03",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "d65954abdc4a3e92dff0b7ba718badd760396600522391a4d5ecaa364846aa30",
                    "EndpointID": "817060ec873b77e0e729865ec7ee97f082191182de757f46acf22851d029169e",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.3",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:03",
                    "DriverOpts": null
                }
            }
        }
    }
]
```



## 进入当前正在运行的容器

通常容器都是使用**后台方式运行**的，如果需要**进入容器**进行一些配置上的修改

**方式一：**

```powershell
docker exec -it 容器ID bash/bash
```

示例：

```powershell
PS C:\Users\wei> docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS          PORTS     NAMES
57f4ef66e9d4   centos    "/bin/bash"   20 minutes ago   Up 20 minutes             stoic_feistel

PS C:\Users\wei> docker exec -it 57f4ef66e9d4 /bin/bash
[root@57f4ef66e9d4 /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```

这种方式突出容器使用

```shell
[root@57f4ef66e9d4 /]# exit
```





**方式二**

```powershell
docker attach 容器ID
```

示例：

> 使用组合键【Ctrl + P + Q】，退出不停止容器（方式一我们进入了容器，以这种方式退出）

```powershell
# Ctrl + P + Q 退出不停止容器
[root@57f4ef66e9d4 /]# read escape sequence

PS C:\Users\wei> docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS          PORTS     NAMES
57f4ef66e9d4   centos    "/bin/bash"   24 minutes ago   Up 24 minutes             stoic_feistel

PS C:\Users\wei> docker attach 57f4ef66e9d4
[root@57f4ef66e9d4 /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```



两种方式的区别：

**docker exec** ： 进入容器开启一个新的终端，可以在里面操作（常用）

证明下这种方式是开启了新的终端：

```powershell
PS C:\Users\wei> docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS         PORTS     NAMES
57f4ef66e9d4   centos    "/bin/bash"   35 minutes ago   Up 2 seconds   
xxxx
PS C:\Users\wei> docker exec -it 57f4ef66e9d4 /bin/bash
[root@57f4ef66e9d4 /]# exit #这个命令是：退出docker并停止，这个是新建的终端
exit

PS C:\Users\wei> docker ps #原始的docker终端并停止
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS          PORTS     NAMES
57f4ef66e9d4   centos    "/bin/bash"   35 minutes ago   Up 16 seconds             xxxx


```



**docker attach**：进入容器正在执行的终端，不会启动新的进程



## 从容器内拷贝文件到主机上

```powershell
docker cp --help

Usage:  docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
        docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH

Copy files/folders between a container and the local filesystem

Use '-' as the source to read a tar archive from stdin
and extract it to a directory destination in a container.
Use '-' as the destination to stream a tar archive of a
container source to stdout.

Options:
  -a, --archive       Archive mode (copy all uid/gid information)
  -L, --follow-link   Always follow symbol link in SRC_PATH
```



```powershell
docker cp 容器ID:容器内的路径 目标主机路径
```

示例：

```powershell
PS C:\Users\wei>  docker ps # 列出当前正在运行的容器
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS          PORTS     NAMES
57f4ef66e9d4   centos    "/bin/bash"   48 minutes ago   Up 12 minutes             xxxx

PS C:\Users\wei> docker attach 57f4ef66e9d4 # 进入这个容器
[root@57f4ef66e9d4 /]# cd /home
[root@57f4ef66e9d4 home]# ls 
[root@57f4ef66e9d4 home]# touch test.java # 创建一个文件
[root@57f4ef66e9d4 home]# ls
test.java

[root@57f4ef66e9d4 home]# exit  # 退出并停止容器，容器停止了，但是文件是还在的
exit
PS C:\Users\wei>  docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

# 从容器中拷贝文件到主机上（该示例是：window 10）
PS C:\Users\wei> docker cp 57f4ef66e9d4:/home/test.java f:\\tmp\\docker

```

运行上面的示例后，

<img src="images/Docker-Note/1614155921895.png" alt="1614155921895" style="zoom:80%;" />

> 现在我们是手工拷贝，以后我们可以使用 -v 卷的技术，可以实现自动同步







# 命令小结

Docker 指令图

![1614149446008](images/Docker-Note/1614149446008.png)



# 练习

## Docker 安装 Nginx

```powershell
##------------------------------下载nginx镜像
PS C:\Users\wei> docker pull nginx # 下载
Using default tag: latest
latest: Pulling from library/nginx
45b42c59be33: Pull complete
8acc495f1d91: Pull complete
ec3bd7de90d7: Pull complete
19e2441aeeab: Pull complete
f5a38c5f8d4e: Pull complete
83500d851118: Pull complete
Digest: sha256:f3693fe50d5b1df1ecd315d54813a77afd56b0245a404055a946574deb6b34fc
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest

PS C:\Users\wei> docker images # 查看镜像
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
nginx        latest    35c43ace9216   6 days ago     133MB
centos       latest    300e315adb2f   2 months ago   209MB

##------------------------------创建并运行nginx容器
# 创建并运行nginx容器，
# -d:后台运行
# 容器名：--name nginx01
# 端口映射：-p 3344:80 ，容器外部（宿主机）端口3344， 容器内nginx的端口为80
PS C:\Users\wei> docker run -d --name nginx01 -p 3344:80 nginx
188fbac2706a631faf1ad140e70c3c57848ad72afcbb3bc9636493c54bc1f7dd

PS C:\Users\wei> docker ps #查看容器是否运行了
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                  NAMES
188fbac2706a   nginx     "/docker-entrypoint.…"   6 seconds ago   Up 4 seconds   0.0.0.0:3344->80/tcp   nginx01

##------------------------------访问容器中的nginx
## 在宿主机（window 10）上请求3344端口
PS C:\WINDOWS\system32> curl.exe localhost:3344
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

##------------------------------进入容器

PS C:\WINDOWS\system32> docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                  NAMES
188fbac2706a   nginx     "/docker-entrypoint.…"   48 minutes ago   Up 48 minutes   0.0.0.0:3344->80/tcp   nginx01
PS C:\WINDOWS\system32> docker exec -it nginx01 /bin/bash #使用容器的名称（这里）
root@188fbac2706a:/# whereis nginx
nginx: /usr/sbin/nginx /usr/lib/nginx /etc/nginx /usr/share/nginx
root@188fbac2706a:/# cd etc/nginx
root@188fbac2706a:/etc/nginx# ls
conf.d  fastcgi_params  koi-utf  koi-win  mime.types  modules  nginx.conf  scgi_params  uwsgi_params  win-utf
root@188fbac2706a:/etc/nginx#


```

这时可以从宿主机（示例是**windows 10**）的`3344`端口访问Docker容器中的`Nginx`（端口：80），下面是在宿主机中使用浏览器访问：

http://localhost:3344/

<img src="images/Docker-Note/1614159728094.png" alt="1614159728094" style="zoom:80%;" />

**思考问题**：

​		我们每次改动Nginx配置文件，都需要进入容器内部？ 十分的麻烦。要是可以在容器外部提供一个映射路径，达到在容器外修改文件名，容器内部可以自动修改？

​       答：-v 数据卷



## Docker安装 Tomcat 

https://hub.docker.com/_/tomcat



```powershell
docker run -it --rm tomcat:9.0
```

run:自动检查，下载，安装

参数`rm` ：运行完之后，自动删除容器，适用于测试。

```powershell
# 下载、创建、启动、用完自动删除
PS C:\WINDOWS\system32> docker run -it --rm tomcat:9.0
Unable to find image 'tomcat:9.0' locally
9.0: Pulling from library/tomcat
0ecb575e629c: Pull complete
7467d1831b69: Pull complete
feab2c490a3c: Pull complete
f15a0f46f8c3: Pull complete
26cb1dfcbebb: Pull complete
242c5446d23f: Pull complete
f22708c7c9c1: Pull complete
d8b7e17ca4bc: Pull complete
91588c31829d: Pull complete
d97abf351b5d: Pull complete
Digest: sha256:076f0048b1340813301852336c32628e7b351202f8ece983717bbb91046e2a62
Status: Downloaded newer image for tomcat:9.0

# 下载完启动
Using CATALINA_BASE:   /usr/local/tomcat
Using CATALINA_HOME:   /usr/local/tomcat
Using CATALINA_TMPDIR: /usr/local/tomcat/temp
Using JRE_HOME:        /usr/local/openjdk-11
Using CLASSPATH:       /usr/local/tomcat/bin/bootstrap.jar:/usr/local/tomcat/bin/tomcat-juli.jar
Using CATALINA_OPTS:
NOTE: Picked up JDK_JAVA_OPTIONS:  --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/java.io=ALL-UNNAMED --add-opens=java.base/java.util=ALL-UNNAMED --add-opens=java.base/java.util.concurrent=ALL-UNNAMED --add-opens=java.rmi/sun.rmi.transport=ALL-UNNAMED
24-Feb-2021 10:11:33.211 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server version name:   Apache Tomcat/9.0.43
24-Feb-2021 10:11:33.214 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server built:          Jan 28 2021 20:25:45 UTC
24-Feb-2021 10:11:33.214 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server version number: 9.0.43.0
24-Feb-2021 10:11:33.214 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log OS Name:               Linux
24-Feb-2021 10:11:33.215 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log OS Version:            5.4.72-microsoft-standard-WSL2
24-Feb-2021 10:11:33.215 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Architecture:          amd64
24-Feb-2021 10:11:33.215 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Java Home:             /usr/local/openjdk-11
24-Feb-2021 10:11:33.215 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log JVM Version:           11.0.10+9
24-Feb-2021 10:11:33.216 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log JVM Vendor:            Oracle Corporation
24-Feb-2021 10:11:33.216 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log CATALINA_BASE:         /usr/local/tomcat
24-Feb-2021 10:11:33.216 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log CATALINA_HOME:         /usr/local/tomcat
24-Feb-2021 10:11:33.229 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: --add-opens=java.base/java.lang=ALL-UNNAMED
24-Feb-2021 10:11:33.229 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: --add-opens=java.base/java.io=ALL-UNNAMED
24-Feb-2021 10:11:33.229 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: --add-opens=java.base/java.util=ALL-UNNAMED
24-Feb-2021 10:11:33.230 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: --add-opens=java.base/java.util.concurrent=ALL-UNNAMED
24-Feb-2021 10:11:33.230 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: --add-opens=java.rmi/sun.rmi.transport=ALL-UNNAMED
24-Feb-2021 10:11:33.230 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.util.logging.config.file=/usr/local/tomcat/conf/logging.properties
24-Feb-2021 10:11:33.230 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager
24-Feb-2021 10:11:33.231 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djdk.tls.ephemeralDHKeySize=2048
24-Feb-2021 10:11:33.231 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.protocol.handler.pkgs=org.apache.catalina.webresources
24-Feb-2021 10:11:33.231 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Dorg.apache.catalina.security.SecurityListener.UMASK=0027
24-Feb-2021 10:11:33.232 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Dignore.endorsed.dirs=
24-Feb-2021 10:11:33.232 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Dcatalina.base=/usr/local/tomcat
24-Feb-2021 10:11:33.232 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Dcatalina.home=/usr/local/tomcat
24-Feb-2021 10:11:33.233 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.io.tmpdir=/usr/local/tomcat/temp
24-Feb-2021 10:11:33.237 INFO [main] org.apache.catalina.core.AprLifecycleListener.lifecycleEvent Loaded Apache Tomcat Native library [1.2.26] using APR version [1.6.5].
24-Feb-2021 10:11:33.238 INFO [main] org.apache.catalina.core.AprLifecycleListener.lifecycleEvent APR capabilities: IPv6 [true], sendfile [true], accept filters [false], random [true].
24-Feb-2021 10:11:33.238 INFO [main] org.apache.catalina.core.AprLifecycleListener.lifecycleEvent APR/OpenSSL configuration: useAprConnector [false], useOpenSSL [true]
24-Feb-2021 10:11:33.243 INFO [main] org.apache.catalina.core.AprLifecycleListener.initializeSSL OpenSSL successfully initialized [OpenSSL 1.1.1d  10 Sep 2019]
24-Feb-2021 10:11:33.659 INFO [main] org.apache.coyote.AbstractProtocol.init Initializing ProtocolHandler ["http-nio-8080"]
24-Feb-2021 10:11:33.693 INFO [main] org.apache.catalina.startup.Catalina.load Server initialization in [732] milliseconds
24-Feb-2021 10:11:33.756 INFO [main] org.apache.catalina.core.StandardService.startInternal Starting service [Catalina]
24-Feb-2021 10:11:33.756 INFO [main] org.apache.catalina.core.StandardEngine.startInternal Starting Servlet engine: [Apache Tomcat/9.0.43]
24-Feb-2021 10:11:33.769 INFO [main] org.apache.coyote.AbstractProtocol.start Starting ProtocolHandler ["http-nio-8080"]
24-Feb-2021 10:11:33.790 INFO [main] org.apache.catalina.startup.Catalina.start Server startup in [96] milliseconds
^A^C24-Feb-2021 10:11:53.700 INFO [Thread-3] org.apache.coyote.AbstractProtocol.pause Pausing ProtocolHandler ["http-nio-8080"]
24-Feb-2021 10:11:53.710 INFO [Thread-3] org.apache.catalina.core.StandardService.stopInternal Stopping service [Catalina]
24-Feb-2021 10:11:53.718 INFO [Thread-3] org.apache.coyote.AbstractProtocol.stop Stopping ProtocolHandler ["http-nio-8080"]
24-Feb-2021 10:11:53.765 INFO [Thread-3] org.apache.coyote.AbstractProtocol.destroy Destroying ProtocolHandler ["http-nio-8080"]
```



正常流程：

```powershell
#--------------------下载镜像
PS C:\Users\wei> docker pull  tomcat:9.0
9.0: Pulling from library/tomcat
Digest: sha256:076f0048b1340813301852336c32628e7b351202f8ece983717bbb91046e2a62
Status: Image is up to date for tomcat:9.0
docker.io/library/tomcat:9.0

#--------------------创建并启动容器，名为：tomcat01
PS C:\Users\wei> docker run -d -p 3355:8080 --name tomcat01 tomcat:9.0
Unable to find image 'tomcat:latest' locally
f83261e7a704759122475559dcd639958e86351fb7e901ebd3920bf9e1911595

# 启动成功后，在宿主机的浏览器中访问：localhost:3355
# 404，tomcat还没配置好，但是表明可以访问了
PS C:\Users\wei> docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS                    NAMES
f83261e7a704   tomcat    "catalina.sh run"        About a minute ago   Up About a minute   0.0.0.0:3355->8080/tcp   tomcat01
188fbac2706a   nginx     "/docker-entrypoint.…"   About an hour ago    Up About an hour    0.0.0.0:3344->80/tcp     nginx01

#--------------------进入容器
PS C:\Users\wei> docker exec -it tomcat01 /bin/bash
root@f83261e7a704:/usr/local/tomcat# ll
bash: ll: command not found

root@f83261e7a704:/usr/local/tomcat# ls -al
total 172
//.......
drwxr-xr-x 2 root root  4096 Feb 10 08:30 webapps
drwxr-xr-x 7 root root  4096 Jan 28 20:28 webapps.dist
//.....
root@f83261e7a704:/usr/local/tomcat# cd webapps
root@f83261e7a704:/usr/local/tomcat/webapps# ls
#webapps目录是空地

# 综上，发现问题：
1. linux命名少了
2. 没有webapps，原因，镜像默认是最小镜像，没有必要的都剔除掉，保证最小的可以运行环境

#--------------------配置tomact
# 把webapps.dist的文件拷贝到webapps目录下

root@f83261e7a704:/usr/local/tomcat/webapps# cd ..
root@f83261e7a704:/usr/local/tomcat# ls
BUILDING.txt  CONTRIBUTING.md  LICENSE  NOTICE  README.md  RELEASE-NOTES  RUNNING.txt  bin  conf  lib  logs  native-jni-lib  temp  webapps  webapps.dist  work
root@f83261e7a704:/usr/local/tomcat# cd webapps.dist
root@f83261e7a704:/usr/local/tomcat/webapps.dist# ls
ROOT  docs  examples  host-manager  manager

# 拷贝
root@f83261e7a704:/usr/local/tomcat/webapps.dist# cd ..
root@f83261e7a704:/usr/local/tomcat# cp -r webapps.dist/* webapps
root@f83261e7a704:/usr/local/tomcat# cd webapps
root@f83261e7a704:/usr/local/tomcat/webapps# ls
ROOT  docs  examples  host-manager  manager
# 这是可以在宿主机的浏览器中访问：localhost:3355，并能看到网站了


```

<img src="images/Docker-Note/1614163623799.png" alt="1614163623799" style="zoom:80%;" />



**思考问题**

​        我们每次要部署项目，都需要进入容器内部？ 十分的麻烦。要是可以在容器外部提供一个映射路径，webapps我们在外部放置项目，就自动同步到内部就好了。

还有就是，docker+mysql的话，删除了docker就等于把数据库删了，这不可取啊，怎么解决呢？



## 部署 es+kibana

**elasticsearch**的特点：

 暴露的端口很多

十分的耗内存

es的数据一般需要放置到安全的目录！挂载

 

https://hub.docker.com/_/elasticsearch

官网示例：

 Run Elasticsearch: 

```powershell
docker run -d --name elasticsearch --net somenetwork -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:tag
```

`--net somenetwork`网路配置，目前我们还没学，暂时不配置

```powershell
#------------------下载，安装、启动
PS C:\Users\wei> docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.6.2
Unable to find image 'elasticsearch:7.6.2' locally
7.6.2: Pulling from library/elasticsearch
ab5ef0e58194: Pull complete
c4d1ca5c8a25: Pull complete
941a3cc8e7b8: Pull complete
43ec483d9618: Pull complete
c486fd200684: Pull complete
1b960df074b2: Pull complete
1719d48d6823: Pull complete
Digest: sha256:1b09dbd93085a1e7bca34830e77d2981521a7210e11f11eda997add1c12711fa
Status: Downloaded newer image for elasticsearch:7.6.2
d9077f7ed237b6bd354fbda6b516c211bb869b7363ceeef7872b90b552587a72

PS C:\Users\wei> docker ps
CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS          PORTS                                            NAMES
d9077f7ed237   elasticsearch:7.6.2   "/usr/local/bin/dock…"   15 seconds ago   Up 11 seconds   0.0.0.0:9200->9200/tcp, 0.0.0.0:9300->9300/tcp   elasticsearch
//.....

# 访问网页
PS C:\Users\wei> curl.exe localhost:9200
{
  "name" : "d9077f7ed237",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "rgD0lAU-TlS0W6q54mXCpw",
  "version" : {
    "number" : "7.6.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",
    "build_date" : "2020-03-26T06:34:37.794943Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}

# ------------------------es 太好内存
# 启动后 Linux很卡，es耗内存，一启动就几个G内存
# docker stats 查看CPU的状态

PS C:\Users\wei> docker stats
CONTAINER ID   NAME            CPU %     MEM USAGE / LIMIT    MEM %     NET I/O           BLOCK I/O   PIDS

d9077f7ed237   elasticsearch   0.52%     1.268GiB / 12.4GiB   10.23%    936B / 0B         0B / 0B     51
f83261e7a704   tomcat01        0.15%     206.5MiB / 12.4GiB   1.63%     10kB / 126kB      0B / 0B     40
188fbac2706a   nginx01         0.00%     4.648MiB / 12.4GiB   0.04%     5.52kB / 5.88kB   0B / 0B     2

#  1.268GiB/12.4GiB   10.23%  内存1.26G ，占用了10.23%，要是我们在阿里云买了1核2G的服务器，就没法
# 玩了

#卡主，先停掉 容器
PS C:\Users\wei> docker stop d9077f7ed237
d9077f7ed237


```

以上运行的es的Docker容器太消耗内存了，这个宿主机会受到影响，

所以，需要我们在启动时，增加内存限制，修改配置文件，-e 环境配置修改

```powershell
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node"  -e ES_JAVA_OPTS="-Xms64m -Xmx512m" elasticsearch:7.6.2
```

` -e ES_JAVA_OPTS="-Xms64m -Xmx521m"`:修改环境变量，分配给ES最小内存64m,最大内存512m

示例：

```powershell
PS C:\Users\wei> docker run -d --name elasticsearch02 -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node"  -e ES_JAVA_OPTS="-Xms64m -Xmx512m" elasticsearch:7.6.2
115e4d08047a96d19158736a51089494add76ea311185d14d0262e892169db8e

PS C:\Users\wei> docker ps
CONTAINER ID   IMAGE                 COMMAND                  CREATED             STATUS             PORTS                                            NAMES
115e4d08047a   elasticsearch:7.6.2   "/usr/local/bin/dock…"   2 minutes ago       Up 2 minutes       0.0.0.0:9200->9200/tcp, 0.0.0.0:9300->9300/tcp   elasticsearch02

PS C:\Users\wei> docker stats 115e4d08047a
CONTAINER ID   NAME              CPU %     MEM USAGE / LIMIT    MEM %     NET I/O     BLOCK I/O   PIDS
115e4d08047a   elasticsearch02   0.56%     415.5MiB / 12.4GiB   3.27%     866B / 0B   0B / 0B     48

# 内存415M左右
[Ctrl + C] #停止监测

# 访问网页
PS C:\Users\wei> curl.exe localhost:9200
{
  "name" : "115e4d08047a",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "UhDLSWImRqCUsWMmsQTYRA",
  "version" : {
    "number" : "7.6.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",
    "build_date" : "2020-03-26T06:34:37.794943Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}

```



思考问题：

​        如何使用Kibana连接ES：

Kibana容器和ES容器 是相互隔离，容器间如何连接？

<img src="images/Docker-Note/1614167839459.png" alt="1614167839459" style="zoom:80%;" />



# 可视化管理工具

## portainer

先用这个

### 什么是portainer

Docker图像化界面管理工具，提供一个后台面板供我们操作，

这宿主机是Linux环境下运行

```powershell
docker run -d -p 8088:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
```

`--restart=always`:方式

`-v /var/run/docker.sock:/var/run/docker.sock`:把它的数据挂载到本机

`--privileged=true`:授权

## Portainer-CentOS

Docker图形化管理工具，提供一个后台面板供我们操作

```shell
docker run -d -p 8088:9000 \
--restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
```





在虚拟机所在的主机（Windows 10）中打开浏览器，访问：http://192.168.130.129:8088

![1616051429818](images/Docker-Note/1616051429818.png)

![1616051476697](images/Docker-Note/1616051476697.png)

选择Local
![1616051744548](images/Docker-Note/1616051744548.png)


![1616051774989](images/Docker-Note/1616051774989.png)

查看容器信息：

![1616052095211](images/Docker-Note/1616052095211.png)



## Portainer-Windows10

用以上在window 10 启动不成功（可能是因为宿主机不是Linux的原因），使用如下命令代替

```powershell
docker run -d -p 8088:9000 portainer/portainer
```

用这个启动，Windosw 10 作为宿主机，最后无法链接，

再使用如下命令：

```powershell
docker run -d -p 8089:9000 --name portainer-win10 --restart=always -v  /pipe/docker_engine:/pipe/docker_engine --privileged=true portainer/portainer
```

使用8089端口



#### 示例 : Centos

```powershell
PS C:\Users\wei> docker run -d -p 8088:9000 portainer/portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
4ce9f6f2fb3587d6910ec08768c7ae5cb81a081a36388f69aa3c99894a684c7a

PS C:\Users\wei> docker ps -a
# 启动不成功
11b3a37c3bfa   portainer/portainer   "/portainer --restar…"   4 minutes ago  Exited (1) About a minute

# 先删掉再创建容器
PS C:\Users\wei> docker rm 11b3a37c3bfa
11b3a37c3bfa

PS C:\Users\wei> docker run -d -p 8088:9000 portainer/portainer
3f9a454fc7d9d88e9e464a779c3e4bcfcd7d9c1f30c3c5371c35b382e4f3e05f
PS C:\Users\wei> docker ps
CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS          PORTS                                            NAMES
3f9a454fc7d9   portainer/portainer   "/portainer"             14 seconds ago   Up 11 seconds   0.0.0.0:8088->9000/tcp                           infallible_grothendieck

```

启动成功后，在宿主机访问：http://localhost:8088/

<img src="images/Docker-Note/1614169414995.png" alt="1614169414995" style="zoom: 50%;" />

 

输入密码：12345678，然后创建用户

<img src="images/Docker-Note/1614169968102.png" alt="1614169968102" style="zoom:80%;" />

选择Local

<img src="images/Docker-Note/1614170016193.png" alt="1614170016193" style="zoom:80%;" />

点击【Connect】，连接失败：

<img src="images/Docker-Note/1614170202363.png" alt="1614170202363" style="zoom:50%;" />

看到提示：

```powershell
Information
Manage the Docker environment where Portainer is running.

 Ensure that you have started the Portainer container with the following Docker flag:

-v "/var/run/docker.sock:/var/run/docker.sock" (Linux).

or

-v \\.\pipe\docker_engine:\\.\pipe\docker_engine (Windows).
```



看来还是得添加参数：

#### 示例 : windows 10

```powershell
PS C:\Users\wei> docker run -d -p 8089:9000 --name portainer-win10 --restart=always -v  /pipe/docker_engine:/pipe/docker_engine --privileged=true portainer/portainer
72bf22620414655270ec317f1f279b354334db76de3395747bb02caf65802da2

PS C:\Users\wei> docker ps
CONTAINER ID   IMAGE                 COMMAND                  CREATED             STATUS             PORTS                                            NAMES
72bf22620414   portainer/portainer   "/portainer"             38 seconds ago      Up 36 seconds      0.0.0.0:8089->9000/tcp                           portainer-win10


```

上述也不行，难道是

```powershell
\\.\pipe\docker_engine_linux 
```





<img src="images/Docker-Note/1614171952723.png" alt="1614171952723" style="zoom:80%;" />

还是链接失败，算了

<img src="images/Docker-Note/1614172634553.png" alt="1614172634553" style="zoom:80%;" />



平时不会使用，就算了，不折腾了



## Rancher

CI/CD再用



# Docker镜像讲解

##  镜像是什么

镜像是一种轻量级、可执行的独立软件包，用来打包软件运行环境和基于环境开发的软件，它包含运行某个软件所需的所有内容，包括代码、运行时、库、环境变量和配置环境。

所有的应用，直接打包docker镜像，就可以直接跑起来



如何得到镜像：

- 远程仓库下载

- 拷贝

- 自己制作

  

## Docker镜像加载原理

### UnionFS(联合文件系统)

**UnionFS**：Union文件系统是一种分层、轻量级并且高性能的文件系统。它支持文件系统的修改作为一次提交来一层层的叠加，同时可以将不同目录挂载到同一个虚拟文件系统（Unite serveral directories a single virtual filessytem）。 Union文件系统是Docker镜像的基础，镜像可以通过分层进行继承，基于基础镜像（没有父镜像），可以制作各种具体的应用镜像。



特性：一次同时加载多个系统文件，但从外面开起来，只是看到一个文件系统，联合加载会把各层文件系统叠加起来，这样最终文件系统会包含所有底层的文件和目录



### 镜像加载原理

Docker的镜像实际上是由一层一层的文件系统组成，这种层级的文件系统。



**bootfs(boot file system)**主要包含bootloader和 kernel.

bootloader主要是引导加载kernel。Linux刚启动时会加载bootfs文件系统，在Docker镜像的最底层是bootfs。

这一层与我们典型的Linux/Unix系统是一样的，包含boot加载和内核，当boot加载完成之后，整个内核就都在内存中了，此时内存的使用权已由bootfs转交给内核，系统也会卸载bootfs。

（bootfs 是Linux系列系统都使用的）



**rootfs(root file system)** ：在bootf之上，包含典型的Linux系统中 的/dev 、/proc、/bin、/etc等标准目录和文件，rootfs就是各种不同操作系统发行版，比如Ubuntu, Centos等等。

平时我们安装进虚拟机的Centos都是好几个G，为什么Docker这里才200M。

<img src="images/Docker-Note/1614215271119.png" alt="1614215271119" style="zoom:80%;" />

对应一个精简的OS，rootfs可以很小，只需包含最基本的命令，工具和程序就可以了。因为底层直接用Host的kernel，自己只需要提供rootfs就可以了。

由此可见，对于不同的Linux发行版，rootf会有差别，因此不同的发行版可以公用bootfs



### 理解分层

#### 分层的镜像

我们取下载一个镜像，注意观察下载的输出日志，可以看到的是一层一层的下载

<img src="images/Docker-Note/1614216068233.png" alt="1614216068233" style="zoom:80%;" />

![1614216440486](images/Docker-Note/1614216440486.png)

有一层已经下载了，就不再下载：

```powershell
a076a628af6f: Already exists
```

Docker镜像结构：

<img src="images/Docker-Note/docker%E9%95%9C%E5%83%8F%E7%BB%93%E6%9E%84.jpg" style="zoom:50%;" />

思考：为什么Docker镜像要采用这个分层的结构呢？

最大的好处是莫过于资源共享。比如：有多个镜像都从相同的Base镜像构建而来，那么宿主机只需要在磁盘上保留一分Base镜像，同时内存中也只需加载一分Base镜像，这样就可以为所有的容器服务了，而且镜像的每一层都可以被共享。

查看镜像的分层方式可以通过命令如下命令查看：

```powershell
docker images inspect IMAGE[:Tag] [IMAGE...]
```

比如查看刚才下载redis镜像信息,

```powershell
PS C:\Users\wei> docker image inspect redis

//.......
"RootFS": {
            "Type": "layers",
            "Layers": [
            "sha256:cb42413394c4059335228c137fe884ff3ab8946a014014309676c25e3ac86864",
            "sha256:8e14cb7841faede6e42ab797f915c329c22f3b39026f8338c4c75de26e5d4e82",
            "sha256:1450b8f0019c829e638ab5c1f3c2674d117517669e41dd2d0409a668e0807e96",
            "sha256:f927192cc30cb53065dc266f78ff12dc06651d6eb84088e82be2d98ac47d42a0",
            "sha256:a24a292d018421783c491bc72f6601908cb844b17427bac92f0a22f5fd809665",
            "sha256:3480f9cdd491225670e9899786128ffe47054b0a5d54c48f6b10623d2f340632"
            ]
        },
        
 //......
```

从节点`Layers`可以看到这个镜像包含的层



**理解**：

​       所有的Docker镜像都起始于一个基础镜像层，当进行修改或增加新的内容时，就会在当前镜像层之上创建新的镜像层，举一个例子，假如基于Ubuntu Linux 16.04创建的一个新的镜像，这就是新的镜像的第一层，如果该镜像中添加Python包，该镜像当前已经包含3个镜像层，如下图所示（只是一个用于演示的简单例子）

<img src="images/Docker-Note/1614218350453.png" alt="1614218350453" style="zoom: 80%;" />





在添加额外的镜像层的同时，镜像始终保持是当期所有镜像的组合，理解这一点非常重要。举一个简单的例子，

每个镜像层包含3个文件，而镜像包含了来自两个镜像层的6个文件

<img src="images/Docker-Note/1614218654133.png" alt="1614218654133" style="zoom:80%;" />

上图中的镜像层跟之前图的略有区别，主要的目的是便于展示文件。

下图展示了一个稍微复杂的三层镜像，在外部看来整个镜像只有6个文件，因为最上层的文件7是文件5的一个更新版本

<img src="images/Docker-Note/1614218880092.png" alt="1614218880092" style="zoom:80%;" />



这种情况下，上层镜像层中大文件覆盖了底层镜像层中欧大文件 ，这样就是的文件的更新版本作为 一个新的镜像层添加到镜像中，

Docker通过存储引擎（新版本采用快照机制）的方式来实现镜像层堆栈，并保证多镜像层对外展示为统一的文件系统。

Linux上可用的存储 引擎有AUFS、Overlay2、DeviceMapper Btfs以及ZFS。顾名思义，每种存储疫情都基于Linux中 对应的文件系统或者块设备技术，并且每种存储疫情都有其独特的性能特点。

Docker在Windows上仅支持windowsfilter 一种存储引擎，该引擎基于NTFS文件系统之上实现 分层和COW

下图展示了与系统显示相同的三层 镜像，所有镜像层堆叠并合并，对外体统统一的视图

<img src="images/Docker-Note/1616063852991.png" alt="1616063852991" style="zoom: 80%;" />



特点

Docker镜像都是只读，当容器启动时，一个新的可写层被加载到啊镜像的顶部

这一层就是我们通常说的容器层，容器之下都叫镜像层

 <img src="images/Docker-Note/1616064265576.png" alt="1616064265576" style="zoom:80%;" />

如何提交一个自己的镜像，commit镜像



# Commit镜像

## 创建新镜像

docker commit 提交容器成为一个新的副本

```shell
docker commit  -m="提交信息 描述"  -a="作者" 容器ID 目标镜像名:[TAG]
```

实战测试

下载运行

```shell
[root@centos7 ~]# docker pull tomcat:9.0
[root@centos7 ~]# docker run -it -p 8080:8080 tomcat 

```

使用Xshell登录Linux系统，并进入tomcat容器

```shell
[root@centos7 ~]# docker ps
CONTAINER ID   IMAGE                 COMMAND             CREATED         STATUS         PORTS                    NAMES
1f7b945ffe13   tomcat                "catalina.sh run"   5 minutes ago   Up 5 minutes   0.0.0.0:8080->8080/tcp   laughing_bhabha

[root@centos7 ~]# docker exec -it 1f7b945ffe13 /bin/bash
root@1f7b945ffe13:/usr/local/tomcat# 

```

启动一个默认的tomcat，发现这个默认的tomcat是一个没有webapps应用的，镜像的原因，官方 的镜像默认webapps下面是没有文件的

```shell
root@1f7b945ffe13:/usr/local/tomcat# cd webapps
root@1f7b945ffe13:/usr/local/tomcat/webapps# ls
```



自己拷贝文件

```shell
root@1f7b945ffe13:/usr/local/tomcat# cp -r webapps.dist/* webapps/
root@1f7b945ffe13:/usr/local/tomcat# cd webapps
root@1f7b945ffe13:/usr/local/tomcat/webapps# ls
ROOT  docs  examples  host-manager  manager

```

测试下tomcat部署是否成功，在虚拟机所在Windows10 中打开浏览器，访问：

http://192.168.130.129:8080/

<img src="images/Docker-Note/1616066369653.png" alt="1616066369653" style="zoom:80%;" />



现在我们把这个已经修改后的容器打包成功一个新的镜像**mytomcat**，

```shell
root@1f7b945ffe13:/usr/local/tomcat/webapps# exit
exit
[root@centos7 ~]# docker ps
CONTAINER ID   IMAGE                 COMMAND             CREATED          STATUS         PORTS                    NAMES
1f7b945ffe13   tomcat                "catalina.sh run"   25 minutes ago   Up 9 minutes   0.0.0.0:8080->8080/tcp   laughing_bhabha

# 创建一个新的镜像 
[root@centos7 ~]# docker  commit -a="kkk" -m="add webapps app" 1f7b945ffe13 mytomcat:1.0
sha256:c95e6d30363e77e6e36997bde0a2822d8d1d4279555ea70eb5d1bf7b2d4a2e1d
[root@centos7 ~]# docker images
REPOSITORY            TAG       IMAGE ID       CREATED         SIZE
mytomcat              1.0       c95e6d30363e   6 seconds ago   672MB
tomcat                9.0       08efef7ca980   4 days ago      667MB
tomcat                latest    08efef7ca980   4 days ago      667MB

```

> 说明：docker commit  -m="提交信息 描述"  -a="作者" 容器ID 目标镜像名:[TAG]



## 使用新镜像

这个新的镜像**mytomcat**,其weapps下有文件，以后使用这个新镜像运行的容器就再也不需要往weapps文件里面 拷贝文件了。

以后就可以使用这个自己的修改过新的镜像,

```shell

#把旧的tomcat容器停止，因为端口冲突
[root@centos7 ~]# docker start 1f7b945ffe13

[root@centos7 ~]# docker run -it -p 8090:8090 mytomcat:1.0
ctl+C
[root@centos7 ~]# docker ps -a
CONTAINER ID   IMAGE                 COMMAND             CREATED          STATUS                        PORTS                    NAMES

ac3799d198f9   tomcat                "catalina.sh run"   12 minutes ago   Up 11 minutes                 0.0.0.0:8080->8080/tcp   trusting_snyder

1f7b945ffe13   tomcat                "catalina.sh run"   5 minutes ago   Up 5 minutes 

#运行新的tomcat
[root@centos7 ~]# docker start ac3799d198f9 

```

访问：http://192.168.130.129:8080/ 可以访问



## 原始镜像与新的镜像对比

<img src="images/Docker-Note/1616064265576.png" alt="1616064265576" style="zoom:80%;" />

把我们已经操作过的层（上图的容器层）再次打包成一个新的镜像，一层一层的叠加

<img src="images/Docker-Note/1616067003945.png" alt="1616067003945" style="zoom:80%;" />



****

参生新的一层



- 原tomcat

```shell
[root@centos7 ~]# docker inspect tomcat 
            "Layers": [                                                              "sha256:0e41e5bdb921aea3c3c9bb5eb61c004fdb6286fe8800f266887243e268fb957a",
  "sha256:644448d6e8779b7078d69c3a080529aa7924f8efb555c589839557f3597bd368",
  "sha256:81496d8c72c2f2c22627354efc459ef8d703e8110d72b8f0d8af121361d5c82c",
  "sha256:bde301416dd2132d01b1b042eed25f8aa59350fbbe61ebdacd04b98148f9c07e",
  "sha256:59f1e8e1ce6624b08eb273d66bcf2b524a7238c96f170049295f5051b087da5c",
  "sha256:a4ed737b0c8fe6e638bb1c24e611e7f6f1b74ba08f7900305e04e84caf82a6e2",
  "sha256:b219714e1f91e969787b364a328b28f430d6073cf91ccabe668b0e807aa28887",
  "sha256:6921406a23782bcd0b554108285f16251c6e18fc1a9e61735fb6fbd0e0a5e170",
  "sha256:7e6c506447e919b7fd5d1652cef148a34fcc27cee8a755e6f16618f897adf0a6",
  "sha256:34c7884ee1258cfbfb60f91e090e6fc58ced04dc36f035743c0dbc9613ff8a09"
            ]

```

tomcat原有10层，



- 新mytomcat镜像

```shell
[root@centos7 ~]# docker inspect mytomcat:1.0
            "Layers": [
               "sha256:0e41e5bdb921aea3c3c9bb5eb61c004fdb6286fe8800f266887243e268fb957a",
               "sha256:644448d6e8779b7078d69c3a080529aa7924f8efb555c589839557f3597bd368",
               "sha256:81496d8c72c2f2c22627354efc459ef8d703e8110d72b8f0d8af121361d5c82c",
               "sha256:bde301416dd2132d01b1b042eed25f8aa59350fbbe61ebdacd04b98148f9c07e",
               "sha256:59f1e8e1ce6624b08eb273d66bcf2b524a7238c96f170049295f5051b087da5c",
               "sha256:a4ed737b0c8fe6e638bb1c24e611e7f6f1b74ba08f7900305e04e84caf82a6e2",
               "sha256:b219714e1f91e969787b364a328b28f430d6073cf91ccabe668b0e807aa28887",
               "sha256:6921406a23782bcd0b554108285f16251c6e18fc1a9e61735fb6fbd0e0a5e170",
               "sha256:7e6c506447e919b7fd5d1652cef148a34fcc27cee8a755e6f16618f897adf0a6",
               "sha256:34c7884ee1258cfbfb60f91e090e6fc58ced04dc36f035743c0dbc9613ff8a09",
               "sha256:9287f4ff67de7e69e970708532da8724c97527228db46e0f9593ee2d1518b595"
            ]

```

共11层，多出了这一层：

```shell
"sha256:9287f4ff67de7e69e970708532da8724c97527228db46e0f9593ee2d1518b595"
```



【里程碑：至此 Docker入门】



# 容器数据卷





# DockerFile





# Docker 网络





# 企业实战

## Docker Compose



## Docker Swarm



集群



## CI/CD Jenkins

