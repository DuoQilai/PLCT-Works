# 零从开始的成长教程
## 1 初识开发板
目前实验室主要的开发板是Licheepi 4A，可以先熟悉下。
### 1.1 Licheepi 4A 的官网
链接：[板卡介绍 - Sipeed Wiki](https://wiki.sipeed.com/hardware/zh/lichee/th1520/lpi4a/1_intro.html)
### 1.2 烧录Licheepi 4A
有两种烧录方法，选emmc烧录。
- 你需要准备的配件：Licheepi 4A的电源适配器、一根tape-c线、一根串口线、HDMI线、键鼠。
- 终端工具：putty、mobaxterm
- 烧录工具：rufus、balenaEtcher
- Linux：[LicheePi4A镜像刷写教程(Linux) | RevyOS Docs](https://docs.revyos.dev/docs/Installation/licheepi4a/)
- Windows：[LicheePi4A镜像刷写教程(Windows) | RevyOS Docs](https://docs.revyos.dev/docs/Installation/licheepi4a-windows/)
### 1.3 基础使用
跟着教程练习登录系统、打开命令行、连接网络、连接蓝牙、软件安装、SSH登录（重要）。
按照教程跑通一遍，文字+图片记录结果，以md格式提交到github。
- 链接：[桌面系统基础使用 - Sipeed Wiki](https://wiki.sipeed.com/hardware/zh/lichee/th1520/lpi4a/5_desktop.html)
### 1.4 维护设备
有了上面的基础，你就可以维护实验室的设备了，主要是学会串口登录和SSH登录。远程使用设备的老师会在群里请你协助怎么做。协助完成后，你可以记录下学到的命令，有什么作用。

注意，使用中的设备不能私自关机，需要先确认。
### 1.5 完成案例
首先按照教程跑通一遍，文字+图片记录结果，以md格式提交到github。

使用录屏软件录制过程：OBS、EV录屏

使用剪辑软件配音，剪掉多余部分加上字幕：剪映，需要会员找我
- [Run Llama.cpp with Deepseek on Risc-V(Licheepi 4A)](https://github.com/Ruixi-Cheng/PLCT-Works/blob/main/month0/week1/LLM_on_Lichee_Pi_4A/Run_Llamacpp_with_Deepseek_on_Risc-V\(Licheepi%204A\).md)
- [Licheepi 4A运行游戏Baby Is You | RevyOS Docs](https://docs.revyos.dev/docs/typical-applications/baby-is-you-game/)

## 2 RuyiSDK
跟练案例、写测试报告（记录步骤和结果）、录制视频（拍摄时英麒logo入镜）
### 2.1 RuyiSDK官网
链接：[Hello Ruyi | RuyiSDK](https://ruyisdk.org/docs/intro/)

### 2.2 安装RuyiSDK
注意是在Linux下
- 链接：[安装 | RuyiSDK](https://ruyisdk.org/docs/Package-Manager/installation)

### 2.3 完成案例
实验室有的板子都可以试试，同1.5

同时，文字+图片记录结果发布论坛：[RISC-V 开发者社区 - RISC-V 开发者社区 (ruyisdk.cn)](https://ruyisdk.cn/)
- 链接：[使用案例 | RuyiSDK](https://ruyisdk.org/docs/category/%E4%BD%BF%E7%94%A8%E6%A1%88%E4%BE%8B)
