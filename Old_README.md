![termux](https://github.com/myfreess/Mytermuxdoc/blob/master/pictures/termux.png)

# Termux不完全指南

[+]推荐&帮助：

命令行的艺术：https://github.com/jlevy/the-art-of-command-line/blob/master/README-zh.md

Termux官方wiki：https://wiki.termux.com/wiki/Main_Page

RE:0从零开始的Termux：https://github.com/breathiness/learn-termux

Archwiki：https://wiki.archlinux.org

Linux基础工具使用指南：https://i.linuxtoy.org/docs/guide/ch17.html

bilibili上的高质量Linux学习视频up主：http://space.bilibili.com/7125370?share_medium=android&share_source=copy_link&bbid=AmFQNFUzVmBUY1czT31PfU8tGCwef0cmF2sOinfoc&ts=1538784100488

然而他用Mac。

Linux挖坑不埋指南：https://segmentfault.com/a/1190000003813761

不要相信他说的话！不要！Gentoo是世界上最可怕的操作系统之一，它甚至都不是Linux(LFS至少是纯正Linux)！

Linux 内核详解:https://github.com/MintCN/linux-insides-zh

Pypi:https://pypi.org/

Explainshell，一个可以解释命令行含义的网站:https://explainshell.com

http://www.freebuf.com/geek/170510.html

http://www.sqlsec.com/2018/05/termux.html

[+]初始化

# 选择shell

# bash
![bash](https://github.com/myfreess/Mytermuxdoc/blob/master/pictures/bash.png)
 
bash是Termux及大多数linux发行版的默认shell(但Termux还默认安装了dash)

启动文件为`$PREFIX/etc/bash.bashrc`和`~/.bashrc`

注：这只是一种简单的说法，bash启动文件的详细情况见下文。

 * PS1

Termux默认只定义了bash提示符为`$`,不包括当前路径，未免不太方便

本人修改bash提示符为['当前路径']，这已经够我用了。

修改方法：`nano ~/.bashrc`，然后修改提示符变量PS1。

```shell
export PS1='[\w]\$'
```

`\w`意为当前路径，必须处于单引号包裹中。

bash提示符完全文档：https://wiki.archlinux.org/index.php/Bash/Prompt_customization_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)

 * bash-completion
 
bash补全还是有的。 

安装&使用：

```shell
(pkg in bash-completion; echo "test -d $PREFIX/share/bash-completion&&source $PREFIX/share/bash-completion/bash_completion" >> ~/.bashrc)
```
然后输入命令时按Tab键，就可以补全参数了。顺带一说，直接在bash会话中按Tab也可以补全目录和文件名。

# zsh
![zsh](https://github.com/myfreess/Mytermuxdoc/blob/master/pictures/zsh.jpg)

zsh是一个现代化的shell，兼容部分bash语法。

安装:

```shell
apt install zsh -y
touch ~/.zshrc
```
启动文件为$HOME/.zshrc(简单说法)

# oh-my-zsh
![ohmyzsh](https://github.com/myfreess/Mytermuxdoc/blob/master/pictures/oh-my-zsh.png) 
 
zsh的配置相当麻烦，所以一般使用oh-my-zsh这个一键脚本进行配置
 
termux有一键安装oh-my-zsh的脚本，可以更换终端配色与字体。

酷安原帖：https://www.coolapk.com/feed/2439237 

安装完成后使用`~/.termux/colors.sh`可选择配色方案，`~/.termux/fonts.sh`可更换字体。

安装:

```shell
apt install zsh git curl -y
bash -c "$(curl -fsSL https://github.com/Cabbagec/termux-ohmyzsh/raw/master/install.sh)"
```

安装后默认主题是agnoster,默认启用git插件。

![agnoster](https://github.com/myfreess/Mytermuxdoc/blob/master/pictures/agnoster.png)

 * 主题

可以通过编辑`$HOME/.zshrc`中的`ZSH_THEME`变量来更换主题。

 * zsh-syntax-highlighting
 
https://github.com/zsh-users/zsh-syntax-highlighting 

默认包含于Cabbagec的脚本中。

假定一个命令不是shell函数，别名，PATH内的可执行文件(就是说这个命令不可以执行)，zsh-syntax-highlighting就会把命令渲染成红色。

 * zsh-autosuggestions
 
[![CircleCI](https://circleci.com/gh/zsh-users/zsh-autosuggestions.svg?style=svg)](https://circleci.com/gh/zsh-users/zsh-autosuggestions) 

<a href="https://asciinema.org/a/37390" target="_blank"><img src="https://asciinema.org/a/37390.png" width="400" /></a>

为zsh增加一个像fish一样的智能命令建议，从shell历史中匹配可能的命令。

安装:

```shell
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
#启动时运行
echo "source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc
```

 * OMZ

如果想省事，可以按这个来，：https://github.com/myfreess/oh-my-termux 

# fish
 
安装:`apt install fish`

fish是开箱即用型shell,UI风格对用户非常友好。

fish 的配置文件是 (~/.config/fish/config.fish)，不过一般我们不改动它。

 * oh-my-fish

![omf](https://github.com/myfreess/Mytermuxdoc/blob/master/pictures/omf.png)

快速，轻量的fish配置框架。
 
```shell
#ohmyfish安装
apt install fish curl git
curl -L https://get.oh-my.fish > install
fish install --path=~/.local/share/omf --config=~/.config/omf
exec fish
#切换shell
chsh -s fish
```
 * omf使用

Oh My Fish 自带的辅助命令工具 omf 可以帮助你快速获取安装新插件和主题。

`omf update`

更新自身和已安装的所有插件和默认主题。

`omf install [<name> or <url>]`

安装 一个或多个 插件。

你可以通过输入指定的 URL 直接安装插件 omf install URL

当没有传入参数时，omf将会从 bundle 文件检索并安装本地尚未安装的插件和主题。

`omf list`

显示本地已安装的插件列表。

`omf theme <theme>`

应用一个主题。查看全部可用主题执行 omf theme。安装之前你也可以预览现有主题。

`omf remove <name>`

移除主题或插件。

 * 卸载

`omf destroy`

卸载 Oh My Fish.

 * termux独有插件

https://github.com/sagebind/plugin-termux

这是oh-my-fish开发组的一位成员专为termux开发的插件。 

注：fish不兼容bash的script语法。

# 冷水
 
1.ohmyzsh可能因为某些因素卡死你的终端！ 

2.fish的智能推荐不区分大小写！

3.用了oh-my-zsh后报错很难看(这是我换用bash的真正原因)。



注：[Termux Shell列表](https://wiki.termux.com/wiki/Shells) 

注：在Termux的shell会话中可通过输入`exit 0`来关闭一个shell会话，Ctrl-d也可。
 
注：在Termux中长按屏幕左边滑出的'keyboard'可打开一些特殊键
 
# Termux上的chsh是什么？
 
Linux上的chsh通过修改`/etc/passwd`文件来改变用户的启动Shell，那Termux这个单用户机制的应用呢？

答案是通过修改`~/.termux/shell`文件，这个文件不存在时Termux就去启动bash，存在时则将其作为启动Shell。

chsh不过一bashscript而己，它会从`$PREFIX/bin`中寻找用户需要的shell，并在`~/.termux`目录中建立名为shell的符号链接指向它。

# [附录]:More about shell

>这里的shell有时指linux shell应用，有时指命令行。

>如果不会用命令行，那不是你的错。GNU/linux独有的精神是自由/justforfun，从unix那里继承的cli操作界面不见得就很好。如果一个人一味狂热地拥护所谓的"Unix哲学"却无视自由精神，那他肯定最终会滚入Mac的怀抱(除非没钱)。不过，既然来玩Termux了，该学还是要学一点的。

 
 * 字面量与shell的字符替换
 
你输的命令shell会先对其中可以用现有规则处理的文本进行处理，然后再决定下一步干什么。

echo $1试试，你会发觉其奇特之处的。

然后执行echo '$1'，查看它们的不同之处。
 
 * 命令编辑
 
按左右箭头特殊键就行，打错字了可以改。
 
 * 历史命令
 
按上下箭头，可以看自己以前用过什么命令。 

 * Linuxshell基本工作原理：exec()和fork()
 
Linux内核提供一种叫系统调用(system call)的玩意，帮助其它程序处理问题。

fork()可以复制出两个相同的，运行在运存中的程序。exec()则可以将请求此调用的程序替换成另一个程序(自己换成自己也不是不行)。这一过程可以用exec命令实现，运行exec ls,会显示一些文件/目录名，然后termux就关闭了，因为shell被ls替换了。

shell在运行一个应用时，会先调用fork()生成一个子shell,子shell则调用exec()将自身替换为真正需要运行的应用。

fork()是比较消耗资源的，所以shell优先调用内置命令，这样的命令由shell自身实现，不调用fork()。

 * 在zsh中使用Tab键
 
你就，一直按，光标移到你想打开/进入的文件/目录，就可以停手了。 

 * 手写zshrc

上面我们说到oh-my-zsh这个zsh配置框架，它很方便，但不够快！如果你是个热爱动手的人，那么是时候自已写zshrc了！

Archwiki给出了详细的方案，可见此处：https://wiki.archlinux.org/index.php/Zsh_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)

 * Xonsh
 
Xonsh是个用python写的shell，兼容bash。 奇特之处在于它同时支持bash&python语法，甚至可以混合使用！

 * fzf
 
 * 隐藏在zsh中的神秘力量
 
数学支持： 
 
```shell
#载入数学函数模块 可以进行一些比较高级的运算
#(也可以将此句写在配置文件中)
% echo "zmodload zsh/mathfunc" >> ~/.zshrc
% exec zsh
#$((数学表达式)) 进行运算，使用 echo 显示结果
% echo $(( sin(1/4.0)**2 + cos(1/4.0)**2 - 1 ))
-1.1102230246251565e-16
```  

 * 深入理解命令行
 
注：以下内容来自王垠

在你执行`ls -l .c`命令时，发生了什么？

shell（在这个例子里是bash）从终端得到输入的字符串 "ls -l .c"。然后 shell 以空白字符为界，切分这个字符串，得到 "ls", "-l" 和 ".c" 三个字符串。

shell 发现第二个字符串是通配符 "*.c"，于是在当前目录下寻找与这个通配符匹配的文件。它找到两个文件： foo.c 和 bar.c。

shell 把这两个文件的名字和其余的字符串一起做成一个字符串数组 {"ls", "-l", "bar.c", "foo.c"}. 它的长度是 4.

shell 生成一个新的进程(使用fork()这个由Linux内核提供的系统调用，编者注。)，在里面执行一个名叫 "ls" 的程序，并且把字符串数组 {"ls", "-l", "bar.c", "foo.c"}和它的长度4，作为ls的main函数的参数。main函数是C语言程序的“入口”，这个你可能已经知道。

ls 程序启动并且得到的这两个参数（argv，argc）后，对它们做一些分析，提取其中的有用信息。比如 ls 发现字符串数组 argv 的第二个元素 "-l" 以 "-" 开头，就知道那是一个选项——用户想列出文件详细的信息，于是它设置一个布尔变量表示这个信息，以便以后决定输出文件信息的格式。

ls 列出 foo.c 和 bar.c 两个文件的“长格式”信息之后退出。以整数0作为返回值。

shell 得知 ls 已经退出，返回值是 0。在 shell 看来，0 表示成功，而其它值（不管正数负数）都表示失败。于是 shell 知道 ls 运行成功了。由于没有别的命令需要运行，shell 向屏幕打印出提示符，开始等待新的终端输入……

 * 不用alias加速命令输入
 
alias是bash的内置命令，用于对标准输入进行字符串替换。

现在尝试一下：

```shell
alias wd="cd $PREFIX/var/dpkg"
wd
pwd
---snip---
#以下为pwd的输出
/data/data/com.termux/files/usr/var/dpkg
---snip---
```
将长，复杂，需要重复使用的命令用alias制定一个短别名，保存在bashrc中，可有效减少打字量。

风险:命令参数有时也会被别名替换。

 * 用函数控制重复性工作
 
函数是shell的一种特性。用户可以将一个命令序列定义为一个函数，节省打字量。

让我们简单操作一下。

```shell
function delete()
#定义函数的名称，这只是其中一种定义形式。
{
#用户定义的函数内容从此符号后开始
if [ -d $@ ]; then
    rm -rf "$@"
else
    echo "这不是一个目录。"
fi
}
#函数内容结束
mkdir empty
delete empty
#使用函数
touch empty
delete empty
---snip---
这不是一个目录。
---snip---
#函数对接收到的参数进行了条件判断
```
这比数学上的函数可简单多了！而且其意义也完全不同。

注：关于if then else语句和$@，下面会有说明。

附：我的自动化github同步函数

```shell
autopush()
{
case $@ in
	$empty)
		something=nothing
		;;
	 *)
		 something=$@
		 ;;
esac		 
git add *
#我只写文档才这样干，有志于编程的各位不要学我。
git commit -m "$something"
git push origin master
}
```

Linux用户的行为是非常矛盾的，一方面写配置文件时他们非常勤快，另一方面在使用交互式shell时连字都懒得多写几个……

注：上面的函数结构适用于bash，不一定适用于其他shell(例如fish)……

使用set命令可以查看你定义了哪些函数。

函数不会打开一个子shell运行，所以别在函数里写exit。

 * shell变量与环境变量		

让我们来打个比方:

变量→纸箱子。

变量的值→纸箱里的水果。

shell变量→只有shell才能打开的箱子。

环境变量→任何进程都可以打开的箱子。

接下来谈谈如何定义变量，这很简单。

```shell
ok=false
#定义一个名为ok的变量，值为false。
echo $ok
#将变量ok的值输出
#使用$<name>来使用一个变量的值。
export ok=false
#使用export这个shell内置命令设置环境变量。
#因为没有进程会去关心/访问ok这样一个环境变量
#所以无法演示
unset ok
#将变量ok"取消"掉，使其值为null
export PATH=/sbin
#这个命令效果倒是立竿见影
#不要慌，长按屏幕，点击More，再选择kill process即可
#回到Termux，终端恢复正常
```

上面这一堆操作是针对bash的，其他shell可能会有所不同。但概念是相同的。

一些对Termux很重要的环境变量：

```shell
echo $PATH
---snip---
/data/data/com.termux/files/usr/bin:/data/data/com.termux/files/usr/bin/applets
#PATH变量的值是一些以冒号分隔的目录，当你执行命令时，shell会去这些目录中寻找对应的linux应用。
#排在前面的目录shell会优先查询
#对PATH内文件的改变shell不会实时查询，shell有一套"缓存"机制
#大多数时候"缓存"机制会加快命令执行速度，少数时候会带来一些问题(例如coreutil,下文可见)
#未完结
```
使用printenv可以查看所有的环境变量。

在Linux发行版上，系统所需环境变量的定义依赖于/etc/profile这个初次启动shell时运行的shellscript.

在Termux上就不一样了，环境变量的定义不依赖于profile(profile的内容会被shell读取并作为命令执行，但经我查看，Termux的profile并没有定义任何一个环境变量……)，而由Termux主应用定义(如果你在bashrc里啥也没写，Termux照样运行得好好的。)

 * 运行一个不在PATH内的可执行文件
 
在文件名前加点和斜杠即可。

例如，在home目录有个名为baidupcs-go的可执行文件，那么我应该怎样执行它?

1.进入home目录

```shell
cd ~
#我没写错
```
2.执行

```shell
chmod 755 baidupcs-go
./baidupcs-go
```
异常简单。 
 
 * type -a

type是个shell内置命令，运行type <command>可以查看一个命令的类型，type -a则列出所有结果。

 * 用管道传输数据
 
管道是shell的一种特性，它经常用于交互式shell中。

管道可以将一个命令的"结果"传递给另一个命令，那么什么是结果？

答案是：标准输出

演示：

```shell
apt list | less
#以一种较平和的方式显示你可以安装的应用
ps | grep $(whoami)
#查看termux内运行的所有linux应用与termux主进程
curl http://distfiles.gentoo.org/releases/arm/autobuilds/20161129/stage3-armv7a-20161129.tar.bz2 | tar xj
#下载一个gentoo的stage包，并直接传输给tar解压
#下载结束时已经解压完毕


 * 布尔运算：与或非的选择

Linux程序运行结束时会给其父进程(这词真怪)发送一个退出码，一般是0，出错时返回其他数字(也有例外，像diff)。使用echo $?可以查看上一次运行的命令的退出码。

这是布尔运算(就是逻辑判断)的基础。让我们操作一把。

```shell
mkdir ~/.zsh&&rmdir~/.zsh
#创建一个目录,如果创建成功再把它删掉
#如果~/.zsh这个目录早就在那儿了，mkdir会报错
#~/.zsh目录就不会被删除
#&&：如果前一条命令退出码为0，就执行后一条命令
#||与&&相反，如果前一条命令退出码不为0，才会执行后一条命令
mkdir ~/.zsh||echo "~/.zsh目录已存在"
#假如在使用||运算符时，程序返回的退出码为0？
#则后一条命令不执行。&&同理，反着想就行
mkdir ~/.zsh&&echo "~/.zsh目录创建成功"||echo "~/.zsh目录已存在"
#想想这条命令几个意思？
```
当然fish不会支持&&。

 * $()：将命令的输出作为变量

```shell 
echo $(echo "Hello World")
#这个太无聊，再看看别的吧

``` 
 * ${}：展开变量
 
echo ${HOME}试试? 
 
 * 输出重定向
```shell 
>
>>
2>
2>>
``` 
 
 * <：以文件作为输入
 
极少用到。 
 
 * <()将命令的输出作为文件 
 
 * shell编程
 
bash可以把文件名作为命令参数，这说明了什么？
 
是的，命令行也可以作为一种编程语言(但它对数学的支持奇烂，zsh好一点)。

几乎所有人都用bash作为script解释器，当然oh-my-zsh/和fisherman的开发者肯定不是这种人。

zsh基本兼容bash语法，还有很多独有的特性，想学zsh编程请看：https://github.com/goreliu/zshguide

 * here文档


# 选择文本编辑器

Linux上最流行的编辑器是Vim和Emacs，nano则适用于新手。

但termux上的nano对中文的显示支持有问题，中文字符串会随机缩短。zile更水，居然不支持中文输入……

~没奈何，Vim与Emacs取其一。~(我用上micro了！居然会有这种质感风格的轻量cli编辑器！)

Vim高效快速，Emacs功能强大，自行选择。Neovim作为vim的分支，也作为选择之一。

Termux官方列出了所有Termux上可用的文本编辑器，详情见wiki。

 * 论Emacs的全能性

Emacs在设计之初的目标就是：提供一个完整的系统工具集所应有的功能(从浏览器到游戏)，又因为Emacs Lisp的出现，它可以让用户简单地对它进行扩展。

例如Emacs其实可以煮咖啡(coffee.el)，不是玩笑话，详情可搜索词条"Emacs煮咖啡"。

Emacs不全面介绍，面向一切不懂计算机的人：https://segmentfault.com/a/1190000012267697

 * 退出Vim

按下'ESC'键，进入命令模式，输入':wq'将保存文件并退出Vim。 

# vim中文支持
 
```shell
mkdir ~/.vim
cd ~/.vim
cat > vimrc <<EOF
set fileencodings=utf-8,gb2312,gb18030,gbk,ucs-bom,cp936,latin1
set enc=utf8
EOF
source ~/.vim/vimrc
#结束
```

注：google中文输入法无法在termux内输入中文。

注：使用Vim或Emacs时按手机返回键，点按呼出键盘将不会生效，需点按屏幕左边滑出的'keyboard'按钮。

尽管vim老手从不用上下左右键，但我等新手还是少不了它的

~酷安某用户修改了termux的特殊键，增加了上下左右键，修改版apk我放在仓库里了，有需要自己下。~

后注：termux更新后增加了juicessh风格的特殊键，修改版已从仓库中移除。

 * 横屏编辑
 
除非使用平板，否则很难兼顾特殊键与中文。 

 * IDE与GUI编辑器
 
重要的是用工具做什么，而不是用什么工具。vim用户中存在部分鄙视GUI与IDE的人(当然大多数只是开玩笑。)，这不友好。

开发一个运行在linux上的好的开源或自由软件，好事。用的是vscode，依然是好事。

用vim却为微软工作的人应该自我反省一下。

当然我对Windows记事本持反对意见，太TM坑了，就是写字也不要用。

# 选择软件源

 * Termux第三方源列表

[1]Tuna镜像源

[2]由xeffyr维护的旧版本源[Warning?]

[3]由xeffyr维护的Extra源[Warning!]

[4]由Auxilus维护的metasploit源

[5]由Grimler91维护的rootpackage源

[6]its-pointless源，含gcc

 * 手动添加源
 
```shell
mkdir tmp&&cd tmp
apt install gnupg dirmngr curl

#mirror&&extra源
apt-key adv --keyserver pool.sks-keyservers.net --recv 9D6D488416B493F0
echo 'deb https://termux.xeffyr.ml/ stable main' >> $PREFIX/etc/apt/sources.list
#echo 'deb https://termux.xeffyr.ml/ extra main x11' >> $PREFIX/etc/apt/sources.list

#root源
apt-key adv --keyserver pgp.mit.edu --recv A46BE53C
mkdir -p $PREFIX/etc/apt/sources.list.d
echo "deb https://grimler.se root stable" > $PREFIX/etc/apt/sources.list.d/termux-root.list
#或者
apt install root-repo -y

#its-pointless源
curl -O https://its-pointless.github.io/pointless.gpg | 
apt-key add pointless.gpg
mkdir $PREFIX/etc/apt/sources.list.d
echo "deb [trusted=yes] https://its-pointless.github.io/files/ termux extras" > $PREFIX/etc/apt/sources.list.d/pointless.list

#x11源
apt-key adv --keyserver pool.sks-keyservers.net --recv 45F2964132545795
echo "deb https://termux-x11.ml x11 main" >> $PREFIX/etc/apt/sources.list
#或者
apt install x11-repo -y

#更新aptcache
apt update
```

 * 后缀为dev的deb包是什么？

pkg-config文件与include文件。

 * termux特色package

包括termux-tools,termux-exec,tsu等

经检查，除termux-exec，termux-elf-cleaner使用C语言编写，其他大部分为bashscript，不得不让人感叹Linux的高度可定制性！

下面给出列表。

termux-tools:bashscript工具集，包含`termux-fix-shebang termux-info termux-open termux-open-url termux-reload-settings termux-setup-storage termux-wake-lock termux-wake-unlock`

termux-api:与Android交互需要使用的工具集，powered by bashscript。

termux-apt-repo:

termux-create-package:字面意思

termux-am:apk文件，在`$PREFIX/libexec/termux-am`目录下。是am命令的Android8.0特别版。

[附录]am命令

am全称activity manager，你能使用am去模拟各种系统的行为，例如去启动一个activity，强制停止进程，发送广播进程，修改设备屏幕属性等等。

就是Android上的应用调试器，给开发者用的。

termux-elf-cleaner：elf文件处理工具

termux-exec：下面介绍



# 软件包管理

 * apt install <package>

安装应用。 

 * apt search <query>

以关键字搜索应用。 

 * apt update
 
更新deb包索引信息，当初次打开无法安装软件包时可运行此命令。

注：因为官方源不保留旧软件包，所以最好每次安装软件包之前都update一次。

 * apt remove <package>
 
卸载软件包。 

 * apt下载的deb包在哪儿？
 
`$PREFIX/var/cache/apt/archives`

 * apt源配置文件

`$PREFIX/etc/apt/sources.list` 

 * apt的本质
 
基于dpkg封装的自动化包管理器。

 * 手动安装deb包
 
dpkg -i ./xxx.deb

 * postinstall
 
postinst这个脚本存在于很多deb包中，初次安装时它会被执行。

 * 解压deb包
 
dpkg -x <package> <dirname> 

 * 为什么不能兼容debian系发行版的deb包(那怕架构相同)？
 
因为软件的安装目录是在deb包中被预制定好的，并且以绝对路径形式制定。

 


>期许:我希望我将来可以达到下图的水准

![mydream](https://github.com/myfreess/Mytermuxdoc/blob/master/pictures/mydream.png)

不过现实还差得远呢。

# TermuxTalk

>组织意念，随心写字

[+]获得读写sdcard权限

`termux-setup-storage`获得sdcard读写权限。

`ln -s target linkname`建立符号链接方便管理。


[+]目录结构

termux根目录为/data/data/com.termux/files

内有home和usr两个目录，对应的变量是$HOME和$PREFIX。

如果觉得这样的目录结构不习惯，可以执行

```shell
apt install proot -y
termux-chroot
```

但这对性能有一定损伤。


[+]lftp
 
轻量的cliftp客户端，交互式操作。

```shell
#使用以下命令登录ftp服务器：
lftp ftp://用户名[:密码]@服务器地址[:端口]
#标准方式，推荐
#如果不指定端口，默认21端口
#如果不在命令中使用明文输入密码，连接时会询问密码(推荐)
#可以使用“书签”收藏服务器站点，也可以在lftp中为当前站点定义别名：
lftp >bookmark           #显示所有收藏
lftp >bookmark add <别名>  #使用 别名 收藏当前站点
#使用别名登录 ftp服务器：
lftp <别名>
#文件下载
#单个文件
lftp >get <name>	 
#目录	
lftp >mirror <dirname>
```
 * windows支持
 
```shell 
lftp >set ftp:charset gbk   #设置远程编码为gbk
lftp >set file:charset utf8 #设置本地编码(Linux系统默认使用 UTF-8，这一步通常可以省略)  
```

[+]openssh
 
openssh是linux上最流行的ssh实现。 
 
包含ssh,scp,sftp,sshd,sftpd，ssh-keygen等多个程序。

sshd是ssh服务守护进程，ssh则是客户端。

Termux的sshd默认端口为8022，不支持密码登录，必须将你自己的ssh公钥输出到`~/.ssh/authorized_keys`这个文件内。

如要在外部网络访问可以使用frp和ngrok将你的Server端口映射到公网上，如梯子钱充够了也可按官方教程使用tor进行端口映射。

管理sshd

```shell
#启动
sshd
#关闭
lsof -i | grep sshd | awk '{print $1}' | xargs kill
```

 * 何为公私钥?

ssh使用一对密钥完成加密/解密过程，被分发给他人的是公钥，自己留着的是私钥。对sshd来说，用户只持有sshd生成的公钥，sshd自己则保留私钥。

ssh的密钥在~/.ssh下，sshd的密钥在$PREFIX/etc/ssh下。

公私钥加密涉及非对称加密，以我的数学水平尚无法解释。

 * 配置文件
 
termux的ssh配置异常简单，无需任何更改。 

# [+]proot

proot是`chroot`及`mount --bind`的用户空间实现，一个简单的容器应用。

termux的proot包内还包含了一个名为`termux-chroot`的bashscript，可在Termux内模拟linux目录结构。

proot使用帮助：https://github.com/myfreess/Mytermuxdoc/blob/master/HowToUseProot.md

顺便一说，github上的termux用户们热心地编写了一系列用于安装运行发行版的bashscript。

可选的发行版：

Fedora,kali,Arch,debian，ubuntu，alpine……

安装：

官方建议见此处:https://wiki.termux.com/wiki/PRoot

隔壁群管理的脚本:https://github.com/YadominJinta/atilo ，可以快速安装linux发行版。

## [附录]不选择Linux的n个理由
![Linux](https://github.com/myfreess/Mytermuxdoc/blob/master/pictures/Linux.jpg)
![Linux](https://github.com/myfreess/Mytermuxdoc/blob/master/pictures/Linux2.jpg)

Linux日常:bug糊脸，依赖大坑，编译报错，没声音，桌面boom……

都很正常，冷静，被坑得多了也就习惯了。

但是人不能被动挨打，所以我们要宣扬主动挨打！

多编译，多帮社区打包(AUR)，学习编程，只用自己配置的WM……

在感受到打包维护的辛苦之后，在感受到定制应用的成就感之后，你就会感叹:

~这帮货写的pkgbuild和Makefile都是什么玩意！~ 打包者真不容易！

但是我不会这么干的，cpu烧不起。

## [附录]桌面环境

经常看到别人乐滋滋晒lxde？其实，像openbox这种WM才是手机最好的选择。

关于桌面怎么装，当然Archwiki最有发言权。先装Xorg，其他自由发挥。

也可以看这里：https://i.linuxtoy.org/docs/guide/ch19.html

## [附录]华圾(华为手机)上的proot I/O error

解决方案见此处：https://github.com/termux/proot/issues/15

[+]tsu
 
tsu是Termux独有的su程序，允许用户以root权限运行Termux内的linux应用。

使用：

```shell
apt install tsu
tsu
#exit可退出root状态
#单次使用root权限
tsudo command
```
[附录]文件权限搞砸了怎么修

```shell
#确定你现在不是root
export user=$(whoami)
tsu
cd ~
cd ..
chmod -hR $user *
```

[+]Git
![git](https://github.com/myfreess/Mytermuxdoc/blob/master/pictures/git.gif)
git是一个分布式的版本控制系统。

一般用户只用`git clone <repourl> <dirname>`这一个命令。

例子：

```shell
#拉取oh-my-zsh安装脚本
git clone https://github.com/Cabbagec/termux-ohmyzsh ~/termux-ohmyzsh
#<repourl>：https://github.com/Cabbagec/termux-ohmyzsh
#<dirname>：~/termux-ohmyzsh
```

但中国网络环境出了名的不好，一般github上的大型项目传输中途会断流！

使用shadowsocks成本又高，最好还是用ssh拉取源码。

如果希望使用ssh拉取源码，那么应该注册一个github账号，创建自己的ssh密钥，并将公钥提交到github。

```shell
apt install openssh
ssh-keygen -t rsa -C "youremail@example.com"
cat $HOME/.ssh/id_rsa.pub
#输出的内容就是你的公钥
```

将公钥提交到github需要在浏览器内完成，此处不作演示。

 * github
![github](https://github.com/myfreess/Mytermuxdoc/blob/master/pictures/github.jpg)
又称gayhub，干啥的我不用说了吧？

 * 用github pages建博客
 
Markdown使用说明：https://www.appinn.com/markdown/ 

[+]Python/Python2
 
python 是目前全世界最流行的编程语言，分为2和3两个版本(语法部分改变)

python有时也指python解释器。`apt install python python2 -y`即可安装解释器。

使用python2编写的项目不能使用python3解释器来运行，反之亦然。

使用`python xxx.py`  或 `python2 xxx.py`来运行一个Python项目。

 * 运行报错？
 
可能的几种情况
 
[1]未安装需要的模块。报错信息`no module named xxxx`

`pip install xxxx`即可
 
[2]解释器版本问题
 
一般会出现:syntax error:
 
[3]脚本自身问题(bug)
 
这需要自身有一定python基础才能修复，反正我没有。
 
[4]权限问题，某些脚本需要以root权限运行。
 
若有Android root权限，在Termux内输入`pkg install tsu`,安装完成后输入`tsu`，让Termux应用获取root权限即可。
 
在输入`tsu`后，可输入`exit`回到普通模式
 
注：在root用户状态下创建文件不是个好主意，可能带来严重的权限问题。
 
注：安装软件包和python依赖包也属于创建文件的行为。
 
 * pyc文件

pyc文件是python的虚拟机字节码文件。事实上，py文件先被解释器翻译为pyc字节码文件，然后导入PVM(Python Virtual Machine,python虚拟机)中运行。

 * pip

pip是一个自动化的python依赖包管理器

同理，使用python2编写的模块只能用pip2安装

```shell
pip install <ModuleName>
#安装依赖包
```

若在repo目录内使用，先查看requirements.txt,若有此文件直接`pip install -r requirements.txt`即可安装所有依赖包。

-r表示从文件中读取参数(read)。

 * 安装报错？
 
[1]使用了错误的pip版本。
 
[2]此模块部分用C编写，需编译。
 
先试着安装`python-dev pkg-config clang`等编译所需工具,如果仍然报错则寻找报错信息中有无`include<xxx.h>`。 若有，则安装对应的dev包和lib包即可。

注：也有人说只要clang装好就没有问题，太扯了…… 

仍无法正确安装，则建议先在github的issues区自行搜索。

`apt install lib*dev`是个好方法。

当没有可用方案时，可以自行创建一个issues，有时实际情况的确难以由用户自行解决。

看看这里也行：https://wiki.termux.com/wiki/Instructions_for_installing_python_packages

搜索引擎永远是我们的好帮手，经统计常见问题大概三分钟出解决方案，下面以pynacl的安装为例。官方的解决方案比较复杂，第三方方案则相当简单。

```shell
apt install clang python python-dev libsodium libsodium-dev
export SODIUM_INSTALL=system
pip install pynacl
```
注：编译需要较多电量与时间。

原解决方案出处:Pypi

原文如下：

```shell
PyNaCl relies on libsodium, a portable C library. A copy is bundled with PyNaCl so to install you can run:
$ pip install pynacl
If you’d prefer to use the version of libsodium provided by your distribution, you can disable the bundled copy during install by running:
$ SODIUM_INSTALL=system pip install pynacl
```
# scrapy安装

scrapy是python中一个著名的爬虫模块，但它的依赖之一cryptography安装极其复杂。

issues:https://github.com/termux/termux-packages/issues/2847

首先，用`uname -m`查看自己的手机(或chrome本)cpu架构，根据结果选择方案。

aarch64与arm架构请前往issues下载xeffyr编译的openssl包。

x86架构则需自行编译openssl。编译时加入no-engine选项。(真的惨)

注：不要使用版本1.1以下的openssl包，这会破坏apt。

如果只安装cryptography，那么准备已经结束。

scrapy：

```shell
pkg install libffi-dev libxml2-dev libxslt-dev
ln -s $PREFIX/include/libxml2/libxml $PREFIX/include/libxml
pip3 install scrapy
#安装步骤来自YadominJinta@github.com
```
装好也不要太高兴，python用户的日常一般是这样的：

![error](https://github.com/myfreess/Mytermuxdoc/blob/master/pictures/runtime.jpg)

注：its-pointless@github维护的社区源中有python模块scipy和numpy。

[+]Nodejs
 
Nodejs是javascript语言的服务器端实现。

PackageManager/模块管理器:npm

在repo中使用:npm install

# npm安装任何包都报错？
 
解决方案:https://github.com/rvagg/node-worker-farm/commit/0b2349c6c7ed5c51e234e418fad226875313e773

手动解决

```shell

vi $PREFIX/lib/node_modules/npm/node_modules/worker-farm/lib/farm.js


#将'maxConcurrentWorkers        : (require('os').cpus() || { length: 1 }).length'内的1改动一下，改成一个小于cpu核心数的数字。
```
[+]ruby

ruby也是一门面向对象的编程语言，但比Python更适用于Web建站，也更重视语法规范。
 
`ruby xxx.rb`可运行一个ruby脚本
 
 * gem
 
gem是ruby的模块管理工具。
 
 * bundler
 
bundler是一个自动化的，面向版本库/repo的ruby模块管理器。
 
 * 安装及使用
 
```shell
gem install bundler
cd <repodir>
#一定保证作者写了Gemfile
bundle install
```

注意:
 
有时repo的启动脚本没有.rb这个后缀，正常，可用head <filename>来查看它的shebang。

何为shebang?
 
shebang是脚本的首行，一般会定义脚本解释器的位置。
 
termux-exec可以使termux适应Linux风格的shebang。
 
或用'termux-fix-shebang <script>' 修改脚本shebang。

一般可在`$PREFIX/bin`中建立脚本的软链接方便使用。
 
这时你应预先修改启动脚本的shebang。
 
 * 常见问题
 
自己认真看看报错即可，仍然建议多看Termux的issues。

注：google翻译是个好东西。

[+]Golang

go是跨平台的编译型语言，golang则是一个go编译器的开源实现。

以csploit项目的核心编译为例：
 
```shell
apt install golang
go get github/cSploit/daemon
#go get将自动下载项目及其依赖，有时也会自动编译
#golang一般无法完成这一步
#请自行挂梯子
cd $GOPATH/src/github/cSploit/daemon
go build -i
```
golang会在$HOME建立go工作目录，在其中的bin子目录有编译完成的elf可执行文件。src目录则包含项目源码，当bin目录为空时，进入源码目录使用`go build`来编译项目。

注：编译时耗电量较大，占用运存也很多

`go run xxx.go`则可以测试而不编译此项目。

总之，编译前多看README是不会有错的。

有一篇好文可以读一读:https://splice.com/blog/contributing-open-source-git-repositories-go/

注：golang编译时不构建共享库。

 * 使用make完成构建

```shell
git clone <repourl>
cd <repodir>
make
make install
#必须有Makefile
```

[+]curl & wget 
 
普通的下载器(-_-)……

言归正传，curl支持的传输协议其实不少，以下为官方介绍:

![curl](https://github.com/myfreess/Mytermuxdoc/blob/master/pictures/curl.svg)

>A command line tool and library for transferring data with URL syntax, supporting HTTP, HTTPS, FTP, FTPS, GOPHER, TFTP, SCP, SFTP, SMB, TELNET, DICT, LDAP, LDAPS, FILE, IMAP, SMTP, POP3, RTSP and RTMP. libcurl offers a myriad of powerful features https://curl.haxx.se/

wget就略单薄一点，只有http和ftp(加上ssl)支持。

它们的下载线程是单线程机制的，所以效率上肯定比不上aria2，优势在于它们是web调(ri)试(zhan)与自动化任务的一把好手。

例如在美剧Mr.Robot中，主角用wget拿了个服务器低权限shell，然后开始提权&搞破坏……

[+]aria2
 
极致强大的cli下载器，支持Metalink等现代下载技术。 

开启rpc配合transdroid食用更佳。

安装&开启rpc

```shell
apt install aria2
#开启rpc
aria2c --enable-rpc --rpc-listen-all
```
然后可以用transdroid方便地从127.0.0.1:6800连接了，下载奇快！

[+]Weechat&irssi
 
Irc聊天客户端。
 
[+]Tor
 
Tor是一个开源的匿名上网项目，既可以避免服务器地址被用户得知，也可防止用户地址被查出。

Tor网站即互联网上一般所说的暗网。

 * 创建tor域名
 
注：全部操作只适用于termux。

只对lighttpd开启的http服务进行了映射，需要映射其他服务请自行更改配置。

```shell
nano $PREFIX/etc/tor/torrc
#############以下为torrc内容##########
#Enable TOR SOCKS proxy
SOCKSPort 127.0.0.1:9050
#Hidden Service: Http
HiddenServiceDir /data/data/com.termux/files/home/.tor/hiddenservice
HiddenServicePort 80 127.0.0.1:8080
############结束################
mkdir /data/data/com.termux/files/home/.tor/hiddenservice
tor&
#切换到新会话
cat ~/tor/hiddenservice/hostname
#显示的内容就是你的tor域名。
```

[+]mutt&alpine
 
邮件客户端。 
 
[+]busybox&coreutil

```shell
busybox是一个实用linux小工具集合，默认已安装。
termux的busybox是定制版，移除用户管理等termux用不到的命令。
注：httpd暂时无法使用。[Wed Oct  3 15:36:03 CST 2018]
coreutil同busybox。
[~/workdir]$ busybox
BusyBox v1.29.3 (2018-09-10 22:47:04 UTC) multi-call binary.
BusyBox is copyrighted by many authors between 1998-2015.
Licensed under GPLv2. See source distribution for detailed
copyright notices.

Usage: busybox [function [arguments]...]
   or: busybox --list[-full]
   or: busybox --install [-s] [DIR]
   or: function [arguments]...

        BusyBox is a multi-call binary that combines many common Unix
        utilities into a single executable.  Most people will create a
        link to busybox for each function they wish to use and BusyBox
        will act like whatever it was invoked as.

Currently defined functions:
        ar, arp, awk, base64, basename, bbconfig,
        bunzip2, bzip2, cal, cat, chattr, chgrp,
        chmod, chown, chpst, chrt, cksum, clear,
        cmp, comm, cp, cpio, crond, crontab, cut,
        date, dc, dd, diff, dirname, dos2unix, du,
        echo, egrep, env, envdir, expand, expr,
        false, find, fold, free, fsync, ftpd,
        ftpget, ftpput, fuser, getopt, grep,
        gunzip, gzip, hd, head, hexdump, hostname,
        httpd, id, ifconfig, inotifyd, install,
        iostat, ipcalc, kill, killall, less,
        linux32, linux64, ln, ls, lsattr, lsof,
        lsusb, lzma, makemime, md5sum, mkdir,
        mkfifo, mknod, mktemp, more, mpstat, mv,
        nc, netstat, nice, nmeter, nohup, nproc,
        od, patch, pgrep, pidof, pipe_progress,
        pkill, pmap, popmaildir, printenv, printf,
        ps, pscan, pstree, pwd, pwdx, readlink,
        realpath, reformime, renice, reset,
        resize, rev, rm, rmdir, route, run-parts,
        runsv, runsvdir, rx, script, scriptreplay,
        sed, sendmail, seq, setsid, setuidgid,
        sha1sum, sha256sum, sha3sum, sha512sum,
        shuf, sleep, smemcap, softlimit, sort,
        split, start-stop-daemon, strings, stty,
        sum, sv, svlogd, sync, sysctl, tac, tail,
        tar, tcpsvd, tee, telnet, telnetd, test,
        tftp, tftpd, time, timeout, top, touch,
        tr, true, tty, ttysize, udpsvd, uname,
        uncompress, unexpand, uniq, unix2dos,
        unlink, unlzma, unxz, unzip, uptime,
        usleep, uudecode, uuencode, vi, watch, wc,
        wget, which, whoami, whois, xargs, xz,
        yes
[~/workdir]$ coreutils --help
Usage: coreutils --coreutils-prog=PROGRAM_NAME [PARAMETERS]...
Execute the PROGRAM_NAME built-in program with the given PARAMETERS.

      --help     display this help and exit
      --version  output version information and exit

Built-in programs:
 [ b2sum base32 base64 basename cat chcon chgrp chmod chown cksum comm cp csplit cut date dd dir dircolors dirname du echo expand expr factor false fmt fold ginstall groups head id join kill link ln logname ls md5sum mkdir mkfifo mknod mktemp mv nice nl nohup nproc numfmt od paste pathchk pr printenv printf ptx pwd readlink realpath rm rmdir runcon seq sha1sum sha224sum sha256sum sha384sum sha512sum shred shuf sleep sort split stat stdbuf stty sum sync tac tail tee test timeout touch tr true truncate tsort tty uname unexpand uniq unlink vdir ]


```

 * 有意思的现象
 
bash下如果卸载coreutil会导致ls等命令暂时丢失。

解决方案：`hash -r`

原因:PATH缓存导致的问题。

奇怪的是，优先级靠前的目录找不到，后面的目录就不找了?

重启之后又正常了……

想必bash在重启之后才刷新了PATH内可执行文件的索引信息吧。

注:来自xeffyr的回复

Just a behaviour of bash - binary path caching. Run `hash -r` to fix.

果然是bash的锅。

 * awk
 
 * vi
 
 * chroot&mount --bind
 
 * ln

 * mount&df

[+]sed

[+]m4

[+]screenfetch&neofetch

[+]file

[+]sendmail

[+]micro

Micro：轻量的质感风格命令行文本编辑器

优秀特性:

 * 极其易用
 
 * 跨平台支持(使用Go编写)
 
 * 中文支持极佳
 
快捷键：

Ctrl-q: 退出

Ctrl-s: 保存

Ctrl-o: 打开文件

Ctrl-z: 撤销

Ctrl-y: 重做

Ctrl-f: 查找

Ctrl-n: 查找下一个

Ctrl-p: 查找上一个

Ctrl-a: 全选

Ctrl-c: 复制

Ctrl-x: 剪切

Ctrl-v: 粘贴

Ctrl-u: 向上滚动半页

Ctrl-d: 向下滚动半页

PageUp: 向上

PageDown: 向下

Ctrl-e: 执行一个命令 

[+]game
 
gnuchess,gnugo啥的。

extra源有doxbox,stable源有fontz，玩些字符游戏没问题！

apt search game可以找到更多游戏！

[+]command-not-found

在你试图执行一个不存在的命令时，提醒你如何安装此命令对应的应用。

[+]GNUscreen&tmux

终端复用工具。

[+]macchanger

修改网卡mac地址工具。

[+]db

后缀名为db的数据库文件的编辑器。

[+]rsync

专业级文件备份工具。

特性:用它删除文件比rm快。

[+]stunnel

使用SSH封装非加密服务的工具。

[+]lynx&w3m

命令行下的web浏览器。

坑b。

[+]nnn

一款命令行文件管理器。

还行，nnn -S我比较喜欢。

主页:https://github.com/jarun/nnn

[+]cowsay

```shell
$ cowsay 山回路转不见君，雪上空留马行处
 _________________________________________
/ 山回路转不见君，雪上空留马              \
\ 行处                                    /
 -----------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```
[+]attr

[+]htop
 
[+]nmap
 
[+]hydra
 
[+]tsocks

# [附录]编译C源码文件

README告诉我，`autoconf&&./configure&&make&&make install`四步走，就能把软件装好！

事实上大多数时候没这么好的事。

言归正传，Termux上的c编译器是`clang`，比gcc更轻量。

当然Linux一贯的特点是兼容并蓄，所以安装后它会建立名为`cc`的符号键接指向自身，以适应使用gcc的一些应用。

当然，一般我们不会直接使用clang进行编译，GNU/Linux上的传统编译管理器是make。

注：GNU/Linux是Linux的正式名称(但不是官方名称)

一般来说大型的C程序都需要先将源码文件编译为对象文件，再从对象文件生成Elf可执行文件(Linux上是这样做的)。

当编译时需要加入一些特殊的选项时，手动编译就不太合适了。

于是开发者会编写一个Makefile，你解开源码包并进入源码目录，运行make完成编译，然后`make install`，安装就完成了。

然而仅靠一个Makefile还是适应不了各平台的差别，于是有了Autoconf这类移植工具。

注：这里说的各平台只包括Unix系的操作系统，windows没那么好解决。

注：现代的gcc支持多种语言的编译。


[附录]TUR

https://github.com/Lexiie/termux-fakeroot.git

https://github.com/Bakaika/fakeroot-tcp.git

https://github.com/Bakaika/patch.git

https://github.com/funnymdzz/qemu-termux-repo.git

https://github.com/formatcom/termux-pacman.git

[Baidupcsgo]

主页：https://github.com/iikira/BaiduPCS-Go

百度网盘不限速下载器 
 
[you-get] 

强大的视频下载器，支持全球大多数视频网站，`pip install you-get`即可安装。
 
[caddy]

主页：https://github.com/mholt/caddy

Go编写的httpServer

[jupyter]

Web编程笔记本(然而我不会python……)

[mapscii]

基于cli的终端地图，Nodejs编写。npm install mapscii -s即可安装。

[hexo]

轻量的个人博客框架by nodejs

[webui-aria2]

主页：https://github.com/ziahamza/webui-aria2

快速，强大，易用的多线程下载器。

[zeronet]

去中心化的web网络

Install:

```shell
apt install clang python2 python2-dev libevent libcrypt-dev libcrypt
pip2 install msgpack gevent
cd $PREFIX/share
git clone https://github.com/HelloZeroNet/ZeroNet.git
mv ZeroNet zeronet
cd $PREFIX/bin
ln -s $PREFIX/share/zeronet/zeronet.py zeronet
termux-fix-shebang zeronet
```
安装完成后在termux中输入`zeronet`即可启动。

[sqlmap]

sql远程管理工具，好用！(认真)

[explainshell]

explainshell.com的本地版本。

[SearX]

拒绝追踪的自由搜索引擎。

[Metasploit-framework]

世界最强渗透测试引擎。

在Termux上安装：https://github.com/myfreess/MSFinstall

[Pupy]

跨Mac Windows Linux Android 的远程控制工具。

官方已添加termux支持。


>注:尽管Termux官方尽可能的为Termux营造linux的使用感受，但仍与linux有很大不同。此帮助手册包含大量linux发行版不支持的Termux特殊性质与配置。


[+]Termux原生图形界面

见x11源，xorg还有openbox啥的。

有文一篇https://yadominjinta.github.io/2018/07/30/GUI-on-termux.html

有项目一个:https://github.com/Hax4us/guitmux
 
[+]justforfun

```shell
curl wttr.in?lang=zh
#天气预报
echo "https://github.com/myfreess" | curl -F-=\<- qrenco.de
#终端下的二维码
```

[+]启动效果

一般打开Termux时会显示`$PREFIX/etc/motd`中的文字，可自行更改。

也有很多人在bashrc中使用figlet等工具制作启动时的艺术字效果。

[+]配色方案和字体

将字体文件复制到$HOME/.termux内，重命名为font.ttf，重启生效。

配色方案如法炮制，复制后重命名为colors.properties。

更好的建议：去google play购买style插件，操作更方便！

[+]More

Termux中长按屏幕，点按'More'出现更多选项。

[+]在Android中调用Termux编辑器

```shell
cd ~
ln -s /sdcard/documents downloads
mkdir ~/bin
cd ~/bin
ln -s $PREFIX/bin/nano termux-file-editor
```

我用nano，vim用户与Emacs用户可如法炮制。

完成后在Termux的home目录内生成downloads目录，编辑完成后文件将保存在这个目录。

[+]url钩子

建立文件`~/bin/termux-url-opener`，然后可以在Android中用Termux打开链接。

可以在此处链接you-get或lynx，自已写一个处理url的脚本也可以。

[+]文件传输

1.文件流向:Termux~>client

```shell
cd $dir
python2 -m SimpleHTTPServer 8000 #python2
python -m http.server 8000 #python3
```
python将监听8000端口，并开启一个简单的http服务器，根目录为$dir，这相当方便易用，风险也小(拒绝使用登录式ftp)

当然了，如果你要的只是快，这样的确很好。但这样不方便整个目录的复制，python的httpserver也不太稳定。如果你经常传输文件，可以考虑一下pure-ftpd

pure-ftpd的使用可见此处：https://i.linuxtoy.org/docs/guide/ch23s05.html，以下是一些ftpserver的注意事项。

1.不要为ftp用户开启可写权限

2.只使用匿名登录

如果需要修改、上传文件，那还是用sftp吧。

[+]与Android交互

这可能是Termux最强大的功能，需要以下支持:

 * [Termux:API]Termux扩展包。
 
 * [termux-api]用bashscript编写的，方便用户使用的工具集。
 
其实Android应用一直以来都支持命令行交互，你可以不用默认工具集，自己重新编写脚本来实现短信发送一类的功能。但这样做并不方便，最好还是在用户脚本内调用这些工具集完成所需功能。

目前已经有人实现了基于短信的交互式shell，异常强大！

注:用了修改版Termux就用不了这个扩展包了，因为Apk签名不统一。

[+]Web环境搭建

 * lighttpd

配置：https://i.linuxtoy.org/docs/guide/ch23s03.html

使用:在写好config文件后使用`lighttpd -f lighttpd.conf`来启动守护进程。

一个简单的lighttpd.conf:

```shell
server.port             = 8080
server.document-root    = "/sdcard/lighttpd/docs"
server.upload-dirs      = ( "/data/data/com.termux/files/usr/tmp" )
index-file.names        = ( "index.html" )
mimetype.assign         = (
                                ".html" => "text/html",
                                ".txt" => "text/plain",
                                ".css" => "text/css",
                                ".js" => "application/x-javascript",
                                ".jpg" => "image/jpeg",
                                ".jpeg" => "image/jpeg",
                                ".gif" => "image/gif",
                                ".png" => "image/png",
                                "" => "application/octet-stream"
                        )
```   	                     
但这只能用于建设静态网站。

 * php
 
 * Mariadb
 
安装/Install：
```shell
apt install mariadb -y
mkdir $PREFIX/etc/my.cnf.d
mysql_install_db
```
启动/start：
```shell
mysqld
mysql
#进入交互界面，exit退出
```

 * memcached



[+]学会不hacking

https://www.anquanke.com/opensource?page=1&c=1

https://github.com/ckjbug/kali-Linux-learning

https://github.com/Jack-Liang/kalitools

https://github.com/wizardforcel/kali-linux-cookbook-zh

让我~饶罗翔老师~来教你~截图~。自己看，自己学！

[附录]无名师与脚本狂

无名师和学生吃早饭时，从黑客大陆来了个陌生访客。

“Ihear y00 are very l33t,”他说。“Pl33z teach m3 all y00 know”。（我听说你很牛，请把你会的都教给我。）

无名师的学生面面相觑，都没听懂这类粗鄙言语。无名师微笑道：“你想弄懂Unix？”

“I want to b3 a wizard hax0r”，陌生人回答，“and 0wn ever3one's b0xen。”（我想当个顶尖黑客，能掌握所有人的机器。）

“我不教这个”，无名师答道。

陌生人很激动。“D00d， y00 r nothing but a p0ser。”，他说。“If y00 n00 anything, y00 wud t33ch m3。”（哥们儿，敢情你没真本事啊，你要知道点儿东西就教给我了。）

“有条路，”无名师说，“可以将你带入真知。”他在纸上写了个IP地址。“黑掉这台机器，这对你来说应该不费什么力气，它的管理员不称职。回来后告诉我你发现了什么。“

陌生人鞠了一躬就离开了。无名师把他的早饭吃完。

几天过去了，几个月过去了。没人再想起陌生人。

数年过去了，黑客大陆来的陌生人回来了。

”你混蛋！“他说，”我黑掉了那台机器，你说的没错，太容易了。但是我被FBI抓起来扔进监狱了。“

”好“，无名师说，”你可以继续下一课了。“他在另一张纸上写了个IP地址交给陌生人。

”你疯了？“陌生人喊道。”经过这事，我再也不黑别人的机器了。”

无名师脸现微笑。“这里就是”，他说，“真知的开始。”

听到此，陌生人眼中一亮。

# [附录]Neoterm

Termux分支，特点是兼容Google中文输入法，自带oh-my-zsh安装脚本，Adb与Fastboot。



写在最后：








 
 
 
 
 
 
 
 
 
 
 
 
 
