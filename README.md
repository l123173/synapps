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
