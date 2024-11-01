# HSTD-CAN-PROTO

[English](README.md) | 简体中文

## 简介

这是HEX-STD CAN HUB的通信协议。用于与CAN HUB进行通信。

通常与WebSocket一起使用。

只能发送`CanBridgeMessage`消息类型。

### 二进制与文本

所有正常数据应使用`binary`发送。`text`消息被视为错误。

### 使用方法

1. 获取/设置CAN设备波特率等。
2. 连接到ws并享受乐趣

#### 通过http设置

对于http+ws的使用，请定义一个称为`root url`的网址。

例如`root url`可以是`10.233.233.1:80`

每个can通道都有自己的`root url`，例如`10.114.51.4/left-arm-can`和`10.114.51.4/right-arm-can`。

关于通道定义，请参阅用户手册。

##### WS address

websocket 地址应为 `root url`/hex-bridge

##### GET `root url`/info
参见`hex_bridge_control.proto`-`Info`

##### GET/POST `root url`/config
参见`hex_bridge_control.proto`-`Config`

### 示例用途

- rust, http+ws: [https://github.com/HEXMOVE/hstd-can-proto-rust-example](https://github.com/HEXMOVE/hstd-can-proto-rust-example)
