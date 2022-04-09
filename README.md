# synapps
先参照这个安装一下https://github.com/epics-docs/how-tos/blob/master/getting-started/linux-packages.rst
这是 epel-release 是增强版的工具包

*具体的东西，在主页的readme里面*  
<font size=6>1 下载</font>  
https://www.aps.anl.gov/BCDA/synApps/Where-to-find-it
从这里可以下载6.1的synapps版本下来，好处是有个configure，可以直接make，是原汁原味的感觉。
下载下来，里面有一个assemxxxxxx.sh的脚本，那个是安装support的脚本，不过用了几次都不得其法，**建议还是不要用这个脚本了**，*直接用下载的文件安装*，如果需要更新，从https://github.com/EPICS-synApps 上下载模块去更新就好了



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

## stream  
**PCRE问题**
https://epics.anl.gov/tech-talk/2020/msg02093.php  用这个版本的pcre，否则容易出问题，比如libpcre.so等等
退一步说，即使下载，也不要pcre2,pcre8.44即可，这可以在版本和tech talk上看到



## asyn
照着release里的模块要求装，要不然报错
**rpc.h错误**
1）dnf --enablerepo=powertools install rpcgen
2）yum install libtirpc-devel, 应该可以看到/usr/include中有tirpc文件
3）configure/CONFIG_SITE 中，注释掉 TIRPC=YES
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
