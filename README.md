# Blender (Headless) Docker Container

> [!NOTE]
> **Open Source Notice**  
> This repository is adapted from [HaiyiMei/blender-docker-headless](https://github.com/HaiyiMei/blender-docker-headless), which licensed under Apache 2.0.

[![license](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)

:rocket: This repository provides a bunch of Docker images for Blender optimized for **<ins>headless</ins>** rendering. It fully supports both **<ins>EEVEE</ins>** and **<ins>CYCLES</ins>** render engines with GPU acceleration through **EGL**.

## Usage

```bash
docker run -it --rm --gpus all \
           -v $(pwd):/workspace \
           -w /workspace \
           kigland/blender:4.5.3-cuda12.8.1
```

## Build

We provide both modifed Dockerfile for global [Dockerfile](Dockerfile) and the Mainland China [Dockerfile.China](Dockerfile.China) version seperately.

```bash
docker build -t kigland/blender:4.5.3-cuda12.8.1 . \
    --build-arg BLENDER_VERSION=4.5.3 \
    --build-arg UBUNTU_CUDA_VERSION=12.8.1-cudnn-devel-ubuntu24.04
```

## Test

```bash
docker run --rm --gpus all \
           -v $(pwd):/workspace \
           -w /workspace \
           kigland/blender:4.5.3-cuda12.8.1 blender -b --python tests/render_eevee.py
```

```bash
docker run --rm --gpus all \
           -v $(pwd):/workspace \
           -w /workspace \
           kigland/blender:4.5.3-cuda12.8.1 blender -b --python tests/render_cycles.py
```

## Transparency and Mirrors

We use following mirror sites in different dockerfile versions.

| Mirror Provider | Mirror Site | Original | Original Site | Dockerfile Version |
| :-------------: | :---------: | :------: | :-----------: | :----------------: |
| Tsinghua University | <https://mirrors.tuna.tsinghua.edu.cn/> | Blender | <https://www.blender.org/download> | China |
| Aliyun | <http://mirrors.aliyun.com> | Ubuntu Deb Source | <http://archive.ubuntu.com> | China |
| [oopsunix](https://github.com/oopsunix) | <https://gh.llkk.cc> | GitHub | <https://github.com> | China |
| RWTH Aachen University | <https://ftp.halifax.rwth-aachen.de> | Blender | <https://www.blender.org/download> | Global |

## Key

- [EGL support](https://archive.blender.org/developer/D6585) and [libglvnd](https://github.com/NVIDIA/libglvnd).
- Enable the `graphics` capability for environment variable `NVIDIA_DRIVER_CAPABILITIES`, [doc](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/docker-specialized.html#driver-capabilities).
