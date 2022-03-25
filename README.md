   由于openwrt云编译使用用ssh修改配置会中道崩殂（似乎是github有意ban掉的），又不想在线下安装linux生成配置文件。所以云编译在图形配置的时候先生成配置文件，再使用该文件进行完整的云编译。

[openwrt编译配置变化文件生成演示](https://p3terx.com/archives/build-openwrt-with-github-actions.html)

[openwrt编译配置变化文件生成代码说明](https://github.com/danshui-git/shuoming/blob/master/%E6%9C%AC%E5%9C%B0%E6%8F%90%E5%8F%96.config.md)

[完整的云编译代码，这个项目是在完整代码的基础上截取其上半部分，ssh操作在其中说明](https://github.com/P3TERX/Actions-OpenWrt)

操作步骤：

1、 【 cd openwrt && make menuconfig 】   图形化配置

2、 【 make defconfig 】                  似乎不需要输入该代码

2、 【 ./scripts/diffconfig.sh > seed.text 】   生成差异文件

3、 两者选其一：【 cat seed.text 】 OR 【 mv seed.text config/ 】  
 直接在屏幕输出差异代码，贴入config文件中 OR 生成text文件上传。

遇到的坑：

/openwrt 目录下的文件不能上传，但是目录下的文件夹可以上传，原因未知。所以把生成的差异数据TXT文件转移到另一个文件夹再上传。
