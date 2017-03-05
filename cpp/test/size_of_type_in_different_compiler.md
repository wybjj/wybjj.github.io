---
title: 各编译器基本类型数据的大小
---

# 各编译器基本类型数据的大小

## 编译器及测试环境

### 测试用编译器概述

目前，最常用的编译器为 Windows 系统下的 Visual C++ 和 Linux 系统下的 GCC。
本次测试，选取了 Visual C++ 2015 和 GCC 4.8.4 并分别编译了 Windows 和 Linux 系统下的 32 位 和 64 位程序。
某些时候，可能会在windows 环境下使用 GCC 编译程序，因此也下载了 TDM-GCC 的 32位和64位版本作为比较。	
下面描述了各编译器在本文中的简称和编译器版本、所运行的操作系统以及编译测试程序时使用的编译命令。

### VC32

编译器：Visual C++ 2015 Update 3 所带 32位 C/C++ 编译器 cl.exe， 版本号 19.00.24210。
操作系统：Windows 10 64位。
编译命令为:

```bat
cl type.c /W4 /Fetest_type_win32
```

### VC64

编译器：Visual C++ 2015 Update 3 所带 64位 C/C++ 编译器 cl.exe， 版本号 19.00.24210。

操作系统：Windows 10 64位。

编译命令为:

```bat
cl type.c /W4 /Fetest_type_x64.exe
```

### GCC32

编译器：GCC 编译器，64位编译器上使用 -m32 参数编译32位程序，版本号 4.8.4(Ubuntu 4.8.4-2ubuntu1~14.04.3)。
	
操作系统：Ubuntu 14.04 64bit。
	
编译命令为:
	
```sh
gcc -m32 -std=c99 -Wall type.c -o test_type32
```
	
### GCC64

编译器：GCC 编译器，64位编译器，版本号 4.8.4(Ubuntu 4.8.4-2ubuntu1~14.04.3)。
	
操作系统：Ubuntu 14.04 64bit。
	
编译命令为:
	
```sh
gcc -std=c99 -Wall type.c -o test_type64
```
	
### TDM32

编译器：TDM-GCC 编译器，GCC 64位编译器，版本号 5.1.0 (tdm64-1)。[tdm-gcc-5.1.0-3.exe 下载](http://sourceforge.net/projects/tdm-gcc/files/TDM-GCC%20Installer/tdm-gcc-5.1.0-3.exe/download)
	
操作系统：Windows 10 64位。
	
编译命令为:
	
```bat
gcc -std=c99 -Wall -o test_type_tdm32.exe type_t32.c
```

### TDM64

编译器：TDM64-GCC 编译器，GCC 64位编译器，版本号 5.1.0 (tdm64-1)。[tdm64-gcc-5.1.0-2.exe 下载](http://sourceforge.net/projects/tdm-gcc/files/TDM-GCC%20Installer/tdm64-gcc-5.1.0-2.exe/download)
	
操作系统：Windows 10 64位。
	
编译命令为:
	
```bat
gcc -std=c99 -Wall -o test_type_tdm64.exe type_t.c
```

## 测试代码

### 测试代码概述

一般的测试程序代码使用 type.c 测试程序。
	
由于 TDM64 的 printf 不支持 C99 标准规定的用于 size_t 类型的 z 长度标记，因此强制转换为 int 类型输出，修改后形成 type_t.c。
	
由于 TDM32 编译时找不到 <uchar.h>，无法使用 char16_t 和 char32_t 类型，因此长度输出null，修改后形成 type_t32.c。

### type.c —— VC32、VC64、GCC32、GCC64 编译使用的测试代码：

```cpp
/* type.c */
#include <stdio.h>
#include <stdbool.h>
#include <wchar.h>
#include <uchar.h>
 
#define PRINT_SIZE(x) printf("%12s %6zu\n", #x, sizeof(x));
#define PRINT_NOTSUPPORT(x) printf("%12s %6s\n", #x, "null");

int main()
{
	PRINT_SIZE(bool);
	PRINT_SIZE(char);
	PRINT_SIZE(wchar_t);
	PRINT_SIZE(char16_t);
	PRINT_SIZE(char32_t);
	PRINT_SIZE(short);
	PRINT_SIZE(int);
	PRINT_SIZE(long);
	PRINT_SIZE(long long);
	PRINT_SIZE(size_t);
	PRINT_SIZE(float);
	PRINT_SIZE(double);
	PRINT_SIZE(long double);
	PRINT_SIZE(void*);
	
	return 0;
}
```

### type_t32.c —— TDM32 编译使用的测试代码为：

```cpp
/* type_t32.c */
#include <stdio.h>
#include <stdbool.h>
#include <wchar.h>
 
#define PRINT_SIZE(x) printf("%12s %6d\n", #x, (int)sizeof(x));
#define PRINT_NOTSUPPORT(x) printf("%12s %6s\n", #x, "null");

int main()
{
	PRINT_SIZE(bool);
	PRINT_SIZE(char);
	PRINT_SIZE(wchar_t);
	PRINT_NOTSUPPORT(char16_t);
	PRINT_NOTSUPPORT(char32_t);
	PRINT_SIZE(short);
	PRINT_SIZE(int);
	PRINT_SIZE(long);
	PRINT_SIZE(long long);
	PRINT_SIZE(size_t);
	PRINT_SIZE(float);
	PRINT_SIZE(double);
	PRINT_SIZE(long double);
	PRINT_SIZE(void*);
	
	return 0;
}
```

### type_t.c —— TDM64 编译使用的测试代码为：

```cpp
/* type_t.c */
#include <stdio.h>
#include <stdbool.h>
#include <wchar.h>
#include <uchar.h>
 
#define PRINT_SIZE(x) printf("%12s %6d\n", #x, (int)sizeof(x));
#define PRINT_NOTSUPPORT(x) printf("%12s %6s\n", #x, "null");

int main()
{
	PRINT_SIZE(bool);
	PRINT_SIZE(char);
	PRINT_SIZE(wchar_t);
	PRINT_SIZE(char16_t);
	PRINT_SIZE(char32_t);
	PRINT_SIZE(short);
	PRINT_SIZE(int);
	PRINT_SIZE(long);
	PRINT_SIZE(long long);
	PRINT_SIZE(size_t);
	PRINT_SIZE(float);
	PRINT_SIZE(double);
	PRINT_SIZE(long double);
	PRINT_SIZE(void*);
	
	return 0;
}
```

## 测试结果

### 各版本程序编译后执行，执行结果统计为如下表所示：

|        type|     std-min|   VC32|   VC64|  GCC32|  GCC64|  TDM32|  TDM64|
|------------|------------|-------|-------|-------|-------|-------|-------|
|        bool|            |      1|      1|      1|      1|      1|      1|
|        char|       8 bit|      1|      1|      1|      1|      1|      1|
|     wchar_t|      16 bit|      2|      2|      4|      4|      2|      2|
|    char16_t|      16 bit|      2|      2|      2|      2|   null|      2|
|    char32_t|      32 bit|      4|      4|      4|      4|   null|      4|
|       short|      16 bit|      2|      2|      2|      2|      2|      2|
|         int|      16 bit|      4|      4|      4|      4|      4|      4|
|        long|      32 bit|      4|      4|      4|      8|      4|      4|
|   long long|      64 bit|      8|      8|      8|      8|      8|      8|
|      size_t|            |      4|      8|      4|      8|      4|      8|
|       float| 6位有效数字|      4|      4|      4|      4|      4|      4|
|      double|10位有效数字|      8|      8|      8|      8|      8|      8|
| long double|10位有效数字|      8|      8|     12|     16|     12|     16|
|       void*|            |      4|      8|      4|      8|      4|      8|	

表中：

* type 列 为测试的 c语言 数据类型。

* std-min 列 为 《C++ Primer 第五版 中文版》 2.1.1 节 介绍的个数据类型的最小尺寸。

* 其余列 为个编译器执行得到的数据类型大小。

### 对测试结果的简要分析

* 无论编译32位还是64位程序，bool、char、short、int、long long、float、double 在所测试的几个编译器的实现中，大小都是一致的。

* long 在 GCC64 中为8字节，其余均为 4 字节

* size_t，void* 在 32位程序中均为4字节，在64位程序中均为8字节。

* 不论32位还是64位程序，wchar_t 在 Visual C++ 中为 2 字节，在 GCC 中为 4 字节， 在 TDM-GCC 中是2字节。

* long double 在 Visual C++ 中与 double 一致为8字节，但在 GCC 和 比 double 要大，且64为程序比32为更大。

