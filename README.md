## OpenIPC for 小米 MJSXJ02HL 标准版 1080p智能摄像头


### 安装

1. 下载[Zadig](https://github.com/muzihuaner/device-mjsxj02hl/blob/master/zadig-2.8.exe). 运行软件并打开完整的设备列表 (`Settings -> List of all devices`).
2. 将摄像头连接到计算机的 USB 端口（套件附带的电线不起作用 - 里面没有数据触点，换数据线）并按下重置按钮，尽快从列表中选择设备HiUSBBurn并安装驱动libusbK程序。可能第一次不会成功（设备在几秒钟后消失，需要非常快地完成所有操作）。
3. 下载 [HiTool](https://github.com/muzihuaner/device-mjsxj02hl/releases/tag/1.0).启动后，选择Hi3518EV300芯片。打开 HiBurn 工具后，选择选择分区表文件（usb-burn.xml）并指定fastboot（u-boot-hi3518ev300-universal.bin）、kernel（uImage.hi3518ev300） 和 rootfs文件（rootfs.squashfs.hi3518ev30）的路径。  
4.点击 烧录 按钮，同意删除某些部分，然后按住重置按钮将摄像头连接到 USB接口。如果正常，刷机过程将开始。需要大约一分钟，弹出成功消弹窗结束。


### 配置

1. 在 SD 卡上创建两个FAT32分区
2.下载仓库并将flash目录内容解压到 SD 卡第一个分区的根目录中。
3. 用文本编辑器打开 `autoconfig/etc/network/interfaces.d/wlan0`文件 填你自己的 [SSID 和password] (默认为 `myssid` 和 `mypassword`).
4. 关闭相机电源，插入SD卡，然后再次打开。如果一切操作正确，过一会儿（1-2 分钟）后，您会听到快门声（有可能不会，白灯等2-3分钟就可以拔下来了），摄像头将连接到您的 Wi-Fi 网络。
5. 重启摄像头电源


### 使用

* 内置 LED 的状态:
    * *橙色* - 系统未加载或 Majestic 未运行
    * *Blue* - 系统已加载且 Majestic 正在运行。
    * *White* - sysupgrade 实用程序正在运行（安装更新或擦除覆盖分区）。
* Web 界面可在端口 85 上访问，网址为http://摄像头IP:85 （可以在路由器里面找）
    * 默认登录名和密码分别为 `root` ， `12345`
* SSH 访问可用ssh root@<camera_ip_address>，默认没有密码。
    * 在 Web 中更改密码后，控制台的密码也会更改。
* Majestic API接口 - https://openipc.org/majestic-endpoints
* 禁用内置 LEDchmod -x /etc/init.d/S00autoled并chmod +x /etc/init.d/S00autoled启用它。
* 禁用自动夜间模式chmod -x /etc/init.d/S96autonight并chmod +x /etc/init.d/S96autonight启用它。
* 要重置设置，请按住重置按钮，打开相机并等待白色 LED 亮起。
* 了解更多 OpenIPC 用法 [Wiki](https://wiki.openipc.org).

### 项目参考

* [MJSXJ02HL application](https://github.com/kasitoru/mjsxj02hl_application)
* [Build tools for mjsxj02hl firmware](https://github.com/kasitoru/mjsxj02hl_firmware)
* [WEB interface for mjsxj02hl firmware](https://github.com/kasitoru/mjsxj02hl_web)
* [mjsxj02hl_uboot](https://github.com/kasitoru/mjsxj02hl_uboot)
* [Прошивка для IP-камеры MJSXJ02HL с поддержкой RTSP и MQTT](https://kasito.ru/mjsxj02hl_firmware/)
* [Прошивка загрузчика IP-камеры MJSXJ02HL с помощью CH341A](https://kasito.ru/proshivka-zagruzchika-ip-kamery-mjsxj02hl-s-pomoshhyu-ch341a/)
* [Прошивка загрузчика IP-камеры MJSXJ02HL с помощью USB](https://kasito.ru/proshivka-zagruzchika-ip-kamery-mjsxj02hl-s-pomoshhyu-usb/)
* [Прошивка загрузчика IP-камеры MJSXJ02HL с помощью MicroSD карты](https://kasito.ru/proshivka-zagruzchika-ip-kamery-mjsxj02hl-s-pomoshhyu-microsd-karty/)

