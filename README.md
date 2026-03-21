## 适用于小米 MJSXJ02HL 的 OpenIPC



### 安装



1. 下载最新版本的[Zadig](https://zadig.akeo.ie/)程序。运行它并打开设备的完整列表（`Settings -> List of all devices`）。
2. 将相机连接到电脑的 USB 端口（套件中附带的连接线无法使用，因为它没有数据触点），同时按住重置按钮，`HiUSBBurn`尽快从设备列表中选择该设备并安装`libusbK`驱动程序。很可能第一次不会成功（设备会在几秒钟后消失，所以您需要快速操作）。
3. 下载[HiTool](http://www.hihope.org/en/download/download.aspx?mtt=36)程序。启动后，选择`Hi3518EV300`芯片。打开 HiBurn 工具，选择[分区表文件](https://raw.githubusercontent.com/OpenIPC/device-mjsxj02hl/master/usb-burn.xml)，并指定[fastboot](https://github.com/OpenIPC/firmware/releases/download/latest/u-boot-hi3518ev300-universal.bin)、[kernel 和 rootfs](https://github.com/OpenIPC/firmware/releases/download/latest/openipc.hi3518ev300-nor-lite.tgz)文件的路径。
4. 按下`Burn`按钮，同意清除部分数据，然后按住重置按钮，将相机连接到 USB 接口。如果一切操作正确，刷机过程将开始。此过程通常需要大约一分钟，完成后会显示成功提示信息。

### 配置



1. 在 SD 卡上创建两个FAT32分区

2. [下载](https://github.com/OpenIPC/device-mjsxj02hl/archive/refs/heads/master.zip)此存储库并将**flash目录中的内容**解压到 SD 卡第一个分区的**根目录**。

3. 使用[Notepad++](https://notepad-plus-plus.org/)打开文件，将Wi-Fi 接入点的[SSID 和密码](https://github.com/OpenIPC/device-mjsxj02hl/blob/master/flash/autoconfig/etc/network/interfaces.d/wlan0#L14)

   `autoconfig/etc/network/interfaces.d/wlan0`

   更改为您自己的（默认情况下，它们是`myssid``mypassword`)

4. 关闭相机电源，插入SD卡，然后重新开机(灯由橙色变为白色)。如果操作正确，稍等片刻（1-2分钟），您会听到快门声，相机将连接到您的Wi-Fi网络。

5. 取出SD卡并重启设备。

### 使用

- 内置LED指示灯状态：

  - *橙色*- 系统未加载或 Majestic 未运行。
  - *蓝色*- 系统已加载，Majestic 正在运行。
  - *白色*- 系统升级实用程序正在运行（安装更新或擦除覆盖分区）。

- Web界面可通过端口85访问，网址为

  http://camera-ip:85

  - 默认登录名和密码分别为`admin`和`12345`。

- SSH 访问方式为

  ```
  ssh root@<camera_ip_address>
  ```

  ，默认情况下没有密码。

  - 在网页上更改密码后，控制台的密码也会随之更改。

- Majestic Endpoints 的相关信息请见此处 - https://openipc.org/majestic-endpoints

- 禁用内置 LED 灯`chmod -x /etc/init.d/S00autoled`并`chmod +x /etc/init.d/S00autoled`启用它。

- 关闭自动夜间模式`chmod -x /etc/init.d/S96autonight`并`chmod +x /etc/init.d/S96autonight`启用它。

- 要重置设置，按住重置按钮，打开相机，等待白色 LED 指示灯亮起。

- [您可以在我们的Wiki](https://wiki.openipc.org/)中找到更多关于使用 OpenIPC 的信息。

### 错误报告

- OpenIPC（固件、软件包、硬件）：https://github.com/OpenIPC/firmware/issues
- Majestic（流媒体播放器 - 音频、视频等）：https://github.com/OpenIPC/majestic/issues
- Microbe（网页界面）：https://github.com/OpenIPC/microbe-web/issues

### 参考:

- [MJSXJ02HL应用程序](https://github.com/kasitoru/mjsxj02hl_application)
- [mjsxj02hl固件的构建工具](https://github.com/kasitoru/mjsxj02hl_firmware)
- [mjsxj02hl固件的WEB界面](https://github.com/kasitoru/mjsxj02hl_web)
- [mjsxj02hl_uboot](https://github.com/kasitoru/mjsxj02hl_uboot)
- [适用于 IP-камеры MJSXJ02HL 和 RTSP 和 MQTT](https://kasito.ru/mjsxj02hl_firmware/)
- [使用 CH341A 刷写 MJSXJ02HL IP 摄像头引导加载程序](https://kasito.ru/proshivka-zagruzchika-ip-kamery-mjsxj02hl-s-pomoshhyu-ch341a/)
- [通过 USB 刷写 MJSXJ02HL IP 摄像头引导程序](https://kasito.ru/proshivka-zagruzchika-ip-kamery-mjsxj02hl-s-pomoshhyu-usb/)
- [使用 MicroSD 卡刷写 MJSXJ02HL IP 摄像头引导程序](https://kasito.ru/proshivka-zagruzchika-ip-kamery-mjsxj02hl-s-pomoshhyu-microsd-karty/)

## MJSXJ02HL 恢复原厂固件

下载还原固件mjsxj02hl_full-dump_4.0.5-0105_sign.bin 使用HiTool 将fastboot 设置为mjsxj02hl_full-dump_4.0.5-0105_sign.bin 长度设置为16M 烧写即可
