# CUDA

*Just a cuda learning note.*

# Introduction

在高性能计算领域，CUDA（[Compute Unified Device Architecture](https://en.wikipedia.org/wiki/CUDA)）是一项革命性的技术。它由 Nvidia 开发，是一个并行计算平台和应用程序编程接口（API）模型，利用 NVIDIA GPU（图形处理器）的强大计算能力来提高软件应用程序的计算速度和效率。

CUDA 对 Ubuntu 用户、程序员和开发者的重要性主要包括：

- 性能增强：CUDA 让程序能够在 Nvidia 的 GPU上执行，这些 GPU 能够同时处理多任务。这种并行处理能力可以显著提升应用程序的速度，尤其是需要进行大量计算的应用程序。
- 多功能性：CUDA 支持多种编程语言，包括 C、C++、Python 和 Fortran。您可以使用喜欢的语言来充分利用 GPU 加速计算能力。
- 应用广泛：CUDA 不仅适用于图形密集型应用程序，还广泛应用于数据分析、科学计算、机器学习、深度学习等领域。如果您从事这些领域的工作，CUDA 可能会改变您的工作方式。
- 社区和资源：Nvidia 为 CUDA 开发人员提供全面的支持，包括详尽的文档、教程以及充满活力的用户和专家社区，让解决问题和学习最佳实践更加容易。

推荐直接从 Nvidia 官方软件源安装最新 CUDA 版本，以下是主要原因：

- 获取最新功能：Nvidia 会持续更新 CUDA 版本，以添加新功能、改进功能和修复错误。安装最新版本可以充分享受这些改进带来的好处。
- 兼容性：较新的 CUDA 版本能够支持最新的 GPU。如果您使用最新的 Nvidia GPU，可能会要求最新的 CUDA 版本。
- 便捷更新：通过导入 Nvidia 官方 APT 软件源和 GPG 密钥，可以轻松使用 APT 软件包管理器获取未来的更新，可以避免手动下载和安装 CUDA 更新。

ref:

- [CUDA Toolkit Documentation](https://docs.nvidia.com/cuda/)

# Install

## cmd

*（下面的安装过程自测有些不支持，ubuntu24.04 还是使用系统软件进行的安装。）*

```bash
# cuda
# https://developer.download.nvidia.cn/compute/cuda/repos/ubuntu2404/x86_64/

# 安装 NVIDIA Container Toolkit
# NVIDIA Container Toolkit 软件仓库在 NVIDIA GitHub 上，所以安装过程依赖于网络，如果失败，请多次尝试。

curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg

curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
  sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
  sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

sudo apt update

sudo apt install -y nvidia-container-toolkit

################################################################################
# step1. 清除 Ubuntu 中已有的 CUDA 和 Nvidia
################################################################################

# 1.1. 卸载 CUDA Toolkit
sudo apt --purge remove "*cuda*" "*cublas*" "*cufft*" "*cufile*" "*curand*" "*cusolver*" "*cusparse*" "*gds-tools*" "*npp*" "*nvjpeg*" "nsight*" "*nvvm*"

# 1.2. 卸载 NVIDIA 驱动Drivers
sudo apt-get --purge remove "*nvidia*" "libxnvctrl*"

# 1.3. 卸载后的清理
sudo apt-get autoremove

# 1.4. 重启
sudo reboot

################################################################################
# step2. 在 Ubuntu 中安装 CUDA
################################################################################

# 2.1. 安装必要的软件包
sudo apt install dirmngr ca-certificates software-properties-common apt-transport-https dkms curl -y

# 2.2. 导入 Nvidia 软件源 GPG 密钥 (Ubuntu 24.04 LTS)
curl -fSsL https://developer.download.nvidia.cn/compute/cuda/repos/ubuntu2404/x86_64/3bf863cc.pub | sudo gpg --dearmor | sudo tee /usr/share/keyrings/nvidia-drivers.gpg > /dev/null 2>&1

# 2.3. 将 Nvidia 软件源添加到 Ubuntu 系统 (Ubuntu 24.04 LTS)
echo 'deb [signed-by=/usr/share/keyrings/nvidia-drivers.gpg] https://developer.download.nvidia.cn/compute/cuda/repos/ubuntu2404/x86_64/ /' | sudo tee /etc/apt/sources.list.d/nvidia-drivers.list

# 2.4. 刷新软件包列表
sudo apt update

# 2.5. 安装 CUDA 和 Nvidia 驱动程序
apt search cuda-drivers

sudo apt install nvidia-driver-555 cuda-drivers-555 cuda

# 2.6. 重启
sudo reboot

################################################################################
# step3. 测试
################################################################################

nvidia-smi
```

## ref

- [Fedora 39/38/37 Linux系统安装NVIDIA驱动程序详细教程](https://www.ecscoupon.com/2342.html)
- [如何在 Ubuntu 中安装 CUDA，详细步骤](https://www.sysgeek.cn/ubuntu-cuda/#google_vignette)
- [Ubuntu完整卸载CUDA和nvidia驱动](https://www.openpilot.cc/archives/4405)
- [Ubuntu24.04安装CUDA和NVIDIA显卡驱动](https://www.openpilot.cc/archives/4411)
- [Ubuntu 24.04 LTS 安装 Docker 和 NVIDIA Container Toolkit](https://cloud.tencent.com/developer/article/2415295)

