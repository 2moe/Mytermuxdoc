# Note

**未完成，等待中**

# Think

在决定整这项目之前，先思考一下：

+ 项目对系统平台有限制吗?(限制windows平台only的项目就别试了)

+ 项目是否依赖于特定的编译器、基础C库？(例如依赖于gcc，glibc)

+ 对内核/硬件有特殊要求，例如Docker依赖于虚拟化技术，fakeroot依赖于sysv ipc，aircrack-ng依赖于支持混杂监听的kernel driver和无线网卡，这些条件往往非常苛刻(aircrack-ng要重编译内核，制作卡刷包并刷入，再用otg接外置网卡)或无法达成。

+ 项目的CPU消耗量很大，有心理准备吗？(例如Openjdk)

+ 项目对其依赖有特殊需求(例如crptography，它需要在编译Openssl库时加入`--no-engine`选项)

+ Termux没有对此项目合适的编译器/解释器。

+ 即使项目本身没什么问题，它的依赖也可能有上述问题。

总之，先把文档多读几遍，动手时才后悔是无用的。

# Fetch Source

注：过程依赖于一些工具，自行安装即可。

在运行一个项目前，先得整下来项目源码。

可能源码放在归档压缩包内，可能项目用git,svn一类的版本管理系统管理，总之先拉回来!

下面的例子默认Bash执行，fish会特别注明！

示例：

```shell
SRC="http://dev.gentoo.org/~tomwij/files/wiki/hello-world-1.0.tar.gz"

#用wget下载(是GNU wget而非默认的wget!执行pkg i wget -y; hash -r来启用gnu wget)

wget -c $SRC #-c意为启用断点续传

#也可以用axel等支持多线程下载的工具
```

反正是下好了。

gitrepo，应该这么整。

```shell
git clone https://github.com/knightking100/hello-worlds.git hello

#git仓库将拉取到hello目录

```

svn示例:

_等一个好心人帮忙写_



归档压缩包类型一般会是tar.gz，tar.xz或tar.bz2，也有用zip，7z和rar归档的人。

首先安装工具链。这一步简单。然后判断类型并解压(判断类型可用file命令)，也简单，网上随处可见。

注：一定要看看下载工具的输出，确定归档压缩包完整性。有条件还可检验MD5和SHA。


阅读Readme和Install，开始安装依赖。

_注:可通过Debian发行版的仓库寻找源码包_

_注：可通过Arch的[database](https://archlinux.org/packages)查找项目依赖_

# Check Language

安装和项目语言对应的编译器，解释器。

可能此语言的编译器termux没有，没关系。

_前面Think那部分再看一遍，做好战斗数月的心理准备，从编译编译器开始。_

还有，Python2和Python3不一样，一定看清楚。

# Hardcode

常有人在项目代码中硬编码目录，此时非得手动改不可。

```shell
pkg i silversearcher-ag
```

用ag查找项目中硬编码的目录，例如：

+ /etc

+ /usr

+ /bin

+ /tmp

+ /var

例子

```shell
ag -i '/var' src/ #查找src目录下所有文件中含/var的文本行并输出。
```

然后，应当用vi或emacs定位，修改。

# Install dependence

唯一要注意的事，使用pkg来代替apt。因为Termux的offical仓库只保留最新的包，可能和本地Package信息文件里的版本号不同。

本地package信息文件在此,可通过`apt update`来更新信息文件。

```shell
ls /data/data/com.termux/files/usr/var/lib/apt/lists
```

除了C共享库，可能还要安装一些语言模块。

**python**


注：此处指python3

python的包管理工具是pip。

开发者一般会建立一个叫requirements.txt的文件，其中包含项目所需的模块信息。此文件一般是用`pip freeze`命令生成的。


在项目根目录执行：

```shell
pip install -r requirements.txt > /dev/null 2> ~/.cache/error.log &
```

接着去吃点东西，喝点水，等待~~戈多~~error。

大多数时候依赖于C库的python模块是装不好的，先别紧张，用less看一下错误。

```shell
less ~/.cache/error.log
#按q退出
```

很重要的一件事是定位真正出错的模块，然后去浏览模块文档。确定模块有哪些C共享库依赖，又有什么特殊要求。

项目文档肯定要先读，万一开发者提供了Termux的安装脚本呢?(例如pupy)

下面举一个真实的例子：

SearX是一个旨在保护隐私的`Metadata search engine`项目，在线版本是searx.me。项目使用Python3编写。

看了一下requirements.txt，依赖中有lxml和cryptography，这两个都有C依赖。在Install.sh中查找，装好两个模块。随后全程顺利，看着Doc用sed把密钥替换了，完成。用searx搜索IT类内容感觉比Bing更方便，不过，在线版我更中意。

也可能项目根目录有setup.py，那么

```shell
python setup.py
```

这样安装。

整完直接运行，不编译。


**ruby**

_等一个好心人帮忙写_

**nodejs**

_同上_

**rust**

_同上_

**go**

_同上_



# Build


**C/C++**

>事实上，上面那些语言编写的项目整不好大多数时候都是C/C++的锅。

C，不用多介绍了，Unix信仰之一。麻烦和优势一样多。

C是传统编译型语言，开发流程是

```shell
写代码 -> 编译 -> 运行
```

C编译出的ELF文件包含最终的机器码，对就是一堆`1`和`0`组成的cpu指令!所以在PC上用常规方式编译出的ELF不适合爪机。因为PC的cpu指令集和爪机的不一样!事实上，C，Scheme，Algol这些高级语言可以移植到不同指令集的平台上已经是用户之幸了!在更早的时代，人们用一卷卷的打孔纸带存储程序，开发者用cpu指令编写程序，直接面对寄存器这些让人头都大的计算机底层概念。所以那时的程序员往往_抽很多烟，喝更多浓咖啡，一把大胡子_。

Go这类现代编译型语言变了很多，比如Go其实是基于Runtime的，编译出的是字节码，能脱离Go环境运行的技巧是

>把字节码和整个Runtime环境一起打包成ELF(所以Go的可执行文件奇大无比)

继续谈C，Termux上的c编译器是clang。没什么好说的，Apple和FSF轮子大战。一般也用不着直接碰clang。出于方便开发的目的，一个项目的C源码文件会有很多个。编译器先将每一个源码文件转换为object文件，然后用连接器将它们变成一个ELF文件：|。也可能有好几个。这个过程手动完成会很乏味，一般开发者会写一份Makefile，然后让用户在项目目录执行make，自动完成编译。

同样出于方便开发的目的，程序员们又弄出了头文件和共享库，这两个玩意直接导致了现在Unix上用户看到编译头都大的局面。即使是Gentoo的Portage，也常常要用户自己修复某些问题。其他Linux发行版就更麻烦了。当然，这是充满了开源精神和自由主义的Linux，若是在Aix那种私有的商业Unix上搞编译事业……

>与中国人一出国就爱国同理，使用商业Unix是迄今为止最快的，理解开源与自由重要性的方式。

Windows使用体验可以，但中国Windows应用生态成功地做到了_毫无死角，极其智能地监控和伤害用户_。不过多讨论。同时编译体验不行。这是FSF最大的成功之一:让全世界用上gcc和autoconf。

Autoconf,Cmake，这是一类制造Makefile的工具，总之挺有意思的，链式反应。

Autoconf依赖于m4，一门奇妙的宏处理语言。Autoconf会先从configure.ac文件产生configure，一个Bash脚本，也可能项目直接放出configure脚本。

等一下!运行configure之前，先做点准备工作。

```shell
find . -name 'config.sub' -exec chmod u+w '{}' \; -exec cp -f "${PREFIX}/share/libtool/build-aux/config.sub" '{}' \;          
find . -name 'config.guess' -exec chmod u+w '{}' \; -exec cp -f "${PREFIX}/share/libtool/build-aux/config.guess" '{}' \;
```

然后可以按通用步骤来了。像这样

```shell
CC=clang bash configure --prefix=${PREFIX} && make && make install
```

C项目是这样，C++要改。


当然，可能项目用cmake管理，甚至于开发者手写了Makefile，那也没关系。


推荐几本书：

_How Linux works_ 美.Brian Ward 著

_跟我一起写Makefile_ 中.陈皓 著


尽管放心，八成会失败。Orez的开发者曾尝试过在Termux上编译Orez，大失败。所以也别想太多，成了给termux-package仓库发个pullrequest，没成把Error信息，设备信息，环境信息拿好，去开个issues。

C++编译同样艰难，建议先学一会C++。
