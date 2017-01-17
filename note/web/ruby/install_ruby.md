# 使用 RVM 安装包管理器安装ruby

## 安装 RVM （第一次尝试，失败）

### 安装命令

```bat
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
\curl -sSL https://get.rvm.io | bash -s stable
```


## 安装 RVM（第一次尝试，成功）

### 安装命令

* Install mpapis public key (might need `gpg2` and or `sudo`)

```bat
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
```

* Download the installer

```bat
\curl -O https://raw.githubusercontent.com/rvm/rvm/master/binscripts/rvm-installer
\curl -O https://raw.githubusercontent.com/rvm/rvm/master/binscripts/rvm-installer.asc
```

* Verify the installer signature (might need `gpg2`), and if it validates...

```bat
gpg --verify rvm-installer.asc &&
```

* Run the installer

```bat
bash rvm-installer stable
```

### 安装完成后提示

```bat
Installation of RVM in /usr/local/rvm/ is almost complete:

  * First you need to add all users that will be using rvm to 'rvm' group,
    and logout - login again, anyone using rvm will be operating with `umask u=rwx,g=rwx,o=rx`.

  * To start using RVM you need to run `source /etc/profile.d/rvm.sh`
    in all your open shell windows, in rare cases you need to reopen all shell windows.

# baijunjie,
#
#   Thank you for using RVM!
#   We sincerely hope that RVM helps to make your life easier and more enjoyable!!!
#
# ~Wayne, Michal & team.

In case of problems: https://rvm.io/help and https://twitter.com/rvm_io
```

## 既然提示了就给用户添加用户组 rvm

```bat
usermod -G rvm baijunjie
usermod -G rvm root
source /etc/profile.d/rvm.sh
```

## 安装ruby

```bat
rvm install ruby
```

## 安装过程中提示

```bat
Searching for binary rubies, this might take some time.
No binary rubies available for: centos/7/x86_64/ruby-2.3.3.
Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
Checking requirements for centos.
Installing requirements for centos.
Installing required packages: libyaml-devel, readline-devel, zlib-devel, libffi-devel, openssl-devel, sqlite-devel................................
Requirements installation successful.
Installing Ruby from source to: /usr/local/rvm/rubies/ruby-2.3.3, this may take a while depending on your cpu(s)...
ruby-2.3.3 - #downloading ruby-2.3.3, this may take a while depending on your connection...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
 18 13.7M   18 2555k    0     0   5912      0  0:40:41  0:07:22  0:33:19     0
```

速度慢的吓人....


