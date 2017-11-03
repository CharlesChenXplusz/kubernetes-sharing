## Docker是什么
Docker是轻量级的、可移植的、自给自足的容器。

## Docker能做什么
可以将应用程序及其依赖打包,用于开发,传输及部署.

 ![Docker](https://www.docker.com/sites/default/files/Package%20software%40x2.png)

## Docker容器与虚拟机区别
* Container
 Containers are an abstraction at the app layer that packages code and dependencies together. Multiple containers can run on the same machine and share the OS kernel with other containers, each running as isolated processes in user space. Containers take up less space than VMs (container images are typically tens of MBs in size), and start almost instantly.

 ![Docker](https://www.docker.com/sites/default/files/Container%402x.png)

 * Virtual machines (VMs) are an abstraction of physical hardware turning one server into many servers. The hypervisor allows multiple VMs to run on a single machine. Each VM includes a full copy of an operating system, one or more apps, necessary binaries and libraries - taking up tens of GBs. VMs can also be slow to boot.

 
![Vm](https://www.docker.com/sites/default/files/VM%402x.png)

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

Run Image:
```
docker run [TAG_NAME]
```

Publish Image:
```
docker tag [TAG_NAME] [YOUR_HUB_NAME]/[YOUR_TAG_NAME]
dokcer push [YOUR_HUB_NAME]/[YOUR_TAG_NAME]
```