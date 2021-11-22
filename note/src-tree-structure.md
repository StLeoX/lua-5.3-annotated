# 1. 源码树的结构

## 1.1. Lua虚拟机内核

lapi.c Lua API。实现大量的 Lua C API（lua_ * 函数）。  
lctype.c 标准库中 ctype 相关实现。  
ldebug.c 调试接口。  
ldo.c Lua 的堆栈和调用结构。处理函数调用（luaD_call / luaD_pcall），扩展堆栈，协程处理等。  
lfunc.c 函数原型及闭包管理。  
lgc.c 垃圾回收。  
lmem.c 内存管理接口【luaM_realloc / luaM_growaux_】。  
lobject.c 对象操作的一些函数。包括数据类型 <-> 字符串转换，原始相等性测试（luaO_rawequalObj）和日志基础 2（luaO_log2）。  
lopcodes.c 虚拟机的字节码定义。  
lstate.c 全局状态机。包括用于打开和关闭 Lua 状态（lua_newstate / lua_close）和线程（luaE_newthread / luaE_freethread）的函数。  
lstring.c 字符串池。  
ltable.c 表类型的相关操作。Lua 表（hash）。  
ltm.c 标记方法。实现从对象访问元方法。  
lvm.c 虚拟机。执行字节码（luaV_execute）。还公开了 lapi.c 使用的一些功能（例如 luaV_concat）。  
lzio.c 通用的缓冲输入流接口。

## 1.2. Lua词法分析器及预编译器

lcode.c Lua 的代码生成器。由 lparser.c 调用。  
ldump.c 保存预编译的 Lua 块。实现 luaU_dump，将功能对象转储为预编译的块字符串。  
llex.c 词法分析器。由 lparser.c 使用。  
lparser.c 解析器。  
lundump.c 加载预编译的 Lua 块。

## 1.3. Lua内置库

lauxlib.c 库编写用到的辅助函数库  
lbaselib.c 基础库  
lbitlib.c 位操作库  
lcorolib.c 协程库  
ldblib.c Debug 库  
linit.c 内嵌库的初始化  
liolib.c IO 库  
lmathlib.c 数学库  
loadlib.c 动态扩展库管理  
loslib.c OS 库  
lstrlib.c 字符串库  
ltablib.c 表处理库

## 1.4. Lua字节码编译器与执行解释器

luac.c Lua编译器（将字节码转储到文件中）  
lua.c Lua解释器

# 2. 源码符号约定

外部符号的前缀指示其来自的模块：

luaA_-lapi.c  
luaB_-lbaselib.c  
luaC_-lgc.c 垃圾回收部分  
luaD_-ldo.c 函数的运行流程：函数调用及返回  
luaE_-lstate.c 虚拟机的当前状态  
luaF_-lfunc.c function实现  
luaG_-ldebug.c  
luaH_-ltable.c table实现  
luaI_-lauxlib.c  
luaK_-lcode.c  
luaL_-lauxlib.c / h，linit.c 公共函数  
luaM_-lmem.c 内存管理  
luaO_-lobject.c 不同的数据类型  
luaP_-lopcodes.c 虚拟机的行为是由一组 opcode 控制的  
luaS_-lstring.c string实现  
luaT_-ltm.c 元表  
luaU_-lundump.c  
luaV_-lvm.c 虚拟机对 opcode 的解析和运作  
luaX_-llex.c  
luaY_-lparser.c  
luaZ_-lzio.c 带缓冲的流处理  
lua_-lapi.c / h + luaconf.h，debug.c  
luai_-luaconf.h  
luaopen_-luaconf.h +库（lbaselib.c，ldblib.c，liolib.c，lmathlib.c，loadlib.c，loslib.c，lstrlib.c，ltablib.c）

# 3. 建议的阅读源代码的次序

首先，阅读各个内置库是如何实现功能扩展和增强的，这会帮助你理解Lua API。  
然后，阅读 Lua 的具体实现，可以开始了解 Lua VM 的实现。   
接下来就是分别理解函数调用和返回的实现，string、metatable、table等核心数据结构的实现。  
debug 模块是一个额外的设施，可以选读。  
最后是 parse 等等编译前端相关的部分，实际上是一些C编写的字符串处理函数，所以建议 **先后端，后前端**。  
内存管理和垃圾收集将是最难的部分，需要扎实的操作系统的基本知识，可能会花掉最多的时间去理解细节。

# 4. 参考

> https://www.cnblogs.com/moran-amos/p/14408624.html  
> https://www.runoob.com/lua/