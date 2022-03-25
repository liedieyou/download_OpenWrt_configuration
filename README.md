由于openwrt云编译用ssh修改配置不成功，又不想在线下安装linux。所以云编译先在配置的时候生成配置文件，再进行完整的云编译。

[openwrt编译配置变化文件生成演示](https://p3terx.com/archives/build-openwrt-with-github-actions.html)

[openwrt编译配置变化文件生成代码说明](https://github.com/danshui-git/shuoming/blob/master/%E6%9C%AC%E5%9C%B0%E6%8F%90%E5%8F%96.config.md)

[完整的云编译代码，这个项目是在完整代码的基础上截取一上半部分，ssh操作在其中说明](https://github.com/P3TERX/Actions-OpenWrt)

cd openwrt && make menuconfig   图形化配置
make defconfig                  似乎不需要输入该代码
./scripts/diffconfig.sh > seed.text   生成差异文件


cat seed.text 直接在屏幕输出差异代码，贴入config文件中
OR
mv seed.text config/  生成text文件上传。


遇到的坑：
/openwrt 目录下的文件不能上传，但是目录下的文件夹可以上传，原因未知。所以把生成的差异数据TXT文件转移到另一个文件夹再上传。
