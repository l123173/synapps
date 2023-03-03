# synapps
https://epics.anl.gov/tech-talk/2019/msg01642.php  here is the instruction about how to run assemble_synApps.sh.
https://epics.anl.gov/tech-talk/2019/msg01647.php   here is the whole command
https://rockylinux.pkgs.org/9/rockylinux-appstream-x86_64/libusb-0.1.7-5.el9.x86_64.rpm.html  could find the lib here for os


网上那个assemble_synApps.sh 多次尝试，确实没有按照你 base目录去修改他的，最后还是要自己改base地址，就相当于一个自动下载  
https://github.com/NSLS-II/installSynApps    倒是这个可以尝试一下看看如何  
先参照这个安装一下https://github.com/epics-docs/how-tos/blob/master/getting-started/linux-packages.rst
这是 epel-release 是增强版的工具包

*具体的东西，在epics的主页 的readme里面*  
**1 下载**  
https://www.aps.anl.gov/BCDA/synApps/Where-to-find-it
从这里可以下载6.1的synapps版本下来，好处是有个configure，可以直接make，是原汁原味的感觉。  
下载下来，里面有一个assemxxxxxx.sh的脚本，那个是安装support的脚本，不过用了几次都不得其法，**建议还是不要用这个脚本了**，*直接用下载的文件安装*，如果需要更新，从https://github.com/EPICS-synApps 上下载模块去更新就好了。  
**2 再下载**
其实里头有很多都虽不是最新的，容易出一些bug，最好是在https://github.com/epics-modules/asyn 重新下载对应模块下来
记得先下载，至少也要下载几个常用的，这个是不是可以用repo来了？
不过这样的花，后面的脚本可能就用不上了

**2 修改，建议分别用2个脚本该改了，自己改太繁琐**  
里面有很多文件路径要修改，很繁琐，建议用脚本：
sed -i "s#EPICS_BASE=/APSshare/epics/base-3.15.6#EPICS_BASE=/home/iasf/epics/base#g" `grep EPICS_BASE=/APSshare/epics/base-3.15.6 -rl ./`  
该脚本其实分2个部分，第一部分（base-3.15.6那里）是configure/RELEASE里的原base目录，后面那个base是你电脑里的新base目录  
第二部分 grep EPICS_BASE=/APSshare/epics/base-3.15.6*这部分是configure/RELEASE的base**原**目录* -rl ./*这个./是要求在support目录下执行该脚本  或者换成相应的support目录*
*第二个脚本* 
sed -i "s#SUPPORT=/home/oxygen40/KLANG/Epics/synApps_6_1/synApps/support#SUPPORT=/home/iasf/epics/module/synApps_6_1/support#g" `grep SUPPORT=/home/oxygen40/KLANG/Epics/synApps_6_1/synApps/support -rl ./`

**3** 
在configure/RELEASE里添加BASE和SUPPORT的地址



## calc

**ExtUitls 错误**
sudo yum install perl-ExtUtils-Command

## motor  
**如果报错 epicsShareFunc’ had not yet been defined**  红色

那么 motorApp/MotorSrc/motordrvCom.h  中，

#ifndef	INCmotordrvComh
#define	INCmotordrvComh 1

#include <shareLib.h>  **增加这一行**
#include <callback.h>
#include <epicsTypes.h>
#include <epicsEvent.h>


**关于motorsim**

需要在注释很多东西，比如 configr/里的 RELEASE 和CONFIG_SITE (BUILD_IOCS = YES   NO改称yes）

反正很多，要照着一个个的看，别光看readme，另外example 和simu是2个东西。

标志就是motor-R7-2-2/modules/motorMotorSim/iocs/motorSimIOC  里有了bin文件
另外，启动的时候不要用 ./st.cmd
用这个启动../../bin/linux-x86_64/motorSim st.cmd.unix ，否则出错。

## xxx
**这个其实可以用命令去下载的，github有时候不灵，等5分钟可能就行了**
命令在motor里面可以找到，在 2021年10月22日 17:45  的l123173邮件里也可以找到。


**如果报错 Can't find file 'devPIMotor.dbd**
（motor有时候也会出现）
是因为motor/module没有安装，单独在git下载motor 是不包含里头的东西的，要用git命令或者单独下载。
单独下载比较麻烦，要注意去搜索名字，对应的名字下载，才可以正常编译;

当然，不想单独下，注释掉也可以。

## areadetector
这个要按照说明一条条的安装，像zlib，jpeg等等。install_guide里说的很详细了，照着操作。  
### 需要说一下的是libjpeg。我还没有试过新的，据说速度会比较快，新的要用cmake编译，老的是用的configure。  
** https://blog.csdn.net/Dancer__Sky/article/details/78631577 **这个讲了新旧2种操作方式  
不要管上面网址的删除操作，新的看上面，老的看下面即可，新老版本的参数都有介绍，对着改就好  
首先，教程里的&am，可以忽略不用管。  
我使用的时候，新版本已经不是make了，而且configure以后，没有生成make文件，只有make.in 和am。  
所以换了几个版本，1.5.3的还可以。  
**好像需要安装nasm**  

### 安装ImageJ
libnsl.so.1 can't 错误，dnf install libnsl* 解决
然后把areaDetector module的 ADViewers/ImageJ/EPICS_areaDetector 这个文件夹，拷贝到ImageJ 的plugin文件里


### getInteger64Param错误  
这个需要下载新的asyn，至少4.37版本以上的   

** 注意在install_guide中，Debian系统，有单独的说明 **  



##powerstools
https://forums.rockylinux.org/t/how-do-i-install-powertools-on-rocky-linux-9/7427/4
rocky9 中使用的是 dnf config-manager --enable crb 不是那个语句了。

## stream  
**PCRE问题**
https://epics.anl.gov/tech-talk/2020/msg02093.php  用这个版本的pcre，否则容易出问题，比如libpcre.so等等
退一步说，即使下载，也不要pcre2,pcre8.44即可，这可以在版本和tech talk上看到

##seq
用这个，git上太多了，也不知道用哪个
https://www-csr.bessy.de/control/SoftDist/sequencer/

## asyn
**rpc.h错误**（不同版本不一样的安装命令）
1）dnf --enablerepo=powertools install rpcgen( 详见https://epics.anl.gov/tech-talk/2022/msg01447.php 或 https://epics.anl.gov/tech-talk/2021/msg01369.php)   
2）yum install libtirpc-devel, 应该可以看到/usr/include中有tirpc文件  
3）configure/CONFIG_SITE 中，注释掉 TIRPC=YES**要做**  
done

# System
**错误**
/bin/csh: bad interpreter: No such file or dictionary
yum install csh

# Extensions

**Medm**
**1)**
X11/Intrinsic.h 或者  X11/Xlib.h
yum install libX*

**2）**
Xm/XmP.h
yum install motif-devel
yum install libXp libXp-devel


https://www-csr.bessy.de/control/SoftDist/sequencer/Installation.html#epics-base
下载seq-2.2.6
