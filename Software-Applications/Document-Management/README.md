# 文档管理

Windows的应用生态里，我们最熟悉的商务应用是微软的Office 套件（Word、Excel、PowerPoint、Outlook、Project、Visio），还有Adobe公司的Photoshop、Acrobat等等。对应到Mac系统中最匹配的分别是iWork（Pages、Numbers、Keynote）、Mail、[OmniPlan](https://itunes.apple.com/cn/app/omniplan/id404656809?mt=12)、[OmniGraffle](https://itunes.apple.com/cn/app/omnigraffle-6/id711830901?mt=12)，图片处理方面的[Pixelmator](https://itunes.apple.com/cn/app/pixelmator/id407963104?mt=12)以及系统自带的预览程序。

在易用性上Mac的应用大部分都很容易上手，但还是需要一个学习过程，转变观念是一方面，数据迁移则是另一个不容忽视的问题。所以我们还需要一个Parallels Desktop，用虚拟机营造一个Windows的工作环境，既为软件兼容服务，也为了方便历史数据的平滑过渡。因为即便是一家公司开发的面向两个平台的软件，在兼容性上还是会存在问题，当然这里主要指的就是Office。

> Parallels Desktop的作用就是把Windows当成Mac的一个应用程序来对待，可以在Mac应用的体验环境下兼容Windows的应用。
针对Parallels Desktop以及上述大型软件的具体介绍，会在后面的专题文章中具体介绍。

打开电脑里的那些大型软件的时候，展开的也是我们日常的工作场景，写个邮件、码码字、画画图、绘制表格整个图表一类的。Mac上多个程序之间的操作体验不只是停留在「command＋tab」的切换上，如果按桌面来部署不同类型的程序，那么切换就是四指在触控板上的轻快一划。通过[Time Sink](https://itunes.apple.com/cn/app/time-sink/id404363161?mt=12)一类的操作统计软件，不难发现，每天除了围绕工作场景的专业软件以外，更多工作时间花费在了其他地方，为了创作内容而进行的准备工作和后续工作：

• 把文档保存在那里更合适？
• 怎样快速的查找以前的文档？
• 一堆素材和资源性的文档如何管理？
• 屏幕截图的管理？
• 想到的东西如何进行快速记录？

#### 文档的存储

Finder左栏的默认列表示意了一个非常清晰的内容组织结构，按照文件的位置（Dropbox、桌面）、类型（文稿、音乐、图片）、作用（下载、共享）、频度（我的所有文件）进行了划分，Windows中也有类似的结构，采用收藏夹和库的方式来组织文件。Finder中还增加了一个标记功能，通过颜色和自定义的标签对文档进行归类。

Finder的文件划分结构下，如果你还钟情于传统的文件夹管理方式，可以在「文稿」一级目录下再进行划分，目录结构保持两层就足够了，再增加实际应用的帮助不大，只会自寻烦恼。

传统的按文件的创建时间、名称排序之外，按应用程序、种类（文件后缀名）分组在某些场景中能更清晰的展现内容。Finder的标记赋予了用户更灵活管理文件的另一种方式，你既可以用它来标注文件的时效性、重要性，也可以用来定义自己的分类。每个文件是可以包含多个标记的，所以几种标注方式可以混用，文字和颜色也可以互补，标记的命名上建议使用你熟悉和直观的词语。

Finder中的分类、分组不仅让文件看上去有组织性，同时也是为了能快速的找到文件。如果说分类和文件夹是**「视距」**内找到文件的方法，那么Mac中还有一个**「超视距」**定位文件的方法，就是Spotlight（control ⌃+空格）。Spotlight是Mac中全局的搜索工具，通过键盘快捷键弹出窗口后，直接输入想要搜索内容的关键词，在Spotlight上可以浏览包括维基百科、必应、地图等方面的网页数据源，同时也可以立即转化测量、温度、汇率等数值。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj2/01.png)

有了Spotlight和Finder的相互支撑，那么文档存储的问题就很简单了，「当前」文档直接保存到「文稿」或者「图片」文件夹里，临时文件保存到「下载」文件夹（可将「下载」排除在Time Machine自动备份之外）。

> 在「系统偏好设置-Spotlight」中能具体设置它的搜索范围，或者到「Spotlight-隐私」中排除不需要检索的文件夹。了解了Spotlight的强大就能体会到实际上文件放在那里不重要，只要平时养成了良好的命名和标注习惯，用Spotlight找到它很快。

当前文档保存到「文稿」，那么「当下」文档可以直接保存到桌面，例如，屏幕截图、图标和文本片段等等创作中要用到的素材。在不同的桌面切换时，桌面上的文件并不会随着切换而变化，所以桌面用来作为创作过程中不同软件的共享空间非常合适。等编辑作业完成，再将桌面上的文件转移到其他地方或者直接删除。

> 触控板上张开拇指和其他三个手指显示桌面

#### 归档文件管理

价值文档的生命周期包含三个阶段：当前（阶段）、当下（时刻）和归档（历史）。「当前」的文档以Finder为管理中心，追求方便和扁平化，利用分类、标记和分组来存储和管理；「当下」的文件因为时效性的关系以桌面为中心，方便在不同程序间共享；而需要「归档」的文件（短期内不会用到，偶尔会检索查询的这类文档）则可以按照时间周期从「文稿」中迁移出来，令「文稿」文件夹更清爽。

将文档按时间条件迁移出「文稿」可以利用Finder中的搜索条件来检索定位一批文件，也可以用「应用程序-实用工具-Automator」制定自动化规则，不过普通用户更适合用简单第三方软件[Hazel](http://www.noodlesoft.com/)来实现，自动根据你设定的规则移动文件到指定的位置。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj2/02.png)

Hazel安装后会在「系统偏好设置」中增加一个设置图标，任务栏默认也会显示一个扫把图标。打开Hazel后添加要监控的文件夹，然后添加相应的规则后就可以启用了。当然，在运行前最好先通过顶栏图标「Stop Hazel」，然后选中文件夹栏下方的眼睛图标，查看匹配规则的文档是否正确，点击预览窗口中每个文档后的字母「 ⓘ」 会显示详细的属性信息。

如上图所示，为了配合Hazel的自动化处理，「文稿」文件夹下我新建了一个「归档」文件夹和「个人」文件夹。目的是把符合条件的文件迁移到「归档」，把包含个人标签的文件迁移到「个人」文件夹。为此创建了四条规则：

  1. 按季度归档移动文稿类型的文件（Scrivener、Pages、Number、Keynote、OmniGraffle等），并按文件后缀创建子文件夹。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj2/03.png)


Hazel规则设置1

  2. 按季度归档文档类型以外的其他文件，其中专门排除了DEVONthink的库文件，而且为了保险加了一个大小的限制。
doc、xls这些微软体系的文档，在Mac的文档分类中被分为压缩文件，没有放在文档分类中，不知道算不算Mac的一种「幽默」。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj2/04.png)


  3. 归档标签是「归档」的文件，在按时间自动处理文件的之外的半自动方式，随时将你觉得需要归档的文件移动到归档文件夹中。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj2/05.png)


  4. 归档标签中包含「个人」的文件到个人文件夹，这条规则主要用来归集私有文件。条件和上条类似，只是把包含的标签改了。

> 当然Hazel的自动处理还可以做很多其他的事情，例如，把大文件集中放到一个地方，结合标签中你命名的「公司」、「会议记录」等按年度、月份等条件进行归档分类，或者定时移动放在桌面的屏幕截图文件等等。
Hazel中的日期可以具体定期其格式，如果要设定归档子文件夹为季度，需要编辑日期的具体格式。

使用本地文件夹的方式归档文件，这样的好处是系统的Spotlight很容易搜索到，而且文件能同样受到Time Machine的保护。累计到一定时间周期，比如一年以后，可以再由归档文件夹里把文件压缩打包丢到TimeCapsule、移动硬盘。

#### 屏幕截图和截图管理

写上一堆文字有时候不如一张截图直观明确，也正是因为对屏幕截图功能的普遍需求，不知道从什么时候开始，是个流行应用就包含截图功能，数数我Mac里就好几个：百度输入法、QQ、Droplr、Evernote，如果再算上OS X自带的截图功能，键盘快捷键都有点分配不过来的感觉。

系统自带的截图包括两个动作：全屏（⇧⌘3）和区域（⇧⌘4）。按「shift+command+4」 激活区域截图，等拖拽选区的指针出来以后，如果继续敲空格就可以直接截取程序窗口。关于系统自带截图热键的介绍，具体参详 [OS X：为屏幕拍照片](http://support.apple.com/kb/HT5775?viewlocale=zh_CN&locale=en_US)。OS X里还另外预装了一个独立的「应用程序-实用工具-抓图」程序，可以设定10秒钟后的定时截取屏幕。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj2/06.png)

系统截图默认是以PNG格式保存到桌面，并自动命名为「屏幕快照（日期和时间）.png」，另外获得的窗口截图包含阴影。如果想改变默认保存的图片格式、命名方式以及保存位置等设置，可以通过命令行或更简单的[OnyX](http://www.onyxmac.com/)来修改。（OnyX是一款免费的针对Mac系统的设置调节软件，比起容易出错的命令行模式来说，操作界面更友好，而且恢复成系统默认的设置也方便。）

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj2/07.png)

Png格式的截图可以集中到图片文件夹，并为其新建一个类似于「Screenshot」的文件夹，便于近期内查看。自动化处理上，可以使用上面提到的Hazel自动定时移动到指定文件夹。

不同于系统自带的，或者某些软件附带的截图功能，专业的截图软件除了截图功能之外，还会包含丰富的标注功能，比较有代表性的有：轻量级的[Skitch](https://itunes.apple.com/cn/app/yin-xiang-bi-ji-quan-dian/id425955336?mt=12)、重量级的[Voila](https://itunes.apple.com/cn/app/voila-screen-recorder-screen/id407741870?mt=12)、[Snagit](https://itunes.apple.com/cn/app/snagit/id492729790?mt=12)。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj2/08.png)

为了处理大量的软件截图，三款软件都用过一段时间，最先放弃的是Skitch，因为标注功能太单一，稍微复杂一点的标注需求就无法满足了。Voila的对截图的分组管理很有特色，对于一堆截图的管理来说会方便很多，不过在多个图片的拼合、标注样式、模板的扩展上就比Snagit要差一截。

> 专业截图软件会将截图保存为自己的私有格式，包含涂层和标注层，这样以后还可以调整标注和其中的文字内容。

#### 思维导图和笔记

系统自带的便笺（应用程序－便笺）、备忘录、文本编辑程序都可以用来记录琐碎和临时的想法，将它们固定在Dock栏上就可以。在网页以及大多数文档程序中选中文字直接按「shift＋command＋Y」能在全局范围下快速激活便笺。第三方的软件中，[Evernote](https://itunes.apple.com/cn/app/yin-xiang-bi-ji/id406056744?mt=12)、[Day One](https://itunes.apple.com/cn/app/day-one-ri-zhi-ri-ji-ruan-jian/id422304217?mt=12)都是值得推荐的笔记软件，通过顶栏上各自的图标就可以打开记录窗口。

思维导图是另一种工作中记录想法的有效手段，有两种类型的可供选择：树形分叉结构的[XMind](http://www.xmind.net/)、[MindNode PRO](https://itunes.apple.com/cn/app/mindnode-pro/id402398561?mt=12)和自由模式的[Scapple](http://www.literatureandlatte.com/scapple.php)，Scapple独特的地方在于可以获得如同在纸面上整理想法的感受，没有中心点的概念，任何地方都可以记录（类似的还有Curio），而XMind、MindNode PRO则是基于一个中心进行发散，通过树形结构记录连接所有内容。

![](http://7q5cfr.com1.z0.glb.clouddn.com/@/mrj2/09.png)

在使用上都可以方便的拖拽图片、文字到其中，支持导出多种格式：PDF、PNG、RTF、TXT、OPML等。

#### 素材和资料的管理

这里的素材是指创作的过程中搜集储备的各种图片、图标、PDF文献、文档、网页等等。从文档数量的比重上来看，素材往往是自己创作文档的好几倍，这一类资源合适用「库」的方式来管理，并与「文稿」性质的文档分隔开来。

库是集中管理文件非常好的一种方式，前面内容中提到的Evernote也拥有库的特点，不过它的目标定位在网页类文件和笔记管理上，而且由于网络的依赖和流量限制等关系，只适用于收藏网页和笔记。

iPhoto就是以图片库的方式来保存照片的，所有的图片、文字、标签全部存储在一个库中，形式上是一个独立的文件，可以任意移动位置，可以放到移动硬盘，也可以放到Dropbox随时同步。iPhoto除了管理个人的照片之外，也是可以用来管理素材图片的，只需要单独建一个照片库就可以。

> 按住option键再点击iPhoto的程序图标，选择加载不同的照片库
>
> 素材库主要时用于本地，所以不建议开启这个库的「照片流」

用[Inboard](https://itunes.apple.com/cn/app/inboard-image-screenshot-photo/id944109819?mt=12)、[Ember](https://itunes.apple.com/cn/app/ember-screenshot-annotate/id402456742?mt=12)来管理照片、网站截图、文本也是个不错的选择，适合偏设计类的图片管理。

专门用来管理文件的第三方软件有[Together](https://itunes.apple.com/cn/app/together-3/id641534696?mt=12)、[DEVONthink Pro](http://www.devontechnologies.com/products/devonthink/devonthink-pro.html)这类的软件，不仅支持标签标注文件，而且预览功能都不错，可以直接在库中查看各种文件。专注于PDF文件和学术资源管理推荐使用[Papers](http://www.papersapp.com/mac/)，尤其适合英文PDF线下和线上的下载和查询资料。

**上面的几款软件都是用来管理资源性文档的，自己创作的文档利用系统来管理和检索会更方便，因为文档一旦被收入到这些文件管理软件的库中，系统就无法再搜索和定位到了。另外，投资购买这几个软件前先评估一下你可能要管理的文件的数量，如果本来没多少，必要性不大。**

> DEVONthink的单数据库文件数上限是20万，字数（Words）上限是3亿，所以即便看上去这个单独的库文件会很大，它的可靠性也不用担心。
