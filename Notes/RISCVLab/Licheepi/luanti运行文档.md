# LicheePi4A_Luanti

#### 1. 安装依赖
```bash
sudo apt update
sudo apt install g++ make libc6-dev cmake git
sudo apt install libpng-dev libjpeg-dev libsqlite3-dev libogg-dev libvorbis-dev libopenal-dev libcurl4-gnutls-dev zlib1g-dev libgmp-dev libjsoncpp-dev libzstd-dev libluajit-5.1-dev gettext libgles2-mesa-dev libsdl2-dev libgles2-mesa-dev libsdl2-dev
```

#### 2. github 加速
```bash
printf '140.82.121.3 github.com\n185.199.108.153 assets-cdn.github.com\n' | sudo tee -a /etc/hosts > /dev/null
sudo /etc/init.d/networking restart
```

#### 3. 安装 gl4es
```bash
git clone https://github.com/ptitSeb/gl4es
cd gl4es
mkdir build
cd build 
cmake .. -DCMAKE_BUILD_TYPE=RelWithDebInfo
make -j$(nproc)
```

#### 4. 获取项目源码
#### 使用 git 获取源码
```bash
git clone --depth 1 https://github.com/luanti-org/luanti
cd luanti
```
#### 使用 wget 获取源码
```bash
wget https://github.com/luanti-org/luanti/archive/master.tar.gz
tar xf master.tar.gz
cd luanti-master
```

#### 5. 编译项目
#### CMake 添加编译选项
```bash
mkdir build
cd build
cmake .. -DUSE_SDL2=ON -DENABLE_OPENGL=OFF -DENABLE_GLES2=ON -DRUN_IN_PLACE=TRUE -DENABLE_OPENGL3=OFF
make -j$(nproc)
```

#### 6. 创建启动脚本 run.sh
``` bash
#!/bin/bash

export LIBGL_FB=1
export LIBGL_SHRINK=1
export LIBGL_ES=2
export LIBGL_GL=21
export LIBGL_ALWAYS_SOFTWARE=1
export LIBGL_EGL=1
export LIBGL_NOVULKAN=1
export LIBGL_NODRI=1

export MESA_LOADER_DRIVER_OVERRIDE=swrast
export GALLIUM_DRIVER=softpipe

export LD_LIBRARY_PATH="path/to/gl4es/lib/:$LD_LIBRARY_PATH"
path/to/luanti/bin/luanti
```

#### 7. 运行游戏
```bash
sudo chmod +x run.sh
./run.sh
```

#### 8. 运行非常卡顿，需要硬件加速，实验成功过一次，硬件配置正确可以流畅运行，目前还在探索中