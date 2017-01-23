# 升级 Centos 6 的 glibc 版本

## 升级原因

因 Centos 6.8 最高只提供 glibc 2.12 版本， 而项目中使用的一些库需要较高版本的 glibc，为了使用这些库，需要将系统的 glibc 版本升级到较高的版本。

## 查看系统当前 glibc 库版本

```sh
$ strings /lib64/libc.so.6 |grep GLIBC_
$ rpm -qa |grep glibc
```

## 通过源码编译安装 glibc

1. 从 glibc [官方网站](http://www.gnu.org/software/libc/)下载glibc 源码

glibc 2.14 源码下载FTP地址为：http://ftp.gnu.org/gnu/libc/glibc-2.14.tar.xz

```sh
wget http://ftp.gnu.org/gnu/libc/glibc-2.14.tar.xz
···

2. 解压缩源码

```sh
xz -d glibc-2.14.tar.xz
tar -xvf glibc-2.14.tar
```

如果需要prots库还需要：
```sh
wget http://ftp.gnu.org/gnu/libc/glibc-ports-2.14.tar.xz
xz -d glibc-ports-2.14.tar.xz
tar -xvf glibc-ports-2.14.tar
mv glibc-ports-2.14 glibc-2.14/ports
```

3. 创建编译目录并切换当前目录到编译目录

```sh
mkdir build
cd build
```

4. 配置 glibc

简单的配置安装目录到 /opt
```sh
../configure --prefix=/opt/glibc-2.14
```

某些资料把 glibc 安装到 /usr/bin 目录：
```sh
../configure  --prefix=/usr --disable-profile --enable-add-ons --with-headers=/usr/include --with-binutils=/usr/bin
```

5. 编译 glibc

```sh
make
```

5. 安装 glibc

```sh
make install
```

## 替换原系统的 libc.so.6 软连接

1. 删除系统的 libc.so.6 软链接

```sh
rm -rf /lib64/libc.so.6 
```

2. 让 /lib64/libc.so.6 软链接指向新编译的 glibc

```sh
LD_PRELOAD=/opt/glibc-2.14/lib/libc-2.14.so  ln -s /opt/glibc-2.14/lib/libc-2.14.so /lib64/libc.so.6
```

注意，glibc 是系统中非常基础的库，删除软连接后系统的 ls ln 等命令都不能正常工作，所以需要指定 LD_PRELOAD 来保证命令正常执行。

如果升级失败，可以使用下面的命令恢复到升级前的状态

```sh
LD_PRELOAD=/lib64/libc-2.12.so ln -s /lib64/libc-2.12.so /lib64/libc.so.6 
```

## 注意事项

* 因 glibc 是非常基础的库，升级需谨慎。
* 如确实有必要升级，尽量采用保守的方法，升级至较近的版本
* 最新的 glibc 需要较新的 gcc 编译器，例如 glibc 2.24 版本需要 GCC 4.7 以上版本才能编译。其他要求可查看源码下的 INSTALL 文件。
* 在虚拟机中升级 Centos 6.8 的 glibc ，完成后重启系统 glibc 版本被恢复到升级前的状态。如何永久升级尚需要继续研究。