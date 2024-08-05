# Conda

*Just a conda learning note.*

## Introduction

Conda 是在 Windows，macOS 和 Linux 上运行的开源软件包管理系统和环境管理系统。

- Anaconda
  - download: 
    - https://repo.anaconda.com/archive/
    - https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/
  
- Miniconda：是 Anaconda 的一个小型引导版本，它只包含 conda、Python 及其所依赖的包，以及少量其他有用的包，包括 pip、zlib 和其他一些包。

  - doc: https://docs.conda.io/en/latest/miniconda.html

  - download: https://repo.anaconda.com/miniconda/

conda install vs pip install:

1. 区别

   - conda 可以管理非 python 包，pip 只能管理 python 包。

   - conda 自己可以用来创建环境，pip 不能，需要依赖 virtualenv 之类的。
   - conda 安装的包是编译好的二进制文件，安装包文件过程中会自动安装依赖包；pip 安装的包是 wheel 或源码，装过程中不会去支持 python 语言之外的依赖项。
   - conda 安装的包会统一下载到一个目录文件中，当环境 B 需要下载的包，之前其他环境安装过，就只需要把之间下载的文件复制到环境 B 中，下载一次多次安装。pip 是直接下载到对应环境中。
   - conda 只能在 conda 管理的环境中使用，例如比如 conda 所创建的虚环境中使用。pip 可以在任何环境中使用，在 conda 创建的环境中使用 pip 命令，需要先安装 pip（conda install pip ），然后可以环境 A 中使用 pip 。conda 安装的包，pip 可以卸载，但不能卸载依赖包，pip 安装的包，只能用 pip 卸载。

2. 安装在哪里

   - conda install xxx：这种方式安装的库都会放在 anaconda3/pkgs 目录下，这样的好处就是，当在某个环境下已经下载好了某个库，再在另一个环境中还需要这个库时，就可以直接从 pkgs 目录下将该库复制至新环境而不用重复下载。
   - pip install xxx：分两种情况，一种情况就是当前 conda 环境的 python 是 conda 安装的，和系统的不一样，那么 xxx 会被安装到 anaconda3/envs/current_env/lib/python3.x/site-packages 文件夹中，如果当前 conda 环境用的是系统的 python，那么 xxx 会通常会被安装到 ~/.local/lib/python3.x/site-packages 文件夹中。

3. 如何判断 conda 中某个包是通过 conda 还是 pip 安装的
   - 执行 conda list ，用 pip 安装的包显示的 build 项目为 pypi。

## Install

### cmd

```bash
# Anaconda

################################################################################
# step1. 下载 Anaconda 安装程序
################################################################################

# 访问 Anaconda 网站并下载适用于 Linux 的最新版本 Anaconda。(或者手动下载)
wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-2024.06-1-Linux-x86_64.sh

################################################################################
# step2. 运行安装脚本
################################################################################

# 打开终端，导航到下载目录，然后执行脚本。
# 安装过程将解压并安装 Anaconda。在此过程中，选择通过更新 shell 配置文件来初始化 Anaconda，从而自动激活基础环境。
bash Anaconda3-2024.06-1-Linux-x86_64.sh

################################################################################
# step3. 设置环境
################################################################################

# vim ~/.bashrc 添加到环境
export PATH="/home/xiaoyu/anaconda3/bin:$PATH"

# 重新启动终端或获取 .bashrc 文件来刷新环境变量。
source ~/.bashrc

# Anaconda 允许为不同的项目创建隔离的环境。 (base) 环境是默认环境，但您可以根据需要创建和激活新环境。要在终端启动时自动停用基本环境，请运行：
conda config --set auto_activate_base false

################################################################################
# step4. conda 数据源管理
################################################################################

# 显示目前 conda 的数据源有哪些
conda config --show channels

# 添加数据源：例如，添加清华 anaconda 镜像：
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/

# 设置搜索时显示通道地址
conda config --set show_channel_urls yes

# 删除数据源
conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
```

### ref

- [在 Ubuntu 24.04 上安装 Anaconda](https://cn.linux-console.net/?p=31096)
- [anaconda安装ubuntu20.4中](https://www.cnblogs.com/zh-clara/p/15242294.html)

## Command

### cmd

**conda 基础命令**

| 命令                  | 说明                  |
| --------------------- | --------------------- |
| conda --version       | 查看 conda 版本       |
| conda config --show   | 查看 conda 的环境配置 |
| conda update conda    | 更新 conda            |
| conda update Anaconda | 更新 Anaconda         |

**conda 环境管理**

| 命令                                      | 说明                                               |
| ----------------------------------------- | -------------------------------------------------- |
| conda env list                            | 查看有哪些虚拟环境                                 |
| conda info -e                             | -                                                  |
| conda info --envs                         | -                                                  |
| conda activate env_name                   | 激活名字为 env_name 的虚拟环境                     |
| conda activate                            | 激活默认虚拟环境（base）                           |
| conda deactive                            | 退出虚拟环境（回到 base 虚拟环境）                 |
| conda create -n env_name python=3.8       | 创建 python 版本为 3.8、名字为 env_name 的虚拟环境 |
| conda create -n env_name                  | 创建 python 版本为最新、名字为 env_name 的虚拟环境 |
| conda remove --name env_name --all        | 将虚拟环境 env_name 及其中所安装的包都删除         |
| conda remove --name env_name package_name | 删除虚拟环境 env_name 中的包 package_name          |

**conda 包管理**

| 命令                         | 说明                                                   |
| ---------------------------- | ------------------------------------------------------ |
| conda list                   | 查询当前环境中安装的包                                 |
| conda search package_name    | 查询当前 Anaconda repository 中是否有包 package_name   |
| conda install package_name   | 在当前虚拟环境中安装包 package_name                    |
| conda install numpy=0.20.3   | 在当前虚拟环境中安装 0.20.3 版本的 numpy 包            |
| conda update numpy           | 将 numpy 包更新到最新版本                              |
| conda uninstall package_name | 卸载包 package_name 及所有依赖于 package_name 的其他包 |
| conda clean -p               | 删除没有用的包（--packages）                           |

### ref

- [Anaconda conda常用命令：从入门到精通](https://blog.csdn.net/chenxy_bwave/article/details/119996001)
- [conda命令大全: 安装，更新，创建，激活，关闭，查看，卸载，删除，清理，重命名，换源，问题](https://www.cnblogs.com/IllidanStormrage/p/15787580.html)
- [【Conda】【Anaconda】Linux下conda设置自动补全](https://blog.csdn.net/RadiantJeral/article/details/126672081)

