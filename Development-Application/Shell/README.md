# Shell

>（一）：功能、配置和插件

关于[shell](http://zh.wikipedia.org/wiki/Unix_shell)，一个广义的解释就是在用户与操作系统之间，提供一个工具或接口给用户来操作计算机系统；用户在shell中通过输入命令行，按下回车键，shell执行命令后就能返回结果，达到操作计算机的效果。  
但有很多人会问，为什么要学习shell呢？以下是我对为什么要学习shell的看法：

  * 在通过[ssh](http://zh.wikipedia.org/wiki/Secure_Shell)来远程操纵Linux/Unix服务器时，都是使用shell而不是用户界面
  * 相比于通过点击多个用户界面来执行操作，输入命令行更加直接和快捷
  * 利用管道组合各种可用工具，来创建和定制宏工具
  * 使用shell script将重复简单的任务自动化

而shell有很多种：Bourne Shell， C Shell，Korn Shell，Bourne-again Shell，TENEX C Shell等，通过命令`cat /etc/shells`可以查看系统支持哪些shell:


![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/01.png)

Linux/Unix默认都是使用Bash(Bourne-again Shell)，但我更倾向于使用[zsh](http://www.zsh.org/)，但由于配置过于复杂，前期很少人使用，但后来有外国程序员弄出一个[Oh My ZSH](http://ohmyz.sh/)来管理zsh的配置和支持更多插件，使得zsh变得更容易使用和更加强大。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/02.png)


# Shell有哪些功能

  * ### 命令历史记录

一旦你在shell敲入正确命令并能执行后，shell就会存储你所敲入命令的历史记录（存放在`~/.bash_history`文件），方便你再次运行之前的命令。  
你可以按方向键`↑`和`↓`来查看之前执行过的命令

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/03.gif)  

可以用`!!`来执行上一条命令，但最常用还是使用`ctrl-r`来搜索命令历史记录

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/04.gif) 

  * ### 命令和文件补全(按`tab`键)

当你输入命令或文件名时，你可以通过按`tab`键来补全命令或文件名，这样可以让你**更快**敲入命令和敲入**正确**的命令。  
有时你忘记具体某个命令，但你记住命令开头的几个字母是`gi`，可以敲入字母`gi`，按`tab`键来显示与前几个字母有关的所有命令：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/05.gif) 


当用`cd`命令前往某个目录时，你不必敲入整个路径的所有目录名，你只需敲入目录前几个字母，然后按`tab`键逐个补全目录名即可。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/06.gif) 


  * ### 命令别名

命令别名是一个比较有用的东西，特别适应用于**简化命令输入**。比如，你要更新cocoapods时，在shell输入以下命令行
    
    pod update --verbose --no-repo-update

但每次都输入这么长的命令行，多么麻烦啊。所以，这时使用命令别名来简化命令行的输入：
    
    alias pod_update='pod update --verbose --no-repo-update'

下次你只需要输入`pod_update`就可以更新cocoapod  
你可以使用`alias`命令来**显示所有命令别名**

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/07.png) 


  * ### 任务控制(job control)

使用shell登陆系统后，想要一边复制文件、一边查找文件、一边进行编译代码、一边下载软件，当然可以通过开启多个shell来完成，但如果想只在一个shell来完成以上多个任务时，此时可以使用shell的一个特性**任务控制**。

在学会如何使用命令来控制任务之前，先了解两个概念：**前台(foreground)**和**后台(background)**。**前台**就是出现提示符让用户操作的环境，而**后台**就是不能与用户交互的环境，你无法使用 `ctrl-c` 终止它，可使用 `bg/fg` 呼叫该任务。

下面介绍一些命令如何控制任务：

##### 1. 将任务放在后台运行：`command + &`

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/08.png)  


注意一下上面打印信息，`[1]`表示job number(任务编号)，`7089`表示PID(进程号)。在后台执行的命令，如果有stdout和stderr，数据依旧输出到屏幕上，可以通过数据重定向传输到文件中，就不会影响前台的工作。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/09.png) 

##### 2. 将任务丢到后台暂停：`ctrl-z`

在shell中执行`find / -print`命令，然后按下`ctrl-z`将任务丢到后台暂停：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/10.png) 


由上面打印可知，任务`find / -print`暂停执行，并将任务放在后台，返回一个job number`[2]`

##### 3. 查看后台所有任务状态：`jobs -l`

输入`jobs -l` 查看后台所有的任务状态：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/11.png)  


仔细查看打印信息，有没有留意到在PID `7417`和`7431`之前有`-`和`+`两个符号，`-`表示最近第二个被放到后台的任务号码，`+`表示最近被放到后台的任务号码。

##### 4. 将后台的任务拿到前台处理：`fg %jobnumber`

输入`fg`会默认取出`+`的任务，然后迅速按下`ctrl-z`

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/12.png)  

看上面打印的**PID**是`7431`，确实如此。再次输入`jobs -l`来查看后台所有任务的信息

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/13.png) 


这次输入`fg %1`来讲后台的任务拿到前台处理。

##### 5. 将后台的任务变成运行中：`bg %jobnumber`

输入`jobs -l`查看任务状态：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/14.png)  


然后输入`bg %2; jobs -l`将后台任务变成运行，并查看任务状态，然后不断地输入打印信息，这时需要关闭终端才能**kill**这个shell进程的子进程。

##### 6. 管理后台当中的任务：`kill -signal %jobnumber`

有时，任务在后台运行或暂停，这时我想结束这个任务，怎样办呢？你可以使用`kill`命令将任务结束。  
输入`find / -print`命令，并按下`ctrl-z`暂停任务：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/15.png)  


输入`kill -9 %1;jobs -l`结束任务并显示任务状态：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/16.png) 


  * ### shell script

shell script是利用shell的功能所编写的一个**程序**，这个程序使用纯文本文件来保存一些shell的命令，并遵循shell的语法规则，搭配数据重定向、管道、和正则表达式等功能来组合各种工具，实现简单重复任务的自动化。

  * ### 通配符

除了完整的字符串之外，shell还支持许多的通配符来帮助用户查询和命令执行。我简答地列出常用的几个通配符：

符号含义

*
表示0到无穷多个任意字符

?
表示有一个任意字符

[]
表示有一个在中括号内的字符。例如[abc]表示有个字符，可能是abc其中一个

[-]
表示在编码顺序内的所有字符。例如[1-7]表示有个字符，范围1到7其中一个

[^]
表示反向选择。例如表示有一个字符，只要不是a,b,c的其他字符都可以

# iTerm 2(for mac) && Oh My Zsh

如果你是mac的用户，推荐一个终端应用[iTerm 2](https://www.iterm2.com/), iTerm 2 相比mac自带的 Terminal 应用，有太多优点了。例如，支持画面分割，可以设置主题，各种使用的快捷键，以及快速唤出。配合 [Oh My Zsh](http://ohmyz.sh/) 使用，简直优雅到爆！

### Oh My Zsh安装

  * ##### curl方式
    
    curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh

  * ##### wget方式
    
    wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O - | sh

安装完之后，关闭当前终端，并重新打开一个，oh my zsh的默认主题是`robbyrussell`，效果如下：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/17.png)  

### 配置

如果你想定制和扩展zsh，oh my zsh提供配置文件`~/.zshrc`来配置，可以设置环境变量和别名；
    
    # Support autojump
    [[ -s ~/.autojump/etc/profile.d/autojump.sh ]] && . ~/.autojump/etc/profile.d/autojump.sh
    
    # setup moco alias name
    alias moco_service="moco start -p 12306 -g settings.json"
    
    #setup macvim alias name
    alias vim="/Applications/MacVim.app/Contents/MacOS/Vim"
    
    #setup pod update alias name
    alias pod_update='pod update --verbose --no-repo-update'

在[Themes](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)列出所有可用主题，每个主题都有截屏效果并教你如何设置，选择你喜欢的主题，在配置文件`~/.zshrc`查找字符串`ZSH_THEME="robbyrussell"`，通过改变`ZSH_THEME`环境变量来改变主题。例如，
    
    ZSH_THEME="agnoster"

**oh my zsh**提供数十种主题，相关文件在`~/.oh-my-zsh/themes` 目录，可以编辑主题来满足自身需求，我是使用默认的`robbyrussell`，不过做了一点小小改动：
    
    PROMPT='%{$fg_bold[red]%}➜ %{$fg_bold[green]%}%p%{$fg[cyan]%}%d %{$fg_bold[blue]%}$(git_prompt_info)%{$fg_bold[blue]%}% %{$reset_color%}> '
    #PROMPT='${ret_status}%{$fg_bold[green]%}%p %{$fg[cyan]%}%c %{$fg_bold[blue]%}$(git_prompt_info)%{$fg_bold[blue]%} % %{$reset_color%}> '

与原来不同的是，将c(表示当前目录)改为d(表示绝对路径)，另外在尾部添加一个`>`作为隔离符号，效果如下：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/18.png) 

### 插件

**oh my zsh**提供丰富的插件，存放在`~/.oh-my-zsh/plugins`目录下：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/19.png)  

想了解每个插件的功能以及如何使用，只要打开相关插件的目录下zsh文件即可，以git插件为例：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/20.png) 

打开`git.plugin.zsh`文件，里面有很多命名别来来简化命令的输入。你可以根据自己的需要来启用哪些插件，只需在`~/.zshrc`配置文件追加内容即可：
    
    plugins=(git autojump osx)

我来介绍一下一些[常用插件](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins)的使用吧：

##### git

当你处在一个git受控的目录下时，Shell明确显示`git`和`branch`信息，另外简化git很多命令，具体使用请参考：[Plugin:git](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugin:git)

##### autojump

autojump插件使你能够快速切换路径，再也不需要逐个敲入目录，只需敲入目标目录，就可以迅速切换目录。

  * 安装  
如果你是mac用户，可以使用`brew`安装：
    
    brew install autojump

如果是linux用户，首先下载**autojump**最近版本，比如：
    
    git clone git://github.com/joelthelion/autojump.git

然后进入目录，执行
    
    ./install.py

最近将以下代码加入`~/.zshrc`配置文件：
    
    [[ -s ~/.autojump/etc/profile.d/autojump.sh ]] && . ~/.autojump/etc/profile.d/autojump.sh

  * 使用  
如果你之前打开过`~/.oh-my-zsh/themes`目录，现在只需敲入`j themes`就可以快速切换到`~/.oh-my-zsh/themes`目录。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/21.png)  

##### osx

  * `tab` - 在一个新标签打开当前目录
  * `cdf` - cd到当前Finder目录
  * `quick-look` - 快速浏览特殊的文件
  * `man-preview` - 在Preview应用打开特定的man page
  * `trash` - 将特定的文件移到垃圾桶

### 使用

  1. 因为zsh兼容bash，所以之前使用bash的人切换到zsh毫无压力
  2. 智能拼写纠正，比如你输入`cls`，会提示

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/22.png) 


  3. 各种补全：除了支持命令补全和文件补全之外，还支持命令参数补全，插件内容补全，只需要按`tab`键
  4. 使用`autojump`智能跳转
  5. 目录浏览和跳转：输入d，就显示在会话里访问的目录列表，输入列表前的序号，即可以跳转

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/23.png)  


  6. 输入`..`可以返回到上级目录

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/24.png) 


YouTube有个演示视频 [zsh shell](https://www.youtube.com/watch?v=HGBgMX5HW_g)详细介绍如果使用Oh My Zsh

# 总结

作为的一个程序员，我觉得shell是一个必不可少的工具，使用它能够毫不费劲地操作计算机。在shell提示下，通过调用各种各样的工具，并结合管道，将这些工具根据自己需要组合起来，创建和制定宏工具，甚至编写shell script来将简单而重复的工作自动化，做到**Don't repeat your self**。

> （二）：变量、数据重定向和管道

重点介绍，shell中的**变量**的如何设置和读取数据，读取之后如何使用变量？每个程序一般都有输入和输出，让我们看看**数据重定向**如何处理输入和输出的？还有，Unix/Linux系统提供丰富的工具，我们如何将这些工具通过**管道**来组合成更加强大的宏工具呢？下面，由我来逐一详细介绍变量、数据重定向和管道。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/25.png) 

# 变量

### 变量的作用

变量与其他程序设计语言一样，都是**存储数据**，然后被程序引用。相比于不使用变量，而是直接使用数据，存在两个问题：

  1. 当数据改变时，直接使用数据的时候却不能灵活地根据数据改变而随着改变，而使用变量却不同，它能够做到这点。
  2. 当数据发生变化时，如果想保证数据**一致性**，必须查找所有引用该数据的所有地方，然后将它修改，当下一次再需要修改时，也是像这种情况一样，是多么繁琐的事，而变量却不用，只需要修改变量值即可。

因此，变量具有**可变性**和**易于修改**的两个特点。

### 变量的分类

在shell中，大概分为两种变量：**环境变量**和**局部变量**，主要区别在于它们的使用范围不同，环境变量可以在父进程与子进程之间共享，而自定义变量只在本进程使用。举一个简单的例子来说明：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/26.png) 


我首先设置一个shell变量`devname=sam`，然后输入`bash`打开一个新的shell，而这个shell是**子进程**，然后`echo $devname`输出变量值，变量值为空，最后`exit`退出子进程。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/27.png) 

但使用`export devname`设置环境变量后，再次进入输入`bash`进入子进程之后，`echo $devname`输出变量值，这次变量值是`sam`

##### 查看环境变量`env`和`set`

如果想查看**系统**中以及**自定义**有哪些环境变量，可以使用`env`命令：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/28.png) 


而`set`命令不仅能查看环境变量，还可以查看与shell接口有关的变量，下面只截取一部分变量：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/29.png) 


### 变量有哪些操作

##### 显示`echo $variable`

如果你想显示某个变量的值，例如`PATH`，你只需要输入：
    
    echo $PATH

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/30.png) 


注意上面一条命令，需要在变量名前加上一个符号`$`，这样才能访问变量

##### 设置`variable=value`和取消`unset`

如果你想设置某个变量的值，只需在变量名和变量值之间用符号`=`连接就行了，例如：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/31.png) 


由上面的输入命令`echo $devname`，显示结果为**空**。由此可知，一开始如果没有设置某个变量时，它的是为**空**。另外，**设置变量的规则**还需要几点注意：

  1. 在命名变量名时，变量名称只能是英文字母和数字，而且首字母不能是数字。下面演示一个错误的例子：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/32.png)  


  2. 等号`=`两边不能有**空格**

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/33.png) 


blank can't exist.png

  3. 如果变量值有空格，可用双引号`" "`或单引号`' '`来包围变量值，但两者是有区别：  
双引号`" "`内的一些特殊字符，可以保持原有的特性，例如：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/34.png) 


而单引号`' '`内的一些特殊字符，仅为一般字符，即纯文本，例如：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/35.png) 


  4. 如果想显示一些特殊字符（$、空格、!等），在字符前面加上用转义字符`\`

  5. 有些时候，变量的值可能**来源于一些命令**，这时你可以使用反单引号```命令```或`$(命令)`，例如：  
使用反单引号```命令```的方式

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/36.png) 


使用`$(命令)`的方式

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/37.png)   


  6. 如果变量想**增加变量的值**，可以使用`$variable`累加

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/38.png) 


  7. 如果变量需要在其他子进程使用，用`export`关键字来设置变量为环境变量
    
    export VARIABLE

  8. 系统环境变量一般都是**字母全部大写**，例如：`PATH`，`HOME`，`SHELL`等

  9. 如果想取消设置变量的值，使用`unset variable`命令。注意，变量之前是没有符号`$`

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/39.png) 

### 环境配置文件

之前那些设置的环境变量，一旦退出系统后，就**不能再次使用**，如果想再次使用，必须重新再设置才行。如果想就算退出系统，也能重新使用自定义的环境变量，那怎么办呢？

不用怕，系统提供一些环境配置文件：`/etc/profile`和`~/.bash_profile`。`/etc/profile`是系统整体的设置，每个用户共享，最好不要修改；而`~/.bash_profile`属于单个用户的设置，每个用户设置后，互不影响和共享。但因为我使用[oh my zsh](http://ohmyz.sh/)，之前`~/.bash_profile`设置一些配置都不生效了，但它提供一个环境配置文件`.zshrc`，所以如果想设置环境变量TEST，只需将`export TEST=test`添加`.zshrc`即可。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/40.png) 


但在`.zshrc`文件设置好环境变量`TEST`后，`echo $TEST`为空，原因是还没使用`source`命令来读取环境配置文件。使用`source .zshrc`命令之后，设置环境变量`TEST`生效了

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/41.png) 


# 数据重定向

### 含义

当输入命令行时，一般都有输入参数(standard input)，而命令行处理完之后，一般都有输出结果，结果有可能成功(standard output)，也有可能失败(standard error)，而这些结果一般都会输出到屏幕上，如果你想控制结果输出到文件或以文件作为输入的话，你需要了解数据重定向的分类和符号操作。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/42.png)  


### 分类

数据重定向主要分为三类：

  * `stdin`，表示标准输入，代码为0，使用`<`或`<<`操作符  
符号`<`表示以文件内容作为输入  
符号`<<`表示输入时的结束符号
  * `stdout`，表示标准输出，代码为1，使用`>`或`>>`操作符  
符号`>`表示以**覆盖**的方式将**正确**的数据输出到指定文件中  
符号`>>`表示以**追加**的方式将**正确**的数据输出到指定文件中
  * `stderr`，表示标准错误输出，代码为2，使用`2>`或`2>>`操作符  
符号`2>`表示以**覆盖**的方式将**错误**的数据输出到指定文件中  
符号`2>>`表示以**追加**的方式将**错误**的数据输出到指定文件中

### 使用

##### stdout

当你输入`ls`命令，屏幕会显示当前目录有哪些文件和目录；而当你使用符号`>`时，输出结果将重定向到`dir.txt`文件，而不显示在屏幕上

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/43.png)  


而符号`>`与符号`>>`有什么**区别**呢？`>`表示当文件存在时，将文件内容清空，然后stdout结果存放到文件中。而`>>`表示当文件存在时，文件内容并没有清空，而是将stdout结果追加到文件尾部。

当你再次输入命令`ls > dir.txt`时，文件内容并没有改变，因为之前文件内容被清空，然后stdout结果存放在`dir.txt`文件

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/44.png) 


而你这次使用符号`ls >> dir.txt`的话，文件内容被追加到`dir.txt`文件

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/45.png)  

##### stderr

这次我输入命令`ls test`显示一个不存在的文件，会显示错误信息。然后将错误信息输出到文件`error.txt`。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/46.png)   

如果你想追加错误信息，可以使用`2>>`符号

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/47.png) 

##### stdout & stderr

  * 将stdout和stderr分离：**`>`和`2>`符号**  
输入`ls README.md test`，在屏幕显示既有正确信息，也有错误信息，如果想将正确信息和错误信息分离到不同文件，你可以同时使用`>`和`2>`符号

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/48.png) 


  * 将stdout和stderr合并：**`&>`符号**  
如果你想将正确信息和错误信息**合并**，且输出到同一个文件，可以使用`&>`符号

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/49.png)  


##### stdin

一般输入一些简单的数据的方式都是通过**键盘**，但是如果要输入大量的数据，最好还是通过**文件**的方式。举一个简单例子：  
首先输入`cat > test`命令之后，你就可以输入内容，那些内容最终会存放在`test`文件

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/50.png) 

但如果有大量数据从一个文件导入到`test`文件时，此时需要用到`<`符号

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/51.png) 

还一个符号`<<`需要解释，符号`<<`表示输入时的结束符号。输入`cat > test << "eof"`命令之后，你就可以输入内容，那些内容最终会存放在`test`文件，输入完内容后可以输入`eof`来结束输入

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/52.png) 


# 管道

在Unix设计哲学中，有一个重要设计原则--[KISS](http://en.wikipedia.org/wiki/KISS_principle)(Keep it Simple, Stupid)，大概意思就是**只关注如何做好一件事，并把它做到极致**。每个程序都有各自的功能，那么有没有一样东西将不同功能的程序互相连通，自由组合成更为强大的宏工具呢？此时，**管道**出现了，它能够让程序实现了**高内聚，低耦合**。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/53.png) 


如果我想查看文件是否存在某个关键字，此时我可以使用管道

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/Shell/54.png) 


命令`cat README.md | grep 'pod'`的处理过程分为两步：

  1. `cat README.md`查看文件内容
  2. 然后将`cat README.md`输出的内容作为`grep 'pod'`命令的输入，再进行处理。

上面一个很关键的符号`|`，就是管道，它能够将前一个命令处理完的`stdout`作为下一条命令`stdin`。

# 扩展阅读

  * [鸟哥的Linux私房菜-基础学习篇](http://book.douban.com/subject/4889838/)
  * [Unix Pipes 管道原稿](http://coolshell.cn/articles/1351.html)
  * Linux Shell  
[工作管理 (job control)](http://vbird.dic.ksu.edu.tw/linux_basic/0440processcontrol.php#background)
  * oh my shell  
[终极 Shell](http://macshuo.com/?p=676)
