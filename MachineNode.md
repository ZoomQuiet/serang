BaseStructure
# AE中的机器结点(Machine Node) #
## AE结点是真正运行用户App的机器。每个这样的结点上所运行的程序分为三部分 ##

  1. App的运行环境相关的程序包括sandbox,这是基础环境
  1. 用于和MR，AR交互的程序
  1. 用户的App


## 提供以下管理接口 ##
|调用方|	描述|
|:--------|:------|
|       |	基础环境安装|
|       |	用户应用的安装|
|       |	向MN注册，告诉MN环境已经准备好了|
|   监控  |sandbox提供的监控信息|


## 调用以下接口 ##
|服务方|	描述|
|:--------|:------|
|MR|	报告自己的状态|

所有的工作为的是解决当面临非常多机器被管理时的问题，希望能达到对系统的傻瓜式维护

基础环境的安装
安装的过程就是复制吗，操作系统是否已经提前安装好了，如果不是网络安装，是否现实：连上网后，自动注册到MR，由MR调度安装
要做到大规模的维护，这个不能少，比如操作系统的升级，也要能直接做掉。

# 应用发布的结构 #
![http://5460.appspot.com/?id=agQ1NDYwcgwLEgVQaG90bxjxAQw&detail=true?nonsense=something_that_ends_with.png](http://5460.appspot.com/?id=agQ1NDYwcgwLEgVQaG90bxjxAQw&detail=true?nonsense=something_that_ends_with.png)

一台机器上运行很多python应用，现在了解到的两种方式

  1. 通过CGI的方式，为每个应用启动一个端口
    * 不用处理URL，每个应用独立端口，容易管理
  1. 不同的应用作为一个应用的模块
    * 对于django需要自己处理url，其他的未知

lighttpd没有每次交互的那个buffer的限制，但nginx对内存的管理也很好，有人把这个buffer设置为128k后，基本可以杜绝一次请求超过1次交互的情况