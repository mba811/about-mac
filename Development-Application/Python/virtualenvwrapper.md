# Virtualenvwrapper 安裝與使用

### 前言

這篇是給知道和會使用virtualenv的OS X user，讓他們在使用virtualenv上更為方便。  
至於安裝過和沒用過virtualenv的可以參考[這篇](http://www.openfoundry.org/tw/tech-column/8516-pythons-virtual-environment-and-multi-version-programming-tools-virtualenv-and-pythonbrew)。

* * *

### 安裝

看個人電腦環境，執行：
    
    $ pip install virtualenvwrapper
    

or
    
    $ sudo pip install virtualenvwrapper
    

接著再增加下面三行到你的shell啟動設定檔(.bashrc、.bash_profile或.profile)：
    
    export WORKON_HOME=$HOME/.virtualenvs  
    export PROJECT_HOME=$HOME/Devel  
    source /usr/local/bin/virtualenvwrapper.sh
    

Reload：
    
    $ source ~/.bashrc
    

* * *

### 使用

1.先run
    
    workon
    

會發現什麼都沒有。

2.run
    
    mkvirtualenv temp
    

會建立virtualenv temp，同時也啟動它。

3.再run
    
    workon
    

會發現有一個temp被建立了。

4.解除虛擬環境的方式跟virtualenv的預設方式一樣，run
    
    deactivate
    

5.當下次想用再次使用虛擬環境時，可以先下workon查看，再下workon+虛擬環境名稱：
    
    $ workon  
    temp1 temp2  
    $ workon temp1  
    (temp1)$
    

6.刪除虛擬環境，run：
    
    rmvirtualenv temp
    

* * *

### Reference

+[Python 的虛擬環境及多版本開發利器─Virtualenv 與 Pythonbrew](http://www.openfoundry.org/tw/tech-column/8516-pythons-virtual-environment-and-multi-version-programming-tools-virtualenv-and-pythonbrew)  
+[Installation of virtualenvwrapper](http://virtualenvwrapper.readthedocs.org/en/latest/install.html)