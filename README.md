# DFS_QtApplicationCompileEnvironment
Linux: [![Build Status](https://dev.azure.com/dfsupplyinc/DFS_QtApplicationCompileEnvironment/_apis/build/status/DFSupply.DFS_QtApplicationCompileEnvironment?branchName=main&jobName=Build%20Linux%20Container)](https://dev.azure.com/dfsupplyinc/DFS_QtApplicationCompileEnvironment/_build/latest?definitionId=1&branchName=main)  
Windows: [![Build Status](https://dev.azure.com/dfsupplyinc/DFS_QtApplicationCompileEnvironment/_apis/build/status/DFSupply.DFS_QtApplicationCompileEnvironment?branchName=main&jobName=Build%20Windows%20Container)](https://dev.azure.com/dfsupplyinc/DFS_QtApplicationCompileEnvironment/_build/latest?definitionId=1&branchName=main)

## Compile Environment(s) for Qt Applications

Capable of building for:
 - Linux x86_64
 - Windows x86_64

Tested and built to run under RHEL 9.x + Windows Server 2022

### Linux Build Environment:  
RHEL 9.x  (8.x for builds tagged 0.1.6 and earlier in ACR)

***Licensing restrictions require to be running on RHEL 8.x or 9.x with an attached subscription***

- Option A: Pull from our Azure Container Registry (tested/stable)
 ```
 podman pull dfsbuildcontainer.azurecr.io/qt-build-env-linux:latest
 podman run -rm -it dfsbuildcontainer.azurecr.io/qt-build-env-linux:latest
 ```
- Option B: Build your own
 ```
 podman build -f DockerFile-linux https://github.com/DFSupply/DFS_QtApplicationCompileEnvironment.git -t qt-build-env:latest
 podman run -rm -it qt-build-env:latest
 ```

To compile for RHEL 9.x (8.x for builds 0.1.6 and earlier in ACR):
----inside of container----
```
cd %your_source_directory%
qmake
make -j$(nproc)
```

### Windows Build Environment:  
Windows Server 2022 LTSC  
***Licensing restrictions require to be running on Windows Server 2022***

- Option A: Pull from our Azure Container Registry (tested/stable)
 ```
 docker pull dfsbuildcontainer.azurecr.io/qt-build-env-windows:latest
 docker run -rm -it dfsbuildcontainer.azurecr.io/qt-build-env-windows:latest
 ```
- Option B: Build your own
 ```
 docker build -f DockerFile-linux https://github.com/DFSupply/DFS_QtApplicationCompileEnvironment.git -t qt-build-env:latest
 docker run -rm -it qt-build-env:latest
 ```

To compile for Windows x64:
----inside of container----
```
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
- Ensure you've increased the container storage size (if on windows) as the 20GB initial max is not enough. Personally recommend 500GB for this image
- Can also use ```nmake``` instead of ```jom``` to build on windows (if preferred)