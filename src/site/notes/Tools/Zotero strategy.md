---
{"dg-publish":true,"permalink":"/tools/zotero-strategy/"}
---


# Zotero使用技巧

## 常用插件工具
- 浏览器插件Zotero connection
	- chrome安装后可以在页面上直接点击从而收录到相应zotero文件夹
- Better BibTex（可选）
	- 用于Latex引用
- Jasminum（中文文献必备）
- ZotFile（必备）
	- 用于整理附件
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

## 快速复制参考文献格式到ppt
* quick copy
	* preference -> export -> quick copy

## 添加搜索引擎（optional）
preferences -> advanced -> files and folders -> show data directory -> Zotero -> engines.json
### 设置Sci-Hub作为PDF解析器
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

## 参考文献引用
中文书籍引用
- 手动添加条目
- 去douban上找相应的书籍利用插件添加

## ref

1. [在zotero中添加百度学术等搜索引擎](https://www.jianshu.com/p/3ce2f43daa3a)
2. [某些网站（例如知网），无论搜索什么，地址栏URL都不会变化，请问如何找到真实的搜索URL地址？ - 知乎](https://www.zhihu.com/question/320027167)
3. [Zotero搭配Sci-Hub](https://zhuanlan.zhihu.com/p/112141757)
4. [Zotero中文书籍引用流程展示 - 知乎](https://zhuanlan.zhihu.com/p/345447630)