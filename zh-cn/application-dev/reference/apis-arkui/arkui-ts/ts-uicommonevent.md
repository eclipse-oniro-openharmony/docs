# 设置事件回调

>**说明：**
>
>本模块首批接口从API version 12开始支持，后续版本的新增接口，采用上角标单独标记接口的起始版本。

## UICommonEvent
用于设置基础事件回调。方法入参为undefied的时候，重置对应的事件回调。
### setOnClick

setOnClick(callback: Callback\<ClickEvent> | undefined): void;

设置[点击事件](./ts-universal-events-click.md#点击事件)的回调。

**参数：**

| 参数名 | 类型   | 必填 | 说明                       |
| ------ | ------ | ---- | -------------------------- |
| callback  | [Callback](./ts-types.md#callback12)<[ClickEvent](./ts-universal-events-click.md#clickevent对象说明)> \| undefined | 是   | 点击事件的回调函数。 |

### setOnTouch

setOnTouch(callback: Callback\<TouchEvent> | undefined): void;

设置[触摸事件](./ts-universal-events-touch.md#触摸事件)的回调。

**参数：**

| 参数名 | 类型   | 必填 | 说明                       |
| ------ | ------ | ---- | -------------------------- |
| callback  | [Callback](./ts-types.md#callback12)<[TouchEvent](./ts-universal-events-touch.md#touchevent对象说明)> \| undefined | 是   | 触摸事件的回调函数。 |


### setOnAppear

setOnAppear(callback: Callback\<void> | undefined): void;

设置[onAppear](./ts-universal-events-show-hide.md#onappear)事件的回调。

**参数：**

| 参数名 | 类型   | 必填 | 说明                       |
| ------ | ------ | ---- | -------------------------- |
| callback  | [Callback](./ts-types.md#callback12)\<void> \| undefined | 是   | onAppear事件的回调函数。 |


### setOnDisappear

setOnDisappear(callback: Callback\<void> | undefined): void;

设置[onDisappear](./ts-universal-events-show-hide.md#ondisappear)事件的回调。

**参数：**

| 参数名 | 类型   | 必填 | 说明                       |
| ------ | ------ | ---- | -------------------------- |
| callback  | [Callback](./ts-types.md#callback12)\<void> \| undefined | 是   | onDisappear事件的回调。 |

### setOnKeyEvent

setOnKeyEvent(callback: Callback\<KeyEvent> | undefined): void;

设置[按键事件](./ts-universal-events-key.md#按键事件)的回调。

**参数：**

| 参数名 | 类型   | 必填 | 说明                       |
| ------ | ------ | ---- | -------------------------- |
| callback  | [Callback](./ts-types.md#callback12)<[KeyEvent](./ts-universal-events-key.md#keyevent对象说明)>  \| undefined | 是   | 按键事件的回调函数。 |

### setOnFocus

setOnFocus(callback:  Callback\<void> | undefined): void;

设置[onFocus](./ts-universal-focus-event.md#onfocus)事件的回调。

**参数：**

| 参数名 | 类型   | 必填 | 说明                       |
| ------ | ------ | ---- | -------------------------- |
| callback  | [Callback](./ts-types.md#callback12)\<void> \| undefined | 是   | onDisappear事件的回调。 |

### setOnBlur

setOnBlur(callback: Callback\<void> | undefined): void;

设置[onBlur](./ts-universal-focus-event.md#onblur)事件的回调。

**参数：**

| 参数名 | 类型   | 必填 | 说明                       |
| ------ | ------ | ---- | -------------------------- |
| callback  | [Callback](./ts-types.md#callback12)\<void> \| undefined | 是   | onDisappear事件的回调。 |

### setOnHover

setOnHover(callback: HoverCallback | undefined): void;

设置[onHover](./ts-universal-mouse-key.md#onhover)事件的回调。

**参数：**

| 参数名 | 类型   | 必填 | 说明                       |
| ------ | ------ | ---- | -------------------------- |
| callback  | [HoverCallback](./ts-types.md#hovercallback12)  \| undefined | 是   | onHover事件的回调函数。 |

### setOnMouse

setOnMouse(callback: Callback\<MouseEvent> | undefined): void;

设置[onMouse](./ts-universal-mouse-key.md#onmouse)事件的回调。

**参数：**

| 参数名 | 类型   | 必填 | 说明                       |
| ------ | ------ | ---- | -------------------------- |
| callback  |  [Callback](./ts-types.md#callback12)<[MouseEvent](./ts-universal-mouse-key.md#mouseevent对象说明)>   \| undefined | 是   | onMouse事件的回调函数。 |