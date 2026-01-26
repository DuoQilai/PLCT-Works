### Ruyi 工具安装
```bash
ruyi update

ruyi install gnu-milkv-milkv-duo-bin qemu-user-riscv-upstream
```

### 创建虚拟环境
为了演示环境切换
``` bash
ruyi venv -t gnu-milkv-milkv-duo-bin generic milkv-glibc-venv

ruyi venv -t gnu-milkv-milkv-duo-bin -e qemu-user-riscv-upstream generic milkv-duo-qemu
```

### 下载编译项目
``` bash
git clone --recursive https://github.com/cuberite/cuberite.git

cd cuberite && mkdir build && cd build

cd cuberite/lib/lua/src
make linux
export PATH=~/ruyi-test/cuberite/lib/lua/src:$PATH

cmake ..  -DCMAKE_TOOLCHAIN_FILE=~/ruyi-test/milkv-glibc-venv/toolchain.cmake

make -j$(nproc)
```

### (可选)模拟运行
``` bash
cd cuberite
ruyi-qemu ./build/Server/Cuberite
```

### 上传板子
``` bash
zip -r cuberite.zip cuberite
scp ./cuberite.zip debian@172.16.60.118:/home/debian/
```

### Milkv Duo S安装Debian镜像
安装方式参考链接：https://matrix.ruyisdk.org/zh-CN/reports/Duo_S-Debian-README/

```bash 
wget https://github.com/scpcom/sophgo-sg200x-debian/releases/download/v1.6.35/duos-e_sd.img.lz4
lz4 -dk duos-e_sd.img.lz4
sudo dd if=duos-e_sd.img of=/dev/sdX bs=1M status=progress
```

### 启动服务
```bash
cd cuberite/build/Server
./Cuberite
```