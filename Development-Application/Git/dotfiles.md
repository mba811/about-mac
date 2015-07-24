# Mac 上使用dotfiles

如果不清楚什么是dotfiles的话，可以参阅[善用dotfiles个人化自己的工作环境](http://cloudchen.logdown.com/posts/49264746647/dotfiles) :

> dotfiles，顾名思义，就是档案名称以. (dot) 为​​prefix 的档案通称，若是您的作业系统是Mac OS X 或是Linux 这类*nix-based 的作业系统，一般来说在视窗环境中是看不到这些档案的，因为对系统来说，他们是所谓的隐藏档，这些档案有一些共通点，那就是他们通常用来储存一些个人化的设定或是自定的拓展功能，以符合使用者本身的使用需求与习惯，有了这些设定好的档案之后，使用者可以让整个系统用起来更为顺手，并且大幅提升他们自身的工作效率！因此对某些使用者来说，这些dotfiles 设定档对他们来说，反而可能是他们机器上最重要的档案呢！

![](http://7q5cfr.com1.z0.glb.clouddn.com/hwj.png)

这份dotfiles是​​fork自  [Holman's dotfiles](https://github.com/holman/dotfiles)，并根据个人的需求修改过，如果有兴趣，阅读完这份文件之后，欢迎fork一份回去配置成适合自己的dotfiles。

更多的dotfiles请参考  [GitHub does dotfiles](https://dotfiles.github.io/)。

* * *

  * [Quick Start](https://www.blogger.com/blogger.g?blogID=696354394590316778#quick-start)
    * [清除并安装OS X](https://www.blogger.com/blogger.g?blogID=696354394590316778#erase-and-reinstall-os-x)
    * [安装Xcode](https://www.blogger.com/blogger.g?blogID=696354394590316778#install-xcode)
    * [安装dotfiles](https://www.blogger.com/blogger.g?blogID=696354394590316778#install-dotfiles)
    * [恢复备份](https://www.blogger.com/blogger.g?blogID=696354394590316778#restore-backup)
  * [How To Use](https://www.blogger.com/blogger.g?blogID=696354394590316778#how-to-use)
    * [dotfiles](https://www.blogger.com/blogger.g?blogID=696354394590316778#dotfiles)
    * [OS X](https://www.blogger.com/blogger.g?blogID=696354394590316778#os-x)
    * [Mackup](https://www.blogger.com/blogger.g?blogID=696354394590316778#mackup)

# [](https://www.blogger.com/blogger.g?blogID=696354394590316778#quick-start)Quick Start

## [](https://www.blogger.com/erase-and-reinstall-os-x)Erase and reinstall OS X

如果你打算从干净的Mac环境开始，请参阅  [OS X：如何清除并安装](http://support.apple.com/zh-tw/HT5943)。

## [](https://www.blogger.com/blogger.g?blogID=696354394590316778#install-xcode)Install Xcode

  1. 更新App Store。
  2. 安装  [Xcode](https://itunes.apple.com/us/app/xcode/id497799835?mt=12)。
  3. 开启Terminal，安装Xcode Command Line Tools:

xcode- select --install

## [](https://www.blogger.com/blogger.g?blogID=696354394590316778#install-dotfiles)Install dotfiles

[下载](https://github.com/amowu/dotfiles/archive/master.zip)或使用git clone一份到  `$HOME`  目录底下的  `.dotfiles`  资料夹里面:
    
    git clone https://github.com/amowu/dotfiles.git ~ /.dotfiles
    

进入  `.dotfiles`  资料夹:
    
    cd  ~ /.dotfiles
    

安装dotfiles:
    
    script/bootstrap
    

`bootstrap.sh`  这个程式会自动完成以下工作:

  1. 检查并安装  [Homebrew](http://brew.sh/)。
  2. 检查并安装  [Oh My Zsh](http://ohmyz.sh/)。
  3. 检查并连结dotfiles( `.zshrc` ,  `.vimrc` ,  `.gitconfig` , `.gitignore` , ...)。
  4. 更新并安装brew packages(binaries, fonts, apps)。
  5. 设置Mac OS X 的defaults settings。

完成之后，手动安装一些App Store 上才有的软体(Dash, Moom, ...)。

## [](https://www.blogger.com/blogger.g?blogID=696354394590316778#restore-backup)Restore backup

使用  [Mackup](https://github.com/lra/mackup)  进行备份回复:
    
    macku​​p restore
    

什么是Mackup? 底下会介绍。

* * *

# [](https://www.blogger.com/blogger.g?blogID=696354394590316778#how-to-use)How To Use

## [](https://www.blogger.com/blogger.g?blogID=696354394590316778#dotfiles)dotfiles

执行  `~/.dotfiles/script/bootstrap`  的时候，脚本会将目录底下所有的  `*.symlink`  档案透过  `ln`  命令建立连结至`$HOME`  目录底下:

topic*.symlink.dotfiles

git gitconfig.symlink ~/.gitconfig

gitignore.symlink ~/.gitignore

macku​​p macku​​p.cfg.symlink ~/.macku​​p.cfg

vim vimrc.symlink ~/.vimrc

zsh zshrc.symlink ~/.zshrc

### [](https://www.blogger.com/blogger.g?blogID=696354394590316778#topical)Topical

每一个环境的配置是以资料夹的形式被独立区分。例如，如果想要新增"Java"的配置到dotfiles，你可以简单的新增一个命名为  `java`  的资料夹，然后将档案建至目录底下。任何副档名是  `.zsh`  的档案将在shell执行时被自动载入至环境中。任何副档名是  `.symlink`的档案将在你执行  `script/bootstrap`  安装时被连结至  `$HOME`  目录底下。.

### [](https://www.blogger.com/blogger.g?blogID=696354394590316778#components)Components

一些目录中比较特别的档案:

  * **bin/** :任何在  `bin/`  目录底下的档案可以在shell执行时直接使用。
  * **topic/*.zsh** :任何  `.zsh`  结尾的档案都会在shell执行时被载入至环境。
  * **topic/path.zsh** :任何命名为  `path.zsh`  的档案会在shell执行时优先被载入至  `$PATH`。
  * **topic/*.symlink** :任何  `*.symlink`  结尾的档案都会在  `$HOME`  目录底下建立连结。这可以让你在配置环境的时候也保持版本控制的优点。新增symlink的时候需要执行  `script/bootstrap`  安装。

不同于  [Holman's dotfiles](https://github.com/holman/dotfiles)，我修改了一些部分:

  * Shell的部分改用  [Oh My Zsh](http://ohmyz.sh/)取代原作者自己配置的zsh。
  * 移除  **topic/aliases.zsh**、**topic/completion.zsh**  等档案，改用Oh My Zsh的[plugins]。([https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins) )代替。
  * 移除  **zsh/prompt.zsh**、**zsh/window.zsh.zsh**  等档案，改用Oh My Zsh的[themes]。([https://github.com/robbyrussell/oh-my-zsh/wiki/Themes](https://github.com/robbyrussell/oh-my-zsh/wiki/Themes) )代替。
  * dotfiles只专注在  **topic/*.symlink**、**topic/path.zsh**  的配置。

## [](https://www.blogger.com/blogger.g?blogID=696354394590316778#os-x)OS X

`bin/dot`  是一支简单的脚本，会在  `script/bootstrap`  配置完dotfiles之后执行，安装自定的OS X程式并设定系统参数配置。

执行  `dot`  之后，它会跑以下两支脚本档:

  1. `$HOME/.dotfiles/homebrew/install.sh`  - Homebrew packages
  2. `$HOME/.dotfiles/osx/set-defaults.sh`  - OS X defaults setting

### [](https://www.blogger.com/blogger.g?blogID=696354394590316778#homebrew-packages)Homebrew packages

执行  `homebrew/install.sh`  的时候，脚本会使用  [Homebrew](http://brew.sh/)  和  [Homebrew Cask](http://caskroom.io/)  来安装  **binary**、**font**  还有 **app**，可以根据个人需求修改这个档案，增加或减少自己需要的packages:
    
    binaries=(
      git
      tree
      ...
    )
    

字型都是以  **font-XXX**  的形式命名，可以用  `brew cask search /font-XXX/`  搜寻是否存在。
    
    fonts=(
      font-roboto
      ...
    )
    

应用程式可以用  `brew cask search XXX`  或是  [Cask Search](http://caskroom.io/search)  网站搜寻是否存在。
    
    apps=(
      dropbox
      google-chrome
      ...
    )
    

以下是目前安装的packages:

Binary

[grc](http://kassiopeia.juls.savba.sk/%7Egarabik/software/grc/README.txt) log 上色

[macku​​p](https://github.com/lra/mackup) 同步应用程式的配置

[tree](http://mama.indstate.edu/users/ice/tree/) 树状目录显示

Font

[font-roboto](http://www.google.com/fonts/specimen/Roboto) Roboto

App

[alfred](http://www.alfredapp.com/) 三大神器之一

[dropbox](http://www.dropbox.com/) 云端硬碟

[google-chrome](https://github.com/amowu/dotfiles/blob/master/www.google.com/chrome) Google 浏览器

[iterm2](http://iterm2.com/) 加强版终端机

[mou](http://25.io/mou/) Markdown 编辑器

[qlcolorcode](https://code.google.com/p/qlcolorcode/) 让Quick Look 支援syntax highlighting

[qlmarkdown](https://github.com/toland/qlmarkdown) 让Quick Look 支援Markdown

[qlstephen](http://whomwah.github.io/qlstephen/) 让Quick Look 支援无副档名的纯文字档

[sourcetree](http://www.sourcetreeapp.com/) Git GUI

[sublime-text3](http://www.sublimetext.com/3) 程式码编辑器

### [](https://www.blogger.com/blogger.g?blogID=696354394590316778#os-x-defaults-setting)OS X defaults setting

执行  `osx/set-defaults.sh`  之后，程式会将Mac OS X的一些系统设置改变，可以根据个人需求修改这个档案，或是参考  [Mathias's dotfiles](https://github.com/mathiasbynens/dotfiles/blob/master/.osx)  整理好的配置。

以下是目前设定的配置:

setting

加快视窗resize 的速度(Cocoa applications) defaults write NSGlobalDomain NSWindowResizeTime -float 0.001

预设展开储存视窗 defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode -bool true

defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode2 -bool true

关闭“你确定要开启这个应用程式?”询问视窗 defaults write com.apple.LaunchServices LSQuarantine -bool false

开启触控板轻触点击功能 defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad Clicking -bool true

defaults -currentHost write NSGlobalDomain com.apple.mouse.tapBehavior -int 1

defaults write NSGlobalDomain com.apple.mouse.tapBehavior -int 1

开启触控板两指轻触弹出右键选单功能 defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad TrackpadRightClick -bool true

开启触控板三指拖曳功能 defaults -currentHost write NSGlobalDomain com.apple.trackpad.threeFingerDragGesture -bool true

defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad TrackpadThreeFingerDrag -bool true

开启触控板四指向下滑出现app expose 功能 defaults write com.apple.AppleMultitouchTrackpad TrackpadThreeFingerVertSwipeGesture -int 0

defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad TrackpadThreeFingerVertSwipeGesture -int 0

defaults write com.apple.dock showAppExposeGestureEnabled -int 1

加快触控板/滑鼠的速度 defaults write NSGlobalDomain com.apple.trackpad.scaling -int 3

defaults write NSGlobalDomain com.apple.mouse.scaling -int 3

开启所有视窗组件支援键盘控制 defaults write NSGlobalDomain AppleKeyboardUIMode -int 3

关闭键盘按住的输入限制 defaults write NSGlobalDomain ApplePressAndHoldEnabled -bool false

加快键盘输入 defaults write NSGlobalDomain KeyRepeat -int 0

预设Finder 起始位置为桌面 defaults write com.apple.finder NewWindowTarget -string "PfDe"

defaults write com.apple.finder NewWindowTargetPath -string "file://${HOME}/Desktop/"

显示副档名 defaults write NSGlobalDomain AppleShowAllExtensions -bool true

显示Finder 状态列 defaults write com.apple.finder ShowStatusBar -bool true

显示Finder 路径列 defaults write com.apple.finder ShowPathbar -bool true

允许框选Finde Quick Look 的文字 defaults write com.apple.finder QLEnableTextSelection -bool true

Finder 标题列显示完整路径 defaults write com.apple.finder _FXShowPosixPathInTitle -bool true

预设搜寻列的结果为当前目录下 defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"

关闭改变副档名的警告提示 defaults write com.apple.finder FXEnableExtensionChangeWarning -bool false

开启资料夹的spring loading 功能 defaults write NSGlobalDomain com.apple.springing.enabled -bool true

开启Dock 的spring loading 功能 defaults write com.apple.dock enable-spring-load-actions-on-all-items -bool true

移除spring loading 的延迟 defaults write NSGlobalDomain com.apple.springing.delay -float 0

避免在network volumes 底下建立.DS_Store 档案 defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true

使用column view 作为Finder 预设显示选项 defaults write com.apple.finder FXPreferredViewStyle -string "clmv"

关闭清空垃圾桶的警告提示 defaults write com.apple.finder WarnOnEmptyTrash -bool false

使用黑色的选单列和Dock defaults write NSGlobalDomain AppleInterfaceStyle Dark

使用缩放的效果作为视窗放大缩小效果 defaults write com.apple.dock mineffect -string "scale"

应用程式缩小至自己的图示 defaults write com.apple.dock minimize-to-application -bool true

显示Dock 应用程式开启中的小亮灯提示 defaults write com.apple.dock show-process-indicators -bool true

关闭Dock 开启应用程式的弹跳动画 defaults write com.apple.dock launchanim -bool false

加快Mission Control 的动画速度 defaults write com.apple.dock expose-animation-duration -float 0.1

关闭Mission Control 的应用程式群组化显示 defaults write com.apple.dock expose-group-by-app -bool false

关闭Dashboard defaults write com.apple.dashboard mcx-disabled -bool true

将Dashboard 从多重桌面之中移除 defaults write com.apple.dock dashboard-in-overlay -bool true

自动隐藏Dock defaults write com.apple.dock autohide -bool true

移除隐藏Dock 的延迟 defaults write com.apple.dock autohide-delay -float 0

移除Dock 的显示/隐藏动画 defaults write com.apple.dock autohide-time-modifier -float 0

将隐藏的应用程式Dock 图示半透明显示 defaults write com.apple.dock showhidden -bool true

以上，若修改过  `homebrew/install.sh`  或  `osx/set-defaults.sh`  之后，直接执行指令:
    
    dot
    

就会再次更新packages 还有defaults setting。

## [](https://www.blogger.com/blogger.g?blogID=696354394590316778#mackup)Mackup

当初始环境都安装好之后，剩下的就是恢复备份。除了  `​​.zsrc`、`.vimrc`  这类dotfile比较适合放在版本控制之外，其他像是Sublime的plugin、iTerm2的setting、Oh My Zsh的plugin、等等很多还有一般应用程式的配置档需要备份，甚至是SSH的key，这些我认为都不适合丢进dotfiles放上GitHub。所以这里介绍  [Mackup](https://github.com/lra/mackup)  这个简单的工具作为解决方案，使用方式很简单，`brew install mackup`  安装完之后只要执行:
    
    macku​​p backup
    

就可以将档案备份到Dropbox 或Google Drive。当需要恢复的时候则是执行:
    
    macku​​p restore
    

就会将云端硬碟上的备份以  `ln`  连结的方式在新电脑上同步。

配置方式也很容易，建立一份  `~/.mackup.cfg`，或是直接使用  `.dofiles/mackup/mackup.cfg.symlink`  来修改:
    
    [storage]
    engine = dropbox #同步的云端硬碟，有dropbox与google_drive可以选择 
    directory = Mackup #同步的资料夹，这里会将所有备份同步至~/Dropbox/Mackup底下
    
    # 指定要同步的应用程式
    [applications_to_sync]
    iterm2
    oh-my-zsh
    sublime-text-3
    ssh
    
    [applications_to_ignore]
    # 指定不想同步的应用程式
    

以下是目前备份的应用程式:

app

[iterm2](http://iterm2.com/) 加强版终端机

[moom](http://manytricks.com/moom/) 视窗布局

[oh-my-zsh](http://ohmyz.sh/) 加强版ZSH

[sourcetree](http://www.sourcetreeapp.com/) Git GUI

[sublime-text-3](http://www.sublimetext.com/) 程式码编辑器

ssh SSH Key

更多详细的配置与支援的软体请参阅  [mackup的文件](https://github.com/lra/mackup/tree/master/doc)。

* * *

## [](https://www.blogger.com/blogger.g?blogID=696354394590316778#)参考文章

  * [Hacker's Guide to Setting up Your Mac](http://lapwinglabs.com/blog/hacker-guide-to-setting-up-your-mac)
  * [First steps with Mac OS X as a Developer](http://carlosbecker.com/posts/first-steps-with-mac-os-x-as-a-developer/)
