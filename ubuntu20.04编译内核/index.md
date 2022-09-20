# UBuntu22.04编译内核 | 2022最新 | 详细图解


# UBuntu22.04编译内核 | 2022最新 | 详细图解

- [官网](https://www.kernel.org/)下载内核源码

- 解压到 `/usr/src`目录 

  `sudo tar -xavf  linux-5.19.8.tar.xz /usr/src`

- 下载安装一系列的软件，为编译内核做准备

  `sudo apt install libncurses5-dev openssl libssl-dev build-essential pkg-config libc6-dev bison flex libelf-dev zlibc minizip libidn11-dev libidn11 qttools5-dev liblz4-tool`

  ```
   sudo apt-get install libncurses5-dev   openssl libssl- dev 
   sudo apt-get install build-essential openssl
   sudo apt-get install pkg-config
   sudo apt-get install libc6-dev
   sudo apt-get install bison
   sudo apt-get install flex
   sudo apt-get install libelf-dev
   sudo apt-get install zlibc minizip
   sudo apt-get install libidn11-dev libidn11
  ```

- 配置ccache，提高后续编译的速度(可选)

  ```
  sudo apt install ccache
  sudo gedit ~/.bashrc
  ```

  在末尾回车，添加如下语句，注意ubuntu要改成你的用户名。

  ```
  export USE_CCACHE=1
  export CCACHE_DIR="/home/ubuntu/.ccache" 
  export CC="ccache gcc"    
  export CXX="ccache g++"    
  export PATH="$PATH:/usr/lib/ccache"
  ```

  生效 `source ~/.bashrc  `

  50G `ccache -M 50G`

  配置以下内容

  ```
  which ccache    # 找到ccache的位置
  cd /usr/bin     # 我的对应ccache路径
  sudo cp ccache /usr/local/bin/  
  # 建立软链接
  sudo ln -s ccache /usr/local/bin/gcc
  sudo ln -s ccache /usr/local/bin/g++
  sudo ln -s ccache /usr/local/bin/cc
  sudo ln -s ccache /usr/local/bin/c++
  ccache -s       # 查看当前的一个状况
  ```

- 净化内核源码

  ```
  sudo make mrproper
  ```

- 将我现有的内核（5.15）版本的config配置信息复制到现在目录下的 .config里面

  `sudo cp /boot/config-5.15.0.47-generic ./.config`

- 通过`make menuconfig` 对内核选项进行配置

  出现以下界面直接退出ESC然后确定yes即可

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20220913112410.png)

- 编译内核

  `sudo make bzImage -j8`

  执行完会在 `/arch/x86/boot/`目录下生成`bzImage`文件

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20220913190925.png)

- 出现的问题

  ```
  Linux内核编译错误：make[1]: *** 没有规则可制作目标“debian(https://so.csdn.net/so/search?q=debian&spm=1001.2101.3001.7020)/canonical-certs.pem”，由“certs/x509_certificate_list” 需求。 停止。**
  ```

  解决方式

  ```
  CONFIG_MODULE_SIG_KEY="cert/signing_key.pem" #这个可能不需要删除，删除了反而可能出其他问题make modules_install时报错
  CONFIG_SYSTEM_TRUSTED_KEYS="debian/canonical-certs.pem" #这个要删除
  ```

  实际上应该根据报的具体错删除指定的内容

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/20220913214810.png)

  

- 编译模块

  `sudo make modules -j8`

- 安装模块

  `sudo make modules_install`

  执行本操作 此时`/lib/modules/`下应该新生成一个新内核版本号的文件.
  此时在新内核目录下的操作都已经做完了。编译安装都已经完成，只剩最后的收尾工作。将新内核添加到启动项里面。

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/20220913215714.png)

- 将3个文件拷贝到boot目录下

  ```
  sudo mkinitramfs /lib/modules/5.19.8/ -o /boot/initrd.img-5.19.8-generic
  sudo cp /usr/src/linux-5.19.8/arch/x86/boot/bzImage /boot/vmlinuz-5.19.8-generic
  sudo cp /usr/src/linux-5.19.8/System.map  /boot/System.map-5.19.8
  ```

  执行完`/boot` 目录下

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20220913220119.png)

- 切换到/boot/grub/目录下，自动查找新内核，更新grub

  首先进入`/boot/grub/` 然后执行`update-grub2` 这时候你查看一下当前目录下的`grub.cfg`文件内容。如果发现里面多了新内核的信息。那么恭喜你！ 可以重启进入新内核了。

![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20220913220836.png)

- 重启Ubuntu

  重启时，长按shift，可进入GRUB，选择Advanced options for ubantu,启动新编译的内核（5.19.8）

![image-20220913221801070](C:\Users\HFFKH\AppData\Roaming\Typora\typora-user-images\image-20220913221801070.png)

![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/20220913222014.png)

## 参考链接

- [ubuntu(20.04)+linux内核（5.17.3）编译内核](https://blog.csdn.net/weixin_62882080/article/details/124260136)
- [Ubantu20.04更换Linux内核版本（5.8.1）](https://blog.csdn.net/Stubborn_Lanmail/article/details/115863781)
- [Ubuntu下编译内核](https://blog.csdn.net/qq_43688952/article/details/88856354)
- [Ubuntu内核编译](https://zhuanlan.zhihu.com/p/371464316)

