# synapps

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

## stream  
**PCRE问题**
https://epics.anl.gov/tech-talk/2020/msg02093.php  用这个版本的pcre，否则容易出问题，比如libpcre.so等等
退一步说，即使下载，也不要pcre2,pcre8.44即可，这可以在版本和tech talk上看到



## asyn
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
