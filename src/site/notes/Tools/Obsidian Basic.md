---
{"dg-publish":true,"permalink":"/tools/obsidian-basic/"}
---


# Obsidian基础使用：日记、周记、块、双链、和Zotero联动
> 我不是在做笔记而是笔记在做我；
> 看了这些笔记工具，一直在迁移笔记的路上；
> -- 网友

之前我做笔记的工具一直是markdown工具比如typora加上网盘，最近正在看卡片笔记写作法
<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">



## 引言
你是否还在为读完一本书只留下许多下划线，而脑袋空空而烦恼？是否还在为要写论文时，一切要重头开始准备材料而苦闷？这里卢曼为你讲解了他思考写作的方法。

其实哪有什么惊人绝技，有的只是把简单有效的方法用到极致罢了。

卡片笔记方法创始人是一个社会科学研究人员卢曼，自己的简历只有寥寥数字，姓名卢曼、研究方向社会学、研究时间30年、成本0，写了50多本著作。而其来源即是平时积累笔记的过程。那么他是怎么记笔记的？


</div></div>
于是开始折腾一些最近比较流行的笔记工具。比如`Obsidian`、`logseq`，到底哪个好用，大家可以自己都试试，这里主要说下Obsidian基础用法。

## Daily
首先是日记功能，每天我们都会记录一些零碎的工作记录、想法或者其他，都可以写在日记里面，我把它称为`dlog`。
- Open Daily plugin in setting-> core plugins->Daily notes
	- 在Daily设置里面可以添加模板，指定存放位置。这里要注意虽然可以改文件名称，但是我以为可以加上精确时间，导致一开始设置为YYYY-MM-DD HH:mm 直接不能创建文件，折腾了好久，用YYYY-MM-DD就可以，如果要精确时间你可以在模板中添加。

## Weekly 
周记复盘。基于`Calendar`插件完成，在设置中找到放置模板以及笔记的文件夹路径，然后点击日记面板中周数就可以新建周记了。

## Blocks
使用\!\[\[\]\]可以引用块的方式来展示之前的笔记，通过在文件名后面加\#一直链接到小标题。比如`![[test#hello world]]` ，下面我就引用本文档自己其中一块，当然好用之处在于可以引用其他文档的块。

<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">



## Weekly 
周记复盘。基于`Calendar`插件完成，在设置中找到放置模板以及笔记的文件夹路径，然后点击日记面板中周数就可以新建周记了。


</div></div>

## links
链接引用方式也很简单，通过\[\[\]\]，如：`[[什么是双向链接]]` ，这里就展示了插入一个链接，然后可以进行跳转操作。双链顾名思义就是你可以链接我，我也可以链接你。这样的好处就是增加文档间的关系，或许在日后通过网状图复盘的时候你可以快速找到聚在一起的文章，从而进行总结。
- 可以从侧边栏，看到`outgoing links:引用的文档`和`backlinks:谁引用这篇文档`
- 安装Sliding Panes插件后使用`ctrl/cmd + 点击`可以分屏展示文档，不安装插件也可以。

## Split
分屏功能，用于同时看不同的文档。目前已支持开新窗口。

## Shortcuts
必备快捷键
命令面板：`ctrl/cmd + p` ，这样你就不用记所有插件的联动方式

## Plugins
插件推荐，除了核心插件，可以打开社区插件，关掉安全模式就可以安装github上的插件了，网络不好建议先查找访问github方式。
使用插件都需要先在设置里面将插件打开。
* Calendar 日历(必备)；设置模板，加上memos的section
* obsidian memos 碎碎念（必备）；设置具体section后面补充内容
* obsidian Pandoc (必备) 转化多种格式如docx等
* Day planner(可选) 每日计划；由于使用时前面有时间戳，容易和memos插件冲突，即你的计划全被处理到memos上面去了，所以需要memos设置具体section。
* kanban 任务看板（可选）
* mindmap 思维导图（可选）
* Sliding panes 分屏用于展示链接文章（可选）
* Citation Zotero联动使用（可选）
* Outlier 大纲式展示，用过幕布等工具的可能知道（可选）
* [ ] ...以后补充

### Plugins development
插件开发，有些你想要的功能，比如联动某些网站记笔记等等没有插件可以支持可以自己开发，详见[[Tools/Obsidian plugins development\|Obsidian plugins development]]

## Zotero
目前是用`citation`插件的方式来联动，感觉还可以
* 安装插件`citation`
* 导出zotero文献基于better bibTex插件格式，可以放到obsidian同级目录（我是整个Library导出，会自动更新）
* 在citation setting中选择biblatex, 设置library目录，就可以操作了。设置目录是目录开头不用\/，直接写
* 快捷键shift + ctrl + o是创建新的文献笔记，快捷键插件中可以设置，笔记目录也可以在插件中设置，写完文献笔记就可以和其他文档相互链接进一步总结了。
![](https://cdn.jsdelivr.net/gh/jmwyf/pichosting@master/zoteroobsidian.png)
## Dateview
[Obsidian 插件之 Dataview - 少数派](https://sspai.com/post/68183?ivk_sa=1024320u)
```{dataview}
list or table
from 
where
```

## Sync
‼️基于iCloud在不同客户端同步要注意各平台要么同时在线都有网络，要么在没有网络情况下退出客户端，不然可能会出现在没网的客户端中没有编辑的文本在联网时自动上传覆盖了在其他客户端中编辑的内容

## Ref
1. [周记创建](https://zhuanlan.zhihu.com/p/403117880)