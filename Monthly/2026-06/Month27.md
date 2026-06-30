# Month27

戊寅小队本月工作

## RuyiSDK

- 开发板示例文档扩充
	 - Canaan K510-CRB-V1.2 KIT：测试用例及说明文档
		- 概述:[README.md](http://github.com/ruyisdk/board-docs/blob/main/K510/README.md);[README_zh.md](https://github.com/ruyisdk/board-docs/blob/main/K510/README_zh.md)
		- [HelloWorld](https://github.com/ruyisdk/board-docs/blob/main/K510/HelloWorld/README.md)
		- [Coremark](https://github.com/ruyisdk/board-docs/blob/main/K510/Coremark/README.md)
		- [RuyiSDK GPIO 示例：GPIO KEYS Demo](https://github.com/ruyisdk/board-docs/blob/main/K510/GPIO_KEYS/README.md)
		- [RuyiSDK 系统示例：RTC Demo](https://github.com/ruyisdk/board-docs/blob/main/K510/RTC/README.md)
	- Milk-V Duo S
		- [SPI 测试](https://github.com/ZihanCheng63/board-docs/blob/main/Duo_S/SPI/README_zh.md)
		- [DF9GMS 测试](https://github.com/ZihanCheng63/board-docs/blob/main/Duo_S/DF9GMS/README_zh.md)
- 前端示例网站
	- 项目仓库：[board-docs-frontend](https://github.com/DuoQilai/board-docs-frontend)
	- 在线站点：[https://board-docs-frontend.pages.dev/](https://board-docs-frontend.pages.dev/)
	- **CI 自动化**：新增每日 `board-docs` 子模块自动同步工作流——有更新则验证 `pnpm build` 通过后推送 `main`，触发线上重新部署。
	- **修复同步流程**：修正 pnpm 安装（仅用 `packageManager` 字段）、submodule sync 在提交前不再 reset、CI pnpm 版本等问题。
	- **示例分类扩展**：扩充示例 `status` 分类 slug（基础 / 外设 / 通信 / 网络 / 系统 / 多媒体 / 视觉 / AI / 加密 / 压缩 / GUI / 性能测试），旧值自动映射。
	- **访问统计**：接入 Cloudflare Web Analytics beacon，并简化为 Cloudflare-only 部署的统计文档。
	- **文档整理**：文档统一收进 `docs/` 目录；README 补充线上地址与部署事实；部署 / 统计文档按场景拆分；补充验证步骤的 Mac 快捷键说明。

## 7月台账

测试开发板的可用性

- 已经烧录镜像、安装ruyi、测试 ruyi gcc 工具链
	- [EBC7700](https://github.com/DuoQilai/PLCT-Works/blob/main/Notes/July_Ledger/EBC7700.md)
	- [P550](https://github.com/DuoQilai/PLCT-Works/blob/main/Notes/July_Ledger/EBC7702.md)
	- [EBC7702](https://github.com/DuoQilai/PLCT-Works/blob/main/Notes/July_Ledger/P550.md)
- 调研开发板操作系统和基本测试用例
	- [A210 Debian](https://github.com/DuoQilai/PLCT-Works/blob/main/Notes/July_Ledger/A210.md)
	- [K3 Ubuntu](https://github.com/DuoQilai/PLCT-Works/blob/main/Notes/July_Ledger/K3_Pico-ITX.md)
	- [SG2044 Ubuntu](https://github.com/DuoQilai/PLCT-Works/blob/main/Notes/July_Ledger/SG2044.md)
- 测试或调研失败
	- V100 
		- 公开资料能证明 V100 平台 Linux 和服务器固件栈已在 FPGA 原型平台上运行和演示；但完整产品规格书、整机手册、系统镜像、BSP 仓库、默认账号密码仍需供应商提供。
	- [CH32V208WBU6-EVT-R0-1v4 测试报告](https://github.com/zhiyao310/ruyisdk-dev-archive/blob/main/reports/ZhiyaoBian/Test%20repoorts/CH32V208.md)
	- [Sipeed Tang Mega 138K 测试报告](https://github.com/ZihanCheng63/my-repo/blob/main/10%E7%A7%8D%E5%BC%80%E5%8F%91%E6%9D%BF%2B%E7%BC%96%E8%AF%91%E5%99%A8%E6%B5%8B%E8%AF%95%E7%94%A8%E4%BE%8B-v2\(1\).docx)
- 调研报告
	- [8项开发板调研报告](https://github.com/zhiyao310/ruyisdk-dev-archive/blob/main/research/8%E9%A1%B9Linux%E5%BC%80%E5%8F%91%E6%9D%BF%E8%B0%83%E7%A0%94%E6%8A%A5%E5%91%8A.md)
## 英麒RISC-V Lab

	todo

## RISC-V Linux系统与开发板实践课程

### riscv-embedded-course · 自研课程大纲（课程研发）

- 项目仓库：[riscv-embedded-course](https://github.com/EnzoDing-rgb/riscv-embedded-course)
- 在线大纲：[https://enzoding-rgb.github.io/riscv-embedded-course/](https://enzoding-rgb.github.io/riscv-embedded-course/)
- 定位：实习生课程研发，独立产出的一版《RISC-V Linux 嵌入式实践》课程草稿——在 RISC-V Linux 开发板上用 RuyiSDK + C 做嵌入式应用，含术语表、章节表、物料 BOM 与递进式项目。

#### 主要工作

- 多轮打磨课程大纲：白话重写、收敛为单板流程、调整 capstone 项目（关键词识别 + LED 控制）、去除 RevyOS 改用通用 Linux 表述、补充推荐教材、按 RuyiSDK 重构结构并附 Advanced Track。
- 产出 10 章 MNIST 方向 `CourseOutline`，精简 BOM 与 README，对齐 ch01–ch07。
- 改为 Linux 嵌入式方向大纲并加入 IoT capstone；README 白话重写。
- 上线 GitHub Pages：单入口 + `index.html` 跳转至 `CourseOutline.html`，浏览器直接可看完整大纲。
- 填写并整理课程进度表，移除本地 Excel 脚手架。


### ruyi-riscv-linux-book · 教材仓库协作（重构 + 教案）

- 项目仓库：[ruyi-riscv-linux-book](https://github.com/DuoQilai/ruyi-riscv-linux-book)

#### 主要工作

- 确立大纲和基本课程仓库架构
- 仓库重构：将仓库重整为按章、按节的标准布局——`chapters/ch01|ch02/` 下每节拆为 `lecture.md`（讲义）+ `lab.md`（实验），整章 `slides.html`，新增 `boards/` 板卡参考与 `docs/archive/` 历史归档。
- 教案撰写：完成 Chapter 1（开发环境篇，1.1–1.5）与 Chapter 2（工具链与工程，2.1–2.6）的讲义与实验，前后写了两版，统一格式；ch02 含 hello、project-template 示例代码。

#### 仓库结构

```
ruyi-riscv-linux-book/
├── docs/CourseOutline.html   # 课程总大纲
├── chapters/
│   ├── ch01/  # 开发环境篇（1.1–1.5）：slides.html + 各节 lecture.md / lab.md
│   └── ch02/  # 工具链与工程（2.1–2.6）：slides.html + code/ + 各节 lecture.md / lab.md
└── boards/    # licheepi4a / k1 板卡参考
```


