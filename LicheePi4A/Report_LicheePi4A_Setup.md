# LicheePi4A启动

## 镜像烧写eMMC测试

镜像链接：[Nginx Directory (iscas.ac.cn)](https://mirror.iscas.ac.cn/revyos/extra/images/lpi4a/20240720/)

![](../../images/setup4a1.png)
### 1. 进入烧录模式
上电，安装风扇，按住板上的BOOT按键不放，然后插入 USB-C 线缆上电（线缆另一头接 PC ），即可进入 USB 烧录模式。
在 Windows 下使用设备管理器查看，会出现 “USB download gadget” 设备。
![](../../images/setup4a2.png)
### 2. 禁用驱动程序签名验证

系统-恢复-高级重启-疑难解答-高级选项-安全模式-选择“禁用强制驱动程序签名”
![](../../images/setup4a3.png)
注意：需要查询自己的恢复密钥，在微软账户里

### 3.开始烧录
下载burntools：[百度网盘 (baidu.com)](https://pan.baidu.com/e/1xH56ZlewB6UOMlke5BrKWQ)
编辑 burn_tool.zip 文件夹里面的 `burn_lpi4a.bat` 文件
![](../../images/setup4a4.png)
双击`burn_lpi4a.bat` 文件开始烧录
![](../../images/setup4a5.png)
烧录成功
![](../../images/setup4a6.png)
登录成功
![](../../images/setup4a7.png)