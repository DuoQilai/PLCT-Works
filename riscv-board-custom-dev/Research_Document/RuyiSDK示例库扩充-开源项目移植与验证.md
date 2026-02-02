# RuyiSDK开源项目移植与验证


---

## 1. 项目背景与目标

### 1.1 核心痛点
当前 RISC-V 开发面临两大难题：
* **环境碎片化**：工具链版本乱，配置难。
* **上手门槛高**：缺乏标准化的验证环境。

### 1.2 项目目标
基于 **RuyiSDK** ：
* **标准化**：统一编译与运行环境。
* **可复现**：无需开发板，让开发者能一键跑通开源库。

---

## 2. 核心技术路线 (四步闭环)

### 1️⃣ 步骤一：环境供给
* **操作**:`ruyi install` 装工具，`ruyi venv` 建环境。
* **价值**：告别手动下载配置，由 Ruyi 统一管理版本。
* **验证**：确保 GCC/LLVM 与目标架构精准匹配。

### 2️⃣ 步骤二：构建 (Build)
* **操作**：在 Ruyi 虚拟环境内交叉编译。
* **价值**：环境隔离，防止宿主机污染。
* **解决**：彻底解决“在我电脑上能跑”的问题。


### 4️⃣ 步骤三：验证 (Verification)
* **操作**：运行脚本，捕获输出。
* **标准**：无物理板，仅用 QEMU 成功输出预期结果。

---

## 3. 可行性

### 3.1 技术可行性
* **Ruyi 成熟度**：虚拟环境功能已完善，工具链功能强大。
* **QEMU模拟器 支持**:RISC-V 用户模式支持良好。

### 3.2 传播可行性 (视频化)
* **结构清晰**：安装 -> 编译 -> 运行，线性流畅。
* **短平快**：适合 5-10 分钟实战演示。

### 3.3 实践
* **有过相关内容实践**:在自己电脑上通过RuyiSDK工具链和QEMU模拟器实现过zlib-ng项目的实战

---

## 4. 计划实战项目库

### 4.1 跑分工具：CoreMark

* **源码获取**：
    ```bash
    git clone [https://github.com/eembc/coremark.git](https://github.com/eembc/coremark.git)
    cd coremark
    ```
* **Ruyi 环境准备**：
    ```bash
    source generic-riscv64-venv/bin/ruyi-activate
    ```
* **构建命令 (Build)**：
    ```bash
    # 使用 Ruyi 环境中的编译器直接编译单文件版本
    $CC -O3 -I. -DPERFORMANCE_RUN=1 -DITERATIONS=1000 core_list_join.c core_main.c core_matrix.c core_state.c core_util.c riscv64/core_portme.c -o coremark_riscv.elf
    ```
* **验证命令 (Verification)**：
    ```bash
    qemu-riscv64 coremark_riscv.elf
    ```
* **预期效果**：终端打印出具体的 `CoreMark 1.0 : [分数]`，视频结尾定格在分数上非常有成就感。

---

### 4.2 算法可视化：ASCII Mandelbrot

* **源码获取**：
    ```bash
    wget [https://raw.githubusercontent.com/wizzard0/mandelbrot/master/mandelbrot.c](https://raw.githubusercontent.com/wizzard0/mandelbrot/master/mandelbrot.c)
    ```
* **Ruyi 环境准备**：
    ```bash
    source generic-riscv64-venv/bin/ruyi-activate
    ```
* **构建命令 (Build)**：
    ```bash
    $CC -O2 mandelbrot.c -o mandelbrot_riscv
    ```
* **验证命令 (Verification)**：
    ```bash
    qemu-riscv64 mandelbrot_riscv
    ```
* **预期效果**：终端屏幕被字符组成的复杂分形图案填满，体现浮点运算能力。

---


### 4.3 轻量级数据处理：cJSON

* **源码获取**：
    ```bash
    git clone [https://github.com/DaveGamble/cJSON.git](https://github.com/DaveGamble/cJSON.git)
    cd cJSON
    ```
* **Ruyi 环境准备**：
    ```bash
    source generic-riscv64-venv/bin/ruyi-activate
    ```
* **构建命令 (Build)**：
    ```bash
    $CC -c cJSON.c -o cJSON.o
    $CC test.c cJSON.o -o cjson_test_riscv -lm
    ```
* **验证命令 (Verification)**：
    ```bash
    qemu-riscv64 cjson_test_riscv
    ```
* **预期效果**：终端打印出构建 JSON 对象和解析 JSON 字符串的详细日志。

---


### 4.4 视觉特效：Donut.c (旋转甜甜圈)

* **源码获取**：
    ```bash
    wget [https://www.a1k0n.net/code/donut.c](https://www.a1k0n.net/code/donut.c)
    ```
* **Ruyi 环境准备**：
    ```bash
    source generic-riscv64-venv/bin/ruyi-activate
    ```
* **构建命令 (Build)**：
    ```bash
    # 必须链接数学库 (-lm)，这是验证工具链标准库链接功能的经典案例
    $CC donut.c -o donut_riscv -lm
    ```
* **验证命令 (Verification)**：
    ```bash
    qemu-riscv64 donut_riscv
    ```
* **预期效果**：终端屏幕中心出现一个由 ASCII 字符组成的旋转甜甜圈，动画流畅，能够直观感受到 QEMU 对浮点指令的模拟效率。

---

### 4.5 移动交互：QR Code Generator (二维码生成)

* **源码获取**：
    ```bash
    git clone [https://github.com/nayuki/QR-Code-generator.git](https://github.com/nayuki/QR-Code-generator.git)
    cd QR-Code-generator/c
    ```
* **Ruyi 环境准备**：
    ```bash
    source generic-riscv64-venv/bin/ruyi-activate
    ```
* **构建命令 (Build)**：
    ```bash
    # 编译演示程序，验证 C99 标准支持
    $CC -std=c99 qrcodegen.c qrcodegen-demo.c -o qr_riscv
    ```
* **验证命令 (Verification)**：
    ```bash
    qemu-riscv64 qr_riscv
    ```
* **预期效果**：终端打印出由“#”字符组成的二维码图案，手机相机扫描屏幕即可准确识别内容。


---

### 4.6 经典游戏：Micro Tetris (微型俄罗斯方块)

* **源码获取**：
    ```bash
    git clone [https://github.com/skraxinger/micro-tetris.git](https://github.com/skraxinger/micro-tetris.git)
    cd micro-tetris
    ```
* **Ruyi 环境准备**：
    ```bash
    source generic-riscv64-venv/bin/ruyi-activate
    ```
* **构建命令 (Build)**：
    ```bash
    # 极简编译，验证基本的逻辑控制
    $CC -O2 tetris.c -o tetris_riscv
    ```
* **验证命令 (Verification)**：
    ```bash
    qemu-riscv64 tetris_riscv
    ```
* **预期效果**：出现经典的方块游戏界面，通过 `j/k/l` 键或方向键控制移动变形，画面刷新无撕裂。

---

### 4.7 极简 AI：Genann 

* **源码获取**：
    ```bash
    git clone [https://github.com/codeplea/genann.git](https://github.com/codeplea/genann.git)
    cd genann
    ```
* **Ruyi 环境准备**：
    ```bash
    source generic-riscv64-venv/bin/ruyi-activate
    ```
* **构建命令 (Build)**：
    ```bash
    # 编译 XOR 训练示例
    $CC -O2 example/xor.c genann.c -o xor_riscv -lm
    ```
* **验证命令 (Verification)**：
    ```bash
    qemu-riscv64 xor_riscv
    ```
* **预期效果**：终端快速滚动打印训练过程中的 Loss 下降数据，最终输出准确的预测概率（如 `Output for [0, 1] is 0.99`）。

---

### 4.8 数据交换：cJSON

* **源码获取**：
    ```bash
    git clone [https://github.com/DaveGamble/cJSON.git](https://github.com/DaveGamble/cJSON.git)
    cd cJSON
    ```
* **Ruyi 环境准备**：
    ```bash
    source generic-riscv64-venv/bin/ruyi-activate
    ```
* **构建命令 (Build)**：
    ```bash
    # 编译对象文件与测试程序
    $CC -c cJSON.c -o cJSON.o
    $CC test.c cJSON.o -o cjson_test_riscv -lm
    ```
* **验证命令 (Verification)**：
    ```bash
    qemu-riscv64 cjson_test_riscv
    ```
* **预期效果**：终端清晰打印出构建 JSON 对象的层级结构，以及解析 JSON 字符串后的键值对日志。

## 5. 结论

该项目既验证了 RuyiSDK 的易用性，又输出了教学内容。
