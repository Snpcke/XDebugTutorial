# XDebug

**_声明：内容来源于个人实验和个人理解，不保证泛用性和正确性，欢迎勘误和拍砖_**

---

## 简介

在程序开发当中 Debug（调试）是相当必须的功能

现代调试工具至少提供以下功能

### 1. 设置断点

**_断点的主要作用是能让运行中的程序暂停，暴露问题现场_**

> 在实际项目开发中，我们往往会遇到 **玄学问题**：
>
> 比如：
>
> 注册时，获取到的 **用户名与预期不同** （有时会把前台写错）
>
> 有时因为前端错误（如：后端接受 POST 请求数据，而前端错写成按 GET 方法提交）
>
> 在这些时候，往往因为代码过多，或者心情烦躁，导致肉眼 Debug 效率低下
>
> 但总的来讲，我们对自己的代码结构是 **有一定的 B 数的**
>
> 这个时候，断点就能 **辅助我们确定问题的来源，并直接暴露问题**

### 2. 变量/内存监控：

**_变量/内存监控能避免编写冗长的 var_dump()，能直接输出并观察运行中程序的各种变量值；并能分析内存状态，为玄幻问题提供解决依据_**

> 断点的主要作用是 **暴露问题** ，变量监控则是 **发现问题的放大镜**

相对于其他的程序设计语言而言，PHP 的运行环境不像其他语言，**它的运行环境不直接提供 Debug 接口**

我们需要自己通过 PHP 插件的形式，来为 PHP 提供 Debug 接口，而这个接口的名字就叫 XDebug

当然，PHP 的 Debug 接口插件并不止 XDebug 一种，只是恰好它提供的支持比较好罢了

---

## 安装

在安装 XDebug 之前，我们需要

1.  **完整的 PHP 环境**，推荐 PHP >= 7.0.x，**最新的 XDebug 已经准备停止对 5.x.x 的 PHP 进行支持**，但并不是完全不支持
1.  **支持 XDebug 的 IDE（开发环境）**，推荐 [PHPStorm](http://www.jetbrains.com/phpstorm/?fromMenu)，**因为只会这个**，同样支持 XDebug 的开发环境还有：**Eclipse**、**NetBeans**、**Zend Studio**，以及某些强悍的编辑器

[转向 PHPStrom 安装流程](PHPStorm.md)

考虑到各位存在各种各样的开发环境

* **WAMP**：学校 FTP 下载的 WAMP 提供的 PHP 编译版本（以 VC 2008 编译）过低，我们需要[下载最新版 WAMP](http://www.wampserver.com/en/#download-wrapper)

* **phpStudy**：由于老版本（远古版本 ~ 2016 版）的 phpStudy 提供的 PHP 编译版本同样过低，我们需要[下载最新版 phpStudy](http://www.phpstudy.net/)

* **XAMPP**：推荐[下载最新版 XAMPP](https://www.apachefriends.org/download.html)

* **自编译环境**：请接受膜拜，您不需要看这个

我们提供以下配置方案

---

## 1. phpStudy

首先，请安装最新的 [phpStudy](http://www.phpstudy.net/)，不赘述

安装好之后请确保 PHP 版本切换到 7.x.x（以 7 打头）

![版本切换](https://ws1.sinaimg.cn/large/e1413d51gy1frfwarhmwbg216s0ovkjl.jpg)

**_接下来是核心部分_**

我们需要打开 PHP 的配置文件，利用 phpStudy 打开 PHP 根目录

![phpStudy PHP 根目录](https://ws1.sinaimg.cn/large/e1413d51gy1frfwl0wv83g216s0ovhdt.jpg)

打开 php.ini 然后将配置文件滚动到底部

在文件底部添上

**_P.S. ：以 ; 开头的是注释_**

```ini
; 更改后
[XDebug]
; 这个值是 XDebug 插件所在的位置，一般需要自己下载
; 而 phpStudy 提供了 XDebug 插件
; 我们只需要找到它的位置即可
; 比如我【使用】的 phpStudy 是安装在 C 盘下的 phpStudy 目录下
; 且版本是 7.0.12-nts
; 所以需要在
; C:\phpStudy\PHPTutorial\php\php-7.0.12-nts\ext
; 目录下找到 php_xdebug.dll
zend_extension = "C:\phpStudy\PHPTutorial\php\php-7.0.12-nts\ext\php_xdebug.dll"
; 开启调试功能，1 为开启
xdebug.remote_enable = 1
; 选择代理方式，请参照手册修改
xdebug.remote_handler = "dbgp"
; 调试地址，可修改
xdebug.remote_host = "localhost"
; 选择调试模式，请参照手册修改
xdebug.remote_mode = "req"
; 调试端口，可修改
xdebug.remote_port = 9000
```

**_然后重启 Apache 服务_**

**_至此，phpStudy XDebug 配置完毕_**

[转向测试流程](Test.md)

---

## 2. XAMPP 7.x.x

**_注意：此版本的 XAMPP 是最新版，PHP 版本为 7.x.x_**

**_低版本(PHP 5.x.x)配置方式与高版本基本一致_**

首先，我们需要安装最新的 [XAMPP](https://www.apachefriends.org/download.html)

XAMPP 的安装，此处不再赘述

**_然后，请启动 XAMPP 的 Apache 服务_**

XAMPP **并没有**自带 XDebug 插件，因此我们需要上 [XDebug 官网](https://xdebug.org/) 下载

但在此之前，我们需要确定我们的 PHP 版本

输出 phpinfo()是最保险的方案，XDebug 官网提供工具用于读取 phpinfo()

如果各位有更好的方法直接输出 phpinfo()请直接输出即可

如果没有，请继续看

首先，进入 XAMPP **Web 根目录**

![打开XAMPP目录](https://ws1.sinaimg.cn/large/e1413d51gy1frfwr4p3nwg216s0ovkjl.jpg)

**_htdocs 即 xampp web 根目录_**

在此目录下新建文件 phpinfo.php

内容如下

```php
<?php
    echo phpinfo();
```

然后，打开浏览器，进入 [http://localhost/phpinfo.php](http://localhost/phpinfo.php)

**_Win 10 用户请不要使用 Edge 浏览器打开该页面，否则输出的信息将可能无法使用_**

![phpinfo](https://ws1.sinaimg.cn/large/e1413d51gy1frfx73f9y3g21gt0rrhdu.jpg)

你可以看到这样的信息，**_不要关闭这个窗口_**

现在让我们回到 [XDebug 官网](https://www.baidu.com/link?url=iBrBnbx_5gR2i1PfD3bCXaE6Ccgri8k4z6C3U0YKD43&wd=&eqid=b95f1bc80001276d000000055afe4287)

![XDebug 支持](https://ws1.sinaimg.cn/large/e1413d51gy1frfxcheliog21gt0rr1kx.jpg)

接下来就可以看到以上页面

回到 [http://localhost/phpinfo.php](http://localhost/phpinfo.php)

**全选网页**Ctrl + A，然后**复制**Ctrl + C

回到刚刚打开的 [XDebug 支持](https://xdebug.org/wizard.php)

将我们刚刚复制的内容填入文本框内

![XDebug In](https://s1.ax1x.com/2018/05/18/C6bTDf.png)

并点击红圈中的按钮，然后得到

![XDebug Out](https://s1.ax1x.com/2018/05/18/C6bL5Q.png)

**_请不要关闭这个窗口，还有用_**

此时，从我们输出的信息可以看出，XDebug 未安装，且当前 PHP 的编译版本为 VC 15

但是这些并不重要

下方的 INSTRUCTIONS 才是重点

此处可以发现，INSTRUCTIONS 为我们提供了详细步骤和下载链接

这个下载链接可以下载 XDebug 插件

> 当然，也有可能有些同学运气不够好，您看到的是另外一些信息
>
> 那么原因可能如下：
>
> 1.  您没有按照步骤来，没有安装最新的 phpStudy / XAMPP / WAMP (这将导致您的 PHP 版本或 PHP 编译版本不够高)
> 1.  您的电脑没有安装足够多、足够新的 Visual C/C++ 运行库
>
> 如果您无法独立解决，请@我们的小天使 魔灯宏

现在请下载这个文件，并放到你找得到的位置

文件下载完成之后，让我们打开 PHP 根目录

![打开 PHP 根目录](https://ws1.sinaimg.cn/large/e1413d51gy1frfx03wl5ig216s0ovnpd.jpg)

在这个目录下有我们需要注意以下文件/文件夹

1.  **ext**：PHP 插件的安装目录
1.  **php.exe**：PHP 解释器的可执行文件
1.  **php.ini**：PHP 配置文件

接下来，请将下载好的 XDebug 插件复制到 PHP 根目录下的 ext 文件夹内

![复制XDebug](https://ws1.sinaimg.cn/large/e1413d51gy1frgr0is83ig211q0mnb2a.jpg)

让我们重新看看 XDebug 官网工具输出的信息

![XDebug Out](https://s1.ax1x.com/2018/05/18/C6bL5Q.png)

下方的 INSTRUCTIONS 的第 3 条告诉了我们

1.  要打开哪里的 php.ini
1.  要干嘛

那么，照本宣科，打开 php.ini 滚动到底部

![PHP.ini](https://ws1.sinaimg.cn/large/e1413d51gy1frgsieouw4g211q0mnu0x.jpg)

添加如下内容

ini
[XDebug]
; 此处路径值由 INSTRUCTIONS 第 3 条提供
zend_extension = "C:\xampp\php\ext\php_xdebug-2.6.0-7.2-vc15.dll"
xdebug.remote_enable = 1
xdebug.remote_handler = "dbgp"
xdebug.remote_host = "localhost"
xdebug.remote_mode = "req"
xdebug.remote_port = 9000

**_然后，请重启 Apache 服务器_**

**_至此，XAMPP 7.x.x XDebug 配置完毕_**

[转向测试流程](Test.md)
