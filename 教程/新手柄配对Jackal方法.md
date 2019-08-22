# 新手柄配对Jackal方法

***

1 请在终端输入以下命令，确认移除sixad

`sudo apt-get purge sixad`

2 请在终端输入以下命令，确认无法找到此包

`dpkg -l sixad`

3 请在终端输入以下命令，确保蓝牙服务正常启动

`sudo service bluetooth status`

3.1 如果没有蓝牙包，请在终端输入以下命令安装gnome的蓝牙支持

`sudo apt-get install gnome-bluetooth`

4 请在终端输入以下命令，同时长按PS键和share键5秒，让工控机自动找到PS4的蓝牙地址XX:XX:XX:XX:XX:XX

`hcitool scan`

4.1 PS键即为手柄的正中间带有logo的键

4.2 PS4手柄的蓝牙名称一般为Wireless Controller

5 请在终端输入以下命令移除原文件

`sudo bluez-test-device remove XX:XX:XX:XX:XX:XX`

注:若为新手柄可跳过第4，5步

6 请在终端输入以下命令确定蓝牙服务启动，并确认

`sudo service bluetooth start`

`ls -la /usr/sbin/bluetoothd`

7 重启PS4手柄

8 长按PS键和share键5秒，之后PS4会闪烁，此时运行下面命令，待显示成功后配对成功。

`sudo ds4drv-pair`

注：若配对成功则PS4手柄灯常亮
