# 文字频道API


## 发送消息

SetChannelMessageSend

#### 接口

|地址|版本|方式|权限|
|:-----|:---------------|:-----|:---------------|
|`/api/v2/channel/message/send`|<Badge type="warning" text="v2" vertical="middle" />|POST|通用权限-查看频道、文字频道-发送消息|

#### 描述

用于向指定频道发送频道消息 / 频道私信

:::tip
按频道限制，60次/30秒

该群已被限制发言频率处罚时，1分钟内仅可发送1条消息
:::

#### 入参

|字段|类型|必传|说明|
|:---------------|:-----|:-----|:---------------|
|channelId|string|是|频道ID|
|messageType|int|是|消息类型，1：文字消息，2：图片消息，3：视频消息，6：卡片消息|
|messageBody|object|是|[消息内容](./message.md#消息内容)|
|referencedMessageId|string|否|回复消息ID|
|dodoSourceId|string|否|DoDoID，非必传，如果传了，则给该成员发送频道私信|

#### 出参

|字段|类型|说明|
|:---------------|:-----|:---------------|
|status|int|[返回码](../start/status.md)|
|message|string|返回信息|
|data|object|返回数据|

#### 数据

|字段|类型|说明|
|:---------------|:-----|:---------------|
|messageId|string|消息ID，如入参传了DoDoID，则返回频道私信消息ID|

#### 入参示例

<CodeGroup>
  <CodeGroupItem title="1 - 文字消息" active>

```json
{
    "channelId": "1000101",
    "messageType": 1,
    "messageBody": {
        "content": "发送文字消息"
    }
}
```

  </CodeGroupItem>

 <CodeGroupItem title="2 - 图片消息">

```json
{
    "channelId": "1000101",
    "messageType": 2,
    "messageBody": {
        "url": "https://img.imdodo.com/dodo/8c77d48865bf547a69fb3bba6228760c.png",
        "width": 500,
        "height": 500,
        "isOriginal": 1
    }
}
```

  </CodeGroupItem>

   <CodeGroupItem title="3 - 视频消息">

```json
{
    "channelId": "1000101",
    "messageType": 3,
    "messageBody": {
        "url": "https://video.imdodo.com/dodo/ff85c752daf7d67884cb9ad3921a5d01.mp4",
        "coverUrl": "https://img.imdodo.com/dodo/8c77d48865bf547a69fb3bba6228760c.png",
        "duration": 100,
        "size": 100
    }
}
```

  </CodeGroupItem>

   <CodeGroupItem title="6 - 卡片消息">

```json
{
    "channelId": "1000101",
    "messageType": 6,
    "messageBody": {
        "content": "附加文本",
        "card": {
            "type": "card",
            "theme": "grey",
            "title": "发送卡片消息",
            "components": [{
                    "type": "section",
                    "text": {
                        "type": "dodo-md",
                        "content": "卡片文本内容"
                    }
                }
            ]
        }
    }
}
```

  </CodeGroupItem>

</CodeGroup>

#### 出参示例

```json
{
    "status": 0,
    "message": "success",
    "data": {
        "messageId": "111111111111111111"
    }
}
```


## 编辑消息

SetChannelMessageEdit

#### 接口

|地址|版本|方式|权限|
|:-----|:---------------|:-----|:---------------|
|`/api/v2/channel/message/edit`|<Badge type="warning" text="v2" vertical="middle" />|POST|通用权限-查看频道、文字频道-发送消息|

#### 描述

用于编辑指定消息ID的频道消息

:::tip
不可编辑频道私信，不可变更消息类型

按频道限制，1次/秒

该群已被限制发言频率处罚时，1分钟内仅可编辑1条消息
:::

#### 入参

|字段|类型|必传|说明|
|:---------------|:-----|:-----|:---------------|
|messageId|string|是|待编辑的消息ID，不可编辑频道私信，不可变更消息类型|
|messageBody|object|是|[消息内容](./message.md#消息内容)|

#### 出参

|字段|类型|说明|
|:---------------|:-----|:---------------|
|status|int|[返回码](../start/status.md)|
|message|string|返回信息|

#### 入参示例

<CodeGroup>
  <CodeGroupItem title="文字消息" active>

```json
{
    "messageId": "111111111111111111",
    "messageBody": {
        "content": "编辑文字消息"
    }
}
```

  </CodeGroupItem>

   <CodeGroupItem title="卡片消息">

```json
{
    "messageId": "111111111111111111",
    "messageBody": {
        "content": "附加文本2",
        "card": {
            "type": "card",
            "theme": "grey",
            "title": "编辑卡片消息",
            "components": [{
                    "type": "section",
                    "text": {
                        "type": "dodo-md",
                        "content": "卡片文本内容2"
                    }
                }
            ]
        }
    }
}
```

  </CodeGroupItem>

</CodeGroup>

#### 出参示例

```json
{
    "status": 0,
    "message": "success"
}
```


## 撤回消息

SetChannelMessageWithdraw

#### 接口

|地址|版本|方式|权限|
|:-----|:---------------|:-----|:---------------|
|`/api/v2/channel/message/withdraw`|<Badge type="warning" text="v2" vertical="middle" />|POST|通用权限-查看频道、文字频道-管理消息|

#### 描述

用于撤回指定消息ID的频道消息

:::tip
不可撤回频道私信
:::

#### 入参

|字段|类型|必传|说明|
|:---------------|:-----|:-----|:---------------|
|messageId|string|是|消息ID，不可撤回频道私信|
|reason|string|否|撤回理由，理由不能大于64个字符或32个汉字|

#### 出参

|字段|类型|说明|
|:---------------|:-----|:---------------|
|status|int|[返回码](../start/status.md)|
|message|string|返回信息|

#### 入参示例

```json
{
    "messageId": "111111111111111111",
    "reason": "撤回测试"
}
```

#### 出参示例
 
```json
{
    "status": 0,
    "message": "success"
}
```


## 添加表情反应

SetChannelMessageReactionAdd

#### 接口

|地址|版本|方式|权限|
|:-----|:---------------|:-----|:---------------|
|`/api/v2/channel/message/reaction/add`|<Badge type="warning" text="v2" vertical="middle" />|POST|通用权限-查看频道、文字频道-添加新反应|

#### 描述

用于操作机器人在自身的频道消息上添加指定反应表情

:::tip
按频道限制，60次/30秒
:::

#### 入参

|字段|类型|必传|说明|
|:---------------|:-----|:-----|:---------------|
|messageId|string|是|消息ID|
|emoji|object|是|[反应表情](./message.md#消息表情)|

#### 出参

|字段|类型|说明|
|:---------------|:-----|:---------------|
|status|int|[返回码](../start/status.md)|
|message|string|返回信息|

#### 入参示例

```json
{
    "messageId": "111111111111111111",
    "emoji": {
        "type": 1,
        "id": "128516"
    }
}
```

#### 出参示例
 
```json
{
    "status": 0,
    "message": "success"
}
```


## 取消表情反应

SetChannelMessageReactionRemove

#### 接口

|地址|版本|方式|权限|
|:-----|:---------------|:-----|:---------------|
|`/api/v2/channel/message/reaction/remove`|<Badge type="warning" text="v2" vertical="middle" />|POST|通用权限-查看频道、文字频道-管理消息|

#### 描述

用于操作机器人在自身的频道消息上移除指定反应表情

:::tip
既可以移除机器人自身的反应表情，也可以移除其他成员的反应表情

按频道限制，60次/30秒
:::

#### 入参

|字段|类型|必传|说明|
|:---------------|:-----|:-----|:---------------|
|messageId|string|是|消息ID|
|emoji|object|是|[反应表情](./message.md#消息表情)|
|dodoSourceId|string|否|DoDoID，不传或传空时表示移除机器人自身的反应|

#### 出参

|字段|类型|说明|
|:---------------|:-----|:---------------|
|status|int|[返回码](../start/status.md)|
|message|string|返回信息|

#### 入参示例

```json
{
    "messageId": "111111111111111111",
    "emoji": {
        "type": 1,
        "id": "128516"
    },
    "dodoSourceId": "666666"
}
```

#### 出参示例
 
```json
{
    "status": 0,
    "message": "success"
}
```