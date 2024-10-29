# HSTD-CAN-PROTO

English | [简体中文](README_CN.md)

## Intro

This is the protocol for the HEX-STD CAN HUB. It is used to communicate with the CAN HUB.

It is usually used with the WebSocket. 

Only `Bridge` message type can be sent.

### Example uses

- rust: [https://github.com/HEXMOVE/hstd-can-proto-rust-example](https://github.com/HEXMOVE/hstd-can-proto-rust-example)

### Binary vs text

All normal data should be sent using `binary`. `text` messages are considered errors.
