# ServiceChat 客服聊天

## 介绍

ServiceChat 是一套运行在 node.js 的客服聊天网页，包括客户端和客服端，放在 node 的初衷也是为了方便学习前端的人更加容易上手，整个项目功能丰富，但可维护性差了写，因为所以的功能和页面都怼在了一个页面，这也算是当初做的比较急的原因吧，但完全不担心使用问题，如果你不满意这种写法可自行抽取封装，感谢支持！

## 功能一览

- 机器人智能聊天
- 客服手动在线离线
- 用户主动向客服发送信息（信息包括文本、表情包）
- 客服选择会话成员，并且主动向用户发送信息（信息包括文本、表情包）
- 用户/客服接收到对方发送的信息
- 客服主动关闭用户会话，离线列表显示离线用户，用户端提示客服主动关闭会话，本次会话结束
- 客服手动离线，清除所有会话列表，用户端提示客服已离线，本次会话结束
- 客服刷新或关闭页面下线，清除所有会话列表，用户端提示客服已离线，本次会话结束
- 用户刷新页面或关闭页面，客服端提示用户已下线，本次会话结束
- 客服切换右边工具栏，选择快捷回复，可选中快捷回复信息以此快速回复内容
- 发送信息，如果服务器中断，信息状态为 0（未发送出），若 20 秒服务器仍为断开，信息状态改成-1（发送失败），若 20 秒内服务器恢复，信息状态改成 1（发送成功）
- 在用户端加入 productId，用户可发送商品卡片
- 客服接收用户发送的商品卡片，并且查看详情
- 完成图片发送，若图片过大时进行图片压缩，图片超大时不允许发送
- 完成图片接收，查看
- 用户多台设备在线时，强制另一台设备下线
- 客服多台设备在线时，强制旧客服端下线，并且中断会员的会话


## 效果图

用户端进入客服界面：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210103085849794.gif#pic_center)
注意：因为需要实现转人工的功能，所有访问时是带来参数的，即地址中的 sendId，目的是为了获取该用户的信息，除此之外，需要注意的是，用户端采用的是手机端，所以需要你在浏览器中 f12，把手机的模拟器亮起来
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210103093823151.jpg#pic_center)
用户转人工：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210103090536395.gif#pic_center)
发送消息（包括文字、图片、表情包）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210103091327169.gif#pic_center)
客服快捷回复功能
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210103091627106.gif#pic_center)
用户下线或客服下线通知
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210103092109974.gif#pic_center)
发送卡片功能
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210103092446352.gif#pic_center)
注意：此时为了模拟浏览的商品，地址参数多了 productId

功能演示暂时先上这些，还有许多的功能等着小伙伴们去探索，应该有人开始疑惑，上面演示的 sendId 和 productId 如何匹配上对应的用户和商品信息呢，其实我是提前放在后端的 json 数组里了，目的是模拟数据库中的数据，除此之外，还有快捷回复、用户留言、机器人回复的 json 信息

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210103093054564.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjAwMDgxNg==,size_16,color_FFFFFF,t_70#pic_center)
接下来，说下项目 clone 下来后，需要完成那些事情才能把项目跑起来

## 安装依赖

- 后端依次输入以下命令：

```javascript
cd service
npm install
node app.js
```

- 前端依次输入以下命令：

```javascript
cd chatroom
npm install
npm run serve
```

## 浏览器运行

- 用户端打开：http://localhost:8080/?sendId=3
- 客服端打开：http://localhost:8080/?sendId=1
- 若需要发送卡片功能，用户端打开：http://localhost:8080/?sendId=3&productId=300
- 具体参数对应的信息，可查看 userList.json 和 product.json 文件

到现在就已经是大功告成，客服项目的最终效果就展示出来了

## 参数说明

### data 数据

| 字段               | 类型      | 描述                     |
| ------------------ | --------- | ------------------------ |
| socket             | Object    | socket 对象              |
| sender             | Object    | 发送者对象               |
| revicer            | Object    | 接收者对象               |
| infoTemplate       | Object    | 信息模板                 |
| productDetail      | Object    | 商品详细信息             |
| browseCard         | Object    | 卡片信息内容             |
| msgTimer           | Object    | 信息发送定时器           |
| windowHeight       | Integer   | 窗口高度                 |
| chatContentHeight  | Integer   | 聊天内容高度             |
| floatBottomHeight  | Integer   | 输入框底部高度           |
| scrollTop          | Integer   | 滚动条位置高度           |
| level              | Integer   | 客服评分等级             |
| solveResult        | Integer   | 是否解决问题             |
| currentEasy        | Integer   | 当前快捷回复树状图 Id    |
| pageIndex          | Integer   | 当前聊天内容页数         |
| pageSize           | Integer   | 当前聊天内容一页的条数   |
| current_state      | Integer   | 当前工具栏 Id            |
| customerMessage    | String    | 客服留言内容             |
| thisQuestion       | String    | 本次问题                 |
| sendInfo           | String    | 发送的聊天内容           |
| abutmentUrl        | String    | 工具栏对接页面的 url     |
| customerImg        | String    | 用户头像                 |
| serviceImg         | String    | 客服头像                 |
| messageTip         | String    | 提示内容                 |
| noCode             | Timestamp | 每次进入客服功能的时间戳 |
| isSelectSession    | Boolean   | 是否选中会话             |
| expressionShow     | Boolean   | 是否显示表情             |
| lastSession        | Boolean   | 是否为全部会话内容       |
| sendState          | Boolean   | 是否可以发送             |
| openImitateProduct | Boolean   | 是否开启虚拟商品         |
| conversition       | Array     | 当前用户会话内容         |
| expressions        | Array     | 表情列表                 |
| serviceTool        | Array     | 客服工具栏列表           |
| fastReplay         | Array     | 快捷回复内容             |
| imageList          | Array     | 聊天内容图片列表         |
| start              | Array     | 评星列表                 |

### infoTemplate 数据

| 字段          | 类型      | 描述                                                                 |
| ------------- | --------- | -------------------------------------------------------------------- |
| SendId        | Integer   | 发送者 Id                                                            |
| ReviceId      | Integer   | 接收者 Id                                                            |
| Content       | String    | 发送内容                                                             |
| Identity      | Integer   | 发送者身份：0 机器人，1 客服员，2.会员                               |
| Type          | Integer   | 信息类型 ：0 文本，1 图片，2 表情，3 商品卡片/订单卡片，4 机器人回复 |
| State         | Integer   | 信息发送状态                                                         |
| NoCode        | Timestamp | 发送者时间戳                                                         |
| OutTradeNo    | String    | 发送者 socketId                                                      |
| CreateDateUtc | String    | 发送信息时间                                                         |
| Title         | String    | 推送卡片-标题                                                        |
| Description   | String    | 推送卡片-描述                                                        |
| Label         | String    | 推送卡片-标签                                                        |
| Thumbnail     | String    | 推送卡片-图片                                                        |
| NoSend        | Boolean   | 卡片标题                                                             |

### sender、revicer 数据

| 字段        | 类型    | 描述          |
| ----------- | ------- | ------------- |
| id          | Integer | Id            |
| isService   | Integer | 是否客服      |
| name        | String  | 名称          |
| onlineState | Boolean | 在线状态      |
| outTradeNo  | Integer | 用户 socketId |
| source      | Integer | 来源          |
| mobile      | String  | 手机号        |
| nickName    | String  | 昵称          |
| cardNo      | String  | 卡号          |
| receptNum   | Integer | 接待用户数量  |

## 简略说明

- 后端处理：
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210103094833522.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjAwMDgxNg==,size_16,color_FFFFFF,t_70#pic_center)
- 前端：

  Chat.vue 是核心文件，需要看懂的话需要一些时间，html 和 css 样式虽然有点多，但这些相信你有基础的话还是不难理解的，其中有点难度的可能是 js 的处理逻辑，qq:3332673880

## 后言

该项目前身其实是我用 C#的 signalr 框架完成的，因为涉及到其他语言，对很多前端学习者来说是不太友好，所以我在想怎么才能把它转移到前端来给更多的前端爱好者来学习，于是花了许多时间将旧项目抽取、改进、完善才有了现在的最终效果，其中 node 涉及到的并不多，也就是简单的 js 而已，大家上手更容易，最后附上我学习中时参考的 socket 手册：[socket.io 中文手册](https://www.w3cschool.cn/socket/)
