# PHPStorm

**_声明：内容来源于个人实验和个人理解，不保证泛用性和正确性，欢迎勘误和拍砖_**

## 简介

一句话简介：**我，开发工具，打钱**

（收费的，打钱才能用）

不过我们有破解方法

---

**_此处以 XAMPP 为 PHP 环境来进行配置，因此会有一点点不同（如 php.exe 的位置）_**

**_这些差异请各位按照各自的环境自行调整_**

---

## 安装

[官方下载地址](http://www.jetbrains.com/phpstorm/)请自行百度： PHPStorm ，安装过程不复杂，不赘述

在安装完成后，假如您是第一次启动 PHPStorm 将会出现下列窗口，询问您是否导入此工具的配置

![导入配置](https://s1.ax1x.com/2018/05/18/Cc9Yt0.png)

若您在过去使用过 PHPStorm，可以选择第一个选项，导入过去的配置

若您没有使用过 PHPStorm，第一个选项还自定义新配置的保存路径

若您既不想导入以往的配置，也不想修改默认配置保存路径，请选择第二个选项

选择确定之后，会要求您对 PHPStorm 进行激活，请选择第二个选项，使用激活码进行激活

![激活码激活](https://s1.ax1x.com/2018/05/18/Cc9a1U.png)

在输入激活码之前，我们需要做一点微小的工作

请打开浏览器，访问 [http://idea.lanyus.com](http://idea.lanyus.com)

您应该可以看到如下页面

**_请不要慌着获取注册码，请注意红框部分_**

![lanyus](https://s1.ax1x.com/2018/05/18/Cc9TAI.png)

我们需要找到 hosts 文件

hosts 文件位置

* **Windows**：C:\Windows\System32\drivers\etc\hosts

**_请在修改之前对 hosts 文件进行备份(简单地复制一下也是可以的)_**

> **_注意_**
>
> 若您是 Win 8/10/Vista 的用户，请将 host 文件复制到桌面再进行修改
>
> 这是因为 Win 8/10/Vista 具有良好的用户权限管理，导致无法在 hosts 所在目录下直接修改文件
>
> 需要复制到低权限需求的目录下再进行修改（比如桌面）
>
> 在修改完毕后，再复制回原目录

打开 hosts 文件，原内容如下

```ini
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#   127.0.0.1       localhost
#   ::1             localhost
```

修改为

```ini
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#   127.0.0.1       localhost
#   ::1             localhost

0.0.0.0 account.jetbrains.com
```

以上工作做完之后，回到 [http://idea.lanyus.com](http://idea.lanyus.com)

点击获取注册码，并复制

回到 PHPStorm

粘贴注册码到文本框内，直接确定即可

接下来选择界面风格

![界面风格](https://s1.ax1x.com/2018/05/18/CcCgVs.png)

推荐常用插件

![常用插件](https://s1.ax1x.com/2018/05/18/CcC42T.png)

## 配置

接下来是正式配置环节

这是初次安装 PHPStorm 出现的欢迎界面

![PHPStorm 开始](https://s1.ax1x.com/2018/05/18/CcCvRK.png)

我们需要为 PHPStorm 配置一些全局设置

这样在以后的开发中就可以偷懒

首先是配置 PHP 解释器

PHP 解释器，即 php.exe，在后面的测试中，内置服务器的启动会依赖这一配置

选项路径：File | Settings | Languages & Frameworks | PHP

这里有两个选项：

* **PHP language level**：即 php 语法支持版本，请与您安装的 php 版本一致
* **CLI interpreter**：即 php 命令行解释器，需要添加并选择，请添加您常用的解释器

![PHP Global instance](https://ws1.sinaimg.cn/large/e1413d51gy1frfty5cewzg216s0ovu0x.jpg)

其次调整 JavaScript 语言版本，为 ES 6 语法特性提供支持

选项路径：File | Settings | Languages & Frameworks | JavaScript

![ES 6](https://ws1.sinaimg.cn/large/e1413d51gy1frfv0wehbsg216s0ov4qp.jpg)

**_至此，PHPStorm 基础配置介绍完毕_**

[转到 XDebug 配置流程](XDebug.md)

[转到测试流程](Test.md)
