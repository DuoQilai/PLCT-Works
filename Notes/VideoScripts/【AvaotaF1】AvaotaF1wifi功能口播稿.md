
大家好，我是谁说现在是冬天呢，今天我们尝试使用avaota这块板子的wifi功能

第一个功能就是联网

输入wifi -o sta，设置 `Wi-Fi` 为 `STATION` 模式

输入wifi -s，扫描当前网络环境的 Wi-Fi 站点

输入 wifi -c ssid 密码 连接Wi-Fi

完成后输入 ifconfig 即可查看当前 ip 地址

可以使用 `ping` 命令测试 网络连接
输出以下内容说明网络是通的
连接wifi之后打开ssh，你就可以用终端工具进行ssh连接你的avaotaf1了

输入 wifi -d 可以断开Wi-Fi

第二个功能是建立 AP

输入 wifi -o ap v821 12345678 可以创建热点
然后打开你的手机然后就可以扫描到 Wi-Fi 了，输入密码 12345678 进行连接

感谢观看～
