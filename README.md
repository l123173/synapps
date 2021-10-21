# synapps

calc module

ExtUitls 错误时
sudo yum install perl-ExtUtils-Command


*********************************
motor  
如果报错 epicsShareFunc’ had not yet been defined,

那么 motorApp/MotorSrc/motordrvCom.h  中，
----------------------------------
#ifndef	INCmotordrvComh
#define	INCmotordrvComh 1

#include <shareLib.h>  增加这一行
#include <callback.h>
#include <epicsTypes.h>
#include <epicsEvent.h>
----------------------------------

