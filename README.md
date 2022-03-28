   由于openwrt云编译使用用ssh修改配置会中道崩殂（似乎是github有意ban掉的），又不想在线下安装linux生成配置文件。所以云编译在图形配置的时候先生成配置文件，再使用该文件进行完整的云编译。

[openwrt编译配置变化文件生成演示](https://p3terx.com/archives/build-openwrt-with-github-actions.html)

[openwrt编译配置变化文件生成代码说明](https://github.com/danshui-git/shuoming/blob/master/%E6%9C%AC%E5%9C%B0%E6%8F%90%E5%8F%96.config.md)

[完整的云编译代码，这个项目是在完整代码的基础上截取其上半部分，ssh操作在其中说明](https://github.com/P3TERX/Actions-OpenWrt)

SSH界面操作步骤：

1、 【 cd openwrt && make menuconfig 】   图形化配置

2、 【 make defconfig 】                  似乎不需要输入该代码

2、 【 ./scripts/diffconfig.sh > seed.text 】   生成差异文件

3、 两者选其一：【 cat seed.text 】 OR 【 mv seed.text config/ 】  
 【直接在屏幕输出差异代码，复制出来贴到完整云编译的config文件中】 OR 【生成txt文件转移到config文件夹后再上传出来】

遇到的坑：

/openwrt 目录下的文件不能上传，但是目录下的文件夹可以上传，原因未知。所以把生成的差异数据TXT文件转移到另一个文件夹再上传。


**以上是云编译openwrt配置文件生成的流程。以下是关于让随身wifi通过路由器上网的流程说明（作为熬夜一周的总结）。  


想法变迁：不想办宽带（城中村宽带太贵）》淘宝买了USB口的随身wifi》随身wifi用wifi上网的速度弱于插USB上网的速度》随身wifi24小时插笔记本太丑陋》酷安上推荐随身wifi可搭配带USB口的路由器》咸鱼买了小米路由器mini

遇到的问题：小米路由器不用U盘刷机、L大固件配置选择、路由器作为旁路由的路由设置。

一、小米路由器不用U盘刷机

使用小米官网解锁路由器SSH服务的方法需要用到FAT32的格式，而我只有一个NTFS格式的U盘，且里面的东西很重要不想转移出来格式化，所以需要一个不用U盘就能开启SSH服务的方法。

1.1 [刷0.8.11开发版固件降级](https://www.right.com.cn/forum/thread-706545-1-1.html)

1.2 [用浏览器破解漏洞获得telnet权限](https://blog.csdn.net/qq22692150/article/details/88052306)

1.3 [putty使用telnet协议进入路由器开启SSH服务dropbear。（有些教程只输入了其中一行代码“/etc/init.d/dropbear start”）](https://www.right.com.cn/forum/thread-183266-1-1.html)

1.4 [刷入breed固件](https://www.right.com.cn/forum/forum.php?mod=viewthread&tid=4028461&extra=page%3D2%26filter%3Dtypeid%26typeid%3D45)

二、为路由器识别USB口网络所增加的固件配置

2.1 [小米路由器mini固件必选的三个路由器型号配置](https://www.right.com.cn/forum/thread-4004484-1-1.html)

2.2 [为识别USB口的选择的驱动配置（我配置了这三个usb驱动“kmod-usb-net kmod-usb-net-rndis kmod-usb-net-cdc-ether”）](https://www.right.com.cn/forum/thread-248630-1-1.html)

2.2.1 [理论上可以只配置“kmod-usb-net-rndis”（kmod-usb-net-rndis 还将安装 kmod-mii、kmod-usb-net、kmod-usb-net-cdc-ether 和 kmod-usb-net-rndis 作为依赖项。）](https://openwrt.org/docs/guide-user/network/wan/wwan/ethernetoverusb_rndis)

三、路由器作为旁路由的路由设置

[旁路由的设置教程有很多，我随便用了其中一个](https://post.smzdm.com/p/axlr2dxd/)









