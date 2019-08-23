# Note

**xeffyr@github**为Termux的unstable仓库添加了Metasploit，现在，执行两行命令。

```shell
pkg i unstable-repo -y
pkg i metasploit -y
```

等待Metasploit安装完成,应该要用几个小时的时间。没自动完成就看下面。

**nokogiri**

Metasploit难搞的主原因是`nokogiri`，这是一个一半用ruby，一半用C编写的ruby模块，它有两个C依赖包，但是它处理依赖的方式独树一帜：

>在gem包里放两个shell脚本，用gem安装`nokogiri`时即时构建依赖包。嗯，是的，那两个脚本的shebang都是#!/bin/sh ……

和python的readline很像：/

解决方法:在错误输出中找到nokogiri的版本号，例如画家给我发的截图中，nokogiri版本为1.10.1，则他应该执行:

```shell
gem install nokogiri -v '1.10.1' -- --use-system-libraries
```

`--use-system-libraries`意为使用本地的so文件，而不是去运行shell脚本从SourceCode编译出so文件。

然后执行命令:

```shell
pkg i metasploit -y
```

等一等，应该会在一个小时内完成安装。

# Another Fault

一些别的错误:

+ `bigdecimal.so`无法加载，已被xeffyr解决(通过设置`LD_PRELOAD`)。

+ `metasploit-framework-5.0.13/lib/net/dns/resolver.rb`硬编码`/etc/resolv.conf`，已被xeffyr修复。

# Suggest

如果不需要exploit，仅仅想要管理自己的另一台机器(或者和朋友开个玩笑)，为什么不用pupy?它有对Termux的offical支持，不用操心适配问题。
