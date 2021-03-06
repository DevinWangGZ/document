# 概述
该文档主要用于记录需求包括用例文档，用例图，基本事件流和备选事件流，在开发过程中，在该文档的基础上进行迭代开发，逐步完善该文档中的用例最后完成整个系统功能的开发

# 系统功能需求
## 系统功能架构
![](http://upload-images.jianshu.io/upload_images/2672763-075a3acd8d213972.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 用例1：匹配聊天者
<strong>用例图</strong>:
![](http://upload-images.jianshu.io/upload_images/2672763-b10a1c369ff72c50.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<strong>范围</strong>:系统用例  
<strong>级别</strong>: 用户目标级别  
<strong>用例角色</strong>: 所有访问网站的人  
<strong>用例的简要描述</strong>：该用例主要描述了用户登录到网站进行基本选择到开始聊天之间的过程。  
<strong>涉众及其关注点</strong>:  

* 所有访问网站的人:希望在点击进入聊天的时候，可以快速的进行匹配，开始聊天，而不是等待很久也没有匹配结果；
* 系统服务：希望接收到的格式和协议正确的请求。

<strong>前置条件</strong>：用户按照url和预定的规则进行访问  
<strong>后置条件</strong>：成功完成匹配，开始聊天  
<strong>基本事件流：</strong>

* 用户通过唯一的url访问网站
* 用户选择性别
 * 系统按照用户的性别提供一组昵称，并提示用户选择自己的昵称
* 系统开始对用户进行匹配，采取优先匹配异性的原则
* 匹配成功

<strong>备选事件流:</strong>  

* <p style="color:red">在匹配的任意时刻失败：</p>
  * 服务器端出错
    * 记录错误日志，备份
    * 重启服务器
  * 用户端网络连接不稳定
    * 用户检查自己的网络连接。
    * 网络连接正常后刷新。
  * 用户主动的关闭匹配页面
    * 属于正常退出，无动作。
* <p style="color:red">没有找到当前可以匹配的人:</p>

<strong>用例非功能性需求：</strong>  

* 匹配时间尽量保证在半分钟之内

<strong>用例业务相关数据：</strong>
  * 用户ID
  * 用户名
  * 用户性别



## 用例2:聊天
<strong>用例图</strong>:
![](http://upload-images.jianshu.io/upload_images/2672763-691ab66060993d97.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<strong>范围</strong>:系统用例  
<strong>级别</strong>: 用户目标级别  
<strong>用例角色</strong>: 两个匹配成功的人  
<strong>用例的简要描述</strong>：该用例主要描述了用户开始聊天到结束聊天之间的过程。  
<strong>涉众及其关注点</strong>:  

* 进入聊天的人:在聊天的过程中，希望消息的即时推送，在聊天过程中，如果不是主动提供，并不希望暴露自己的任何个人信息。  
* 系统服务：希望接收到的格式和协议正确的请求。

<strong>前置条件</strong>：系统以对用户匹配成功  
<strong>后置条件</strong>：良好的聊天体验  
<strong>基本事件流：</strong>

1. 用户1发送消息，系统接收到该消息后将该消息显示在用户1的聊天页面和用户2的聊天页面
2. 用户2对用户1发送的消息进行应答，或者用户1继续向用户2发送消息  
用户不断重复1～2步，直到其中一人选择了重新匹配或者返回首页为止
 3. 结束聊天

 <strong>备选事件流:</strong>  

* <p style="color:red">在聊天过程中的任意时刻失败：</p>
  * 服务器端出错
    * 用户双方同时断开连接
    * 记录错误日志，备份
    * 重启服务器
  * 用户端网络连接不稳定
    * 用户双方同时断开连接
    * 用户检查自己的网络连接。
    * 网络连接正常后刷新，重新进入聊天。
  * 某一方主动关闭聊天页面
    * 聊天双方同时退出聊天
* 聊天过程中某一方点击重新匹配:
  * 聊天双方同时断开连接
  * 为点击重新匹配的用户进行重新匹配，不改变用户的昵称
  * 提示另一方连接已断开，并弹窗提供该用户选择重新匹配或者返回首页

* 聊天过程中某一方点击返回首页:
   * 聊天双方同时断开连接
   * 系统清除点击返回首页用户的保留信息并跳转到首页
   * 提示另一方连接已断开，并弹窗提供该用户选择重新匹配或者返回首页

<strong>非功能性需求：</strong>  

* 聊天过程中消息的实时性
* 聊天窗口不宜过大
* <p style="color:red">聊天内容的过滤</p>
<strong>用例业务相关数据：</strong>
  * 用户ID
  * 用户名
  * 聊天消息

## 用例3:热点推送
<strong>用例图</strong>:
![](http://upload-images.jianshu.io/upload_images/2672763-6b736bb081d4a655.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<strong>范围</strong>:系统用例  
<strong>级别</strong>: 用户目标级别  
<strong>用例角色</strong>: 任何处在聊天页面的用户  
<strong>用例的简要描述</strong>：该用例主要描述了用户在聊天过程中对热点推送的点击操作  
<strong>涉众及其关注点</strong>:  

* 处在聊天页面的用户: 显示推送的新闻希望具有时效性；对感兴趣的新闻可以查看原文；有对热度话题的显示；在整个过程中，如果不是主动提供，并不希望暴露自己的任何个人信息；

* 系统服务：希望接收到的格式和协议正确的请求。

<strong>前置条件</strong>：用户处在聊天页面  
<strong>后置条件</strong>：对热点的成功推送  
<strong>基本事件流：</strong>

1. 用户点击感兴趣的推送热点或<span style="color:red">热度话题</span>。
2. 对此次点击进行记录
3. 跳转到显示详情的页面
用户不断重复1～2步，直到不再点击或者退出聊天为止

 <strong>备选事件流:</strong>  

* <p style="color:red">在推送热点的任意时刻失败：</p>
  * 服务器端出错
    * 在页面显示提示信息
    * 记录错误日志，备份
  * 用户端网络连接不稳定
    * 用户断开连接
    * 用户检查自己的网络连接。
    * 网络连接正常后刷新，重新进入聊天。
  * 用户主动关闭聊天页面
    * 正常退出
 * <p style="color:red">跳转受限</p>


<strong>非功能性需求：</strong>  

* 推送新闻的时效性
<strong>用例业务相关数据：</strong>
  * 热点新闻URL
  * 热点新闻Title
  * 热点新闻点击量
