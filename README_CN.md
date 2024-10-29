# HSTD-CAN-PROTO

[English](README.md) | 简体中文

## 简介

这是 HEX-STD CAN HUB 所使用的协议。它用于与 CAN HUB 通信。一般与 WebSocket 一起使用。

只能发送 `Bridge` 消息类型

### 示例用途

- rust: [https://github.com/HEXMOVE/hstd-can-proto-rust-example](https://github.com/HEXMOVE/hstd-can-proto-rust-example)

### websocket 数据类型

所有正常数据应使用 `binary` 发送。`text` 消息被视为错误。
