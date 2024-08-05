# Docker
*Just a docker learning note.*

## Introduction

Docker 的元素；

- ***Docker 引擎***：负责在主机上构建和运行容器。
- ***Docker Daemon***：管理 Docker 容器的运行进程。
- ***Docker 客户端***：一个单独的命令工具，用于执行命令并与正在运行的容器交互。
- ***Docker Compose***：用于轻松管理为单个服务提供支持的多个容器。

## Install

### cmd

```bash
# ubuntu24.04 install docker
# ps: 自测官方源下载有问题，建议使用国内源！

################################################################################
# step1. 配置 Docker 存储库
################################################################################

# 1.1. 执行更新和升级系统的基本步骤
sudo apt update && sudo apt upgrade -y
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

# 1.2. 导入 docker apt 存储库 GPG 密钥
# 官方源
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
# 国内原
curl -fsSL https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/ubuntu/gpg | sudo apt-key add -

# 1.3. 将存储库添加到 apt 源（source.list）
# 官方源
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
# 国内源
sudo add-apt-repository "deb [arch=amd64] https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/ubuntu $(lsb_release -cs) stable"

# 1.4. 更新 apt 软件包缓存
sudo apt update

################################################################################
# step2. 安装 Docker 引擎包
################################################################################

# 2.1. 配置存储库后，可以使用 apt 包管理器轻松安装该包。
# 安装的组件包括：
#     docker-ce：Docker Engine。
#     docker-ce-cli：用于与 Docker 守护进程通信的命令行工具。
#     containerd.io：管理容器生命周期的容器运行时环境。
#     docker-buildx-plugin：增强镜像构建功能的 Docker 扩展工具，特别是在多平台构建方面。
#     docker-compose-plugin：通过单个 YAML 文件管理多容器 Docker 应用的配置管理插件。
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# 2.2. 在软件包列表中，我们包含了顺利运行所需的其他 Docker 依赖项。通过查询安装的版本来验证其是否有效。
docker --version

# 2.3. Compose 插件也应该可以在命令行中使用。
docker compose version

################################################################################
# step3. 建立 Docker 用户组
################################################################################

# 3.1. 建立 docker 组
sudo groupadd docker

# 3.2. 将当前用户加入 docker 组
sudo usermod -aG docker $USER

# 3.3. 重启 docker 服务
sudo service docker restart

# 3.4. 切换当前回话到新的 group
newgrp - docker

################################################################################
# step4. 测试 Docker 是否安装正确
################################################################################

docker run hello-world
```

### ref

- [在 Ubuntu 24.04 上安装 Docker 并运行 Docker 容器](https://cn.linux-console.net/?p=31545)
- [如何在 Ubuntu 24.04 LTS 上安装 Docker](https://www.sysgeek.cn/install-docker-ubuntu/)
- [Ubuntu16.04 安装 Docker及"gpg: 找不到有效的 OpenPGP 数据"解决方法](https://cloud.tencent.com/developer/article/1843420)

## Command

### cmd

**docker 基础命令**

| 命令           | 说明                                     |
| -------------- | ---------------------------------------- |
| docker version | 显示 Docker 版本信息。                   |
| docker info    | 显示 Docker 系统信息，包括镜像和容器数。 |

**docker 镜像命令**

| 命令          | 说明           |
| ------------- | -------------- |
| docker images | 列出本地镜像。 |

**docker 容器命令**

| 命令      | 说明       |
| --------- | ---------- |
| docker ps | 列出容器。 |

### ref

- [Docker 命令大全 | 菜鸟教程](https://www.runoob.com/docker/docker-command-manual.html)
- [docker介绍及常用命令大全（超详细）](https://blog.csdn.net/qq_25919879/article/details/127054566)

