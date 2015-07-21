# Vgrant安装配置

实际上Vagrant只是一个让你可以方便设置你想要的虚拟机的便携式工具，它底层支持VirtualBox、VMware甚至AWS作为虚拟机系统，本书中我们将使用VirtualBox来进行说明，所以第一步需要先安裝Vagrant和VirtualBox。

## VirtualBox安装

VirtualBox是Oracle开源的虚拟化系统，它支持多个平台，所以你可以到官方网站：[https://www.virtualbox.org/wiki/Downloads/](https://www.virtualbox.org/wiki/Downloads/) 下载适合你平台的VirtualBox最新版本并安装，它的安装过程都很傻瓜化，一步一步执行就可以完成安装了。

## Vagrant安装

最新版本的Vagrant已经无法通过`gem`命令来安装，因为依赖库太多了，所以目前无法使用`gem`来安装，目前网络上面很多教程还是类似这样的命令，那些都是错误的。目前唯一安装的办法就是到官方网站下载打包好的安装包：[http://www.vagrantup.com/downloads.html](http://www.vagrantup.com/downloads.html) 他的安装过程和VirtualBox的安装一样都是傻瓜化安装，一步一步执行就可以完成安装。

> 尽量下载最新的程序，因为VirtualBox经常升级，升级后有些接口会变化，老的Vagrant可能无法使用。

要想检测安装是否成功，可以打开终端命令行工具，输入`vagrant`，看看程序是不是已经可以运行了。如果不行，请检查一下$PATH里面是否包含`vagrant`所在的路径。

## Vagrant配置

当我们安装好VirtualBox和Vagrant后，我们要开始考虑在VM上使用什么操作系统了，一个打包好的操作系统在Vagrant中称为Box，即Box是一个打包好的操作系统环境，目前网络上什么都有，所以你不用自己去制作操作系统或者制作Box：[vagrantcloud](https://vagrantcloud.com/)上面有大家熟知的大多数操作系统，你只需要下载就可以了，下载主要是为了安装的时候快速，当然Vagrant也支持在线安装。

### 建立开发环境目录

我的开发机是Mac，所以我建立了如下的开发环境目录，读者可以根据自己的系统不同建立一个目录就可以：
    
    D:\DevelopFolder
    

### 下载box

前面讲了box是一个操作系统环境，实际上它是一个zip包，包含了Vagrant的配置信息和VirtualBox的虚拟机镜像文件.我们这一次的实战使用官方提供了一个box:Ubuntu lucid 64 [http://files.vagrantup.com/lucid64.box](http://files.vagrantup.com/lucid64.box)

当然你也可以选一个自己团队在用的系统，例如CentOS、Debian等，我们可以通过上面说的地址下载开源爱好者们制作好的box。当然你自己做一个也行，下一节我会讲述如何自己制作包。

### 添加box

添加box的命令如下：
    
    vagrant box add base 远端的box地址或者本地的box路径
    

`vagrant box add` 是添加box的命令

`base`是box的名称，可以是任意的字符串，`base`是默认名称，主要用来标识一下你添加的box，后面的命令都是基于这个标识来操作的。

例子：
    
    vagrant box add base http://files.vagrantup.com/lucid64.box
    vagrant box add base https://dl.dropbox.com/u/7225008/Vagrant/CentOS-6.3-x86_64-minimal.box
    vagrant box add base CentOS-6.3-x86_64-minimal.box
    vagrant box add "CentOS 6.3 x86_64 minimal" CentOS-6.3-x86_64-minimal.box
    

我在开发机上面是这样操作的，首先进入我们的开发环境目录`D:\DevelopFolder`，执行如下的命令
    
    vagrant box add base lucid64.box
    

安装过程的信息：
    
    Downloading or copying the box...
    Extracting box...te: 47.5M/s, Estimated time remaining: --:--:--)
    Successfully added box 'base' with provider 'virtualbox'!
    

box中的镜像文件被放到了：`/Users/当前用户名/.vagrant.d/boxes/`，如果在window系统中应该是放到了： `C:\Users\当前用户名\.vagrant.d\boxes\`目录下。

通过`vagrant box add`这样的方式安装远程的box，可能很慢，所以建议大家先下载box到本地再执行这样的操作。

### 初始化

初始化的命令如下：
    
    vagrant init
    

如果你添加的box名称不是base，那么需要在初始化的时候指定名称，例如
    
    vagrant init "CentOS 6.3 x86_64 minimal"
    

初始化过程的信息：
    
    A `Vagrantfile` has been placed in this directory.
    You are now ready to `vagrant up` your first virtual environment!
    Please read the comments in the Vagrantfile as well as documentation on `vagrantup.com` for more information on using Vagrant.
    

这样就会在当前目录生成一个 `Vagrantfile`的文件，里面有很多配置信息，后面我们会详细讲解每一项的含义，但是默认的配置就可以开箱即用。

### 启动虚拟机

启动虚拟机的命令如下：
    
    vagrant up
    

启动过程的信息:
    
    Bringing machine 'default' up with 'virtualbox' provider...
    [default] Importing base box 'base'...
    [default] Matching MAC address for NAT networking...
    [default] Setting the name of the VM...
    [default] Clearing any previously set forwarded ports...
    [default] Creating shared folders metadata...
    [default] Clearing any previously set network interfaces...
    [default] Preparing network interfaces based on configuration...
    [default] Forwarding ports...
    [default] -- 22 => 2222 (adapter 1)
    [default] Booting VM...
    [default] Waiting for VM to boot. This can take a few minutes.
    [default] VM booted and ready for use!
    [default] Mounting shared folders...
    [default] -- /vagrant
    

### 连接到虚拟机

上面已经启动了虚拟机，之后我们就可以通过ssh来连接到虚拟机了。比如在我的开发机中可以像这样来连接：
    
    vagrant ssh
    

连接到虚拟机后的信息如下：
    
    Linux lucid64 2.6.32-38-server #83-Ubuntu SMP Wed Jan 4 11:26:59 UTC 2012 x86_64 GNU/Linux
    Ubuntu 10.04.4 LTS
    
    Welcome to the Ubuntu Server!
     * Documentation:  http://www.ubuntu.com/server/doc
    New release 'precise' available.
    Run 'do-release-upgrade' to upgrade to it.
    
    Welcome to your Vagrant-built virtual machine.
    Last login: Fri Sep 14 07:31:39 2012 from 10.0.2.2
    

这样我们就可以像连接到一台服务器一样进行操作了。

> window机器不支持这样的命令，必须使用第三方客户端来进行连接，例如putty、Xshell4等.
> 
> putty为例：
> 
> 主机地址: 127.0.0.1
> 
> 端口: 2222
> 
> 用户名: vagrant
> 
> 密码: vagrant

### 系统信息

进入系统之后我们可以看一下系统的基础信息：
    
    vagrant@lucid64:/vagrant$ df -h
    Filesystem            Size  Used Avail Use% Mounted on
    /dev/mapper/lucid64-root
                           78G  945M   73G   2% /
    none                  179M  176K  179M   1% /dev
    none                  184M     0  184M   0% /dev/shm
    none                  184M   64K  184M   1% /var/run
    none                  184M     0  184M   0% /var/lock
    none                  184M     0  184M   0% /lib/init/rw
    none                   78G  945M   73G   2% /var/lib/ureadahead/debugfs
    /dev/sda1             228M   17M  199M   8% /boot
    /vagrant              298G   76G  222G  26% /vagrant
    

`/vagrant`这个目录是自动映射的，被映射到`D:\DevelopFolder`，这样就方便我们以后在开发机中进行开发，在虚拟机中进行运行效果测试了。

### Vagrantfile配置文件详解

在我们的开发目录下有一个文件`Vagrantfile`，里面包含有大量的配置信息，主要包括三个方面的配置，虚拟机的配置、SSH配置、Vagrant的一些基础配置。Vagrant是使用Ruby开发的，所以它的配置语法也是Ruby的，但是我们没有学过Ruby的人还是可以跟着它的注释知道怎么配置一些基本项的配置。

  1. box设置
    
     config.vm.box = "base"
    

上面这配置展示了Vagrant要去启用那个box作为系统，也就是上面我们输入`vagrant init Box名称`时所指定的box，如果沒有输入box名称的話，那么默认就是`base`，VirtualBox提供了VBoxManage这个命令行工具，可以让我们设定VM，用`modifyvm`这个命令让我们可以设定VM的名称和内存大小等等，这里说的名称指的是在VirtualBox中显示的名称，我们也可以在Vagrantfile中进行设定，在Vagrantfile中加入如下这行就可以设定了：
    
     config.vm.provider "virtualbox" do |v|
       v.customize ["modifyvm", :id, "--name", "astaxie", "--memory", "512"]
     end
    

这行设置的意思是调用VBoxManage的`modifyvm`的命令，设置VM的名称为`astaxie`，内存为512MB。你可以类似的通过定制其它VM属性来定制你自己的VM。

  2. 网络设置

Vagrant有两种方式来进行网络连接，一种是host-only(主机模式)，意思是主机和虚拟机之间的网络互访，而不是虚拟机访问internet的技术，也就是只有你一個人自High，其他人访问不到你的虚拟机。另一种是Bridge(桥接模式)，该模式下的VM就像是局域网中的一台独立的主机，也就是说需要VM到你的路由器要IP，这样的话局域网里面其他机器就可以访问它了，一般我们设置虚拟机都是自high为主，所以我们的设置一般如下：
    
     config.vm.network :private_network, ip: "11.11.11.11"
    

这里我们虚拟机设置为hostonly，并且指定了一个IP，IP的话建议最好不要用`192.168..`这个网段，因为很有可能和你局域网里面的其它机器IP冲突，所以最好使用类似`11.11..`这样的IP地址。

  3. hostname设置

`hostname`的设置非常简单，Vagrantfile中加入下面这行就可以了：
    
     config.vm.hostname = "go-app"
    

设置`hostname`非常重要，因为当我们有很多台虚拟服务器的时候，都是依靠`hostname`來做识别的，例如Puppet或是Chef，都是通过`hostname`來做识别的，既然设置那么简单，所以我们就別偷懒，设置一个。

  4. 同步目录

我们上面介绍过`/vagrant`目录默认就是当前的开发目录，这是在虚拟机开启的时候默认挂载同步的。我们还可以通过配置来设置额外的同步目录：
    
     config.vm.synced_folder  "/Users/astaxie/data", "/vagrant_data"
    

上面这个设定，第一个参数是主机的目录，第二个参数是虚拟机挂载的目录

  5. 端口转发
    
     config.vm.network :forwarded_port, guest: 80, host: 8080
    

上面这句配置可厉害了，这一行的意思是把对host机器上8080端口的访问请求forward到虚拟机的80端口的服务上，例如你在你的虚拟机上使用nginx跑了一个Go应用，那么你在host机器上的浏览器中打开`http://localhost:8080`时，Vagrant就会把这个请求转发到VM里面跑在80端口的nginx服务上，因此我们可以通过这个设置来帮助我们去设定host和VM之间，或是VM和VM之间的信息交互。

> > > 修改完Vagrantfile的配置后，记得要用`vagrant reload`命令来重启VM之后才能使用VM更新后的配置
