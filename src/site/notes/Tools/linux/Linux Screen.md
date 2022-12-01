---
{"dg-publish":true,"permalink":"/tools/linux/linux-screen/"}
---


# Ubuntu下screen的使用

- [[Tools/linux/Linux Screen#简介\|简介]]
- [[Tools/linux/Linux Screen#安装\|安装]]
- [[Tools/linux/Linux Screen#新建窗口\|新建窗口]]
- [[Tools/linux/Linux Screen#分离会话\|分离会话]]
- [[Tools/linux/Linux Screen#恢复会话\|恢复会话]]
- [[Tools/linux/Linux Screen#杀死会话\|杀死会话]]
- [[Tools/linux/Linux Screen#清除dead\|清除dead]]

## 简介
关掉终端xshell之后网站也随着关闭，我们可以使用screen[^1]命令，来让保证退出ssh之后程序继续在后台跑。

利用SSH远程连接服务器，运行程序需要保证在此期间窗口不能关闭并且连接不能断开，否则当前窗口所运行的任务就被杀死[^2]。

## 安装
首先可以先查看是否安装screen，通过命令
`screen -ls`
若出现

> The program 'screen' is currently not installed. You can install it by typing:
> sudo apt install screen

说明尚未安装，安装提示，通过命令：
`sudo apt install screen` 安装screen

## 新建窗口
screen -S name
- 可直接通过命令`screen`新建一个窗口，并进入窗口。但通过这种方式新建的窗口没有名字，只有系统分配给它的一个id。当需要恢复窗口时，只能通过id号来恢复。
- 通过命令`screen -S name`，这样就可以新建一个名字为name的窗口，同样系统也会分配给它一个id，当恢复该窗口时既可以通过id号也可以通过窗口名。

## 分离会话
退出当前新建的窗口，通过快键键Ctrl+a+d实现分离，此时窗口会跳出[detached]的提示，并回到主窗口。

## 恢复会话
screen -r name
首先查看当前有哪些screen窗口，通过命令：
`screen -ls` 将列出窗口列表
![](https://cdn.jsdelivr.net/gh/jmwyf/pichosting@master/screen.png)
由以上可知，当前有两个窗口，其中test窗口已经被杀死，test2窗口分离。可以通过以下命令恢复test2：
`screen -r test2` 或 `screen -r 27582`
这样就返回了test2窗口

## 杀死会话
通过命令`kill -9 threadnum`
注意此处只能通过id号来杀死窗口。

## 清除dead
通过命令`screen -wipe`
这个命令将自动清除所有处于dead状态的窗口


[^1]: [GNU's Screen](http://www.gnu.org/software/screen/)
[^2]: [ubuntu下screen的使用 - 裸奔的太阳 - 博客园](https://www.cnblogs.com/quan-coder/p/9857883.html)