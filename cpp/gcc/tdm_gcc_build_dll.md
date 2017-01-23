# 使用 TDM-GCC 在 WINDOWS 上编译生成dll

## 参考资料

* [MinGW gcc 生成动态链接库 dll 的一些问题汇总](http://blog.csdn.net/liyuanbhu/article/details/42612365)

## 测试代码

* count_of_bit.c 计算数字中二进制位1的个数函数，用来生成dll

```cpp
/* count_of_bit.c */
int count_of_bit(int val)
{
	int cnt = 0;
	int v = 1;
	for (int n = 0; n < 32; n++)
	{
		if (val & v)
		{
			cnt++;
		}
		v = v << 1;
	}
	return cnt;
}
```

* main.c 主函数，调用dll中的函数，用来测试dll

```cpp
/* main.c */
#include <stdio.h>
#include <stdlib.h>

int count_of_bit(int val);

int main( int argc, char* argv[])
{
	int val = 0;
	if( argc > 1 )
	{
		val = atoi(argv[1]);
	}
	printf("bit of %d is %d\n", val, count_of_bit(val));
}
```

## 编译 count_of_bit.c 生成dll

```bat
gcc -shared -o count_of_bit.dll -Wl,--output-def,count_of_bit.def,--out-implib,count_of_bit.lib count_of_bit.c
```

参数说明：

* -shared 生成动态连接库

* -o 输出dll文件名称

* -Wl 后续跟传送给ld的参数

> + --output-def,count_of_bit.def 生成导出函数定义文件 .def
>
> + --out-implib,count_of_bit.lib 生成导入库文件 .lib 

## 编译 main.c 生成 test.exe 可执行文件

```bat
gcc main.c count_of_bit.lib -o test.exe
```

## 测试可执行文件

```bat
# test 0
bit of 0 is 0
# test 1
bit of 1 is 1
# test 127
bit of 127 is 7
# test 77889900
bit of 77889900 is 10
```
