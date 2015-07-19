# 数据管理

「文档管理」侧重的是计算机本地文档的组织、检索和存储，「数据管理」侧重的是数据在不同位置的流转和控制，从一台计算机到另一台计算机，从主机到备份硬盘，从本地到云端，以及从软件到软件。数据的流动不仅带来安全和便利，还携带着我们的使用习惯、工作场景和喜好。这一节我们聊聊Mac软件中涉及到数据管理应用：迁移助手、Time Machine、iTunes、iCloud，1Password。

**数据管理的关键词是：还原、迁移、恢复。**

#### Time Machine

启动Time Machine以后，软件会对整个整磁盘做一个完整备份，以后每个小时，Time Machine通过Mac OS X系统的FSEvents(文件系统事件)进程对系统的所有变化进行持续的追踪。当发现过去一小时的系统发生变化以后，Time Machine对那些变化的文件进行备份，属于渐进备份(incremental backup)。以后每天会将头一天的小时备份自动清除，每周会将上一周的每天备份自动清除，保持了一套完整的系统备份。如果电脑没有连上Time Machine硬盘（或超出了Time Capsule的无线信号覆盖范围），系统可以智能地把文件临时备份到电脑的本地硬盘上。

还原整个系统，需要在启动时按住「command+R 」键以从恢复系统启动电脑。显示的「恢复」菜单包括从 Time Machine 备份恢复的选项，选择实用工具中的「从 Time Machine 备份进行恢复」。

相对于还原整个系统，平时使用更多的是还原单个文件，通过顶栏的Time Machine图标直接「进入Time Machine」的时光隧道。

Time Machine浏览器类似时光机的视图窗口中，右边有一个显示时间的垂直刻度线，它表示了备份文件版本所在的时间点。本地快照将与常规备份一起显示在时间线上，二者以不同颜色加以区分。灰色刻度标记代表本地快照，粉色刻度标记代表存储在外置备份磁盘或 Time Capsule 中的备份，如果电脑未连接到外置备份磁盘或 Time Capsule，则粉色刻度标记将变暗。从备份中恢复文件或删除文件的区别在于右键菜单中你的选择。

**一个文件从本地删除后，备份中还会保留，如果要彻底的删除，需要由备份呢中也进行删除。**

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj5/01.png)

具体操作如下：进入「进入Time Machine偏好设置...」暂时关闭「Time Machine」。然后点击「进入Time Machine」选项，在Time Machine界面中的Finder窗口中找到文件所在的位置，右键单击它并在菜单中选择「删除所有备份中当前文件」选项。  
￼  
**原来的备份磁盘空间满了怎么办？**  
整个备份实际上是以磁盘映像文件的形式存在于备份硬盘上的，在停用「Time Machine」后，可以直接双击加载这个磁盘映像文件并对其内容进行访问。

如果原来的备份磁盘空间不足，只需要将新的备份硬盘格式化，将文件夹「Backups.backupdb」拖到新备份驱动器就可以完成备份数据的迁移。具体操作步骤可以参看[Time Machine：如何将备份从当前备份驱动器传输到新的备份驱动器](http://support.apple.com/kb/HT5096?viewlocale=zh_CN)。

**如何提高每次备份的效率？**

  1. 排除频繁变动的大文件  
在5GHz的Wi-Fi网络环境下，备份的平均速度能达到10-13MB/s，几百兆的数据很快就能完成，但是如果每次都备份上GB的数据，花费的时间就会长很多，这里主要的原因是第三方的Papers、DEVONthink Pro这类数据库模式的单一大文件导致的，DEVONthink Pro中微小的变动都会导致整个巨大的数据库文件变化，从而触发Time Machine每小时的备份动作。所以这一类的大的文件，建议排除在Time Machine备份以外，换成周期性的人工备份。

  2. 休眠时间进行自动备份，充分利用设备休眠时间进行自动备份，确认「系统偏好设置-节能器」中勾选了「接上电源适配器时启用Power Nap」，这样，只要电源线插着，晚上合上盖Mac也能自动进行备份。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj5/02.png)


> 首次备份，或者人工备份DEVONthink Pro、Parallels Desktop虚拟机这样的超大的文件时，用「Thunderbolt 至以太网转接器」连接有线进行操作速度会更快。
> 
> 单独手动备份超大的第三方库文件，可以有效降低Time Machine备份的容量大小和提高备份效率；

#### 使用迁移助手

迁移助手是以账户为单元将数据从一台Mac复制到另一台Mac，也可以由Windows复制个人账户相关的数据。  
迁移助手主要用于新旧电脑之间的数据迁移上，即可以[使用“迁移助理”从另一台 Mac 传输文件](http://support.apple.com/kb/HT4413?viewlocale=zh_CN)到另一台，也可以基于[Windows 迁移助理](http://support.apple.com/kb/ht4796?viewlocale=zh_CN)由[从 PC 传输信息](http://support.apple.com/kb/PH14328?viewlocale=zh_CN)。

在使用场景上迁移助理主要用于设备之间，Time Machine则只用于本机的数据备份和还原。如果想把一台机器上Time Machine备份的内容还原到其他机器，只能通过迁移助理来完成。

> 将 Time Machine 备份迁移到新 Mac  
有了新 Mac 后，您可以传输之前制作的 Time Machine 备份中的所有应用软件、文件、设置和其他信息。首次启动新 Mac 时，设置助理会询问您是否要从备份恢复。如果您已设置新 Mac，可使用迁移助理（位于“应用程序/实用工具”中）来执行相同任务。
> 
> 当迁移助理完成传输并且您选择现有 Time Machine 备份驱动器之后，系统将提示您“继承备份历史”。选中之后，您将能在新 Mac 上继续使用现有的 Time Machine 备份。

迁移助理的向导界面中会引导你选择需要迁移的数据，如果你已经设置好帐号进入了系统，然后使用迁移向导，那么受 FileVault 保护的帐户，会提示「无法将 FileVault 用户传输到包含现有用户的 Mac 中」，需要启动旧的 Mac，先关闭该帐户的 FileVault 保护功能，然后再迁移数据。

#### iTunes 资料库

启用iCloud以后，iTunes中已经没有必要保存App一类的东西，需要的时候iPhone或者iPad上随时通过App Store的「已购项目」下载就可以了。iTunes本地保存最多的是音乐和Podcast，这些数据的迁移很简单。只需要将「音乐-iTunes」文件夹复制到新的磁盘位置就可以了。复制完成后，运行一次其中的「iTunes Library.itl」库文件就完成了迁移。  
￼
![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj5/03.png) 

为了节省本地空间，iTunes的库是可以迁移到NAS或者移动硬盘里进行访问的，不过为了保证访问的质量，最少需要5GHz的Wi-Fi网路环境才能保障数据传输速度的要求。

> 如果只是进行备份，可以参看这里：[iTunes 资料库拷贝到外置硬盘驱动器来进行备份](http://support.apple.com/kb/HT1751?viewlocale=zh_CN)。

**iPhone中的音乐和iTunes的同步问题**，虽然iPhone也可以直接删除「音乐」程序中的歌曲，不过和iTunes同步的时候还是以iTunes中的音乐为准，反过来如果在iTunes中删除了某个歌曲，下次同步时会从iPhone中删除掉。

Mac这样设计目的是将电脑上的iTunes定位为音乐的管理中心，所有的操作是以Mac端为准的。要想把不喜欢的歌曲从iPhone上一次性删除，比较好的策略是：在iPhone上给不喜欢的歌曲评分（点击歌曲专辑封面下方会出现评分的5个小点），通过iTunes同步后，按评分排序删除不喜欢的歌曲，最后再和iPhone同步一次就可以了。

**播客的空间占用问题**，iTunes中的播客（Podcast）随着时间的推移会占用很大的空间，有必要修改每个播客的订阅设置，开启「删除已播放的单集」。

#### iCloud文档数据

iCloud文档同步是iCloud同步中开放给应用程序同步文档数据的地方，支持iCloud的应用可以利用它来完成不同设备之间的文档同步，例如，Mac自带的Pages、Numbers、Keynote，还有第三方的Day One、Ulysses、Pixelmator等等。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj5/04.png)

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj5/05.png) 

iCloud的设置中可以决定启用那些应用的iCloud同步，同时也可以在这里管理和删除应用程序的iCloud文档内容。点击iCloud存储空间旁的「管理」按钮进入iCloud文档的具体管理界面，选中程序列表中的程序，然后决定是「删除」还是「全部删除」。

和OS X 10.10中即将推出的新功能iCloud Drive相比，现在的iCloud文档的访问操作显得太隐晦了，要辗转好几个层级才能访问到。iCloud Drive直接整合到了文件管理器Finder中，有点类似Dropbox的方式，在Finder中就能方便的访问云端文件或者将文件保存到云端，不知道这个功能出来以后是否可以替代Dropbox，毕竟目前国内访问Dropbox并不是很顺畅，需要设置代理。

#### 密码管理

网站访问的密码推荐优先使用Safari自带的密码管理器来设置密码和完成自动登录。通过iCloud，储存的密码会自动同步到其他Mac和iOS设备，所以不用担心Safari生成的密码过于复杂而增加你在其他设备上访问时的繁琐程度。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj5/06.png) 

Safari中存储的密码，会在登录对应的网站时自动提示输入。如果要查询密码，打开Safari的「偏好设置-密码」管理界面，通过搜索来快速定位存储的密码，勾选「显示所选网站密码」来显示密码内容。

Safari只是管理网站密码的小管家，「钥匙串访问」（应用程序-实用工具-钥匙串访问）程序才是密码的总管，其中不仅包含所有的网站密码，还包括邮箱帐号、Time Capsule、WIFI、共享文件夹、加密磁盘映像口令等各种密码。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj5/07.png) 

遇到无线路由器Wi-Fi密码修改导致的无法登录？忘记了Time Capsule磁盘访问账户名称WIFI密码等情况，都会用到「钥匙串访问」程序。WIFI密码错误的问题，在「钥匙串访问」通过SSID名称搜索到具体的WIFI连接记录以后删除旧的记录重新登录WIFI就可以。

钥匙串中保存的密码通过iCloud会同步到iOS和其他Mac中，这意味着如果你在Mac上登录连接过的WIFI，iPhone上不会提示就可以自动登录。时间长了或许自己都不记得密码是多少，或者遇到其他人想知道具体的WIFI连接密码时，我们可以通过「钥匙串访问」搜索WIFI的SSID名称，双击打开具体密码信息页面，勾选「显示密码」。  
￼
![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj5/08.png)

第三方密码管理软件的需求主要是在跨平台和不同浏览器这一块，例如最有代表性的[1Password](https://itunes.apple.com/cn/app/1password/id443987910?mt=12)，在网站密码管理这一块和Safari的密码管理功能上有所重叠，不过它的优势是通过插件可以在Chrome、Safari、Firefox、Opera这些浏览器上同步1Password保存的网站密码，另一个特色就是可以用来管理非网站类的各种密码，例如：软件序列号、银行卡、电子邮件账户、Ftp密码等等。

[1Password](https://agilebits.com/onepassword)支持Windows、Mac、iOS和Android，支持iCloud、Dropbox的同步，是密码管理上非常好的助力。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj5/09.png)
  
同步方式上，1Password可以选择Dropbox来保存和同步密码，如果这样设定，那么除了1Password的主密码以外，你还需要记好Dropbox的密码，否则在新机器部署时容易陷入一个死循环，因为这确实是一个实际发生过的故事：→ 要配置1Password必须先安装好Dropbox，→要登录Dropbox，→需要查找Dropbox密码，要查询密码就需要安装1Password，→ 回到起点 ♾ 。

密码管理的原则中，除了集中分类存储以外，建议尽量为每个账户设置使用「密码生成器」生成的随机密码，这种随机密码没有规律可言，被破解或者网站数据库泄露也不会影响其他账户的安全。另外，如Apple ID、Gmail这些重要账户不要仅依靠密码来提高安全性，建议开启两步验证，短信通知一类的安全保障手段。