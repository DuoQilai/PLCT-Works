# Month29

戊寅小队本月工作

## RuyiSDK Board Docs

- Ruyi 示例文档库：
	- 仓库：[ruyisdk/board-docs](https://github.com/ruyisdk/board-docs)
	- 开发板示例文档扩充：
		- SpacemiT K3 Pico-ITX：新增中英文板卡概述及 CoreMark、HelloWorld、llama-server 中文示例文档，见 [PR #33](https://github.com/ruyisdk/board-docs/pull/33)。
		- HelloWorld 英文文档：补充 BPI-F3、Duo、Duo S、EBC7700、Jupiter2、K3 Pico-ITX、LicheePi 4A 等开发板的英文文档，见 [PR #36](https://github.com/ruyisdk/board-docs/pull/36)。
		- Canaan K510：整理 CoreMark 与 HelloWorld 的中英文文档和示例目录，见 [PR #37](https://github.com/ruyisdk/board-docs/pull/37)。
		- BPI-CANMV-K230D-Zero（原 K230D）：新增板卡概述与系统安装文档，文档见 [PR #41](https://github.com/ruyisdk/board-docs/pull/41)，命名更新见 [PR #42](https://github.com/ruyisdk/board-docs/pull/42)。
	- 仓库维护：
		- 将示例分类元数据统一为 `category`，见 [PR #27](https://github.com/ruyisdk/board-docs/pull/27)。
		- 完善中英文示例文档模板，见 [PR #28](https://github.com/ruyisdk/board-docs/pull/28)。
		- 新增元数据检查及配套工作流，见 [PR #30](https://github.com/ruyisdk/board-docs/pull/30)。
		- 新增 DCO 检查并改进 Pull Request 模板，见 [PR #31](https://github.com/ruyisdk/board-docs/pull/31)。
		- 将 `board-docs` 的文档站入口更新为 [boards.ruyisdk.org](https://boards.ruyisdk.org/)，见 [PR #32](https://github.com/ruyisdk/board-docs/pull/32)。
		- 新增 README 支持矩阵自动生成与一致性检查，见 [PR #34](https://github.com/ruyisdk/board-docs/pull/34)。
		- 补充板卡与示例命名、版本记录和中英文文档规范，见 [PR #35](https://github.com/ruyisdk/board-docs/pull/35)。
		- 统一 Ruyi 安装章节和版本化下载路径，新增版本更新脚本及每月版本更新工作流，见 [PR #38](https://github.com/ruyisdk/board-docs/pull/38)。
		- 新增示例级中英文覆盖率检查，支持报告模式和严格模式，见 [PR #40](https://github.com/ruyisdk/board-docs/pull/40)。
- board-docs-frontend：
	- 项目仓库：[DuoQilai/board-docs-frontend](https://github.com/DuoQilai/board-docs-frontend)
	- 在线站点：[中文入口](https://boards.ruyisdk.org/)；[英文入口](https://boards.ruyisdk.org/en/)
	- 完善示例分类读取和展示逻辑，支持 `category` 元数据、扩充分类体系并统一入门分类标签，见 [PR #1](https://github.com/DuoQilai/board-docs-frontend/pull/1)、[PR #2](https://github.com/DuoQilai/board-docs-frontend/pull/2) 和 [PR #3](https://github.com/DuoQilai/board-docs-frontend/pull/3)。
	- 配置正式站点地址、站点地图和中英文语言配置，新增 Pull Request 与 `main` 分支构建检查，见 [PR #5](https://github.com/DuoQilai/board-docs-frontend/pull/5)。
	- 完成中英文界面、共享页面组件、英文路由和语言切换，见 [PR #6](https://github.com/DuoQilai/board-docs-frontend/pull/6)。
	- 新增前端分类与 `board-docs` 元数据的双向一致性检查；未知分类回退到“其他”，并可发现跨仓库分类不一致，见 [PR #7](https://github.com/DuoQilai/board-docs-frontend/pull/7)。
	- 按页面语言选择 `README.md`、`README_zh.md` 或旧版示例文档；缺少对应语言时显示回退提示，见 [PR #8](https://github.com/DuoQilai/board-docs-frontend/pull/8)。

## RuyiSDK Support Matrix

- 仓库：[ruyisdk/support-matrix](https://github.com/ruyisdk/support-matrix)
- 操作系统支持报告更新：
	- VisionFive 2 Lite：
		- 新增中英文 Ubuntu 测试报告：[PR #390](https://github.com/ruyisdk/support-matrix/pull/390)。
		- 新增中英文 Debian 测试报告：[PR #391](https://github.com/ruyisdk/support-matrix/pull/391)。
	- Canaan K510：
		- 更新中英文 BuildRoot 测试报告：[PR #392](https://github.com/ruyisdk/support-matrix/pull/392)。

## K3 Pico-ITX AI 服务与设备中控

- 仓库：[DuoQilai/k3-agent-server](https://github.com/DuoQilai/k3-agent-server)
- 建立可复现的 K3 AI 服务部署基线，整理 DSH Agent、llama-server、本地模型、systemd 用户服务及日常启停与日志文档，见 [Commit 3bc2926](https://github.com/DuoQilai/k3-agent-server/commit/3bc29267401823a65c2ff6a0a180b1615349e3b2)。
- 完成 fleet 设备中控 MVP：提供设备清单、SSH/scp 操作、CLI、stdio MCP 服务和审计约束，见 [PR #1](https://github.com/DuoQilai/k3-agent-server/pull/1)。
- 编写 OpenClaw 部署与运维文档，见 [PR #2](https://github.com/DuoQilai/k3-agent-server/pull/2)。

## RISC-V Linux 系统与开发板实践课程

- ruyi-riscv-linux-book：
	- 项目仓库：[DuoQilai/ruyi-riscv-linux-book](https://github.com/DuoQilai/ruyi-riscv-linux-book)
	- 课程修改方案：
		- [《课程内容更新汇报（第 1–4 章）》](https://github.com/DuoQilai/ruyi-riscv-linux-book/blob/enzo/MISC/course-updates-report.md)：汇总 8 月 20—26 日的课程调整，包括 RuyiSDK 安装、虚拟环境、系统烧录和交叉编译流程，以及 C 语言、GPIO、继电器、`select` 和命令解析示例的补充与结构优化。
	- 第 1—6 章课程内容建设：
		- [PR #4](https://github.com/DuoQilai/ruyi-riscv-linux-book/pull/4)：完成课程首页、大纲、课程说明、评价标准和导航等课程框架，以及第一章“环境与工具链”的讲义、实验和 CoreMark 上板通道验收内容。
		- [PR #5](https://github.com/DuoQilai/ruyi-riscv-linux-book/pull/5)：完成第二章“够用的 C 语言基础”的讲义与实验，补充多文件构建、命令表、滞回温控等可运行示例和学生练习脚手架。
		- [PR #6](https://github.com/DuoQilai/ruyi-riscv-linux-book/pull/6)：完成第三章“GPIO 与执行器”的讲义与继电器控制风扇实验，提供 GPIO 示例、温控程序和 LicheePi 4A 相关参考资料。
		- [PR #7](https://github.com/DuoQilai/ruyi-riscv-linux-book/pull/7)：完成第四章“串口对话与温控”的讲义与实验，覆盖 DHT22、TXS 电平转换、命令分发和基于 `select` 的采样控制主循环。
		- [PR #8](https://github.com/DuoQilai/ruyi-riscv-linux-book/pull/8)：完成第五章“网络与 MQTT”的讲义与远程控灯实验，覆盖 Broker、主题、发布订阅、状态上报和 TCP/IP 分层抓包，并提供 `mqtt-led` 项目脚手架。
		- [PR #9](https://github.com/DuoQilai/ruyi-riscv-linux-book/pull/9)：完成第六章“线程与协同”的讲义与实验，提供 `race-demo` 和 `tri-thread` 示例，讲解数据竞争、ThreadSanitizer、互斥锁和安全退出。

## RISC-V 中国峰会

- 提交两项峰会提案：
	- [RISC-V课程移植方法与RuyiSDK生态建设](https://cfp2026.riscv-summit-china.org/rvsc2026/talk/review/JJPCAAGRQEGEDGWMXHGFHZCBGA97ASGT)
	- [从碎片化到体系化：RISC-V 课程质量评估与系统化重构](https://cfp2026.riscv-summit-china.org/rvsc2026/talk/review/KLZWWYCLBYPQHYWYHKHT8CYPHNMGHYSF)

## 其他

- 开发板测试素材：
	- 补充 A210 SODIMM V2、RISC-V Book 和 RISC-V Book 2 的 5 张测试环境照片及拍摄说明，见 [PR #3](https://github.com/DuoQilai/asciinema/pull/3)。
	- 补充 VisionFive 2 Lite 和 K510 的 4 张测试环境照片，见 [PR #4](https://github.com/DuoQilai/asciinema/pull/4)。
- RuyiSDK 汇报材料：
	- 完成[《RuyiSDK 支持矩阵与开发板文档》汇报材料](https://github.com/DuoQilai/PLCT-Works/blob/main/Notes/RuyiSDK/RuyiSDK%E6%94%AF%E6%8C%81%E7%9F%A9%E9%98%B5%E4%B8%8E%E5%BC%80%E5%8F%91%E6%9D%BF%E6%96%87%E6%A1%A3-%E6%B1%87%E6%8A%A5.pptx) 。
