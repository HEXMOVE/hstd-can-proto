# HSTD-CAN-PROTO

### Example uses

- rust: [https://github.com/HEXMOVE/hstd-can-proto-rust-example](https://github.com/HEXMOVE/hstd-can-proto-rust-example)

### Binary vs text

All normal data should be sent using `binary`. `text` messages are considered errors.

### How to establish a connection

1. Send a version request to confirm the version of the other side: (Optional, but you would want to do it)
   1. ProtocolVersion = HexBridgeProtocolRequest, msg = protocol_version_request = true
2. Send a package request asking for: (Optional, but you would want to do it)
   1. Property DeviceInfo
   2. Property DeviceConfig
3. Confirm that the device meets the conditions for use: (Optional, but you would want to do it)
   1. Property Request MessageSourceInfo, mainly to see if the channel you want to open exists, and whether it supports EXT CAN and CAN FD
4. Set the Message Source you want to open, usually SOURCE_EXTERNAL_CAN
   1. MessageSourceConfig set enable, baud rate, filter, terminal resistance, etc.
   2. Note that you should read the config after setting it to confirm that it set to the correct value.
5. You can now open the channel. This is usually optional because EXT CAN will be opened by default.
6. You can now send and receive messages.

### Receiving a CAN message

Just decode the message. All HEX-STD devices has heartbeat messages, so you will always receive messages.

### Sending a CAN message

To send a CAN message without suffering, ***please read*** the comments in `hexstd_can_msg.proto` carefully.

If you really just TL;DR: It is required to set `MsgSourceType source`. If you don't set it, the message might be dropped or sent to the wrong channel.

### Error handling

If you receive a `Text` message, you don't have to close the connection though it is recommended. But you do really want to log it and see what's wrong.

The CAN HUB will close the connection if the `protocol_version` is not compatible.
