# MySQL

### 安装 MySQL

用下面的命令就可以自动安装了：
    
    $ brew install mysql
    

如果想让 MySQL 开机自动启动，可以如下操作：
    
    $ mkdir -p ~/Library/LaunchAgents
    $ ln -sfv /usr/local/opt/mysql/*.plist ~/Library/LaunchAgents
    $ find /usr/local/Cellar/mysql/ -name "homebrew.mxcl.mysql.plist" -exec cp {} ~/Library/LaunchAgents/ \;
    $ launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
    

设置 MySQL 用户以及数据存放地址
    
    $ unset TMPDIR
    $ mysql_install_db --verbose --user=`whoami` --basedir="$(brew --prefix mysql)" --datadir=/usr/local/var/mysql --tmpdir=/tmp
    

好了，可以启动了
    
    $ mysql.server start
    

另外的参数还有 `{start|stop|restart|reload|force-reload|status}`

大部分的介绍就在此结束了。