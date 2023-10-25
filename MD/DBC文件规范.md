# DBC文件范例学习

```范例
VERSION ""


NS_ : 
	
	BA_
	BA_DEF_
	BA_DEF_DEF_
	BA_DEF_DEF_REL_
	BA_DEF_REL_
	BA_DEF_SGTYPE_
	BA_REL_
	BA_SGTYPE_
	BU_BO_REL_
	BU_EV_REL_
	BU_SG_REL_
	BO_TX_BU_	
	CAT_
	CAT_DEF_
	CM_
	ENVVAR_DATA_		
	EV_DATA_	
	FILTER
	NS_DESC_
	SGTYPE_
	SGTYPE_VAL_
	SG_MUL_VAL_		
	SIG_GROUP_
	SIG_TYPE_REF_
	SIG_VALTYPE_
	SIGTYPE_VALTYPE_		
	VAL_
	VAL_TABLE_

BS_ :

BU_: CLM EAS  

//定义一个消息 ID：1281 名称：CLM_0x501 DLC：8 信源：CLM
BO_ 1281 CLM_0x501 : 8 CLM
//SG_ SignalName : StartBit|Length@ByteOrder+ (Factor, Offset) [Minimum|Maximum] "Unit" ReceiverNodes
 SG_ CLM_0x501_SET_SPEED : 6|7@0+ (100,0) [0|128] "rpm" Vector__XXX
 SG_ CLM_0x501_COM_VALID : 7|1@0+ (1,0) [0|1] "/" Vector__XXX
 SG_ CLM_0x501_COM_ACTIVE : 9|2@0+ (1,0) [0|3] "/" Vector__XXX
 SG_ CLM_0x501_POW_LIM : 39|8@0+ (0.04,0) [0|128] "Kw" Vector__XXX


BO_ 1306 EAS_0x51A: 8 EAS 
 SG_ EAS_0x51A_ACT_SPEED : 6|7@0+ (100,0) [0|128] "rpm" Vector__XXX
 SG_ EAS_0x51A_ACT_VOL : 15|9@0+ (1,0) [0|512] "V" Vector__XXX
 SG_ EAS_0x51A_ACT_CUR : 22|9@0+ (0.1,0) [0|512] "A" Vector__XXX
 //这里有些信号值范围跟协议里是不同的。
 SG_ EAS_0x51A_ACT_TEMP : 29|8@0+ (1,-40) [0|512] "℃" Vector__XXX
 SG_ EAS_0x51A_ALIVE_COUNT : 35|4@0+ (1,0) [0|512] "次" Vector__XXX
 SG_ EAS_0x51A_BASE_STATE : 43|4@0+ (1,0) [0|16] "/" Vector__XXX
 SG_ EAS_0x51A_FAIL_GRADE : 44|2@0+ (1,0) [0|100] "/" Vector__XXX
 SG_ EAS_0x51A_FAIL_STATE : 47|5@0+ (1,0) [0|100] "/" Vector__XXX

 
VAL_ 1281 CLM_0x501_COM_VALID  1 "信号有效" 0 "信号无效" 
VAL_ 1281 CLM_0x501_COM_ACTIVE  3 "命令无效" 2 "压缩机开" 1 "压缩机关" 0"自测" ;
VAL_ 1306 EAS_0x51A_BASE_STATE 7 "诊断和标定" 5 "故障" 4"控制电源接通" 2 "使能" 0"就绪" ;
VAL_ 1306 EAS_0x51A_FAIL_GRADE 3 "最高级" 2 "次高级" 1"一般" 0 "无故障" ;
VAL_ 1306 EAS_0x51A_FAIL_STATE 5 "缺相" 9 "无电压" 6"过温" 10 "过载1" 14 "过载2" 18"过流4" 22 "过压3" 7"过流1" 11 "过流2" 15 "过流3" 19 "过压1" 23 "过压2" 27 "低压故障" 31 "通信故障";

CM_ SG_ 1281 CLM_0x501_POW_LIM "功率限制"
CM_ SG_ 1281 CLM_0x501_SET_SPEED "设置速度"
CM_ SG_ 1281 CLM_0x501_COM_VALID "命令使能"
CM_ SG_ 1281 CLM_0x501_COM_ACTIVE "压缩机激活"
CM_ SG_ 1306 EAS_0x51A_ACT_SPEED "反馈速度"
CM_ SG_ 1306 EAS_0x51A_ACT_VOL "反馈电压"
CM_ SG_ 1306 EAS_0x51A_ACT_CUR "反馈电流"
CM_ SG_ 1306 EAS_0x51A_ALIVE_COUNT "ALIVE计数"
CM_ SG_ 1306 EAS_0x51A_ACT_TEMP "反馈温度"
CM_ SG_ 1306 EAS_0x51A_BASE_STATE "基本状态"
CM_ SG_ 1306 EAS_0x51A_FAIL_GRADE "故障级别"
CM_ SG_ 1306 EAS_0x51A_FAIL_STATE "故障类别"
```

## 1. 标识

VERSION 【版本】

NS_ :  【命名空间NameSpace：通过定义命名空间，可以将具有相似功能或归属于特定子系统的对象进行分类和管理。】

BS_  【？？？】

BU_ 【节点】

BO_ 【消息】

SG_ 【信号】

VAL_ 【数值表ValueTable】

CM_ 【添加注释】