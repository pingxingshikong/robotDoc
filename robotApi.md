### coinMonitor api v1.0


>http://coin.i1314i.com


#### 消息订阅

2) 调用方式：POST

>headers

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|robot-token|鉴权令牌|string|Y|         |


>订阅到的数据
> 
```
{
    "finalFromName":"山山而川",
    "finalFromWxid":"wxid_es7stpo47c5n21",
    "fromName":"搞钱-主",
    "fromWxid":"19061446947@chatroom",
    "msg":"1",
    "msgId":0,
    "msgTime":1675319663,
    "msgType":1,
    "requestId":14288,
    "robotWxid":"wxid_lgxmu46zpkhs12",
    "type":200
}
```

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|finalFromName|消息发送人|string|Y|         |
|finalFromWxid|消息发送人ID|string|Y|         |
|fromName|消息所属群聊/好友名称|string|Y |         |
|fromWxid|消息所属群聊/好友名称|string|Y |         |
|msg|消息内容|string|Y |         |
|msgId|消息ID|int|Y |         |
|msgTime|消息时间|long|Y |         |
|msgType|消息类型|string|Y | 见下表格     |
|requestId|请求ID|long|Y |         |
|robotWxid|机器人ID|string|Y |         |
|type|状态|200|Y |         |

msgType消息类型

|类型ID      |字段说明         |
| -------------|:--------------:|
|1|文本消息|
|3|图片消息|
|34|语音消息|
|42|名片消息|
|43|视频|
|47|动态表情|
|48|地理位置|
|49|分享链接|
|2001|红包|
|2002|小程序|
|2003|群邀请|



#### 获取群聊列表

>/api/wechat/chatroomList

2) 调用方式：GET/POST

>headers

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|robot-token|鉴权令牌|string|Y|         |

>response body

```
{
	"code": "200",
	"msg": "success",
	"data": [
		{
			"memberCount": 5,
			"isManager": 0,
			"robotManagerName": "测试机器人",
			"nickName": "搞钱-主",
			"chatRoomId": "19061446947@chatroom",
			"robotId": "wxid_lgxmu46zpkhs12"
		},
		{
			"memberCount": 3,
			"isManager": 0,
			"robotManagerName": "测试机器人",
			"nickName": "机器人测试群",
			"chatRoomId": "35015657170@chatroom",
			"robotId": "wxid_lgxmu46zpkhs12"
		}
	]
}
```


|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|robotId|机器微信ID|string|Y|         |
|nickName|群聊名称|string|Y|         |
|robotManagerName|配置名称|string|Y |         |
|chatRoomId|群聊ID|string|Y |         |
|memberCount|群聊人数|int|Y |         |
|isManager|机器人是否为群聊管理员|int|Y |         |


#### 获取好友列表

>/api/wechat/friendList

2) 调用方式：GET/POST

>headers

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|robot-token|鉴权令牌|string|Y|         |

>response body

```
{
	"code": "200",
	"msg": "success",
	"data": [
		{
			"note": "山山而川",
			"robotManagerName": "elon musk",
			"nickName": "山山而川",
			"chatFriendId": "wxid_es7stpo47c5n21",
			"wxNumber": "zeqiangq",
			"robotId": "wxid_lgxmu46zpkhs12",
			"headImgUrl": "http://wx.qlogo.cn/mmhead/ver_1/LVn6NMxxljUy5F9WXqwq4YJkk2IdI3MDk6kmeLBxoq55QKcOpnyiawCvTUSTZ1PROTKSaGPeMmphAjvd9icwqFcNUhM5B7kIcibGR3gzfSqibw8/0"
		}
	]
}
```


|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|robotId|机器微信ID|string|Y|         |
|note|微信备注|string|Y|         |
|nickName|微信好友昵称|string|Y|         |
|robotManagerName|配置名称|string|Y |         |
|chatFriendId|好友ID|string|Y |         |
|wxNumber|微信号|string|Y |         |
|headImgUrl|头像链接|string|Y |         |





#### 根据群聊ID/好友ID发送文本消息

2) 调用方式：HTTP POST

>/api/wechat/sendTextMsg


>headers

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|robot-token|鉴权令牌|string|Y|         |
|Content-Type|application/json |string |Y|         |

>request body

```
{
	"robotId":"wxid_lgxmu46zpkhs12",
	"targetChatId": ["19061446947@chatroom","35015657170@chatroom"],
	"message":"text"
}
```

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|robotId|机器微信ID|string|Y|         |
|targetChatId|群聊/好友id数组|string[]|Y|         |
|message|消息|string|Y |         |

>response body

```
{
	"code": "200",
	"msg": "successfully sent message to 2 room and friend"
}
```

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|code          |状态码 100 代表失败 200代表成功 |string  |           |  |


#### 根据群聊ID/好友ID发送图片消息

2) 调用方式：HTTP POST

>/api/wechat/sendPictureMsg


>headers

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|robot-token|鉴权令牌|string|Y|         |
|Content-Type|application/json |string |Y|         |

>request body

```
{
	"robotId":"wxid_lgxmu46zpkhs12",
	"targetChatId": ["19061446947@chatroom","35015657170@chatroom"],
	"pictureUrlList":["https://s2.51cto.com/images/100/blog/index/logonew5.png"]
}
```

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|robotId|机器微信ID|string|Y|         |
|targetChatId|群聊/好友id数组|string[]|Y|         |
|pictureUrlList|图片url列表|string[]|Y |         |

>response body

```
{
	"code": "200",
	"msg": "successfully sent picture to 2 room and friend"
}
```

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|code          |状态码 100 代表失败 200代表成功 |string  |           |  |









#### 根据自定义消息ID发送文本消息

2) 调用方式：HTTP POST

>/api/wechat/sendTextMsgByNoticeId


>headers

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|robot-token|鉴权令牌|string|Y|         |
|Content-Type|application/json |string |Y|         |

>request body

```
{
	"robotId":"wxid_lgxmu46zpkhs12",
	"noticeId":"CoinPriceGet",
	"message":"text"
}
```

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|robotId|机器微信ID|string|Y|         |
|noticeId|自定义消息ID|string|Y|         |
|message|消息|string|Y |         |

>response body

```
{
	"code": "200",
	"msg": "successfully sent message to 1 room and friend"
}
```

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|code          |状态码 100 代表失败 200代表成功 |string  |           |  |


#### 根据自定义消息ID发送图片消息

2) 调用方式：HTTP POST

>/api/wechat/sendPictureMsgByTypeId


>headers

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|robot-token|鉴权令牌|string|Y|         |
|Content-Type|application/json |string |Y|         |

>request body

```
{
	"robotId":"wxid_lgxmu46zpkhs12",
	"noticeId":"CoinPriceGet",
	"pictureUrlList":["https://s2.51cto.com/images/100/blog/index/logonew5.png"]
}
```

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|robotId|机器微信ID|string|Y|         |
|noticeId|自定义消息ID|string|Y|         |
|pictureUrlList|图片url列表|string[]|Y |         |

>response body

```
{
	"code": "200",
	"msg": "successfully sent picture to 1 room and friend"
}
```

|字段名称       |字段说明         |类型            |必填            |备注     |
| -------------|:--------------:|:--------------:|:--------------:| ------:|
|code          |状态码 100 代表失败 200代表成功 |string  |           |  |










#### 注意事项

```
    请确保发送的chatRoomId在token允许列表中,否则消息将不会发送至相应的群聊中
    通过pin发送消息时请确保pin已经配置映射列表
```

