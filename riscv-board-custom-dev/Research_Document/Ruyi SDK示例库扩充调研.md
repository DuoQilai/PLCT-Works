# Ruyi SDK示例库扩充调研

本文档旨在明确第三方成熟项目向Ruyi SDK示例库的迁移标准、适配流程及资源选型，为示例库扩充提供统一规范，确保迁移后的示例符合Ruyi SDK构建体系、可在Ruyi虚拟环境（venv）中正常编译运行，覆盖嵌入式RISC-V、图形/多媒体、外设交互等核心场景。



# 1 前提条件

## 1.1适用范围

本指南适用于Ruyi SDK开发者、生态贡献者，用于迁移开源组织/厂商提供的成熟项目至Ruyi SDK示例库，涵盖项目选型、构建适配、文档编写、验证验收全流程。

## 1.2术语定义

|术语|定义|
|---|---|
|Ruyi venv|Ruyi SDK提供的虚拟开发环境，用于隔离工具链、依赖包，确保构建一致性|
|工具链适配|将第三方项目的构建脚本（Makefile/CMake）改造为适配Ruyi SDK RISC-V工具链（rv32/rv64）的格式|
|示例标准化|迁移后的示例需符合Ruyi SDK示例库目录结构、README模板、启动脚本规范|
## 1.3环境配置

- 已安装Ruyi SDK最新稳定版（建议v2.0+），并配置环境变量

- 已激活Ruyi虚拟环境，确认工具链可用性（执行`riscv64-unknown-linux-gnu-gcc -v`验证）

- 具备基础构建工具（CMake 3.20+、Make、Git）

- 针对图形/多媒体示例，需提前安装gl4es、SDL2等依赖库（通过Ruyi venv安装：`ruyi install gl4es`）

# 2 RISC-V生态原生资源

本节按场景分类梳理可迁移资源，明确每类资源的选型依据、适配步骤及Ruyi SDK兼容性要点，所有资源均来自成熟开源组织/厂商，具备工业级稳定性。

## 2.1 CORE-V MCU SDK Examples

### 资源信息

- 来源：OpenHW Group（RISC-V开源生态核心组织）

- 仓库地址：[openhwgroup/core-v-mcu-sdk-examples](https://github.com/openhwgroup/core-v-mcu-sdk-examples)

- 核心场景：RISC-V MCU外设交互、FreeRTOS应用、CLI工具开发

- 兼容性：适配RV32/RV64架构，支持IMAC/V扩展，可直接对接Ruyi SDK工具链

### 迁移步骤

1. 资源获取：克隆仓库至本地，选取最小功能示例（如UART输出、GPIO控制），排除依赖CORE-V专属SDK的模块

2. 构建适配：
        

    - Makefile改造：替换工具链前缀为Ruyi SDK路径，示例：`CROSS_COMPILE=$(RUYI_VENV)/bin/riscv64-unknown-linux-gnu-`

    - CMake改造：添加Ruyi工具链文件，指定架构参数 `-march=rv64gcv -mabi=lp64d`

3. 环境集成：编写`activate.sh`脚本，自动激活Ruyi venv并配置环境变量

4. 验证：在Ruyi venv中执行`make`编译，通过QEMU或RISC-V开发板运行示例，确认功能正常

## 2.2 core-v-mcu 快速启动示例

资源地址：[core-v-mcu/emulation/quickstart](https://github.com/openhwgroup/core-v-mcu/blob/master/emulation/quickstart/README.md)，可作为Ruyi SDK最小Console示例模板，迁移重点为简化构建流程，保留启动代码核心逻辑，适配Ruyi venv的一键构建。

# 2  图形/多媒体资源（扩展Ruyi GLES/SDL能力）

## 2.1 SFML（Simple and Fast Multimedia Library）

### 资源信息

- 类型：跨平台图形/多媒体库

- 核心能力：窗口管理、2D渲染、输入响应、音频播放

- 适配场景：Ruyi SDK图形示例演示、轻量级多媒体应用开发

### 迁移要点

- 选型：选取基础示例（如空白窗口创建、彩色矩形渲染），避免依赖复杂音频组件

- 依赖适配：通过Ruyi venv安装gl4es（OpenGL ES兼容层），配置`LIBGL_ALWAYS_SOFTWARE=1`确保无硬件GPU也可运行

- 构建配置：在CMake中指定SFML库路径（Ruyi venv安装路径），链接gl4es库解决渲染兼容性问题

## 2.2 Allegro 游戏开发库

资源地址：[Allegro 官方文档](https://en.wikipedia.org/wiki/Allegro_(software_library))，迁移重点为其2D绘图基础示例，改造CMake构建脚本适配Ruyi RISC-V工具链，简化依赖（关闭音频、网络模块），聚焦图形渲染核心功能，作为Ruyi SDK图形示例的补充。

# 4  嵌入式外设/网络资源

## 4.1 Silicon Labs 外设示例

### 资源信息

- 仓库地址：[SiliconLabs/peripheral_examples_simplicity_sdk](https://github.com/SiliconLabs/peripheral_examples_simplicity_sdk)

- 核心价值：提供标准化外设操作（GPIO、UART、I2C）的目录结构与文档模板，可借鉴用于Ruyi SDK外设示例的规范化编写

### 迁移思路

1. 结构借鉴：采用“示例名称-功能描述-硬件适配-构建步骤-运行说明”的文档结构

2. 代码适配：将原MCU外设代码改写为RISC-V通用接口，基于libgpiod实现GPIO操作，替换原厂商专属驱动

3. 文档标准化：按Ruyi官方README模板补充依赖列表、Ruyi venv激活命令、故障排查要点

## 4.2 WiSeConnect SDK 网络示例

资源地址：[WiSeConnect SDK 示例文档](https://docs.silabs.com/wiseconnect/3.5.1/wiseconnect-examples/)，迁移最小网络示例（如DHCP获取IP、TCP客户端通信），适配Ruyi SDK的网络依赖库，改造为RISC-V架构可运行的轻量级网络示例。

# 5  扩展音视频能力

推荐资源：[音视频开源示例集合](https://github.com/0voice/awesome_audio_video_learning)，选取OpenGL基础渲染、YUV图像显示等示例，迁移重点为适配Ruyi SDK的SDL2库与RISC-V工具链，简化编码模块，保留核心渲染流程，作为Ruyi SDK高级示例。

# 6 附录：参考资源清单

| 资源名称                    | 类型         | 参考链接                                                              |
| ----------------------- | ---------- | ----------------------------------------------------------------- |
| CORE-V MCU SDK Examples | RISC-V原生示例 | https://github.com/openhwgroup/core-v-mcu-sdk-examples            |
| SFML 官方文档               | 图形/多媒体库    | https://en.wikipedia.org/wiki/Simple_and_Fast_Multimedia_Library  |
| Silicon Labs 外设示例       | 嵌入式外设模板    | https://github.com/SiliconLabs/peripheral_examples_simplicity_sdk |
| 音视频开源示例集合               | 高级示例基础     | https://github.com/0voice/awesome_audio_video_learning            |