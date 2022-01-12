# Experiment about running i386 container on 64-bit OS

## Introduction

This repository is about the notes to explore running the i386 docker container on a 64-bit host OS (Ubuntu WSL2).

## i386

First, I created a dummy i386 image by `buildx`.

```bash
docker buildx ls  
docker buildx create --name mybuilder
docker buildx use mybuilder
docker buildx build --platform linux/386 -t kuangda/i386:latest --push .
```

But running the image shows `x86_64`. 

```bash
docker run --rm --platform linux/386 kuangda/i386 uname -m 
```

## Other architectures

Then I tried two other images. Interestingly, the kernels of them are actually 32-bit.


```bash
docker run -it --rm ghcr.io/castisdev/centos5-i386:1.0
# i686
```

```bash
docker run --rm --platform arm32/v6 arm32v6/bash uname -m   
# armv7l
```

## Relative readings

- Leverage multi-CPU architecture support [(Link)](https://docs.docker.com/desktop/multi-arch/#:~:text=When%20running%20an%20image%20with,provide%20a%20variety%20of%20architectures.)

