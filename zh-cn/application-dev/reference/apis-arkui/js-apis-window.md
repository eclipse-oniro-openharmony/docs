# @ohos.window (窗口)

窗口提供管理窗口的一些基础能力，包括对当前窗口的创建、销毁、各属性设置，以及对各窗口间的管理调度。

该模块提供以下窗口相关的常用功能：

- [Window](#window)：当前窗口实例，窗口管理器管理的基本单元。
- [WindowStage](#windowstage9)：窗口管理器。管理各个基本窗口单元。

> **说明：**
>
> 本模块首批接口从API version 6开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import window from '@ohos.window';
```

## WindowType<sup>7+</sup>


窗口类型枚举。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 名称                                  | 值 | 说明                                                                                     |
|-------------------------------------| ------ |----------------------------------------------------------------------------------------|
| TYPE_APP                            | 0      | 表示应用子窗口。<br>**模型约束：** 此接口仅可在FA模型下使用。                                                   |
| TYPE_SYSTEM_ALERT                   | 1      | 表示系统告警窗口。<br>- **说明：** 从API version 11开始废弃。<br>- 从 API version 7开始支持。                               |
| TYPE_FLOAT<sup>9+</sup>             | 8      | 表示悬浮窗。<br>**模型约束：** 此接口仅可在Stage模型下使用。<br>**需要权限：** ohos.permission.SYSTEM_FLOAT_WINDOW |
| TYPE_DIALOG<sup>10+</sup>           | 16      | 表示模态窗口。<br>**模型约束：** 此接口仅可在Stage模型下使用。                                                 |

## Configuration<sup>9+</sup>

创建子窗口或系统窗口时的参数。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 名称 | 类型 | 必填 | 说明                                                                          |
| ---------- | -------------------------- | -- |-----------------------------------------------------------------------------|
| name       | string                     | 是 | 窗口名字。                                                                       |
| windowType | [WindowType](#windowtype7) | 是 | 窗口类型。                                                                       |
| ctx        | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | 否 | 当前应用上下文信息。不设置，则默认为空。<br>FA模型下不需要使用该参数，即可创建子窗口，使用该参数时会报错。<br>Stage模型必须使用该参数，用于创建悬浮窗、模态窗或系统窗口。 |
| displayId  | number                     | 否 | 当前物理屏幕id。不设置，则默认为-1，该参数应为整数。                                             |
| parentId   | number                     | 否 | 父窗口id。不设置，则默认为-1，该参数应为整数。                                                           |

## AvoidAreaType<sup>7+</sup>

窗口内容需要规避区域的类型枚举。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 名称                             | 值   | 说明                                                         |
| -------------------------------- | ---- | ------------------------------------------------------------ |
| TYPE_SYSTEM                      | 0    | 表示系统默认区域。一般包括状态栏、导航栏，各设备系统定义可能不同。 |
| TYPE_CUTOUT                      | 1    | 表示刘海屏区域。                                             |
| TYPE_SYSTEM_GESTURE<sup>9+</sup> | 2    | 表示手势区域。                                               |
| TYPE_KEYBOARD<sup>9+</sup>       | 3    | 表示软键盘区域。                                             |
| TYPE_NAVIGATION_INDICATOR<sup>11+</sup> | 4    | 表示导航条区域。                                      |


## SystemBarProperties

状态栏、导航栏的属性。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 名称                                   | 类型 |  必填 | 说明                                                         |
| -------------------------------------- | -------- | ---- | ------------------------------------------------------------ |
| statusBarColor                         | string   |  否   | 状态栏背景颜色，为十六进制RGB或ARGB颜色，不区分大小写，例如`#00FF00`或`#FF00FF00`。默认值：`#0x66000000`。 |
| isStatusBarLightIcon<sup>7+</sup>      | boolean  |  否   | 状态栏图标是否为高亮状态。true表示高亮；false表示不高亮。默认值：false。 |
| statusBarContentColor<sup>8+</sup>     | string   |  否   | 状态栏文字颜色。当设置此属性后， `isStatusBarLightIcon`属性设置无效。默认值：`0xE5FFFFFF。` |
| navigationBarColor                     | string   |  否   | 导航栏背景颜色，为十六进制RGB或ARGB颜色，不区分大小写，例如`#00FF00`或`#FF00FF00`。默认值：`#0x66000000。` |
| isNavigationBarLightIcon<sup>7+</sup>  | boolean  |  否   | 导航栏图标是否为高亮状态。true表示高亮；false表示不高亮。默认值：false。 |
| navigationBarContentColor<sup>8+</sup> | string   |  否   | 导航栏文字颜色。当设置此属性后， `isNavigationBarLightIcon`属性设置无效。默认值：`#0xE5FFFFFF。` |

## Orientation<sup>9+</sup>

窗口显示方向类型枚举。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 名称                                  | 值   | 说明                          |
| ------------------------------------- | ---- | ----------------------------- |
| UNSPECIFIED                           | 0    | 表示未定义方向模式，由系统判定。 |
| PORTRAIT                              | 1    | 表示竖屏显示模式。             |
| LANDSCAPE                             | 2    | 表示横屏显示模式。   |
| PORTRAIT_INVERTED                     | 3    | 表示反向竖屏显示模式。   |
| LANDSCAPE_INVERTED                    | 4    | 表示反向横屏显示模式。 |
| AUTO_ROTATION                         | 5    | 表示传感器自动旋转模式。 |
| AUTO_ROTATION_PORTRAIT                | 6    | 表示传感器自动竖向旋转模式。 |
| AUTO_ROTATION_LANDSCAPE               | 7    | 表示传感器自动横向旋转模式。 |
| AUTO_ROTATION_RESTRICTED              | 8    | 表示受开关控制的自动旋转模式。 |
| AUTO_ROTATION_PORTRAIT_RESTRICTED     | 9    | 表示受开关控制的自动竖向旋转模式。 |
| AUTO_ROTATION_LANDSCAPE_RESTRICTED    | 10   | 表示受开关控制的自动横向旋转模式。 |
| LOCKED                                | 11   | 表示锁定模式。 |

## Rect<sup>7+</sup>

窗口矩形区域。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 名称   | 类型 | 可读 | 可写 | 说明               |
| ------ | -------- | ---- | ---- | ------------------ |
| left   | number   | 是   | 是   | 矩形区域的左边界，单位为px，该参数为整数。 |
| top    | number   | 是   | 是   | 矩形区域的上边界，单位为px，该参数应为整数。 |
| width  | number   | 是   | 是   | 矩形区域的宽度，单位为px，该参数应为整数。 |
| height | number   | 是   | 是   | 矩形区域的高度，单位为px，该参数应为整数。 |

## AvoidArea<sup>7+</sup>

窗口内容规避区域。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 名称       | 类型      | 可读 | 可写 | 说明               |
| ---------- | ------------- | ---- | ---- | ------------------ |
| visible<sup>9+</sup>    | boolean       | 是   | 是   | 规避区域是否可见。true表示可见；false表示不可见。 |
| leftRect   | [Rect](#rect7) | 是   | 是   | 屏幕左侧的矩形区。 |
| topRect    | [Rect](#rect7) | 是   | 是   | 屏幕顶部的矩形区。 |
| rightRect  | [Rect](#rect7) | 是   | 是   | 屏幕右侧的矩形区。 |
| bottomRect | [Rect](#rect7) | 是   | 是   | 屏幕底部的矩形区。 |

## Size<sup>7+</sup>

窗口大小。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 名称   | 类型 | 可读 | 可写 | 说明       |
| ------ | -------- | ---- | ---- | ---------- |
| width  | number   | 是   | 是   | 窗口宽度，单位为px，该参数应为整数。 |
| height | number   | 是   | 是   | 窗口高度，单位为px，该参数应为整数。 |

## RectChangeReason<sup>12+</sup>

窗口矩形（窗口位置及窗口大小）变化的原因。

**系统能力：** SystemCapability.Window.SessionManager

| 名称                  | 值   | 说明                                                         |
| --------------------- | ---- | ------------------------------------------------------------ |
| UNDEFINED                 | 0    | 默认值。                                                   |
| MAXIMIZE                | 1    | 窗口最大化。                                                   |
| RECOVER              | 2    | 窗口恢复到上一次的状态。                                                   |
| MOVE | 3    | 窗口拖拽移动。 |
| DRAG  | 4    | 窗口拖拽缩放。 |
| DRAG_START  | 5    | 窗口开始拖拽缩放。 |
| DRAG_END  | 6    | 窗口结束拖拽缩放。 |

## RectChangeOptions<sup>12+</sup>

窗口矩形（窗口位置及窗口大小）变化返回的值及变化原因。

**系统能力：** SystemCapability.Window.SessionManager

| 名称       | 类型      | 可读 | 可写 | 说明               |
| ---------- | ------------- | ---- | ---- | ------------------ |
| rect   | [Rect](#rect7) | 是   | 是   | 窗口矩形变化后的值。 |
| reason    | [RectChangeReason](#rectchangereason12) | 是   | 是   | 窗口矩形变化的原因。 |

## WindowProperties

窗口属性。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 名称                                  | 类型                  | 可读 | 可写 | 说明                                                                                                     |
| ------------------------------------- | ------------------------- | ---- | ---- |--------------------------------------------------------------------------------------------------------|
| windowRect<sup>7+</sup>               | [Rect](#rect7)             | 是   | 是   | 窗口尺寸。                                                                                                  |
| drawableRect<sup>11+</sup>            | [Rect](#rect7)             | 是   | 是   | 窗口内可绘制区域尺寸，其中左边界上边界是相对窗口计算。                                                                                                  |
| type<sup>7+</sup>                     | [WindowType](#windowtype7) | 是   | 是   | 窗口类型。                                                                                                  |
| isFullScreen                          | boolean                   | 是   | 是   | 是否全屏，默认为false。true表示全屏；false表示非全屏。                                                                     |
| isLayoutFullScreen<sup>7+</sup>       | boolean                   | 是   | 是   | 窗口是否为沉浸式，默认为false。true表示沉浸式；false表示非沉浸式。                                                               |
| focusable<sup>7+</sup>                | boolean                   | 是   | 否   | 窗口是否可聚焦，默认为true。true表示可聚焦；false表示不可聚焦。                                                                 |
| touchable<sup>7+</sup>                | boolean                   | 是   | 否   | 窗口是否可触摸，默认为true。true表示可触摸；false表示不可触摸。                                                                 |
| brightness                            | number                    | 是   | 是   | 屏幕亮度。该参数为浮点数，可设置的亮度范围为[0.0, 1.0]，其取1.0时表示最大亮度值。如果窗口没有设置亮度值，表示亮度跟随系统，此时获取到的亮度值为-1。                      |
| dimBehindValue<sup>(deprecated)</sup> | number                    | 是   | 是   | 靠后窗口的暗度值。该参数为浮点数，取值范围为[0.0, 1.0]，其取1.0表示最暗。<br>- **说明：** 从API version 9开始废弃。<br>- 从 API version 7开始支持。 |
| isKeepScreenOn                        | boolean                   | 是   | 是   | 屏幕是否常亮，默认为false。true表示常亮；false表示不常亮。                                                                   |
| isPrivacyMode<sup>7+</sup>            | boolean                   | 是   | 是   | 隐私模式，默认为false。true表示模式开启；false表示模式关闭。                                                                  |
| isRoundCorner<sup>(deprecated)</sup>  | boolean                   | 是   | 是   | 窗口是否为圆角。默认为false。true表示圆角；false表示非圆角。<br>- **说明：** 从API version 9开始废弃。<br/>- 从 API version 7开始支持。      |
| isTransparent<sup>7+</sup>            | boolean                   | 是   | 是   | 窗口是否透明。默认为false。true表示透明；false表示不透明。                                                                   |
| id<sup>9+</sup>                       | number                    | 是   | 否   | 窗口ID，默认值为0，该参数应为整数。                                                                                    |

## ColorSpace<sup>8+</sup>

色域模式。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 名称       | 值 | 说明           |
| ---------- | ------ | -------------- |
| DEFAULT    | 0      | 默认SRGB色域模式。 |
| WIDE_GAMUT | 1      | 广色域模式。   |

## WindowEventType<sup>10+</sup>

窗口生命周期。

| 名称       | 值 | 说明       |
| ---------- | ------ | ---------- |
| WINDOW_SHOWN      | 1      | 切到前台。<br> **系统能力：** SystemCapability.WindowManager.WindowManager.Core。|
| WINDOW_ACTIVE     | 2      | 获焦状态。<br> **系统能力：** SystemCapability.WindowManager.WindowManager.Core。|
| WINDOW_INACTIVE   | 3      | 失焦状态。<br> **系统能力：** SystemCapability.WindowManager.WindowManager.Core。|
| WINDOW_HIDDEN     | 4      | 切到后台。<br> **系统能力：** SystemCapability.WindowManager.WindowManager.Core。|
| WINDOW_DESTROYED<sup>11+</sup>  | 7      | 窗口销毁。<br> **系统能力：** SystemCapability.Window.SessionManager。|

## WindowLimits<sup>11+</sup>

窗口尺寸限制参数。可以通过[setWindowLimits](#setwindowlimits11)设置窗口尺寸限制，并且可以通过[getWindowLimits](#getwindowlimits11)获得当前的窗口尺寸限制。

**系统能力：** SystemCapability.Window.SessionManager

| 名称      | 类型   | 可读 | 可写 | 说明                                                         |
| :-------- | :----- | :--- | :--- | :----------------------------------------------------------- |
| maxWidth  | number | 是   | 是   | 窗口的最大宽度。单位为px，该参数为整数。值默认为0，表示该属性不发生变化。下限值为0，上限值为系统限定的最大宽度。  |
| maxHeight | number | 是   | 是   | 窗口的最大高度。单位为px，该参数为整数。值默认为0，表示该属性不发生变化。下限值为0，上限值为系统限定的最大高度。  |
| minWidth  | number | 是   | 是   | 窗口的最小宽度。单位为px，该参数为整数。值默认为0，表示该属性不发生变化。下限值为0，上限值为系统限定的最小宽度。  |
| minHeight | number | 是   | 是   | 窗口的最小高度。单位为px，该参数为整数。值默认为0，表示该属性不发生变化。下限值为0，上限值为系统限定的最小高度。  |

## WindowStatusType<sup>11+</sup>

窗口模式枚举。

**系统能力：** SystemCapability.Window.SessionManager

| 名称       | 值   | 说明                          |
| ---------- | ---- | ----------------------------- |
| UNDEFINED  | 0    | 表示APP未定义窗口模式。       |
| FULL_SCREEN | 1    | 表示APP全屏模式。             |
| MAXIMIZE    | 2    | 表示APP窗口最大化模式。   |
| MINIMIZE    | 3    | 表示APP窗口最小化模式。   |
| FLOATING    | 4    | 表示APP自由悬浮形式窗口模式。   |
| SPLIT_SCREEN  | 5    | 表示APP分屏模式。   |

## TitleButtonRect<sup>11+</sup>

标题栏上的最小化、最大化、关闭按钮矩形区域，该区域位置坐标相对窗口右上角。

**系统能力：**  SystemCapability.Window.SessionManager

| 名称   | 类型   | 可读 | 可写 | 说明                                       |
| ------ | ------ | ---- | ---- | ------------------------------------------ |
| right  | number | 是   | 是   | 矩形区域的右边界，单位为vp，该参数为整数。 |
| top    | number | 是   | 是   | 矩形区域的上边界，单位为vp，该参数为整数。 |
| width  | number | 是   | 是   | 矩形区域的宽度，单位为vp，该参数为整数。   |
| height | number | 是   | 是   | 矩形区域的高度，单位为vp，该参数为整数。   |

## window.createWindow<sup>9+</sup>

createWindow(config: Configuration, callback: AsyncCallback&lt;Window&gt;): void

创建子窗口或者系统窗口，使用callback异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------------------------------------- | -- | --------------------------------- |
| config   | [Configuration](#configuration9)       | 是 | 创建窗口时的参数。   |
| callback | AsyncCallback&lt;[Window](#window)&gt; | 是 | 回调函数。返回当前创建的窗口对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 1300001 | Repeated operation. |
| 1300006 | This window context is abnormal. |
| 1300008 | The operation is on invalid display. |
| 1300009 | The parent window is invalid. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
let config: window.Configuration = {
  name: "test",
  windowType: window.WindowType.TYPE_DIALOG,
  ctx: this.context
};
try {
  window.createWindow(config, (err: BusinessError, data) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to create the window. Cause: ' + JSON.stringify(err));
      return;
    }
    windowClass = data;
    console.info('Succeeded in creating the window. Data: ' + JSON.stringify(data));
    windowClass.resize(500, 1000);
  });
} catch (exception) {
  console.error('Failed to create the window. Cause: ' + JSON.stringify(exception));
}
```

## window.createWindow<sup>9+</sup>

createWindow(config: Configuration): Promise&lt;Window&gt;

创建子窗口或者系统窗口，使用Promise异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------ | -------------------------------- | -- | ------------------ |
| config | [Configuration](#configuration9) | 是 | 创建窗口时的参数。 |

**返回值：**

| 类型 | 说明 |
| -------------------------------- | ------------------------------------ |
| Promise&lt;[Window](#window)&gt; | Promise对象。返回当前创建的窗口对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 1300001 | Repeated operation. |
| 1300006 | This window context is abnormal. |
| 1300008 | The operation is on invalid display. |
| 1300009 | The parent window is invalid. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
let config: window.Configuration = {
  name: "test",
  windowType: window.WindowType.TYPE_DIALOG,
  ctx: this.context
};
try {
  let promise = window.createWindow(config);
  promise.then((data) => {
    windowClass = data;
    console.info('Succeeded in creating the window. Data:' + JSON.stringify(data));
  }).catch((err: BusinessError) => {
    console.error('Failed to create the Window. Cause:' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to create the window. Cause: ' + JSON.stringify(exception));
}
```

## window.findWindow<sup>9+</sup>

findWindow(name: string): Window

查找name所对应的窗口。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明     |
| ------ | ------ | ---- | -------- |
| name   | string | 是   | 窗口id。 |

**返回值：**

| 类型 | 说明 |
| ----------------- | ------------------- |
| [Window](#window) | 当前查找的窗口对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
let windowClass: window.Window | undefined = undefined;
try {
  windowClass = window.findWindow('test');
} catch (exception) {
  console.error('Failed to find the Window. Cause: ' + JSON.stringify(exception));
}
```

## window.getLastWindow<sup>9+</sup>

getLastWindow(ctx: BaseContext, callback: AsyncCallback&lt;Window&gt;): void

获取当前应用内最上层的子窗口，若无应用子窗口，则返回应用主窗口，使用callback异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------------------------------------- | -- | ---------------------------------------- |
| ctx      | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | 是 | 当前应用上下文信息。 |
| callback | AsyncCallback&lt;[Window](#window)&gt; | 是 | 回调函数。返回当前应用内最后显示的窗口对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 1300002 | This window state is abnormal.   |
| 1300006 | This window context is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...
  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    try {
      window.getLastWindow(this.context, (err: BusinessError, data) => {
        const errCode: number = err.code;
        if (errCode) {
          console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(err));
          return;
        }
        windowClass = data;
        console.info('Succeeded in obtaining the top window. Data: ' + JSON.stringify(data));
      });
    } catch (exception) {
      console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(exception));
    }
  }
}
```

## window.getLastWindow<sup>9+</sup>

getLastWindow(ctx: BaseContext): Promise&lt;Window&gt;

获取当前应用内最上层的子窗口，若无应用子窗口，则返回应用主窗口，使用Promise异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------ | ----------- | ---- | ------------------------------------------------------------ |
| ctx    | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | 是   | 当前应用上下文信息。 |

**返回值：**

| 类型 | 说明 |
| -------------------------------- | ------------------------------------------- |
| Promise&lt;[Window](#window)&gt; | Promise对象。返回当前应用内最后显示的窗口对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 1300002 | This window state is abnormal.   |
| 1300006 | This window context is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...
  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    try {
      let promise = window.getLastWindow(this.context);
      promise.then((data) => {
        windowClass = data;
        console.info('Succeeded in obtaining the top window. Data: ' + JSON.stringify(data));
      }).catch((err: BusinessError) => {
        console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(err));
      });
    } catch (exception) {
      console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(exception));
    }
  }
}
```

## window.shiftAppWindowFocus<sup>11+</sup>
shiftAppWindowFocus(sourceWindowId: number, targetWindowId: number): Promise&lt;void&gt;

在同应用内将窗口焦点从源窗口转移到目标窗口，仅支持应用主窗和子窗的焦点转移。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名          | 类型   | 必填  | 说明                    |
| -------------- | ------ | ----- | ----------------------- |
| sourceWindowId | number | 是    | 源窗口id，必须是获焦状态。|
| targetWindowId | number | 是    | 目标窗口id。             |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                                      |
| ------- | --------------------------------------------- |
| 1300002 | This window state is abnormal.                |
| 1300003 | This window manager service works abnormally. |
| 1300004 | Unauthorized operation.                       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let sourceWindowId: number = 40;
  let targetWindowId: number = 41;
  let promise = window.shiftAppWindowFocus(sourceWindowId, targetWindowId);
  promise.then(() => {
    console.info('Succeeded in shifting app window focus');
  }).catch((err: BusinessError) => {
    console.error('Failed to shift app window focus. Cause:' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to shift app window focus. Cause:' + JSON.stringify(exception));
}
```

## window.create<sup>(deprecated)</sup>

create(id: string, type: WindowType, callback: AsyncCallback&lt;Window&gt;): void

创建子窗口，使用callback异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[createWindow()](#windowcreatewindow9)。

**模型约束：** 此接口仅可在FA模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                   | 必填 | 说明                                 |
| -------- | -------------------------------------- | ---- | ------------------------------------ |
| id       | string                                 | 是   | 窗口id。                             |
| type     | [WindowType](#windowtype7)              | 是   | 窗口类型。                           |
| callback | AsyncCallback&lt;[Window](#window)&gt; | 是   | 回调函数。返回当前创建的子窗口对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
window.create('test', window.WindowType.TYPE_APP, (err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to create the subWindow. Cause: ' + JSON.stringify(err));
    return;
  }
  windowClass = data;
  console.info('Succeeded in creating the subWindow. Data: ' + JSON.stringify(data));
});
```

## window.create<sup>(deprecated)</sup>

create(id: string, type: WindowType): Promise&lt;Window&gt;

创建子窗口，使用Promise异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[createWindow()](#windowcreatewindow9-1)。

**模型约束：** 此接口仅可在FA模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型                      | 必填 | 说明       |
| ------ | ------------------------- | ---- | ---------- |
| id     | string                    | 是   | 窗口id。   |
| type   | [WindowType](#windowtype7) | 是   | 窗口类型。 |

**返回值：**

| 类型                             | 说明                                    |
| -------------------------------- | --------------------------------------- |
| Promise&lt;[Window](#window)&gt; | Promise对象。返回当前创建的子窗口对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
let promise = window.create('test', window.WindowType.TYPE_APP);
promise.then((data) => {
  windowClass = data;
  console.info('Succeeded in creating the subWindow. Data: ' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to create the subWindow. Cause: ' + JSON.stringify(err));
});
```

## window.create<sup>(deprecated)</sup>

create(ctx: BaseContext, id: string, type: WindowType, callback: AsyncCallback&lt;Window&gt;): void

创建系统窗口，使用callback异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[createWindow()](#windowcreatewindow9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                                    | 必填 | 说明                                 |
| -------- | ------------------------------------------------------- | ---- | ------------------------------------ |
| ctx      | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | 是   | 当前应用上下文信息。                 |
| id       | string                                                  | 是   | 窗口id。                             |
| type     | [WindowType](#windowtype7)                              | 是   | 窗口类型。                           |
| callback | AsyncCallback&lt;[Window](#window)&gt;                  | 是   | 回调函数。返回当前创建的子窗口对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
window.create('test', window.WindowType.TYPE_SYSTEM_ALERT, (err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to create the window. Cause: ' + JSON.stringify(err));
    return;
  }
  windowClass = data;
  console.info('Succeeded in creating the window. Data: ' + JSON.stringify(data));
  windowClass.resetSize(500, 1000);
});
```

## window.create<sup>(deprecated)</sup>

create(ctx: BaseContext, id: string, type: WindowType): Promise&lt;Window&gt;

创建系统窗口，使用Promise异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[createWindow()](#windowcreatewindow9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型                      | 必填 | 说明                                                         |
| ------ | ------------------------- | ---- | ------------------------------------------------------------ |
| ctx    | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | 是   | 当前应用上下文信息。 |
| id     | string                    | 是   | 窗口id。                                                     |
| type   | [WindowType](#windowtype7) | 是   | 窗口类型。                                                   |

**返回值：**

| 类型                             | 说明                                    |
| -------------------------------- | --------------------------------------- |
| Promise&lt;[Window](#window)&gt; | Promise对象。返回当前创建的子窗口对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
let promise = window.create('test', window.WindowType.TYPE_SYSTEM_ALERT);
promise.then((data) => {
  windowClass = data;
  console.info('Succeeded in creating the window. Data:' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to create the Window. Cause:' + JSON.stringify(err));
});
```

## window.find<sup>(deprecated)</sup>

find(id: string, callback: AsyncCallback&lt;Window&gt;): void

查找id所对应的窗口，使用callback异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[findWindow()](#windowfindwindow9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                   | 必填 | 说明                                 |
| -------- | -------------------------------------- | ---- | ------------------------------------ |
| id       | string                                 | 是   | 窗口id。                             |
| callback | AsyncCallback&lt;[Window](#window)&gt; | 是   | 回调函数。返回当前查找到的窗口对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
window.find('test', (err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to find the Window. Cause: ' + JSON.stringify(err));
    return;
  }
  windowClass = data;
  console.info('Succeeded in finding the window. Data: ' + JSON.stringify(data));
});
```

## window.find<sup>(deprecated)</sup>

find(id: string): Promise&lt;Window&gt;

查找id所对应的窗口，使用Promise异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[findWindow()](#windowfindwindow9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明     |
| ------ | ------ | ---- | -------- |
| id     | string | 是   | 窗口id。 |

**返回值：**

| 类型                             | 说明                                  |
| -------------------------------- | ------------------------------------- |
| Promise&lt;[Window](#window)&gt; | Promise对象。返回当前查找的窗口对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
let promise = window.find('test');
promise.then((data) => {
  windowClass = data;
  console.info('Succeeded in finding the window. Data: ' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to find the Window. Cause: ' + JSON.stringify(err));
});
```

## window.getTopWindow<sup>(deprecated)</sup>

getTopWindow(callback: AsyncCallback&lt;Window&gt;): void

获取当前应用内最后显示的窗口，使用callback异步回调。

> **说明：**
>
> 从 API version 6开始支持，从API version 9开始废弃，推荐使用[getLastWindow()](#windowgetlastwindow9)。

**模型约束：** 此接口仅可在FA模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                   | 必填 | 说明                                         |
| -------- | -------------------------------------- | ---- | -------------------------------------------- |
| callback | AsyncCallback&lt;[Window](#window)&gt; | 是   | 回调函数。返回当前应用内最后显示的窗口对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
window.getTopWindow((err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(err));
    return;
  }
  windowClass = data;
  console.info('Succeeded in obtaining the top window. Data: ' + JSON.stringify(data));
});
```

## window.getTopWindow<sup>(deprecated)</sup>

getTopWindow(): Promise&lt;Window&gt;

获取当前应用内最后显示的窗口，使用Promise异步回调。

> **说明：**
>
> 从 API version 6开始支持，从API version 9开始废弃，推荐使用[getLastWindow()](#windowgetlastwindow9-1)。

**模型约束：** 此接口仅可在FA模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型                             | 说明                                            |
| -------------------------------- | ----------------------------------------------- |
| Promise&lt;[Window](#window)&gt; | Promise对象。返回当前应用内最后显示的窗口对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
let promise = window.getTopWindow();
promise.then((data)=> {
    windowClass = data;
    console.info('Succeeded in obtaining the top window. Data: ' + JSON.stringify(data));
}).catch((err: BusinessError)=>{
    console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(err));
});
```

## window.getTopWindow<sup>(deprecated)</sup>

getTopWindow(ctx: BaseContext, callback: AsyncCallback&lt;Window&gt;): void

获取当前应用内最后显示的窗口，使用callback异步回调。

> **说明：**
>
> 从 API version 8开始支持，从API version 9开始废弃，推荐使用[getLastWindow()](#windowgetlastwindow9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                   | 必填 | 说明                                                         |
| -------- | -------------------------------------- | ---- | ------------------------------------------------------------ |
| ctx      | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md)                            | 是   | 当前应用上下文信息。 |
| callback | AsyncCallback&lt;[Window](#window)&gt; | 是   | 回调函数。返回当前应用内最后显示的窗口对象。                 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage:window.WindowStage){
    console.info('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    try {
      window.getTopWindow(this.context, (err: BusinessError, data) => {
        const errCode: number = err.code;
        if(errCode){
          console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(err));
          return ;
        }
        windowClass = data;
        console.info('Succeeded in obtaining the top window. Data: ' + JSON.stringify(data));
      });
    } catch(error){
      console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(error));
    }
  }
}
```

## window.getTopWindow<sup>(deprecated)</sup>

getTopWindow(ctx: BaseContext): Promise&lt;Window&gt;

获取当前应用内最后显示的窗口，使用Promise异步回调。

> **说明：**
>
> 从 API version 8开始支持，从API version 9开始废弃，推荐使用[getLastWindow()](#windowgetlastwindow9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ----------- | ---- | ------------------------------------------------------------ |
| ctx    | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | 是   | 当前应用上下文信息。 |

**返回值：**

| 类型                             | 说明                                            |
| -------------------------------- | ----------------------------------------------- |
| Promise&lt;[Window](#window)&gt; | Promise对象。返回当前应用内最后显示的窗口对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage:window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    let promise = window.getTopWindow(this.context);
    promise.then((data) => {
      windowClass = data;
      console.info('Succeeded in obtaining the top window. Data: ' + JSON.stringify(data));
    }).catch((error: BusinessError) => {
      console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(error));
    });
  }
}
```

## SpecificSystemBar<sup>11+</sup>

当前支持显示或隐藏的系统栏类型。

**系统能力：** SystemCapability.Window.SessionManager

| 名称                  | 类型       | 说明     |
|---------------------|----------|--------|
| status              | string   | 状态栏。   |
| navigation          | string   | 导航栏。   |
| navigationIndicator | string   | 底部导航条。 |

## Window

当前窗口实例，窗口管理器管理的基本单元。

下列API示例中都需先使用[getLastWindow()](#windowgetlastwindow9)、[createWindow()](#windowcreatewindow9)、[findWindow()](#windowfindwindow9)中的任一方法获取到Window实例（windowClass），再通过此实例调用对应方法。

### showWindow<sup>9+</sup>

showWindow(callback: AsyncCallback&lt;void&gt;): void

显示当前窗口，使用callback异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | ------------------------- | -- | --------- |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

windowClass.showWindow((err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to show the window. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in showing the window.');
});
```

### showWindow<sup>9+</sup>

showWindow(): Promise&lt;void&gt;

显示当前窗口，使用Promise异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型 | 说明 |
| ------------------- | ----------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.showWindow();
promise.then(() => {
  console.info('Succeeded in showing the window.');
}).catch((err: BusinessError) => {
  console.error('Failed to show the window. Cause: ' + JSON.stringify(err));
});
```

### destroyWindow<sup>9+</sup>

destroyWindow(callback: AsyncCallback&lt;void&gt;): void

销毁当前窗口，使用callback异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | ------------------------- | -- | --------- |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

windowClass.destroyWindow((err) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to destroy the window. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in destroying the window.');
});
```

### destroyWindow<sup>9+</sup>

destroyWindow(): Promise&lt;void&gt;

销毁当前窗口，使用Promise异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型 | 说明 |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.destroyWindow();
promise.then(() => {
  console.info('Succeeded in destroying the window.');
}).catch((err: BusinessError) => {
  console.error('Failed to destroy the window. Cause: ' + JSON.stringify(err));
});
```

### moveWindowTo<sup>9+</sup>

moveWindowTo(x: number, y: number, callback: AsyncCallback&lt;void&gt;): void

移动窗口位置，使用callback异步回调。

全屏模式窗口不支持该操作。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | ------------------------- | -- | --------------------------------------------- |
| x        | number                    | 是 | 窗口在x轴方向移动的值，值为正表示右移，单位为px，该参数仅支持整数输入。 |
| y        | number                    | 是 | 窗口在y轴方向移动的值，值为正表示下移，单位为px，该参数仅支持整数输入。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。                                     |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  windowClass.moveWindowTo(300, 300, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to move the window. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in moving the window.');
  });
} catch (exception) {
  console.error('Failed to move the window. Cause:' + JSON.stringify(exception));
}
```

### moveWindowTo<sup>9+</sup>

moveWindowTo(x: number, y: number): Promise&lt;void&gt;

移动窗口位置，使用Promise异步回调。

全屏模式窗口不支持该操作。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -- | ----- | -- | --------------------------------------------- |
| x | number | 是 | 窗口在x轴方向移动的值，值为正表示右移，单位为px，该参数仅支持整数输入。 |
| y | number | 是 | 窗口在y轴方向移动的值，值为正表示下移，单位为px，该参数仅支持整数输入。 |

**返回值：**

| 类型 | 说明 |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let promise = windowClass.moveWindowTo(300, 300);
  promise.then(() => {
    console.info('Succeeded in moving the window.');
  }).catch((err: BusinessError) => {
    console.error('Failed to move the window. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to move the window. Cause:' + JSON.stringify(exception));
}
```

### resize<sup>9+</sup>

resize(width: number, height: number, callback: AsyncCallback&lt;void&gt;): void

改变当前窗口大小，使用callback异步回调。

应用主窗口与子窗口存在大小限制，默认宽度范围：[320, 1920]，默认高度范围：[240, 1920]，单位为vp。
应用主窗口与子窗口的最小宽度与最小高度可由产品端进行配置，配置后的最小宽度与最小高度以产品段配置值为准，具体尺寸限制范围可以通过[getWindowLimits](#getwindowlimits11)接口进行查询。

系统窗口存在大小限制，宽度范围：[0, 1920]，高度范围：[0, 1920]，单位为vp。

设置的宽度与高度受到此约束限制，规则：
若所设置的窗口宽/高尺寸小于窗口最小宽/高限值，则窗口最小宽/高限值生效；
若所设置的窗口宽/高尺寸大于窗口最大宽/高限值，则窗口最大宽/高限值生效。

全屏模式窗口不支持该操作。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | ------------------------- | -- | ------------------------ |
| width    | number                    | 是 | 目标窗口的宽度，单位为px，该参数仅支持整数输入，负值为非法参数。 |
| height   | number                    | 是 | 目标窗口的高度，单位为px，该参数仅支持整数输入，负值为非法参数。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。                |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  windowClass.resize(500, 1000, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to change the window size. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in changing the window size.');
  });
} catch (exception) {
  console.error('Failed to change the window size. Cause:' + JSON.stringify(exception));
}
```

### resize<sup>9+</sup>

resize(width: number, height: number): Promise&lt;void&gt;

改变当前窗口大小，使用Promise异步回调。

应用主窗口与子窗口存在大小限制，默认宽度范围：[320, 1920]，默认高度范围：[240, 1920]，单位为vp。
应用主窗口与子窗口的最小宽度与最小高度可由产品端进行配置，配置后的最小宽度与最小高度以产品段配置值为准，具体尺寸限制范围可以通过[getWindowLimits](#getwindowlimits11)接口进行查询。

系统窗口存在大小限制，宽度范围：[0, 1920]，高度范围：[0, 1920]，单位为vp。

设置的宽度与高度受到此约束限制，规则：
若所设置的窗口宽/高尺寸小于窗口最小宽/高限值，则窗口最小宽/高限值生效；
若所设置的窗口宽/高尺寸大于窗口最大宽/高限值，则窗口最大宽/高限值生效。

全屏模式窗口不支持该操作。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------ | ------ | -- | ------------------------ |
| width  | number | 是 | 目标窗口的宽度，单位为px，该参数仅支持整数输入，负值为非法参数。 |
| height | number | 是 | 目标窗口的高度，单位为px，该参数仅支持整数输入，负值为非法参数。 |

**返回值：**

| 类型 | 说明 |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let promise = windowClass.resize(500, 1000);
  promise.then(() => {
    console.info('Succeeded in changing the window size.');
  }).catch((err: BusinessError) => {
    console.error('Failed to change the window size. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to change the window size. Cause: ' + JSON.stringify(exception));
}
```

### getWindowProperties<sup>9+</sup>

getWindowProperties(): WindowProperties

获取当前窗口的属性，返回WindowProperties。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型 | 说明 |
| ------------------------------------- | ------------- |
| [WindowProperties](#windowproperties) | 当前窗口属性。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
try {
  let properties = windowClass.getWindowProperties();
} catch (exception) {
  console.error('Failed to obtain the window properties. Cause: ' + JSON.stringify(exception));
}
```

### getWindowAvoidArea<sup>9+</sup>

getWindowAvoidArea(type: AvoidAreaType): AvoidArea

获取窗口内容规避的区域；如系统栏区域、刘海屏区域、手势区域、软键盘区域等与窗口内容重叠时，需要窗口内容避让的区域。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ---- |----------------------------------| -- | ------------------------------------------------------------ |
| type | [AvoidAreaType](#avoidareatype7) | 是 | 表示规避区类型。 |

**返回值：**

| 类型 | 说明 |
|--------------------------| ----------------- |
| [AvoidArea](#avoidarea7) | 窗口内容规避区域。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
let type = window.AvoidAreaType.TYPE_SYSTEM;
try {
  let avoidArea = windowClass.getWindowAvoidArea(type);
} catch (exception) {
  console.error('Failed to obtain the area. Cause:' + JSON.stringify(exception));
}
```

### setWindowLayoutFullScreen<sup>9+</sup>

setWindowLayoutFullScreen(isLayoutFullScreen: boolean, callback: AsyncCallback&lt;void&gt;): void

设置窗口的布局是否为沉浸式布局，使用callback异步回调。
沉浸式布局是指布局不避让状态栏与导航栏，组件可能产生与其重叠的情况。
非沉浸式布局是指布局避让状态栏与导航栏，组件不会与其重叠。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------------------ | ------------------------- | -- | --------- |
| isLayoutFullScreen | boolean                   | 是 | 窗口的布局是否为沉浸式布局（该沉浸式布局状态栏、导航栏仍然显示）。true表示沉浸式布局；false表示非沉浸式布局。 |
| callback           | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isLayoutFullScreen = true;
try {
  windowClass.setWindowLayoutFullScreen(isLayoutFullScreen, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the window layout to full-screen mode.');
  });
} catch (exception) {
  console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(exception));
}
```

### setWindowLayoutFullScreen<sup>9+</sup>

setWindowLayoutFullScreen(isLayoutFullScreen: boolean): Promise&lt;void&gt;

设置窗口的布局是否为沉浸式布局，使用Promise异步回调。
沉浸式布局是指布局不避让状态栏与导航栏，组件可能产生与其重叠的情况。
非沉浸式布局是指布局避让状态栏与导航栏，组件不会与其重叠。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------------------ | ------- | -- | ------------------------------------------------------------------------------------------------ |
| isLayoutFullScreen | boolean | 是 | 窗口的布局是否为沉浸式布局（该沉浸式布局状态栏、导航栏仍然显示）。true表示沉浸式布局；false表示非沉浸式布局。 |

**返回值：**

| 类型 | 说明 |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isLayoutFullScreen = true;
try {
  let promise = windowClass.setWindowLayoutFullScreen(isLayoutFullScreen);
  promise.then(() => {
    console.info('Succeeded in setting the window layout to full-screen mode.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(exception));
}
```

### setWindowSystemBarEnable<sup>9+</sup>

setWindowSystemBarEnable(names: Array<'status' | 'navigation'>, callback: AsyncCallback&lt;void&gt;): void

设置窗口全屏模式时导航栏、状态栏的可见模式，使用callback异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | ---------------------------- | -- | --------- |
| names    | Array<'status'\|'navigation'> | 是 | 设置窗口全屏模式时状态栏和导航栏是否显示。<br>例如，需全部显示，该参数设置为['status',&nbsp;'navigation']；不设置，则默认不显示。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
// 此处以不显示导航栏、状态栏为例
import { BusinessError } from '@ohos.base';

let names: Array<'status' | 'navigation'> = [];
try {
  windowClass.setWindowSystemBarEnable(names, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the system bar to be invisible.');
  });
} catch (exception) {
  console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(exception));
}
```

### setWindowSystemBarEnable<sup>9+</sup>

setWindowSystemBarEnable(names: Array<'status' | 'navigation'>): Promise&lt;void&gt;

设置窗口全屏模式时导航栏、状态栏的可见模式，使用Promise异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型  | 必填 | 说明 |
| ----- | ---------------------------- | -- | --------------------------------- |
| names | Array<'status'\|'navigation'> | 是 | 设置窗口全屏模式时状态栏和导航栏是否显示。<br>例如，需全部显示，该参数设置为['status',&nbsp;'navigation']；不设置，则默认不显示。 |

**返回值：**

| 类型 | 说明 |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
// 此处以不显示导航栏、状态栏为例
import { BusinessError } from '@ohos.base';

let names: Array<'status' | 'navigation'> = [];
try {
  let promise = windowClass.setWindowSystemBarEnable(names);
  promise.then(() => {
    console.info('Succeeded in setting the system bar to be invisible.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(exception));
}
```

### setSpecificSystemBarEnabled<sup>11+</sup>

setSpecificSystemBarEnabled(name: SpecificSystemBar, enable: boolean): Promise&lt;void&gt;

设置窗口全屏模式时导航栏、状态栏、底部导航条的显示和隐藏，使用Promise异步回调。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名 | 类型  | 必填 | 说明 |
| ----- | ---------------------------- | -- | --------------------------------- |
| name  | [SpecificSystemBar](#specificsystembar11) | 是 | 设置窗口全屏模式时，显示或隐藏的系统栏类型。 |
| enable  | boolean | 是 | 设置窗口全屏模式时状态栏、导航栏或底部导航条是否显示，true表示显示 false表示隐藏。|

**返回值：**

| 类型 | 说明 |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
// 此处以隐藏底部导航条为例
import { BusinessError } from '@ohos.base';

try {
  let promise = windowClass.setSpecificSystemBarEnabled('navigationIndicator', false);
  promise.then(() => {
    console.info('Succeeded in setting the system bar to be invisible.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(exception));
}
```

### setWindowSystemBarProperties<sup>9+</sup>

setWindowSystemBarProperties(systemBarProperties: SystemBarProperties, callback: AsyncCallback&lt;void&gt;): void

设置窗口全屏模式时窗口内导航栏、状态栏的属性，使用callback异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名              | 类型                                        | 必填 | 说明                   |
| ------------------- | ------------------------------------------- | ---- | ---------------------- |
| SystemBarProperties | [SystemBarProperties](#systembarproperties) | 是   | 导航栏、状态栏的属性。 |
| callback            | AsyncCallback&lt;void&gt;                   | 是   | 回调函数。             |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let SystemBarProperties: window.SystemBarProperties = {
  statusBarColor: '#ff00ff',
  navigationBarColor: '#00ff00',
  //以下两个属性从API Version8开始支持
  statusBarContentColor: '#ffffff',
  navigationBarContentColor: '#00ffff'
};
try {
  windowClass.setWindowSystemBarProperties(SystemBarProperties, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the system bar properties.');
  });
} catch (exception) {
  console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(exception));
}
```

### setWindowSystemBarProperties<sup>9+</sup>

setWindowSystemBarProperties(systemBarProperties: SystemBarProperties): Promise&lt;void&gt;

设置窗口全屏模式时窗口内导航栏、状态栏的属性，使用Promise异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名              | 类型                                        | 必填 | 说明                   |
| ------------------- | ------------------------------------------- | ---- | ---------------------- |
| SystemBarProperties | [SystemBarProperties](#systembarproperties) | 是   | 导航栏、状态栏的属性。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let SystemBarProperties: window.SystemBarProperties = {
  statusBarColor: '#ff00ff',
  navigationBarColor: '#00ff00',
  //以下两个属性从API Version8开始支持
  statusBarContentColor: '#ffffff',
  navigationBarContentColor: '#00ffff'
};
try {
  let promise = windowClass.setWindowSystemBarProperties(SystemBarProperties);
  promise.then(() => {
    console.info('Succeeded in setting the system bar properties.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(exception));
}
```

### getWindowSystemBarProperties<sup>12+</sup>

getWindowSystemBarProperties(): SystemBarProperties

主窗口获取导航栏、状态栏的属性。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型 | 说明 |
| ------------------------------------- | ------------- |
| [SystemBarProperties](#systembarproperties) | 当前导航栏、状态栏属性。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300003 | This window manager service works abnormally. |
| 1300004 | Unauthorized operation.                       |


**示例：**

```ts
// EntryAbility.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    let windowClass: window.Window | undefined = undefined;
    windowStage.getMainWindow((err: BusinessError, data) => {
      const errCode: number = err.code;
      if (errCode) {
        console.error('Failed to obtain the main window. Cause: ' + JSON.stringify(err));
        return;
      }
      windowClass = data;
      try {
        let systemBarProperty = windowClass.getWindowSystemBarProperties();
        console.info('Success in obtaining system bar properties. Property: ' + JSON.stringify(systemBarProperty));
      } catch (err) {
        console.error('Failed to get system bar properties. Code: ' + JSON.stringify(err));
      }
    });
  }
};
```

### setPreferredOrientation<sup>9+</sup>

setPreferredOrientation(orientation: Orientation, callback: AsyncCallback&lt;void&gt;): void

设置窗口的显示方向属性，使用callback异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名              | 类型                                        | 必填 | 说明                   |
| ------------------- | ------------------------------------------- | ---- | ---------------------- |
| Orientation         | [Orientation](#orientation9)                | 是   | 窗口显示方向的属性。         |
| callback            | AsyncCallback&lt;void&gt;                   | 是   | 回调函数。             |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let orientation = window.Orientation.AUTO_ROTATION;
try {
  windowClass.setPreferredOrientation(orientation, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set window orientation. Cause: ' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting window orientation.');
  });
} catch (exception) {
  console.error('Failed to set window orientation. Cause: ' + JSON.stringify(exception));
}
```

### setPreferredOrientation<sup>9+</sup>

setPreferredOrientation(orientation: Orientation): Promise&lt;void&gt;

设置窗口的显示方向属性，使用Promise异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名              | 类型                                        | 必填 | 说明                   |
| ------------------- | ------------------------------------------- | ---- | ---------------------- |
| Orientation         | [Orientation](#orientation9)                | 是   | 窗口显示方向的属性。       |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let orientation = window.Orientation.AUTO_ROTATION;
try {
  let promise = windowClass.setPreferredOrientation(orientation);
  promise.then(() => {
    console.info('Succeeded in setting the window orientation.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the window orientation. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set window orientation. Cause: ' + JSON.stringify(exception));
}
```

### getUIContext<sup>10+</sup>

getUIContext(): UIContext

获取UIContext实例。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型       | 说明                   |
| ---------- | ---------------------- |
| [UIContext](js-apis-arkui-UIContext.md#uicontext) | 返回UIContext实例对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
import { UIContext } from '@ohos.arkui.UIContext';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    // 为主窗口加载对应的目标页面。
    windowStage.loadContent("pages/page2", (err: BusinessError) => {
      let errCode: number = err.code;
      if (errCode) {
        console.error('Failed to load the content. Cause:' + JSON.stringify(err));
        return;
      }
      console.info('Succeeded in loading the content.');
      // 获取应用主窗口。
      let windowClass: window.Window | undefined = undefined;
      windowStage.getMainWindow((err: BusinessError, data) => {
        let errCode: number = err.code;
        if (errCode) {
          console.error('Failed to obtain the main window. Cause: ' + JSON.stringify(err));
          return;
        }
        windowClass = data;
        console.info('Succeeded in obtaining the main window. Data: ' + JSON.stringify(data));
        // 获取UIContext实例。
        let uiContext: UIContext | null = null;
        uiContext = windowClass.getUIContext();
      })
    });
  }
};
```

### setUIContent<sup>9+</sup>

setUIContent(path: string, callback: AsyncCallback&lt;void&gt;): void

根据当前工程中某个页面的路径为窗口加载具体页面内容，使用callback异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | ------------------------- | -- | -------------------- |
| path     | string                    | 是 | 要加载到窗口中的页面内容的路径，Stage模型下该路径需添加到工程的main_pages.json文件中，FA模型下该路径需添加到工程的config.json文件中。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。          |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  windowClass.setUIContent('pages/page2/page3', (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in loading the content.');
  });
} catch (exception) {
  console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
}
```

### setUIContent<sup>9+</sup>

setUIContent(path: string): Promise&lt;void&gt;

根据当前工程中某个页面的路径为窗口加载具体页面内容，使用Promise异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ---- | ------ | -- | ------------------ |
| path | string | 是 | 要加载到窗口中的页面内容的路径，Stage模型下该路径需添加到工程的main_pages.json文件中，FA模型下该路径需添加到工程的config.json文件中。 |

**返回值：**

| 类型 | 说明 |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let promise = windowClass.setUIContent('pages/page2/page3');
  promise.then(() => {
    console.info('Succeeded in loading the content.');
  }).catch((err: BusinessError) => {
    console.error('Failed to load the content. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to load the content. Cause: ' + JSON.stringify(exception));
}
```

### loadContent<sup>9+</sup>

loadContent(path: string, storage: LocalStorage, callback: AsyncCallback&lt;void&gt;): void

根据当前工程中某个页面的路径为窗口加载具体页面内容，通过LocalStorage传递状态属性给加载的页面，使用callback异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                            | 必填 | 说明                                                         |
| -------- | ----------------------------------------------- | ---- | ------------------------------------------------------------ |
| path     | string                                          | 是   | 要加载到窗口中的页面内容的路径，该路径需添加到工程的main_pages.json文件中。 |
| storage  | [LocalStorage](../../quick-start/arkts-localstorage.md) | 是   | 页面级UI状态存储单元，这里用于为加载到窗口的页面内容传递状态属性。 |
| callback | AsyncCallback&lt;void&gt;                       | 是   | 回调函数。                                                   |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let storage: LocalStorage = new LocalStorage();
    storage.setOrCreate('storageSimpleProp', 121);
    try {
      if (!windowClass) {
        console.info('Failed to load the content. Cause: windowClass is null');
      }
      else {
        (windowClass as window.Window).loadContent('pages/page2', storage, (err: BusinessError) => {
          const errCode: number = err.code;
          if (errCode) {
            console.error('Failed to load the content. Cause:' + JSON.stringify(err));
            return;
          }
          console.info('Succeeded in loading the content.');
        });
      }
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```

### loadContent<sup>9+</sup>

loadContent(path: string, storage: LocalStorage): Promise&lt;void&gt;

根据当前工程中某个页面的路径为窗口加载具体页面内容，通过LocalStorage传递状态属性给加载的页面，使用Promise异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名  | 类型                                            | 必填 | 说明                                                         |
| ------- | ----------------------------------------------- | ---- | ------------------------------------------------------------ |
| path    | string                                          | 是   | 要加载到窗口中的页面内容的路径，该路径需添加到工程的main_pages.json文件中。 |
| storage | [LocalStorage](../../quick-start/arkts-localstorage.md) | 是   | 页面级UI状态存储单元，这里用于为加载到窗口的页面内容传递状态属性。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let storage: LocalStorage = new LocalStorage();
    storage.setOrCreate('storageSimpleProp', 121);
    try {
      if (!windowClass) {
        console.info('Failed to load the content. Cause: windowClass is null');
      }
      else {
        let promise = (windowClass as window.Window).loadContent('pages/page2', storage);
        promise.then(() => {
          console.info('Succeeded in loading the content.');
        }).catch((err: BusinessError) => {
          console.error('Failed to load the content. Cause:' + JSON.stringify(err));
        });
      }
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```

### loadContentByName<sup>11+</sup>

loadContentByName(name: string, storage: LocalStorage, callback: AsyncCallback&lt;void&gt;): void

为当前窗口加载[命名路由](../../ui/arkts-routing.md#命名路由)页面，通过LocalStorage传递状态属性给加载的页面，使用callback异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                                    | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| name     | string                                                  | 是   | 命名路由页面的名称。                                             |
| storage  | [LocalStorage](../../quick-start/arkts-localstorage.md) | 是   | 页面级UI状态存储单元，这里用于为加载到窗口的页面内容传递状态属性。 |
| callback | AsyncCallback&lt;void&gt;                               | 是   | 回调函数。                                                   |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                                      |
| -------- | --------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |

**示例：**

```ts
// ets/entryability/EntryAbility.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
import * as Index from '../pages/Index'; // 导入命名路由页面

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window = windowStage.getMainWindowSync(); // 获取应用主窗口
    let storage: LocalStorage = new LocalStorage();
    storage.setOrCreate('storageSimpleProp', 121);
    try {
      if (!windowClass) {
        console.info('Failed to load the content. Cause: windowClass is null');
      } else {
        (windowClass as window.Window).loadContentByName(Index.entryName, storage, (err: BusinessError) => {
          const errCode: number = err.code;
          if (errCode) {
            console.error('Failed to load the content. Cause:' + JSON.stringify(err));
            return;
          }
          console.info('Succeeded in loading the content.');
        });
      }
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```
```ts
// ets/pages/Index.ets
export const entryName : string = 'Index';
@Entry({routeName: entryName, storage : LocalStorage.getShared()})
@Component
export struct Index {
  @State message: string = 'Hello World'
  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

### loadContentByName<sup>11+</sup>

loadContentByName(name: string, callback: AsyncCallback&lt;void&gt;): void

为当前窗口加载[命名路由](../../ui/arkts-routing.md#命名路由)页面内容，使用callback异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明             |
| -------- | ------------------------- | ---- | ---------------- |
| name     | string                    | 是   | 命名路由页面的名称。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。       |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                                      |
| -------- | --------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |

**示例：**

```ts
// ets/entryability/EntryAbility.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
import * as Index from '../pages/Index'; // 导入命名路由页面

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window = windowStage.getMainWindowSync(); // 获取应用主窗口
    try {
      if (!windowClass) {
        console.info('Failed to load the content. Cause: windowClass is null');
      } else {
        (windowClass as window.Window).loadContentByName(Index.entryName, (err: BusinessError) => {
          const errCode: number = err.code;
          if (errCode) {
            console.error('Failed to load the content. Cause:' + JSON.stringify(err));
            return;
          }
          console.info('Succeeded in loading the content.');
        });
      }
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```
```ts
// ets/pages/Index.ets
export const entryName : string = 'Index';
@Entry({routeName: entryName})
@Component
export struct Index {
  @State message: string = 'Hello World'
  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

### loadContentByName<sup>11+</sup>

loadContentByName(name: string, storage?: LocalStorage): Promise&lt;void&gt;

为当前窗口加载[命名路由](../../ui/arkts-routing.md#命名路由)页面，通过LocalStorage传递状态属性给加载的页面，使用Promise异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名  | 类型                                                    | 必填 | 说明                                                         |
| ------- | ------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| name    | string                                                  | 是   | 命名路由页面的名称。                                             |
| storage | [LocalStorage](../../quick-start/arkts-localstorage.md) | 否   | 页面级UI状态存储单元，这里用于为加载到窗口的页面内容传递状态属性。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                                      |
| -------- | --------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |

**示例：**

```ts
// ets/entryability/EntryAbility.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
import * as Index from '../pages/Index'; // 导入命名路由页面

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window = windowStage.getMainWindowSync(); // 获取应用主窗口
    let storage: LocalStorage = new LocalStorage();
    storage.setOrCreate('storageSimpleProp', 121);
    try {
      if (!windowClass) {
        console.info('Failed to load the content. Cause: windowClass is null');
      } else {
        let promise = (windowClass as window.Window).loadContentByName(Index.entryName, storage);
        promise.then(() => {
          console.info('Succeeded in loading the content.');
        }).catch((err: BusinessError) => {
          console.error('Failed to load the content. Cause:' + JSON.stringify(err));
        });
      }
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```
```ts
// ets/pages/Index.ets
export const entryName : string = 'Index';
@Entry({routeName: entryName, storage : LocalStorage.getShared()})
@Component
export struct Index {
  @State message: string = 'Hello World'
  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

### isWindowShowing<sup>9+</sup>

isWindowShowing(): boolean

判断当前窗口是否已显示。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型 | 说明 |
| ------- | ------------------------------------------------------------------ |
| boolean | 当前窗口是否已显示。true表示当前窗口已显示，false则表示当前窗口未显示。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
try {
  let data = windowClass.isWindowShowing();
  console.info('Succeeded in checking whether the window is showing. Data: ' + JSON.stringify(data));
} catch (exception) {
  console.error('Failed to check whether the window is showing. Cause: ' + JSON.stringify(exception));
}
```

### on('windowSizeChange')<sup>7+</sup>

on(type:  'windowSizeChange', callback: Callback&lt;Size&gt;): void

开启窗口尺寸变化的监听。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                           | 必填 | 说明                                                     |
| -------- | ------------------------------ | ---- | -------------------------------------------------------- |
| type     | string                         | 是   | 监听事件，固定为'windowSizeChange'，即窗口尺寸变化事件。 |
| callback | Callback&lt;[Size](#size7)&gt; | 是   | 回调函数。返回当前的窗口尺寸。                           |

**示例：**

```ts
try {
  windowClass.on('windowSizeChange', (data) => {
    console.info('Succeeded in enabling the listener for window size changes. Data: ' + JSON.stringify(data));
  });
} catch (exception) {
  console.error('Failed to enable the listener for window size changes. Cause: ' + JSON.stringify(exception));
}
```

### off('windowSizeChange')<sup>7+</sup>

off(type: 'windowSizeChange', callback?: Callback&lt;Size&gt;): void

关闭窗口尺寸变化的监听。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                          | 必填 | 说明                                                     |
| -------- | ----------------------------- | ---- | -------------------------------------------------------- |
| type     | string                        | 是   | 监听事件，固定为'windowSizeChange'，即窗口尺寸变化事件。 |
| callback | Callback&lt;[Size](#size7)&gt; | 否   | 回调函数。返回当前的窗口尺寸。如果传入参数，则关闭该监听。如果未传入参数，则关闭窗口尺寸变化的监听。                           |

**示例：**

```ts
try {
  windowClass.off('windowSizeChange');
} catch (exception) {
  console.error('Failed to disable the listener for window size changes. Cause: ' + JSON.stringify(exception));
}
```

### on('avoidAreaChange')<sup>9+</sup>

on(type: 'avoidAreaChange', callback: Callback&lt;{ type: AvoidAreaType, area: AvoidArea}&gt;): void

开启系统规避区变化的监听。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                                               | 必填 | 说明                                   |
| -------- |------------------------------------------------------------------| ---- |--------------------------------------|
| type     | string                                                           | 是   | 监听事件，固定为'avoidAreaChange'，即系统规避区变化事件。 |
| callback | Callback&lt;{ type: [AvoidAreaType](#avoidareatype7), area: [AvoidArea](#avoidarea7) }&gt; | 是   | 回调函数。返回当前规避区以及规避区类型。|

**示例：**

```ts
try {
  windowClass.on('avoidAreaChange', (data) => {
    console.info('Succeeded in enabling the listener for system avoid area changes. type:' +
    JSON.stringify(data.type) + ', area: ' + JSON.stringify(data.area));
  });
} catch (exception) {
  console.error('Failed to enable the listener for system avoid area changes. Cause: ' + JSON.stringify(exception));
}
```

### off('avoidAreaChange')<sup>9+</sup>

off(type: 'avoidAreaChange', callback?: Callback&lt;{ type: AvoidAreaType, area: AvoidArea }&gt;): void

关闭系统规避区变化的监听。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                                                          | 必填  | 说明                                 |
| -------- |-----------------------------------------------------------------------------|-----|------------------------------------|
| type     | string                                                                      | 是   | 监听事件，固定为'avoidAreaChange'，即系统规避区变化事件。 |
| callback | Callback&lt;{ type: [AvoidAreaType](#avoidareatype7), area: [AvoidArea](#avoidarea7) }&gt; | 否   | 回调函数。返回当前规避区以及规避区类型。如果传入参数，则关闭该监听。如果未传入参数，则关闭所有系统规避区变化的监听。|

**示例：**

```ts
try {
  windowClass.off('avoidAreaChange');
} catch (exception) {
  console.error('Failed to disable the listener for system avoid area changes. Cause: ' + JSON.stringify(exception));
}
```

### on('keyboardHeightChange')<sup>7+</sup>

on(type: 'keyboardHeightChange', callback: Callback&lt;number&gt;): void

开启固定态输入法窗口软键盘高度变化的监听。从API version 10开始，改变输入法窗口为固定态或者悬浮态方法详细介绍请参见[输入法服务](../apis-ime-kit/js-apis-inputmethodengine.md#changeflag10)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                | 必填 | 说明                                        |
| -------- | ------------------- | ---- |-------------------------------------------|
| type     | string              | 是   | 监听事件，固定为'keyboardHeightChange'，即键盘高度变化事件。 |
| callback | Callback&lt;number&gt; | 是   | 回调函数。返回当前的键盘高度，返回值为整数，单位为px。     |

**示例：**

```ts
try {
  windowClass.on('keyboardHeightChange', (data) => {
    console.info('Succeeded in enabling the listener for keyboard height changes. Data: ' + JSON.stringify(data));
  });
} catch (exception) {
  console.error('Failed to enable the listener for keyboard height changes. Cause: ' + JSON.stringify(exception));
}
```

### off('keyboardHeightChange')<sup>7+</sup>

off(type: 'keyboardHeightChange', callback?: Callback&lt;number&gt;): void

关闭固定态输入法窗口软键盘高度变化的监听。从API version 10开始，改变输入法窗口为固定态或者悬浮态方法详细介绍请参见[输入法服务](../apis-ime-kit/js-apis-inputmethodengine.md#changeflag10)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                   | 必填 | 说明                                                         |
| -------- | ---------------------- | ---- | ------------------------------------------------------------ |
| type     | string                 | 是   | 监听事件，固定为'keyboardHeightChange'，即键盘高度变化事件。 |
| callback | Callback&lt;number&gt; | 否   | 回调函数。返回当前的键盘高度，返回值为整数，单位为px。若传入参数，则关闭该监听。如果未传入参数，则关闭所有固定态输入法窗口软键盘高度变化的监听。                               |

**示例：**

```ts
try {
  windowClass.off('keyboardHeightChange');
} catch (exception) {
  console.error('Failed to disable the listener for keyboard height changes. Cause: ' + JSON.stringify(exception));
}
```

### on('touchOutside')<sup>11+</sup>

on(type: 'touchOutside', callback: Callback&lt;void&gt;): void

开启本窗口区域范围外的点击事件的监听。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                | 必填 | 说明                                                         |
| -------- | ------------------- | ---- | ------------------------------------------------------------ |
| type     | string              | 是   | 监听事件，固定为'touchOutside'，即本窗口范围外的点击事件。 |
| callback | Callback&lt;void&gt; | 是   | 回调函数。当点击事件发生在本窗口范围之外的回调。                               |

**示例：**

```ts
try {
  windowClass.on('touchOutside', () => {
    console.info('touch outside');
  });
} catch (exception) {
  console.error('Failed to register callback. Cause: ' + JSON.stringify(exception));
}
```

### off('touchOutside')<sup>11+</sup>

off(type: 'touchOutside', callback?: Callback&lt;void&gt;): void

关闭本窗口区域范围外的点击事件的监听。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                   | 必填 | 说明                                   |
| -------- |----------------------| ---- |--------------------------------------|
| type     | string               | 是   | 监听事件，固定为'touchOutside'，即本窗口范围外的点击事件。 |
| callback | Callback&lt;void&gt; | 否   | 回调函数。当点击事件发生在本窗口范围之外的回调。如果传入参数，则关闭该监听。如果未传入参数，则关闭所有本窗口区域范围外的点击事件的监听。            |

**示例：**

```ts
try {
  windowClass.off('touchOutside');
} catch (exception) {
  console.error('Failed to unregister callback. Cause: ' + JSON.stringify(exception));
}
```

### on('screenshot')<sup>9+</sup>

on(type: 'screenshot', callback: Callback&lt;void&gt;): void

开启截屏事件的监听。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                | 必填 | 说明                                                         |
| -------- | ------------------- | ---- | ------------------------------------------------------------ |
| type     | string              | 是   | 监听事件，固定为'screenshot'，即截屏事件。 |
| callback | Callback&lt;void&gt; | 是   | 回调函数。发生截屏事件时的回调。                               |

**示例：**

```ts
try {
  windowClass.on('screenshot', () => {
    console.info('screenshot happened');
  });
} catch (exception) {
  console.error('Failed to register callback. Cause: ' + JSON.stringify(exception));
}
```

### off('screenshot')<sup>9+</sup>

off(type: 'screenshot', callback?: Callback&lt;void&gt;): void

关闭截屏事件的监听。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                   | 必填 | 说明                                                         |
| -------- | ---------------------- | ---- | ------------------------------------------------------------ |
| type     | string                 | 是   | 监听事件，固定为'screenshot'，即截屏事件。 |
| callback | Callback&lt;void&gt; | 否   | 回调函数。发生截屏事件时的回调。若传入参数，则关闭该监听。若未传入参数，则关闭所有截屏事件的监听。 |

**示例：**

```ts
let callback = () => {
  console.info('screenshot happened');
};
try {
  windowClass.on('screenshot', callback);
} catch (exception) {
  console.error('Failed to register callback. Cause: ' + JSON.stringify(exception));
}
try {
  windowClass.off('screenshot', callback);
  // 如果通过on开启多个callback进行监听，同时关闭所有监听：
  windowClass.off('screenshot');
} catch (exception) {
  console.error('Failed to unregister callback. Cause: ' + JSON.stringify(exception));
}
```

### on('dialogTargetTouch')<sup>10+</sup>

on(type: 'dialogTargetTouch', callback: Callback&lt;void&gt;): void

开启模态窗口目标窗口的点击事件的监听。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                                          |
| -------- | ------------------- | ---- | ------------------------------------------------------------ |
| type     | string              | 是   | 监听事件，固定为'dialogTargetTouch'，即模态窗口目标窗口的点击事件。 |
| callback | Callback&lt;void&gt;| 是   | 回调函数。当点击事件发生在模态窗口目标窗口的回调。 |

**示例：**

```ts
try {
  windowClass.on('dialogTargetTouch', () => {
    console.info('touch dialog target');
  });
} catch (exception) {
  console.error('Failed to register callback. Cause: ' + JSON.stringify(exception));
}
```

### off('dialogTargetTouch')<sup>10+</sup>

off(type: 'dialogTargetTouch', callback?: Callback&lt;void&gt;): void

关闭模态窗口目标窗口的点击事件的监听。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                    | 必填 | 说明                                                          |
| -------- | ---------------------- | ---- | ------------------------------------------------------------ |
| type     | string                 | 是   | 监听事件，固定为'dialogTargetTouch'，即模态窗口目标窗口的点击事件。 |
| callback | Callback&lt;void&gt;      | 否   | 回调函数。当点击事件发生在模态窗口目标窗口的回调。若传入参数，则关闭该监听。若未传入参数，则关闭所有模态窗口目标窗口的点击事件的监听。 |

**示例：**

```ts
try {
  windowClass.off('dialogTargetTouch');
} catch (exception) {
  console.error('Failed to unregister callback. Cause: ' + JSON.stringify(exception));
}
```

### on('windowEvent')<sup>10+</sup>

on(type: 'windowEvent', callback: Callback&lt;WindowEventType&gt;): void

开启窗口生命周期变化的监听。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                                       | 必填 | 说明                                                         |
| -------- | ---------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                                     | 是   | 监听事件，固定为'windowEvent'，即窗口生命周期变化事件。 |
| callback | Callback&lt;[WindowEventType](#windoweventtype10)&gt; | 是   | 回调函数。返回当前的窗口生命周期状态。                 |

**示例：**

```ts
try {
  windowClass.on('windowEvent', (data) => {
    console.info('Window event happened. Event:' + JSON.stringify(data));
  });
} catch (exception) {
  console.error('Failed to register callback. Cause: ' + JSON.stringify(exception));
}
```

### off('windowEvent')<sup>10+</sup>

off(type: 'windowEvent', callback?: Callback&lt;WindowEventType &gt;): void

关闭窗口生命周期变化的监听。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                                       | 必填 | 说明                                                         |
| -------- | ---------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                                     | 是   | 监听事件，固定为'windowEvent'，即窗口生命周期变化事件。 |
| callback | Callback&lt;[WindowEventType](#windoweventtype10)&gt; | 否   | 回调函数。返回当前的窗口生命周期状态。若传入参数，则关闭该监听。若未传入参数，则关闭所有窗口生命周期变化的监听。                 |

**示例：**

```ts
try {
  windowClass.off('windowEvent');
} catch (exception) {
  console.error('Failed to unregister callback. Cause: ' + JSON.stringify(exception));
}
```

### on('windowVisibilityChange')<sup>11+</sup>

on(type: 'windowVisibilityChange', callback: Callback&lt;boolean&gt;): void

开启本窗口可见状态变化事件的监听。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名   | 类型                       | 必填 | 说明                                                         |
| -------- | --------------------------| ---- | ------------------------------------------------------------ |
| type     | string                    | 是   | 监听事件，固定为'windowVisibilityChange'，即本窗口可见状态变化的事件。 |
| callback | Callback&lt;boolean&gt;   | 是   | 回调函数。当本窗口可见状态发生变化后的回调。回调函数返回boolean类型参数，当返回参数为true时表示窗口可见，否则表示窗口不可见。                               |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal.                |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
try {
  windowClass.on('windowVisibilityChange', (boolean) => {
    console.info('Window visibility changed, isVisible=' + boolean);
  });
} catch (exception) {
  console.error('Failed to register callback. Cause: ' + JSON.stringify(exception));
}
```

### off('windowVisibilityChange')<sup>11+</sup>

off(type: 'windowVisibilityChange', callback?: Callback&lt;boolean&gt;): void

关闭本窗口可见状态变化事件的监听。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名   | 类型                        | 必填 | 说明                                   |
| -------- |----------------------------| ---- |--------------------------------------|
| type     | string                     | 是   | 监听事件，固定为'windowVisibilityChange'，即本窗口可见状态变化的事件。 |
| callback | Callback&lt;boolean&gt;    | 否   | 回调函数。当本窗口可见状态发生变化时的回调。如果传入参数，则关闭该监听。如果未传入参数，则关闭所有本窗口可见状态变化事件的回调。            |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal.                |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
try {
  windowClass.off('windowVisibilityChange');
} catch (exception) {
  console.error('Failed to unregister callback. Cause: ' + JSON.stringify(exception));
}
```

### on('noInteractionDetected')<sup>12+</sup>

on(type: 'noInteractionDetected', timeout: number, callback: Callback&lt;void&gt;): void

开启本窗口在指定超时时间内无交互事件的监听，交互事件支持物理键盘输入事件和屏幕触控点击事件，不支持软键盘输入事件。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名   | 类型                       | 必填 | 说明                                                         |
| -------- | --------------------------| ---- | ------------------------------------------------------------ |
| type     | string                    | 是   | 监听事件，固定为'noInteractionDetected'，即本窗口在指定超时时间内无交互的事件。 |
| timeout     | number                    | 是   | 指定本窗口在多长时间内无交互即回调，单位为秒(s)。该参数仅支持整数输入，负数和小数为非法参数。 |
| callback | Callback&lt;void&gt;      | 是   | 回调函数。当本窗口在指定超时时间内无交互事件时的回调。  |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal.                |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
try {
  windowClass.on('noInteractionDetected', 60, () => {
    console.info('no interaction in 60s');
  });
} catch (exception) {
  console.error('Failed to register callback. Cause: ' + JSON.stringify(exception));
}
```

### off('noInteractionDetected')<sup>12+</sup>

off(type: 'noInteractionDetected', callback?: Callback&lt;void&gt;): void

关闭本窗口在指定超时时间内无交互事件的监听，交互事件支持物理键盘输入事件和屏幕触控点击事件，不支持软键盘输入事件。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名   | 类型                        | 必填 | 说明                                   |
| -------- |----------------------------| ---- |--------------------------------------|
| type     | string                     | 是   | 监听事件，固定为'noInteractionDetected'，即本窗口在指定超时时间内无交互的事件。 |
| callback | Callback&lt;void&gt;    | 否   | 回调函数，当本窗口在指定超时时间内无交互事件时的回调。如果传入参数，则关闭该监听。如果未传入参数，则关闭所有本窗口在指定超时时间内无交互事件的监听。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal.                |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
try {
  windowClass.off('noInteractionDetected');
} catch (exception) {
  console.error('Failed to unregister callback. Cause: ' + JSON.stringify(exception));
}
```

### on('windowStatusChange')<sup>11+</sup>

on(type:  'windowStatusChange', callback: Callback&lt;WindowStatusType&gt;): void

开启窗口模式变化的监听。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名   | 类型                           | 必填 | 说明                                                     |
| -------- | ------------------------------ | ---- | -------------------------------------------------------- |
| type     | string                         | 是   | 监听事件，固定为'windowStatusChange'，即窗口模式变化事件。 |
| callback | Callback&lt;[WindowStatusType](#windowstatustype11)&gt; | 是   | 回调函数。返回当前的窗口模式。                           |

**示例：**

```ts
try {
  windowClass.on('windowStatusChange', (WindowStatusType) => {
      console.info('Succeeded in enabling the listener for window status changes. Data: ' + JSON.stringify(WindowStatusType));
  });
} catch (exception) {
  console.error('Failed to enable the listener for window status changes. Cause: ' + JSON.stringify(exception));
}
```

### off('windowStatusChange')<sup>11+</sup>

off(type: 'windowStatusChange', callback?: Callback&lt;WindowStatusType&gt;): void

关闭窗口模式变化的监听。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名   | 类型                          | 必填 | 说明                                                     |
| -------- | ----------------------------- | ---- | -------------------------------------------------------- |
| type     | string                        | 是   | 监听事件，固定为'windowStatusChange'，即窗口模式变化事件。 |
| callback | Callback&lt;[WindowStatusType](#windowstatustype11)&gt; | 否   | 回调函数。返回当前的窗口模式。如果传入参数，则关闭该监听。如果未传入参数，则关闭所有窗口模式变化的监听。                           |

**示例：**

```ts
try {
  windowClass.off('windowStatusChange');
} catch (exception) {
  console.error('Failed to disable the listener for window status changes. Cause: ' + JSON.stringify(exception));
}
```

### on('windowTitleButtonRectChange')<sup>11+</sup>

on(type: 'windowTitleButtonRectChange', callback: Callback&lt;TitleButtonRect&gt;): void

开启标题栏上的最小化、最大化、关闭按钮矩形区域变化的监听。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名   | 类型                                                  | 必填 | 说明                                                         |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                                | 是   | 监听事件，固定为'windowTitleButtonRectChange'，即标题栏上的最小化、最大化、关闭按钮矩形区域变化事件。 |
| callback | Callback&lt;[TitleButtonRect](#titlebuttonrect11)&gt; | 是   | 回调函数。返回当前标题栏上的最小化、最大化、关闭按钮矩形区域。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                       |
| -------- | ------------------------------ |
| 1300002  | This window state is abnormal. |

**示例：**

```ts
try {
  windowClass.on('windowTitleButtonRectChange', (titleButtonRect) => {
      console.info('Succeeded in enabling the listener for window title buttons area changes. Data: ' + JSON.stringify(titleButtonRect));
  });
} catch (exception) {
  console.error('Failed to enable the listener for window title buttons area changes. Cause: ' + JSON.stringify(exception));
}
```

### off('windowTitleButtonRectChange')<sup>11+</sup>

off(type: 'windowTitleButtonRectChange', callback?: Callback&lt;TitleButtonRect&gt;): void

关闭标题栏上的最小化、最大化、关闭按钮矩形区域变化的监听。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名   | 类型                                                  | 必填 | 说明                                                         |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                                | 是   | 监听事件，固定为'windowTitleButtonRectChange'，即标题栏上的最小化、最大化、关闭按钮矩形区域变化事件。 |
| callback | Callback&lt;[TitleButtonRect](#titlebuttonrect11)&gt; | 否   | 回调函数。返回当前标题栏上的最小化、最大化、关闭按钮矩形区域。如果传入参数，则关闭该监听。如果未传入参数，则关闭所有标题栏上的最小化、最大化、关闭按钮矩形区域变化的监听。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                       |
| -------- | ------------------------------ |
| 1300002  | This window state is abnormal. |

**示例：**

```ts
try {
  windowClass.off('windowTitleButtonRectChange');
} catch (exception) {
  console.error('Failed to disable the listener for window title buttons area changes. Cause: ' + JSON.stringify(exception));
}
```

### on('windowRectChange')<sup>12+</sup>

on(type:  'windowRectChange', callback: Callback&lt;RectChangeOptions&gt;): void

开启窗口矩形（窗口位置及窗口大小）变化的监听。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名   | 类型                           | 必填 | 说明                                                     |
| -------- | ------------------------------ | ---- | -------------------------------------------------------- |
| type     | string                         | 是   | 监听事件，固定为'windowRectChange'，即窗口矩形变化事件。 |
| callback | Callback&lt;[RectChangeOptions](#rectchangeoptions12)&gt; | 是   | 回调函数。返回当前窗口矩形变化值及变化原因。                           |

**示例：**

```ts
windowClass.on('windowRectChange', (data: window.RectChangeOptions) => {
    console.info('Succeeded window rect changes. Data: ' + JSON.stringify(data));
});
```

### off('windowRectChange')<sup>12+</sup>

off(type: 'windowRectChange', callback?: Callback&lt;RectChangeOptions&gt;): void

关闭窗口矩形（窗口位置及窗口大小）变化的监听。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名   | 类型                           | 必填 | 说明                                                         |
| -------- | ------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                         | 是   | 监听事件，固定为'windowRectChange'，即窗口矩形变化事件。     |
| callback | Callback&lt;[RectChangeOptions](#rectchangeoptions12)&gt; | 否   | 回调函数。返回当前的窗口矩形及变化原因。如果传入参数，则关闭该监听。如果未传入参数，则关闭所有窗口矩形变化的监听。 |

**示例：**

```ts
windowClass.off('windowRectChange');
```

### isWindowSupportWideGamut<sup>9+</sup>

isWindowSupportWideGamut(callback: AsyncCallback&lt;boolean&gt;): void

判断当前窗口是否支持广色域模式，使用callback异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | ---------------------------- | -- | -------------------------------------------------------------------------------- |
| callback | AsyncCallback&lt;boolean&gt; | 是 | 回调函数。返回true表示当前窗口支持广色域模式，返回false表示当前窗口不支持广色域模式。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

windowClass.isWindowSupportWideGamut((err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to check whether the window support WideGamut. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in checking whether the window support WideGamut Data: ' + JSON.stringify(data));
});
```

### isWindowSupportWideGamut<sup>9+</sup>

isWindowSupportWideGamut(): Promise&lt;boolean&gt;

判断当前窗口是否支持广色域模式，使用Promise异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型 | 说明 |
| ---------------------- | ------------------------------------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise对象。返回true表示当前窗口支持广色域模式，返回false表示当前窗口不支持广色域模式。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.isWindowSupportWideGamut();
promise.then((data) => {
  console.info('Succeeded in checking whether the window support WideGamut. Data: ' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to check whether the window support WideGamut. Cause: ' + JSON.stringify(err));
});
```

### setWindowColorSpace<sup>9+</sup>

setWindowColorSpace(colorSpace:ColorSpace, callback: AsyncCallback&lt;void&gt;): void

设置当前窗口为广色域模式或默认色域模式，使用callback异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ---------- | ------------------------- | -- | ----------- |
| colorSpace | [ColorSpace](#colorspace8) | 是 | 设置色域模式。 |
| callback   | AsyncCallback&lt;void&gt; | 是 | 回调函数。   |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  windowClass.setWindowColorSpace(window.ColorSpace.WIDE_GAMUT, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set window colorspace. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting window colorspace.');
  });
} catch (exception) {
  console.error('Failed to set window colorspace. Cause:' + JSON.stringify(exception));
}
```

### setWindowColorSpace<sup>9+</sup>

setWindowColorSpace(colorSpace:ColorSpace): Promise&lt;void&gt;

设置当前窗口为广色域模式或默认色域模式，使用Promise异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ---------- | ------------------------- | -- | ------------- |
| colorSpace | [ColorSpace](#colorspace8) | 是 | 设置色域模式。 |

**返回值：**

| 类型 | 说明 |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let promise = windowClass.setWindowColorSpace(window.ColorSpace.WIDE_GAMUT);
  promise.then(() => {
    console.info('Succeeded in setting window colorspace.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set window colorspace. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set window colorspace. Cause:' + JSON.stringify(exception));
}
```

### getWindowColorSpace<sup>9+</sup>

getWindowColorSpace(): ColorSpace

获取当前窗口色域模式。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型 | 说明 |
| ------------------------- | ------------- |
| [ColorSpace](#colorspace8) | 当前色域模式。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
let colorSpace = windowClass.getWindowColorSpace();
```

### setWindowBackgroundColor<sup>9+</sup>

setWindowBackgroundColor(color: string): void

设置窗口的背景色。Stage模型下，该接口需要在[loadContent()](#loadcontent9)或[setUIContent()](#setuicontent9)调用生效后使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ----- | ------ | -- | ----------------------------------------------------------------------- |
| color | string | 是 | 需要设置的背景色，为十六进制RGB或ARGB颜色，不区分大小写，例如`#00FF00`或`#FF00FF00`。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

private SetUIContent(windowClass: window.Window) {
    windowClass.setUIContent("pages/ButtonWindow",(err: BusinessError) => {
      if (err.code) {
        console.error('Failed to load the content. Cause:' + JSON.stringify(err));
        return;
      }
      console.info('Succeeded in loading the content.');
      let color: string = '#00ff33';
      try {
        windowClass.setWindowBackgroundColor(color);
      } catch (exception) {
        console.error('Failed to set the background color. Cause: ' + JSON.stringify(exception));
      };
    });
}
```

### setWindowBrightness<sup>9+</sup>

setWindowBrightness(brightness: number, callback: AsyncCallback&lt;void&gt;): void

允许应用窗口设置屏幕亮度值，使用callback异步回调。

当前屏幕亮度规格：窗口设置屏幕亮度生效时，控制中心不可以调整系统屏幕亮度，窗口恢复默认系统亮度之后，控制中心可以调整系统屏幕亮度。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                                        |
| ---------- | ------------------------- | -- |-------------------------------------------|
| brightness | number                    | 是 | 屏幕亮度值。该参数为浮点数，取值范围为[0.0, 1.0]或-1.0。1.0表示最亮，-1.0表示默认亮度。 |
| callback   | AsyncCallback&lt;void&gt; | 是 | 回调函数。                                     |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let brightness: number = 1;
try {
  windowClass.setWindowBrightness(brightness, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the brightness. Cause: ' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the brightness.');
  });
} catch (exception) {
  console.error('Failed to set the brightness. Cause: ' + JSON.stringify(exception));
}
```

### setWindowBrightness<sup>9+</sup>

setWindowBrightness(brightness: number): Promise&lt;void&gt;

允许应用窗口设置屏幕亮度值，使用Promise异步回调。

当前屏幕亮度规格：窗口设置屏幕亮度生效时，控制中心不可以调整系统屏幕亮度，窗口恢复默认系统亮度之后，控制中心可以调整系统屏幕亮度。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                                     |
| ---------- | ------ | -- |----------------------------------------|
| brightness | number | 是 | 屏幕亮度值。该参数为浮点数，取值范围为[0.0, 1.0]或-1.0。1.0表示最亮，-1.0表示默认亮度。 |

**返回值：**

| 类型 | 说明 |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let brightness: number = 1;
try {
  let promise = windowClass.setWindowBrightness(brightness);
  promise.then(() => {
    console.info('Succeeded in setting the brightness.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the brightness. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the brightness. Cause: ' + JSON.stringify(exception));
}
```

### setWindowFocusable<sup>9+</sup>

setWindowFocusable(isFocusable: boolean, callback: AsyncCallback&lt;void&gt;): void

设置点击时是否支持切换焦点窗口，使用callback异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ----------- | ------------------------- | -- | ------------------------------------------------------- |
| isFocusable | boolean                   | 是 | 点击时是否支持切换焦点窗口。true表示支持；false表示不支持。 |
| callback    | AsyncCallback&lt;void&gt; | 是 | 回调函数。                                               |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isFocusable: boolean = true;
try {
  windowClass.setWindowFocusable(isFocusable, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the window to be focusable. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the window to be focusable.');
  });
} catch (exception) {
  console.error('Failed to set the window to be focusable. Cause:' + JSON.stringify(exception));
}
```

### setWindowFocusable<sup>9+</sup>

setWindowFocusable(isFocusable: boolean): Promise&lt;void&gt;

设置点击时是否支持切换焦点窗口，使用Promise异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ----------- | ------- | -- | -------------------------------------------------------- |
| isFocusable | boolean | 是 | 点击时是否支持切换焦点窗口。true表示支持；false表示不支持。  |

**返回值：**

| 类型 | 说明 |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isFocusable: boolean = true;
try {
  let promise = windowClass.setWindowFocusable(isFocusable);
  promise.then(() => {
    console.info('Succeeded in setting the window to be focusable.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the window to be focusable. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the window to be focusable. Cause:' + JSON.stringify(exception));
}
```

### setWindowKeepScreenOn<sup>9+</sup>

setWindowKeepScreenOn(isKeepScreenOn: boolean, callback: AsyncCallback&lt;void&gt;): void

设置屏幕是否为常亮状态，使用callback异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------------- | ------------------------- | -- | ---------------------------------------------------- |
| isKeepScreenOn | boolean                   | 是 | 设置屏幕是否为常亮状态。true表示常亮；false表示不常亮。  |
| callback       | AsyncCallback&lt;void&gt; | 是 | 回调函数。                                            |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isKeepScreenOn: boolean = true;
try {
  windowClass.setWindowKeepScreenOn(isKeepScreenOn, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the screen to be always on. Cause: ' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the screen to be always on.');
  });
} catch (exception) {
  console.error('Failed to set the screen to be always on. Cause: ' + JSON.stringify(exception));
}
```

### setWindowKeepScreenOn<sup>9+</sup>

setWindowKeepScreenOn(isKeepScreenOn: boolean): Promise&lt;void&gt;

设置屏幕是否为常亮状态，使用Promise异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------------- | ------- | -- | --------------------------------------------------- |
| isKeepScreenOn | boolean | 是 | 设置屏幕是否为常亮状态。true表示常亮；false表示不常亮。 |

**返回值：**

| 类型 | 说明 |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isKeepScreenOn: boolean = true;
try {
  let promise = windowClass.setWindowKeepScreenOn(isKeepScreenOn);
  promise.then(() => {
    console.info('Succeeded in setting the screen to be always on.');
  }).catch((err: BusinessError) => {
    console.info('Failed to set the screen to be always on. Cause:  ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the screen to be always on. Cause: ' + JSON.stringify(exception));
}
```

### setWindowPrivacyMode<sup>9+</sup>

setWindowPrivacyMode(isPrivacyMode: boolean, callback: AsyncCallback&lt;void&gt;): void

设置窗口是否为隐私模式，使用callback异步回调。设置为隐私模式的窗口，窗口内容将无法被截屏或录屏。此接口可用于禁止截屏/录屏的场景。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**需要权限：** ohos.permission.PRIVACY_WINDOW

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------------- | ------------------------- | -- | ------------------------------------------------------ |
| isPrivacyMode | boolean                   | 是 | 窗口是否为隐私模式。true表示模式开启；false表示模式关闭。  |
| callback      | AsyncCallback&lt;void&gt; | 是 | 回调函数。                                              |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isPrivacyMode: boolean = true;
try {
  windowClass.setWindowPrivacyMode(isPrivacyMode, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the window to privacy mode. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the window to privacy mode.');
  });
} catch (exception) {
  console.error('Failed to set the window to privacy mode. Cause:' + JSON.stringify(exception));
}
```

### setWindowPrivacyMode<sup>9+</sup>

setWindowPrivacyMode(isPrivacyMode: boolean): Promise&lt;void&gt;

设置窗口是否为隐私模式，使用Promise异步回调。设置为隐私模式的窗口，窗口内容将无法被截屏或录屏。此接口可用于禁止截屏/录屏的场景。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**需要权限：** ohos.permission.PRIVACY_WINDOW

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------------- | ------- | -- | ----------------------------------------------------- |
| isPrivacyMode | boolean | 是 | 窗口是否为隐私模式。true表示模式开启；false表示模式关闭。 |

**返回值：**

| 类型 | 说明 |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isPrivacyMode: boolean = true;
try {
  let promise = windowClass.setWindowPrivacyMode(isPrivacyMode);
  promise.then(() => {
    console.info('Succeeded in setting the window to privacy mode.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the window to privacy mode. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the window to privacy mode. Cause:' + JSON.stringify(exception));
}
```

### setWindowTouchable<sup>9+</sup>

setWindowTouchable(isTouchable: boolean, callback: AsyncCallback&lt;void&gt;): void

设置窗口是否为可触状态，使用callback异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ----------- | ------------------------- | -- | ----------------------------------------------- |
| isTouchable | boolean                   | 是 | 窗口是否为可触状态。true表示可触；false表示不可触。 |
| callback    | AsyncCallback&lt;void&gt; | 是 | 回调函数。                                        |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isTouchable = true;
try {
  windowClass.setWindowTouchable(isTouchable, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the window to be touchable. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the window to be touchable.');
  });
} catch (exception) {
  console.error('Failed to set the window to be touchable. Cause:' + JSON.stringify(exception));
}
```

### setWindowTouchable<sup>9+</sup>

setWindowTouchable(isTouchable: boolean): Promise&lt;void&gt;

设置窗口是否为可触状态，使用Promise异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ----------- | ------- | -- | ----------------------------------------------- |
| isTouchable | boolean | 是 | 窗口是否为可触状态。true表示可触；false表示不可触。 |

**返回值：**

| 类型 | 说明 |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isTouchable: boolean = true;
try {
  let promise = windowClass.setWindowTouchable(isTouchable);
  promise.then(() => {
    console.info('Succeeded in setting the window to be touchable.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the window to be touchable. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the window to be touchable. Cause:' + JSON.stringify(exception));
}
```

### snapshot<sup>9+</sup>

snapshot(callback: AsyncCallback&lt;image.PixelMap&gt;): void

获取窗口截图，使用callback异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名      | 类型                      | 必填 | 说明                 |
| ----------- | ------------------------- | ---- | -------------------- |
| callback    | AsyncCallback&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)&gt; | 是   | 回调函数。  |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

windowClass.snapshot((err: BusinessError, pixelMap: image.PixelMap) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to snapshot window. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in snapshotting window. Pixel bytes number: ' + pixelMap.getPixelBytesNumber());
  pixelMap.release(); // PixelMap使用完后及时释放内存
});
```

### snapshot<sup>9+</sup>

snapshot(): Promise&lt;image.PixelMap&gt;

获取窗口截图，使用Promise异步回调。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)&gt; | Promise对象。返回当前窗口截图。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

let promise = windowClass.snapshot();
promise.then((pixelMap: image.PixelMap) => {
  console.info('Succeeded in snapshotting window. Pixel bytes number: ' + pixelMap.getPixelBytesNumber());
  pixelMap.release(); // PixelMap使用完后及时释放内存
}).catch((err: BusinessError) => {
  console.error('Failed to snapshot window. Cause:' + JSON.stringify(err));
});
```

### setAspectRatio<sup>10+</sup>

setAspectRatio(ratio: number): Promise&lt;void&gt;

设置窗口内容布局的比例，使用Promise异步回调。

仅应用主窗口支持此接口功能，比例参数将持久化保存，关闭应用或重启设备设置的比例仍然生效。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名             | 类型    | 必填 | 说明                                        |
| ------------------ | ------- | ---- |-------------------------------------------|
| ratio | number | 是   | 除边框装饰之外的窗口内容布局的宽高比。该参数为浮点数，受窗口最大最小尺寸限制，比例值下限为最小宽度/最大高度，上限为最大宽度/最大高度。窗口最大最小尺寸由[WindowLimits](#windowlimits11)和系统限制的交集决定，系统限制优先级高于[WindowLimits](#windowlimits11)。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300004 | Unauthorized operation.                      |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let ratio = 1.0;
  let promise = windowClass.setAspectRatio(ratio);
  promise.then(() => {
    console.info('Succeeded in setting aspect ratio of window.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the aspect ratio of window. Cause:' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the aspect ratio of window. Cause: ' + JSON.stringify(exception));
}
```

### setAspectRatio<sup>10+</sup>

setAspectRatio(ratio: number, callback: AsyncCallback&lt;void&gt;): void

设置窗口内容布局的比例，使用callback异步回调。

仅应用主窗口支持此接口功能，比例参数将持久化保存，关闭应用或重启设备设置的比例仍然生效。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名             | 类型    | 必填 | 说明                                         |
| ------------------ | ------- | ---- |--------------------------------------------|
| ratio | number | 是   | 除边框装饰之外的窗口内容布局的宽高比。该参数为浮点数，取值范围为(0.0, +∞)。 |
| callback    | AsyncCallback&lt;void&gt; | 是   | 回调函数。                                      |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300004 | Unauthorized operation.                      |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let ratio = 1.0;
  windowClass.setAspectRatio(ratio, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the aspect ratio of window. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the aspect ratio of window.');
  });
} catch (exception) {
  console.error('Failed to set the aspect ratio of window. Cause: ' + JSON.stringify(exception));
}
```

### resetAspectRatio<sup>10+</sup>

resetAspectRatio(): Promise&lt;void&gt;

取消设置窗口内容布局的比例，使用Promise异步回调。

仅应用主窗口支持此接口功能，调用后将清除持久化储存的比例信息。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300004 | Unauthorized operation.                      |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let promise = windowClass.resetAspectRatio();
  promise.then(() => {
    console.info('Succeeded in resetting aspect ratio of window.');
  }).catch((err: BusinessError) => {
    console.error('Failed to reset the aspect ratio of window. Cause:' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to reset the aspect ratio of window. Cause: ' + JSON.stringify(exception));
}
```

### resetAspectRatio<sup>10+</sup>

resetAspectRatio(callback: AsyncCallback&lt;void&gt;): void

取消设置窗口内容布局的比例，使用callback异步回调。

仅应用主窗口支持此接口功能，调用后将清除持久化储存的比例信息。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名             | 类型    | 必填 | 说明                                                         |
| ------------------ | ------- | ---- | ------------------------------------------------------------ |
| callback    | AsyncCallback&lt;void&gt; | 是   | 回调函数。           |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300004 | Unauthorized operation.                      |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  windowClass.resetAspectRatio((err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to reset the aspect ratio of window. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in resetting aspect ratio of window.');
  });
} catch (exception) {
  console.error('Failed to reset the aspect ratio of window. Cause: ' + JSON.stringify(exception));
}
```

### minimize<sup>11+</sup>

minimize(callback: AsyncCallback&lt;void&gt;): void

此接口根据调用对象不同，实现不同的两个功能：

当调用对象为主窗口时，实现最小化功能，可在Dock栏中还原；

当调用对象为子窗口时，实现隐藏功能，不可在Dock栏中还原。

使用callback异步回调。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300003 | This window manager service works abnormally. |

**示例：**

```js
import { BusinessError } from '@ohos.base';

windowClass.minimize((err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to minimize the window. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in minimizing the window.');
});
```

### minimize<sup>11+</sup>

minimize(): Promise&lt;void&gt;

此接口根据调用对象不同，实现不同的两个功能：

当调用对象为主窗口时，实现最小化功能，可在Dock栏中还原；

当调用对象为子窗口时，实现隐藏功能，不可在Dock栏中还原。

使用Promise异步回调。

**系统能力：** SystemCapability.Window.SessionManager

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300003 | This window manager service works abnormally. |

**示例：**

```js
import { BusinessError } from '@ohos.base';

let promise = windowClass.minimize();
promise.then(() => {
  console.info('Succeeded in minimizing the window.');
}).catch((err: BusinessError) => {
  console.error('Failed to minimize the window. Cause: ' + JSON.stringify(err));
});
```

### maximize<sup>12+</sup>

maximize(): Promise&lt;void&gt;

主窗口调用，实现最大化功能，使用Promise异步回调。

**系统能力：** SystemCapability.Window.SessionManager

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal.                |
| 1300003 | This window manager service works abnormally. |
| 1300004 | Unauthorized operation.                       |
| 1300005 | This window stage is abnormal. |

**示例：**

```js
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    windowStage.getMainWindow((err: BusinessError, data) => {
      const errCode: number = err.code;
      if (errCode) {
        console.error('Failed to obtain the main window. Cause: ' + JSON.stringify(err));
        return;
      }
      windowClass = data;
      let promise = windowClass.maximize();
      promise.then(() => {
        console.info('Succeeded in maximizing the window.');
      }).catch((err: BusinessError) => {
        console.error('Failed to maximize the window. Cause: ' + JSON.stringify(err));
      });
    });
  }
};
```

### recover<sup>11+</sup>

recover(): Promise&lt;void&gt;

将主窗口从全屏、最大化、分屏模式下还原为浮动窗口，并恢复到进入该模式之前的大小和位置，已经是浮动窗口模式不可再还原。使用Promise异步回调。此接口仅在部分设备类型下生效。

**系统能力：** SystemCapability.Window.SessionManager

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300001 | Repeated operation. |
| 1300002 | This window state is abnormal. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.recover();
promise.then(() => {
  console.info('Succeeded in recovering the window.');
}).catch((err: BusinessError) => {
  console.error('Failed to recover the window. Cause: ' + JSON.stringify(err));
});
```

### getWindowLimits<sup>11+</sup>

getWindowLimits(): WindowLimits

获取当前窗口的尺寸限制。

**系统能力：** SystemCapability.Window.SessionManager

**返回值：**

| 类型                          | 说明           |
| ----------------------------- | ------------------ |
| [WindowLimits](#windowlimits11) | 当前窗口尺寸限制。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                       |
| :------- | :----------------------------- |
| 1300002  | This window state is abnormal. |

**示例：**

```ts
try {
  let windowLimits = windowClass.getWindowLimits();
} catch (exception) {
  console.error('Failed to obtain the window limits of window. Cause: ' + JSON.stringify(exception));
}
```

### setWindowLimits<sup>11+</sup>

setWindowLimits(windowLimits: WindowLimits): Promise&lt;WindowLimits&gt;

设置当前窗口的尺寸限制，使用Promise异步回调。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名       | 类型                          | 必填 | 说明                           |
| :----------- | :---------------------------- | :--- | :----------------------------- |
| windowLimits | [WindowLimits](#windowlimits11) | 是   | 目标窗口的尺寸限制，单位为px。 |

**返回值：**

| 类型                                         | 说明                                |
| :------------------------------------------- | :---------------------------------- |
| Promise&lt;[WindowLimits](#windowlimits11)&gt; | Promise对象。返回设置后的尺寸限制。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                                      |
| :------- | :-------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |
| 1300004 | Unauthorized operation.                |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
try {
  let windowLimits: window.WindowLimits = {
    maxWidth: 1500,
    maxHeight: 1000,
    minWidth: 500,
    minHeight: 400
  };
  let promise = windowClass.setWindowLimits(windowLimits);
    promise.then((data) => {
    console.info('Succeeded in changing the window limits. Cause:' + JSON.stringify(data));
  }).catch((err: BusinessError) => {
    console.error('Failed to change the window limits. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to change the window limits. Cause:' + JSON.stringify(exception));
}
```

### setWindowMask<sup>12+</sup>

setWindowMask(windowMask: Array&lt;Array&lt;number&gt;&gt;): Promise&lt;void&gt;;

设置异形窗口的掩码，使用Promise异步回调。异形窗口为非常规形状的窗口，掩码用于描述异形窗口的形状。此接口仅限子窗和全局悬浮窗可用，仅2in1设备可用。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名       | 类型                          | 必填 | 说明                           |
| :----------- | :---------------------------- | :--- | :----------------------------- |
| windowMask | Array&lt;Array&lt;number&gt;&gt; | 是   | 异形窗口的掩码，该参数仅支持宽高为窗口宽高、取值为整数0和整数1的二维数组输入，整数0代表所在像素透明，整数1代表所在像素不透明，宽高不符合的二维数组或二维数组取值不为整数0和整数1的二维数组为非法参数。 |

**返回值：**

| 类型                                         | 说明                                |
| :------------------------------------------- | :---------------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                                      |
| :------- | :-------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
try {
  let windowMask: Array<Array<number>> = [
      [0, 0, 0, 1, 0, 0, 0],
      [0, 0, 1, 1, 1, 0, 0],
      [0, 1, 1, 0, 1, 1, 0],
      [1, 1, 0, 0, 0, 1, 1]
    ];
  let promise = windowClass.setWindowMask(windowMask);
    promise.then(() => {
    console.info('Succeeded in setting the window mask.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the window mask. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the window mask. Cause:' + JSON.stringify(exception));
}
```

### keepKeyboardOnFocus<sup>11+</sup>

keepKeyboardOnFocus(keepKeyboardFlag: boolean): void

窗口获焦时保留由其他窗口创建的软键盘，仅支持系统窗口与应用子窗口。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名           | 类型    | 必填 | 说明                                                         |
| ---------------- | ------- | ---- | ------------------------------------------------------------ |
| keepKeyboardFlag | boolean | 是   | 是否保留其他窗口创建的软键盘。true表示保留；false表示不保留。|

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ---------------------------------------- |
| 1300002 | This window state is abnormal.           |
| 1300004 | Unauthorized operation.                  |

**示例：**

```ts
try {
  windowClass.keepKeyboardOnFocus(true);
} catch (exception) {
  console.error('Failed to keep keyboard onFocus. Cause: ' + JSON.stringify(exception));
}
```

### setWindowDecorVisible<sup>11+</sup>

setWindowDecorVisible(isVisible: boolean): void

主窗口设置标题栏是否可见。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名    | 类型    | 必填 | 说明                                          |
| --------- | ------- | ---- | --------------------------------------------- |
| isVisible | boolean | 是   | 设置标题栏是否可见，true为可见，false为隐藏。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                       |
| -------- | ------------------------------ |
| 1300002  | This window state is abnormal. |
| 1300004  | Unauthorized operation.        |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    // 为主窗口加载对应的目标页面。
    windowStage.loadContent("pages/page2", (err: BusinessError) => {
      let errCode: number = err.code;
      if (errCode) {
        console.error('Failed to load the content. Cause:' + JSON.stringify(err));
        return;
      }
      console.info('Succeeded in loading the content.');
      // 获取应用主窗口。
      let mainWindow: window.Window | undefined = undefined;
      windowStage.getMainWindow((err: BusinessError, data) => {
        let errCode: number = err.code;
        if (errCode) {
          console.error('Failed to obtain the main window. Cause: ' + JSON.stringify(err));
          return;
        }
        mainWindow = data;
        console.info('Succeeded in obtaining the main window. Data: ' + JSON.stringify(data));
        let isVisible = false;
        // 调用setWindowDecorVisible接口
        try {
            mainWindow.setWindowDecorVisible(isVisible);
        } catch (exception) {
            console.error('Failed to set the visibility of window decor. Cause: ' + JSON.stringify(exception));
        }
      })
    });
  }
};
```

### setSubWindowModal<sup>12+</sup>

setSubWindowModal(isModal: boolean): Promise&lt;void&gt;

设置子窗的模态属性是否启用，使用Promise异步回调。

子窗口调用该接口时，设置子窗口模态属性是否启用。启用子窗口模态属性后，其父级窗口不能响应用户操作，直到子窗口关闭或者子窗口的模态属性被禁用。

子窗口之外的窗口调用该接口时，会报错。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名    | 类型    | 必填 | 说明                                          |
| --------- | ------- | ---- | --------------------------------------------- |
| isModal | boolean | 是   | 设置子窗口模态属性是否启用，true为启用，false为不启用。 |


**返回值：**

| 类型 | 说明 |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                       |
| -------- | ------------------------------ |
| 1300002  | This window state is abnormal. |
| 1300004  | Unauthorized operation.        |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.setSubWindowModal(true);
promise.then(() => {
  console.info('Succeeded in setting subwindow modal');
}).catch((err: BusinessError) => {
  console.error('Failed to set subwindow modal. Cause:' +  JSON.stringify(err));
})
```

### setWindowDecorHeight<sup>11+</sup>

setWindowDecorHeight(height: number): void

设置窗口标题栏高度。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| height | number | 是   | 设置的窗口标题栏高度。该参数为整数，取值范围为[37,112]，单位为vp。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                       |
| -------- | ------------------------------ |
| 1300002  | This window state is abnormal. |

**示例：**

```ts
let height: number = 50;
try {
  windowClass.setWindowDecorHeight(height);
} catch (exception) {
  console.error('Failed to set the height of window decor. Cause: ' + JSON.stringify(exception));
}
```

### getWindowDecorHeight<sup>11+</sup>

getWindowDecorHeight(): number

获取窗口标题栏高度。

**系统能力：** SystemCapability.Window.SessionManager

**返回值：**

| 类型   | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| number | 返回的窗口标题栏高度。该参数为整数，取值范围为[37,112]，单位为vp。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                       |
| -------- | ------------------------------ |
| 1300002  | This window state is abnormal. |

**示例：**

```ts
try {
  let height = windowClass.getWindowDecorHeight();
} catch (exception) {
  console.error('Failed to get the height of window decor. Cause: ' + JSON.stringify(exception));
}
```

### getTitleButtonRect<sup>11+</sup>

getTitleButtonRect(): TitleButtonRect

获取标题栏上的最小化、最大化、关闭按钮矩形区域。

**系统能力：** SystemCapability.Window.SessionManager

**返回值：**

| 类型                                  | 说明                                                         |
| ------------------------------------- | ------------------------------------------------------------ |
| [TitleButtonRect](#titlebuttonrect11) | 标题栏上的最小化、最大化、关闭按钮矩形区域，该区域位置坐标相对窗口右上角。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                       |
| -------- | ------------------------------ |
| 1300002  | This window state is abnormal. |

**示例：**

```ts
try {
  let titleButtonArea = windowClass.getTitleButtonRect();
  console.info('Succeeded in obtaining the area of title buttons. Data: ' + JSON.stringify(titleButtonArea));
} catch (exception) {
  console.error('Failed to get the area of title buttons. Cause: ' + JSON.stringify(exception));
}
```

### enableLandscapeMultiWindow<sup>12+</sup>

enableLandscapeMultiWindow(): Promise&lt;void&gt;

在开启多窗动态布局下，配置支持横向悬浮窗。

此接口只有在module.json5配置文件中[abilities](../../quick-start/module-configuration-file.md#abilities标签)标签中的preferMultiWindowOrientation属性为landscape_auto时才生效。

**系统能力：** SystemCapability.Window.SessionManager

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.enableLandscapeMultiWindow();
promise.then(() => {
    console.info('Succeeded in making multi-window become landscape.');
}).catch((err: BusinessError) => {
    console.error('Failed to make multi-window become landscape. Cause: ' + JSON.stringify(err));
});
```

### disableLandscapeMultiWindow<sup>12+</sup>

disableLandscapeMultiWindow(): Promise&lt;void&gt;

在开启多窗动态布局下，配置支持竖向悬浮窗。

此接口只有在module.json5配置文件中[abilities](../../quick-start/module-configuration-file.md#abilities标签)标签中的preferMultiWindowOrientation属性为landscape_auto时才生效。

**系统能力：** SystemCapability.Window.SessionManager

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.disableLandscapeMultiWindow();
promise.then(() => {
    console.info('Succeeded in making multi-window become not landscape.');
}).catch((err: BusinessError) => {
    console.error('Failed to make multi-window become not landscape. Cause: ' + JSON.stringify(err));
});
```

### show<sup>(deprecated)</sup>

show(callback: AsyncCallback&lt;void&gt;): void

显示当前窗口，使用callback异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[showWindow()](#showwindow9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

windowClass.show((err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to show the window. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in showing the window.');
});
```

### show<sup>(deprecated)</sup>

show(): Promise&lt;void&gt;

显示当前窗口，使用Promise异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[showWindow()](#showwindow9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.show();
promise.then(() => {
  console.info('Succeeded in showing the window.');
}).catch((err: BusinessError) => {
  console.error('Failed to show the window. Cause: ' + JSON.stringify(err));
});
```

### destroy<sup>(deprecated)</sup>

destroy(callback: AsyncCallback&lt;void&gt;): void

销毁当前窗口，使用callback异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[destroyWindow()](#destroywindow9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

windowClass.destroy((err: BusinessError) => {
  const errCode: number = err.code;
  if (err.code) {
    console.error('Failed to destroy the window. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in destroying the window.');
});
```

### destroy<sup>(deprecated)</sup>

destroy(): Promise&lt;void&gt;

销毁当前窗口，使用Promise异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[destroyWindow()](#destroywindow9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.destroy();
promise.then(() => {
  console.info('Succeeded in destroying the window.');
}).catch((err: BusinessError) => {
  console.error('Failed to destroy the window. Cause: ' + JSON.stringify(err));
});
```

### moveTo<sup>(deprecated)</sup>

moveTo(x: number, y: number, callback: AsyncCallback&lt;void&gt;): void

移动窗口位置，使用callback异步回调。

全屏模式窗口不支持该操作。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[moveWindowTo()](#movewindowto9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                                              |
| -------- | ------------------------- | ---- | ------------------------------------------------- |
| x        | number                    | 是   | 窗口在x轴方向移动的值，值为正表示右移，单位为px，该参数仅支持整数输入。 |
| y        | number                    | 是   | 窗口在y轴方向移动的值，值为正表示下移，单位为px，该参数仅支持整数输入。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。                                        |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

windowClass.moveTo(300, 300, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to move the window. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in moving the window.');
});
```

### moveTo<sup>(deprecated)</sup>

moveTo(x: number, y: number): Promise&lt;void&gt;

移动窗口位置，使用Promise异步回调。

全屏模式窗口不支持该操作。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[moveWindowTo()](#movewindowto9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                                              |
| ------ | ------ | ---- | ------------------------------------------------- |
| x      | number | 是   | 窗口在x轴方向移动的值，值为正表示右移，单位为px，该参数仅支持整数输入。 |
| y      | number | 是   | 窗口在y轴方向移动的值，值为正表示下移，单位为px，该参数仅支持整数输入。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.moveTo(300, 300);
promise.then(() => {
  console.info('Succeeded in moving the window.');
}).catch((err: BusinessError) => {
  console.error('Failed to move the window. Cause: ' + JSON.stringify(err));
});
```

### resetSize<sup>(deprecated)</sup>

resetSize(width: number, height: number, callback: AsyncCallback&lt;void&gt;): void

改变当前窗口大小，使用callback异步回调。

应用主窗口与子窗口存在大小限制，默认宽度范围：[320, 1920]，默认高度范围：[240, 1920]，单位为vp。
应用主窗口与子窗口的最小宽度与最小高度可由产品端进行配置，配置后的最小宽度与最小高度以产品段配置值为准，具体尺寸限制范围可以通过[getWindowLimits](#getwindowlimits11)接口进行查询。

系统窗口存在大小限制，宽度范围：[0, 1920]，高度范围：[0, 1920]，单位为vp。

设置的宽度与高度受到此约束限制，规则：
若所设置的窗口宽/高尺寸小于窗口最小宽/高限值，则窗口最小宽/高限值生效；
若所设置的窗口宽/高尺寸大于窗口最大宽/高限值，则窗口最大宽/高限值生效。

全屏模式窗口不支持该操作。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[resize()](#resize9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                       |
| -------- | ------------------------- | ---- | -------------------------- |
| width    | number                    | 是   | 目标窗口的宽度，单位为px，该参数仅支持整数输入，负值为非法参数。 |
| height   | number                    | 是   | 目标窗口的高度，单位为px，该参数仅支持整数输入，负值为非法参数。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。                 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

windowClass.resetSize(500, 1000, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to change the window size. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in changing the window size.');
});
```

### resetSize<sup>(deprecated)</sup>

resetSize(width: number, height: number): Promise&lt;void&gt;

改变当前窗口大小，使用Promise异步回调。

应用主窗口与子窗口存在大小限制，默认宽度范围：[320, 1920]，默认高度范围：[240, 1920]，单位为vp。
应用主窗口与子窗口的最小宽度与最小高度可由产品端进行配置，配置后的最小宽度与最小高度以产品段配置值为准，具体尺寸限制范围可以通过[getWindowLimits](#getwindowlimits11)接口进行查询。

系统窗口存在大小限制，宽度范围：[0, 1920]，高度范围：[0, 1920]，单位为vp。

设置的宽度与高度受到此约束限制，规则：
若所设置的窗口宽/高尺寸小于窗口最小宽/高限值，则窗口最小宽/高限值生效；
若所设置的窗口宽/高尺寸大于窗口最大宽/高限值，则窗口最大宽/高限值生效。

全屏模式窗口不支持该操作。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[resize()](#resize9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                       |
| ------ | ------ | ---- | -------------------------- |
| width  | number | 是   | 目标窗口的宽度，单位为px，该参数仅支持整数输入，负值为非法参数。 |
| height | number | 是   | 目标窗口的高度，单位为px，该参数仅支持整数输入，负值为非法参数。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.resetSize(500, 1000);
promise.then(() => {
  console.info('Succeeded in changing the window size.');
}).catch((err: BusinessError) => {
  console.error('Failed to change the window size. Cause: ' + JSON.stringify(err));
});
```

### getProperties<sup>(deprecated)</sup>

getProperties(callback: AsyncCallback&lt;WindowProperties&gt;): void

获取当前窗口的属性，使用callback异步回调，返回WindowProperties。

> **说明：**
>
> 从 API version 6开始支持，从API version 9开始废弃，推荐使用[getWindowProperties()](#getwindowproperties9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                                       | 必填 | 说明                         |
| -------- | ---------------------------------------------------------- | ---- | ---------------------------- |
| callback | AsyncCallback&lt;[WindowProperties](#windowproperties)&gt; | 是   | 回调函数。返回当前窗口属性。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

windowClass.getProperties((err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to obtain the window properties. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in obtaining the window properties. Data: ' + JSON.stringify(data));
});
```

### getProperties<sup>(deprecated)</sup>

getProperties(): Promise&lt;WindowProperties&gt;

获取当前窗口的属性，使用Promise异步回调，返回WindowProperties。

> **说明：**
>
> 从 API version 6开始支持，从API version 9开始废弃，推荐使用[getWindowProperties()](#getwindowproperties9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型                                                 | 说明                            |
| ---------------------------------------------------- | ------------------------------- |
| Promise&lt;[WindowProperties](#windowproperties)&gt; | Promise对象。返回当前窗口属性。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.getProperties();
promise.then((data) => {
  console.info('Succeeded in obtaining the window properties. Data: ' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to obtain the window properties. Cause: ' + JSON.stringify(err));
});
```

### getAvoidArea<sup>(deprecated)</sup>

getAvoidArea(type: [AvoidAreaType](#avoidareatype7), callback: AsyncCallback&lt;[AvoidArea](#avoidarea7)&gt;): void

获取窗口内容规避的区域；如系统栏区域、刘海屏区域、手势区域、软键盘区域等与窗口内容重叠时，需要窗口内容避让的区域。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[getWindowAvoidArea()](#getwindowavoidarea9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                            | 必填 | 说明                                                         |
| -------- |-----------------------------------------------| ---- | ------------------------------------------------------------ |
| type     | [AvoidAreaType](#avoidareatype7)              | 是   | 表示规避区类型。|
| callback | AsyncCallback&lt;[AvoidArea](#avoidarea7)&gt; | 是   | 回调函数。返回窗口内容规避区域。                             |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let type = window.AvoidAreaType.TYPE_SYSTEM;
windowClass.getAvoidArea(type, (err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to obtain the area. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in obtaining the area. Data:' + JSON.stringify(data));
});
```

### getAvoidArea<sup>(deprecated)</sup>

getAvoidArea(type: [AvoidAreaType](#avoidareatype7)): Promise&lt;[AvoidArea](#avoidarea7)&gt;

获取窗口内容规避的区域；如系统栏区域、刘海屏区域、手势区域、软键盘区域等与窗口内容重叠时，需要窗口内容避让的区域。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[getWindowAvoidArea()](#getwindowavoidarea9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型                               | 必填 | 说明                                                         |
| ------ |----------------------------------| ---- | ------------------------------------------------------------ |
| type   | [AvoidAreaType](#avoidareatype7) | 是   | 表示规避区类型。 |

**返回值：**

| 类型                                      | 说明                                |
|-----------------------------------------| ----------------------------------- |
| Promise&lt;[AvoidArea](#avoidarea7)&gt; | Promise对象。返回窗口内容规避区域。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let type = window.AvoidAreaType.TYPE_SYSTEM;
let promise = windowClass.getAvoidArea(type);
promise.then((data) => {
  console.info('Succeeded in obtaining the area. Data:' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to obtain the area. Cause:' + JSON.stringify(err));
});
```

### setFullScreen<sup>(deprecated)</sup>

setFullScreen(isFullScreen: boolean, callback: AsyncCallback&lt;void&gt;): void

设置窗口的布局是否为全屏布局，使用callback异步回调。
全屏布局是指窗口大小为全屏幕，状态栏与导航栏不显示。
非全屏布局是指状态栏与导航栏显示，窗口大小避让状态栏与导航栏位置。

> **说明：**
>
> 从 API version 6开始支持，从API version 9开始废弃，推荐联合使用[setWindowSystemBarEnable()](#setwindowsystembarenable9)和[setWindowLayoutFullScreen()](#setwindowlayoutfullscreen9)实现全屏。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名       | 类型                      | 必填 | 说明                                           |
| ------------ | ------------------------- | ---- | ---------------------------------------------- |
| isFullScreen | boolean                   | 是   | 是否设为全屏布局（该全屏布局影响状态栏导航栏显示）。true表示全屏；false表示非全屏。 |
| callback     | AsyncCallback&lt;void&gt; | 是   | 回调函数。                                     |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isFullScreen: boolean = true;
windowClass.setFullScreen(isFullScreen, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to enable the full-screen mode. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in enabling the full-screen mode.');
});
```

### setFullScreen<sup>(deprecated)</sup>

setFullScreen(isFullScreen: boolean): Promise&lt;void&gt;

设置窗口的布局是否为全屏布局，使用Promise异步回调。
全屏布局是指窗口大小为全屏幕，状态栏与导航栏不显示。
非全屏布局是指状态栏与导航栏显示，窗口大小避让状态栏与导航栏位置。

> **说明：**
>
> 从 API version 6开始支持，从API version 9开始废弃，推荐联合使用[setWindowSystemBarEnable()](#setwindowsystembarenable9-1)和[setWindowLayoutFullScreen()](#setwindowlayoutfullscreen9-1)实现全屏。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名       | 类型    | 必填 | 说明                                           |
| ------------ | ------- | ---- | ---------------------------------------------- |
| isFullScreen | boolean | 是   | 是否设为全屏布局（该全屏布局影响状态栏导航栏显示）。true表示全屏；false表示非全屏。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isFullScreen: boolean = true;
let promise = windowClass.setFullScreen(isFullScreen);
promise.then(() => {
  console.info('Succeeded in enabling the full-screen mode.');
}).catch((err: BusinessError) => {
  console.error('Failed to enable the full-screen mode. Cause: ' + JSON.stringify(err));
});
```

### setLayoutFullScreen<sup>(deprecated)</sup>

setLayoutFullScreen(isLayoutFullScreen: boolean, callback: AsyncCallback&lt;void&gt;): void

设置窗口的布局是否为沉浸式布局，使用callback异步回调。
沉浸式布局是指布局不避让状态栏与导航栏，组件可能产生与其重叠的情况。
非沉浸式布局是指布局避让状态栏与导航栏，组件不会与其重叠。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[setWindowLayoutFullScreen()](#setwindowlayoutfullscreen9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名             | 类型                      | 必填 | 说明                                                         |
| ------------------ | ------------------------- | ---- | ------------------------------------------------------------ |
| isLayoutFullScreen | boolean                   | 是   | 窗口的布局是否为沉浸式布局（该沉浸式布局不影响状态栏、导航栏显示）。true表示沉浸式布局；false表示非沉浸式布局。 |
| callback           | AsyncCallback&lt;void&gt; | 是   | 回调函数。                                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isLayoutFullScreen: boolean = true;
windowClass.setLayoutFullScreen(isLayoutFullScreen, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the window layout to full-screen mode.');
});
```

### setLayoutFullScreen<sup>(deprecated)</sup>

setLayoutFullScreen(isLayoutFullScreen: boolean): Promise&lt;void&gt;

设置窗口的布局是否为沉浸式布局，使用Promise异步回调。
沉浸式布局是指布局不避让状态栏与导航栏，组件可能产生与其重叠的情况。
非沉浸式布局是指布局避让状态栏与导航栏，组件不会与其重叠。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[setWindowLayoutFullScreen()](#setwindowlayoutfullscreen9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名             | 类型    | 必填 | 说明                                                         |
| ------------------ | ------- | ---- | ------------------------------------------------------------ |
| isLayoutFullScreen | boolean | 是   | 窗口的布局是否为沉浸式布局（该沉浸式布局不影响状态栏、导航栏显示）。true表示沉浸式布局；false表示非沉浸式布局。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isLayoutFullScreen: boolean = true;
let promise = windowClass.setLayoutFullScreen(isLayoutFullScreen);
promise.then(() => {
  console.info('Succeeded in setting the window layout to full-screen mode.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(err));
});
```

### setSystemBarEnable<sup>(deprecated)</sup>

setSystemBarEnable(names: Array<'status' | 'navigation'>, callback: AsyncCallback&lt;void&gt;): void

设置窗口全屏模式时导航栏、状态栏的可见模式，使用callback异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[setWindowSystemBarEnable()](#setwindowsystembarenable9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                                                         |
| -------- | ---------------------------- | ---- | ------------------------------------------------------------ |
| names    | Array<'status'\|'navigation'> | 是   | 设置窗口全屏模式时状态栏和导航栏是否显示。<br>例如，需全部显示，该参数设置为['status',&nbsp;'navigation']；不设置，则默认不显示。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。                                                   |

**示例：**

```ts
// 此处以不显示导航栏、状态栏为例
import { BusinessError } from '@ohos.base';

let names: Array<'status' | 'navigation'> = [];
windowClass.setSystemBarEnable(names, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the system bar to be invisible.');
});
```

### setSystemBarEnable<sup>(deprecated)</sup>

setSystemBarEnable(names: Array<'status' | 'navigation'>): Promise&lt;void&gt;

设置窗口全屏模式时导航栏、状态栏的可见模式，使用Promise异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[setWindowSystemBarEnable()](#setwindowsystembarenable9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型  | 必填 | 说明                                                         |
| ------ | ---------------------------- | ---- | ------------------------ |
| names  | Array<'status'\|'navigation'> | 是   | 设置窗口全屏模式时状态栏和导航栏是否显示。<br>例如，需全部显示，该参数设置为['status',&nbsp;'navigation']；不设置，则默认不显示。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
// 此处以不显示导航栏、状态栏为例
import { BusinessError } from '@ohos.base';

let names: Array<'status' | 'navigation'> = [];
let promise = windowClass.setSystemBarEnable(names);
promise.then(() => {
  console.info('Succeeded in setting the system bar to be invisible.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(err));
});
```

### setSystemBarProperties<sup>(deprecated)</sup>

setSystemBarProperties(systemBarProperties: SystemBarProperties, callback: AsyncCallback&lt;void&gt;): void

设置窗口全屏模式时窗口内导航栏、状态栏的属性，使用callback异步回调。

> **说明：**
>
> 从 API version 6开始支持，从API version 9开始废弃，推荐使用[setWindowSystemBarProperties()](#setwindowsystembarproperties9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名              | 类型                                        | 必填 | 说明                   |
| ------------------- | ------------------------------------------- | ---- | ---------------------- |
| SystemBarProperties | [SystemBarProperties](#systembarproperties) | 是   | 导航栏、状态栏的属性。 |
| callback            | AsyncCallback&lt;void&gt;                   | 是   | 回调函数。             |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let SystemBarProperties: window.SystemBarProperties = {
  statusBarColor: '#ff00ff',
  navigationBarColor: '#00ff00',
  //以下两个属性从API Version8开始支持
  statusBarContentColor: '#ffffff',
  navigationBarContentColor: '#00ffff'
};
windowClass.setSystemBarProperties(SystemBarProperties, (err) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the system bar properties.');
});
```

### setSystemBarProperties<sup>(deprecated)</sup>

setSystemBarProperties(systemBarProperties: SystemBarProperties): Promise&lt;void&gt;

设置窗口全屏模式时窗口内导航栏、状态栏的属性，使用Promise异步回调。

> **说明：**
>
> 从 API version 6开始支持，从API version 9开始废弃，推荐使用[setWindowSystemBarProperties()](#setwindowsystembarproperties9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名              | 类型                                        | 必填 | 说明                   |
| ------------------- | ------------------------------------------- | ---- | ---------------------- |
| SystemBarProperties | [SystemBarProperties](#systembarproperties) | 是   | 导航栏、状态栏的属性。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let SystemBarProperties: window.SystemBarProperties = {
  statusBarColor: '#ff00ff',
  navigationBarColor: '#00ff00',
  //以下两个属性从API Version8开始支持
  statusBarContentColor: '#ffffff',
  navigationBarContentColor: '#00ffff'
};
let promise = windowClass.setSystemBarProperties(SystemBarProperties);
promise.then(() => {
  console.info('Succeeded in setting the system bar properties.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(err));
});
```

### loadContent<sup>(deprecated)</sup>

loadContent(path: string, callback: AsyncCallback&lt;void&gt;): void

为当前窗口加载具体页面内容，使用callback异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[setUIContent()](#setuicontent9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                 |
| -------- | ------------------------- | ---- | -------------------- |
| path     | string                    | 是   | 要加载到窗口中的页面内容的路径，Stage模型下该路径需添加到工程的main_pages.json文件中，FA模型下该路径需添加到工程的config.json文件中。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

windowClass.loadContent('pages/page2/page3', (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to load the content. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in loading the content.');
});
```

### loadContent<sup>(deprecated)</sup>

loadContent(path: string): Promise&lt;void&gt;

为当前窗口加载具体页面内容，使用Promise异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[setUIContent()](#setuicontent9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                 |
| ------ | ------ | ---- | -------------------- |
| path   | string | 是   | 要加载到窗口中的页面内容的路径，Stage模型下该路径需添加到工程的main_pages.json文件中，FA模型下该路径需添加到工程的config.json文件中。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.loadContent('pages/page2/page3');
promise.then(() => {
  console.info('Succeeded in loading the content.');
}).catch((err: BusinessError) => {
  console.error('Failed to load the content. Cause: ' + JSON.stringify(err));
});
```

### isShowing<sup>(deprecated)</sup>

isShowing(callback: AsyncCallback&lt;boolean&gt;): void

判断当前窗口是否已显示，使用callback异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[isWindowShowing()](#iswindowshowing9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                         | 必填 | 说明                                                         |
| -------- | ---------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback&lt;boolean&gt; | 是   | 回调函数。返回true表示当前窗口已显示，返回false表示当前窗口未显示。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

windowClass.isShowing((err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to check whether the window is showing. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in checking whether the window is showing. Data: ' + JSON.stringify(data));
});
```

### isShowing<sup>(deprecated)</sup>

isShowing(): Promise&lt;boolean&gt;

判断当前窗口是否已显示，使用Promise异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[isWindowShowing()](#iswindowshowing9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型                   | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise对象。返回true表示当前窗口已显示，返回false表示当前窗口未显示。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.isShowing();
promise.then((data) => {
  console.info('Succeeded in checking whether the window is showing. Data: ' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to check whether the window is showing. Cause: ' + JSON.stringify(err));
});
```

### on('systemAvoidAreaChange')<sup>(deprecated)</sup>

on(type: 'systemAvoidAreaChange', callback: Callback&lt;AvoidArea&gt;): void

开启系统规避区变化的监听。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[on('avoidAreaChange')](#onavoidareachange9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                       | 必填 | 说明                                                    |
| -------- |------------------------------------------| ---- | ------------------------------------------------------- |
| type     | string                                   | 是   | 监听事件，固定为'systemAvoidAreaChange'，即系统规避区变化事件。 |
| callback | Callback&lt;[AvoidArea](#avoidarea7)&gt; | 是   | 回调函数。返回当前规避区。                             |

**示例：**

```ts
windowClass.on('systemAvoidAreaChange', (data) => {
  console.info('Succeeded in enabling the listener for system avoid area changes. Data: ' + JSON.stringify(data));
});
```

### off('systemAvoidAreaChange')<sup>(deprecated)</sup>

off(type: 'systemAvoidAreaChange', callback?: Callback&lt;AvoidArea&gt;): void

关闭系统规避区变化的监听。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[off('avoidAreaChange')](#offavoidareachange9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                       | 必填 | 说明                                                    |
| -------- |------------------------------------------| ---- | ------------------------------------------------------- |
| type     | string                                   | 是   | 监听事件，固定为'systemAvoidAreaChange'，即系统规避区变化事件。 |
| callback | Callback&lt;[AvoidArea](#avoidarea7)&gt; | 否   | 回调函数。返回当前规避区。若传入参数，则关闭该监听。若未传入参数，则关闭所有系统规避区变化的监听。           |

**示例：**

```ts
windowClass.off('systemAvoidAreaChange');
```

### isSupportWideGamut<sup>(deprecated)</sup>

isSupportWideGamut(callback: AsyncCallback&lt;boolean&gt;): void

判断当前窗口是否支持广色域模式，使用callback异步回调。

> **说明：**
>
> 从 API version 8开始支持，从API version 9开始废弃，推荐使用[isWindowSupportWideGamut()](#iswindowsupportwidegamut9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                         | 必填 | 说明                                                         |
| -------- | ---------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback&lt;boolean&gt; | 是   | 回调函数。返回true表示当前窗口支持广色域模式，返回false表示当前窗口不支持广色域模式。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

windowClass.isSupportWideGamut((err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to check whether the window support WideGamut. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in checking whether the window support WideGamut Data: ' + JSON.stringify(data));
});
```

### isSupportWideGamut<sup>(deprecated)</sup>

isSupportWideGamut(): Promise&lt;boolean&gt;

判断当前窗口是否支持广色域模式，使用Promise异步回调。

> **说明：**
>
> 从 API version 8开始支持，从API version 9开始废弃，推荐使用[isWindowSupportWideGamut()](#iswindowsupportwidegamut9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型                   | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise对象。返回true表示当前窗口支持广色域模式，返回false表示当前窗口不支持广色域模式。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.isSupportWideGamut();
promise.then((data) => {
  console.info('Succeeded in checking whether the window support WideGamut. Data: ' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to check whether the window support WideGamut. Cause: ' + JSON.stringify(err));
});
```

### setColorSpace<sup>(deprecated)</sup>

setColorSpace(colorSpace:ColorSpace, callback: AsyncCallback&lt;void&gt;): void

设置当前窗口为广色域模式或默认色域模式，使用callback异步回调。

> **说明：**
>
> 从 API version 8开始支持，从API version 9开始废弃，推荐使用[setWindowColorSpace()](#setwindowcolorspace9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名     | 类型                      | 必填 | 说明         |
| ---------- | ------------------------- | ---- | ------------ |
| colorSpace | [ColorSpace](#colorspace8) | 是   | 设置色域模式。 |
| callback   | AsyncCallback&lt;void&gt; | 是   | 回调函数。   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

windowClass.setColorSpace(window.ColorSpace.WIDE_GAMUT, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set window colorspace. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting window colorspace.');
});
```

### setColorSpace<sup>(deprecated)</sup>

setColorSpace(colorSpace:ColorSpace): Promise&lt;void&gt;

设置当前窗口为广色域模式或默认色域模式，使用Promise异步回调。

> **说明：**
>
> 从 API version 8开始支持，从API version 9开始废弃，推荐使用[setWindowColorSpace()](#setwindowcolorspace9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名     | 类型                      | 必填 | 说明           |
| ---------- | ------------------------- | ---- | -------------- |
| colorSpace | [ColorSpace](#colorspace8) | 是   | 设置色域模式。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.setColorSpace(window.ColorSpace.WIDE_GAMUT);
promise.then(() => {
  console.info('Succeeded in setting window colorspace.');
}).catch((err: BusinessError) => {
  console.error('Failed to set window colorspace. Cause: ' + JSON.stringify(err));
});
```

### getColorSpace<sup>(deprecated)</sup>

getColorSpace(callback: AsyncCallback&lt;ColorSpace&gt;): void

获取当前窗口色域模式，使用callback异步回调。

> **说明：**
>
> 从 API version 8开始支持，从API version 9开始废弃，推荐使用[getWindowColorSpace()](#getwindowcolorspace9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                           | 必填 | 说明                                                       |
| -------- | ---------------------------------------------- | ---- | ---------------------------------------------------------- |
| callback | AsyncCallback&lt;[ColorSpace](#colorspace8)&gt; | 是   | 回调函数。当获取成功，err为undefined，data为当前色域模式。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

windowClass.getColorSpace((err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to get window colorspace. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in getting window colorspace. Cause:' + JSON.stringify(data));
});
```

### getColorSpace<sup>(deprecated)</sup>

getColorSpace(): Promise&lt;ColorSpace&gt;

获取当前窗口色域模式，使用Promise异步回调。

> **说明：**
>
> 从 API version 8开始支持，从API version 9开始废弃，推荐使用[getWindowColorSpace()](#getwindowcolorspace9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型                                     | 说明                            |
| ---------------------------------------- | ------------------------------- |
| Promise&lt;[ColorSpace](#colorspace8)&gt; | Promise对象。返回当前色域模式。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.getColorSpace();
promise.then((data) => {
  console.info('Succeeded in getting window color space. Cause:' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to get window colorspace. Cause: ' + JSON.stringify(err));
});
```

### setBackgroundColor<sup>(deprecated)</sup>

setBackgroundColor(color: string, callback: AsyncCallback&lt;void&gt;): void

设置窗口的背景色，使用callback异步回调。Stage模型下，该接口需要在[loadContent()](#loadcontent9)或[setUIContent()](#setuicontent9)调用生效后使用。

> **说明：**
>
> 从 API version 6开始支持，从API version 9开始废弃，推荐使用[setWindowBackgroundColor()](#setwindowbackgroundcolor9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                                                         |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| color    | string                    | 是   | 需要设置的背景色，为十六进制RGB或ARGB颜色，不区分大小写，例如`#00FF00`或`#FF00FF00`。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。                                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let color: string = '#00ff33';
windowClass.setBackgroundColor(color, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the background color. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the background color.');
});
```

### setBackgroundColor<sup>(deprecated)</sup>

setBackgroundColor(color: string): Promise&lt;void&gt;

设置窗口的背景色，使用Promise异步回调。Stage模型下，该接口需要在[loadContent()](#loadcontent9)或[setUIContent()](#setuicontent9)调用生效后使用。

> **说明：**
>
> 从 API version 6开始支持，从API version 9开始废弃，推荐使用[setWindowBackgroundColor()](#setwindowbackgroundcolor9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| color  | string | 是   | 需要设置的背景色，为十六进制RGB或ARGB颜色，不区分大小写，例如`#00FF00`或`#FF00FF00`。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let color: string = '#00ff33';
let promise = windowClass.setBackgroundColor(color);
promise.then(() => {
  console.info('Succeeded in setting the background color.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the background color. Cause: ' + JSON.stringify(err));
});
```

### setBrightness<sup>(deprecated)</sup>

setBrightness(brightness: number, callback: AsyncCallback&lt;void&gt;): void

允许应用窗口设置屏幕亮度值，使用callback异步回调。

当前屏幕亮度规格：窗口设置屏幕亮度生效时，控制中心不可以调整系统屏幕亮度，窗口恢复默认系统亮度之后，控制中心可以调整系统屏幕亮度。

> **说明：**
>
> 从 API version 6开始支持，从API version 9开始废弃，推荐使用[setWindowBrightness()](#setwindowbrightness9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名     | 类型                      | 必填 | 说明                                    |
| ---------- | ------------------------- | ---- |---------------------------------------|
| brightness | number                    | 是   | 屏幕亮度值。该参数为浮点数，取值范围为[0.0, 1.0]或-1.0。1.0表示最亮，-1.0表示默认亮度。 |
| callback   | AsyncCallback&lt;void&gt; | 是   | 回调函数。                                 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let brightness: number = 1;
windowClass.setBrightness(brightness, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the brightness. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the brightness.');
});
```

### setBrightness<sup>(deprecated)</sup>

setBrightness(brightness: number): Promise&lt;void&gt;

允许应用窗口设置屏幕亮度值，使用Promise异步回调。

当前屏幕亮度规格：窗口设置屏幕亮度生效时，控制中心不可以调整系统屏幕亮度，窗口恢复默认系统亮度之后，控制中心可以调整系统屏幕亮度。

> **说明：**
>
> 从 API version 6开始支持，从API version 9开始废弃，推荐使用[setWindowBrightness()](#setwindowbrightness9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                                       |
| ---------- | ------ | ---- |------------------------------------------|
| brightness | number | 是   | 屏幕亮度值。该参数为浮点数，取值范围为[0.0, 1.0]或-1.0。1.0表示最亮，-1.0表示默认亮度。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let brightness: number = 1;
let promise = windowClass.setBrightness(brightness);
promise.then(() => {
  console.info('Succeeded in setting the brightness.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the brightness. Cause: ' + JSON.stringify(err));
});
```

### setDimBehind<sup>(deprecated)</sup>

setDimBehind(dimBehindValue: number, callback: AsyncCallback&lt;void&gt;): void

窗口叠加时，设备有子窗口的情况下设置靠后的窗口的暗度值，使用callback异步回调。

> **说明：**
>
> 该接口不支持使用。从 API version 7开始支持，从API version 9开始废弃。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名         | 类型                      | 必填 | 说明                                     |
| -------------- | ------------------------- | ---- |----------------------------------------|
| dimBehindValue | number                    | 是   | 表示靠后的窗口的暗度值，取值范围为[0.0, 1.0]，取1.0时表示最暗。 |
| callback       | AsyncCallback&lt;void&gt; | 是   | 回调函数。                                  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

windowClass.setDimBehind(0.5, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the dimness. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the dimness.');
});
```

### setDimBehind<sup>(deprecated)</sup>

setDimBehind(dimBehindValue: number): Promise&lt;void&gt;

窗口叠加时，设备有子窗口的情况下设置靠后的窗口的暗度值，使用Promise异步回调。

> **说明：**
>
> 该接口不支持使用。从 API version 7开始支持，从API version 9开始废弃。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名         | 类型   | 必填 | 说明                                               |
| -------------- | ------ | ---- | -------------------------------------------------- |
| dimBehindValue | number | 是   | 表示靠后的窗口的暗度值，取值范围为0-1，1表示最暗。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.setDimBehind(0.5);
promise.then(() => {
  console.info('Succeeded in setting the dimness.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the dimness. Cause: ' + JSON.stringify(err));
});
```

### setFocusable<sup>(deprecated)</sup>

setFocusable(isFocusable: boolean, callback: AsyncCallback&lt;void&gt;): void

设置点击时是否支持切换焦点窗口，使用callback异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[setWindowFocusable()](#setwindowfocusable9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名      | 类型                      | 必填 | 说明                         |
| ----------- | ------------------------- | ---- | ---------------------------- |
| isFocusable | boolean                   | 是   | 点击时是否支持切换焦点窗口。true表示支持；false表示不支持。 |
| callback    | AsyncCallback&lt;void&gt; | 是   | 回调函数。                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isFocusable: boolean = true;
windowClass.setFocusable(isFocusable, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the window to be focusable. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the window to be focusable.');
});
```

### setFocusable<sup>(deprecated)</sup>

setFocusable(isFocusable: boolean): Promise&lt;void&gt;

设置点击时是否支持切换焦点窗口，使用Promise异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[setWindowFocusable()](#setwindowfocusable9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名      | 类型    | 必填 | 说明                         |
| ----------- | ------- | ---- | ---------------------------- |
| isFocusable | boolean | 是   | 点击时是否支持切换焦点窗口。true表示支持；false表示不支持。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isFocusable: boolean = true;
let promise = windowClass.setFocusable(isFocusable);
promise.then(() => {
  console.info('Succeeded in setting the window to be focusable.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the window to be focusable. Cause: ' + JSON.stringify(err));
});
```

### setKeepScreenOn<sup>(deprecated)</sup>

setKeepScreenOn(isKeepScreenOn: boolean, callback: AsyncCallback&lt;void&gt;): void

设置屏幕是否为常亮状态，使用callback异步回调。

> **说明：**
>
> 从 API version 6开始支持，从API version 9开始废弃，推荐使用[setWindowKeepScreenOn()](#setwindowkeepscreenon9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名         | 类型                      | 必填 | 说明                     |
| -------------- | ------------------------- | ---- | ------------------------ |
| isKeepScreenOn | boolean                   | 是   | 设置屏幕是否为常亮状态。true表示常亮；false表示不常亮。 |
| callback       | AsyncCallback&lt;void&gt; | 是   | 回调函数。               |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isKeepScreenOn: boolean = true;
windowClass.setKeepScreenOn(isKeepScreenOn, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the screen to be always on. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the screen to be always on.');
});
```

### setKeepScreenOn<sup>(deprecated)</sup>

setKeepScreenOn(isKeepScreenOn: boolean): Promise&lt;void&gt;

设置屏幕是否为常亮状态，使用Promise异步回调。

> **说明：**
>
> 从 API version 6开始支持，从API version 9开始废弃，推荐使用[setWindowKeepScreenOn()](#setwindowkeepscreenon9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名         | 类型    | 必填 | 说明                     |
| -------------- | ------- | ---- | ------------------------ |
| isKeepScreenOn | boolean | 是   | 设置屏幕是否为常亮状态。true表示常亮；false表示不常亮。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isKeepScreenOn: boolean = true;
let promise = windowClass.setKeepScreenOn(isKeepScreenOn);
promise.then(() => {
  console.info('Succeeded in setting the screen to be always on.');
}).catch((err: BusinessError) => {
  console.info('Failed to set the screen to be always on. Cause:  ' + JSON.stringify(err));
});
```

### setOutsideTouchable<sup>(deprecated)</sup>

setOutsideTouchable(touchable: boolean, callback: AsyncCallback&lt;void&gt;): void

设置是否允许可点击子窗口之外的区域，使用callback异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃。
>
> 从 API version 9开始，系统默认允许点击子窗口之外的区域，此接口不再支持使用，也不再提供替代接口。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名    | 类型                      | 必填 | 说明             |
| --------- | ------------------------- | ---- | ---------------- |
| touchable | boolean                   | 是   | 设置是否可点击。true表示可点击；false表示不可点击。 |
| callback  | AsyncCallback&lt;void&gt; | 是   | 回调函数。       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

if (!windowClass) {
  console.info('Failed to load the content. Cause: windowClass is null');
}
else {
  (windowClass as window.Window).setOutsideTouchable(true, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the area to be touchable. Cause: ' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the area to be touchable.');
  });
}
```

### setOutsideTouchable<sup>(deprecated)</sup>

setOutsideTouchable(touchable: boolean): Promise&lt;void&gt;

设置是否允许可点击子窗口之外的区域，使用Promise异步回调。。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃。
>
> 从 API version 9开始，系统默认允许点击子窗口之外的区域，此接口不再支持使用，也不再提供替代接口。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名    | 类型    | 必填 | 说明             |
| --------- | ------- | ---- | ---------------- |
| touchable | boolean | 是   | 设置是否可点击。true表示可点击；false表示不可点击。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

if (!windowClass) {
  console.info('Failed to load the content. Cause: windowClass is null');
}
else {
let promise = (windowClass as window.Window).setOutsideTouchable(true);
promise.then(() => {
  console.info('Succeeded in setting the area to be touchable.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the area to be touchable. Cause: ' + JSON.stringify(err));
});
}
```

### setPrivacyMode<sup>(deprecated)</sup>

setPrivacyMode(isPrivacyMode: boolean, callback: AsyncCallback&lt;void&gt;): void

设置窗口是否为隐私模式，使用callback异步回调。设置为隐私模式的窗口，窗口内容将无法被截屏或录屏。此接口可用于禁止截屏/录屏的场景。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[setWindowPrivacyMode()](#setwindowprivacymode9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名        | 类型                      | 必填 | 说明                 |
| ------------- | ------------------------- | ---- | -------------------- |
| isPrivacyMode | boolean                   | 是   | 窗口是否为隐私模式。true表示模式开启；false表示模式关闭。 |
| callback      | AsyncCallback&lt;void&gt; | 是   | 回调函数。           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isPrivacyMode: boolean = true;
windowClass.setPrivacyMode(isPrivacyMode, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the window to privacy mode. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the window to privacy mode.');
});
```

### setPrivacyMode<sup>(deprecated)</sup>

setPrivacyMode(isPrivacyMode: boolean): Promise&lt;void&gt;

设置窗口是否为隐私模式，使用Promise异步回调。设置为隐私模式的窗口，窗口内容将无法被截屏或录屏。此接口可用于禁止截屏/录屏的场景。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[setWindowPrivacyMode()](#setwindowprivacymode9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名        | 类型    | 必填 | 说明                 |
| ------------- | ------- | ---- | -------------------- |
| isPrivacyMode | boolean | 是   | 窗口是否为隐私模式。true表示模式开启；false表示模式关闭。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isPrivacyMode: boolean = true;
let promise = windowClass.setPrivacyMode(isPrivacyMode);
promise.then(() => {
  console.info('Succeeded in setting the window to privacy mode.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the window to privacy mode. Cause: ' + JSON.stringify(err));
});
```

### setTouchable<sup>(deprecated)</sup>

setTouchable(isTouchable: boolean, callback: AsyncCallback&lt;void&gt;): void

设置窗口是否为可触状态，使用callback异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[setWindowTouchable()](#setwindowtouchable9)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名      | 类型                      | 必填 | 说明                 |
| ----------- | ------------------------- | ---- | -------------------- |
| isTouchable | boolean                   | 是   | 窗口是否为可触状态。true表示可触；false表示不可触。 |
| callback    | AsyncCallback&lt;void&gt; | 是   | 回调函数。           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isTouchable = true;
if (!windowClass) {
  console.info('Failed to load the content. Cause: windowClass is null');
}
else {
  (windowClass as window.Window).setTouchable(isTouchable, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the window to be touchable. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the window to be touchable.');
  });
}
```

### setTouchable<sup>(deprecated)</sup>

setTouchable(isTouchable: boolean): Promise&lt;void&gt;

设置窗口是否为可触状态，使用Promise异步回调。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃，推荐使用[setWindowTouchable()](#setwindowtouchable9-1)。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名      | 类型    | 必填 | 说明                 |
| ----------- | ------- | ---- | -------------------- |
| isTouchable | boolean | 是   | 窗口是否为可触状态。true表示可触；false表示不可触。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let isTouchable = true;
let promise = windowClass.setTouchable(isTouchable);
promise.then(() => {
  console.info('Succeeded in setting the window to be touchable.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the window to be touchable. Cause: ' + JSON.stringify(err));
});
```

## WindowStageEventType<sup>9+</sup>

WindowStage生命周期。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 名称       | 值 | 说明       |
| ---------- | ------ | ---------- |
| SHOWN      | 1      | 切到前台。 |
| ACTIVE     | 2      | 获焦状态。 |
| INACTIVE   | 3      | 失焦状态。 |
| HIDDEN     | 4      | 切到后台。 |
| RESUMED<sup>11+</sup> | 5      | 前台可交互状态。前台应用进入多任务为不可交互状态，继续返回前台时恢复可交互状态。 |
| PAUSED<sup>11+</sup>  | 6      | 前台不可交互状态。前台应用进入多任务为不可交互状态，继续返回前台时恢复可交互状态。 |

## SubWindowOptions<sup>11+</sup>

子窗口创建参数。

**系统能力：** SystemCapability.Window.SessionManager

| 名称      | 类型  | 可读 | 可写 | 说明         |
| ---------- | ---- | ---- | ---- | ----------- |
| title    | string | 否 | 是 | 子窗口标题。       |
| decorEnabled | boolean | 否 | 是 | 子窗口是否显示装饰。true表示子窗口显示装饰，false表示子窗口不显示装饰。       |
| isModal<sup>12+</sup>    | boolean | 否 | 是 | 子窗口是否启用模态属性。true表示子窗口启用模态属性，其父级窗口不能响应用户操作，false表示子窗口禁用模态属性，其父级窗口能响应用户操作。不设置，则默认为false。       |

## WindowStage<sup>9+</sup>

窗口管理器。管理各个基本窗口单元，即[Window](#window)实例。

下列API示例中都需在[onWindowStageCreate()](../apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityonwindowstagecreate)函数中使用WindowStage的实例调用对应方法。

### getMainWindow<sup>9+</sup>

getMainWindow(callback: AsyncCallback&lt;Window&gt;): void

获取该WindowStage实例下的主窗口，使用callback异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                   | 必填 | 说明                                          |
| -------- | -------------------------------------- | ---- | --------------------------------------------- |
| callback | AsyncCallback&lt;[Window](#window)&gt; | 是   | 回调函数。返回当前WindowStage下的主窗口对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    windowStage.getMainWindow((err: BusinessError, data) => {
      const errCode: number = err.code;
      if (errCode) {
        console.error('Failed to obtain the main window. Cause: ' + JSON.stringify(err));
        return;
      }
      windowClass = data;
      console.info('Succeeded in obtaining the main window. Data: ' + JSON.stringify(data));
    });
  }
};
```

### getMainWindow<sup>9+</sup>

getMainWindow(): Promise&lt;Window&gt;

获取该WindowStage实例下的主窗口，使用Promise异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型                             | 说明                                             |
| -------------------------------- | ------------------------------------------------ |
| Promise&lt;[Window](#window)&gt; | Promise对象。返回当前WindowStage下的主窗口对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    let promise = windowStage.getMainWindow();
    promise.then((data) => {
      windowClass = data;
      console.info('Succeeded in obtaining the main window. Data: ' + JSON.stringify(data));
    }).catch((err: BusinessError) => {
      console.error('Failed to obtain the main window. Cause: ' + JSON.stringify(err));
    });
  }
};
```

### getMainWindowSync<sup>9+</sup>

getMainWindowSync(): Window

获取该WindowStage实例下的主窗口。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型 | 说明 |
| ----------------- | --------------------------------- |
| [Window](#window) | 返回当前WindowStage下的主窗口对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    try {
      let windowClass = windowStage.getMainWindowSync();
    } catch (exception) {
      console.error('Failed to obtain the main window. Cause: ' + JSON.stringify(exception));
    }
  }
};
```

### createSubWindow<sup>9+</sup>

createSubWindow(name: string, callback: AsyncCallback&lt;Window&gt;): void

创建该WindowStage实例下的子窗口，使用callback异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                   | 必填 | 说明                                          |
| -------- | -------------------------------------- | ---- | --------------------------------------------- |
| name     | string                                 | 是   | 子窗口的名字。                                |
| callback | AsyncCallback&lt;[Window](#window)&gt; | 是   | 回调函数。返回当前WindowStage下的子窗口对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    try {
      windowStage.createSubWindow('mySubWindow', (err: BusinessError, data) => {
        const errCode: number = err.code;
        if (errCode) {
          console.error('Failed to create the subwindow. Cause: ' + JSON.stringify(err));
          return;
        }
        windowClass = data;
        console.info('Succeeded in creating the subwindow. Data: ' + JSON.stringify(data));
        if (!windowClass) {
          console.info('Failed to load the content. Cause: windowClass is null');
        }
        else {
          (windowClass as window.Window).resize(500, 1000);
        }
      });

    } catch (exception) {
      console.error('Failed to create the subwindow. Cause: ' + JSON.stringify(exception));
    }
  }
};
```

### createSubWindow<sup>9+</sup>

createSubWindow(name: string): Promise&lt;Window&gt;

创建该WindowStage实例下的子窗口，使用Promise异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明           |
| ------ | ------ | ---- | -------------- |
| name   | string | 是   | 子窗口的名字。 |

**返回值：**

| 类型                             | 说明                                             |
| -------------------------------- | ------------------------------------------------ |
| Promise&lt;[Window](#window)&gt; | Promise对象。返回当前WindowStage下的子窗口对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    try {
      let promise = windowStage.createSubWindow('mySubWindow');
      promise.then((data) => {
        windowClass = data;
        console.info('Succeeded in creating the subwindow. Data: ' + JSON.stringify(data));
      }).catch((err: BusinessError) => {
        console.error('Failed to create the subwindow. Cause: ' + JSON.stringify(err));
      });
    } catch (exception) {
      console.error('Failed to create the subwindow. Cause: ' + JSON.stringify(exception));
    }
  }
};
```

### createSubWindowWithOptions<sup>11+</sup>

createSubWindowWithOptions(name: string, options: SubWindowOptions): Promise&lt;Window&gt;

创建该WindowStage实例下的子窗口，使用Promise异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名 | 类型   | 必填 | 说明           |
| ------ | ------ | ---- | -------------- |
| name   | string | 是   | 子窗口的名字。 |
| options  | [SubWindowOptions](#subwindowoptions11) | 是   | 子窗口参数。  |

**返回值：**

| 类型                             | 说明                                             |
| -------------------------------- | ------------------------------------------------ |
| Promise&lt;[Window](#window)&gt; | Promise对象。返回当前WindowStage下创建的子窗口对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    try {
      let options : window.SubWindowOptions = {
        title: 'title',
        decorEnabled: true
      };
      let promise = windowStage.createSubWindowWithOptions('mySubWindow', options);
      promise.then((data) => {
        windowClass = data;
        console.info('Succeeded in creating the subwindow. Data: ' + JSON.stringify(data));
      }).catch((err: BusinessError) => {
        console.error('Failed to create the subwindow. Cause: ' + JSON.stringify(err));
      });
    } catch (exception) {
      console.error('Failed to create the subwindow. Cause: ' + JSON.stringify(exception));
    }
  }
};
```

### getSubWindow<sup>9+</sup>

getSubWindow(callback: AsyncCallback&lt;Array&lt;Window&gt;&gt;): void

获取该WindowStage实例下的所有子窗口，使用callback异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                                | 必填 | 说明                                              |
| -------- | --------------------------------------------------- | ---- | ------------------------------------------------- |
| callback | AsyncCallback&lt;Array&lt;[Window](#window)&gt;&gt; | 是   | 回调函数。返回当前WindowStage下的所有子窗口对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300005 | This window stage is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    let windowClass: window.Window[] = [];
    windowStage.getSubWindow((err: BusinessError, data) => {
      const errCode: number = err.code;
      if (errCode) {
        console.error('Failed to obtain the subwindow. Cause: ' + JSON.stringify(err));
        return;
      }
      windowClass = data;
      console.info('Succeeded in obtaining the subwindow. Data: ' + JSON.stringify(data));
    });
  }
};
```

### getSubWindow<sup>9+</sup>

getSubWindow(): Promise&lt;Array&lt;Window&gt;&gt;

获取该WindowStage实例下的所有子窗口，使用Promise异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**返回值：**

| 类型                                          | 说明                                                 |
| --------------------------------------------- | ---------------------------------------------------- |
| Promise&lt;Array&lt;[Window](#window)&gt;&gt; | Promise对象。返回当前WindowStage下的所有子窗口对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300005 | This window stage is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    let windowClass: window.Window[] = [];
    let promise = windowStage.getSubWindow();
    promise.then((data) => {
      windowClass = data;
      console.info('Succeeded in obtaining the subwindow. Data: ' + JSON.stringify(data));
    }).catch((err: BusinessError) => {
      console.error('Failed to obtain the subwindow. Cause: ' + JSON.stringify(err));
    })
  }
};
```

### loadContent<sup>9+</sup>

loadContent(path: string, storage: LocalStorage, callback: AsyncCallback&lt;void&gt;): void

为当前WindowStage的主窗口加载具体页面内容，通过LocalStorage传递状态属性给加载的页面，使用callback异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                            | 必填 | 说明                                                         |
| -------- | ----------------------------------------------- | ---- | ------------------------------------------------------------ |
| path     | string                                          | 是   | 要加载到窗口中的页面内容的路径，该路径需添加到工程的main_pages.json文件中。  |
| storage  | [LocalStorage](../../quick-start/arkts-localstorage.md) | 是   | 页面级UI状态存储单元，这里用于为加载到窗口的页面内容传递状态属性。 |
| callback | AsyncCallback&lt;void&gt;                       | 是   | 回调函数。                                                   |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  storage: LocalStorage = new LocalStorage();

  onWindowStageCreate(windowStage: window.WindowStage) {
    this.storage.setOrCreate('storageSimpleProp', 121);
    console.log('onWindowStageCreate');
    try {
      windowStage.loadContent('pages/page2', this.storage, (err: BusinessError) => {
        const errCode: number = err.code;
        if (errCode) {
          console.error('Failed to load the content. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in loading the content.');
      });
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```

### loadContent<sup>9+</sup>

loadContent(path: string, storage?: LocalStorage): Promise&lt;void&gt;

为当前WindowStage的主窗口加载具体页面内容，通过LocalStorage传递状态属性给加载的页面，使用Promise异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名  | 类型                                            | 必填 | 说明                                                         |
| ------- | ----------------------------------------------- | ---- | ------------------------------------------------------------ |
| path    | string                                          | 是   | 要加载到窗口中的页面内容的路径，该路径需添加到工程的main_pages.json文件中。 |
| storage | [LocalStorage](../../quick-start/arkts-localstorage.md) | 否   | 页面级UI状态存储单元，这里用于为加载到窗口的页面内容传递状态属性。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  storage: LocalStorage = new LocalStorage();

  onWindowStageCreate(windowStage: window.WindowStage) {
    this.storage.setOrCreate('storageSimpleProp', 121);
    console.log('onWindowStageCreate');
    try {
      let promise = windowStage.loadContent('pages/page2', this.storage);
      promise.then(() => {
        console.info('Succeeded in loading the content.');
      }).catch((err: BusinessError) => {
        console.error('Failed to load the content. Cause:' + JSON.stringify(err));
      });
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
    ;
  }
};
```

### loadContent<sup>9+</sup>

loadContent(path: string, callback: AsyncCallback&lt;void&gt;): void

为当前WindowStage的主窗口加载具体页面内容，使用callback异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                 |
| -------- | ------------------------- | ---- | -------------------- |
| path     | string                    | 是   | 要加载到窗口中的页面内容的路径，该路径需添加到工程的main_pages.json文件中。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。           |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    try {
      windowStage.loadContent('pages/page2', (err: BusinessError) => {
        const errCode: number = err.code;
        if (errCode) {
          console.error('Failed to load the content. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in loading the content.');
      });
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```

### loadContentByName<sup>11+</sup>

loadContentByName(name: string, storage: LocalStorage, callback: AsyncCallback&lt;void&gt;): void

为当前WindowStage加载[命名路由](../../ui/arkts-routing.md#命名路由)页面，通过LocalStorage传递状态属性给加载的页面，使用callback异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                                    | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| name     | string                                                  | 是   | 命名路由页面的名称。                                             |
| storage  | [LocalStorage](../../quick-start/arkts-localstorage.md) | 是   | 页面级UI状态存储单元，这里用于为加载到窗口的页面内容传递状态属性。 |
| callback | AsyncCallback&lt;void&gt;                               | 是   | 回调函数。                                                   |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                                      |
| -------- | --------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |

**示例：**

```ts
// ets/entryability/EntryAbility.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
import * as Index from '../pages/Index'; // 导入命名路由页面

export default class EntryAbility extends UIAbility {
  // ...

  storage: LocalStorage = new LocalStorage();

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    this.storage.setOrCreate('storageSimpleProp', 121);
    try {
      windowStage.loadContentByName(Index.entryName, this.storage, (err: BusinessError) => {
        const errCode: number = err.code;
        if (errCode) {
          console.error('Failed to load the content. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in loading the content.');
      });
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```
```ts
// ets/pages/Index.ets
export const entryName : string = 'Index';
@Entry({routeName: entryName, storage : LocalStorage.getShared()})
@Component
export struct Index {
  @State message: string = 'Hello World'
  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

### loadContentByName<sup>11+</sup>

loadContentByName(name: string, callback: AsyncCallback&lt;void&gt;): void

为当前WindowStage加载[命名路由](../../ui/arkts-routing.md#命名路由)页面，使用callback异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明             |
| -------- | ------------------------- | ---- | ---------------- |
| name     | string                    | 是   | 命名路由页面的名称。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。       |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                                      |
| -------- | --------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |

**示例：**

```ts
// ets/entryability/EntryAbility.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
import * as Index from '../pages/Index'; // 导入命名路由页面

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    try {
      windowStage.loadContentByName(Index.entryName, (err: BusinessError) => {
        const errCode: number = err.code;
        if (errCode) {
          console.error('Failed to load the content. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in loading the content.');
      });
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```
```ts
// ets/pages/Index.ets
export const entryName : string = 'Index';
@Entry({routeName: entryName})
@Component
export struct Index {
  @State message: string = 'Hello World'
  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

### loadContentByName<sup>11+</sup>

loadContentByName(name: string, storage?: LocalStorage): Promise&lt;void&gt;;

为当前WindowStage加载[命名路由](../../ui/arkts-routing.md#命名路由)页面，通过LocalStorage传递状态属性给加载的页面，使用promise异步回调。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名  | 类型         | 必填 | 说明                                                         |
| ------- | ------------ | ---- | ------------------------------------------------------------ |
| name    | string       | 是   | 命名路由页面的名称。                                             |
| storage | LocalStorage | 否   | 页面级UI状态存储单元，这里用于为加载到窗口的页面内容传递状态属性。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息                                      |
| -------- | --------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |

**示例：**

```ts
// ets/entryability/EntryAbility.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
import * as Index from '../pages/Index'; // 导入命名路由页面

export default class EntryAbility extends UIAbility {
  // ...

  storage: LocalStorage = new LocalStorage();

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    this.storage.setOrCreate('storageSimpleProp', 121);
    try {
      let promise = windowStage.loadContentByName(Index.entryName, this.storage);
      promise.then(() => {
        console.info('Succeeded in loading the content.');
      }).catch((err: BusinessError) => {
        console.error('Failed to load the content. Cause:' + JSON.stringify(err));
      });
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```
```ts
// ets/pages/Index.ets
export const entryName : string = 'Index';
@Entry({routeName: entryName, storage : LocalStorage.getShared()})
@Component
export struct Index {
  @State message: string = 'Hello World'
  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

### on('windowStageEvent')<sup>9+</sup>

on(eventType: 'windowStageEvent', callback: Callback&lt;WindowStageEventType&gt;): void

开启WindowStage生命周期变化的监听。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 监听事件，固定为'windowStageEvent'，即WindowStage生命周期变化事件。 |
| callback | Callback&lt;[WindowStageEventType](#windowstageeventtype9)&gt; | 是   | 回调函数。返回当前的WindowStage生命周期状态。                |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    try {
      windowStage.on('windowStageEvent', (data) => {
        console.info('Succeeded in enabling the listener for window stage event changes. Data: ' +
        JSON.stringify(data));
      });
    } catch (exception) {
      console.error('Failed to enable the listener for window stage event changes. Cause:' +
      JSON.stringify(exception));
    }
  }
};
```

### off('windowStageEvent')<sup>9+</sup>

off(eventType: 'windowStageEvent', callback?: Callback&lt;WindowStageEventType&gt;): void

关闭WindowStage生命周期变化的监听。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 监听事件，固定为'windowStageEvent'，即WindowStage生命周期变化事件。 |
| callback | Callback&lt;[WindowStageEventType](#windowstageeventtype9)&gt; | 否   | 回调函数。返回当前的WindowStage生命周期状态。若传入参数，则关闭该监听。若未传入参数，则关闭所有WindowStage生命周期变化的监听。                |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    try {
      windowStage.off('windowStageEvent');
    } catch (exception) {
      console.error('Failed to disable the listener for window stage event changes. Cause:' +
      JSON.stringify(exception));
    }
  }
};
```

### setDefaultDensityEnabled()<sup>12+</sup>

setDefaultDensityEnabled(enabled: boolean): void

设置应用是否使用系统默认Density。

不调用此接口进行设置，则表示不使用系统默认Density，即窗口会跟随系统显示大小变化重新布局。

**模型约束：** 此接口仅可在Stage模型下使用。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名           | 类型    | 必填 | 说明                         |
| ---------------- | ------- | ---- | ---------------------------- |
| enabled | boolean | 是   | 是否设置应用使用系统默认Density。true表示使用系统默认Density，窗口不跟随系统显示大小变化重新布局；false表示不使用系统默认Density，窗口跟随系统显示大小变化重新布局。 |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID | 错误信息 |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    try {
      windowStage.setDefaultDensityEnabled(true);
    } catch (exception) {
      console.error('Failed to set default density enabled. Cause:' + JSON.stringify(exception));
    }
  }
};
```
