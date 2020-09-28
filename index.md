# Traceless.OPQ
OPQ C# SDK 【netcore 3.1】

这里是Netcore 3.1 OPQ C# SDK

![.NET Core](https://github.com/traceless0929/Traceless.OPQ/workflows/.NET%20Core/badge.svg)

![Nuget](https://github.com/traceless0929/Traceless.OPQ/workflows/Nuget/badge.svg)

[WIKI点击进入](https://github.com/OPQBOT/OPQ/wiki)

我的测试环境：**Linux centos 3.10.0-1127.el7.x86_64**



Nuget

```powershell
//SDK模块
Install-Package Traceless.OPQSDK -Version 0.0.16
```



#### 开发【直接使用本库】

1. clone本库
2. 复制Traceless.Robot.Plugins.MyPlugin并更改插件名，修改插件信息
3. 在事件中完成逻辑开发
4. 完成

#### 开发【使用Nuget】
1. 新建项目
2. Nuget引用Traceless.OPQSDK
3. 在程序某处添加代码  **await OPQSDK.Plugin.OPQMain.Client();**
4. 创建<项目命名空间>.Plugins.<你的插件Class名称>,并使用**OPQSDK.Plugin.BasePlugin**作为基类，如[MyPlugin](https://github.com/traceless0929/Traceless.OPQ/blob/master/Traceless.Robot/Plugins/MyPlugin.cs)

5. 在事件中完成逻辑开发

6. 完成

#### 使用

1. 配置App.config，设置OPQ地址及机器人QQ【你也可以直接修改运行目录下的<程序集名称>.config文件】
2. 编译【自己选择平台，理论上netcore支持的平台，SDK也都支持（艹那不是全平台了么）】
3. 发布【发布到对应机器上】
4. 启动【启动对应平台文件 win可直接支持exe，linux需安装dotnet环境 使用dotnet命令启动，当然如果带着依赖的独立包的话，就不需要dotnet环境了】

## TODO

1. 更优雅的接口调用
2. ......

## 已完成

5. 重构basePlugin，不再使用反射调用事件方法 ✔
6. 增加OPQ码机制，功能类似酷Q码 ✔
7. 修复了获取群列表和群成员列表出现的NPE问题 ✔
8. 增加发送消息接口延迟等待机制，减少调用发送接口过于频繁产生消息丢失的可能性 ✔
9. 增加腾讯AI平台-智能闲聊\语音合成 接口 ✔

#### 项目结构

Traceless.OPQSDK：SDK本体，不做二次开发无需修改，SDK更新替换即可

Traceless.SocketIO：基于Websocket4Net的Socket.io实现【用于连接socket接收事件】

Traceless.Utils：一些工具方法

1. 高效、自带并发控制、内存控制等netcore自带HttpclientFactory的控制台使用实现
2. 腾讯AI开放平台-智能闲聊及语音合成（AILab）实现
3. 随机工具类

Traceless.Robot：SDK宿主程序，本DEMO实用Netcore控制台程序，你也可以使用任何程序作为宿主程序



##### Api支持备注

涉及支付、转账的接口不对接，如 转账\获取钱包余额\发红包 等

##### Api支持【持续更新中】

| API                  | 可用 | 测试过 | 备注                                                         |
| --------------------- | ---- | ------ | ------------------------------------------------------------ |
| 发群消息【图片、语音、文字】                | ✔    | ✔      | 可能不会支持xml等，可自行根据webapi拓展 |
| 发好友消息【图片、语音、文字】                | ✔    | ✔      | 可能不会支持xml等，可自行根据webapi拓展 |
| 群组管理 | ✔ | ✔ | 加群 拉人 踢群 退群 |
| 添加好友 | ✔ | ✔ |                                                              |
| 获取好友列表 | ✔ | ✔ |                                                              |
| 获取群组列表 | ✔ | ✔ |                                                              |
| 撤回消息 | ✔ | ✔ |                                                              |
| 搜索群组 | ✔ | ✔ |                                                              |
| 群成员列表 | ✔ | ✔ | |
| QQ资料卡点赞 | ✔ | ✔ | |
| 获取QQ相关ck | ✔ | ✔ | |
| 处理好友请求 | ✔ | ✔ | |
| 处理群邀请 | ✔ | ✔ | |
| 修改群名片 | ✔ | ✔ |  |
| 设置头衔 | ✔ | ✔ | |
| 发送群公告 | ✔ | ✔ | |
| 获取任意用户信息昵称头像等 | ✔ | ✔ | |
| 全员禁言开启/关闭 | ✔ | ✔ | |
| 禁言某人 | ✔ | ✔ | |

##### 三方Api支持【持续更新中】

| API                  | 可用 | 测试过 | 备注                                                         |
| --------------------- | ---- | ------ | ------------------------------------------------------------ |
| 获取插件数据根目录                | ✔    | ✔      |  |
|                 |     |       |  |


##### 事件支持【理论上全都可用，欢迎提交Issue帮我完成测试】

| 事件                  | 可用 | 测试过 | 备注                                                         |
| --------------------- | ---- | ------ | ------------------------------------------------------------ |
| 群消息                | ✔    | ✔      |                                                              |
| 私聊消息              | ✔    | ✔      |                                                              |
| QQ登陆成功事件        | ✔    | ✖      |                                                              |
| 网络变化事件          | ✔    | ✖      | 网络波动引起当前链接 释放 随机8-15s会自动重连登陆 被t下线的QQ 不会在重连 |
| QQ离线事件            | ✔    | ✖      | 可能的原因(TX 踢号/异地登陆/冻结/被举报等 导致等Session失效) |
| 加好友申请被同意/拒绝 | ✔    | ✔      |                                                              |
| 主动删除了好友        | ✔    | ✔      |                                                              |
| 加好友成功后的通知    | ✔    | ✔      |                                                              |
| 收到好友请求          | ✔    | ✔      |                                                              |
| 退群成功              | ✔    | ✔      |                                                              |
| 好友消息撤回          | ✔    | ✔      |                                                              |
| 群禁言                | ✔    | ✔      |                                                              |
| 群撤回                | ✔    | ✔      |                                                              |
| 群头衔变更            | ✔    | ✔      |                                                              |
| 加群请求              | ✔    | ✔      |                                                              |
| 群管理变更            | ✔    | ✔      | 机器人是不是管理员都能收到此群管变更事件                     |
| 有人退群              | ✔    | ✔      | 无论机器人是不是管理员 群里任意成员 都能收到 此退群事件      |
| 加群成功              | ✔    | ✔      |                                                              |
| 收到群邀请            | ✔    | ✔      |                                                              |
|                       |      |        |                                                              |
|                       |      |        |                                                              |
|                       |      |        |                                                              |
|                       |      |        |                                                              |
|                       |      |        |                                                              |
|                       |      |        |                                                              |
|                       |      |        |                                                              |



##### OPQ码

| 类型     | 格式                       | 说明                 | 是否OPQ自带 | 备注                                                     |
| -------- | -------------------------- | -------------------- | ----------- | -------------------------------------------------------- |
| AT人     | [ATUSER(QQ号)]             | AT某个人             | ✔           |                                                          |
| AT全体   | [ATALL()]                  | AT全体               | ✔           |                                                          |
| 获取昵称 | [GETUSERNICK(QQ号)]        | 获取某个人的QQ昵称   | ✔           |                                                          |
| 网络图片 | [CODE:pic,url=网络图片URL] | 表示发送某张网络图片 | ✖           | 网络图片需要带https/http标头                             |
| 语音     | CODE:voice,url=语音URL]    | 表示发送某段语音     | ✖           | 语音URL为OPQ语音消息返回体中的url，暂不支持自定义网络url |
| 富文本分享卡片     | [CODE:rich,url=跳转地址,title=标题,desc=描述,prompt=在聊天列表里的缩略信息,preview=缩略图,tag=左角标的说明]    | 表示发送具有点击跳转功能的卡片     | ✖           | 地址\缩略图 需要http(s)地址 |


参考项目：

[C# 插件 By:枫林](https://github.com/fenglindubu/IOTQQ_Socket)

[仓鼠的QQ Bot框架-Java版本](https://github.com/MiniDay/HamsterBot-IOTQQ)