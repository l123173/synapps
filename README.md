# synapps

## calc

**ExtUitls 错误**
sudo yum install perl-ExtUtils-Command

## motor  
**如果报错 epicsShareFunc’ had not yet been defined**

那么 motorApp/MotorSrc/motordrvCom.h  中，

#ifndef	INCmotordrvComh
#define	INCmotordrvComh 1

#include <shareLib.h>  **增加这一行**
#include <callback.h>
#include <epicsTypes.h>
#include <epicsEvent.h>


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
