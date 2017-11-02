## Docker是什么
Docker是一个开源的引擎，可以轻松的为任何应用创建一个轻量级的、可移植的、自给自足的容器。开发者在笔记本上编译测试通过的容器可以批量地在生产环境中部署，包括VMs（虚拟机）、bare metal、OpenStack 集群和其他的基础应用平台。 

## 应用场景
Docker通常用于如下场景：

1. web应用的自动化打包和发布；
2. 自动化测试和持续集成、发布；
3. 在服务型环境中部署和调整数据库或其他的后台应用；
4. 从头编译或者扩展现有的OpenShift或Cloud Foundry平台来搭建自己的PaaS环境。

## Docker容器与虚拟机区别

 ![Image of Yaktocat](https://pic3.zhimg.com/50/20006deca0fccda0d536edd626835e9e_720x4096.jpg)
 
![Image of Yaktocat](https://www.docker.com/sites/default/files/VM%402x.png)

## 镜像与容器
镜像是一个轻量级，独立的可执行包，其中包含运行一段软件所需的一切，包括代码，运行时，库，环境变量和配置文件。

容器是镜像的运行时实例 - 实际执行时镜像在内存中的内容。 默认情况下，它与主机环境完全隔离，只能访问主机文件和端口(如果配置为这样做).

## Dockerfile
Docker可以通过Dockerfile来生成镜像.Dockerfile中包含了所有来组装镜像的命令.

例:
```
FROM java:openjdk-8u111-jdk-alpine

Add build/libs/*.jar app.jar
ENTRYPOINT ["java", "-jar","/app.jar"]
```

Build Image command:
```
docker build -t [TAG_NAME] .
```
