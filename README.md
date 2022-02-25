# DFS_QtApplicationCompileEnvironment
Compile Environment for Qt Applications in Linux

Capable of building for:
 - Linux x86_64
 - Windows x86_64

Tested and built to run under RHEL 8.x

```
subscription-manager repos --enable=codeready-builder-for-rhel-8-x86_64-rpms
yum install podman -y
git clone https://github.com/DFSupply/DFS_QtApplicationCompileEnvironment.git
cd DFS_QtApplicationCompileEnvironment
podman build -f DockerFile -t qt-build-env:latest
podman run -it qt-build-env:latest
```