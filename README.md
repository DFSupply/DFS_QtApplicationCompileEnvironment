# DFS_QtApplicationCompileEnvironment
[![Build Status](https://dev.azure.com/dfsupplyinc/Azure%20Pipelines%20GitHub/_apis/build/status/DFSupply.DFS_QtApplicationCompileEnvironment?branchName=main)](https://dev.azure.com/dfsupplyinc/Azure%20Pipelines%20GitHub/_build/latest?definitionId=1&branchName=main)

Compile Environment(s) for Qt Applications

Capable of building for:
 - Linux x86_64
 - Windows x86_64

Tested and built to run under RHEL 8.x + WIN10

Linux Build Environment:
***Licensing restrictions require to be running on RHEL 8.x with an attached subscription***
```
subscription-manager repos --enable=codeready-builder-for-rhel-8-x86_64-rpms
yum install podman -y
podman build -f DockerFile-linux https://github.com/DFSupply/DFS_QtApplicationCompileEnvironment.git -t qt-build-env:latest
podman run -it qt-build-env:latest

----inside of container----
cd %your source directory%
qmake
make -j$(nproc)
```

To cross-compile in the linux environment (if you **do not** require QtWebEngine):
```
export PATH=/opt/mxe/usr/bin:$PATH
cd %your source directory%
/opt/mxe/usr/bin/x86_64-w64-mingw32.static-qmake-qt5
make -j$(nproc)
```

Windows Build Environment (assume docker EE installed):
***Licensing restrictions require to be running on Windows Server 2022***
```
docker build -f DockerFile-windows https://github.com/DFSupply/DFS_QtApplicationCompileEnvironment.git -t qt-build-env:latest
docker run -it qt-build-env:latest

----inside of container----
cd %your source directory%
qmake
jom
```