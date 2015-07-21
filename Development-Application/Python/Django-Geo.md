# Mac OS Django Geo 环境搭建

试了试Django + ElasticSearch搭建一个简单的地图显示。在这之前需要安装下各种依赖，

因为一直在报错
    
        File "/home/www/nx2/nx2/nx/models.py", line 6, in <module>
        from django.contrib.gis.geos import Point
    ImportError: cannot import name Point
    

后来找到原理是没有安装Geo的一些依赖

## Mac OS Homebrew GeoDjango安装
    
    $ brew install postgresql
    $ brew install postgis
    $ brew install gdal
    $ brew install libgeoip
    

## Mac OS GeoDjango MacPorts安装
    
    $ sudo port install postgresql93-server
    $ sudo port install geos
    $ sudo port install proj
    $ sudo port install postgis
    $ sudo port install gdal +geos
    $ sudo port install libgeoip
