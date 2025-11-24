# LicheePi 4A 镜像刷写教程 (Windows)

## 从 eMMc 启动

### 硬件准备
- LicheePi 4A 开发板 × 1
- Type-C 数据线 × 1

### 软件准备：
#### 1.Fastboot 工具
**下载方式一**
[点击这里下载 Android Platform Tools](https://developer.android.com/studio/releases/platform-tools) 
包含 `fastboot.exe` 和 `adb.exe`

**下载方式二：**
您可以使用类似 Everything 的索引工具查找电脑上是否已安装了 `fastboot.exe`。

**检查方法：**
```powershell
# 在命令行中检查 fastboot 版本
fastboot --version
```

如果没有安装 fastboot 或者版本低于 34，可使用以下命令安装最新版本：

```powershell
# 使用 Windows Package Manager 安装最新版 fastboot
winget install google.platformtools
```

**注意：** 过低版本的 fastboot 刷写最新镜像可能会出现异常。

#### 2.系统镜像文件
需要下载以下文件：
- **u-boot 文件** (`u-boot-with-spl.bin`)
- **boot 文件** (`boot.ext4`)
- **root 文件** (`root.ext4`)

**下载地址：**  
##### 系统镜像下载
从以下链接下载 LicheePi 4A 的系统镜像：
- **RevyOS 20240720（5.10 内核）**  
  下载地址：https://fast-mirror.isrc.ac.cn/revyos/extra/images/lpi4a/20240720/
- **最新版本 20251030（6.6 内核）**  
  下载地址：https://fast-mirror.isrc.ac.cn/revyos/extra/images/lpi4a/20251030/

##### 内核版本说明
**RevyOS 20240720（5.10 内核）**  
- 5.10 内核处于较为成熟的状态
- 在视频编解码以及各种应用上表现更加稳定
- **推荐新手使用**

**最新版本 20251030（6.6 内核）**  
- 6.6 内核可能会出现一些未知问题
- 已知问题：视频方面卡顿、USB 失去供电等
- 目前正在修复中
- **建议有经验的用户测试使用**

#### 3. Google USB 驱动
**下载地址：**  
[Google USB Driver](https://dl.google.com/android/repository/usb_driver_r13-windows.zip)

### 刷写镜像
#### 第一步：连接设备进入刷写模式
1. 将 **靠近 BOOT 键的 Type-C 接口** 连接到电脑。
2. 按住开发板上的 **BOOT** 按键不松开，同时按一下reset键。

#### 第二步：在设备管理器中识别设备
1. 在 Windows 开始菜单徽标上单击鼠标 **右键**。
2. 选择 **设备管理器**。
3. 在设备管理器列表中，展开 **其他设备**。
4. 如果看到 **USB download gadget** 设备，并且带有黄色的感叹号，则表示设备已被识别但未安装驱动程序。

#### 第三步：安装 Google USB 驱动
1. 在 **USB download gadget** 设备上单击鼠标 **右键**。
2. 选择 **更新驱动程序**。
3. 在弹出的窗口中，选择 **“浏览我的电脑以查找驱动程序”**。
4. 接着选择 **“让我从计算机上的可用驱动程序列表中选取”**。
5. 勾选 **“显示所有设备”**，然后点击 **“下一步”**。
6. 点击 **“从磁盘安装...”** 按钮。
7. 在弹出的窗口中点击 **“浏览”**。
8. 导航到您之前解压 **Google USB 驱动** 的文件夹，找到并选中 `android_winusb.inf` 文件，然后点击 **“确定”**。
9. 在驱动程序列表中，选择 **Android Bootloader Interface**，然后点击 **“下一步”**。
10. 系统可能会弹出确认对话框，请点击 **“是”**。
11. 随后可能会弹出 **Windows 安全中心** 对话框，提示正在安装驱动，请点击 **“安装”**。
12. 等待安装完成，提示成功后，驱动即安装完毕。

若上述步骤出现问题，请回到设备管理器找到该设备，点击 **卸载驱动程序**，然后重新插拔开发板并重试。

#### 第四步：进入 Fastboot 环境并刷写镜像
1. 进入 Fastboot 环境并验证设备连接
```powershell
.\fastboot.exe devices
```
预期结果：？       fastboot

2. 刷写并重启至临时 U-Boot
```powershell
.\fastboot.exe flash ram .\u-boot-with-spl-lpi4a-16g.bin
.\fastboot.exe reboot
```
注意：请将文件路径替换为您的板卡规格对应的实际 U-Boot 文件路径。

3. 重新安装驱动（如需要）
开发板重启后，如果设备管理器再次出现 "USB download gadget" 未知设备，请按照驱动安装教程重新安装 Fastboot 驱动。

4. 刷写系统镜像
确保设备被正确识别后，依次执行以下命令：
```powershell
.\fastboot.exe flash uboot u-boot-with-spl-lpi4a-16g.bin
.\fastboot.exe flash boot boot-lpi4a-20240720_171951.ext4
.\fastboot.exe flash root root-lpi4a-20240720_171951.ext4
```
重要提示：请将文件路径替换为您的板卡规格对应的实际文件路径。

**刷写时间说明**
uboot 和 boot 分区刷写较快。
root 分区刷写约需 5 分钟。

**关键检查点**
刷写 root 文件时，如数据块数量异常（2000+ 或 3000+），说明操作有误，需要重新刷写。

-完成启动
所有镜像刷写完成后，通过重新拔插开发板电源线来正常启动系统。