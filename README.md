# DFS_QtApplicationCompileEnvironment
Compile Environment for Qt Applications in Linux

Tested and built for RHEL 8.x

```
yum install -y podman
podman build -f DockerFile -t qt-build-env:latest
podman run -it qt-build-env:latest /bin/bash
```