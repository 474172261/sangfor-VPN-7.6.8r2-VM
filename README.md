# sangfor-VPN-7.6.8r2-VM
为获取深信服VPN做测试的一些帮助信息.

默认4430的管理密码: admin:admin

官方vm的使用方法, [文件参考](https://github.com/Hagb/docker-easyconnect/issues/143):
1. 获取7.6.1虚拟机 https://download.sangfor.com/Download/Product/SSL/vSSL7.6.1_for_VMware.ova 
2. 下载7.6.8 r2 升级包[下载地址](http://download.sangfor.com.cn/download/product/sslvpn/SSLM7.6.8R2(20200224)_built-up_DLAN6.0.0(20191226).cssu) , (解压密码: sangforupd~!@#$%)
3. 下载[升级工具](http://download.sangfor.com.cn/download/product/tools/SANGF)
4. 使用升级工具安装cssu, 更新到7.6.8r2


云端vpn的磁盘安装方法:
1. 下载[磁盘文件压缩包](https://www.dropbox.com/s/5i7ck9d0u5wzxxm/sanfor-vpn-7.6.8-r2_disk_data_with_partion.7z?dl=0), 解压得到`sanfor-vpn-7.6.8-r2.image`
2. 使用vmware worktation创建一个ubuntu虚拟机(是linux就行), 新添加一个41G的空硬盘
3. 将磁盘文件挂载进去. (在虚拟机设置里添加共享文件夹, 然后`/usr/bin/vmhgfs-fuse .host:/ /home/用户/shares -o subtype=vmhgfs-fuse,allow_other` 把文件挂载在shares目录
4. 假设空硬盘位置在 `/dev/sdb`, `dd if=/home/用户/shares/sanfor-vpn-7.6.8-r2.image of=/dev/sdb status=progress` 把文件数据写入到磁盘. 写入完成后, 关闭虚拟机.
5. 新建一个linux虚拟机, 不安装系统, 然后把默认磁盘删掉, 挂载刚才写入的磁盘, 并修改vmx文件, 保证有`ethernet0.virtualDev = "e1000"`, 没有就添加.
6. 启动虚拟机, 不出意外, 就可以正常启动了.



如果想使用它的ssh, 有几种方法, 可以把vmdk里的/bin/ping替换为反向shell程序, 然后使用ping触发它. 有了反向shell, 添加用户啥的就不说了.
