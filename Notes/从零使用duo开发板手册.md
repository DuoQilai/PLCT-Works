# 从零使用duo开发板手册
## 1.购买所需研发物料

【必须的装备】duo、电烙铁、锡线、剪刀、1*20p排针 *2、sd卡、切割垫板、USB to TTL线、tap-c线、面包板、跳线数干、杜邦线数干

【购买流程】批量购买需要先在晶姐处报备后在京东购买

【其他配件】确认需要验证的帖子需要的配件，按需购买

## 2.焊接

【用到的工具】duo、电烙铁、锡线、1*20p排针 *2、吸锡器（可选）、吸锡线（可选）

【焊接排针】安装后，首先焊接两边的针脚便于调整位置，再全部焊接。

【注意事项】保持室内通风，注意安全，如对自己没有信心可花10元找楼下电器维修的大哥帮助

## 3.参考资料

[Milk-V Duo 相关资料合集 - Duo - MilkV Community](https://community.milkv.io/t/milk-v-duo/33)

包含Board、Docker、GitHub、Docs、SDK

### Board

https://developer-assets.sophon.cn/sophon-developer-prod-s3/thread-attachment/23/05/12/19/CV180xB_QFN68.zip

包含一些硬件指南，如：CV180xB_CV180xC_VI 接口场景详细说明、CV180xB_38板硬件指南_V1.0、CV180xB_EVB板硬件指南_V1.0、EVB开发板 SCH&PCB位号图

### Docker

https://hub.docker.com/repository/docker/dreamcmi/cv1800-docker/general

算能科技CV1800系列SDK编译环境，包括下载地址和使用方法

### GitHub

[milk-v/duo-manifest (github.com)](https://github.com/milk-v/duo-manifest)

已存档，新链接：[milkv-duo/duo-buildroot-sdk: Milk-V Duo Official buildroot SDK (github.com)](https://github.com/milkv-duo/duo-buildroot-sdk)

环境搭建方法

### Docs

[🍐 Duo | Milk-V (milkv.io)](https://milkv.io/docs/duo/)

硬件参数、环境搭建、烧录方法

### SDK

https://developer.sophgo.com/thread/471.html

CV181x/CV180x MMF SDK 开发文档汇总

### 论坛

[Sophgo](https://forum.sophgo.com/)

环境搭建方法、体验文档、技术分享

## 4.复现视频教程

这是一个Milk-V Duo开箱视频_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1br4y1d763/
【Milk-v duo】 尝试串行控制台登录+复现RJ45扩展版联网+USB联网_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1Z14y1C7cW/
【Milk-v duo】 尝试串行控制台登录+复现RJ45扩展版联网+USB联网_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1Z14y1C7cW/
【Milk-v duo】 测试通过VLC显示CAM-GC2083摄像头拍摄画面_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV188411v7tc/
【Milk-v duo】 duo简介和开发环境搭建_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1PF411S7To/
【Milk-v duo】 在duo中开启 Swap虚拟内存的方法_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV18841167gs/
【Milk-v duo】 基于Milk-v duo和Densenet的图像分类_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1BN4y1k7Z1/
【Milk-v duo】 基于Milk-v duo和Squeezenet的图像分类_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1sN41137ot/
【Milk-v duo】 基于Milk-v duo和Resnet18的图像分类_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1zj411a7Ka/
【Milk-v duo】 基于Milk-v duo和YOLOv5的目标检测_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1iG41197qa/
【Milk-v duo】 使用Milk-v duo驱动DF9GMS微型舵机_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1Dj411E7yD/
【Milk-v duo】 基于Milk-v duo和ShuffleNetV2的图像分类_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1bu4y1j7yG/
【Milk-v duo】Duo USB&Ethernet IO-Board简介和使用方法_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1Ga4y1Z7oM/
【Milk-v duo】 使用Milk-v duo驱动DHT22温湿度传感器_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1uG411S7cz/

【Milk-V Duo】 通过大核控制小核点亮 LED_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1nH4y1y7CM/
【Milk-V Duo】 Milk-V Duo 交叉编译SQLite3_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1FN4y147Wm/
【Milk-V Duo】基于 Googlenet 的图像分类_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1Wt4y1Z7uQ/
【Milk-V Duo】 复现SPI驱动点亮屏幕(st7789)_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1Uw41177BX/
【Milk-V Duo】Buildroot SDK简介和编译镜像的方法_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1J2421K7xz/
【Milk-V Duo】配置Docker开发环境_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1gK411h7YP/
【Milk-V Duo】使用 pinpong 库实现 Duo 板载 LED 闪烁_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1QB421674a/
开箱！Milk-V 的新年礼！_哔哩哔哩_bilibili
【Milk-V Duo】 使用 Arduino 开发Milk-V Duo_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1ft42147ad/
【Milk-V Duo】TDL SDK 简介和编译方法_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1J2421K7xz/
【Milk-V Duo】复现在小核上运行Zephyr OS_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1uK421Y7x9/
【Milk-V Duo】基于TDL SDK实现YOLOv5 目标检测_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1Vw4m1U71C/
【Milk-V Duo】在Duo 上运行ThreadX_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1yi421C7SK/
【Milk-V Duo】引脚复用配置方法_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1nH4y1u7zX/
【Milk-V Duo S】Duo S 启动！_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1Bm421N72y/
【Milk-V Duo S】在Duo S运行故事机baby llama2_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1dn4y197UW/
【Milk-V Duo S】在 Duo S 上使用 TDL SDK 高效部署人脸检测模型_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1AM4m1m7fe/
【Milk-V Duo S】使用Wi-Fi连接Duo S_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV11r421T7Sk/
【Milk-V Duo】wiringX简介和配置开发环境_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1jr421K7yk/