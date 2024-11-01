#  在 LicheePi4A 上运行 Celeste Linux

## 1  安装 Box64

编译步骤

```shell
git clone https://github.com/ptitSeb/box64.git
cd box64
mkdir build
cd build
cmake .. -D RV64=1 -D CMAKE_BUILD_TYPE=RelWithDebInfo
sudo make install -j$(nproc)
```

## 2 安装gl4es

编译步骤

```shell
git clone https://github.com/ptitSeb/gl4es
cd gl4es
mkdir build
cd build
cmake .. -D CMAKE_BUILD_TYPE=RelWithDebInfo
make -j4 
```
## 3 下载并解包 Celeste Linux

试玩地址：https://archive.org/details/celeste-v-1.4.0.0-linux

下载7zip版本

## 4 运行 Celeste Linux

进入 Celeste Linux 的解包目录，然后 cd 到二进制所在的目录：

```shell
cd Celeste_(v1.4.0.0)_[Linux]
```

至此已完成所有的准备工作，使用如下命令即可以运行 WPS Linux：

```shell
# 运行 Celeste
box64 ./Celeste.bin.x86_64
# 运行 Celeste加上帧数显示
GALLIUM_HUD=fps box64 ./Celeste.bin.x86_64
# 运行 Celeste终端打印帧数
LIBGL_FPS=1 box64 ./Celeste.bin.x86_64
```

若运行sh脚本，则增加环境变量
```
BOX64_BASH=/path/to/box64/tests/bash
```





