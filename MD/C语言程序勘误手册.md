# C程序BUG修改记录

<center>2023年7月19日</center>

---

* 通讯底层文件[CAN_Com_process.h]

```
#define BTIM_TABLE    {\//  PripheralClock=36MHz【×】
   {CAN_RSJW_1tq,CAN_TBS1_10tq,CAN_TBS2_1tq,3},\
   {CAN_RSJW_1tq,CAN_TBS1_8tq,CAN_TBS2_1tq,4},\
   {CAN_RSJW_2tq,CAN_TBS1_13tq,CAN_TBS2_1tq,3},\
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,3},\
   {CAN_RSJW_1tq,CAN_TBS1_13tq,CAN_TBS2_1tq,4},\
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,4},\
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,5},\
   {CAN_RSJW_1tq,CAN_TBS1_15tq,CAN_TBS2_1tq,7},\
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,8},\
   {CAN_RSJW_1tq,CAN_TBS1_14tq,CAN_TBS2_1tq,10},\
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,10},\
   {CAN_RSJW_1tq,CAN_TBS1_13tq,CAN_TBS2_1tq,15},\
   {CAN_RSJW_1tq,CAN_TBS1_14tq,CAN_TBS2_1tq,15},\// 150K
   {CAN_RSJW_1tq,CAN_TBS1_8tq,CAN_TBS2_1tq,25},\// 144K
   {CAN_RSJW_1tq,CAN_TBS1_6tq,CAN_TBS2_1tq,36},\// 125K
   {CAN_RSJW_1tq,CAN_TBS1_13tq,CAN_TBS2_1tq,20},\// 120K
   {CAN_RSJW_1tq,CAN_TBS1_6tq,CAN_TBS2_1tq,45},\// 100K
   {CAN_RSJW_1tq,CAN_TBS1_14tq,CAN_TBS2_1tq,25},\// 90K
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,25},\// 80K
   {CAN_RSJW_1tq,CAN_TBS1_14tq,CAN_TBS2_1tq,30},\// 75K
   {CAN_RSJW_1tq,CAN_TBS1_13tq,CAN_TBS2_1tq,40},\// 60K
   {CAN_RSJW_1tq,CAN_TBS1_14tq,CAN_TBS2_1tq,45},\// 50K
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,50},\// 40K
   {CAN_RSJW_1tq,CAN_TBS1_14tq,CAN_TBS2_1tq,75},\// 30K
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,100}}// 20K
```
中间有些注释删掉了，在删掉注释的地方是不报错的，保留注释的地方报错——
```报错
Error[Pe007]: unrecognized token E:\OneDrive\E35&CAN_PROJX\CAN_Com_JXPR\projects\CAN_Com_JXPR\inc\CAN_Com_process.h 81 
```
但是这个程序部分我是从前一个版本copy过来的，为什么原来的程序不报错？？？
```User_Can_Config.c
/* 波特率索引到BTIM寄存器配置表*/
const tCAN_BaudRate  CAN_BaudRateInitTab[]= {      // CLK=36MHz
   {CAN_RSJW_1tq,CAN_TBS1_10tq,CAN_TBS2_1tq,3},     // 1M
   {CAN_RSJW_1tq,CAN_TBS1_8tq,CAN_TBS2_1tq,4},     // 900K
   {CAN_RSJW_2tq,CAN_TBS1_13tq,CAN_TBS2_1tq,3},     // 800K
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,3},     // 666K
   {CAN_RSJW_1tq,CAN_TBS1_13tq,CAN_TBS2_1tq,4},     // 600K
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,4},     // 500K
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,5},     // 400K
   {CAN_RSJW_1tq,CAN_TBS1_15tq,CAN_TBS2_1tq,7},    // 300K
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,8},    // 250K
   {CAN_RSJW_1tq,CAN_TBS1_14tq,CAN_TBS2_1tq,10},	// 225K
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,10},    // 200K
   {CAN_RSJW_1tq,CAN_TBS1_13tq,CAN_TBS2_1tq,15},	// 160K
   {CAN_RSJW_1tq,CAN_TBS1_14tq,CAN_TBS2_1tq,15},    // 150K
   {CAN_RSJW_1tq,CAN_TBS1_8tq,CAN_TBS2_1tq,25},		// 144K
   {CAN_RSJW_1tq,CAN_TBS1_6tq,CAN_TBS2_1tq,36},   // 125K
   {CAN_RSJW_1tq,CAN_TBS1_13tq,CAN_TBS2_1tq,20},	// 120K
   {CAN_RSJW_1tq,CAN_TBS1_6tq,CAN_TBS2_1tq,45},    // 100K
   {CAN_RSJW_1tq,CAN_TBS1_14tq,CAN_TBS2_1tq,25},   // 90K
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,25},   // 80K
   {CAN_RSJW_1tq,CAN_TBS1_14tq,CAN_TBS2_1tq,30},	// 75K
   {CAN_RSJW_1tq,CAN_TBS1_13tq,CAN_TBS2_1tq,40},    // 60K
   {CAN_RSJW_1tq,CAN_TBS1_14tq,CAN_TBS2_1tq,45},    // 50K
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,50},    // 40K
   {CAN_RSJW_1tq,CAN_TBS1_14tq,CAN_TBS2_1tq,75},   // 30K
   {CAN_RSJW_1tq,CAN_TBS1_16tq,CAN_TBS2_1tq,100},   // 20K
};
```
<center>2023年7月27日</center>

---

【软件问题】IAR突然特别卡——解决：由于新的文件路径带有中文“桌面”
【软件问题】没有办法进行寻定义和寻声明的跳转——解决：clean、重新编译

<center>2023年8月23日</center>

---

* 警惕带参宏，尤其是字符连接宏的括号问题！！！

```字符连接宏定义
//Tools.h
#define _toString(str)			#str
#define toString(str)				_toString(str)
#define _conStr(a, b)				(a##b)
#define conStr(a, b)				_conStr(a, b)
#define _conStr3(a, b, c)		(a##b##c)
#define conStr3(a, b, c)		_conStr3(a, b, c)
//CanPrtcl1_Instantiator.c
/* 这些值都是作为右值赋值的，里面可能有数组“{A,B,C,...}”*/
#define Prtcl1_INFO               conStr3(Prtcl_,_Prtcl1,_Info)
#define Prtcl1_TXMSG_L            conStr3(Prtcl_,_Prtcl1,_TXMSG_L)
#define Prtcl1_RXMSG_L            conStr3(Prtcl_,_Prtcl1,_RXMSG_L)
#define Prtcl1_TXMSG1_SGN_L       conStr3(Prtcl_,_Prtcl1,_TXMSG1_SGN_L)
#define Prtcl1_RXMSG1_SGN_L       conStr3(Prtcl_,_Prtcl1,_RXMSG1_SGN_L)
#define Prtcl1_TXMSG1_SPU_L       conStr3(Prtcl_,_Prtcl1,_TXMSG1_SPU_L)
#define Prtcl1_RXMSG1_SPU_L       conStr3(Prtcl_,_Prtcl1,_RXMSG1_SPU_L)

/* 信号标幺化参数列表*/
const float Prtcl1_TxMsg1_SgnPeru_l[Prtcl1_TxMsg1_SgnNum] = Prtcl1_TXMSG1_SPU_L;
const float Prtcl1_RxMsg1_SgnPeru_l[Prtcl1_RxMsg1_SgnNum] = Prtcl1_RXMSG1_SPU_L;
/* 信号参数列表*/
const Signal_t Prtcl1_TxMsg1_Sgns_l[Prtcl1_TxMsg1_SgnNum] = Prtcl1_TXMSG1_SGN_L;/* [Error:"Prtcl1_TXMSG1_SGN_L"expected a constant value.] */
const Signal_t Prtcl1_RxMsg1_Sgns_l[Prtcl1_RxMsg1_SgnNum] = Prtcl1_RXMSG1_SGN_L;/* Error */
/* 消息参数列表*/
const CanMsg_t Prtcl1_TxMsg_l[Prtcl1_TxMsgNum] = Prtcl1_TXMSG_L;/* Error */
const CanMsg_t Prtcl1_RxMsg_l[Prtcl1_RxMsgNum] = Prtcl1_RXMSG_L;/* Error */
/* 协议层信息*/
const CanNodePrtcl_t Prtcl1 = Prtcl1_INFO;/* Error */
```
> 分析：因为最终展开是({A,B,C,...})作为右值，不知道编译器会把这个认为是什么，但肯定是非法的。
> 解决方案：Option->C/C++ Compiler->Preprocesser output to file选项打开，在Debug/List/xxx.i中有预处理后的文件，查看预处理问题。


* 警惕IAR编译器中的类型问题，尤其是数组名和数组指针。
> 定义数组指针的三种方法：
> 1. 定义数组类型，用数组类型定义数组指针。
> 2. 定义数组指针类型，用数组指针直接定义。
> 3. 直接定义

```
//第一种
int a[10] = {0};
typdef int A[10];       //[10]代表步长
                        //数组指针和指针的区别:
                        //数组指针的步长是sizeof(int)*10；指针的步长是sizeof(int)
A *p = NULL;            //p数组指针类型的变量!!!!!!

//第二种
int a[10] = {0};
typedef int(*P)[10];
P q;                        //数组指针变量

//第三种
int a[10] = {0};
int(*q)[10];                //q数组指针变量

```

<center>2023年8月28日</center>

---

* 注意类型问题，尤其是函数名/结构体变量声明过后就想使用其地址作为右值初始化其他变量时，一定要用取地址运算，因为初始化要求右值必须是常量，而刚刚定义的无论是指针变量还是函数指针，本质都是变量，不能作为右值。

```
typedef struct{
  uint32_t            ID;
  uint8_t             MsgType;          /* CAN_Message_Type*/
  uint8_t             SignalNum;
  uint8_t             Length;
  uint8_t             SendType;         /* CAN_MessageSend_Type*/
  uint32_t            Cycle_ms;
  Signal_t const      *pSgnList;
  Callback_fp const   *callback;//类型定义时要用二级指针
  SignalsInf_t const  *SignalsInf;
}CanMsg_t;

//定义函数指针
extern Callback_fp Prtcl1_TxMsg1_callback;
extern Callback_fp Prtcl1_RxMsg1_callback;

//赋值时取地址
const CanMsg_t Prtcl1_TxMsg_l[1] = {{0x51A,((uint8_t)0x00),7,8, ((uint8_t)0x00),100,\
Prtcl1_TxMsg1_Sgns_l, &Prtcl1_TxMsg1_callback,&Prtcl1_TxMsg1_SgnInf_l}};
```

* 很多预编译的问题可以通过打开.i文件输出，分析.i文件得到解答。这里可以看到宏展开后的结果。


<center>2023年9月12日</center>

---

* GPIO的初始化过程中，GPIO_Speed成员一定要初始化！！
因为在函数中一般只用临时变量作为外设初始化变量，假如不初始化的话，它的值是不确定的，而GPIO_Speed成员又是枚举型变量，如果不初始化，会导致外设初始化函数的参数检查不通过，导致初始化失败！！