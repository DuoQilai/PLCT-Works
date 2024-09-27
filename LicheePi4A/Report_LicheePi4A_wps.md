#  在 LicheePi4A 上运行 WPS Linux

## 1  安装 Box64

编译

```shell
git clone https://github.com/ptitSeb/box64.git
cd box64
mkdir build
cd build
cmake .. -D RV64=1 -D CMAKE_BUILD_TYPE=RelWithDebInfo
sudo make install -j$(nproc)
```

## 2 下载并解包 WPS Linux

WPS 官方提供了两个版本可供下载：

1. 英文版：[https://www.wps.com/office/linux/](https://www.wps.com/office/linux/)
2. 中文版：[https://linux.wps.cn/](https://linux.wps.cn/)

请任选其一并下载 Deb 包。

这里以英文版为例，下载完成后，使用 `dpkg-deb` 命令完成解包：

```shell
mkdir wps
cd wps
dpkg-deb --extract ../wps-office_11.1.0.11723.XA_amd64.deb .
```

## 3 运行 WPS Linux

进入 WPS Linux 的解包目录，然后 cd 到二进制所在的目录：

```shell
cd opt/kingsoft/wps-office/office6/
```

至此已完成所有的准备工作，使用如下命令即可以运行 WPS Linux：

```shell
# 运行 WPS Word
box64 ./wps
# 运行 WPS Excel
box64 ./et
# 运行 WPS PowerPoint
box64 ./wpp
```





