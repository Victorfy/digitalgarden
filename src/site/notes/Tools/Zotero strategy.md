---
{"dg-publish":true,"permalink":"/tools/zotero-strategy/"}
---


# Zotero使用技巧

- [[Tools/Zotero strategy#安装\|安装]]
- [[Tools/Zotero strategy#常用插件工具\|常用插件工具]]
- [[Tools/Zotero strategy#坚果云存储文献\|坚果云存储文献]]
- [[Tools/Zotero strategy#利用Sci-hub下载原文\|利用Sci-hub下载原文]]
- [[Tools/Zotero strategy#引用参考文献\|引用参考文献]]
	- [[Tools/Zotero strategy#引用参考文献\|中文书籍引用]]
	- [[Tools/Zotero strategy#引用参考文献\|中英文混合引用]]
	- [[Tools/Zotero strategy#引用参考文献\|快速复制参考文献格式到ppt]]
- [[Tools/Zotero strategy#添加搜索引擎\|添加搜索引擎]]

## 安装
- 官网[Zotero | Your personal research assistant](https://www.zotero.org/)下载安装

## 常用插件工具
zotero拥有很多开源插件，实现比如文献重命名、影响因子更新等，这也是相比其他文献管理软件来说优势之一。
- 浏览器插件Zotero connection
	- chrome安装后可以在页面上直接点击从而收录到相应zotero文件夹
- Jasminum（中文文献必备）
- ZotFile（必备）
	- 用于整理附件
- Better BibTex（可选）
	- 用于Latex引用
- 其他插件可看[Zotero中文社区](https://zotero-chinese.gitee.io/zotero-plugins/#/)
	- 更新影响因子之类的

## 坚果云存储文献
可以利用坚果云实现pdf文件在多台电脑间同步
- 坚果云上新建zotero文件夹
- 安装Zotfile插件
	- 设置源附件目录（默认目录）
	- 目标附件目录（坚果云地址），zotero connection拉取附件后可以移动到坚果云
- Zotero - preference - advanced - files and folder - linked attachment选择相对路径填写坚果云中新建的路径
- 在其他电脑上安装坚果云同理设置即可同步附件

## 利用Sci-hub下载原文
设置Sci-Hub作为PDF解析器[^1]
- PDF resolvers的设置在Zotero的Config Editor中。
- 我们打开Zotero的首选项，进入`Advanced-->Config Editor`。
- 搜索`extensions.zotero.findPDFs.resolvers`，如下。
- 双击`extensions.zotero.findPDFs.resolvers`，默认情况下是只有一对`[]`。
- 删除`[]`，并将以下代码粘贴进去。
```text
{
    "name":"Sci-Hub",
    "method":"GET",
    "url":"https://sci-hub.ren/{doi}",
    "mode":"html",
    "selector":"#pdf",
    "attribute":"src",
    "automatic":true
}
```
- 然后点击OK。
到此就成功将Sci-Hub配置为PDF解析器了，也就是说替代了默认的Unpaywall。

## 引用参考文献
### 中文书籍引用
- 手动添加条目[^2]
- 去douban上找相应的书籍利用浏览器connection插件添加
### 中英文混合引用
- 直接同时生成“等”和“et al”，在下面代码库中找到合适自己的引用方式，一般用002[^3]
### 快速复制参考文献格式到ppt
* quick copy
	* preference -> export -> quick copy

## 添加搜索引擎
添加搜索引擎[^4]可以在Zotero右上角`lookup engine`添加一下快速查找该文献信息的方式，比如用connected papers网站来查某篇文献。通过编辑engines.json来完成，基于文献信息加上网站本身网址来确定结果。
preferences -> advanced -> files and folders -> show data directory -> Zotero -> engines.json


[^1]: [Zotero搭配Sci-Hub](https://zhuanlan.zhihu.com/p/112141757)
[^2]: [Zotero中文书籍引用流程展示 - 知乎](https://zhuanlan.zhihu.com/p/345447630)
[^3]: [GitHub - redleafnew/Chinese-STD-GB-T-7714-related-csl: GB/T 7714相关的csl以及Zotero使用技巧及教程。](https://github.com/redleafnew/Chinese-std-GB-T-7714-related-csl)
[^4]: [在zotero中添加百度学术等搜索引擎](https://www.jianshu.com/p/3ce2f43daa3a)，[某些网站（例如知网），无论搜索什么，地址栏URL都不会变化，请问如何找到真实的搜索URL地址？ - 知乎](https://www.zhihu.com/question/320027167)
