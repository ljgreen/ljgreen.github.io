--- 
layout: posts
categories: kernel
title: something related to compiling linux kernel
---
##Study something new every day!
> compile linux kernel

最近由于实验需要重新编译内核，在Ubuntu 12.04下，将原有的内核linux-3.13.0换成linux-2.6.35内核；
<li>
apt-get install libncurses5-dev build-essential kernel-package；
</li>

<li>
make menuconfig然后exit；
</li>

<li>
make；（期间会遇到一些问题，需要自己上网查找，都能解决）
</li>

<li>
make modules_install;
</li>

<li>
make install;
</li>

<li>
修改/boot/grub/grub.cgf文件，将set timeout_style=hidden注释掉，并将set timeout=10，这样在开机的时候
就能够选择启动内核。
</li>

> virtual box 虚拟机与主机共享文件夹
> 
* 安装virtualbox增强工具;
* 建立与主机的共享文件夹；
* 在虚拟机下执行：mount -t vboxsf shared_folder_name /media/share_file 其中shared_folder_name是你建立的共享文件夹的名字，share_file是你的虚拟机中的挂载点，通过share_file你就可以访问主机的文件了

