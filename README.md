# DFS_QtApplicationCompileEnvironment
Linux: [![Build Status](https://dev.azure.com/dfsupplyinc/DFS_QtApplicationCompileEnvironment/_apis/build/status/DFSupply.DFS_QtApplicationCompileEnvironment?branchName=main&jobName=Build%20Linux%20Container)](https://dev.azure.com/dfsupplyinc/DFS_QtApplicationCompileEnvironment/_build/latest?definitionId=1&branchName=main)  
Windows: [![Build Status](https://dev.azure.com/dfsupplyinc/DFS_QtApplicationCompileEnvironment/_apis/build/status/DFSupply.DFS_QtApplicationCompileEnvironment?branchName=main&jobName=Build%20Windows%20Container)](https://dev.azure.com/dfsupplyinc/DFS_QtApplicationCompileEnvironment/_build/latest?definitionId=1&branchName=main)

## Compile Environment(s) for Qt Applications

Capable of building for:
 - Linux x86_64
 - Windows x86_64

Tested and built to run under RHEL 8.x + Windows Server 2022

### Linux Build Environment:  
RHEL 8.x  
***Licensing restrictions require to be running on RHEL 8.x with an attached subscription***
```
subscription-manager repos --enable=codeready-builder-for-rhel-8-x86_64-rpms
podman build -f DockerFile-linux https://github.com/DFSupply/DFS_QtApplicationCompileEnvironment.git -t qt-build-env:latest
podman run -rm -it qt-build-env:latest

----inside of container----
cd %your_source_directory%
qmake
make -j$(nproc)
```

To cross-compile in the linux environment (if you **do not** require QtWebEngine):
```
export PATH=/opt/mxe/usr/bin:$PATH
cd %your_source_directory%
/opt/mxe/usr/bin/x86_64-w64-mingw32.static-qmake-qt5
make -j$(nproc)
```

### Windows Build Environment:  
Windows Server 2022 LTSC  
***Licensing restrictions require to be running on Windows Server 2022***
```
docker build -f DockerFile-windows https://github.com/DFSupply/DFS_QtApplicationCompileEnvironment.git -t qt-build-env:latest
docker run -rm -it qt-build-env:latest

----inside of container----
cd %your_source_directory%
c:\vcpkg\installed\x64-windows\tools\qt5\bin\qmake.exe
jom
```

Shared library copy (SAMPLE - your use may vary)
```
c:\vcpkg\installed\x64-windows\tools\qt5\bin\windeployqt.exe %your_binary_directory%
xcopy c:\vcpkg\intalled\x64-windows\bin\*.dll %your_binary_directory%\ /E/H
xcopy c:\vcpkg\intalled\x64-windows\plugins\*.dll %your_binary_directory%\ /E/H
```

#### Important Notes

- Assuming podman (RHEL) or docker EE (Windows Server) are already installed and configured
- Ensure you've increased the container storage size (if on windows) as the 20GB initial max is not enough. Personally recommand 200GB minimum for this image
- Can also use ```nmake``` instead of jom to build on windows (if preferred)