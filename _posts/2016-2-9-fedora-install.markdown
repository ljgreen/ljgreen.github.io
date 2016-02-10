--- 
layout: posts
categories: kernel
title: Install fedora on virtualbox
---
##Study something new every day!
> Install Fedora

<ol>
<li>
在存储中右键添加SCSI控制器，旧版本的内核不支持SATA控制器,创建新的vmdb虚拟磁盘；
</li>
<li>
选择bridged网络，在安装界面上不要选择configure DHCP，选择manually configuration；IP地址的前三段与host相同，最后一段不同，其它DNS，netmask，和gateway都一样；
</li>
<li>
在**设置**中选择**共享文件夹**，添加共享文件夹路径，修改共享文件夹名称**share_folder**,登录虚拟机后，`mount -t vboxsf share_folder /mnt/`
</li>
</ol>
