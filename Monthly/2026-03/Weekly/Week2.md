# Week 2

本周工作
## RuyiSDK

示例库扩充——cpufetch:
-  [LicheePi4A_cpufetch测试文档](https://github.com/zhiyao310/plct_works/blob/main/outcome_list/Licheepi4A/cpufetch/LicheePi4A_cpufetch.md)
	- 视频链接：[【RISC-V架构识别】在Licheepi4A上使用cpufetch获取CPU信息](https://www.bilibili.com/video/BV1j8wFzSE2x?vd_source=63f9297bce04de7108868464326f7b22)
-  [Ruyi 平台下 cpufetch 安装与使用测试报告](https://github.com/zhiyao310/plct_works/blob/main/outcome_list/Licheepi4A/cpufetch/Ruyi%20%E5%B9%B3%E5%8F%B0%E4%B8%8B%20cpufetch%20%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8%E6%B5%8B%E8%AF%95%E6%8A%A5%E5%91%8A.md)
	- [ruyisdk资源接入issue](https://github.com/ruyisdk/packages-index/issues/168)

示例库扩充——tiny-AES-c
- 测试文档

示例库进展
- 示例库提交模板
- 示例库官网展现形式：
	1. 主页 划分一个区域 2*3 展示 大约最新的6个开发板（手动维护）
	2. 集成设备页：计划参考支持矩阵的 https://matrix.ruyisdk.org/ 默认页面展示所有的开发板，并支持查询。
		docs仓库中的文档对开发板的集成：通过在文档中加入开发板链接

## 支持矩阵

- [修复文档失效链接 pr](https://github.com/ruyisdk/support-matrix/pull/385)
- 申请【Sipeed Tang Mega 138K】测试
- 在 fork 的仓库继续提交文档

## 英麒

- 利用 LicheePi 4A 平台（基于 Revy OS）成功从源码编译并运行 Home Assistant 核心服务 (Core)，视频还没录制和剪辑好。
	- 文档链接： https://gitee.com/zjx_666/lichee-pi_4-a/blob/master/Home_Assistant.md
- Triton 在 RISC-V 平台（LicheePi 4A）的静态编译调研：
	1. 已经成功打通了 ZCC 交叉编译工具链，通过测试命令，已经确认编译器能正常生成支持向量扩展的指令。
	2. 在尝试构建 Triton 后端插件时，发现教程中展示的 third_party/riscv 源代码目录在官方 Triton 仓库中并不存在。教程中的 RISC-V 后端（包含 compiler.py 和 driver.py 等核心逻辑）是针对 ZCC 编译器定制开发的非公开代码。