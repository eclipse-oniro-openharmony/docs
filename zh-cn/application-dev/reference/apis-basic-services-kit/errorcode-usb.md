# USB服务错误码

> **说明：**
>
> 以下仅介绍本模块特有错误码，通用错误码请参考[通用错误码说明文档](../errorcode-universal.md)。

## 14400001 连接USB设备被拒绝

**错误信息**

Permission denied. Call requestRight to get the permission first.

**错误描述**

当调用USB模块部分接口时，如果没有相关权限，会报此错误码。

**可能原因**

没有获取到设备的使用权限。

**处理步骤**

调用requestRight方法申请设备的使用权限。

## 14400002 HDC功能被禁用

**错误信息**

Permission denied. The HDC is disabled by the system.

**错误描述**

HDC被系统禁用。

**可能原因**

没有申请USB调试权限。

**处理步骤**

申请USB调试权限。

## 14400003 不支持的端口角色切换

**错误信息**

Unsupported operation. The current device does not support port role switching.

**错误描述**

不支持的操作。当前设备不支持端口角色切换。

**可能原因**

不是正确的端口角色。

**处理步骤**

使用正确的端口角色。

## 14400004 服务异常

**错误信息**

Service exception. Possible causes: No accessory is plugged in.

**错误描述**

服务异常。

**可能原因：**

没有配件插入。

**处理步骤**

插入配件。

## 14400005 数据库操作异常

**错误信息**

Database operation exception.

**错误描述**

数据库操作异常。

**处理步骤**

尝试重新调用接口。

## 14400006 不支持的USB设备侧功能

**错误信息**

Unsupported operation. The function is not supported.

**错误描述**

不支持的操作。当前设备不支持该USB设备侧功能切换。

**可能原因**

不是正确的USB设备侧功能。

**处理步骤**

使用正确的USB设备侧功能。

## 14401001 目标USB配件未匹配

**错误信息**

The target USBAccessory not matched.

**错误描述**

目标USB配件未匹配。

**处理步骤**

通过getAccessoryList获得配件列表，使用匹配的USBAccessory重新操作。

## 14401002 打开配件节点失败

**错误信息**

Failed to open the native accessory node.

**错误描述**

打开配件节点失败。

**处理步骤**

尝试重新调用接口。

## 14401003 不能重复打开配件

**错误信息**

Cannot reopen the accessory.

**错误描述**

不能重复打开配件。

**处理步骤**

配件已被打开，继续执行后续开发操作。

## 14400007 I/O错误

**错误信息**

usb submit transmission input/output error.

**错误描述**

libusb实际读/写/取消，操作失败。

**处理步骤**

尝试重新操作。

## 14400008 参数无效

**错误信息**

transmission invalid parameter.

**错误描述**

libusb识别为无效参数。

**处理步骤**

重新检查传入参数是否正确，设备类型是否正确。

## 14400009 没有设备(连接已断开)

**错误信息**

no such device (it may have been disconnected).

**错误描述**

libusb未识别到正确设备信息。

**处理步骤**

检查设备类型是否正确，检查设备是否已成功连接。

## 14400010 超时

**错误信息**

transmission time out error.

**错误描述**

读/写操作超时。

**处理步骤**

首先检查缓冲区是否已经成功读取/写入数据，如果有数据，则视为成功，如无数据，则操作超时尝试重新操作，或重新设置超时时间。

## 14400011 其他错误

**错误信息**

transmission other error.

**错误描述**

libusb返回为其他错误。例如在某些场景中有可能存在资源繁忙、系统拒绝访问、信号中断等预料之外的错误。

**处理步骤**

查阅设备相关资料，尝试重新操作。

## 14400012 溢出

**错误信息**

transmission overflow error.

**错误描述**

实时传输时部分分包数据丢失。

**处理步骤**

检查参数分包数量与期望读写数据长度的设置，建议单包大小（期望读写数据长度 / 分包数量）设置为8的整数倍，可以减少丢包率，实时传输模式主要用以传输音视频数据，丢包为正常现象。溢出且有实际数据读写，亦可视为成功。

## 14400013 内存不足

**错误信息**

insufficient memory.

**错误描述**

libusb在做内存申请时无内存可用，libusb单次最大传输数据为1kb。

**处理步骤**

及时清理内存。

## 14400014 接口/平台不支持

**错误信息**

interface does not support.

**错误描述**

无法打开libusb接口。

**处理步骤**

检查libusb开关是否打开（使用宏LIBUSB_ENABLE控制），平台是否支持使用libusb。

## 14400015 错误参数

**错误信息**

napi get params error.

**错误描述**

napi参数检查返回错误

**处理步骤**

重新检查传参是否按照接口参数定义正确传参。

