
### 1. Milkv Duo S安装Debian镜像
安装方式参考链接：https://matrix.ruyisdk.org/zh-CN/reports/Duo_S-Debian-README/

#### 准备SD卡和读卡器写入镜像
```bash 
wget https://github.com/scpcom/sophgo-sg200x-debian/releases/download/v1.6.35/duos-e_sd.img.lz4
lz4 -dk duos-e_sd.img.lz4
sudo dd if=duos-e_sd.img of=/dev/sdX bs=1M status=progress
```
#### 串口登录
用户名 debian
密码 rv

#### 连接wifi
```bash
touch /boot/wifi.sta

vim /boot/wifi.ssid
// 输入wifi名称 “My WiFi”

vim /boot/wifi.pass
// 输入wifi密码 “password”
```

#### 安装依赖
```bash
sudo apt update
sudo apt install git build-essential cmake
```

### 2. 编译安装Cuberite
克隆项目
```bash
git clone --recursive https://github.com/cuberite/cuberite.git
```

#### 编译项目
```bash
mkdir build
cd build
cmake ..
make -j$(nproc)
```

#### 启动服务
```bash
./build/Server/Cuberite
```
```text
启动服务之后可以在局域网中监听服务
假设板子的ip地址是192.168.0.1 
主机浏览器可以直接访问 192.168.0.1:8080
可以看到服务器设置和状态
```

### 3. 主机连接游戏
#### 本地主机下载Java版MineCraft
推荐开源MineCraft启动器 HMCL
直接下载游戏

#### 启动游戏
点击 多人游戏-直接连接-输入服务器ip地址

此时可以加入服务器，游戏体验比较流畅