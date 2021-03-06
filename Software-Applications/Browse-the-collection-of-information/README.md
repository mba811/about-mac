# 信息的浏览与采集

OS X里负责「看」的主要是「预览」和「Safari」，一个是针对保存到本地的各种文档格式的查看，一个负责网页内容的浏览。

## 预览

和程序的名字一样直观，OS X中选中文件后敲空格，默认就会用启动预览程序进行查看，再次敲空格则键退出预览，查看过程中可以使用箭头按键在多个文件之间进行切换查看。「预览」过程虽然操作很简单，不过实际上预览程序极具内涵，能直接查看PDF、文档（TXT、DOC、PAGE）、多种图片（JPEG、TIFF、GIF、PNG）、视频（MOV、MP4），另外计算机上安装的绝大多数软件也支持预览程序直接查看其自有格式。

  * 除了方便快捷的「看」，「预览」程序还能对PDF和图片进行一定的编辑处理，这里值得推荐的是对PDF文件的合并和给PDF文件加封面。

  * 在预览程序中同时打开要合并的PDF文档，选取「显示-缩略图」以打开「缩略图」面板；

  * 选择您要在文稿中移动的页面的缩略图，可以在点按每个页面缩略图的同时按 Shift 键或 Command 键，以选中多个页面。 在边栏中上下拖移选中的页面，直到找到合适的位置后松开鼠标；

> [OS X：使用「预览」合并 PDF 文稿](http://support.apple.com/kb/HT6174?viewlocale=zh_CN)

给PDF文件添加封面的操作也同样简单，从桌面或Finder图片文件夹拖移图片到PDF文件缩略图首页的位置即可。

### 预览中查看的内容能选择复制吗？

默认情况下，预览查看文本类型（TXT、PDF、DOC、PAGE）的文件时只能查看不能选中其中的内容，不过在终端程序（应用程序-实用工具-终端）中粘贴运行以下命令后就可以进行选中和复制，这会在内容采集中更方便。
    
    defaults write com.apple.finder QLEnableTextSelection -bool TRUE;killall Finder

恢复原样的命令是：
    
    defaults delete com.apple.finder QLEnableTextSelection;killall Finder

除了命令行的方式还可以用[OnyX](http://www.onyxmac.com/)来修改。（OnyX是一款免费的针对Mac系统的设置调节软件，比起容易出错的命令行模式来说，操作界面更友好，而且恢复成系统默认的设置也方便。）

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj1/01.png)

## Safari浏览器和扩展

作为OS X的原生浏览器，Safari 和Apple自己的设备结合才是完美的，在触控板上双指上下滑动滚动网页、双指轻拍放大页面、双指左右滑动可以在浏览过的页面之间切换，两指捏合缩小进入标签浏览页面，左右滑动切换标签页。所有的操作平顺流畅，而且符合手势的自然习惯，使用一段时间以后再换到其他浏览器就觉得十分的别扭。

> 启用iCloud以后，Safari的书签、记录的登录密码、阅读列表和正在浏览的标签页可以在多个设备之间同步，真正的实现了阅读和浏览的不间断，实现了内容在Mac、iPad、iPhone之间的流转，而钥匙串的同步也使得在iPhone这样的设备上登录网站变的很简单，只要Mac上记录保存过登录信息到钥匙串，iPhone、iPad上再次登录同一个网站时，再也不用「捉」着小键盘输入一堆密码。

浏览网页时，我们的基本需求包括几个方面，视觉上的、内容收藏上的、还有就是痕迹的保留和清除。

> 在不安装扩展的情况下，将网页直接添加到Safari自己的阅读列表（地址栏左侧的+或者「shift ⇧＋command ⌘＋D」）是首选方案，打开Safari的侧边栏就能方便的浏览阅读列表中的内容，而且可以保持在阅读器模式下进行前后翻页。另外，iCloud的同步能很迅速的让你在iPad或者iPhone上同步阅读阅读列表中收藏的内容。

个人也比较推荐收藏到阅读列表的模式，不只是收藏内容，而且能尽快的消化和完成阅读，否则收集的再多也没有实际的意义。第三方的[Evernote Web Clipper](http://evernote.com/intl/zh-cn/webclipper/)扩展，则定位于做离线收藏和归档，用来归档阅读后觉得有收藏价值的整篇网页或者部分内容。[Evernote](https://itunes.apple.com/cn/app/yin-xiang-bi-ji/id406056744?mt=12)作为网页这一类内容的管理中心，同时兼做一些零碎的笔记。

> Evernote免费提供给普通账户每个月60MB的流量，对于一般商务工作来说是足够的，而且未来升级成高级账户也很简单。菜单栏上的Evernote图标，可以快速的实现笔记、录音和截屏，是采集内容和记录想法的有力助手。

选中一段文字快速保存，这种需求在内容采集上非常频繁，用浏览器扩展来完成不是太顺畅，起码要进入右键菜单，然后选择对应的菜单项目。就算是最原始的「command＋C」和「command＋V」也需要打开一个目标程序才可以。在Mac中还有很多方式：

  * 拖拽到Dock程序图标上，选中文字然后直接拖拽到Dock上的「文本编辑」程序的图标上，就会自动创建一个包含这些内容的新文本文件，当然还可以直接拖到「邮件」程序变成一封新邮件，拖向Evernote变成笔记等等；

  * 直接生成便笺，选中内容后直接按「shift ⇧＋command ⌘＋Y」就会生成一个桌面悬浮的便笺，这个快捷不仅仅可以作用于网页；

  * 选中后直接弹出悬浮窗进行操作，安装上[PopClip](https://itunes.apple.com/cn/app/popclip/id445189367?mt=12)插件，选中内容后可以进行翻译、发送微博、存为文件、发送邮件、添加到任务、存储到Evernote，甚至添加Markdown语法标记等等，不仅在网页里，在其他程序里都可以。这种灵活的内容采集方式已经上升到和工作流的融合上，而且通过安装[PopClip扩展](http://pilotmoon.com/popclip/extensions/)还可以和更多的应用之间产生联动，属于非常实用的效率工具。

除了Evernote这种网页内容采集的插件，Safari里安装的其他三个插件都是和改善阅读有关的：

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj1/02.png)

  * [µblock](https://chrismatic.io/ublock/ublock-latest.safariextz)用来过滤网页中的广告，支持自定义，继Adblock和Adblock Plus之后的后起之秀，支持框架内容的点选过滤、自定义和白名单。只看想看的内容，非常好用的内容清洁工，把大量的图片、悬浮广告去掉后对网页刷新都有很大的提升。

  * [ClickToPlugin](http://hoyois.github.io/safariextensions/clicktoplugin/)用来将Flash转为HTML5的格式播放，Flash的播放很不环保，占用大量的CPU从而导致机器很容易「发烧」，针对国内的视频网站，网友在这个插件的基础上扩展开发了ClickToPluginforChina，鉴于作者一向低调的要求，如果有兴趣的话自行Google搜索。

  * [CustomReader](http://canisbos.com/customreader)是进一步优化Safari的阅读器功能的，允许用户调整阅读界面的字体。Safari的阅读器位于地址栏的右侧，处于可用状态时会显示为蓝色的按钮，进入阅读界面以后，内容会被单纯的显示出来，没有边栏、没有广告，而且字体大小可以自行调节。

> 安全提示，[Safari扩展网站](https://extensions.apple.com/)以外获取的扩展有可能存在安全风险，请确认后再进行安装。

还有一种阅读上的字体情结没有采用插件的方式，而是用更绿色和环保的CSS文件来解决的。

> 将[Safari 字体替换CSS](http://d.pr/HGT7)中的内容粘贴到文本编辑程序中，另存为纯文本并改名为.CSS在Safari中调用就可以了（Safari偏好设置-高级-样式表）。样式表中将网页中的宋体替换成了冬青黑和Helvetica Neue，生效后可以去新浪的官网看看效果。

### 浏览器的痕迹和清理

多数使用场景中，浏览器的浏览痕迹对提升浏览速度是有直接帮助的，毕竟下载过的内容不用重复下载。而且Safari中通过双指左右翻页能在浏览过的页面之中来回切换，这种特性也有赖于对历史页面的缓存才能实现。所以Safari「偏好设置－通用」选项中的「移除历史记录项目」不用设置的太短，毕竟经常去访问的就那么一些网站。

> 在浏览网站的隐私防范方面，除了可以直接以隐私模式浏览网站（菜单栏，「Safari-无痕浏览」），启用隐私模式浏览时，Safari 会停用历史记录，同时，它还会停止保存你的搜索信息以及你在线填写的数据。另外，在Safari的隐私设置中还可以主动勾选「要求网站不要跟踪我」，向网站发送不跟踪的请求。

每次进入无痕浏览模式都需要通过菜单操作不是很方便，可以为它添加一个键盘快捷方式。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj1/03.png)

系统偏好设置－键盘－快捷键－应用程序快捷键，选择应用程序「Safari」，菜单标题中输入和Safari菜单中一致的菜单名称「无痕浏览」，最后添加一个自定义的快捷键保存就可以了。保存后Safari的菜单中同样可以看到。