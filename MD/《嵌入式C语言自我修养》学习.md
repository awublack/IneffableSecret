# 嵌入式C语言自我修养

<center>2023年7月18日</center>
---

# 第6章-GNU C编译器扩展语法精讲


#define offsetof(type,member)   ((size_t)&(((type*)0)->member))        //取member成员在type类型中的偏移地址
#define container_of(ptr,type,member)   ({              \
    const (typeof((type*)0->member)) *_mptr = (ptr);    \              //常量指针型变量取值，防止输入宏是一个自增之类的表达式
    (type*)((char*)_mptr - offset(type,member));        \              //强制转换为char变量
})
