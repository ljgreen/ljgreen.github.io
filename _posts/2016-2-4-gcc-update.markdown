--- 
layout: posts
categories: kernel
title: gcc update in ubuntu system
---
##Study something new every day!
> compile linux kernel

最近由于实验需要重新编译内核，在Ubuntu 10.04下，编译内核linux-2.6.12，但是gcc版本是gcc-4.4，需要更换较低版本的gcc-3.4

* 下载所需要的软件：
<ol>
<li>
wget http://old-releases.ubuntu.com/ubuntu/pool/universe/g/gcc-3.4/gcc-3.4-base_3.4.6-6ubuntu3_i386.deb
</li>
<li>
wget http://old-releases.ubuntu.com/ubuntu/pool/universe/g/gcc-3.4/gcc-3.4_3.4.6-6ubuntu3_i386.deb
</li>
<li>
wget http://old-releases.ubuntu.com/ubuntu/pool/universe/g/gcc-3.4/cpp-3.4_3.4.6-6ubuntu3_i386.deb
</li>
<li>
wget http://old-releases.ubuntu.com/ubuntu/pool/universe/g/gcc-3.4/g++-3.4_3.4.6-6ubuntu3_i386.deb
</li>
<li>
wget http://old-releases.ubuntu.com/ubuntu/pool/universe/g/gcc-3.4/libstdc++6-dev_3.4.6-6ubuntu3_i386.deb
</li>
</ol>

* 安装这些软件：

<ol>
<li>
sudo dpkg --force-depends -i gcc-3.4-base_3.4.6-6ubuntu3_i386.deb
</li>
<li>
sudo dpkg --force-depends -i gcc-3.4_3.4.6-6ubuntu3_i386.deb
</li>
<li>
sudo dpkg --force-depends -i 
cpp-3.4_3.4.6-6ubuntu3_i386.deb
</li>
<li>
sudo dpkg --force-depends -i 
g++-3.4_3.4.6-6ubuntu3_i386.deb
</li>
<li>
sudo dpkg --force-depends -i 
libstdc++6-dev_3.4.6-6ubuntu3_i386.deb
</li>
</ol>

* 增加gcc-4.4和gcc-3.4的可选项：

<ol>
<li>
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.4 40
</li>
<li>
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-3.4 30
</li>
<li>
sudo update-alternatives --config gcc
</li>
<li>
选择gcc-3.4对应的数字，回车
</li>
</ol>