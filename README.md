# DFS_QtApplicationCompileEnvironment
Compile Environment for Qt Applications in Linux

Tested and built for RHEL 8.x

```
subscription-manager repos --enable=codeready-builder-for-rhel-8-x86_64-rpms
yum install podman -y
podman build -f DockerFile -t qt-build-env:latest
podman run -it qt-build-env:latest
```