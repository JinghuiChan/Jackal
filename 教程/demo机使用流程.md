Hello Jackal!

demo机使用流程：

（1）通过SSH方式连接本体运行 roscore;

    ssh administrator @192.168.2.110(默认本体为该IP)

（2）通过SSH方式连接本体运行 

    sudo chmod 777 /dev/ttyUSB0 #给予端口权限
	
	roslaunch rplidar.launch #启动本体和雷达，并做tf转换
    
    tf转换: Edit rplidar.launch file add the following contents:
    
    <node pkg="tf" type="static_transform_publisher" name="link1_broadcaster" args="0.20 0 0 0 0 0 base_link     laser 50" />
	
（3）在个人pc端 运行 source workspace/devel/setup.bash

（4）验证以上步骤是否正常

    a) 验证车子本体是否可动，可用手柄控制或者运行teleop包通过键盘控制
	
	b) 验证雷达 查看雷达数据，rostopic echo /scan
	
	c) 验证tf转换 rosrun tf view_frames  ——>生成frames.pdf文件 ——> evince frames.pdf查看tf树
	
（5）验证完毕之后运行导航包

    PC端：
	
	cd ~/workspace
	
	source devel/setup.bash
	
	cd /src/Jackal/Jackal_navigation/launch
	
	roslaunch gmapping_demo.launch
    
	note:Edit arg(scan_topic) in gmapping_demo.launch
    
    <arg name="scan_topic" default="scan" />
    
	至此，建图程序启动完毕，用手柄控制完成建图(需要控制速度，不要过快)，建图完毕运行以下命令保存地图：
	
	rosrun map_server map_saver -f xxx  （默认保存在当前运行该命令的目录下，可在./map路径下保存，之后启动时默认该路径读取地图）
	
（6）重载地图，运行amcl自主导航

    PC端：
	
	a) 配置地图文件 amcl_demo.launch
	
	b) 启动amcl  roslaunch amcl.launch

	
注：本体上已留VGA和usb延长线供键盘鼠标雷达使用，充电需把电池取出。
