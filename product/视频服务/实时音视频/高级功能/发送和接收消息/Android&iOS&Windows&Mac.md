## 内容介绍

TRTC SDK 提供了发送自定义消息的功能，通过该功能，角色为主播的用户都可以向同一个视频房间里的其他用户广播自己的定制消息。

## 支持的平台 

| iOS | Android | Mac OS | Windows | Electron|微信小程序 | Web 端|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|   &#10003;  |   &#10003;   |   &#10003;  |   &#10003;   | &#10003;  |  ×  |   ×  |

>? Web 端和微信小程序端客户，可通过 IM 提供的时通讯来实现。登录IM后发送消息来进行业务逻辑处理，详情请参见 [Web&小程序&uni-app SDK API](https://cloud.tencent.com/document/product/269/37411)。


## 发送接收原理
某一个用户的自定义消息会被夹在音视频数据流中，随着音视频数据一起传输给房间里的其他用户。由于音视频线路本身并不是100%可靠的，为了提高可靠性，TRTC SDK 内部本身实现了一些可靠性保护机制。

![](https://main.qcloudimg.com/raw/1e1802613a22a93d9222fcea94a9fcfd.png)

## 消息发送

通过调用 TRTCCloud 的 `sendCustomCmdMsg` 接口发送的，发送时需要指定四个参数：


| 参数名 | 参数说明 |
|:--------:|:--------------|
| cmdID | 消息ID，取值范围为 1 ~ 10，不同业务类型的消息应当使用不同的 cmdID。 |
| data | 待发送的消息，最大支持 1KB（1000字节）的数据大小。 |
| reliable | 是否可靠发送，可靠发送的代价是会引入一定的延时，因为接收端要暂存一段时间的数据来等待重传。 |
| ordered | 是否要求有序，即是否要求接收端接收的数据顺序和发送端发送的顺序一致，这会带来一定的接收延时，因为在接收端需要暂存并排序这些消息。 |

>!请将 reliable 和 ordered 同时设置为 YES 或 NO, 暂不支持交叉设置。

<dx-codeblock>
::: Objective-C ObjectiveC
//发送自定义消息的示例代码
- (void)sendHello {
    // 自定义消息命令字, 这里需要根据业务定制一套规则，这里以0x1代表发送文字广播消息为例
    NSInteger cmdID = 0x1;
    NSData *data = [@"Hello" dataUsingEncoding:NSUTF8StringEncoding];
    // reliable 和 ordered 目前需要一致，这里以需要保证消息按发送顺序到达为例
    [trtcCloud sendCustomCmdMsg:cmdID data:data reliable:YES ordered:YES];
}
:::
::: Java Java
//发送自定义消息的示例代码
public void sendHello() {
    try {
        // 自定义消息命令字, 这里需要根据业务定制一套规则，这里以0x1代表发送文字广播消息为例
        int cmdID = 0x1;
        String hello = "Hello";
        byte[] data = hello.getBytes("UTF-8");
        // reliable 和 ordered 目前需要一致，这里以需要保证消息按发送顺序到达为例
        trtcCloud.sendCustomCmdMsg(cmdID, data, true, true);
				
    } catch (UnsupportedEncodingException e) {
        e.printStackTrace();
    }
}
:::
::: C++ C++
// 发送自定义消息的示例代码
void sendHello()
{
    // 自定义消息命令字, 这里需要根据业务定制一套规则，这里以0x1代表发送文字广播消息为例

    uint32_t cmdID = 0x1;
    uint8_t* data = { '1', '2', '3' };
    uint32_t dataSize = 3;  // data的长度

    // reliable 和 ordered 目前需要一致，这里以需要保证消息按发送顺序到达为例
    trtcCloud->sendCustomCmdMsg(cmdID, data, dataSize, true, true);
}
:::
::: C# C#
// 发送自定义消息的示例代码
private void sendHello()
{
    // 自定义消息命令字, 这里需要根据业务定制一套规则，这里以0x1代表发送文字广播消息为例

    uint cmdID = 0x1;
    byte[] data = { '1', '2', '3' };
    uint dataSize = 3;  // data的长度

    // reliable 和 ordered 目前需要一致，这里以需要保证消息按发送顺序到达为例
    mTRTCCloud.sendCustomCmdMsg(cmdID, data, dataSize, true, true);
}
:::
</dx-codeblock>


## 消息接收

当房间中的一个用户通过 `sendCustomCmdMsg` 发出自定义消息后，房间中其他的用户可以通过 SDK 回调中的 `onRecvCustomCmdMsg` 接口来接收这些消息。


<dx-codeblock>
::: Objective-C ObjectiveC
//接收和处理房间内其他人发送的消息
- (void)onRecvCustomCmdMsgUserId:(NSString *)userId cmdID:(NSInteger)cmdId seq:(UInt32)seq message:(NSData *)message
{
	// 接收到 userId 发送的消息
    switch (cmdId)  // 发送方和接收方协商好的cmdId
    {
    case 0:
        // 处理cmdId = 0消息
        break;
    case 1:
        // 处理cmdId = 1消息
        break;
    case 2:
        // 处理cmdId = 2消息
        break;
    default:
        break;
    }
}
:::
::: Java Java
//继承 TRTCCloudListener，实现 onRecvCustomCmdMsg 方法接收和处理房间内其他人发送的消息
public void onRecvCustomCmdMsg(String userId, int cmdId, int seq, byte[] message) {
	// 接收到 userId 发送的消息
    switch (cmdId)  // 发送方和接收方协商好的cmdId
    {
    case 0:
        // 处理cmdId = 0消息
        break;
    case 1:
        // 处理cmdId = 1消息
        break;
    case 2:
        // 处理cmdId = 2消息
        break;
    default:
        break;
    
}
:::
::: C++ C++
// 接收和处理房间内其他人发送的消息
void TRTCCloudCallbackImpl::onRecvCustomCmdMsg(
                            const char* userId, int32_t cmdId, uint32_t seq, const uint8_t* msg, uint32_t msgSize)
{
    // 接收到 userId 发送的消息
    switch (cmdId)  // 发送方和接收方协商好的cmdId
    {
    case 0:
        // 处理cmdId = 0消息
        break;
    case 1:
        // 处理cmdId = 1消息
        break;
    case 2:
        // 处理cmdId = 2消息
        break;
    default:
        break;
    }
}
:::
::: C# C#
// 接收和处理房间内其他人发送的消息
public void onRecvCustomCmdMsg(string userId, int cmdId, uint seq, byte[] msg, uint msgSize)
{
    // 接收到 userId 发送的消息
    switch (cmdId)  // 发送方和接收方协商好的cmdId
    {
    case 0:
        // 处理cmdId = 0消息
        break;
    case 1:
        // 处理cmdId = 1消息
        break;
    case 2:
        // 处理cmdId = 2消息
        break;
    default:
        break;
    }
}
:::
</dx-codeblock>

## 使用限制

由于自定义消息享受比音视频数据更高的传输优先级，如果自定义数据发送过多，音视频数据可能会被干扰到，从而导致画面卡顿或者模糊。所以，我们针对自定义消息的发送进行了如下的频率限制：

- 自定义消息会被云广播给房间内所有用户，所以每秒最多能发送 30 条消息。
- 每个消息包（即 data 的大小）最大为 1 KB，超过则很有可能会被中间路由器或者服务器丢弃。
- 每个客户端每秒最多能发送总计 8 KB 数据，也就是如果每个数据包都是 1KB，那么每秒钟您最多只能发送 8 个数据包。








