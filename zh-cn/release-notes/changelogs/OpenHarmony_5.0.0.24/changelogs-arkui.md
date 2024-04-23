# ArkUI子系统Changelog

## cl.arkui.1 ScrollBar组件没有子节点时，支持显示默认样式的滚动条

**访问级别**

公开接口

**变更原因**
从API version 12开始，ScrollBar组件没有子节点时，支持显示默认样式的滚动条。

**变更影响**

该变更为非兼容性变更。

API version 11及以前，ScrollBar组件没有子节点时，不显示滚动条。

API version 12及以后，ScrollBar组件没有子节点时，支持显示默认样式的滚动条。

**API Level**

12

**变更发生版本**

从OpenHarmony SDK 5.0.0.24 版本开始。

**变更的接口/组件**

ScrollBar组件

**适配指导**

请查阅[ScrollBar组件](../../../application-dev/reference/apis-arkui/arkui-ts/ts-basic-components-scrollbar.md)文档进行适配。

## cl.arkui.7 RichEditor菜单弹出时滚动组件后菜单显隐规格变更

**访问级别**

公开接口

**变更原因**

RichEditor菜单弹出后，滚动停止时菜单是否显示的UX默认行为改变

**变更影响**

变更前：RichEditor菜单弹出后，滚动组件时菜单隐藏，停止滚动时菜单不自动重新显示。

变更后：RichEditor菜单弹出后，滚动组件时菜单隐藏，停止滚动时会自动重新显示。
| 变更前 | 变更后 |
|---------|---------|
| ![alt text](menu_disappear_onScrollEnd.gif)| ![alt text](menu_appear_onScrollEnd.gif)|
**起始API Level**

该特性变更起始支持版本为 API 12。

**变更发生版本**

从OpenHarmony SDK 5.0.0.24开始。

**适配指导**

UX默认行为变更，无需适配。不影响功能逻辑，请关注当前富文本菜单在停止滚动时的UX表现。
