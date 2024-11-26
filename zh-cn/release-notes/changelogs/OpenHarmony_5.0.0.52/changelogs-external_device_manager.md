# 驱动子系统扩展外设管理模块Changelog
## cl.usbddk.1 USB_DDK/HID_DDK错误码定义变更

**访问级别**

公开接口。

**变更原因**

优化开发体验，规范错误码格式。

**变更影响**

该变更为不兼容变更。

**USB错误码**

| 变更前 | 变更后 |
| ------ | ------ |
| USB_DDK_SUCCESS = 0 | 未变更 |
| USB_DDK_FAILED = -1 | 废弃 |
| USB_DDK_INVALID_PARAMETER = -2 | USB_DDK_INVALID_PARAMETER = 401 |
| USB_DDK_MEMORY_ERROR = -3 | USB_DDK_MEMORY_ERROR = 27400001 |
| USB_DDK_INVALID_OPERATION = -4 | USB_DDK_INVALID_OPERATION = 27400002 |
| USB_DDK_NULL_PTR = -5 | 废弃 |
| USB_DDK_DEVICE_BUSY = -6 | 废弃 |
| USB_DDK_TIMEOUT = -7 | USB_DDK_TIMEOUT = 27400004 |
| USB_DDK_NO_PERM = 201 | 新增 |
| USB_DDK_IO_FAILED = 27400003 | 新增 |

**HID错误码**

| 变更前 | 变更后 |
| ------ | ------ |
| HID_DDK_SUCCESS = 0 | 未变更 |
| HID_DDK_NO_PERM = -6 | HID_DDK_NO_PERM = 201 |
| HID_DDK_INVALID_PARAMETER = -2 | HID_DDK_INVALID_PARAMETER = 401 |
| HID_DDK_FAILURE = -1 | HID_DDK_FAILURE = 27300001 |
| HID_DDK_NULL_PTR = -4 | HID_DDK_NULL_PTR = 27300002 |
| HID_DDK_INVALID_OPERATION = -3 | HID_DDK_INVALID_OPERATION = 27300003 |
| HID_DDK_TIMEOUT = -5 | HID_DDK_TIMEOUT = 27300004 |

**起始 API Level**

10

**变更发生的版本**

从OpenHarmonySDK 5.0.0.52开始。

**变更的接口/组件**

drivers/external_device_manager

**适配指导**

[USB DDK开发指导](../../../application-dev/napi/usb-ddk-guidelines.md)

[HID DDK开发指导](../../../application-dev/napi/hid-ddk-guidelines.md)
