# Month28

戊寅小队本月工作

## RuyiSDK 7月台账

- Fork [trdthg/asciinema](https://github.com/trdthg/asciinema)，并在自己的 Fork 仓库 [DuoQilai/asciinema](https://github.com/DuoQilai/asciinema) 中，基于其中的 `asciinema expect` 功能编写 RISC-V 开发板 GCC/LLVM 工具链测试脚本，并录制测试过程。
- 测试用例文档：
	- [board-compiler-test-cases.md](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md)
	- [10种开发板+编译器测试用例.docx](https://github.com/DuoQilai/asciinema/blob/develop/202607/10%E7%A7%8D%E5%BC%80%E5%8F%91%E6%9D%BF%2B%E7%BC%96%E8%AF%91%E5%99%A8%E6%B5%8B%E8%AF%95%E7%94%A8%E4%BE%8B.docx)

- 测试流程和结果整理：
	- 测试说明：[202607/README.md](https://github.com/DuoQilai/asciinema/blob/develop/202607/README.md)
	- 测试用例：[board-compiler-test-cases.md](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md)
	- 测试脚本：[examples/](https://github.com/DuoQilai/asciinema/tree/develop/examples)
	- 测试截图和视频录制：[board-compiler-test-cases_media/](https://github.com/DuoQilai/asciinema/tree/develop/202607/board-compiler-test-cases_media)

- ESWIN EBC7700：
	- 测试用例：[GCC和LLVM对EBC7700的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L34)
	- 测试脚本：[01-ebc7700.sh](https://github.com/DuoQilai/asciinema/blob/develop/examples/01-ebc7700.sh)
	- 测试截图和视频录制：[测试素材](https://github.com/DuoQilai/asciinema/tree/develop/202607/board-compiler-test-cases_media/1.ebc7700)

- HiFive Premier P550：
	- 测试用例：[GCC和LLVM对SiFive HiFive Premier P550的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L63)
	- 测试脚本：[02-p550.sh](https://github.com/DuoQilai/asciinema/blob/develop/examples/02-p550.sh)
	- 测试截图和视频录制：[测试素材](https://github.com/DuoQilai/asciinema/tree/develop/202607/board-compiler-test-cases_media/2.p550)

- ESWIN EBC7702：
	- 测试用例：[GCC和LLVM对ESWIN EBC7702的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L92)
	- 测试脚本：[03-ebc7702.sh](https://github.com/DuoQilai/asciinema/blob/develop/examples/03-ebc7702.sh)
	- 测试截图和视频录制：[测试素材](https://github.com/DuoQilai/asciinema/tree/develop/202607/board-compiler-test-cases_media/3.ebc7702)

- SG2044 EVB：
	- 测试用例：[GCC和LLVM对SG2044的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L122)
	- 测试脚本：[04-sg2044.sh](https://github.com/DuoQilai/asciinema/blob/develop/examples/04-sg2044.sh)
	- 测试截图和视频录制：[测试素材](https://github.com/DuoQilai/asciinema/tree/develop/202607/board-compiler-test-cases_media/4.Sg2044)

- A210 SODIMM V2：
	- 测试用例：[GCC和LLVM对A210 SODIMM V2的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L151)
	- 测试脚本：[05-a210-v2.sh](https://github.com/DuoQilai/asciinema/blob/develop/examples/05-a210-v2.sh)
	- 测试截图和视频录制：[测试素材](https://github.com/DuoQilai/asciinema/tree/develop/202607/board-compiler-test-cases_media/5.a210-v2)

- VisionFive 2 Lite：
	- 测试用例：[GCC和LLVM对VisionFive 2 Lite的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L180)
	- 测试脚本：[06-vf2-lite.sh](https://github.com/DuoQilai/asciinema/blob/develop/examples/06-vf2-lite.sh)
	- 测试截图和视频录制：[测试素材](https://github.com/DuoQilai/asciinema/tree/develop/202607/board-compiler-test-cases_media/6.VisionFive2Lite)

- Canaan K510 CRB-V1.2 KIT：
	- 测试用例：[GCC和LLVM对Canaan K510 CRB-V1.2 KIT的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L209)
	- 测试脚本：[07-k510.sh](https://github.com/DuoQilai/asciinema/blob/develop/examples/07-k510.sh)
	- 测试截图和视频录制：[测试素材](https://github.com/DuoQilai/asciinema/tree/develop/202607/board-compiler-test-cases_media/7.K510)

- Milk-V Megrez：
	- 测试用例：[GCC和LLVM对Milk-V Megrez的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L248)
	- 测试脚本：[08-megrez.sh](https://github.com/DuoQilai/asciinema/blob/develop/examples/08-megrez.sh)
	- 测试截图和视频录制：[测试素材](https://github.com/DuoQilai/asciinema/tree/develop/202607/board-compiler-test-cases_media/8.Megrez)

- RISC-V Book（如意笔记本甲辰版）：
	- 测试用例：[GCC和LLVM对RISC-V Book（如意笔记本甲辰版）的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L277)
	- 测试脚本：[09-rvbook.sh](https://github.com/DuoQilai/asciinema/blob/develop/examples/09-rvbook.sh)
	- 测试截图和视频录制：[测试素材](https://github.com/DuoQilai/asciinema/tree/develop/202607/board-compiler-test-cases_media/9.ruyibook)

- RISC-V Book 2（如意二代笔记本）：
	- 测试用例：[GCC和LLVM对RISC-V Book 2（如意二代笔记本）的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L306)
	- 测试脚本：[10-rvbook2.sh](https://github.com/DuoQilai/asciinema/blob/develop/examples/10-rvbook2.sh)
	- 测试截图和视频录制：[测试素材](https://github.com/DuoQilai/asciinema/tree/develop/202607/board-compiler-test-cases_media/10.rvbook2)

- SpacemiT K3 Pico-ITX：
	- 测试用例：[GCC和LLVM对SpacemiT K3 Pico-ITX的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L335)
	- 测试脚本：[11-k3.sh](https://github.com/DuoQilai/asciinema/blob/develop/examples/11-k3.sh)

- Milk-V Jupiter2 Dev Kit：
	- 测试用例：[GCC和LLVM对Milk-V Jupiter2 Dev Kit的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L385)

- K3 CoM260 Kit 16G：
	- 测试用例：[GCC和LLVM对K3 CoM260 Kit 16G的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L414)

- K3 Pico-ITX 32G：
	- 测试用例：[GCC和LLVM对K3 Pico-ITX 32G的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L443)

## Ruyi 示例文档库

- 仓库：[ruyisdk/board-docs](https://github.com/ruyisdk/board-docs)
- 开发板示例文档扩充
	- VisionFive 2 Lite
		- [RuyiSDK 外设示例：基础按键检测](https://github.com/ruyisdk/board-docs/blob/add-documents-K510-VF2Lite/VisionFive2Lite/Button/README_zh.md)
	- Canaan K510-CRB-V1.2 KIT
		- [RuyiSDK 外设示例：通信测试](https://github.com/ruyisdk/board-docs/blob/add-documents-K510-VF2Lite/K510/UART/README.md)
	- Milk-V Jupiter2
		- 概述：[README.md](https://github.com/ruyisdk/board-docs/blob/main/Jupiter2/README.md)；[README_zh.md](https://github.com/ruyisdk/board-docs/blob/main/Jupiter2/README_zh.md)
		- [RuyiSDK 基础示例：HelloWorld](https://github.com/ruyisdk/board-docs/blob/main/Jupiter2/HelloWorld/README_zh.md)
		- [RuyiSDK 基础示例：Coremark](https://github.com/ruyisdk/board-docs/blob/main/Jupiter2/Coremark/README_zh.md)
- board-docs-frontend：
	- 在线站点：[board-docs-frontend](https://board-docs-frontend.pages.dev/)
	- Commit：[fix(ci): replace git submodule update --remote with explicit fetch/checkout](https://github.com/DuoQilai/board-docs-frontend/commit/3295c3f)
	- Commit：[docs: remove dev setup and manual trigger, keep essentials](https://github.com/DuoQilai/board-docs-frontend/commit/38a8fc9)

- 仓库维护：
	- 仓库配置：
		- [.gitignore](https://github.com/ruyisdk/board-docs/blob/main/.gitignore)
	- 贡献规范：
		- [CONTRIBUTING.md](https://github.com/ruyisdk/board-docs/blob/ospp-readiness/CONTRIBUTING.md)
		- [CONTRIBUTING_zh.md](https://github.com/ruyisdk/board-docs/blob/ospp-readiness/CONTRIBUTING_zh.md)
	- GitHub 模板：
		- [.github/ISSUE_TEMPLATE/content-bug.yml](https://github.com/ruyisdk/board-docs/blob/ospp-readiness/.github/ISSUE_TEMPLATE/content-bug.yml)
		- [.github/ISSUE_TEMPLATE/content-new.yml](https://github.com/ruyisdk/board-docs/blob/ospp-readiness/.github/ISSUE_TEMPLATE/content-new.yml)
		- [.github/ISSUE_TEMPLATE/content-outdated.yml](https://github.com/ruyisdk/board-docs/blob/ospp-readiness/.github/ISSUE_TEMPLATE/content-outdated.yml)
		- [.github/PULL_REQUEST_TEMPLATE.md](https://github.com/ruyisdk/board-docs/blob/ospp-readiness/.github/PULL_REQUEST_TEMPLATE.md)
	- 文档模板更新：
		- [templates/](https://github.com/ruyisdk/board-docs/blob/ospp-readiness/templates/%5Bboard-name%5D/%5Bexample-name%5D/README_zh.md)

## RuyiSDK Support Matrix

- 操作系统支持报告更新：
	- Update Premier P550 Ubuntu 24.04.3 LTS report.
	- Add EBC7702 Ubuntu 24.04.4 LTS report.
	- Update LicheePi4A RevyOS test report to 20251226.
	- PR：[ruyisdk/support-matrix#389](https://github.com/ruyisdk/support-matrix/pull/389)


## 英麒 RISC-V Lab

- 测试用例：[GCC和LLVM对EBC7700的支持测试](https://github.com/DuoQilai/asciinema/blob/develop/202607/board-compiler-test-cases.md#L34)
- 实习总结：[SitongZhang](https://github.com/DuoQilai/ruyisdk-dev-archive/tree/main/reports/SitongZhang)

## RISC-V Linux 系统与开发板实践课程

- ruyi-riscv-linux-book：
	- 在线预览：[ruyi-riscv-linux-book](https://enzoding-rgb.github.io/ruyi-riscv-book/)
	- [CourseOutline.html](https://enzoding-rgb.github.io/ruyi-riscv-book/CourseOutline.html)
	- [intro.md](https://enzoding-rgb.github.io/ruyi-riscv-book/intro.md)
	- [course-evaluation-standard.md](https://enzoding-rgb.github.io/ruyi-riscv-book/course-evaluation-standard.md)
	- [misc/boards/riscv-ai-boards-2025-2026.md](https://github.com/DuoQilai/ruyi-riscv-linux-book/blob/enzo/misc/boards/riscv-ai-boards-2025-2026.md)
	- [chapters/ch03/lab.html](https://enzoding-rgb.github.io/ruyi-riscv-book/chapters/ch03/lab.html)
	- Commit：[docs: ship ch01–ch06 lecture/lab pages and scaffolds](https://github.com/DuoQilai/ruyi-riscv-linux-book/commit/2a8e65f)
	- Commit：[docs: add course evaluation standard (CIPP+OBE fused)](https://github.com/DuoQilai/ruyi-riscv-linux-book/commit/3c4694c)
	- Commit：[ch03: zero-to-assembly temp-fan lab + LPi4A gpiochip1 pin defaults](https://github.com/DuoQilai/ruyi-riscv-linux-book/commit/a157f5e)
