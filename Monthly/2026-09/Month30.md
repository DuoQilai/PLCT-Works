# Month30

戊寅小队本月工作

## RuyiSDK Board Docs

- Ruyi 示例文档库：
	- 仓库：[ruyisdk/board-docs](https://github.com/ruyisdk/board-docs)
	- 开发板示例文档扩充：
		- HiFive Premier P550：新增中英文板卡概述、Hello World 和 CoreMark 示例，覆盖 GCC、LLVM 工具链的编译与运行，见 [PR #46](https://github.com/ruyisdk/board-docs/pull/46)。
		- SpaceMIT K3 CoM260 Kit：新增中英文板卡概述和 Hello World 示例、中文 CoreMark 示例，并补充 ROS 2 第 1—2 章课程入口，见 [PR #47](https://github.com/ruyisdk/board-docs/pull/47)。
	- ROS 2 课程接入：
		- 为 K3 Pico-ITX 新增课程入口及第一章课程元数据，关联 RISC-V 与 x86 版本的教案、实验手册和运行环境，见 [PR #44](https://github.com/ruyisdk/board-docs/pull/44)。
		- 将课程文档来源切换至 GitHub 镜像，完善课程介绍、教案和实验手册的链接，见 [PR #45](https://github.com/ruyisdk/board-docs/pull/45)。
		- 为 K3 Pico-ITX、CoM260 Kit 接入独立课程目录，并增加 CoM260 Kit 第 3—4 章的 RISC-V 与 x86 课程入口，见 [PR #48](https://github.com/ruyisdk/board-docs/pull/48)。
		- 更新 K3 Pico-ITX、CoM260 Kit 的课程元数据，改为引用课程仓库 `course_support` 目录下的板卡课程清单，见 [PR #49](https://github.com/ruyisdk/board-docs/pull/49)。
	- 仓库维护：统一板卡文档、元数据及中英文索引中的 SpaceMIT 厂商名称，见 [PR #43](https://github.com/ruyisdk/board-docs/pull/43)。
- board-docs-frontend：
	- 项目仓库：[DuoQilai/board-docs-frontend](https://github.com/DuoQilai/board-docs-frontend)
	- 在线站点：[中文入口](https://boards.ruyisdk.org/)；[英文入口](https://boards.ruyisdk.org/en/)
	- 新增 ROS 2 课程页面和中英文访问路由，按开发板、章节及 RISC-V／x86 版本组织教案与实验手册；支持远程文档、图片和视频同步，补充首页课程预览、更新提示及统一顶部导航，见 [PR #9](https://github.com/DuoQilai/board-docs-frontend/pull/9)。
	- 优化移动端课程目录和正文显示，调整表格、长链接及代码块在窄屏下的布局，见 [PR #10](https://github.com/DuoQilai/board-docs-frontend/pull/10)。
	- 增加课程上一章／下一章导航，修正当前课程及章节的目录定位，并在首页展示最新课程章节，见 [PR #11](https://github.com/DuoQilai/board-docs-frontend/pull/11)。
	- 从固定版本的课程子模块读取目录、正文和媒体，依据课程目录生成章节路由、导航和最新章节预览；同步失败时保留原有缓存与素材，见 [PR #12](https://github.com/DuoQilai/board-docs-frontend/pull/12)。
	- 同步更新 README 中的课程目录路径示例，与课程仓库的新目录结构保持一致，见 [PR #13](https://github.com/DuoQilai/board-docs-frontend/pull/13)。

## RuyiSDK Support Matrix

- 仓库：[ruyisdk/support-matrix](https://github.com/ruyisdk/support-matrix)
- 操作系统支持报告更新：
	- HiFive Premier P550：
		- 更新 Debian 中英文测试报告，补充镜像烧录、启动与串口登录记录，见 [PR #393](https://github.com/ruyisdk/support-matrix/pull/393)。
		- 新增 Fedora 44 Server 中英文测试报告，补充 Bootchain 更新、启动配置及串口登录验证，见 [PR #400](https://github.com/ruyisdk/support-matrix/pull/400)。
	- Milk-V Duo S：
		- 更新 Arch Linux 测试报告，补充新版镜像的安装步骤、启动日志和录屏，见 [PR #394](https://github.com/ruyisdk/support-matrix/pull/394)。
		- 更新 Debian 13 社区镜像 v1.9.6 测试报告，补充系统信息、串口登录结果及启动告警记录，见 [PR #395](https://github.com/ruyisdk/support-matrix/pull/395)。
		- 更新 RT-Thread、RT-Thread Smart 5.2.2 测试报告，完善源码编译、小核与 FIP 打包、启动日志和录屏，见 [PR #396](https://github.com/ruyisdk/support-matrix/pull/396)、[PR #397](https://github.com/ruyisdk/support-matrix/pull/397)。
		- 更新 Ubuntu 24.04 LTS 中英文测试报告，补充镜像安装、系统信息和启动验证，见 [PR #398](https://github.com/ruyisdk/support-matrix/pull/398)。
		- 更新 Zephyr 4.1.99 中英文测试报告，完善构建、固件打包、UART1 接线和 C906 小核 Hello World 运行记录，见 [PR #405](https://github.com/ruyisdk/support-matrix/pull/405)。
		- 更新 xv6 中英文测试报告，补齐镜像准备、启动文件重新打包、烧录及成功启动证据，见 [PR #407](https://github.com/ruyisdk/support-matrix/pull/407)。
	- SpaceMIT K3 CoM260 Kit：
		- 新增中英文板卡概述及 Buildroot 1.0.7 测试报告，记录 TITANTOOLS 烧录、串口登录和 Weston 桌面验证，见 [PR #399](https://github.com/ruyisdk/support-matrix/pull/399)。
		- 新增 Bianbu 4.0.6 LXQt 中英文测试报告，补充系统初始化、串口登录、系统信息和桌面截图，见 [PR #401](https://github.com/ruyisdk/support-matrix/pull/401)。
		- 新增 OpenHarmony 6.1 中英文测试报告，记录默认启动因缺少设备树失败的问题，以及临时使用另一设备树进入 shell 和桌面的验证过程，见 [PR #402](https://github.com/ruyisdk/support-matrix/pull/402)。
		- 整理 openEuler 24.03-LTS-SP4 中英文待测文档，覆盖镜像下载与校验、解压烧录、UART 接线及 SD 卡启动步骤，见 [PR #403](https://github.com/ruyisdk/support-matrix/pull/403)。
	- CH32V307：更新 RT-Thread 5.3.1 中英文测试报告，改用官方 BSP，补充 SDK 依赖、存储配置、串口命令及板载以太网 DHCP／ping 验证，见 [PR #404](https://github.com/ruyisdk/support-matrix/pull/404)。
	- CH32V003：新增基于官方 `ch32v003f4p6-evt` BSP 的 RT-Thread 中英文测试报告，补充 Windows 编译、WCH-LinkE 接线、烧录与 USART1 启动至 msh 的验证记录，实测范围限于串口控制台，见 [PR #408](https://github.com/ruyisdk/support-matrix/pull/408)。
	- ESP32-C3：新增 RT-Thread 5.3.1 中英文测试报告，记录编译、烧录、启动至 msh 及基础命令验证，并补充 Windows 链接脚本和芯片版本适配说明，见 [PR #406](https://github.com/ruyisdk/support-matrix/pull/406)。
- 支持矩阵网站：排查并恢复内容同步，核对 CoM260 Kit 四项系统、P550 Fedora 44 和 CH32V307 RT-Thread 5.3.1 的页面更新，见 [CoM260 Kit 页面](https://matrix.ruyisdk.org/zh-CN/boards/CoM260_Kit/)、[P550 页面](https://matrix.ruyisdk.org/boards/Premier_P550/)、[CH32V307 页面](https://matrix.ruyisdk.org/boards/CH32V307/)。

## RISC-V ROS 2 机器人操作系统编程课程

- 项目仓库：[ROS2_RISCV](https://gitee.com/yunxiangluo/ROS2_RISCV)；[GitHub 镜像](https://github.com/DuoQilai/ROS2_RISCV)
- K3 Pico-ITX 课程移植与验证：
	- 完成第一章独立 C++17 课程源码、教师教案及实验手册，验证环境安装、DDS 通信与域隔离、生命周期节点、IDE 远程调试及 K3 与 x86 Gazebo 联动；整理第 1—4 章的运行证据、截图和连续录像，见 [PR !2](https://gitee.com/yunxiangluo/ROS2_RISCV/pulls/2)。
	- 完成第 2—4 章独立源码、教案和实验手册，覆盖节点与命名空间、日志工具、话题与自定义消息、QoS、执行器和服务通信，补充板端运行及 Gazebo 运动、停止验证，见 [Commit 07c86bb](https://gitee.com/chuachuaa/ROS2_RISCV/commit/07c86bbc94aa6cbd3a514b86230de8d167e41d93)。
- CoM260 Kit 课程移植与验证：
	- 第 1—2 章：基于 Bianbu 4.0.6／ROS 2 Humble 建立板端与 x86 课程环境，完成独立文档和 C++17 示例，验证 DDS、生命周期、建包、命名空间、日志过滤、远程调试和仿真里程计反馈，见 [PR !3](https://gitee.com/yunxiangluo/ROS2_RISCV/pulls/3)。
	- 第 3—4 章：完成话题、自定义消息、QoS、执行器和服务通信的教案、实验及源码；验证从空目录建包、方形运动、速度服务、无时钟与中断退出行为，并补充连续录像和运行记录，见 [PR !4](https://gitee.com/yunxiangluo/ROS2_RISCV/pulls/4)。
	- 第 5—6 章：完成动作通信、参数与 Launch 的 C++17 示例、教案和实验手册，验证动作反馈与取消、目标拒绝、参数校验、动态调速、巡航配置及独立信号停止；完成与 x86 Gazebo 的运动和停车联调、Nav2 组合启动验证，补齐截图、CAST、MP4、GIF 和实测记录，见 [PR !5](https://gitee.com/yunxiangluo/ROS2_RISCV/pulls/5)。
- 课程目录与镜像维护：
	- 在课程仓库新增 K3 Pico-ITX 和 CoM260 Kit 的板卡课程目录，统一维护章节、教案、实验、编程语言及运行环境，见 [PR #1](https://github.com/DuoQilai/ROS2_RISCV/pull/1)。
	- 补充 `course_support` 目录下的板卡课程清单，保留 K3 Pico-ITX 第一章入口，并将 CoM260 Kit 的 RISC-V／x86 教案及实验入口补齐至第六章，见 [PR !5](https://gitee.com/yunxiangluo/ROS2_RISCV/pulls/5)。
	- 改进 Gitee 到 GitHub 的课程镜像同步，保留 GitHub 侧课程目录，并补充冲突、拉取失败及并发更新场景的验证，见 [PR #2](https://github.com/DuoQilai/ROS2_RISCV/pull/2)。

## RISC-V Linux 系统与开发板实践课程

- 项目仓库：[DuoQilai/ruyi-riscv-linux-book](https://github.com/DuoQilai/ruyi-riscv-linux-book)
- 第五章“网络与 MQTT”：将实验细化为命令解析、虚拟灯命令环及真实 GPIO／MQTT 远程控灯三个递进环节，补充实机接线、命令与状态联调、非法命令拒绝及板端 tcpdump 抓包证据，见 [PR #8](https://github.com/DuoQilai/ruyi-riscv-linux-book/pull/8)。
- 第六章“线程与协同”：新增成对快照加锁练习，完善 race-demo、snapshot-lock 与 tri-thread 的递进实验；修正并发控制、MQTT 载荷匹配与连接／收发错误处理，补充线程创建和 GPIO 初始化失败检查；完善加锁重编命令、竞态复现、ThreadSanitizer、加锁对照及三线程协同的板端截图、录屏和实物动作录像，见 [PR #9](https://github.com/DuoQilai/ruyi-riscv-linux-book/pull/9)。
- 综合项目：补充 K3 端侧 Agent 与荔枝派的 MQTT 联调工具、部署说明和实物演示，提供状态查询、风扇及 LED 控制接口，整理 Qwen2.5-1.5B Q4_0 本地推理与云端模型调用的运行材料；完善阈值参数格式、上下限关系及板端状态读回校验，明确本轮温湿度为模拟数据、风扇及 LED 为真实 GPIO 控制，见 [PR #11](https://github.com/DuoQilai/ruyi-riscv-linux-book/pull/11)。

## 其他

- 开发板测试素材：新增 EBC7702 的 2 张、SG2044 EVB 的 1 张测试环境照片，整理 VisionFive 2 Lite 与 K510 已有照片的命名和引用，并更新测试总表中的录制材料说明，见 [PR #5](https://github.com/DuoQilai/asciinema/pull/5)。
- RuyiSDK 双周报材料：
	- 补充第 75 期支持矩阵和开发板文档进展，见 [PR #327](https://github.com/ruyisdk/wechat-articles/pull/327)。
	- 补充第 76 期开发板系统测试、ROS 2 课程入口和移动端显示改进，见 [PR #342](https://github.com/ruyisdk/wechat-articles/pull/342)。
	- 补充第 77 期系统测试报告、P550／CoM260 Kit 示例和课程导航进展，见 [PR #356](https://github.com/ruyisdk/wechat-articles/pull/356)。
