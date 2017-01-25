# Visual C++ 命令行编译 C/C++ 程序

## Visual C++ 命令行编译的几种方式

1. CL

使用编译器（cl.exe）把源代码编译成应用程序、静态库、动态链接库。

2. Link

使用连接器（link.exe）把编译好的对象文件和静态库连接到应用程序和动态链接库中。

3. MSBuild（Visual C++）

与在 Visual Studio IDE 中一样，可以使用MSBuild （msbuild.exe）构件 Visual C++ 项目和解决方案。

4. DEVENV
使用 DEVENV （devenv.exe）和一些命令行参数（例如  /Build 或 /Clean） 可以在不显示 Visual Studio IDE 的情况下构建程序。

5. NMAKE

使用 NMAKE （nmake.exe）可以使用传统的 makefile 文件实现自动化构建 Visual C++ 项目。

## 使用 CL 编译器编译代码

* 编译命令格式

```bat
CL [option...] file... [option | file]... [lib...] [@command-file] [/link link-opt...]
```

	* option 编译选项
	* file 一个或多个源代码、.obj和库的文件名。 CL将编译源代码并将 .obj 文件和库文件将被传递给连接器。
	* lib 一个或多个库的名称，这些库将被传递给连接器。
	* command-file 一个包含多个选项和文件名的命令文件。
	* link-opt 一个或多个传递给连接选项。

* 编译c 语言 Hello World 程序

	c 语言 Hello World 程序代码
	
```cpp
	#include <stdio.h>
	
	int main()
	{
		printf("Hello, World\n");
	}
```


	编译源代码


```bat
	cl /W4 hello_world.c
```
	
	其中， /W4 选项打开针对程序结构的警告，打开警告有助于开发人员查找一些难以发现的程序错误。
	如果c程序源代码没有使用 .c 扩展名，需要用 /Tcfilename 或 /TC 选项指定。

* 编译 c++ 语言Hello World程序

	c++ Hello World 程序代码
	
```cpp
	#include <iostream>
	
	int main()
	{
		std::cout << "Hello, World" << std::endl;
	}
```

	编译源代码
	
```bat
	cl /W4 /EHsc hello_world.cpp
```
	
	其中， /EHsc 编译选项用来打开标准异常处理。如果不打，编译器会提示警告信息。
	如果c++源代码没有使用 .cpp 扩展名，需要用 /Tpfilename 或 /TP 选项指定。
	
	
## 参考文档
* [MSDN CL编译选项](https://msdn.microsoft.com/EN-US/library/19z1t1wy(v=VS.140,d=hv.2).aspx)
