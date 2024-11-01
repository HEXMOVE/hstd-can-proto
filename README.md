# HSTD-CAN-PROTO

English | [简体中文](README_CN.md)

## Intro

This is the protocol for the HEX-STD CAN HUB. It is used to communicate with the CAN HUB.

It is usually used with the WebSocket. 

Only `CanBridgeMessage` message type can be sent.

### Binary vs text

All normal data should be sent using `binary`. `text` messages are considered errors.

### How to use

1. Get/Set can device baudrate, etc.
2. Connect to ws and have fun

#### Setting up by http

For http+ws usage, define a url called `root url`.

For example `root url` can be `10.233.233.1:80`

Each can channel has its own `root url`, for example `10.114.51.4/left-arm-can` and `10.114.51.4/right-arm-can`.

For channel defines refer to user manual.

##### WS address

websocket address should be on `root url`/hex-bridge

##### GET `root url`/info
See `hex_bridge_control.proto`-`Info`

##### GET/POST `root url`/config
See `hex_bridge_control.proto`-`Config`

### Example uses

- rust, http+ws: [https://github.com/HEXMOVE/hstd-can-proto-rust-example](https://github.com/HEXMOVE/hstd-can-proto-rust-example)
