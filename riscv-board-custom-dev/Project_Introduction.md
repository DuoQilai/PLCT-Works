# 项目介绍

## 0.常用链接

- 会议室： [#腾讯会议：573-6340-5422](https://meeting.tencent.com/dm/rT2cne6IsIew)
- [新人指引](https://github.com/DuoQilai/PLCT-Works/blob/main/RISC-V_short_video/baby_book.md)
- [RuyiSDK官网](https://ruyisdk.org/docs/intro/)
- [RuyiSDK 示例库扩充调研报告](https://github.com/DuoQilai/PLCT-Works/blob/main/riscv-board-custom-dev/Research_Document/Research_sample_lib.md)
- [RISC-V 开发板与操作系统支持矩阵贡献指南](https://github.com/ruyisdk/support-matrix/blob/main/CONTRIBUTING_zh.md)
- [产出备份仓库](https://github.com/DuoQilai/ruyisdk-dev-archive/blob/main/README.md)
- [支持矩阵目前提交的仓库](https://github.com/DuoQilai/support-matrix)
- [原支持矩阵（我们后期直接维护这个仓库）](https://github.com/ruyisdk/support-matrix)
- [支持矩阵前端网页](https://matrix.ruyisdk.org/)
## 1.基本信息

### 开发板资源缺口梳理 
在你负责或接触的开发板验证过程中，请重点关注：
RuyiSDK 当前尚未集成、但开发板实际开发中确实需要的资源  （除镜像外，如：工具链、厂商定制工具、模拟器、厂商 SDK、厂商 Demo等）这些资源暂时无法依赖厂商主动补充、需要我们先行整理与登记的内容

请先自行收集这些缺口资源记录成文档或表格，作为后续补充 package-index 的依据。

### 文档与产出统一备份规范
从2月产出开始，所有提交到个人仓库的（测试文档、调研文档、视频、技术分享slides等所有产出），需要在[备份仓库](https://github.com/DuoQilai/ruyisdk-dev-archive/blob/main/README.md)同步备份一份，同时周报、月报中的所有链接使用备份仓库的链接

2月的月报更新本周内完成，后续每月同步提交。

### Ruyi 示例库扩充：文档+代码同时提交
示例文档全部以用户手册模式，每步需要文字描述+运行结果图片+视频（最好有，可选），同时提交 Demo 代码到[仓库](https://github.com/DuoQilai/riscv-board-custom-dev)。（暂无设备验证的文档不做图片要求，在文档上备注下）之前已经提交过示例文档的同学补充提交代码文件。

### 支持矩阵测试文档

每人至少负责 1 块开发板，为所负责的开发板维护支持矩阵测试文档。
比如 RevyOS LPi4A 版本测试报告，20250930 版本旧了，直接原地覆盖原文件提交

#### 目前要求：

1. 根据[RISC-V 开发板与操作系统支持矩阵贡献指南](https://github.com/ruyisdk/support-matrix/blob/main/CONTRIBUTING_zh.md)，暂时提交到[我fork的仓库](https://github.com/DuoQilai/support-matrix)
2. 按周持续更新（每周至少一次有内容变化）
- 开发板安排：Licheepi4A @边芷瑶  、Duo256 @崔啟运 、Mars @费翔 、DuoS @郑航 （开发板的安排可以商量，后续也会更改新的开发板～）

## 2.项目方案

- [RISC-V教学内容及短视频吸引因素-CSDN博客](https://blog.csdn.net/jtwqwq/article/details/139909781?app_version=6.3.8&code=app_1562916241&csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22139909781%22%2C%22source%22%3A%22jtwqwq%22%7D&uLinkId=usr1mkqgl919blen&utm_source=app)
- [RISC-V教学短视频同类视频调研报告-CSDN博客](https://blog.csdn.net/jtwqwq/article/details/139909796?app_version=6.3.8&code=app_1562916241&csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22139909796%22%2C%22source%22%3A%22jtwqwq%22%7D&uLinkId=usr1mkqgl919blen&utm_source=app)
- [懂点儿RV-RISC-V短视频教学系列项目方案](https://github.com/DuoQilai/PLCT-Works/blob/main/RISC-V_short_video/Project_proposal.md)
- [视频流量调研](https://github.com/DuoQilai/PLCT-Works/blob/main/RISC-V_short_video/Research_Document/video_ResearchDocument.md)
- [开发板demo教学系列项目方案](https://github.com/DuoQilai/PLCT-Works/blob/main/RISC-V_short_video/Project_proposal_bestpractice.md)
- [二进制翻译教学系列](https://github.com/DuoQilai/PLCT-Works/blob/main/RISC-V_short_video/Project_proposal_box64.md)
- 已下架：[YOLO实战教程：王者荣耀目标识别](https://github.com/DuoQilai/PLCT-Works/blob/main/RISC-V_short_video/Project_proposal_yolo11.md)
- [YOLO实战教程：车牌目标识别](https://github.com/DuoQilai/PLCT-Works/blob/main/RISC-V_short_video/Project_proposal_yolo11_new.md)

## 3.团队协作

- [工作守则速查](https://github.com/lazyparser/survival-manual-for-interns/edit/master/rules.rst)
- 会议室： [#腾讯会议：573-6340-5422](https://meeting.tencent.com/dm/rT2cne6IsIew)
- 即时通信：微信

### 新人指引

[新人指引](https://github.com/DuoQilai/PLCT-Works/blob/main/RISC-V_short_video/baby_book.md)
### 例会信息

- 例会名称：戊寅小队例会
- 例会形式：腾讯会议
- 例会时间：每周五下午02：00-02：30

## 4.发布列表

todo