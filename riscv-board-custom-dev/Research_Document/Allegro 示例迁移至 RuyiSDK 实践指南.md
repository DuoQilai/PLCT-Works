# Allegro 示例迁移至 RuyiSDK 环境实践指南

本文档提供 **Allegro 官方图形示例** 迁移至 RuyiSDK 环境的标准化流程，指导开发者将第三方跨平台图形库示例，改造为适配 RuyiSDK 虚拟环境（venv）、支持 RISC-V 架构的可构建/可运行工程，用于扩充 RuyiSDK 官方示例库，验证 RuyiSDK 在图形应用场景的可用性。

# 1. 文档概述

### 1.1 适用范围

本指南适用于 RuyiSDK 开发者、生态贡献者，以 Allegro 5 最小图形示例（Hello Window）为模板，可复用于其他 Allegro 示例的迁移工作，适配 LicheePi 4A/RevyOS 等 RISC-V 硬件平台。

### 1.2 术语定义

|术语|定义|
|---|---|
|Ruyi venv|RuyiSDK 提供的虚拟开发环境，用于隔离工具链、依赖包，确保跨环境构建一致性|
|交叉编译|基于 x86_64 主机，通过 RuyiSDK 工具链编译生成 RISC-V 架构可执行程序|
|Allegro 核心模块|指 Allegro 5 的基础图形、字体组件（allegro-5、allegro-font、allegro-ttf）|

## 2. 前提条件

### 2.1 软件环境

1. 已安装 RuyiSDK v2.0+ 稳定版，且配置环境变量（执行 `ruyi --version` 验证）；

2. 已激活 RuyiSDK 虚拟环境，确认 RISC-V 工具链可用性（执行 `riscv64-unknown-linux-gnu-gcc -v` 验证）；

3. 主机已安装依赖工具：CMake 3.10+、Make、Git、pkg-config；

4. 目标 RISC-V 平台（或仿真环境）已预装 Allegro 5 库及依赖（`allegro5-dev`、`libegl1-mesa-dev`、`libgles2-mesa-dev`）。

### 2.2 硬件环境

- 推荐硬件：LicheePi 4A（RV64 架构，支持图形加速）；
- 备选环境：RISC-V QEMU 仿真环境（需启用图形后端支持）。

## 3. 迁移优势

在 RuyiSDK 示例库扩充场景中，选择 Allegro 而非其他图形 / 多媒体库（如 SDL、SFML），核心基于以下适配价值与场景匹配度优势：

- 示例粒度适配 SDK 教学需求，迁移成本低；
- 文档体系完善，降低适配风险；
-  轻量无冗余，适配 RISC-V 嵌入式场景；
- 构建体系兼容 RuyiSDK 工具链规范

## 4. 迁移原则

为确保迁移后的示例符合 RuyiSDK 生态规范，严格遵循以下原则：

1. 不修改 Allegro 库本身源码，仅适配示例工程构建逻辑与代码适配；
2. 编译流程强制依赖 RuyiSDK 工具链与虚拟环境，杜绝系统级工具链依赖；
3. 构建配置（CMake/Makefile）不硬编码路径，依赖 RuyiSDK 环境变量动态解析；
4. 示例代码保持最小化依赖，仅保留核心图形功能，适配 RISC-V 嵌入式场景。

## 5. 工程结构（RuyiSDK 标准）

迁移后的工程结构严格对齐 RuyiSDK 官方示例库规范，兼顾可读性与可维护性，结构如下：

```Plain Text

allegro-hello/                # 示例工程根目录（小写连字符命名）
├── README.md                 # 标准化文档（本文档）
├── CMakeLists.txt            # RuyiSDK 适配构建脚本
├── main.c                    # 迁移后的核心代码
├── run.sh                    # 一键构建运行脚本（Ruyi venv 集成）
└── platform-notes.md         # 平台适配与故障排查说明
```

## 6. 环境准备

### 6.1 激活 RuyiSDK 虚拟环境

```Bash
# 激活 RuyiSDK 虚拟环境（根据实际安装路径调整脚本路径）
source ${RUYI_SDK_PATH}/scripts/activate-ruyi.sh
# 验证环境激活成功（输出 RuyiSDK 版本信息）
ruyi --version
```

#### 说明

- 必须激活虚拟环境，确保工具链、环境变量（如 `RUYI_SYSROOT`）被正确加载，这是 RuyiSDK 构建的核心前提，避免与系统工具链冲突。

### 6.2 安装依赖库

在 RuyiSDK 虚拟环境中，通过系统包管理器安装 Allegro 依赖（以 RevyOS 为例）：

```Bash
sudo apt update && sudo apt install -y allegro5-dev liballegro5-dev pkg-config
```

#### 说明

- 依赖 `pkg-config` 用于动态解析 Allegro 库路径，符合 RuyiSDK 构建系统“动态依赖”的最佳实践，避免硬编码库路径导致的兼容性问题。

## 7. 示例代码迁移与适配

### 7.1 代码来源与适配逻辑

基于 Allegro 官方示例 `examples/ex_hello.c` 精简适配，核心改造目标：

1. 保留 Allegro 官方标准初始化流程，确保代码规范性；

2. 移除平台相关冗余代码，适配 RISC-V 通用架构；

3. 简化依赖，仅保留核心图形、字体模块，降低迁移复杂度。

### 7.2 适配后代码（main.c）

```C
#include <allegro5/allegro.h>
#include <allegro5/allegro_font.h>
#include <allegro5/allegro_ttf.h>
#include <stdio.h>

int main(void) {
    // 初始化 Allegro 核心库（遵循官方初始化顺序，参考 Getting Started 文档）
    if (!al_init()) {
        fprintf(stderr, "Failed to initialize Allegro core\n");
        return -1;
    }

    // 初始化字体附加组件（依赖核心库初始化完成，顺序不可调整）
    al_init_font_addon();
    al_init_ttf_addon();

    // 创建图形窗口（640x480 分辨率，适配嵌入式图形场景）
    ALLEGRO_DISPLAY *display = al_create_display(640, 480);
    if (!display) {
        fprintf(stderr, "Failed to create Allegro display\n");
        return -1;
    }

    // 加载内置字体（避免依赖外部字体文件，减少迁移依赖）
    ALLEGRO_FONT *font = al_create_builtin_font();
    if (!font) {
        fprintf(stderr, "Failed to load built-in font\n");
        al_destroy_display(display);
        return -1;
    }

    // 绘制内容（黑色背景、白色居中文字，验证图形渲染能力）
    al_clear_to_color(al_map_rgb(0, 0, 0));
    al_draw_text(font, al_map_rgb(255, 255, 255),
                 320, 240, ALLEGRO_ALIGN_CENTER,
                 "Hello from RuyiSDK + Allegro");
    al_flip_display(); // 刷新显示缓冲区，使绘制内容生效（Allegro 渲染必做步骤）

    al_rest(3.0); // 停留 3 秒，便于观察渲染结果

    // 资源释放（遵循“先创建后释放”原则，避免内存泄漏）
    al_destroy_font(font);
    al_destroy_display(display);

    return 0;
}
```

#### 关键适配说明

1. 增加错误日志输出（`fprintf`）：便于 RuyiSDK 环境下调试，解决嵌入式场景无图形界面调试的痛点；
2. 严格遵循 Allegro 官方初始化顺序（核心库 → 附加组件）：参考官方 Getting Started 文档，确保跨平台兼容性；
3. 使用内置字体：避免依赖外部 TTF 文件，减少示例工程的外部依赖，符合 RuyiSDK 示例“独立可运行”的要求。

## 8. CMake 构建脚本适配（CMakeLists.txt）

### 8.1 适配代码

```CMake
cmake_minimum_required(VERSION 3.10)
project(allegro_hello C)

# 配置 C 标准（兼容 RuyiSDK 工具链，选用 C99 通用标准）
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

# 依赖 pkg-config 解析 Allegro 库（遵循 Allegro 官方推荐方式，适配 RuyiSDK 动态依赖机制）
find_package(PkgConfig REQUIRED)
pkg_check_modules(ALLEGRO REQUIRED allegro-5 allegro_font-5 allegro_ttf-5)

# 生成可执行文件
add_executable(${PROJECT_NAME} main.c)

# 链接 Allegro 库与头文件（动态解析路径，避免硬编码）
target_include_directories(${PROJECT_NAME} PRIVATE
    ${ALLEGRO_INCLUDE_DIRS}
)
target_link_libraries(${PROJECT_NAME}
    ${ALLEGRO_LIBRARIES}
)

# 适配 RuyiSDK 交叉编译（传递库路径参数，确保链接正确）
target_compile_options(${PROJECT_NAME} PRIVATE ${ALLEGRO_CFLAGS_OTHER})
```

#### 适配原因说明

1. 明确指定 C 标准为 C99：RuyiSDK 工具链对 C99 支持最完善，同时兼容 Allegro 库的编译要求，避免版本兼容问题；

2. 依赖 `pkg_check_modules` 解析完整组件：不仅解析核心库，还包含字体组件，确保链接无遗漏，符合 RuyiSDK“完整依赖解析”的构建规范；

3. 传递 `ALLEGRO_CFLAGS_OTHER`：自动加载 Allegro 库的额外编译参数，适配 RuyiSDK 交叉编译时的库路径映射，解决跨架构链接问题。

## 9. 一键构建运行脚本（[run.sh](run.sh)）

### 9.1 脚本代码

```Bash
#!/bin/bash
set -euo pipefail  # 开启严格模式，捕获错误并退出，符合 RuyiSDK 脚本规范

# 检查 RuyiSDK 虚拟环境是否激活
if [ -z "${RUYI_SYSROOT:-}" ]; then
    echo "Error: RuyiSDK 虚拟环境未激活，请先执行 source ${RUYI_SDK_PATH}/scripts/activate-ruyi.sh"
    exit 1
fi

# 创建构建目录（隔离构建产物，符合 RuyiSDK 工程化规范）
mkdir -p build && cd build

# 调用 CMake 配置构建（指定 RuyiSDK 工具链与 sysroot）
cmake .. \
    -DCMAKE_C_COMPILER=riscv64-unknown-linux-gnu-gcc \  # RuyiSDK 标准 RV64 工具链前缀
    -DCMAKE_CXX_COMPILER=riscv64-unknown-linux-gnu-g++ \
    -DCMAKE_SYSROOT="${RUYI_SYSROOT}" \  # 关联 RuyiSDK 系统根目录，确保依赖解析正确
    -DCMAKE_BUILD_TYPE=Release

# 编译工程（使用多线程加速，适配 RuyiSDK 工具链性能优化）
make -j$(nproc)

# 运行示例程序
echo "=== 启动 Allegro 示例程序 ==="
./allegro_hello
```

#### 核心设计逻辑

1. 增加环境检查：避免用户未激活虚拟环境导致构建失败，符合 RuyiSDK 脚本“前置校验”的设计习惯；

2. 显式指定 RuyiSDK 工具链：使用官方标准工具链前缀 `riscv64-unknown-linux-gnu-`，确保与虚拟环境工具链一致，杜绝系统工具链干扰；

3. 关联 `RUYI_SYSROOT`：让 CMake 从 RuyiSDK 系统根目录解析依赖，而非系统路径，符合 RuyiSDK“隔离构建”的核心原则。

## 10. 平台适配与故障排查（[platform-notes.md](platform-notes.md)）

### 10.1 测试平台信息

- 硬件平台：LicheePi 4A（RV64 架构，配备 Mali-G52 GPU）

- 系统环境：RevyOS（基于 Debian，适配 RISC-V 图形栈）

- 图形后端：依赖系统 EGL/GLES 驱动，需确保 GPU 驱动正常加载

### 10.2 常见故障排查

1. 窗口创建失败（`Failed to create Allegro display`）

    - 原因：图形后端未启用或 GPU 驱动异常；

    - 解决方案：执行 `glxinfo | grep "OpenGL ES"` 验证 GLES 支持，重新安装 `mesa-utils-extra` 修复图形栈。

2. 库链接错误（`undefined reference to al_init`）

    - 原因：Allegro 库未正确解析，或 pkg-config 路径异常；

    - 解决方案：在 Ruyi 虚拟环境中执行 `pkg-config --cflags --libs allegro-5`，确认输出正常路径。

3. 工具链找不到（`riscv64-unknown-linux-gnu-gcc: command not found`）

    - 原因：Ruyi 虚拟环境未激活，或环境变量配置错误；

    - 解决方案：重新激活虚拟环境，检查 `PATH` 变量是否包含 `${RUYI_SDK_PATH}/bin`。



## 附录：参考资源

本迁移流程严格遵循 Allegro 官方规范，参考以下资源确保兼容性与标准性：

| 资源类型 | 名称                            | 链接                                                         | 用途                                                   |
| -------- | ------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------ |
| 源码仓库 | Allegro 5 GitHub 仓库           | [https://github.com/liballeg/allegro5](https://github.com/liballeg/allegro5) | 示例代码来源（`examples/ex_hello.c`）                  |
| 入门指南 | Allegro 5 Getting Started Guide | [https://allegro5.org/docs/html/refman/getting_started.html](https://allegro5.org/docs/html/refman/getting_started.html) | 遵循官方初始化流程（`al_init()`、组件加载顺序）        |
| API 文档 | Allegro API Reference           | [https://liballeg.org/api.html](https://liballeg.org/api.html) | 确认 `ALLEGRO_DISPLAY`、`al_draw_text` 等 API 标准用法 |
| 官方主页 | Allegro 官方网站                | [https://liballeg.org/](https://liballeg.org/)               | 验证库特性与依赖关系                                   |
