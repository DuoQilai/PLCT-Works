# RISC-V GCC/LLVM 工具链测试步骤：SpacemiT K3 Pico-ITX

## 1. 当前结论和状态

结论先行：K3 目录按 SpacemiT 官方开发套件 `K3 Pico-ITX` 调研。官方页面能证明开发套件入口存在，`spacemit-com/K3-Ubuntu-Images` 已提供 K3 Ubuntu 26.04 预装镜像、MD5 和刷机路径；交付状态汇总将其列为 P3 待实测平台。当前仍缺少本地 PDF、实际刷写启动记录、板端登录记录和 Hello World / CoreMark 实测证据，不能判定通过。

| 项目 | 状态 | 说明 |
|---|---|---|
| 开发板名称 | 资料存在 | 官网开发套件页显示为 `K3 Pico-ITX` |
| SoC | 资料存在 | SpacemiT K3 |
| CPU / IP 核 | 资料存在 | K3 / X100 路线；X100 官方资料用于 ISA 方向参考，实际核心数和 ISA 以板端输出为准 |
| 系统镜像 | 资料存在，待验证 | `K3-Ubuntu-Images` release `20260530` 提供 Ubuntu 26.04 预装桌面镜像、MD5、fastboot 和 Titantools 刷机路径；仍需实际下载校验和板端启动 |
| RuyiSDK 工具链 | 待验证 | 按项目统一流程使用 `gnu-plct` 和 `llvm-plct` |
| GCC Hello World | 待验证 | 本文提供步骤，未实测 |
| LLVM Hello World | 待验证 | 本文提供步骤，未实测 |
| GCC CoreMark | 待验证 | 起始参数 `rv64gcv/lp64d`，完整扩展以板端 ISA 为准 |
| LLVM CoreMark | 待验证 | 起始参数 `rv64gcv/lp64d`，完整扩展以板端 ISA 为准 |
| 交付判断 | 资料存在，待验证，当前不适合直接交付 | 需要补充实体板卡、镜像下载校验、刷写启动、版本输出、板端运行和 CoreMark 分数 |

## 2. 资料依据和测试边界

SpacemiT 官方开发套件页面列出 `K3 Pico-ITX`，前端详情配置中的产品 ID 为 `k3-pico-itx`，官方文档路径为 `hardware/eco/k3_pico/root_overview.md`。

SpacemiT GitHub 组织仓库 `K3-Ubuntu-Images` 明确面向 K3 Pico-ITX 提供 UEFI 启动的 Ubuntu RISC-V 预装镜像。latest release 为 tag `20260530` / `2026.05.30`，说明为 SpacemiT K3 的 Ubuntu 26.04 预装桌面镜像，支持板卡包含 `Pico-ITX` 和 `COM260`。release 同时给出 fastboot 使用的 `img.zst`、Titantools GUI 使用的 `tar.gz`、对应 MD5、首次登录默认账号 `ubuntu/ubuntu`，以及升级 `edk2-spacemit`、`spacemit-ec-firmware` 的后续命令。

公开报道和 SpacemiT X100 官方页可作为 K3 / X100 路线背景资料，但它们不能替代 K3 Pico-ITX 开发板级资料。本文只覆盖通用 Linux 用户态 C/C++ 编译运行，不覆盖 NPU、AI SDK、图形、多媒体、服务器虚拟化或安全扩展专项测试。

测试边界：

- 默认测试对象为 `K3 Pico-ITX` 实体开发套件。
- 如果实际拿到的板卡不是 K3 Pico-ITX，而是 K3 CoM260、Jupiter 2 NX、Sipeed K3 或其他 K3 生态板，应另建或改名测试步骤，不直接复用本结论。
- 使用 `K3-Ubuntu-Images` 时，必须记录 release tag、镜像文件名、MD5 校验结果、刷机方式和首次登录方式。
- `K3-Ubuntu-Images` 的镜像和 MD5 证明官方镜像资料存在；只有实际下载校验、刷写、启动和登录日志才能作为交付证据。
- Hello World 不强制打开全部扩展。
- CoreMark 必须记录 `-march/-mabi`，并保存实际运行输出和分数。
- K3 的 AI/NPU、BF16、向量宽度等资料不能替代 CoreMark 板端运行证据。
- QEMU 只能预验证通用 RISC-V Linux 用户态脚本；不建议直接把 K3 官方整机镜像当作 QEMU 可启动镜像，QEMU 不能覆盖 K3 UEFI、EC 固件、fastboot、图形/NPU/多媒体外设，也不能作为 K3 交付实测。

## 3. 扩展参数依据

K3 / X100 公开资料可作为向量能力方向线索，因此首次 CoreMark 可尝试：

```text
-march=rv64gcv -mabi=lp64d
```

到货后必须根据板端信息修订：

```bash
uname -a
cat /etc/os-release
lscpu
cat /proc/cpuinfo
```

工具链支持检查：

```bash
riscv64-plct-linux-gnu-gcc --target-help | grep -A80 "Known valid arguments for -mcpu" || true
riscv64-plct-linux-gnu-gcc -mcpu=help || true
clang --target=riscv64-linux-gnu --print-supported-cpus || true
```

参数选择原则：

| 情况 | 参数 |
|---|---|
| 板端 ISA 和工具链均支持向量 | `-march=rv64gcv -mabi=lp64d` |
| 板端列出更多用户态 Z 扩展，工具链接受 | 在 `rv64gcv` 后追加经确认的扩展 |
| 向量参数编译失败 | 回退 `-march=rv64gc -mabi=lp64d` |
| 工具链支持明确 K3/X100 的 `-mcpu` | 可试用 `-mcpu=<confirmed-name>`，但必须记录支持证据 |

不要在缺少板端 ISA 的情况下直接把公开资料中的 RVA23、虚拟化、加密、AI 能力展开成超长 `-march`。

## 4. 启动准备和烧录日志要求

镜像下载和校验：

| 烧录方式 | 官方 release 文件 | 校验要求 |
|---|---|---|
| fastboot 命令行 | `ubuntu-26.04-preinstalled-desktop-riscv64.img.zst` | 下载同目录 `.md5`，本地执行 `md5sum ubuntu-26.04-preinstalled-desktop-riscv64.img.zst` 并和官方 MD5 对比 |
| Titantools 图形界面 | `ubuntu-26.04-preinstalled-desktop-riscv64.tar.gz` | 下载同目录 `.md5`，本地执行 `md5sum ubuntu-26.04-preinstalled-desktop-riscv64.tar.gz` 并和官方 MD5 对比 |

```bash
md5sum ubuntu-26.04-preinstalled-desktop-riscv64.img.zst
cat ubuntu-26.04-preinstalled-desktop-riscv64.img.zst.md5
```

fastboot 路径按官方 README.zh.rst 记录：

1. 将 K3 Pico-ITX 切换到刷机模式。日志中必须写明 FDL / Download 键、上电、USB 数据线连接顺序；如果实际板卡按键命名不同，要拍照或文字说明。
2. 在 Ubuntu 22.04 或更新版本主机安装依赖并克隆官方仓库：

```bash
sudo apt-get update
sudo apt-get install git ubuntu-dev-tools fastboot
git clone https://github.com/spacemit-com/K3-Ubuntu-Images.git gadget
cd gadget
```

3. 一键刷机并保存完整日志：

```bash
make IMG=/path/to/ubuntu-26.04-preinstalled-desktop-riscv64.img.zst all
```

4. 如需手动排查，官方 README.zh.rst 给出的流程是：先将 `.img.zst` 解压得到 `.img`，再用 `image_flash.py` 从镜像提取分区文件到 `./temp`，把从 PPA 获取的 `u-boot.itb` 放入 `./temp/u-boot.itb`，再执行 fastboot 烧写。测试日志中必须说明是否使用了一键流程还是手动流程。

```bash
unzstd /path/to/ubuntu-26.04-preinstalled-desktop-riscv64.img.zst
python3 image_flash.py \
    --img /path/to/ubuntu-26.04-preinstalled-desktop-riscv64.img \
    --partition partition_universal.json
cp /path/to/u-boot.itb temp/u-boot.itb
sudo python3 image_flash.py --fastboot fastboot.yaml
```

Titantools 路径按官方 README.zh.rst 记录：

1. 安装 SpacemiT Titantools（Windows 安装包或 Linux AppImage），记录版本和下载来源。
2. 将开发板切换至刷机模式：按住 FDL / Download 键的同时接通电，再插入 USB 数据线。
3. 打开 Titantools，进入“研发工具 -> 单机烧录”。
4. 点击“扫描设备”并选中开发板。
5. 选择下载的 `.tar.gz` 或解压后的目录。
6. 点击“开始烧录”，等待烧录完成；保存扫描设备、镜像选择、进度和完成页面截图。

首次启动和登录：

```text
默认账号：ubuntu
默认密码：ubuntu
```

官方 release 说明首次登录会要求修改密码。测试报告只记录“已按交付策略修改密码”，不要保存长期密码明文。首次登录后按 release note 执行固件/系统更新，并保存输出；其中 `spacemit-ec-firmware` 官方说明可能导致系统关机，因此应单独放在最后执行，并记录是否自动关机、是否可再次启动。

```bash
echo yes | sudo tee /etc/flash-kernel/ignore-efi
sudo apt-get update
sudo apt-get install edk2-spacemit
sudo apt-get full-upgrade
sudo apt-get install spacemit-ec-firmware
```

启动链证据可按官方 README.zh.rst 记录为：

```text
BootROM -> FSBL(U-Boot SPL) -> OpenSBI -> EDK2 UEFI -> GRUB -> Linux
```

日志中只要能确认刷写完成、首次启动、登录、改密和系统信息，才可进入 GCC/LLVM 测试；如果只完成镜像下载或 MD5 校验，状态仍是“资料存在，待验证”。

## 5. 测试用例

| 测试用例标识 | K3-1 |
|---|---|
| 测试用例名称 | GCC 和 LLVM 对 SpacemiT K3 Pico-ITX 开发套件的支持测试 |
| 测试说明 | 验证 K3 Pico-ITX Linux 环境中 RuyiSDK 管理的 GCC/LLVM 工具链能否完成 Hello World 和 CoreMark 编译、板端运行和结果记录 |
| 测试用例初始化 | 准备 K3 Pico-ITX 开发套件、串口或 SSH 登录方式、`K3-Ubuntu-Images` Ubuntu 26.04 镜像、MD5 校验文件、刷机工具、网络连接和账号信息 |
| 前提与约束 | 系统已启动到 64 位 Linux；以下步骤默认板端原生执行；如改为交叉编译，必须记录 sysroot 来源、传输方式和板端运行命令 |
| 终止条件 | GCC/LLVM 版本可记录；GCC/LLVM Hello World 均输出 `Hello, World!`；GCC/LLVM CoreMark 均输出校验通过信息、`Iterations/Sec` 和最终分数 |

| 序号 | 输入及操作说明 | 期望测试结果 |
|---|---|---|
| 1 | 记录板卡和镜像信息。记录板卡名称必须写 `K3 Pico-ITX`。优先记录 `K3-Ubuntu-Images` release `20260530`，镜像文件名、下载地址、MD5 地址、刷机方式和启动介质。fastboot 路径对应 `ubuntu-26.04-preinstalled-desktop-riscv64.img.zst`；Titantools GUI 路径对应 `ubuntu-26.04-preinstalled-desktop-riscv64.tar.gz`。 | 板卡和系统镜像来源清楚；如果实际型号不是 K3 Pico-ITX，不得继续按本用例判定。 |
| 2 | 按第 4 节下载并校验镜像，选择 fastboot 或 Titantools 完成刷写后首次登录。fastboot 路径保存 `make IMG=... all` 或手动 `image_flash.py` 输出；Titantools 路径保存扫描设备、选择 `.tar.gz`、开始烧录、烧录完成截图。首次登录默认账号按 release 记录为 `ubuntu/ubuntu`，首次登录后必须修改密码并执行 release note 中的后续更新命令。 | 镜像 MD5 校验成功；刷写成功；系统可登录；默认账号只作为首次登录资料，不作为长期交付账号；如缺少刷写日志或首次登录日志，状态保持“待验证”。 |
| 3 | 记录系统和 CPU 信息。<br><br>`uname -a`<br>`uname -m`<br>`cat /etc/os-release`<br>`lscpu`<br>`cat /proc/cpuinfo` | 保存核心数、ISA、uarch、系统版本和内核版本。 |
| 4 | 安装依赖。<br><br>`sudo apt update`<br>`sudo apt install -y wget tar zstd xz-utils git build-essential make file ca-certificates` | 依赖安装成功；非 Debian/Ubuntu 系统记录等价命令。 |
| 5 | 安装或验证 RuyiSDK。本期统一使用 RuyiSDK `0.50.0` riscv64 二进制。<br><br>`wget https://mirror.iscas.ac.cn/ruyisdk/ruyi/tags/0.50.0/ruyi-0.50.0.riscv64`<br>`chmod +x ./ruyi-0.50.0.riscv64`<br>`sudo cp -v ./ruyi-0.50.0.riscv64 /usr/local/bin/ruyi`<br><br>验证：<br>`ruyi version` | 记录实际 RuyiSDK 版本；期望输出 `Ruyi 0.50.0`。 |
| 6 | 配置 Ruyi 包索引并安装工具链。<br><br>`ruyi config set repo.remote https://mirror.iscas.ac.cn/git/ruyisdk/packages-index.git`<br>`ruyi config set repo.branch main`<br>`ruyi update`<br>`ruyi install gnu-plct llvm-plct` | `gnu-plct` 和 `llvm-plct` 安装成功，记录实际包版本。 |
| 7 | 创建并激活 GCC 虚拟环境，记录版本。<br><br>`ruyi venv -t toolchain/gnu-plct manual venv-gnu-plct-k3`<br>`. ./venv-gnu-plct-k3/bin/ruyi-activate`<br>`which riscv64-plct-linux-gnu-gcc`<br>`riscv64-plct-linux-gnu-gcc -v` | 保存 GCC 路径和版本输出。 |
| 8 | 编译并运行 Hello World（GCC）。<br><br>`cat > hello.c <<'EOF'`<br>`#include <stdio.h>`<br>`int main(void) {`<br>`    printf("Hello, World!\n");`<br>`    return 0;`<br>`}`<br>`EOF`<br>`riscv64-plct-linux-gnu-gcc hello.c -o hello-gcc`<br>`file hello-gcc`<br>`./hello-gcc` | 板端输出 `Hello, World!`。 |
| 9 | 获取 CoreMark。<br><br>`ruyi extract coremark`<br>`cd coremark-*` | 记录 CoreMark 来源和版本。 |
| 10 | 编译并运行 CoreMark（GCC，向量起始参数）。<br><br>`make SHELL=/bin/bash PORT_DIR=linux64 clean`<br>`make SHELL=/bin/bash PORT_DIR=linux64 CC=riscv64-plct-linux-gnu-gcc XCFLAGS="-O3 -march=rv64gcv -mabi=lp64d" compile`<br>`mv coremark.exe coremark-gcc-k3`<br>`./coremark-gcc-k3` | 输出校验通过和 `Iterations/Sec`。实际分数：待实测填写。 |
| 11 | 如 GCC 向量参数失败，回退到 `rv64gc`。<br><br>`make SHELL=/bin/bash PORT_DIR=linux64 clean`<br>`make SHELL=/bin/bash PORT_DIR=linux64 CC=riscv64-plct-linux-gnu-gcc XCFLAGS="-O3 -march=rv64gc -mabi=lp64d" compile`<br>`mv coremark.exe coremark-gcc-k3-rv64gc`<br>`./coremark-gcc-k3-rv64gc` | 记录失败日志、回退参数、运行输出和分数。 |
| 12 | 退出 GCC 环境。<br><br>`cd ..`<br>`ruyi-deactivate` | 成功退出。 |
| 13 | 创建并激活 LLVM 虚拟环境，记录版本。<br><br>`ruyi venv -t toolchain/llvm-plct manual --sysroot-from gnu-plct venv-llvm-plct-k3`<br>`. ./venv-llvm-plct-k3/bin/ruyi-activate`<br>`which clang`<br>`clang -v` | 保存 LLVM/Clang 路径和版本输出。 |
| 14 | 编译并运行 Hello World（LLVM）。<br><br>`clang --target=riscv64-linux-gnu hello.c -o hello-llvm`<br>`file hello-llvm`<br>`./hello-llvm` | 板端输出 `Hello, World!`。 |
| 15 | 编译并运行 CoreMark（LLVM，向量起始参数）。<br><br>`cd coremark-*`<br>`make SHELL=/bin/bash PORT_DIR=linux64 clean`<br>`make SHELL=/bin/bash PORT_DIR=linux64 CC=clang XCFLAGS="-O3 --target=riscv64-linux-gnu -march=rv64gcv -mabi=lp64d" compile`<br>`mv coremark.exe coremark-llvm-k3`<br>`./coremark-llvm-k3` | 输出校验通过和 `Iterations/Sec`。实际分数：待实测填写。 |
| 16 | 如 LLVM 向量参数失败，回退到 `rv64gc`。<br><br>`make SHELL=/bin/bash PORT_DIR=linux64 clean`<br>`make SHELL=/bin/bash PORT_DIR=linux64 CC=clang XCFLAGS="-O3 --target=riscv64-linux-gnu -march=rv64gc -mabi=lp64d" compile`<br>`mv coremark.exe coremark-llvm-k3-rv64gc`<br>`./coremark-llvm-k3-rv64gc` | 记录失败日志、回退参数、运行输出和分数。 |
| 17 | 退出 LLVM 环境并归档证据。<br><br>`cd ..`<br>`ruyi-deactivate` | 保存系统信息、工具链版本、Hello World 输出、CoreMark 输出和分数。 |

## 6. 实测记录表

| 项目 | 实际记录 |
|---|---|
| 开发板实物型号 | K3 Pico-ITX，待实物版本号和丝印确认 |
| SoC | SpacemiT K3 |
| CPU / IP 核 | K3 / X100 路线，待板端确认 |
| 系统镜像 | `K3-Ubuntu-Images` release `20260530` Ubuntu 26.04 预装桌面镜像；待实际下载、MD5 校验、刷写和启动记录 |
| 启动准备和刷写日志 | 待实测填写：MD5、fastboot/Titantools 路径、刷写完成证据、首次登录改密、固件/系统更新输出 |
| RuyiSDK 版本 | 待实测填写 |
| GCC 工具链来源和版本 | `gnu-plct`，待实测填写 |
| LLVM 工具链来源和版本 | `llvm-plct`，待实测填写 |
| GCC Hello World 编译命令 | `riscv64-plct-linux-gnu-gcc hello.c -o hello-gcc` |
| GCC Hello World 板端运行结果 | 待实测填写 |
| LLVM Hello World 编译命令 | `clang --target=riscv64-linux-gnu hello.c -o hello-llvm` |
| LLVM Hello World 板端运行结果 | 待实测填写 |
| GCC CoreMark 编译命令 | `make SHELL=/bin/bash PORT_DIR=linux64 CC=riscv64-plct-linux-gnu-gcc XCFLAGS="-O3 -march=rv64gcv -mabi=lp64d" compile` |
| GCC CoreMark 运行结果和分数 | 待实测填写，必须包含 `Iterations/Sec` |
| LLVM CoreMark 编译命令 | `make SHELL=/bin/bash PORT_DIR=linux64 CC=clang XCFLAGS="-O3 --target=riscv64-linux-gnu -march=rv64gcv -mabi=lp64d" compile` |
| LLVM CoreMark 运行结果和分数 | 待实测填写，必须包含 `Iterations/Sec` |
| `-march/-mcpu` 来源 | K3 Pico-ITX 官方入口 + SpacemiT X100/RVA23/RVV 1.0 公开资料 + 板端 ISA 待确认；不使用未验证 `-mcpu` |
| 当前状态 | 资料存在，待验证，当前不适合直接交付 |

## 7. 参考资料

- SpacemiT 官网：<https://www.spacemit.com/en/>
- SpacemiT K3 Pico-ITX 官方开发套件页：<https://www.spacemit.com/community/development-kit/k3-pico-itx>
- SpacemiT K3 Pico-ITX 官方文档入口：<https://www.spacemit.com/community/document?lang=en&nodepath=hardware/eco/k3_pico/root_overview.md>
- SpacemiT K3 Ubuntu 镜像仓库：<https://github.com/spacemit-com/K3-Ubuntu-Images>
- SpacemiT K3 Ubuntu 镜像中文 README：<https://github.com/spacemit-com/K3-Ubuntu-Images/blob/main/README.zh.rst>
- SpacemiT K3 Ubuntu 20260530 release：<https://github.com/spacemit-com/K3-Ubuntu-Images/releases/tag/20260530>
- SpacemiT Titantools 刷机工具指南：<https://www.spacemit.com/community/document/info?lang=zh&nodepath=tools/user_guide/flasher_user_guide.md>
- K3 Ubuntu 26.04 fastboot 镜像：<https://archive.spacemit.com/image/k3/version/ubuntu/26.04/20260530/ubuntu-26.04-preinstalled-desktop-riscv64.img.zst>
- K3 Ubuntu 26.04 fastboot 镜像 MD5：<https://archive.spacemit.com/image/k3/version/ubuntu/26.04/20260530/ubuntu-26.04-preinstalled-desktop-riscv64.img.zst.md5>
- K3 Ubuntu 26.04 Titantools 镜像包：<https://archive.spacemit.com/image/k3/version/ubuntu/26.04/20260530/ubuntu-26.04-preinstalled-desktop-riscv64.tar.gz>
- K3 Ubuntu 26.04 Titantools 镜像包 MD5：<https://archive.spacemit.com/image/k3/version/ubuntu/26.04/20260530/ubuntu-26.04-preinstalled-desktop-riscv64.tar.gz.md5>
- SpacemiT X100 core 官方页：<https://www.spacemit.com/en/spacemit-x100-core/>
- CNX Software K3/X100 报道：<https://www.cnx-software.com/2025/07/22/three-high-performance-risc-v-processors-to-watch-in-h2-2025-ultrarisc-ur-dp1000-zizhe-a210-and-spacemit-k3/>
- SpacemiT V100/X100 技术背景：<https://www.prnewswire.com/news-releases/risc-v-breakthrough-spacemit-develops-server-cpu-chip-v100-for-next-generation-ai-applications-30234
