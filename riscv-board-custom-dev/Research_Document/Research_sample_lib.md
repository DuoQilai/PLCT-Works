# RuyiSDK 示例库扩充调研报告

## 一、调研方向介绍

当前 RuyiSDK 示例内容以 工具链验证（Hello World、Coremark） 为主，更偏向内部测试与能力证明，但对普通开发者而言，仍存在以下问题：

- 示例难以回答“我能用 Ruyi 做什么”
- 缺乏贴近真实开发场景的参考路径
- 新用户难以从示例中形成持续使用习惯

因此，本次调研从多个维度对 “示例库如何服务开发者体验” 进行拆分分析，重点关注以下三类内容：

- 基础验证类示例
- 功能/库支持类示例
- 应用实战类示例

目标是为后续 Ruyi 示例库形成长期、可复用、可扩展的内容结构提供依据。

调研文档：
- [RuyiSDK开源项目移植与验证](https://github.com/DuoQilai/PLCT-Works/blob/main/riscv-board-custom-dev/Research_Document/RuyiSDK%E7%A4%BA%E4%BE%8B%E5%BA%93%E6%89%A9%E5%85%85-%E5%BC%80%E6%BA%90%E9%A1%B9%E7%9B%AE%E7%A7%BB%E6%A4%8D%E4%B8%8E%E9%AA%8C%E8%AF%81.md)
- [Ruyi SDK示例库扩充调研](https://github.com/DuoQilai/PLCT-Works/blob/main/riscv-board-custom-dev/Research_Document/Ruyi%20SDK%E7%A4%BA%E4%BE%8B%E5%BA%93%E6%89%A9%E5%85%85%E8%B0%83%E7%A0%94%E8%A1%A5%E5%85%85.md)
- [Ruyi SDK示例库扩充调研](https://github.com/DuoQilai/PLCT-Works/blob/main/riscv-board-custom-dev/Research_Document/Ruyi%20SDK%E7%A4%BA%E4%BE%8B%E5%BA%93%E6%89%A9%E5%85%85%E8%B0%83%E7%A0%94%E8%A1%A5%E5%85%85.md)
- [Ruyi SDK示例库扩充调研](https://github.com/DuoQilai/PLCT-Works/blob/main/riscv-board-custom-dev/Research_Document/Ruyi%20SDK%E7%A4%BA%E4%BE%8B%E5%BA%93%E6%89%A9%E5%85%85%E8%B0%83%E7%A0%94.md)
- [Milk-V Duo TDL-SDK人脸检测迁移RuyiSDK编译教程](https://github.com/DuoQilai/PLCT-Works/blob/main/riscv-board-custom-dev/Research_Document/Milk-V%20Duo%E4%BA%BA%E8%84%B8%E6%A3%80%E6%B5%8B%E8%BF%81%E7%A7%BBRuyiSDK%E7%BC%96%E8%AF%91%E6%95%99%E7%A8%8B.md)
- [Allegro 示例迁移至 RuyiSDK 环境实践指南](https://github.com/DuoQilai/PLCT-Works/blob/main/riscv-board-custom-dev/Research_Document/Allegro%20%E7%A4%BA%E4%BE%8B%E8%BF%81%E7%A7%BB%E8%87%B3%20RuyiSDK%20%E5%AE%9E%E8%B7%B5%E6%8C%87%E5%8D%97.md)
- [RuyiSDK 扩充示例库项目汇总表](https://github.com/jason-hue/plct/blob/main/%E6%9D%82%E9%A1%B9/%E4%B8%80%E3%80%81%20RuyiSDK%20%E6%89%A9%E5%85%85%E7%A4%BA%E4%BE%8B%E5%BA%93%E9%A1%B9%E7%9B%AE%E6%B1%87%E6%80%BB%E8%A1%A8.md)

---

## 二、示例类型调研分析

### 1. 基础验证类示例

以“能否成功安装、编译、运行”为核心，证明 RuyiSDK + 工具链 + 开发板 在技术上的可用性。

#### 内容特征

- Hello World
- Coremark
- 基础编译 / 运行流程

#### 目标受众

- RuyiSDK 项目内部
- 第三方测试机构
- 有经验的开发者（用于快速确认环境）

#### 示例风格

- 步骤清晰、结果明确
- 强调编译参数、架构信息、指令集支持
- 偏技术说明，偏“报告型”
#### 调研示例

| 序号  | 项目名称              | 类别   | 核心价值 / 验证点                  | 源码链接                                                                                           |
| --- | ----------------- | ---- | --------------------------- | ---------------------------------------------------------------------------------------------- |
| 1   | Hello World       | 基础示例 | 验证系统最小运行与基础外设输出             | [GitHub](https://github.com/milkv-duo/duo-examples/tree/main/hello-world)                      |
| 2   | Coremark          | 性能验证 | 验证工具链正确性与 CPU 整数性能，属于行业通用基准 | [GitHub](https://github.com/eembc/coremark)                                                    |
| 3   | core-v-mcu 快速启动示例 | 基础验证 | Ruyi SDK 最小 Console / 启动模板  | [GitHub](https://github.com/openhwgroup/core-v-mcu/blob/master/emulation/quickstart/README.md) |


---

### 2. 功能 / 库支持类示例

围绕单一技术能力（如 GPIO、编译流程、库调用）提供最小可运行示例。

#### 内容特征

- wiringX 等常用外设库
- OpenCV 基础几何绘图
- 网络、文件系统等基础能力
#### 目标受众

- 初学者
- 刚接触 RISC-V 的开发者
- 想快速做点东西的玩家 / 工程师
#### 示例风格

- 以任务为导向（点灯 / 控制 / 通信）
- 强调“用 Ruyi 怎么更省事”
- 示例短、小、成功反馈快
#### 调研示例

| 序号  | 项目名称                    | 类别            | 核心价值 / 验证点                     | 源码链接                                                                                    |
| --- | ----------------------- | ------------- | ------------------------------ | --------------------------------------------------------------------------------------- |
| 1   | 2048.c                  | 终端应用          | 终端 IO、ANSI 转义码、单文件编译           | [GitHub](https://github.com/mevdschee/2048.c)                                           |
| 2   | cpufetch                | 系统工具          | RISC-V 架构识别（显示 ISA 扩展）         | [GitHub](https://github.com/Dr-Noob/cpufetch)                                           |
| 3   | tiny-AES-c              | 算法/安全         | 验证 RISC-V 基础算力与逻辑运算正确性         | [GitHub](https://github.com/kokke/tiny-AES-c)                                           |
| 4   | SQLite                  | 数据库           | 验证文件系统 I/O 与 C 标准库兼容性          | [官网](https://www.sqlite.org/download.html)                                              |
| 5   | Lua                     | 脚本语言          | 证明 Ruyi 可编译并运行完整的语言运行时         | [GitHub](https://github.com/lua/lua)                                                    |
| 6   | Dhrystone               | 性能跑分          | 业界标准整数运算指标，厂商认可度高              | [GitHub](https://github.com/Keith-S-Thompson/dhrystone)                                 |
| 7   | iperf3                  | 网络工具          | 验证板子网络带宽与驱动表现的核心工具             | [GitHub](https://github.com/esnet/iperf)                                                |
| 8   | Zstd                    | 压缩算法          | 验证工具链对密集内存操作的优化能力              | [GitHub](https://github.com/facebook/zstd)                                              |
| 9   | minimp3                 | 多媒体           | 纯 C 编写，验证 RISC-V 数据解码能力        | [GitHub](https://github.com/lieff/minimp3)                                              |
| 10  | wiringX                 | 外设控制          | 验证 RISC-V 板卡 GPIO/I2C/SPI 外设驱动 | [GitHub](https://github.com/wiringX/wiringX)                                            |
| 11  | CORE-V MCU SDK Examples | MCU 外设 / RTOS | RISC-V 原生外设能力验证示例              | [GitHub](https://github.com/openhwgroup/core-v-mcu-sdk-examples)                        |
| 12  | SFML                    | 图形窗口          | Ruyi 图形/SDL/gl4es 能力验证         | [官网](https://en.wikipedia.org/wiki/Simple_and_Fast_Multimedia_Library)                  |
| 13  | Silicon Labs            | 嵌入式外设         | Ruyi SDK 外设示例，验证 GPIO/UART     | [GitHub](https://github.com/SiliconLabs/peripheral_examples_simplicity_sdk)             |
| 14  | Allegro                 | 图形库 / 多媒体     | 验证 Ruyi SDK GLES/SDL 图形渲染能力    | [Allegro 官方文档](https://en.wikipedia.org/wiki/Allegro_(software_library))                |
| 15  | WiSeConnect SDK         | 网络工具          | 验证 RISC-V DHCP/TCP 基础网络通信能力    | [WiSeConnect SDK 示例文档](https://docs.silabs.com/wiseconnect/3.5.1/wiseconnect-examples/) |
| 16  | 音视频开源示例集合               | 音视频           | 验证 RISC-V OpenGL/SDL2 音视频渲染能力  | [音视频开源示例集合](https://github.com/0voice/awesome_audio_video_learning)                     |

---

### 3. 应用实战类示例

将多个能力点组合成一个完整的小应用，用于展示 RuyiSDK 在真实场景中的使用方式。

#### 内容特征

- 简单 Web 服务
- 图像分类 / 人脸检测
- 结合具体开发板能力的完整应用

#### 目标受众

- 有一定基础的开发者
- 学生项目 / Demo 展示
- 厂商技术人员

#### 示例风格

- 实践导向
- 强调完整流程（构建 → 运行 → 效果）
- 不追求复杂算法，追求“跑通 + 可复现”

#### 调研示例

| 序号  | 项目名称          | 类别         | 核心价值 / 验证点              | 源码链接                                                    |
| --- | ------------- | ---------- | ----------------------- | ------------------------------------------------------- |
| 1   | Mongoose      | 网络服务       | 极简 Web 服务器，验证网络协议栈      | [GitHub](https://github.com/cesanta/mongoose)           |
| 2   | TIDL-SDK 人脸检测 | AI / CV 应用 | 面向用户的完整 AI 应用场景         | [GitHub](https://github.com/Dr-Noob/cpufetch)           |


---

## 三、示例类型与用户匹配关系总结

| 示例类型  | 主要内容                   | 目标受众      | 在示例库中的级别 |
| ----- | ---------------------- | --------- | -------- |
| 基础验证类 | Hello World / Coremark | 内部测试 / 老手 | 起点、基础    |
| 功能库示例 | wiringX / 网络           | 初学者       | 核心       |
| 应用实战类 | Web / AI / 图像          | 进阶用户      | 拓展       |
