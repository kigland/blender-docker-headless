# Blender Docker Headless

[![actions](https://kigland.com/haiyimei/blender-docker-headless/actions/workflows/docker-build-push.yml/badge.svg)](https://github.com/kigland/blender-docker-headless/actions/workflows/docker-build-push.yml)
[![license](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)

:rocket: This repository provides a bunch of Docker images for Blender optimized for **<ins>headless</ins>** rendering. It fully supports both **<ins>EEVEE</ins>** and **<ins>CYCLES</ins>** render engines with GPU acceleration through **EGL**.

## Usage

```bash
docker run -it --rm --gpus all -v $(pwd):/workspace -w /workspace ghcr.io/kigland/blender:blender-3.6-cuda11.7.1-ubuntu20.04
```

## Build

```bash
docker build -t kigland/blender:blender-3.6-cuda11.7.1-ubuntu20.04 . \
    --build-arg BLENDER_VERSION=3.6.18 \
    --build-arg UBUNTU_CUDA_VERSION=11.7.1-cudnn8-devel-ubuntu20.04
```

## Test

```bash
docker run --rm --gpus all -v $(pwd):/workspace -w /workspace kigland/blender:blender-3.6-cuda11.7.1-ubuntu20.04 blender -b --python tests/render_eevee.py
```

```bash
docker run --rm --gpus all -v $(pwd):/workspace -w /workspace kigland/blender:blender-3.6-cuda11.7.1-ubuntu20.04 blender -b --python tests/render_cycles.py
```

## Key

- [EGL support](https://archive.blender.org/developer/D6585) and [libglvnd](https://github.com/NVIDIA/libglvnd).
- Enable the `graphics` capability for environment variable `NVIDIA_DRIVER_CAPABILITIES`, [doc](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/docker-specialized.html#driver-capabilities).
ender-docker/tree/master
