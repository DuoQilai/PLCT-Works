## 3.4 测试用例及说明

| 序号  | 开发板                  | 处理器           | IP核（主CPU）       |
| --- | -------------------- | ------------- | --------------- |
| 1   | ESWIN EBC7700        | EIC7700X      | SiFive P550     |
| 2   | HiFive Premier P550  | EIC7700X      | SiFive P550     |
| 3   | ESWIN EBC7702        | EIC7702X      | SiFive P550     |
| 4   | SpacemiT K3 Pico-ITX | SpacemiT K3   | X100            |
| 5   | SG2044 EVB           | SOPHGO SG2044 | T-Head C920v2   |
| 6   | A210 SODIMM V2       | A210          | 4xC920 + 4xC908 |
| 7   | VisionFive 2 Lite    | JH7110        | SiFive U74      |
| 8   | Canaan K510 CRB-V1.2 KIT | K510      | Dual 64bit cores |
| 9   |                      |               |                 |
| 10  |                      |               |                 |

测试10种RISC-V开发板上GCC和LLVM工具链的测试情况，验证 GCC 和 LLVM 工具链是否能在目标RISC-V开发板上正常安装、编译和运行程序。通过 Hello World 和 Coremark 两个程序验证基本功能和性能。使用 RuyiSDK作为统一的工具链管理工具，确保测试环境的一致性。开发板型号列表如下：

**测试流程为：**

系统初始化：系统镜像下载与烧录（如RevyOS、Ubuntu、Debian等），串口连接与登录，网络配置。

环境准备：安装系统依赖包（如 build-essential, git, wget 等），安装 ruyi 包管理器（按板卡实测版本；P550 为 0.50.0），通过 ruyi 包管理器安装 gnu-ruyisdk 和 llvm-ruyisdk 工具链。

GCC测试：创建并激活GCC虚拟环境，验证GCC版本，编译并运行 Hello World，编译并运行 Coremark 基准测试。

LLVM测试：创建并激活LLVM虚拟环境，验证Clang版本，编译并运行 Hello World，编译并运行 Coremark 基准测试（部分板卡使用特定 -march 参数）。

环境清理：退出虚拟环境，完成测试。

### 测试用例 1-1：GCC和LLVM对EBC7700的支持测试

| 字段      | 内容                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 测试用例标识  | 1-1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| 测试用例名称  | GCC和LLVM对EBC7700的支持测试                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| 测试说明    | 验证GCC和LLVM对EBC7700的支持情况                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| 测试用例初始化 | 1.准备好开发板、Micro USB数据线、MicroSD卡、读卡器、Type-C数据线、Type-C电源适配器<br>2.下载系统镜像：https://github.com/eswincomputing/ebc7700-sbc-ubuntu/releases<br>下载sbc-ubuntu-24.04-preinstalled-server-riscv64_20260313_1243_67.img.zst到本地，解压缩。<br>3.镜像烧录：<br>把SD卡插进读卡器，读卡器插电脑的USB口。<br>打开烧录软件balnenaEtcher，点击从文件烧录，选择解压出的镜像文件，然后在选择目标磁盘中选择 MicroSD 卡的读卡器，最后点击现在烧录! 刷写<br>![image1.png](https://raw.githubusercontent.com/DuoQilai/PLCT-Works/main/Notes/July_Ledger/board-compiler-test-cases_media/image1.png)<br>![image2.png](https://raw.githubusercontent.com/DuoQilai/PLCT-Works/main/Notes/July_Ledger/board-compiler-test-cases_media/image2.png)<br>刷写完成，SD卡插进开发板的卡槽，给开发板插上Micro USB数据线，另一端插电脑 USB 口。<br>![image3.png](https://raw.githubusercontent.com/DuoQilai/PLCT-Works/main/Notes/July_Ledger/board-compiler-test-cases_media/image3.png)<br>打开串口工具Mobaxterm，波特率设置为115200。<br>5.给开发板插上电源线。<br>6.登录用户名和密码都为：ubuntu<br>登录成功后需要更改密码，按照提示操作就好。 |
| 前提与约束 | 开发板系统烧录已完成且已成功通过终端登录；开发板有可用的有线网络连接 |
| 终止条件    | 测试用例全部通过                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

**测试步骤：**

| 序号 | 输入及操作说明 | 期望测试结果 |
| --- | --- | --- |
| 1 | 安装ruyi包管理器<br>sudo apt update; sudo apt install -y wget tar zstd xz-utils git build-essential | 成功安装 |
| 2 | 安装ruyi包管理器<br>wget https://mirror.iscas.ac.cn/ruyisdk/ruyi/tags/0.47.0/ruyi.riscv64<br>chmod +x ruyi.riscv64<br>sudo cp -v ruyi.riscv64 /usr/local/bin/ruyi | 成功安装 |
| 3 | 安装GCC和LLVM工具链<br>ruyi update<br>ruyi install gnu-ruyisdk (0.20260625.0)<br>ruyi install llvm-ruyisdk (22.1.8-ruyi.20260625) | 成功安装 |
| 4 | 创建并激活ruyi虚拟环境（GCC）<br>ruyi venv -t toolchain/gnu-ruyisdk manual venv-gnu-ruyisdk<br>. venv-gnu-ruyisdk/bin/ruyi-activate | 成功创建并激活虚拟环境 |
| 5 | 验证GCC版本<br>riscv64-ruyisdk-linux-gnu-gcc -v | 输出版本号 |
| 6 | 编译并运行Hello World（GCC）<br>cat &lt;&lt; EOF &gt; hello.c<br>#include &lt;stdio.h&gt;<br>int main() {<br>printf("Hello, World!\\n");<br>return 0;<br>}<br>EOF<br>riscv64-ruyisdk-linux-gnu-gcc hello.c -o hello-gcc<br>./hello-gcc | 输出Hello, World! |
| 7 | 编译并运行coremark（GCC）<br>git clone https://github.com/eembc/coremark<br>cd coremark<br>make CC=riscv64-ruyisdk-linux-gnu-gcc XCFLAGS="-march=rv64gc_zba_zbb" compile<br>./coremark.exe | 输出coremark结果 |
| 8 | 返回上级目录并退出ruyi GCC虚拟环境<br>cd ..; ruyi-deactivate | 成功退出虚拟环境 |
| 9 | 创建并激活ruyi虚拟环境（LLVM）<br>ruyi venv -t toolchain/llvm-ruyisdk manual --sysroot-from gnu-ruyisdk venv-llvm-ruyisdk<br>. venv-llvm-ruyisdk/bin/ruyi-activate | 成功创建并激活虚拟环境 |
| 10 | 验证LLVM版本<br>clang -v | 输出版本号 |
| 11 | 编译并运行Hello World（LLVM）<br>clang hello.c -o hello-llvm; ./hello-llvm | 输出Hello, World! |
| 12 | 编译coremark（LLVM）<br>cd coremark; make clean; make CC=clang XCFLAGS="-march=rv64gc_zba_zbb -O3" compile<br>./coremark.exe | 输出coremark结果 |
| 13 | 返回上级目录并退出ruyi LLVM虚拟环境<br>cd ..; ruyi-deactivate | 成功退出虚拟环境 |

### 测试用例 1-2：GCC和LLVM对SiFive HiFive Premier P550的支持测试

| 字段 | 内容 |
| --- | --- |
| 测试用例标识 | 1-2 |
| 测试用例名称 | GCC和LLVM对SiFive HiFive Premier P550的支持测试 |
| 测试说明 | 验证GCC和LLVM对SiFive HiFive Premier P550的支持情况 |
| 测试用例初始化 | 1. 下载操作系统镜像文件和 bootloader，并解压镜像文件。<br>wget https://github.com/sifiveinc/hifive-premier-p550-ubuntu/releases/download/2025.11.00/ubuntu-24.04-preinstalled-server-riscv64.img.xz<br>wget https://github.com/sifiveinc/freedom-u-sdk/releases/download/2026.07.00-HFP550/bootloader_ddr5_secboot.bin<br>unxz -d ubuntu-24.04-preinstalled-server-riscv64.img.xz<br>2. 挂载 MicroSD 卡，并将镜像文件和 bootloader 文件复制到 MicroSD 卡中。以下命令假设 `/dev/sdc` 为 MicroSD 卡设备，实际设备名请根据主机环境确认。<br>sudo mkdir -p /mnt/sd<br>sudo mount /dev/sdc /mnt/sd<br>sudo cp ./ubuntu-24.04-preinstalled-server-riscv64.img ./bootloader_ddr5_secboot.bin /mnt/sd/<br>sync<br>sudo umount /mnt/sd<br>3. 插入 MicroSD 卡，连接开发板串口，启动开发板并进入 SPI Flash 中的 U-Boot。确保拨码开关为 SPI Flash 启动模式：`DIP_SW1[3:0] = 0100`，其中 SW 的 `ON = 0`，`OFF = 1`。在串口终端中出现 `Hit any key to stop autoboot` 时，迅速按下回车键进入 U-Boot 命令行终端。<br>4. 使用定制的 U-Boot 命令烧录镜像。<br>确认 MicroSD 卡状态：<br>=&gt; ls mmc 1<br>如需烧录新的 bootloader，执行以下命令：<br>=&gt; ext4load mmc 1 0x90000000 bootloader_ddr5_secboot.bin<br>=&gt; es_burn write 0x90000000 flash<br>烧录系统镜像：<br>=&gt; es_fs write mmc 1 ubuntu-24.04-preinstalled-server-riscv64.img mmc 0<br>5. 重启开发板。<br>=&gt; reset |
| 前提与约束 | 开发板系统烧录已完成且已成功通过终端登录；开发板有可用的有线网络连接 |
| 终止条件 | 测试用例全部通过 |

**测试步骤：**

| 序号  | 输入及操作说明                                                                                                                                                                                                                                                         | 期望测试结果          |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| 1   | 安装依赖包<br>sudo apt update; sudo apt install -y wget tar zstd xz-utils git build-essential                                                                                                                                                                        | 成功安装            |
| 2   | 安装ruyi包管理器<br>wget https://mirror.iscas.ac.cn/ruyisdk/ruyi/tags/0.50.0/ruyi-0.50.0.riscv64<br>chmod +x ./ruyi-0.50.0.riscv64<br>sudo cp -v ./ruyi-0.50.0.riscv64 /usr/local/bin/ruyi                                                                            | 成功安装            |
| 3   | 安装GCC和LLVM工具链<br>ruyi update<br>ruyi install gnu-ruyisdk (0.20260625.0)<br>ruyi install llvm-ruyisdk (22.1.8-ruyi.20260625)                                                                                                                                     | 成功安装            |
| 4   | 创建并激活ruyi虚拟环境（GCC）<br>ruyi venv -t gnu-ruyisdk generic ~/venv-gnu-ruyisdk<br>source ~/venv-gnu-ruyisdk/bin/ruyi-activate                                                                                                                                        | 成功创建虚拟环境        |
| 5   | 验证GCC版本<br>riscv64-ruyisdk-linux-gnu-gcc -v                                                                                                                                                                                                                     | 输出版本号           |
| 6   | 编译并运行Hello World（GCC）<br>cat &lt;&lt; EOF &gt; hello.c<br>#include &lt;stdio.h&gt;<br>int main() {<br>printf("Hello, World!\\n");<br>return 0;<br>}<br>EOF<br>riscv64-ruyisdk-linux-gnu-gcc hello.c -o hello-gcc<br>./hello-gcc                                 | 输出Hello, World! |
| 7   | 编译并运行coremark（GCC）<br>git clone https://github.com/eembc/coremark<br>cd coremark<br>make CC=riscv64-ruyisdk-linux-gnu-gcc XCFLAGS="-O3 -march=rv64imafdch_zicsr_zifencei_zca_zcd_zba_zbb -mabi=lp64d" compile<br>mv coremark.exe coremark-gcc<br>./coremark-gcc | 输出coremark结果    |
| 8   | 返回上级目录并退出ruyi GCC虚拟环境<br>cd ..; ruyi-deactivate                                                                                                                                                                                                                 | 成功退出虚拟环境        |
| 9   | 创建并激活ruyi虚拟环境（LLVM）<br>ruyi venv -t llvm-ruyisdk generic --sysroot-from gnu-ruyisdk ~/venv-llvm-ruyisdk<br>source ~/venv-llvm-ruyisdk/bin/ruyi-activate                                                                                                         | 成功创建并激活虚拟环境     |
| 10  | 验证LLVM版本<br>clang -v                                                                                                                                                                                                                                            | 输出版本号           |
| 11  | 编译并运行Hello World（LLVM）<br>clang hello.c -o hello-llvm; ./hello-llvm                                                                                                                                                                                           | 输出Hello, World! |
| 12  | 编译并运行coremark（LLVM）<br>cd coremark; make clean; make CC=clang XCFLAGS="-O3 -march=rv64imafdch_zicsr_zifencei_zca_zcd_zba_zbb -mabi=lp64d" compile<br>mv coremark.exe coremark-llvm<br>./coremark-llvm                                                         | 输出coremark结果    |
| 13  | 返回上级目录并退出ruyi LLVM虚拟环境<br>cd ..; ruyi-deactivate                                                                                                                                                                                                                | 成功退出虚拟环境        |

### 测试用例 1-3：GCC和LLVM对ESWIN EBC7702的支持测试

| 字段 | 内容 |
| --- | --- |
| 测试用例标识 | 1-3 |
| 测试用例名称 | GCC和LLVM对ESWIN EBC7702的支持测试 |
| 测试说明 | 验证GCC和LLVM对ESWIN EBC7702的支持情况 |
| 测试用例初始化 | 1. 下载 bootloader 和 Ubuntu 镜像文件，并解压镜像。<br>wget https://github.com/eswincomputing/ebc7702-dev-board-ubuntu/releases/download/2025.12.30/bootloader_EBC7702-D01_die0.bin<br>wget https://github.com/eswincomputing/ebc7702-dev-board-ubuntu/releases/download/2025.12.30/bootloader_EBC7702-D01_die1.bin<br>wget https://github.com/eswincomputing/ebc7702-dev-board-ubuntu/releases/download/2025.12.30/d560-24.04-preinstalled-server-riscv64_20260313_1628_70.img.zst<br>zstd -d d560-24.04-preinstalled-server-riscv64_20260313_1628_70.img.zst<br>2. 格式化并挂载 MicroSD 卡，将 Ubuntu 镜像和 bootloader 文件复制到卡中。以下命令假设 MicroSD 卡设备为 `/dev/sdc`，实际设备名请根据主机环境确认。注意：以下操作会清空 `/dev/sdc` 上的所有内容。<br>lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINT,MODEL<br>sudo umount /dev/sdc* 2&gt;/dev/null \|\| true<br>sudo mkfs.ext4 -F -L SDCARD /dev/sdc<br>sudo mkdir -p /mnt/sd<br>sudo mount /dev/sdc /mnt/sd<br>sudo cp ./d560-24.04-preinstalled-server-riscv64_20260313_1628_70.img /mnt/sd/<br>sudo cp ./bootloader_EBC7702-D01_die0.bin /mnt/sd/<br>sudo cp ./bootloader_EBC7702-D01_die1.bin /mnt/sd/<br>ls -lh /mnt/sd/<br>sync<br>sudo umount /mnt/sd<br>3. 插入 MicroSD 卡，连接开发板串口并上电。在串口终端出现 `Hit any key to stop autoboot` 时按下回车，进入 U-Boot 命令行。<br>4. 使用定制的 U-Boot 命令烧录 bootloader 和系统镜像，然后重启开发板。注意：EBC7702 是双 die 板，die0 / die1 bootloader 不能混用。<br>=&gt; ls mmc 1<br>=&gt; ext4load mmc 1 0x100000000 bootloader_EBC7702-D01_die0.bin<br>=&gt; es_burn write 0x100000000 flash<br>=&gt; ext4load mmc 1 0x100000000 bootloader_EBC7702-D01_die1.bin<br>=&gt; es_burn write 0x100000000 flash 1<br>=&gt; es_fs write mmc 1 d560-24.04-preinstalled-server-riscv64_20260313_1628_70.img mmc 0<br>=&gt; reset |
| 前提与约束 | 开发板系统烧录已完成且已成功通过终端登录；开发板有可用的有线网络连接 |
| 终止条件 | 测试用例全部通过 |

**测试步骤：**

| 序号  | 输入及操作说明                                                                                                                                                                                                                         | 期望测试结果          |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| 1   | 安装依赖包<br>sudo apt update; sudo apt install -y wget tar zstd xz-utils git build-essential                                                                                                                                        | 成功安装            |
| 2   | 安装ruyi包管理器<br>wget https://mirror.iscas.ac.cn/ruyisdk/ruyi/tags/0.50.0/ruyi-0.50.0.riscv64<br>chmod +x ./ruyi-0.50.0.riscv64<br>sudo cp -v ./ruyi-0.50.0.riscv64 /usr/local/bin/ruyi                                            | 成功安装            |
| 3   | 安装GCC和LLVM工具链<br>ruyi update<br>ruyi install gnu-ruyisdk (0.20260625.0)<br>ruyi install llvm-ruyisdk (22.1.8-ruyi.20260625)                                                                                                     | 成功安装            |
| 4   | 创建并激活ruyi虚拟环境（GCC）<br>ruyi venv -t gnu-ruyisdk generic ~/venv-gnu-ruyisdk-ebc7702<br>source ~/venv-gnu-ruyisdk-ebc7702/bin/ruyi-activate                                                                                        | 成功创建虚拟环境        |
| 5   | 验证GCC版本<br>riscv64-ruyisdk-linux-gnu-gcc -v                                                                                                                                                                                     | 输出版本号           |
| 6   | 编译并运行Hello World（GCC）<br>cat &lt;&lt; EOF &gt; hello.c<br>#include &lt;stdio.h&gt;<br>int main() {<br>printf("Hello, World!\\n");<br>return 0;<br>}<br>EOF<br>riscv64-ruyisdk-linux-gnu-gcc hello.c -o hello-gcc<br>./hello-gcc | 输出Hello, World! |
| 7   | 编译并运行coremark（GCC）<br>git clone https://github.com/eembc/coremark<br>cd coremark<br>make CC=riscv64-ruyisdk-linux-gnu-gcc XCFLAGS="-O3 -march=rv64imafdch_zicntr_zicsr_zifencei_zihpm_zba_zbb -mabi=lp64d" compile<br>mv coremark.exe coremark-gcc<br>./coremark-gcc                          | 输出coremark结果    |
| 8   | 返回上级目录并退出ruyi GCC虚拟环境<br>cd ..; ruyi-deactivate                                                                                                                                                                                 | 成功退出虚拟环境        |
| 9   | 创建并激活ruyi虚拟环境（LLVM）<br>ruyi venv -t llvm-ruyisdk generic --sysroot-from gnu-ruyisdk ~/venv-llvm-ruyisdk-ebc7702<br>source ~/venv-llvm-ruyisdk-ebc7702/bin/ruyi-activate                                                         | 成功创建并激活虚拟环境     |
| 10  | 验证LLVM版本<br>clang -v                                                                                                                                                                                                            | 输出版本号           |
| 11  | 编译并运行Hello World（LLVM）<br>clang hello.c -o hello-llvm; ./hello-llvm                                                                                                                                                           | 输出Hello, World! |
| 12  | 编译并运行coremark（LLVM）<br>cd coremark; make clean; make CC=clang XCFLAGS="-O3 -march=rv64imafdch_zicntr_zicsr_zifencei_zihpm_zba_zbb -mabi=lp64d" compile<br>mv coremark.exe coremark-llvm<br>./coremark-llvm                    | 输出coremark结果    |
| 13  | 返回上级目录并退出ruyi LLVM虚拟环境<br>cd ..; ruyi-deactivate                                                                                                                                                                                 | 成功退出虚拟环境            |


### 测试用例 1-4：GCC和LLVM对SpacemiT K3 Pico-ITX的支持测试

| 字段 | 内容 |
| --- | --- |
| 测试用例标识 | 1-4 |
| 测试用例名称 | GCC和LLVM对SpacemiT K3 Pico-ITX的支持测试 |
| 测试说明 | 验证GCC和LLVM对SpacemiT K3 Pico-ITX的支持情况 |
| 测试用例初始化 | 1. 下载操作系统镜像文件，并校验镜像文件。K3 镜像包内已包含启动固件和系统分区文件，不需要单独下载 bootloader，也不需要解压。<br>wget https://archive.spacemit.com/image/k3/version/bianbu/v4.0/Bianbu-LXQt-K3-v4.0-20260430170328.tar.gz<br>wget https://archive.spacemit.com/image/k3/version/bianbu/v4.0/Bianbu-LXQt-K3-v4.0-20260430170328.tar.gz.md5<br>md5sum Bianbu-LXQt-K3-v4.0-20260430170328.tar.gz<br>cat Bianbu-LXQt-K3-v4.0-20260430170328.tar.gz.md5<br>2. 连接 Type-C 烧录线和开发板电源。若使用独立烧录 Type-C 口，需要额外给开发板供电；该接口只用于数据传输，不能给开发板供电。<br>1. 使用 Type-C 数据线连接 K3 Pico-ITX 和电脑<br>2. 给 K3 Pico-ITX 接入电源<br>3. 确认 USB 线为数据线，不是纯充电线<br>3. 进入 FDL 烧录模式。开发板关机状态：按住 FDL 固件烧录按键不松开；插入 Type-C 数据线，并给开发板上电；松开 FDL 按键；使用 Titan 或 fastboot 进行烧录。开发板已开机状态：按住 FDL 固件烧录按键不松开；短按 RST 复位按键；松开 FDL 按键；使用 Titan 或 fastboot 进行烧录。<br>4. 使用 Titan 工具烧录系统镜像。<br>1. 打开 SpacemiT Titan / Titan Flasher<br>2. 点击扫描设备，确认可以识别到 K3 Pico-ITX<br>3. 选择镜像文件：Bianbu-LXQt-K3-v4.0-20260430170328.tar.gz<br>4. 点击开始烧录<br>5. 等待烧录进度完成<br>5. 重启开发板。<br>1. 烧录完成后断开开发板电源<br>2. 重新连接开发板电源<br>3. 等待系统启动<br>6. 连接串口并查看启动日志。串口参数：波特率 115200；数据位 8；停止位 1；校验位 None；流控 None。<br>Linux 主机连接串口示例：<br>sudo picocom -b 115200 /dev/ttyUSB0 |
| 前提与约束 | 开发板系统烧录已完成且已成功通过终端登录；开发板有可用的有线网络连接 |
| 终止条件 | 测试用例全部通过 |

**测试步骤：**

| 序号 | 输入及操作说明 | 期望测试结果 |
| --- | --- | --- |
| 1 | 安装依赖包<br>sudo apt update; sudo apt install -y wget tar zstd xz-utils git build-essential make file ca-certificates | 成功安装 |
| 2 | 安装ruyi包管理器<br>wget https://mirror.iscas.ac.cn/ruyisdk/ruyi/tags/0.50.0/ruyi-0.50.0.riscv64<br>chmod +x ./ruyi-0.50.0.riscv64<br>sudo cp -v ./ruyi-0.50.0.riscv64 /usr/local/bin/ruyi<br>ruyi version | 成功安装 |
| 3 | 安装GCC和LLVM工具链<br>ruyi update<br>ruyi install gnu-ruyisdk (0.20260625.0)<br>ruyi install llvm-ruyisdk (22.1.8-ruyi.20260625) | 成功安装 |
| 4 | 创建并激活ruyi虚拟环境（GCC）<br>ruyi venv -t gnu-ruyisdk generic ~/venv-gnu-ruyisdk-k3<br>source ~/venv-gnu-ruyisdk-k3/bin/ruyi-activate | 成功创建并激活虚拟环境 |
| 5 | 验证GCC版本<br>riscv64-ruyisdk-linux-gnu-gcc -v | 输出版本号 |
| 6 | 编译并运行Hello World（GCC）<br>cat &lt;&lt; EOF &gt; hello.c<br>#include &lt;stdio.h&gt;<br>int main() {<br>printf("Hello, World!\\n");<br>return 0;<br>}<br>EOF<br>riscv64-ruyisdk-linux-gnu-gcc hello.c -o hello-gcc<br>./hello-gcc | 输出Hello, World! |
| 7 | 编译并运行coremark（GCC）<br>git clone https://github.com/eembc/coremark<br>cd coremark<br>make CC=riscv64-ruyisdk-linux-gnu-gcc XCFLAGS="-O3 -march=rv64gcv -mabi=lp64d" compile<br>mv coremark.exe coremark-gcc<br>./coremark-gcc | 输出coremark结果 |
| 8 | 返回上级目录并退出ruyi GCC虚拟环境<br>cd ..; ruyi-deactivate | 成功退出虚拟环境 |
| 9 | 创建并激活ruyi虚拟环境（LLVM）<br>ruyi venv -t llvm-ruyisdk generic --sysroot-from gnu-ruyisdk ~/venv-llvm-ruyisdk-k3<br>source ~/venv-llvm-ruyisdk-k3/bin/ruyi-activate | 成功创建并激活虚拟环境 |
| 10 | 验证LLVM版本<br>clang -v | 输出版本号 |
| 11 | 编译并运行Hello World（LLVM）<br>clang hello.c -o hello-llvm; ./hello-llvm | 输出Hello, World! |
| 12 | 编译并运行coremark（LLVM）<br>cd coremark; make clean; make CC=clang XCFLAGS="-O3 -march=rv64gcv -mabi=lp64d" compile<br>mv coremark.exe coremark-llvm<br>./coremark-llvm | 输出coremark结果 |
| 13 | 返回上级目录并退出ruyi LLVM虚拟环境<br>cd ..; ruyi-deactivate | 成功退出虚拟环境 |

### 测试用例 1-5：GCC和LLVM对SG2044的支持测试

| 字段 | 内容 |
| --- | --- |
| 测试用例标识 | 1-5 |
| 测试用例名称 | GCC和LLVM对SG2044的支持测试 |
| 测试说明 | 验证GCC和LLVM对SG2044的支持情况 |
| 测试用例初始化 | 1. 下载操作系统镜像文件，并解压镜像文件。<br>wget https://github.com/sophgo/bootloader-riscv/releases/download/sg2044-v0.1/ubuntu-24.04.1-riscv64-sg2044-20241025.template.img.xz<br>wget https://github.com/sophgo/bootloader-riscv/releases/download/sg2044-v0.1/md5sum.txt<br>grep ubuntu-24.04.1-riscv64-sg2044-20241025.template.img.xz md5sum.txt \| md5sum -c -<br>unxz -d ubuntu-24.04.1-riscv64-sg2044-20241025.template.img.xz<br>mv ubuntu-24.04.1-riscv64-sg2044-20241025.template.img ubuntu-sophgo.img<br>2. 将 Ubuntu 镜像写入 MicroSD 卡。以下命令假设 `/dev/sdc` 为 MicroSD 卡设备，实际设备名请根据主机环境确认。<br>lsblk<br>sudo dd if=ubuntu-sophgo.img of=/dev/sdc bs=1024M status=progress<br>sync<br>3. 如果使用的是官方 template 镜像，需要将 SG2044 BSP 固件复制到 MicroSD 卡 EFI 分区。以下命令假设 MicroSD 卡 EFI 分区为 `/dev/sdc1`，且 BSP 固件已经生成在 `install/soc_sg2044/single_chip/firmware/` 目录。<br>sudo mkdir -p /mnt/EFI<br>sudo mount /dev/sdc1 /mnt/EFI<br>sudo mkdir -p /mnt/EFI/riscv64<br>sudo cp install/soc_sg2044/single_chip/firmware/* /mnt/EFI/riscv64/<br>sync<br>sudo umount /mnt/EFI<br>4. 插入 MicroSD 卡，连接开发板串口，启动 SG2044 EVB。串口参数：波特率 115200；数据位 8；停止位 1；校验位 None；流控 None。<br>Linux 主机连接串口示例：<br>sudo picocom -b 115200 /dev/ttyUSB0<br>5. 系统启动后登录 Ubuntu。用户名：ubuntu；密码：ubuntu。<br>6. 验证系统信息。<br>cat /etc/os-release<br>uname -a<br>cat /proc/device-tree/model 2&gt;/dev/null \| tr '\0' '\n'<br>lscpu<br>lsblk<br>ip a<br>7. 重启开发板。<br>sudo reboot |
| 前提与约束 | 开发板系统烧录已完成且已成功通过终端登录；开发板有可用的有线网络连接 |
| 终止条件 | 测试用例全部通过 |

**测试步骤：**

| 序号 | 输入及操作说明 | 期望测试结果 |
| --- | --- | --- |
| 1 | 安装依赖包<br>sudo apt update; sudo apt install -y wget tar zstd xz-utils git build-essential make file ca-certificates | 成功安装 |
| 2 | 安装ruyi包管理器<br>wget https://mirror.iscas.ac.cn/ruyisdk/ruyi/tags/0.50.0/ruyi-0.50.0.riscv64<br>chmod +x ./ruyi-0.50.0.riscv64<br>sudo cp -v ./ruyi-0.50.0.riscv64 /usr/local/bin/ruyi<br>ruyi version | 成功安装 |
| 3 | 安装GCC和LLVM工具链<br>ruyi update<br>ruyi install gnu-ruyisdk (0.20260625.0)<br>ruyi install llvm-ruyisdk (22.1.8-ruyi.20260625) | 成功安装 |
| 4 | 创建并激活ruyi虚拟环境（GCC）<br>ruyi venv -t gnu-ruyisdk generic ~/venv-gnu-ruyisdk-sg2044<br>source ~/venv-gnu-ruyisdk-sg2044/bin/ruyi-activate | 成功创建并激活虚拟环境 |
| 5 | 验证GCC版本<br>riscv64-ruyisdk-linux-gnu-gcc -v | 输出版本号 |
| 6 | 编译并运行Hello World（GCC）<br>cat &lt;&lt; EOF &gt; hello.c<br>#include &lt;stdio.h&gt;<br>int main() {<br>printf("Hello, World!\\n");<br>return 0;<br>}<br>EOF<br>riscv64-ruyisdk-linux-gnu-gcc hello.c -o hello-gcc<br>./hello-gcc | 输出Hello, World! |
| 7 | 编译并运行coremark（GCC）<br>git clone https://github.com/eembc/coremark<br>cd coremark<br>make CC=riscv64-ruyisdk-linux-gnu-gcc XCFLAGS="-O3 -march=rv64gcv -mabi=lp64d" compile<br>mv coremark.exe coremark-gcc<br>./coremark-gcc | 输出coremark结果 |
| 8 | 返回上级目录并退出ruyi GCC虚拟环境<br>cd ..; ruyi-deactivate | 成功退出虚拟环境 |
| 9 | 创建并激活ruyi虚拟环境（LLVM）<br>ruyi venv -t llvm-ruyisdk generic --sysroot-from gnu-ruyisdk ~/venv-llvm-ruyisdk-sg2044<br>source ~/venv-llvm-ruyisdk-sg2044/bin/ruyi-activate | 成功创建并激活虚拟环境 |
| 10 | 验证LLVM版本<br>clang -v | 输出版本号 |
| 11 | 编译并运行Hello World（LLVM）<br>clang hello.c -o hello-llvm; ./hello-llvm | 输出Hello, World! |
| 12 | 编译并运行coremark（LLVM）<br>cd coremark; make clean; make CC=clang XCFLAGS="-O3 -march=rv64gcv -mabi=lp64d" compile<br>mv coremark.exe coremark-llvm<br>./coremark-llvm | 输出coremark结果 |
| 13 | 返回上级目录并退出ruyi LLVM虚拟环境<br>cd ..; ruyi-deactivate | 成功退出虚拟环境 |

### 测试用例 1-6：GCC和LLVM对A210 SODIMM V2的支持测试

| 字段 | 内容 |
| --- | --- |
| 测试用例标识 | 1-6 |
| 测试用例名称 | GCC和LLVM对A210 SODIMM V2的支持测试 |
| 测试说明 | 验证GCC和LLVM对A210 SODIMM V2的支持情况 |
| 测试用例初始化 | 1. 下载 A210 SODIMM V2 操作系统镜像文件，并解压镜像文件。<br>wget https://developer.zhcomputing.com/downloads/release/zhihesdk/v2.9.0/br2image-v2.9.0-a210_evb.tar.gz<br>tar -xzf br2image-v2.9.0-a210_evb.tar.gz<br>cd "$(dirname "$(find . -name fastboot_images.sh \| head -n 1)")"<br>2. 安装 Fastboot 工具，并确认镜像目录中包含烧录脚本和 eMMC 镜像文件。<br>sudo apt update; sudo apt install -y android-sdk-platform-tools<br>fastboot --version<br>ls fastboot_images.sh emmc-gpt_primary.img emmc_boot-loader.img emmc-boot_a.img emmc-system_a.img<br>chmod +x fastboot_images.sh<br>3. 连接开发板并进入 USB 烧录模式。接入 12V DC 电源，连接 TTL 串口，串口波特率设置为 115200；将 USB-A 烧录接口连接到主机。按下 Power Button 启动开发板后，按住 Flash Button 不放，再按一下 Reset Button，然后松开 Flash Button，使开发板进入 USB 烧录模式。<br>fastboot devices<br>4. 执行烧录脚本，将镜像烧录到开发板 eMMC。<br>sudo ./fastboot_images.sh<br>5. 烧录完成后，按 Reset Button 重启开发板，等待串口进入登录界面。<br>Welcome to Buildroot<br>buildroot login:<br>6. 使用 root 用户登录系统。如需 SSH 登录，进入系统后先设置 root 密码。<br>root<br>passwd |
| 前提与约束 | 开发板系统烧录已完成且已成功通过终端登录；开发板有可用的有线网络连接 |
| 终止条件 | 测试用例全部通过 |

**测试步骤：**

| 序号  | 输入及操作说明                                                                                                                                                                                                                             | 期望测试结果          |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| 1   | 安装依赖包<br>sudo apt update; sudo apt install -y wget tar zstd xz-utils git build-essential make file ca-certificates                                                                                                                | 成功安装            |
| 2   | 安装ruyi包管理器<br>wget https://mirror.iscas.ac.cn/ruyisdk/ruyi/tags/0.50.0/ruyi-0.50.0.riscv64<br>chmod +x ./ruyi-0.50.0.riscv64<br>sudo cp -v ./ruyi-0.50.0.riscv64 /usr/local/bin/ruyi<br>ruyi version                                | 成功安装            |
| 3   | 安装GCC和LLVM工具链<br>ruyi update<br>ruyi install gnu-ruyisdk (0.20260625.0)<br>ruyi install llvm-ruyisdk (22.1.8-ruyi.20260625)                                                                                                         | 成功安装            |
| 4   | 创建并激活ruyi虚拟环境（GCC）<br>ruyi venv -t gnu-ruyisdk generic ~/venv-gnu-ruyisdk-a210-sodimm-v2<br>source ~/venv-gnu-ruyisdk-a210-sodimm-v2/bin/ruyi-activate                                                                              | 成功创建并激活虚拟环境     |
| 5   | 验证GCC版本<br>riscv64-ruyisdk-linux-gnu-gcc -v                                                                                                                                                                                         | 输出版本号           |
| 6   | 编译并运行Hello World（GCC）<br>cat &lt;&lt; EOF &gt; hello.c<br>#include &lt;stdio.h&gt;<br>int main() {<br>printf("Hello, World!\\n");<br>return 0;<br>}<br>EOF<br>riscv64-ruyisdk-linux-gnu-gcc hello.c -o hello-gcc<br>./hello-gcc | 输出Hello, World! |
| 7   | 编译并运行coremark（GCC）<br>git clone https://github.com/eembc/coremark<br>cd coremark<br>make CC=riscv64-ruyisdk-linux-gnu-gcc XCFLAGS="-O3 -mcpu=xt-c920 -mabi=lp64d" compile<br>mv coremark.exe coremark-gcc<br>./coremark-gcc         | 输出coremark结果    |
| 8   | 返回上级目录并退出ruyi GCC虚拟环境<br>cd ..; ruyi-deactivate                                                                                                                                                                                     | 成功退出虚拟环境        |
| 9   | 创建并激活ruyi虚拟环境（LLVM）<br>ruyi venv -t llvm-ruyisdk generic --sysroot-from gnu-ruyisdk ~/venv-llvm-ruyisdk-a210-sodimm-v2<br>source ~/venv-llvm-ruyisdk-a210-sodimm-v2/bin/ruyi-activate                                               | 成功创建并激活虚拟环境     |
| 10  | 验证LLVM版本<br>clang -v                                                                                                                                                                                                                | 输出版本号           |
| 11  | 编译并运行Hello World（LLVM）<br>clang hello.c -o hello-llvm; ./hello-llvm                                                                                                                                                               | 输出Hello, World! |
| 12  | 编译并运行coremark（LLVM）<br>cd coremark; make clean; make CC=clang XCFLAGS="-O3 -march=rv64gcv -mabi=lp64d" compile<br>mv coremark.exe coremark-llvm<br>./coremark-llvm                                                              | 输出coremark结果    |
| 13  | 返回上级目录并退出ruyi LLVM虚拟环境<br>cd ..; ruyi-deactivate                                                                                                                                                                                    | 成功退出虚拟环境        |

### 测试用例 1-7：GCC和LLVM对VisionFive 2 Lite的支持测试

| 字段 | 内容 |
| --- | --- |
| 测试用例标识 | 1-7 |
| 测试用例名称 | GCC和LLVM对VisionFive 2 Lite的支持测试 |
| 测试说明 | 验证GCC和LLVM对VisionFive 2 Lite的支持情况 |
| 测试用例初始化 | 准备好开发板、USB转TTL串口模块、杜邦线、Type-C数据线、Type-C电源适配器<br>1.下载系统镜像：https://cdimage.ubuntu.com/releases/24.04.3/release/ubuntu-24.04.3-preinstalled-server-riscv64+jh7110.img.xz<br>参考 https://canonical-ubuntu-boards.readthedocs-hosted.com/en/latest/how-to/starfive-visionfive-2/<br>2.eMMC系统安装：<br>下载烧录软件压缩包https://files.waveshare.net/wiki/VisionFive2/SFFB_Tool_V1.0.7z，并解压(含usb_driver)。<br>下载串口工具压缩包https://github.com/TeraTermProject/teraterm/releases/download/v5.6.0/teraterm-5.6.0-arm64.exe，并解压。<br>使用串口连接VisionFive2 Lite 40Pin上对应的引脚：<br>从黑线开始，从左到右，开发板一侧分别为：GND、TX、RX；分别对应串口的GND、RX、TX。<br>![vf2-image1.png](https://raw.githubusercontent.com/DuoQilai/PLCT-Works/main/Notes/July_Ledger/board-compiler-test-cases_media/vf2-image1.png)<br>串口插电脑 USB 口，打开串口工具TeraTerm，波特率设置为115200，给板子上电，同时立刻在串口窗口里按任意键，打断自动启动，进入 U-Boot 命令行，输入命令 fastboot usb 0。<br>3.驱动安装：<br>打开设备管理器查看是否有USB Download Gadget出现在其他设备下，双击打开属性菜单，点击更新驱动程序。<br>![vf2-image2.png](https://raw.githubusercontent.com/DuoQilai/PLCT-Works/main/Notes/July_Ledger/board-compiler-test-cases_media/vf2-image2.png)<br>选择“浏览我的电脑以获取驱动程序”，添加文件夹路径 SFFB_Tool_V1.0\usb_driver，然后点击“下一步”继续安装。<br>![vf2-image3.png](https://raw.githubusercontent.com/DuoQilai/PLCT-Works/main/Notes/July_Ledger/board-compiler-test-cases_media/vf2-image3.png)<br>4.镜像烧录：<br>打开烧录软件SFFB_Tool，选择对应的镜像文件，然后点击startAll或者Action下的Run按键，开始传输镜像。<br>![vf2-image4.png](https://raw.githubusercontent.com/DuoQilai/PLCT-Works/main/Notes/July_Ledger/board-compiler-test-cases_media/vf2-image4.png)<br>等待传输完成即可断电。<br>5.给开发板上电开机。<br>6.登录用户密码为：starfive |
| 前提与约束 | 开发板系统烧录已完成且已成功通过终端登录；开发板有可用的有线网络连接 |
| 终止条件 | 测试用例全部通过 |

**测试步骤：**

| 序号 | 输入及操作说明 | 期望测试结果 |
| --- | --- | --- |
| 1 | 安装依赖包<br>sudo apt update; sudo apt install -y wget tar zstd xz-utils git build-essential | 成功安装 |
| 2 | 安装ruyi包管理器<br>wget https://mirror.iscas.ac.cn/ruyisdk/ruyi/tags/0.50.0/ruyi-0.50.0.riscv64<br>chmod +x ./ruyi-0.50.0.riscv64<br>sudo cp -v ./ruyi-0.50.0.riscv64 /usr/local/bin/ruyi | 成功安装 |
| 3 | 安装GCC和LLVM工具链<br>ruyi update<br>ruyi install gnu-ruyisdk (0.20260625.0)<br>ruyi install llvm-ruyisdk (22.1.8-ruyi.20260625) | 成功安装 |
| 4 | 创建并激活ruyi虚拟环境（GCC）<br>ruyi venv -t toolchain/gnu-ruyisdk manual venv-gnu-ruyisdk<br>. ~/venv-gnu-ruyisdk/bin/ruyi-activate | 成功创建并激活虚拟环境 |
| 5 | 验证GCC版本<br>riscv64-ruyisdk-linux-gnu-gcc -v | 输出版本号 |
| 6 | 编译并运行Hello World（GCC）<br>cat &lt;&lt; EOF &gt; hello.c<br>#include &lt;stdio.h&gt;<br>int main(void) {<br>printf("Hello, World!\\n");<br>return 0;<br>}<br>EOF<br>riscv64-ruyisdk-linux-gnu-gcc hello.c -o hello-gcc<br>./hello-gcc | 输出Hello, World! |
| 7 | 编译并运行coremark（GCC）<br>git clone https://github.com/eembc/coremark<br>cd coremark<br>make CC=riscv64-ruyisdk-linux-gnu-gcc XCFLAGS="-march=rv64gc_zba_zbb" compile<br>mv coremark.exe coremark-gcc<br>./coremark-gcc | 输出coremark结果 |
| 8 | 返回上级目录并退出ruyi GCC虚拟环境<br>cd ..; ruyi-deactivate | 成功退出虚拟环境 |
| 9 | 创建并激活ruyi虚拟环境（LLVM）<br>ruyi venv -t toolchain/llvm-ruyisdk manual --sysroot-from gnu-ruyisdk venv-llvm-ruyisdk<br>. ~/venv-llvm-ruyisdk/bin/ruyi-activate | 成功创建并激活虚拟环境 |
| 10 | 验证LLVM版本<br>clang -v | 输出版本号 |
| 11 | 编译并运行Hello World（LLVM）<br>clang hello.c -o hello-llvm<br>./hello-llvm | 输出Hello, World! |
| 12 | 编译并运行coremark（LLVM）<br>cd coremark<br>make clean<br>make CC=clang XCFLAGS="-march=rv64gc_zba_zbb" compile<br>mv coremark.exe coremark-llvm<br>./coremark-llvm | 输出coremark结果 |
| 13 | 返回上级目录并退出ruyi LLVM虚拟环境<br>cd ..; ruyi-deactivate | 成功退出虚拟环境 |

### 测试用例 1-8：GCC和LLVM对Canaan K510 CRB-V1.2 KIT的支持测试

| 字段 | 内容 |
| --- | --- |
| 测试用例标识 | 1-8 |
| 测试用例名称 | GCC和LLVM对Canaan K510 CRB-V1.2 KIT的支持测试 |
| 测试说明 | 验证GCC和LLVM对Canaan K510 CRB-V1.2 KIT的支持情况 |
| 测试用例初始化 | 准备好开发板、Type-C数据线(开发板已附带)、Type-C电源适配器、microSD卡一张<br>1.下载并编译系统镜像：<br>参考文档：https://www.docker.com<br>2.拉取源码仓库：<br>git clone --depth=1 https://github.com/kendryte/k510_buildroot<br>3.启动Docker容器并构建：<br>进入容器：<br>sh k510_buildroot/tools/docker/run_k510_docker.sh<br>构建系统镜像：<br>make dl && make<br>构建完成后，输入exit或按Ctrl+D退出容器。<br>4.验证镜像文件：<br>构建完成后，生成的镜像文件位于：<br>k510_buildroot/k510_crb_lp3_v1_2_defconfig/images/sysimage-sdcard.img<br>可执行查看：<br>ls -lh k510_buildroot/k510_crb_lp3_v1_2_defconfig/images/<br>5.镜像烧录：<br>插入microSD卡，确认设备名：<br>lsblk<br>烧录镜像：<br>sudo dd if=~/tes/k510_buildroot/k510_crb_lp3_v1_2_defconfig/images/sysimage-sdcard.img of=/dev/sdb bs=1M status=progress<br>根据实际路径更改。<br>确保数据完全写入：<br>sync<br>6.上电：<br>检查启动开关：开发板插入microSD卡，确保板载SW1开关处于microSD卡启动位置（BOOT0=OFF/1，BOOT1=ON/0）。<br>硬件连接：插入USB Type-C供电和USB-UART串口，丝印为DC:5V和UART。<br>确认串口设备，如/dev/ttyUSB0或/dev/ttyACM0。<br>7.串口登录：<br>首次需要进行串口设置：<br>sudo minicom -s<br>选Serial port setup，然后A键修改设备名为实际设备/dev/ttyUSB0，确保Bps/Par/Bits为115200 8N1，并且Hardware Flow Control为No。<br>打开串口终端：<br>sudo minicom<br>登录系统：用户名root，密码为空（直接回车）。 |
| 前提与约束 | 开发板系统烧录已完成且已成功通过终端登录；开发板有可用的有线网络连接 |
| 终止条件 | 测试用例全部通过 |

**测试步骤：**

| 序号 | 输入及操作说明 | 期望测试结果 |
| --- | --- | --- |
| 1 | 安装依赖包<br>sudo apt update; sudo apt install -y wget tar zstd xz-utils git build-essential | 成功安装 |
| 2 | 安装ruyi包管理器<br>wget https://mirror.iscas.ac.cn/ruyisdk/ruyi/tags/0.50.0/ruyi-0.50.0.amd64<br>chmod +x ./ruyi-0.50.0.amd64<br>sudo cp -v ./ruyi-0.50.0.amd64 /usr/local/bin/ruyi | 成功安装 |
| 3 | 安装GCC和LLVM工具链<br>ruyi update<br>ruyi install gnu-ruyisdk (0.20260625.0)<br>ruyi install llvm-ruyisdk (22.1.8-ruyi.20260625) | 成功安装 |
| 4 | 创建并激活ruyi虚拟环境（GCC）<br>ruyi venv -t gnu-ruyisdk generic gcc-env<br>. gcc-env/bin/ruyi-activate | 成功创建并激活虚拟环境 |
| 5 | 验证GCC版本<br>riscv64-ruyisdk-linux-gnu-gcc -v | 输出版本号 |
| 6 | 编译Hello World（GCC）<br>cat &lt;&lt; EOF &gt; hello.c<br>#include &lt;stdio.h&gt;<br>int main(void) {<br>printf("Hello, World!\\n");<br>return 0;<br>}<br>EOF<br>riscv64-ruyisdk-linux-gnu-gcc -static hello.c -o hello-gcc | 成功编译 |
| 7 | 编译coremark（GCC）<br>git clone https://github.com/eembc/coremark<br>cd coremark<br>make CC=riscv64-ruyisdk-linux-gnu-gcc XCFLAGS="-static -march=rv64imafdc" compile<br>mv coremark.exe coremark-gcc | 成功编译 |
| 8 | 将GCC构建的二进制传输至开发板<br>PC端：<br>python3 -m http.server 8000<br>开发板minicom端：<br>wget http://10.13.61.37:8000/hello-gcc -O /root/hello-gcc<br>wget http://10.13.61.37:8000/coremark-gcc -O /root/coremark-gcc | 成功传输 |
| 9 | 在开发板端运行Hello World（GCC）<br>chmod +x /root/hello-gcc<br>/root/hello-gcc | 输出Hello, World! |
| 10 | 在开发板端运行CoreMark（GCC）<br>chmod +x /root/coremark-gcc<br>/root/coremark-gcc | 输出coremark结果 |
| 11 | 返回上级目录并退出ruyi GCC虚拟环境(PC)<br>cd ..; ruyi-deactivate | 成功退出虚拟环境 |
| 12 | 创建并激活ruyi虚拟环境（LLVM）<br>ruyi venv -t llvm-ruyisdk generic --sysroot-from gnu-ruyisdk llvm-env<br>. llvm-env/bin/ruyi-activate | 成功创建并激活虚拟环境 |
| 13 | 验证LLVM版本<br>clang -v | 输出版本号 |
| 14 | 编译Hello World（LLVM）<br>cat &lt;&lt; EOF &gt; hello.c<br>#include &lt;stdio.h&gt;<br>int main(void) {<br>printf("Hello, World!\\n");<br>return 0;<br>}<br>EOF<br>clang -static --target=riscv64-linux-gnu -march=rv64imafdc -mabi=lp64d hello.c -o hello-llvm | 成功编译 |
| 15 | 剥离Hello World属性段<br>OBJCOPY=~/tes/k510_buildroot/k510_crb_lp3_v1_2_defconfig/host/bin/riscv64-buildroot-linux-gnu-objcopy<br>if [ ! -f "$OBJCOPY" ]; then<br>OBJCOPY=/opt/riscv64-lp64d--glibc--stable-2025.08-1/bin/riscv64-linux-objcopy<br>fi<br>$OBJCOPY --remove-section=.riscv.attributes hello-llvm hello_llvm_stripped | 生成剥离文件hello_llvm_stripped |
| 16 | 编译coremark（LLVM）<br>cd coremark<br>make clean<br>make CC=clang XCFLAGS="-static --target=riscv64-linux-gnu -march=rv64imafdc -mabi=lp64d -Iposix" compile<br>mv coremark.exe coremark-llvm | 成功编译 |
| 17 | 剥离CoreMark属性段<br>OBJCOPY=~/tes/k510_buildroot/k510_crb_lp3_v1_2_defconfig/host/bin/riscv64-buildroot-linux-gnu-objcopy<br>if [ ! -f "$OBJCOPY" ]; then<br>OBJCOPY=/opt/riscv64-lp64d--glibc--stable-2025.08-1/bin/riscv64-linux-objcopy<br>fi<br>$OBJCOPY --remove-section=.riscv.attributes coremark-llvm coremark_llvm_stripped | 生成剥离文件coremark_llvm_stripped |
| 18 | 将LLVM构建的二进制传输至开发板<br>PC端：<br>python3 -m http.server 8000<br>开发板minicom端：<br>wget http://10.13.61.37:8000/hello_llvm_stripped -O /root/hello_llvm_stripped<br>wget http://10.13.61.37:8000/coremark_llvm_stripped -O /root/coremark_llvm_stripped | 成功传输 |
| 19 | 在开发板端运行Hello World（LLVM）<br>chmod +x /root/hello_llvm_stripped<br>/root/hello_llvm_stripped | 输出Hello, World! |
| 20 | 在开发板端运行CoreMark（LLVM）<br>chmod +x /root/coremark_llvm_stripped<br>/root/coremark_llvm_stripped | 输出coremark结果 |
| 21 | 返回上级目录并退出ruyi LLVM虚拟环境(PC)<br>cd ..; ruyi-deactivate | 成功退出虚拟环境 |