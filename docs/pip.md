# Pip

*Just a pip learning note.*

## Introduction

pip 是 Python 包管理工具，该工具提供了对Python 包的查找、下载、安装、卸载的功能。

## Install

### cmd

```bash
# pip

################################################################################
# step1. 下载
################################################################################

# python3
sudo apt install python3-pip

################################################################################
# step2. 设置
################################################################################

# 设置 pip 命令自动补全
pip completion --bash >> ~/.bashrc

# 查看源
pip config list

# 更换清华源
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

### ref

- [Python pip 安装与使用 | 菜鸟教程](https://www.runoob.com/w3cnote/python-pip-install-usage.html)
- [PIP 命令自动补全](https://www.jianshu.com/p/dc376efab7c0)
- [Pip源设置（使用清华源）](https://www.cnblogs.com/missjade/p/12992038.html)
- [查看pip源和换源](https://blog.csdn.net/qq_40891747/article/details/116592227)

## Command

### cmd

**pip 基础命令**

| 命令          | 说明          |
| ------------- | ------------- |
| pip --version | 查看 pip 版本 |

