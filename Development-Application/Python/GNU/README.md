# Mac OS 安装GNU命令行工具

因为某种原因，使用了一个新的Mac OS系统，又出于某种原因需要安装Emacs 24，才发现原来自带的版本是23，于是下了一个安装之。原来Mac OS的很多常用软件并不是更新得频繁，对于一个有最新强迫症的人来说，这。。。

## 安装之前

原文:[http://www.topbug.net/blog/2013/04/14/install-and-use-gnu-command-line-tools-in-mac-os-x/](http://www.topbug.net/blog/2013/04/14/install-and-use-gnu-command-line-tools-in-mac-os-x/)

需要有Hombrew，而且还要有Xcode
    
    ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
    

添加到`.zshrc`或者`.bashrc`，一直习惯用bash，用的是`.bash_profile`。

## 安装GNU命令行工具

1.安装coreutils
    
        brew install coreutils
    

2.添加brew的repo
    
        brew tap homebrew/dupes
    

3.安装下列的软件
    
    brew install binutils
    brew install diffutils
    brew install ed --default-names
    brew install findutils --default-names
    brew install gawk
    brew install gnu-indent --default-names
    brew install gnu-sed --default-names
    brew install gnu-tar --default-names
    brew install gnu-which --default-names
    brew install gnutls --default-names
    brew install grep --default-names
    brew install gzip
    brew install screen
    brew install watch
    brew install wdiff --with-gettext
    brew install wget
    

对于那些已经安装的想要最新版本的
    
    brew install bash
    brew install emacs
    brew install gdb  # gdb requires further actions to make it work. See `brew info gdb`.
    brew install gpatch
    brew install m4
    brew install make
    brew install nano
    

不是GNU的
    
    brew install file-formula
    brew install git
    brew install less
    brew install openssh --with-brewed-openssl
    brew install perl518   # must run "brew tap homebrew/versions" first!
    brew install python --with-brewed-openssl
    brew install rsync
    brew install svn
    brew install unzip
    brew install vim --override-system-vi
    brew install macvim --override-system-vim --custom-system-icons
    brew install zsh
    

### 总结

虽然感觉起来没有什么大的变化，但是有种以后更新方便的感觉，只是没有GNU/Linux上来得爽，有提示可更新。
