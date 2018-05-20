# 测试

***声明：内容来源于个人实验和个人理解，不保证泛用性和正确性，欢迎勘误和拍砖***

## 目录

- [配置浏览器](#browser)
- [准备](#ready)
- [检查 XDebug 安装情况](#check)
- [测试 XDebug](#test)

-------------------------

***此处以 XAMPP 为PHP 环境来进行配置，因此会有一点点不同（如 php.exe 的位置）***

***这些差异请各位按照各自的环境自行调整***

-------------------------

***此时，我们假设您已经成功安装了 PHP 环境，PHPStorm 和 XDebug***

如果没有安装成功... 那就很尴尬了...

-------------------------

<ac id="browser"></ac>

## 配置浏览器

接下来我们需要准备 XDebug 中的另外一环，浏览器

***当然，这一步不是必须的，若您有其他的客户端，如 RESTful Client ，CLI only Browser 等客户端，请自行根据需要配置***

***浏览器的作用是触发 XDebug 请求，同时···浏览目标页***

之前的步骤为我们部署了Server（服务器端）环境，要想触发 XDebug，还需要 Client （客户端），而客户端的组成即包含了PHPStorm和浏览器

浏览器有多种选择

- Chrome (Chromium) 及其它套壳浏览器
  - 360 浏览器
  - 360 极速浏览器
  - QQ 浏览器
  - ...
- FireFox
- ...

任何一款浏览器，理论上都支持 XDebug

但上述浏览器能通过安装插件的方式，更方便触发 XDebug 过程

***由于，Chrome 严格的插件管理机制，以及插件商店要翻墙，***

所以我们选择使用火狐（FireFox）

不推荐安装旧版本的插件，因为插件标准日新月异，很可能装上之后，跑不起来

浏览器的安装，不做赘述

请打开火狐浏览器，进入插件市场

![插件市场](https://ws1.sinaimg.cn/large/e1413d51gy1frhn3he0klg21gt0rrqv5.jpg)

搜索XDebug，并安装

![安装XDebug](https://ws1.sinaimg.cn/large/e1413d51gy1frhn87kv1sg21gt0rre81.jpg)

***重启浏览器***

接下来您将能够在地址栏看到，一只小虫子图标

![按钮](https://ws1.sinaimg.cn/large/e1413d51gy1frhncn4hjtg21gt073dkb.jpg)

请对小虫子**右键**

***至此，浏览器配置完毕***

-------------------------

<ac id="check"></ac>

## 检查 XDebug 安装情况

您可以直接通过在phpinfo()中搜索 XDebug来检查配置情况

***但搜到了，并不代表安装成功，要能用***

为了方便下一步测试，我们直接打开 PHPStorm 来检查配置情况

首先，打开PHPStorm

然后打开设置，打开PHP 解释器配置

![XDebug](https://ws1.sinaimg.cn/large/e1413d51gy1frfvjpde4ig216s0ovu0p.jpg)

若看到Debugger 标志出现 XDebug x.x.x 字样，这就意味着，至少我们的配置是能够被 PHP 正确加载

<ac id="ready"></ac>

## 准备

打开PHPStorm，新建项目，放于Web 根目录下

![新建项目](https://ws1.sinaimg.cn/large/e1413d51gy1frgtmecr0ug21gt0rru0x.jpg)

新建test.php文件

![新建文件](https://ws1.sinaimg.cn/large/e1413d51gy1frhlbxre9og21gt0rrwqw.jpg)

为了方便，我们调整一下按钮布局

![调整布局](https://ws1.sinaimg.cn/large/e1413d51gy1frhlg72w2tg21gt0rr49g.jpg)

然后在test.php文件中写入一些php 语句**（随便写）**

![编辑文件](https://ws1.sinaimg.cn/large/e1413d51gy1frhlmnckp2g21gt0rrn7e.jpg)

添加断点，在行号右边的一列，点击鼠标

![添加断点](https://ws1.sinaimg.cn/large/e1413d51gy1frho4bl8z7g21gt0rrguq.jpg)

PHPStorm 启动项目的方式比较多，对于微型项目或小型项目，可以直接通过右上角按钮，打开浏览器

![打开浏览器](https://ws1.sinaimg.cn/large/e1413d51gy1frhp86p57ng21gt0rrtk0.jpg)

这种方式，会直接运行当前文件，这里有一些需要注意的点：

> 在默认情况下，以上述方式运行项目并不会使用你安装的PHP 环境
>
> 若不经过配置， PHPStorm 会在内部启动一个内置服务器以运行您的项目
>
> 注意，这种方式的缺点在于：虽然它会使用您的php.ini，但这些请求不会经过 Apache
>
> 这将导致一些 Apache 进行的优化过程无法起作用，同时无法负担大型项目和压力测试
>
> 注意您的地址栏
>
> ![地址栏](https://ws1.sinaimg.cn/large/e1413d51gy1frhpnfp7x9j21hd038mxk.jpg)
>
> URL 并不是预想中的localhost/test/test.php，即不是默认使用 80 端口
>
> 而是经过了63342端口
>
> 这是经由内置服务器启动的标志
>
> 为了避免这种情况，我们需要进行一些配置

回到 PHPStorm，打开设置，进入部署设置

选项路径：File | Settings | Build, Execution, Deployment | Deployment

![部署设置](https://ws1.sinaimg.cn/large/e1413d51gy1frhpvw7v7fg21gt0rraou.jpg)

添加新的部署配置，这里我们添加本地位置，因为此处的服务器运行在本地

想进行远程开发的各位，可以添加远程位置。

![添加本地](https://ws1.sinaimg.cn/large/e1413d51gy1frhq7yn3q2g21gt0rrqoe.jpg)

这里为什么要使用http://localhost/test作为web 服务器的根目录呢？

不知道您是否还想的起：***我们的项目处于 XAMPP 的 web 根目录下***

而且，我们的项目叫：***test***

这也就意味着，通过localhost/test这一 URL 可以访问到这个项目

这样的配置也就意味着：对于本项目而言，我们把localhost/test视作Web 根目录

在运行项目时，就不会启动内置服务器，而是直接访问localhost/test

***但，这样的配置是不严谨的，具体如何改善，请各位自行探究***

![URL](https://ws1.sinaimg.cn/large/e1413d51gy1frhqi1j67fg21gt0rr7i5.jpg)

此时，URL 即和我们预想的一致，并且所有请求都会经过 Apache 服务器进行解析、传递

***接下来终于进入正题：测试 XDebug***

-------------------------

<ac id="test"></ac>

## 测试 XDebug

回到 PHPStorm

审视一下我们的按钮栏

会发现一个电话按钮，这个按钮的介绍是Start Listening for PHP Debug Connections

点击，开始监听 Debug 请求

![开始监听](https://ws1.sinaimg.cn/large/e1413d51gy1frhqpqpi12g21gt04ldil.jpg)

然后重新运行当前文件

![重新运行](https://ws1.sinaimg.cn/large/e1413d51gy1frhquz61aqg21gt0rrk4w.jpg)

嗯... 没有反应...

这是因为我们还没有开启浏览器的 XDebug 开关

请回忆一下：我们在之前安装了浏览器 XDebug 插件

***这个插件的用途就是用于触发 XDebug 请求***

现在，开启XDebug 插件，刷新当前页面

![打开并刷新页面](https://ws1.sinaimg.cn/large/e1413d51gy1frhqzdlt7bg21gt0rrn1l.jpg)

现在请注意到您的任务栏

![闪烁](https://ws1.sinaimg.cn/large/e1413d51gy1frhr1q0vftj20j3017jrf.jpg)

此时，您的 PHPStorm 会因为接受到了 XDebug 请求发生闪烁

让我们回到 PHPStorm

此时，PHPStorm 会因为接受到意料之外的 Debug 请求，而出现提示

当然，若不想看到这个提示框，您可以选择预先配置或直接确定，PHPStorm 会自动添加相关配置

![Debug 请求](https://ws1.sinaimg.cn/large/e1413d51gy1frhr4l8sn6j21a60qpq4t.jpg)

从这个窗口中，我们可以看到一些详尽的信息，包括：请求来源，请求目标等...

不需要过多处理，直接点击左边按钮，接受即可

![Debug 视图](https://ws1.sinaimg.cn/large/e1413d51gy1frhrudwqoej21a00qo0vo.jpg)

此时，由于已经添加断点的缘故，PHPStorm 自动打开了Debug 视图

接下来我们看向Debug 视图

![下方 Debug 视图](https://ws1.sinaimg.cn/large/e1413d51gy1frht9943h9j219i0awjsf.jpg)

第一排需要注意的是这10 个按钮，我们逐一说明

![按钮](https://ws1.sinaimg.cn/large/e1413d51gy1frht98ykw1j20as02mjrb.jpg)

- 1 **跳转到执行点**：当您在 Debug 时来回浏览多个文件，却突然忘记执行到什么位置时，可以点击它，回到执行点（即深蓝色的那一行）

- 2 **单步越过**：简称 “步越” 或 “步进”，越过当前行，继续执行下一行代码，当运行到函数执行而不想了解函数细节时适合使用

- 3 **单步进入**：简称 “步入”，当前行是函数或其他复杂逻辑时，可进入其实现细节，当想要了解实现细节时，适合使用

- 4 **单步进入（强制）**：和步入相似，但强制步入可以进入某些原生函数，观察其实现或声明细节，这个功能对于 PHP 来说似乎不明显

- 5 **单步跳出**：简称 “步出”，与步入相反，作用是跳出当前代码段（如函数、逻辑段等）

- 6 **运行到光标位置**：让程序运行到光标所在位置

- 7 **即时运行**：将会打开一个窗口，允许程序员运行一些 PHP 语句来进一步了解状况

- 8 **显示变量地址**：决定是否显示出变量的内存地址

- 9 **隐藏内容为空的全局变量**：决定是否隐藏内容为空的全局变量

- 10 ***效果不明确，请自行研究***

接下来是最左边的一列按钮

![最左边按钮](https://ws1.sinaimg.cn/large/e1413d51gy1frhszuz9b4j202y0af74d.jpg)

- 1 **恢复运行**：继续运行程序，直到被断点中断

- 2 **暂停程序**：当断点触发时会自动进入这个状态，或者当存在常驻程序时，也可以手动暂停

- 3 **终止程序**：停止当前正在运行的程序，同时也会中断请求

- 4 **浏览断点**：浏览当前项目中所有的断点

- 5 **忽略断点**：决定是否忽略所有断点

- 6 **重置视图布局**：当手残关闭了某个窗口时，可以使用这个按钮恢复

- 7 **设置选项**：对视图进行设置

***至此，基本的 Debug 功能介绍完毕***
