# 从c语言代码生成汇编
## Visual C++ 生成汇编

* 编译时生成汇编文件
```bat
cl /Fa hello.c
```

* 指定汇编文件的文件名
```bat
cl /Fahello.c hello.c
```

## gcc 生成汇编
```bat
gcc -S hello.c
```