# Ruyi SDK示例库扩充调研

本文档在原有RISC-V原生、图形/多媒体、嵌入式外设/网络等方向基础上，新增物联网、轻量化AI/ML、嵌入式文件系统、安全加密、RTOS进阶、总线通信进阶等扩充方向，明确各方向可迁移的成熟开源项目、适配流程及验证标准，进一步丰富Ruyi SDK示例库的场景覆盖度，确保新增示例符合Ruyi venv构建体系，可在RISC-V架构下稳定编译运行。

# 1 扩充方向选型原则

1. 资源成熟度：优先选择开源社区维护活跃、工业级验证的项目，避免小众/无人维护的资源；

2. 架构兼容性：原生支持或可低成本适配RV32/RV64架构，兼容RISC-V标准扩展（如IMAC/V/Crypto等）；

3. 轻量易迁移：选取最小功能集示例，避免过度依赖专属硬件/闭源组件，降低适配复杂度；

4. 场景匹配度：覆盖物联网、边缘计算、嵌入式安全等Ruyi SDK核心目标场景；

5. 构建适配性：可通过改造Makefile/CMake适配Ruyi SDK工具链，兼容Ruyi venv依赖管理体系。



# 2 物联网(IoT)轻量化示例

## 2.1 lwIP（轻量级IP协议栈）

#### 资源信息

- 来源：瑞典计算机科学研究院（SICS）、开源社区长期维护

- 仓库地址：[savannah.nongnu.org/projects/lwip/](https://savannah.nongnu.org/projects/lwip/)

- 核心场景：RISC-V嵌入式设备低功耗网络通信、IPv4/IPv6轻量部署、TCP/UDP基础通信

- 兼容性：原生支持嵌入式RISC-V架构，无硬件独占依赖，可适配Ruyi SDK RV32/RV64工具链

### 迁移适配要点

1. 资源裁剪：选取`lwip/contrib/examples`中最小示例（如echo server/client），移除POSIX系统依赖，保留裸机/RTOS适配层；

2. 构建改造：

    - Makefile：替换工具链前缀为`$(RUYI_VENV)/bin/riscv64-unknown-linux-gnu-`，添加`-DLWIP_NO_SYS=0`（启用系统适配层）；

    - CMake：引入Ruyi工具链文件，指定编译参数`-march=rv64gc -mabi=lp64d`，链接Ruyi venv中的`pthread`库；

3. 环境集成：编写`run_lwip.sh`脚本，自动激活Ruyi venv，配置网络模拟环境（QEMU用户态网络）；

4. 依赖适配：通过`ruyi install lwip`安装Ruyi venv适配版lwip依赖，解决头文件路径问题。

### 验证方式

在Ruyi venv中执行`make`编译，通过QEMU RISC-V虚拟机启动echo server，宿主机通过网络端口测试通信连通性。



## 2.2 Paho MQTT Embedded-C

### 资源信息

- 来源：Eclipse基金会

- 仓库地址：[eclipse/paho.mqtt.embedded-c](https://github.com/eclipse/paho.mqtt.embedded-c)

- 核心场景：RISC-V嵌入式设备MQTT协议通信、物联网设备端消息上报/订阅

- 兼容性：纯C实现，支持RV32/RV64，可对接lwip网络底层

### 迁移适配要点

1. 资源选取：选择`samples/MQTTClient-C`基础示例（如MQTT连接/发布/订阅），排除依赖OSAL（操作系统适配层）的复杂模块；

2. 底层适配：将示例网络底层替换为lwip（已迁移的轻量IP协议栈），适配Ruyi SDK的网络接口；

3. 构建配置：在CMake中指定Paho库路径（Ruyi venv安装路径），添加编译宏`-DPAHO_WITH_SSL=0`（暂关闭SSL，降低适配复杂度）；

4. 文档补充：按Ruyi示例规范，新增MQTT服务器搭建指引、Ruyi venv环境变量配置说明。



# 3  AI/ML轻量化推理示例

## 3.1 TinyML Examples

### 资源信息

- 来源：TinyML社区、Google TensorFlow Lite for Microcontrollers

- 仓库地址：[tensorflow/tflite-micro/examples](https://github.com/tensorflow/tflite-micro/tree/main/examples)

- 核心场景：RISC-V嵌入式设备端轻量化机器学习推理（如手势识别、环境传感器数据分类）

- 兼容性：支持RISC-V 32/64位架构，可通过CMSIS-NN优化RISC-V指令集

### 迁移适配要点

1. 示例裁剪：选取最小示例（如`hello_world`、`micro_speech`精简版），移除依赖ARM CMSIS的模块，替换为RISC-V通用数学库；

2. 工具链适配：

    - 在Makefile中添加Ruyi SDK工具链路径，指定`-march=rv64gcv -mabi=lp64d`（启用向量扩展加速推理）；

    - 链接Ruyi venv中的`libriscv_nn`库（RISC-V神经网络加速库）；

3. 依赖安装：通过`ruyi install tflite-micro`安装适配RISC-V的TensorFlow Lite Micro库；

4. 验证优化：在QEMU RISC-V虚拟机中运行推理示例，通过打印输出确认推理结果，优化编译参数减少二进制体积。



## 3.2 NanoEdge AI Studio示例

### 资源信息

- 来源：STMicroelectronics（适配RISC-V版本）

- 核心场景：嵌入式设备异常检测、传感器数据分析

- 兼容性：提供纯C代码生成能力，可直接适配RISC-V架构

### 迁移适配要点

1. 代码生成：通过NanoEdge AI Studio生成无OS依赖的RISC-V适配代码；

2. 构建集成：将生成的代码整合到Ruyi SDK示例目录，编写适配Ruyi venv的Makefile；

3. 硬件验证：在RISC-V开发板（如昉·星光2）上接入传感器，验证AI推理功能。

# 4  嵌入式文件系统示例

## 4.1 LittleFS

### 资源信息

- 来源：ARM开源团队、开源社区

- 仓库地址：[littlefs-project/littlefs](https://github.com/littlefs-project/littlefs)

- 核心场景：RISC-V嵌入式设备低功耗、小闪存文件系统操作（如SPI Flash文件读写）

- 兼容性：无架构依赖，纯C实现，可直接适配RISC-V

### 迁移适配要点

1. 示例选取：选取`examples/posix`最小示例，替换POSIX接口为Ruyi SDK提供的嵌入式存储接口；

2. 构建改造：在CMake中指定LittleFS源码路径，添加编译宏`-DLFS_NO_MALLOC=1`（适配嵌入式无堆场景）；

3. 硬件适配：对接RISC-V开发板的SPI Flash驱动（基于libgpiod实现），编写存储设备初始化脚本；

4. 验证：在Ruyi venv中编译，通过QEMU模拟SPI Flash，验证文件创建、读写、删除功能。

## 4.2 FatFs

### 资源信息

- 来源：[elm-chan.org](http://elm-chan.org)（开源嵌入式文件系统）

- 核心场景：RISC-V设备FAT32/EXFAT文件系统操作，兼容SD卡/U盘等存储设备

- 兼容性：跨架构纯C实现，支持RV32/RV64

### 迁移适配要点

1. 代码适配：将FatFs的底层磁盘I/O接口替换为Ruyi SDK的存储驱动（如SD卡驱动）；

2. 构建配置：Makefile中添加Ruyi工具链前缀，链接`libsd`库（Ruyi venv安装）；

3. 文档标准化：补充Ruyi venv下SD卡挂载命令、FatFs格式化流程说明。



# 5 RISC-V安全加密示例

## mbed TLS（ARM mbed Crypto）

### 资源信息

- 来源：ARM开源、Eclipse基金会维护

- 仓库地址：[ARMmbed/mbedtls](https://github.com/ARMmbed/mbedtls)

- 核心场景：RISC-V设备轻量级TLS/SSL通信、对称/非对称加密（AES/RSA/ECC）

- 兼容性：支持RISC-V架构，可适配RISC-V Crypto扩展

### 迁移适配要点

1. 配置裁剪：通过`config.h`关闭非必要加密算法，保留基础AES/RSA，减少代码体积；

2. 工具链适配：在CMake中指定Ruyi SDK工具链，添加`-march=rv64gc+crypto`（启用RISC-V Crypto扩展）；

3. 依赖适配：通过`ruyi install mbedtls`安装Ruyi venv适配版库，解决链接依赖；

4. 示例验证：编译TLS客户端/服务器示例，在QEMU中验证RISC-V设备与宿主机的加密通信。



# 6  RTOS进阶应用示例

## Zephyr RTOS RISC-V示例

### 资源信息

- 来源：Linux基金会、Zephyr社区

- 仓库地址：[zephyrproject-rtos/zephyr/samples](https://github.com/zephyrproject-rtos/zephyr/tree/main/samples)

- 核心场景：RISC-V设备多线程调度、中断管理、设备树适配

- 兼容性：原生支持RISC-V 32/64位，可对接Ruyi SDK工具链

### 迁移适配要点

1. 示例裁剪：选取`basic/blinky`、`basic/threads`最小示例，移除Zephyr专属SDK依赖；

2. 构建适配：

    - 替换Zephyr工具链为Ruyi SDK路径，修改`ZEPHYR_TOOLCHAIN_VARIANT=ruyi`；

    - 适配Ruyi venv的设备树文件，指定RISC-V开发板（如昉·星光2）的硬件配置；

3. 环境集成：编写`zephyr_activate.sh`，自动激活Ruyi venv并配置Zephyr构建环境。
