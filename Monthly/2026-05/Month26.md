# Month26

戊寅小队本月工作

## RuyiSDK

- 开发板示例文档扩充
	- VisionFive2Lite
		- [RuyiSDK GPIO功能示例：VisionFive 2 Lite GPIO PUD 验证](https://github.com/zhiyao310/board-docs/blob/main/VisionFive2Lite/GPIO_PUD/README_zh.md)
		- [RuyiSDK GPIO功能示例：VisionFive 2 Lite LED 闪烁基准测试](https://github.com/zhiyao310/board-docs/blob/main/VisionFive2Lite/GPIO_LED/README_zh.md)
	- DuoS 
		- [PWM 脉宽调制测试](https://github.com/ZihanCheng63/ruyisdk-dev-archive/blob/main/reports/ZihanCheng/Duo_S/example_pwm_Duo_S.md)
		- [I2C OLED 显示屏测试](https://github.com/ZihanCheng63/ruyisdk-dev-archive/blob/main/reports/ZihanCheng/Duo_S/example_I2C_Duo_S.md)
	- ESP32-P4-Function-EV-Board
		- 概述:[README.md](https://github.com/zhiyao310/board-docs/blob/main/ESP32-P4/README.md);[README_zh.md](https://github.com/zhiyao310/board-docs/blob/main/ESP32-P4/README_zh.md)
		- [HelloWorld](https://github.com/zhiyao310/board-docs/blob/main/ESP32-P4/HelloWorld/README_zh.md)
		- [Coremark](https://github.com/zhiyao310/board-docs/blob/main/ESP32-P4/Coremark/README_zh.md)
		- [RuyiSDK LVGL 示例：LVGL Demo v8](https://github.com/zhiyao310/board-docs/blob/main/ESP32-P4/LVGL%20Demo%20v8/README_zh.md)
		- [RuyiSDK LVGL 示例：LVGL Demo v9](https://github.com/zhiyao310/board-docs/blob/main/ESP32-P4/LVGL_Demo_v9/README_zh.md)
	- Nuclei RV-STAR
		- [Coremark](https://github.com/ZihanCheng63/ruyisdk-dev-archive/blob/main/reports/ZihanCheng/Nuclei%20RV-STAR/example_Coremark_rv-star.md)
		- [HelloWorld](https://github.com/ZihanCheng63/ruyisdk-dev-archive/blob/main/reports/ZihanCheng/Nuclei%20RV-STAR/example_HelloWorld_rv-star.md)
- RuyiSDK开发资源梳理和资源申请
	- [[Resource Request]: riscv32-esp-elf Toolchain for ESP32 Series (Bare-metal)](https://github.com/ruyisdk/ruyisdk/issues/87)
## 英麒RISC-V Lab

Licheepi4A 示例文档：  
- [YOLOV5s](https://github.com/TOT2232/board-docs/blob/main/LicheePi4A/YOLOV5s/README_zh.md)

Duo 256M 示例文档：  
- [YOLOv5](https://github.com/TOT2232/board-docs/blob/main/Duo_256m/YOLOv5/READEME_zh.md)
- [YOLOv8](https://github.com/TOT2232/board-docs/blob/main/Duo_256m/YOLOv8/README_zh.md)
- [YOLOv11](https://github.com/TOT2232/board-docs/blob/main/Duo_256m/YOLOv11/README_zh.md)
- [YOLOv12](https://github.com/TOT2232/board-docs/blob/main/Duo_256m/YOLOv12/README_zh.md)

## 科学日
### 1.RuyiSDK RISC-V 嵌入式开发课堂 ——DHT22+OLED 温湿度检测编程实验

- [RuyiSDK RISC-V 嵌入式开发课堂主体文档](https://github.com/DuoQilai/PLCT-Works/blob/main/Notes/ScienceDay/%E7%A7%91%E5%AD%A6%E6%97%A5/RuyiSDK%20RISC-V%20%E5%B5%8C%E5%85%A5%E5%BC%8F%E5%BC%80%E5%8F%91%E8%AF%BE%E5%A0%82%20%E2%80%94%E2%80%94DHT22%2BOLED%20%E6%B8%A9%E6%B9%BF%E5%BA%A6%E6%A3%80%E6%B5%8B%E7%BC%96%E7%A8%8B%E5%AE%9E%E9%AA%8C.md#752-%E5%AE%8C%E6%95%B4%E4%BB%A3%E7%A0%81) 
- [Dht22 部署文档](https://github.com/ZihanCheng63/my-repo/blob/main/Duo_S/Dht22%20%E9%83%A8%E7%BD%B2%E6%96%87%E6%A1%A3.md)
- [OLED 例题](https://github.com/ZihanCheng63/my-repo/blob/main/ruyi/%E7%A7%91%E5%AD%A6%E6%97%A5/%E4%BE%8B%E9%A2%98)
- [OLED 示例填空](https://github.com/ZihanCheng63/my-repo/blob/main/ruyi/%E7%A7%91%E5%AD%A6%E6%97%A5/%E5%A1%AB%E7%A9%BA)

### 2.中科院公众科学日 · RISC-V 三国杀互动 Demo

### 活动概况

- 参与中科院公众科学日展示活动，现场布展并演示全栈互动应用，活动当天工作量较大。
- 项目仓库：[OpenSiliconBet](https://github.com/EnzoDing-rgb/OpenSiliconBet) — RISC-V 三国杀 · 指令集 × AI/Agent 时代互动 Demo。

#### 项目概述

- 全栈小应用（FastAPI + React/Vite）：论坛交锋形式，设 RISC-V / x86 / ARM 三阵营 + Lex 主持 + 黄仁勋环节 + 观众问答。
- 面向中关村·公众科学日类科普分会场，不做胜负式辩论，强调科普互动体验。

#### 5 月开发迭代

- **5 月 11–13 日：项目启动与基建搭建**
    
    - 搭建 FastAPI 后端 + React/Vite 前端骨架。
    - 接入火山引擎 API（OpenAI 协议），完成 LLM 对话编排。
    - 完成 deep-research 背景调研与跨源资料整合（`docs/background/`）。
    - 五嘉宾 perspective SKILL 设计与文档（`docs/characters/`）。
- **5 月 14 日：核心功能成型**
    
    - 黄仁勋角色接入并成功发言。
    - DeepResearch 背景资料补充完善。
    - 项目初具雏形，跑通完整辩论/论坛流程。
    - 接入 DashScope TTS（qwen3-tts-vc-realtime），实现五辩手 + 黄仁勋语音合成。
    - 完成 `.env` 环境变量配置体系与 `.env.example` 模板。
- **5 月 15–16 日：功能打磨与 v0.1 发布**
    
    - 完成 EndingScreen 粒子动画结尾页面。
    - 音量提升 100x + Q&A 独立音频状态机。
    - 跳过观众问答 + Chat TTS 功能。
    - 开场视频增强 + Lex 开场白音频音量提升 10 倍。
    - 修复 Q&A 无音频问题，添加 `noAutoStart` prop。
    - 发布 v0.1 版本。
- **5 月 17 日：收尾与远程联调**
    
    - 远程 pull + merge，完成最终现场可用版本。

#### 文档体系

- `docs/design/architecture.md` — 架构宪章
- `docs/design/implementation.md` — 实现计划与测试策略
- `docs/design/realtime-tts-architecture.md` — 实时 TTS 架构
- `docs/background/deep-research.md` — 共享事实背景
- `docs/characters/` — 五嘉宾视角 SKILL
- `dev.sh` — 一键本地运行 / Cloudflare Tunnel 生产部署脚本
- `README.md` — 完整项目文档与使用说明

#### 技术栈

- 后端：FastAPI, Uvicorn, OpenAI SDK, DashScope TTS（可选）, WebSocket
- 前端：React 18, TypeScript, Vite, Vitest
- 部署：Cloudflare Tunnel；生产可由 FastAPI 单端口托管 `frontend/dist`

嵌入式
## 其他运行相关

- [B站视频去水印及二次剪辑操作手册](https://github.com/zhiyao310/ruyisdk-dev-archive/blob/main/research/bili_test.md)

## RISC-V Linux系统与开发板实践课程
- [初步教学大纲](https://github.com/EnzoDing-rgb/riscv-embedded-course/blob/master/docs/outline.md)
- [调研文档]()