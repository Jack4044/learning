# Nsight Compute

*Just a nsight compute learning note.*

# Introduction

Nsight Compute 的主要用途之一是提供对 Kernel 的 GPU 性能分析指标。

ref:

- [NVIDIA Nsight Compute](https://developer.nvidia.com/nsight-compute)

# Install

## cmd

```bash
# nsight compute
# https://developer.nvidia.com/nsight-compute
# https://developer.download.nvidia.cn/compute/cuda/repos/ubuntu2404/x86_64/

# 1. 下载
wget https://developer.download.nvidia.cn/compute/cuda/repos/ubuntu2404/x86_64/cuda-nsight-compute-12-5_12.5.1-1_amd64.deb

# 2. sudo dpkg -i 
```



## ref



# Command



## env

```bash
# docker env
docker run --gpus all -it --shm-size=256g --ulimit memlock=-1 --ulimit stack=67108864 --cap-add=SYS_ADMIN --name your_name -v /your_path:/your_path nvcr.io/nvidia/pytorch:xx.xx-py3 bash

# cmd example:
docker run --gpus all -it --shm-size=256g --ulimit memlock=-1 --ulimit stack=67108864 --cap-add=SYS_ADMIN --name xiaoyu -v /home/xiaoyu/workspace:/home/xiaoyu/workspace nvcr.io/nvidia/pytorch:22.04-py3 bash
```

## 锁频

```bash
# 查看频率
nvidia-smi dmon

# 锁频
nvidia-smi -i devices_id -lgc 1410
```

## 抓取文件

```bash
# cmd
#    其中， -o 为 output file name
#    会得到 bn.ncu-rep
ncu --set full -o bn -f --section "regex:.*" --clock-control none python bn.py
```

```python
# example: bn.py
import torch
import torch.nn as nn

m = nn.BatchNorm2d(64).cuda()
input = torch.randn(64, 64, 112, 112).cuda()
output = m(input)
```

