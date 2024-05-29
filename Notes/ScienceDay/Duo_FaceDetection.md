# 在Milk-V Duo 实现人脸检测使用说明

## 准备

- Duo
- 大于 1GB 的 microSD 卡
- Type-C 数据线
- CAM-GC2083
- 排线

## 硬件连接

硬件连接的方法

![](Notes/ScienceDay/images/camera1.png)

## USBnet设置

### Windows

1.通过Type-C线将Duo与电脑连接。

2."RNDIS" 设备出现在设备管理器中。

![](Notes/ScienceDay/images/camera3.png)

3.选择 "RNDIS "并右键单击以更新驱动程序。

![](Notes/ScienceDay/images/camera4.png)

4.选择 "Browse my computer for drivers"

![](Notes/ScienceDay/images/camera5.png)

5.选择 "Let me pick from a list of available drivers on my computer"

![](Notes/ScienceDay/images/camera6.png)

6.选择 "Network adapters"

![](Notes/ScienceDay/images/camera7.png)

7.Manufacturer/Model: Microsoft/USB RNDIS Adapter

![](Notes/ScienceDay/images/camera8.png)

8.忽略警告信息

![](Notes/ScienceDay/images/camera9.png)

9.驱动程序更新成功

![](Notes/ScienceDay/images/camera10.png)

10.检查 "USB RNDIS Adapter"

![](Notes/ScienceDay/images/camera11.png)

11.找到IP并使用ping来测试网络

![](Notes/ScienceDay/images/camera12.png)

## SSH

1.打开终端，输入 **ssh root@192.168.42.1**, 并回答是

![](Notes/ScienceDay/images/camera13.png)

2.输入密码 **milkv** (密码将不显示在屏幕上)

![](Notes/ScienceDay/images/camera14.png)

3.登陆成功

![](Notes/ScienceDay/images/camera15.png)

## 软件测试

该测试仅用来测试摄像头是否能正常工作，在Duo上运行测试程序推流，在PC端用VLC播放器拉流。

首先确保可以通过USB网络(RNDIS)正常ssh到Duo设备。默认固件ssh的用户名和密码分别是`root/milkv`。

最新的固件已经集成了测试程序

登陆到 Duo 终端：

```bash
ssh root@192.168.42.1
```

执行测试程序推流：

```bash
camera-test.sh
```

正常情况下，终端最后会看到如下日志：

```{8}
Bind VI with VPSS Grp(0), Chn(0)
Attach VBPool(0) to VPSS Grp(0) Chn(0)
Attach VBPool(1) to VPSS Grp(0) Chn(1)
Initialize VENC
venc codec: h264
venc frame size: 1280x720
Initialize RTSP
rtsp://127.0.1.1/h264
prio:0
anchor:-8,-8,8,8
anchor:-16,-16,16,16
bbox:bbox_8_Conv_dequant
landmark:kps_8_Conv_dequant
score:score_8_Sigmoid_dequant
anchor:-32,-32,32,32
anchor:-64,-64,64,64
bbox:bbox_16_Conv_dequant
landmark:kps_16_Conv_dequant
score:score_16_Sigmoid_dequant
anchor:-128,-128,128,128
anchor:-256,-256,256,256
bbox:bbox_32_Conv_dequant
landmark:kps_32_Conv_dequant
score:score_32_Sigmoid_dequant
Enter TDL thread
Enter encoder thread
0 R:1165 B:3087 CT:2688
1 R:1464 B:2327 CT:3937
2 R:1974 B:1613 CT:7225
Golden 1464 1024 2327
```

注意 rtsp: 开头的链接，把 IP 改成 Duo 的 IP 就是我们要在 VLC 中拉流的地址了。

在PC上打开VLC播放器，菜单“媒体”中选择“打开网络串流”，选择“网络”标签，在“请输入网络URL”中输入：

```text
rtsp://192.168.42.1/h264
```

点开左下角的 `显示更多选项`，可以设置 `缓存` 的值来调整延时，默认是1000毫秒，也就是1秒。网络环境较好时比如在局域网内，可以将其调低来降低延迟，可以设置为100到300。如果网络环境较差或者画面出现卡顿时，可以尝试将其调高。

![](Notes/ScienceDay/images/camera16.png)

再点”播放“，就可以看到摄像头推流的画面了：

![](Notes/ScienceDay/images/camera2.png)

此时用摄像头对准人脸，Duo 终端中会打印摄像头实时检测到的人脸个数：

```text
face count: 5
face count: 6
face count: 5
face count: 4
face count: 0
face count: 1
face count: 0
```
