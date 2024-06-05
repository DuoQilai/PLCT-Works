# k230/k510/duosdk列表
## k230sdk结构简介

| 一级目录    | 二级目录               | 说明             |
| ------- | ------------------ | -------------- |
| configs | NA                 | 资源配置 (内存分配规划)  |
| output  | NA                 | SDK编译产物        |
| src     | big                | 大核RTSmart代码    |
| src     | common             | 大小核公共代码        |
| src     | little             | 小核Linux代码      |
| tools   | docker             | dockerfile     |
| tools   | doxygen            | doxygen脚本和配置文件 |
| tools   | kconfig            |                |
| tools   | gen_image.sh       | 生成可烧写镜像的脚本     |
| tools   | gen_image_cfg      | 镜像分区配置文件       |
| tools   | tuning-tool-client | PC端图像调试工具      |

各个目录用途描述如下：

- `configs`： 存放SDK的板级默认配置，主要包含如下信息：参考板类型，toolchain路径，
    
    内存布局规划，存储规划配置等
    
- `src`：源代码目录，分为 大核代码（`big`），公共组件（`common`），小核代码（`little`）三个目录。
    
    大核代码包含：`rt-smart`操作系统代码，`mpp`代码，`unittest`代码
    
    公共组件包含：`cdk`代码和`opensbi`代码
    
    小核代码包含：`linux`内核代码，`buildroot`代码，`uboot`代码
    
- `tools`：存放各种工具，脚本等。例如`kconfig`，`doxygen`，`dockerfile`等
    
- `board`：环境变量、镜像配置文件、文件系统等




## k510sdk结构简介

| **文件**          | **内容描述**                                                                                                                                                                                 |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| board           | 文件夹，其是K510各种配置文件和脚本，如生成镜像的配置文件（genimage-xxx.cfg），buildroot的post-image脚本，U-Boot默认环境变量等。                                                                                                   |
| Config.in       | 其中内容指示了需要buildroot编译的package。                                                                                                                                                            |
| configs         | 文件夹，其中是开发板默认编译配置文件。当前保存有K510 CRB-V0.1、K510 CRB-V1.2和K510 EVB三块板的默认编译配置文件:  <br>- `k510_crb_lp3_v1_2_defconfig`  <br>- `k510_crb_lp3_v0_1_defconfig`  <br>- `k510_evb_lp3_v1_1_defconfig` |
| external.desc   | buildroot的external机制配置文件。                                                                                                                                                                |
| external.mk     |                                                                                                                                                                                          |
| Makefile        | k510 SDK的主Makefile。                                                                                                                                                                      |
| package         | 文件夹，其中主要是K510 应用程序，Config.in文件中的内容将决定该目录下哪些应用程序被编译。                                                                                                                                      |
| patches         | 文件夹，其中是buildroot的补丁文件，Makefile在解压源码的时候会将此目录下的补丁文件打到相应源码目录。                                                                                                                               |
| pkg-download    | 文件夹，其中是dl文件夹的压缩包。                                                                                                                                                                        |
| README.md       | sdk 相关说明。                                                                                                                                                                                |
| release_note.md |                                                                                                                                                                                          |
| toolchain       | 文件夹，其中是交叉编译工具链。                                                                                                                                                                          |
| dl              | 文件夹，是pkg-download中的dl 解压缩包，如果有添加其它包也会下载到该目录下。                                                                                                                                            |
## duosdk结构简介

| **文件**            | **内容描述**                      |
| ----------------- | ----------------------------- |
| build             | 编译目录，存放编译脚本以及各board差异化配置      |
| build.sh          | Milk-V Duo 一键编译脚本             |
| buildroot-2021.05 | buildroot 开源工具                |
| freertos          | freertos 系统                   |
| fsbl              | fsbl启动固件，prebuilt 形式存在        |
| install           | 执行一次完整编译后，临时存放各 image 路径      |
| isp_tuning        | 图像效果调试参数存放路径                  |
| linux_5.10        | 开源 linux 内核                   |
| middleware        | 自研多媒体框架，包含 so 与 ko            |
| device            | 存放 Milk-V Duo 相关配置及脚本文件的目录    |
| opensbi           | 开源 opensbi 库                  |
| out               | Milk-V Duo 最终生成的 SD 卡烧录镜像所在目录 |
| ramdisk           | 存放最小文件系统的 prebuilt 目录         |
| u-boot-2021.10    | 开源 uboot 代码                   |
## 树形结构
### k230
[PLCT-Works/k230d/k230tree.txt at main · DuoQilai/PLCT-Works (github.com)](https://github.com/DuoQilai/PLCT-Works/blob/main/k230d/k230tree.txt)
### k510
[PLCT-Works/k230d/k510tree.txt at main · DuoQilai/PLCT-Works (github.com)](https://github.com/DuoQilai/PLCT-Works/blob/main/k230d/k510tree.txt)
### duo
[PLCT-Works/k230d/duotree.txt at main · DuoQilai/PLCT-Works (github.com)](https://github.com/DuoQilai/PLCT-Works/blob/main/k230d/duotree.txt)
## 参考文档：
- [kendryte/k230_sdk: Kendryte K230 SDK (github.com)](https://github.com/kendryte/k230_sdk)
- [k510_docs/zh/K510_SDK_Build_and_Burn_Guide.md at dev · kendryte/k510_docs (github.com)](https://github.com/kendryte/k510_docs/blob/dev/zh/K510_SDK_Build_and_Burn_Guide.md)
- [duo-buildroot-sdk/README-zh.md at develop · milkv-duo/duo-buildroot-sdk (github.com)](https://github.com/milkv-duo/duo-buildroot-sdk/blob/develop/README-zh.md)