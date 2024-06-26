# Proto 文件定义

## Websocket 约定

### Binary 与 text

正常数据全部使用 `binary` 发送, `text` 都发送 Error。

### 建立连接流程

1. 发送包问询：
   1. Property DeviceInfo
   2. Property DeviceConfig
2. 确认设备符合使用条件
   1. Property Request MessageSourceInfo，主要看想要打开的 channel 是否存在，是否支持 EXT CAN 与 CAN FD
3. 设置需要开启的 Message Source，一般是 SOURCE_EXTERNAL_CAN
   1. MessageSourceConfig 设置 使能，波特率，过滤器，终端电阻等

### 严重错误处理流程

1. 版本头不兼容
   1. 使用 `Text` 通道返回错误并 **关闭连接**
