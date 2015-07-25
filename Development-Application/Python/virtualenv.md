# Virtualenv

## 创建 python 虚拟环境及简单使用

进行不同的 python 项目开发，有的时候会遇到这样的情况：python 版本不一样，使用的软件包版本不一样。这种问题最佳的解决办法是使用 virtualenv 为不同的项目搭建独立的 python 环境。

## virtualenv

### 安装
    
    sudo pip install virtualenv
    

### 创建
    
    mkdir myproject
    cd myproject
    virtualenv myproject_ENV
    

  1. 创建项目文件夹 `myproject`

  2. 进入项目目录

  3. 创建虚拟环境 `myproject_ENV`

这时候会发现在 `myproject` 目录下新增了一个 `myproject_ENV` 的文件夹。

### 使用
    
    cd myproject_ENV
    source ./bin/activate
    

  1. 进入虚拟环境目录 `myproject_ENV`

  2. 激活

这时候在命令行的最左边会显示该虚拟环境的名称。不妨使用下面的命令查看一下变化：
    
    which python
    which pip
    pip list
    

如果想要退出虚拟环境，使用这个命令就可以了：
    
    deactivate
    

## 扩展包 Virtualenvwrapper

Virtualenvwrapper 的作用是：更方便的创建/激活/管理/销毁虚拟环境。

### 安装及配置
    
    sudo pip install virtualenvwrapper
    

默认安装完成后并不能使用 Virtualenvwrapper 的命令，需要进行配置，在 `~/.bashrc` 文件中添加：
    
    if [ `id -u` != '0' ]; then
    
      export VIRTUALENV_USE_DISTRIBUTE=1        # <-- Always use pip/distribute
      export WORKON_HOME=$HOME/.virtualenvs       # <-- Where all virtualenvs will be stored
      source /usr/local/bin/virtualenvwrapper.sh
      export PIP_VIRTUALENV_BASE=$WORKON_HOME
      export PIP_RESPECT_VIRTUALENV=true
    
    fi
    

之后运行命令：
    
    source ~/.bashrc
    

### 使用
    
    mkvirtualenv myproject_ENV    # 创建虚拟环境 myproject_ENV
    workon myproject_ENV          # 激活 myproject_ENV
    deactivate                    # 离开
    rmvirtualenv myproject_ENV    # 删除 myproject_ENV
    lsvirtualenv                  # 虚拟环境列表
    

### 其他命令
    
    showvirtualenv [env]             # 显示指定环境的详情。
    rmvirtualenv [env]               # 移除指定的虚拟环境，移除的前提是当前没有在该环境中工作。如在该环境工作，先使用deactivate退出。
    cpvirtualenv [source] [dest]     # 复制一份虚拟环境。
    cdvirtualenv [subdir]            # 把当前工作目录设置为所在的环境目录。
    cdsitepackages [subdir]          # 把当前工作目录设置为所在环境的sitepackages路径。
    add2virtualenv [dir] [dir]       # 把指定的目录加入当前使用的环境的path中，这常使用于在多个project里面同时使用一个较大的库的情况。
    toggleglobalsitepackages -q      # 控制当前的环境是否使用全局的sitepackages目录。
    

## 参考

  1. virtualenv documentation: [https://virtualenv.pypa.io/en/latest/](https://virtualenv.pypa.io/en/latest/)

  2. virtualenvwrapper documentation: [http://virtualenvwrapper.readthedocs.org/en/latest/](http://virtualenvwrapper.readthedocs.org/en/latest/)
