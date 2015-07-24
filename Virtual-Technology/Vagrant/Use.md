# Vgrant使用入门

前面我们已经学会了如何安装并配置Vagrant，而且也已经按照默认的方式开启了，那么这一小节就给大家介绍一下Vagrant的高级应用。

## Vagrant常用命令

前面讲了Vagrant的几个命令：

  * `vagrant box add` 添加box的操作
  * `vagrant init` 初始化box的操作
  * `vagrant up` 启动虚拟机的操作
  * `vagrant ssh` 登录拟机的操作

Vagrant还包括如下一些操作：

  * `vagrant box list`

显示当前已经添加的box列表

      $ vagrant box list
      base (virtualbox)


  * `vagrant box remove`

删除相应的box

      $ vagrant box remove base virtualbox
      Removing box 'base' with provider 'virtualbox'...


  * `vagrant destroy`

停止当前正在运行的虚拟机并销毁所有创建的资源

      $ vagrant destroy
      Are you sure you want to destroy the 'default' VM? [y/N] y
      [default] Destroying VM and associated drives...


  * `vagrant halt`

关机

      $ vagrant halt
      [default] Attempting graceful shutdown of VM...


  * `vagrant package`

打包命令，可以把当前的运行的虚拟机环境进行打包

      $ vagrant package
      [default] Attempting graceful shutdown of VM...
      [default] Clearing any previously set forwarded ports...
      [default] Creating temporary directory for export...
      [default] Exporting VM...
      [default] Compressing package to: /Users/astaxie/vagrant/package.box


  * `vagrant plugin`

用于安装卸载插件

  * `vagrant provision`

通常情况下Box只做最基本的设置，而不是设置好所有的环境，因此Vagrant通常使用Chef或者Puppet来做进一步的环境搭建。那么Chef或者Puppet称为provisioning，而该命令就是指定开启相应的provisioning。按照Vagrant作者的说法，所谓的provisioning就是"The problem of installing software on a booted system"的意思。除了Chef和Puppet这些主流的配置管理工具之外，我们还可以使用Shell来编写安装脚本。

例如： `vagrant provision --provision-with chef`

  * `vagrant reload`

重新启动虚拟机，主要用于重新载入配置文件

      $ vagrant reload
      [default] Attempting graceful shutdown of VM...
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
      [default] Setting hostname...
      [default] Mounting shared folders...
      [default] -- /vagrant


  * `vagrant resume`

恢复前面被挂起的状态

      $vagrant resume
      [default] Resuming suspended VM...
      [default] Booting VM...
      [default] Waiting for VM to boot. This can take a few minutes.
      [default] VM booted and ready for use!


  * `vagrant ssh-config`

输出用于ssh连接的一些信息

      $vagrant ssh-config
      Host default
      HostName 127.0.0.1
      User vagrant
      Port 2222
      UserKnownHostsFile /dev/null
      StrictHostKeyChecking no
      PasswordAuthentication no
      IdentityFile "/Users/username/.vagrant.d/insecure_private_key"
      IdentitiesOnly yes
      LogLevel FATAL


  * `vagrant status`

获取当前虚拟机的状态

      $vagrant status
      Current machine states:

      default                   running (virtualbox)

      The VM is running. To stop this VM, you can run `vagrant halt` to
      shut it down forcefully, or you can run `vagrant suspend` to simply
      suspend the virtual machine. In either case, to restart it again,
      simply run `vagrant up`.


  * `vagrant suspend`

挂起当前的虚拟机

      $ vagrant suspend
      [default] Saving VM state and suspending execution...


## 模拟打造多机器的分布式系统

前面这些单主机单虚拟机主要是用来自己做开发机，从这部分开始的内容主要将向大家介绍如何在单机上通过虚拟机来打造分布式造集群系统。这种多机器模式特别适合以下几种人：

  1. 快速建立产品网络的多机器环境，例如web服务器、db服务器
  2. 建立一个分布式系统，学习他们是如何交互的
  3. 测试API和其他组件的通信
  4. 容灾模拟，网络断网、机器死机、连接超时等情况

Vagrant支持单机模拟多台机器，而且支持一个配置文件Vagrntfile就可以跑分布式系统。

现在我们来建立多台VM跑起來，並且让他们之间能够相通信，假设一台是应用服务器、一台是DB服务器，那么这个结构在Vagrant中非常简单，其实和单台的配置差不多，你只需要通过`config.vm.define`来定义不同的角色就可以了，现在我们打开配置文件进行如下设置：

    Vagrant.configure("2") do |config|
      config.vm.define :web do |web|
        web.vm.provider "virtualbox" do |v|
              v.customize ["modifyvm", :id, "--name", "web", "--memory", "512"]
        end
        web.vm.box = "base"
        web.vm.hostname = "web"
        web.vm.network :private_network, ip: "11.11.1.1"
      end

      config.vm.define :db do |db|
        db.vm.provider "virtualbox" do |v|
              v.customize ["modifyvm", :id, "--name", "db", "--memory", "512"]
        end
        db.vm.box = "base"
        db.vm.hostname = "db"
        db.vm.network :private_network, ip: "11.11.1.2"
      end
    end


这里的设置和前面我们单机设置配置类似，只是我们使用了`:web`以及`:db`分別做了两个VM的设置，并且给每个VM设置了不同的`hostname`和IP，设置好之后再使用`vagrant up`将虚拟机跑起来：

    $ vagrant up
    Bringing machine 'web' up with 'virtualbox' provider...
    Bringing machine 'db' up with 'virtualbox' provider...
    [web] Setting the name of the VM...
    [web] Clearing any previously set forwarded ports...
    [web] Creating shared folders metadata...
    [web] Clearing any previously set network interfaces...
    [web] Preparing network interfaces based on configuration...
    [web] Forwarding ports...
    [web] -- 22 => 2222 (adapter 1)
    [web] Running any VM customizations...
    [web] Booting VM...
    [web] Waiting for VM to boot. This can take a few minutes.
    [web] VM booted and ready for use!
    [web] Setting hostname...
    [web] Configuring and enabling network interfaces...
    [web] Mounting shared folders...
    [web] -- /vagrant
    [db] Setting the name of the VM...
    [db] Clearing any previously set forwarded ports...
    [db] Fixed port collision for 22 => 2222. Now on port 2200.
    [db] Creating shared folders metadata...
    [db] Clearing any previously set network interfaces...
    [db] Preparing network interfaces based on configuration...
    [db] Forwarding ports...
    [db] -- 22 => 2200 (adapter 1)
    [db] Running any VM customizations...
    [db] Booting VM...
    [db] Waiting for VM to boot. This can take a few minutes.
    [db] VM booted and ready for use!
    [db] Setting hostname...
    [db] Configuring and enabling network interfaces...
    [db] Mounting shared folders...
    [db] -- /vagrant


看到上面的信息输出后，我们就可以通过`vagrant ssh`登录虚拟机了，但是这次和上次使用的不一样了，这次我们需要指定相应的角色，用来告诉ssh你期望连接的是哪一台：

    $ vagrant ssh web
    vagrant@web:~$

    $ vagrant ssh db
    vagrant@db:~$


是不是很酷！现在接下来我们再来验证一下虚拟机之间的通信，让我们先使用ssh登录web虚拟机，然后在web虚拟机上使用ssh登录web虚拟机(默认密码是`vagrant`)：

    $ vagrant ssh web
    Linux web 2.6.32-38-server #83-Ubuntu SMP Wed Jan 4 11:26:59 UTC 2012 x86_64 GNU/Linux
    Ubuntu 10.04.4 LTS

    Welcome to the Ubuntu Server!
     * Documentation:  http://www.ubuntu.com/server/doc
    New release 'precise' available.
    Run 'do-release-upgrade' to upgrade to it.

    Welcome to your Vagrant-built virtual machine.
    Last login: Thu Aug  8 18:55:44 2013 from 10.0.2.2
    vagrant@web:~$ ssh 11.11.1.2
    The authenticity of host '11.11.1.2 (11.11.1.2)' can't be established.
    RSA key fingerprint is e7:8f:07:57:69:08:6e:fa:82:bc:1c:f6:53:3f:12:9e.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added '11.11.1.2' (RSA) to the list of known hosts.
    vagrant@11.11.1.2's password:
    Linux db 2.6.32-38-server #83-Ubuntu SMP Wed Jan 4 11:26:59 UTC 2012 x86_64 GNU/Linux
    Ubuntu 10.04.4 LTS

    Welcome to the Ubuntu Server!
     * Documentation:  http://www.ubuntu.com/server/doc
    New release 'precise' available.
    Run 'do-release-upgrade' to upgrade to it.

    Welcome to your Vagrant-built virtual machine.
    Last login: Thu Aug  8 18:58:50 2013 from 10.0.2.2
    vagrant@db:~$


通过上面的信息我们可以看到虚拟机之间通信是畅通的，所以现在开始你伟大的架构设计吧，你想设计怎么样的架构都可以，唯一限制你的就是你主机的硬件配置了。
