# HSTD-CAN-PROTO

[English](README.md) | 简体中文

## 简介

这是 HEX-STD CAN HUB 所使用的协议。它用于与 CAN HUB 通信。一般与 WebSocket 一起使用。使用 Google Protocol Buffers 3 编写。

### Protobuf

Protocol Buffers（简称 Protobuf）是由 Google 开发的一种数据序列化协议，类似于 XML 或 JSON，但是更小、更快、更简单。它用于结构化数据的序列化，非常适合高效地进行数据存储或 RPC（远程过程调用）数据交换。

核心特点
- 高效性：Protobuf 设计用于占用极小的传输带宽和存储空间。它的二进制格式使得它比 XML 更小，解析速度也更快。
- 跨平台：Protobuf 支持多种编程语言，包括 C++、Java、Python 等，使得它可以在不同的系统和语言间进行数据交换。
- 可扩展性：Protobuf 设计允许你定义的数据结构可以在不破坏已部署程序的情况下进行修改，你可以添加或删除字段而保持代码的向后兼容性。

Protocol 是一个及其成熟的通信协议，被多个大厂广泛的使用，网上存在大量中英教程，可以轻松的学习。这里不再赘述。

### 示例用途

- rust: [https://github.com/HEXMOVE/hstd-can-proto-rust-example](https://github.com/HEXMOVE/hstd-can-proto-rust-example)

### websocket 数据类型

所有正常数据应使用`binary`发送。`text`消息被视为错误。

### 如何建立连接

1. 发送版本请求以确认对方的版本：（可选，但建议执行）
    1. ProtocolVersion = HexBridgeProtocolRequest，msg = protocol_version_request = true
2. 发送包请求询问：（可选，但建议执行）
    1. 属性 DeviceInfo
    2. 属性 DeviceConfig
3. 确认设备符合使用条件：（可选，但建议执行）
    1. 属性 Request MessageSourceInfo，主要查看您想要打开的通道是否存在，以及是否支持 EXT CAN 和 CAN FD
4. 设置您想要打开的消息源，通常为 SOURCE_EXTERNAL_CAN
    1. MessageSourceConfig 设置启用，波特率，过滤器，终端电阻等。
    2. 注意设置后应读取配置以确认其设置正确。
5. 现在您可以打开通道。这通常是可选的，因为 EXT CAN 默认会被打开。
6. 现在您可以发送和接收消息。

### 接收CAN消息

直接 Protobuf 解码就完了。所有HEX-STD设备都有心跳消息，因此您将始终收到消息。

### 发送CAN消息

为了 ***无痛*** 发送CAN消息，***请仔细阅读*** `hexstd_can_msg.proto` 中的注释。

如果您真特别不愿意读一下，总之：需要设置 `MsgSourceType source`。如果您不设置，消息可能会被丢弃或发送到错误的通道。

### 错误处理

如果您收到一个`文本`消息，虽然建议您关闭连接，但不必这么做。但您确实要记录下来并查看出了什么问题。

如果 `protocol_version` 不兼容，CAN HUB 将关闭连接。
