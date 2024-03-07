# @ohos.arkui.observer (无感监听)

提供UI组件行为变化的无感监听能力。

> **说明：**
>
> 从API Version 11开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。
>

## 导入模块

```ts
import observer from '@ohos.arkui.observer'
```

## NavDestinationState

NavDestination组件状态。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称      | 值  | 说明                     |
| --------- | --- | ------------------------ |
| ON_SHOWN  | 0   | NavDestination组件显示。 |
| ON_HIDDEN | 1   | NavDestination组件隐藏。 |

## ScrollEventType

滚动事件的类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称      | 值  | 说明                     |
| --------- | --- | ------------------------ |
| SCROLL_START  | 0   | 滚动事件开始。 |
| SCROLL_STOP   | 1   | 滚动事件结束。 |

## RouterPageState

routerPage生命周期触发时对应的状态

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称              | 值  | 说明                    |
| ----------------- | --- | ----------------------- |
| ABOUT_TO_APPEAR       | 0   | page即将显示            |
| ABOUT_TO_DISAPPEAR    | 1   | page即将销毁            |
| ON_PAGE_SHOW          | 2   | page显示                |
| ON_PAGE_HIDE          | 3   | page隐藏                |
| ON_BACK_PRESS         | 4   | page返回时              |

## NavDestinationInfo

NavDestination组件信息。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称         | 类型                                               | 必填 | 说明                                         |
| ------------ | -------------------------------------------------- | ---- | -------------------------------------------- |
| navigationId | [ResourceStr](arkui-ts/ts-types.md#resourcestr) | 是   | 包含NavDestination组件的Navigation组件的id。 |
| name         | [ResourceStr](arkui-ts/ts-types.md#resourcestr) | 是   | NavDestination组件的名称。                   |
| state        | [NavDestinationState](#navdestinationstate)        | 是   | NavDestination组件的状态。                   |

## ScrollEventInfo<sup>12+</sup>

ScrollEvent滚动信息。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称         | 类型                                               | 必填 | 说明                                         |
| ------------ | -------------------------------------------------- | ---- | -------------------------------------------- |
| id           | string                                             | 是   | 滚动组件的id。                               |
| eventType    | [ScrollEventType](#ScrollEventType)                | 是   | 滚动事件的类型。                             |
| offset       | number                                             | 是   | 滚动组件的当前偏移量。                        |

## RouterPageInfo

RouterPageInfo包含的信息。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称         | 类型                                               | 必填 | 说明                                          |
| ------------ | -------------------------------------------------- | ---- | -------------------------------------------- |
| context      | [UIAbilityContext](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md) / [UIContext](./js-apis-arkui-UIContext.md) | 是   | 触发生命周期的routerPage页面对应的上下文信息 |
| index        | number                                             | 是   | 触发生命周期的routerPage在栈中的位置。         |
| name         | string                                             | 是   | 触发生命周期的routerPage页面的名称。           |
| path         | string                                             | 是   | 触发生命周期的routerPage页面的路径。           |
| state        | [RouterPageState](#routerpagestate)                | 是   | 触发生命周期的routerPage页面的状态             |

## observer.on('navDestinationUpdate')

on(type: 'navDestinationUpdate', callback: Callback\<NavDestinationInfo\>): void

监听NavDestination组件的状态变化。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名   | 类型                                                  | 必填 | 说明                                                                     |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------------------ |
| type     | string                                                | 是   | 监听事件，固定为'navDestinationUpdate'，即NavDestination组件的状态变化。 |
| callback | Callback\<[NavDestinationInfo](#navdestinationinfo)\> | 是   | 回调函数。返回当前的NavDestination组件状态。                             |

**示例：**

```ts
observer.on('navDestinationUpdate', (info) => {
    console.info('NavDestination state update', JSON.stringify(info));
});
```

## observer.off('navDestinationUpdate')

off(type: 'navDestinationUpdate', callback?: Callback\<NavDestinationInfo\>): void

取消监听NavDestination组件的状态变化。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名   | 类型                                                  | 必填 | 说明                                                                     |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------------------ |
| type     | string                                                | 是   | 监听事件，固定为'navDestinationUpdate'，即NavDestination组件的状态变化。 |
| callback | Callback\<[NavDestinationInfo](#navdestinationinfo)\> | 否   | 回调函数。返回当前的NavDestination组件状态。                             |

**示例：**

```ts
observer.off('navDestinationUpdate');
```

## observer.on('navDestinationUpdate')

on(type: 'navDestinationUpdate', options: { navigationId: ResourceStr }, callback: Callback\<NavDestinationInfo\>): void

监听NavDestination组件的状态变化。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名   | 类型                                                                 | 必填 | 说明                                                                     |
| -------- | -------------------------------------------------------------------- | ---- | ------------------------------------------------------------------------ |
| type     | string                                                               | 是   | 监听事件，固定为'navDestinationUpdate'，即NavDestination组件的状态变化。 |
| options  | { navigationId: [ResourceStr](arkui-ts/ts-types.md#resourcestr) } | 是   | 指定监听的Navigation的id。                                               |
| callback | Callback\<[NavDestinationInfo](#navdestinationinfo)\>                | 是   | 回调函数。返回当前的NavDestination组件状态。                             |

**示例：**

```ts
observer.on('navDestinationUpdate', { navigationId: "testId" }, (info) => {
    console.info('NavDestination state update', JSON.stringify(info));
});
```

## observer.off('navDestinationUpdate')

off(type: 'navDestinationUpdate', options: { navigationId: ResourceStr }, callback?: Callback\<NavDestinationInfo\>): void

取消监听NavDestination组件的状态变化。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名   | 类型                                                                 | 必填 | 说明                                                                     |
| -------- | -------------------------------------------------------------------- | ---- | ------------------------------------------------------------------------ |
| type     | string                                                               | 是   | 监听事件，固定为'navDestinationUpdate'，即NavDestination组件的状态变化。 |
| options  | { navigationId: [ResourceStr](arkui-ts/ts-types.md#resourcestr) } | 是   | 指定监听的Navigation的id。                                               |
| callback | Callback\<[NavDestinationInfo](#navdestinationinfo)\>                | 否   | 回调函数。返回当前的NavDestination组件状态。                             |

**示例：**

```ts
observer.off('navDestinationUpdate', { navigationId: "testId" });
```

## observer.on('scrollEvent')<sup>12+</sup>

on(type: 'scrollEvent', callback: Callback\<ScrollEventInfo\>): void

监听滚动事件的开始和结束。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名   | 类型                                                  | 必填 | 说明                                                                     |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------------------ |
| type     | string                                                | 是   | 监听事件，固定为'scrollEvent'，即滚动事件的开始和结束。                   |
| callback | Callback\<[ScrollEventInfo](#ScrollEventInfo)\>       | 否   | 回调函数。返回滚动事件的信息。                                           |

## observer.off('scrollEvent')<sup>12+</sup>

off(type: 'scrollEvent', callback?: Callback\<ScrollEventInfo\>): void

取消监听滚动事件的开始和结束。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名   | 类型                                                  | 必填 | 说明                                                                     |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------------------ |
| type     | string                                                | 是   | 监听事件，固定为'scrollEvent'，即滚动事件的开始和结束。                   |
| callback | Callback\<[ScrollEventInfo](#ScrollEventInfo)\>       | 否   | 回调函数。返回滚动事件的信息。                                           |

## observer.on('scrollEvent')<sup>12+</sup>

on(type: 'scrollEvent', options: { id: string }, callback: Callback\<ScrollEventInfo\>): void

监听滚动事件的开始和结束。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名   | 类型                                                                 | 必填 | 说明                                                                     |
| -------- | -------------------------------------------------------------------- | ---- | ------------------------------------------------------------------------ |
| type     | string                                                               | 是   | 监听事件，固定为'scrollEvent'，即滚动事件的开始和结束。                   |
| options  | { id: string }                                                       | 是   | 指定监听的滚动组件的id。                                                 |
| callback | Callback\<[ScrollEventInfo](#ScrollEventInfo)\>                      | 否   | 回调函数。返回滚动事件的信息。                                            |

## observer.off('scrollEvent')<sup>12+</sup>

off(type: 'scrollEvent', options: { id: string }, callback?: Callback\<ScrollEventInfo\>): void

取消监听滚动事件的开始和结束。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名   | 类型                                                                 | 必填 | 说明                                                                     |
| -------- | -------------------------------------------------------------------- | ---- | ------------------------------------------------------------------------ |
| type     | string                                                               | 是   | 监听事件，固定为'scrollEvent'，即滚动事件的开始和结束。                   |
| options  | { id: string }                                                       | 是   | 指定监听的滚动组件的id。                                                 |
| callback | Callback\<[ScrollEventInfo](#ScrollEventInfo)\>                      | 否   | 回调函数。返回滚动事件的信息。                                            |

**示例：**

```ts
import observer from '@ohos.arkui.observer'

@Entry
@Component
struct Index {
  scroller: Scroller = new Scroller();
  options: observer.ObserverOptions = { id:"testId" };
  private arr: number[] = [0, 1, 2, 3, 4, 5, 6, 7]

  build() {
    Row() {
      Column() {
        Scroll(this.scroller) {
          Column() {
            ForEach(this.arr, (item: number) => {
              Text(item.toString())
                .width('90%')
                .height(150)
                .backgroundColor(0xFFFFFF)
                .borderRadius(15)
                .fontSize(16)
                .textAlign(TextAlign.Center)
                .margin({ top: 10 })
            }, (item: string) => item)
          }.width('100%')
        }
        .id("testId")
        .height('80%')
      }
      .width('100%')

      Row() {
        Button('UIObserver on')
          .onClick(() => {
            observer.on('scrollEvent', (info) => {
              console.info('NavDestination state update', JSON.stringify(info));
            });
          })
        Button('UIObserver off')
          .onClick(() => {
            observer.off('scrollEvent', (info) => {
              console.info('NavDestination state update', JSON.stringify(info));
            });
          })
      }

      Row() {
        Button('UIObserverWithId on')
          .onClick(() => {
            observer.on('scrollEvent', this.options, (info) => {
              console.info('NavDestination state update', JSON.stringify(info));
            });
          })
        Button('UIObserverWithId off')
          .onClick(() => {
            observer.off('scrollEvent', this.options, (info) => {
              console.info('NavDestination state update', JSON.stringify(info));
            });
          })
      }
    }
    .height('100%')
  }
}
```

## observer.on('routerPageUpdate')<sup>11+</sup>

on(type: 'routerPageUpdate', context: UIAbilityContext | UIContext, callback: Callback\<observer.RouterPageInfo\>): void

监听router中page页面的状态变化。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 监听事件，固定为'routerPageUpdate'，即router中page页面的状态变化。 |
| context  | [UIAbilityContext](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md) / [UIContext](./js-apis-arkui-UIContext.md) | 是   | 上下文信息，用以指定监听页面的范围 |
| callback | Callback\<[RouterPageInfo](#routerpageinfo)\>        | 是   | 回调函数。携带pageInfo，返回当前的page页面状态。                 |

**示例：**

```ts
// used in UIAbility
import observer from '@ohos.arkui.observer';
// callBackFunc is user defined function
observer.on('routerPageUpdate', this.context, callBackFunc);
// uiContext could be got by window's function: getUIContext()
observer.on('routerPageUpdate', this.uiContext, callBackFunc);
```

## observer.off('routerPageUpdate')<sup>11+</sup>

off(type: 'routerPageUpdate', context: UIAbilityContext | UIContext, callback?: Callback\<observer.RouterPageInfo\>): void

取消监听router中page页面的状态变化。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 监听事件，固定为'routerPageUpdate'，即router中page页面的状态变化。 |
| context  | [UIAbilityContext](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md) / [UIContext](./js-apis-arkui-UIContext.md) | 是   | 上下文信息，用以指定监听页面的范围 |
| callback | Callback\<[RouterPageInfo](#routerpageinfo)\>        | 否   | 需要被注销的回调函。                 |

**示例：**

```ts
// used in UIAbility
import observer from '@ohos.arkui.observer';
// callBackFunc is user defined function
observer.off('routerPageUpdate', this.context, callBackFunc);
// uiContext could be got by window's function: getUIContext()
observer.off('routerPageUpdate', this.uiContext, callBackFunc);
```