# July_Ledger 文件说明

本目录用于整理 7 月相关 RISC-V 开发板的 GCC/LLVM 工具链测试步骤、资料依据和实测状态记录。

| 文件               | 简单描述                                                                                                                            |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `A210.md`        | 知合计算 A210 平台的 RISC-V GCC/LLVM 工具链测试步骤和资料边界说明，重点记录官方资料、烧录准备、`rv64gcv/lp64d` 起始参数以及待实测项。                                          |
| `EBC7700.md`     | ESWIN EBC7700 / EBC77 Series SBC 的 GCC/LLVM 测试用例，包含板端 ISA 依据、RuyiSDK 工具链安装、Hello World 和 CoreMark 测试流程，并记录部分 GCC CoreMark 实测结果。 |
| `EBC7702.md`     | ESWIN EBC7702 Mini-DTX Mainboard 的 GCC/LLVM 测试步骤，整理官方资料、双 die / bootloader 注意事项、板端 ISA 参数和测试边界。                                 |
| `K3_Pico-ITX.md` | SpacemiT K3 Pico-ITX 的调研和测试步骤文档，记录官方 Ubuntu 镜像来源、fastboot / Titantools 烧录路径、启动日志要求和待实测的 GCC/LLVM 流程。                            |
| `P550.md`        | HiFive Premier P550 / HF106 的 GCC/LLVM 工具链测试步骤，包含硬件启动检查、RuyiSDK 安装、GCC 已实测状态以及 LLVM 待测步骤。                                       |
| `SG2044.md`      | SOPHGO SG2044 EVB 的调研和 GCC/LLVM 测试步骤文档，说明官方资料来源、Ubuntu 启动介质准备、`rv64gcv/lp64d` 参数起点和待实测交付条件。                                     |
| `README.md`      | 本文件，汇总说明 `July_Ledger` 目录中各文件的用途。                                                                                               |
### 平台操作系统

| 平台                        | 已确认 / 可推断的操作系统支持                                                                                                                                        |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A210                      | 官方 SDK 快速上手提供 Buildroot 和 Debian 预编译镜像类型；实际镜像 URL、checksum、刷写日志仍待实测记录。                                                                                  |
| K3 Pico-ITX               | 官方 `K3-Ubuntu-Images` 提供 Ubuntu 26.04 预装桌面镜像，支持 fastboot / Titantools 刷写路径。                                                                             |
| SG2044 EVB                | SOPHGO 官方资料包含 SG2044 EVB Ubuntu 镜像安装、BIOS、BSP、Boot Flow 等文档。                                                                                            |
| SpacemiT Vital Stone V100 | 公开资料能证明 V100 平台 Linux 和服务器固件栈已在 FPGA 原型平台上运行和演示；资料显示服务器平台方向支持 BRS、OpenSBI、UEFI(BIOS)、Linux、SMBIOS、ACPI 和 OP-TEE；完整产品规格书、整机手册、系统镜像、BSP 仓库、默认账号密码仍需供应商提供。 |
| EBC7700                   | Ubuntu                                                                                                                                                  |
| EBC7702                   | Ubuntu                                                                                                                                                  |
| P550                      | Ubuntu                                                                                                                                                  |

