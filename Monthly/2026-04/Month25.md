# Month25

戊寅小队本月工作

## RuyiSDK
-  RuyiSDK 示例库文档展示的前端页面
	- 前端仓库： [https://github.com/DuoQilai/board-docs-frontend.git](https://github.com/DuoQilai/board-docs-frontend.git)
	- 前端仓库内容包括：
		- 完成了 2 轮迭代，现已支持BPI-F3、Duo、Duo_256m、Duo_S、Meles、Pioneer、LicheePi3A、LicheePi4A等开发板。
		- 前端网页代码完成了给 VS Code 和 Eclipse 插件团队的消息发送。
		- 针对团队提出的新需求做了 patch。
		- 更新并拉取前端文档仓库和 README。
		- 根据插件侧需求，完善了“仅在 VS Code WebView / Eclipse 内生效”的前端交互：
	    - 通过 userAgent 判断 VS Code（包含 `Code/`）来控制按钮显隐；浏览器环境不展示；Eclipse/VS Code 外也不展示。
	    - 在页面右上角增加按钮「在 VS Code 中使用」；点击后调用 `vscode.postMessage({ type: 'copilot', url, model, profile })` 把当前文档原文 URL 与（从文档属性读取的）开发板型号/示例名称回传给 VS Code。
		- 按要求将网站文档仓库切到 `ruyisdk/board-docs`，并处理目录展示（不显示 `/templates`，用于后续新增模板目录）。
		- 跟进 UI 细节：标签图标替换为 ruyisdk logo。
		- 学习 Electron 桌面开发与 VS Code 插件开发的基本逻辑，更好地理解对方团队需求并协作对齐。
	-  网站连接： https://board-docs-frontend.pages.dev/
	-  文档仓库： https://github.com/ruyisdk/board-docs/

- 开发板示例文档扩充
	- Licheepi4A 
		- cpufetch
			- 视频链接：[【RuyiSDK示例】使用Ruyi工具链编译cpufetch](https://www.bilibili.com/video/BV1fiw7zBE6F?buvid=Y14C16117DC47F7240DFA9AB49C606069273&is_story_h5=false&mid=7O7lEOQTno7ebx%2FEwA0C1w%3D%3D&plat_id=116&share_from=ugc&share_medium=iphone&share_plat=ios&share_session_id=821B26EC-6E57-4DE1-AD38-1154FCC458E7&share_source=COPY&share_tag=s_i&spmid=united.player-video-detail.0.0&timestamp=1773655425&unique_k=xB64uZq&up_id=179700748)
			- 视频链接：[【RISC-V架构识别】在Licheepi4A上使用cpufetch获取CPU信息](https://www.bilibili.com/video/BV1j8wFzSE2x?vd_source=63f9297bce04de7108868464326f7b22)
	- [使用 Ruyi 工具链在 LicheePi 4A 上编译并运行GStreamer](https://github.com/zhiyao310/ruyisdk-dev-archive/blob/main/examples/GStreamer_LPi4A.md)
	- [RuyiSDK 计算机视觉示例__LicheePi 4A OpenCV](https://github.com/zhiyao310/board-docs/blob/main/LicheePi4A/OpenCV/README_zh.md)
	- VisionFive2Lite
		- 概述： [README.md](https://github.com/zhiyao310/board-docs/tree/main/VisionFive2Lite);[README_zh.md](https://github.com/zhiyao310/board-docs/blob/main/VisionFive2Lite/README_zh.md)
		- [HelloWorld](https://github.com/zhiyao310/board-docs/blob/main/VisionFive2Lite/HelloWorld/README_zh.md)
		- [Coremark](https://github.com/zhiyao310/board-docs/blob/main/VisionFive2Lite/Coremark/README_zh.md)
	- Duo256
		- [使用 RuyiSDK 在 Milk-V Duo256m 上编译运行 mailbox-test 教程](https://github.com/cuiqiyun/ruyisdk-dev-archive/blob/main/examples/%E4%BD%BF%E7%94%A8%20RuyiSDK%20%E5%9C%A8%20Milk-V%20Duo256m%20%E4%B8%8A%E7%BC%96%E8%AF%91%E8%BF%90%E8%A1%8C%20mailbox-test%20%E6%95%99%E7%A8%8B.md)
		- [使用 RuyiSDK 在 Milk-V Duo256m 上编译运行 opencv-mobile 教程](https://github.com/cuiqiyun/outcome_list_cqy/blob/main/Duo%20256m/%E4%BD%BF%E7%94%A8%20RuyiSDK%20%E5%9C%A8%20Milk-V%20Duo256M%20%E4%B8%8A%E7%BC%96%E8%AF%91%E8%BF%90%E8%A1%8C%20opencv-mobile%20%E6%95%99%E7%A8%8B.md)
	- DuoS 
		- [Mailbox-test](https://github.com/ruyisdk/board-docs/tree/main/Duo_S/Mailbox-test)
		- [Blink](https://github.com/ruyisdk/board-docs/tree/main/Duo_S/Blink)
		- [Dht22](https://github.com/ruyisdk/board-docs/tree/main/Duo_S/Dht22)
		- [ADC](https://github.com/ruyisdk/board-docs/tree/main/Duo_S/ADC)
	- Mars
		- [Milk-V Mars_2048](https://github.com/feifei-xx/riscv-board-custom-dev/blob/main/Mars/Milk-V%20Mars_2048.md)
		- [Milk-V Mars_Coremark](https://github.com/feifei-xx/ruyisdk-dev-archive/blob/main/examples/CoreMark/Milk-V%20Mars_CoreMark.md)
- RuyiSDK开发资源梳理和资源申请
	- [Go Toolchain](https://github.com/ruyisdk/ruyisdk/issues/80)
## 英麒RISC-V Lab
Licheepi4A示例文档：
- [YOLOX](https://github.com/ruyisdk/board-docs/blob/main/LicheePi4A/YOLOX/README_zh.md)
- [MobilenetV2](https://github.com/ruyisdk/board-docs/tree/main/LicheePi4A/MobilenetV2)
- [YOLOV5n](https://github.com/ruyisdk/board-docs/tree/main/LicheePi4A/YOLOV5n)

## 2026欧洲峰会
- 扩展摘要中稿
	- From Fragmentation to Systematization: A Standardized Quality Selection and Reconstruction Approach for RISC-V Courses Sub.  # C3QQBZ. Fuyuan Zhang and Yunxiang Luo.