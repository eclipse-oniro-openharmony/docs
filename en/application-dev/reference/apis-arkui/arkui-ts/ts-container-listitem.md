# ListItem

The **\<ListItem>** component displays specific items in the list. It must be used together with **\<List>**.

> **NOTE**
>
> - This component is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.
> - The parent of this component can only be [\<List>](ts-container-list.md) or [\<ListItemGroup>](ts-container-listitemgroup.md).

## Child Components

This component can contain a single child component.

## APIs

Since API version 9, this API is supported in ArkTS widgets.

### ListItem<sup>10+</sup>

ListItem(value?: ListItemOptions)

**Parameters**

| Name| Type                                     | Mandatory| Description                                                    |
| ------ | --------------------------------------------- | ---- | ------------------------------------------------------------ |
| value  | [ListItemOptions](#listitemoptions10) | No  | Value of the list item, containing the **style** parameter of the **ListItemStyle** enum type.|

### ListItem<sup>(deprecated)</sup>

ListItem(value?: string)

This API is deprecated since API version 10. You are advised to use [ListItem<sup>10+</sup>](#listitem10) instead.

**Parameters**

| Name| Type                     | Mandatory| Description|
| ------ | ----------------------------- | ---- | -------- |
| value  | string | No  | N/A      |

## Attributes

In addition to the [universal attributes](ts-universal-attributes-size.md), the following attributes are supported.

### sticky<sup>(deprecated)</sup>

sticky(value: Sticky)

Sets the sticky effect of the list item.

This attribute is deprecated since API version 9. You are advised to use [the sticky attribute of the \<List> component](ts-container-list.md#attributes) instead.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type                               | Mandatory| Description                                      |
| ------ | ----------------------------------- | ---- | ------------------------------------------ |
| value  | [Sticky](#stickydeprecated) | Yes  | Sticky effect of the list item.<br>Default value: **Sticky.None**|

### editable<sup>(deprecated)</sup>

editable(value: boolean | EditMode)

Sets whether to enable edit mode, where the list item can be deleted or moved.

This API is deprecated since API version 9. There is no substitute API.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type                                                        | Mandatory| Description                                      |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------ |
| value  | boolean \| [EditMode](#editmodedeprecated) | Yes  | Whether to enable edit mode.<br>Default value: **false**|

### selectable<sup>8+</sup>

selectable(value: boolean)

Sets whether the list item is selectable for multiselect. This attribute takes effect only when mouse frame selection is enabled for the parent **\<List>** container.

**Widget capability**: Since API version 9, this API is supported in ArkTS widgets.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type   | Mandatory| Description                                             |
| ------ | ------- | ---- | ------------------------------------------------- |
| value  | boolean | Yes  | whether the list item is selectable for multiselect.<br>Default value: **true**|

### selected<sup>10+</sup>

selected(value: boolean)

Sets whether the list item is selected. This attribute supports two-way binding through [$$](../../../quick-start/arkts-two-way-sync.md). This attribute must be used before the [style for the selected state](./ts-universal-attributes-polymorphic-style.md) is set. Otherwise, the style settings will not take effect.

**Widget capability**: Since API version 10, this API is supported in ArkTS widgets.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type   | Mandatory| Description                                    |
| ------ | ------- | ---- | ---------------------------------------- |
| value  | boolean | Yes  | Whether the list item is selected.<br>Default value: **false**|

### swipeAction<sup>9+</sup>

swipeAction(value: SwipeActionOptions)

Sets the swipe action item displayed when the list item is swiped out from the screen edge.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type                                             | Mandatory| Description                |
| ------ | ------------------------------------------------- | ---- | -------------------- |
| value  | [SwipeActionOptions](#swipeactionoptions) | Yes  | Swipe action item displayed when the list item is swiped out from the screen edge.|

## Sticky<sup>(deprecated)</sup>
This API is deprecated since API version 9. You are advised to use [the stickyStyle enum of the \<List> component](ts-container-list.md#stickystyle9) instead.
| Name| Value| Description|
| -------- | -------- | -------- |
| None |  0  | The list item is not sticky.|
| Normal |  1  | The list item is sticky with no special effects.|
| Opacity |  2  | The list item is sticky with opacity changes.|

## EditMode<sup>(deprecated)</sup>
This API is deprecated since API version 9. There is no substitute API.
| Name    | Value| Description       |
| ------ | ------ | --------- |
| None   |  0  | The editing operation is not restricted.   |
| Deletable |  1  | The list item can be deleted.|
| Movable |  2  | The list item can be moved.|

## SwipeEdgeEffect<sup>9+</sup>
| Name    | Value| Description       |
| ------ | ------ | --------- |
|   Spring   |    0    | When the list item scrolls to the edge of the list, it can continue to scroll for a distance.<br>If the delete area is set, the list item can continue to scroll after the scroll distance exceeds the delete threshold and,<br>after being released, rebound following the spring curve.|
|   None   |    1    | The list item cannot scroll beyond the edge of the list.<br>If the delete area is set, the list item cannot continue to scroll after the scroll distance exceeds the delete threshold.<br>If the delete callback is set, it is triggered when the delete threshold is reached and the list item is released.|

## SwipeActionOptions

The top level of the @builder function corresponding to **start** and **end** must be a single component and cannot be an **if/else**, **ForEach**, or **LazyForEach** statement.

The swipe gesture works only in the list item area. If a swipe causes a child component to extend beyond the list item area, the portion outside the area does not respond to the swipe. In light of this, avoid setting **swipeAction** to a component too wide in a multi-column list.

| Name                        | Type                                                        | Mandatory| Description                                                        |
| ---------------------------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| start                        | [CustomBuilder](ts-types.md#custombuilder8) \| [SwipeActionItem](#swipeactionitem10) | No  | Swipe action item displayed on the left of the list item when the item is swiped right (in vertical list layout) or above the list item when the item is swiped down (in horizontal list layout).|
| end                          | [CustomBuilder](ts-types.md#custombuilder8) \| [SwipeActionItem](#swipeactionitem10) | No  | Swipe action item displayed on the right of the list item when the item is swiped left (in vertical list layout) or below the list item when the item is swiped up (in horizontal list layout).|
| edgeEffect                   | [SwipeEdgeEffect](#swipeedgeeffect9)                 | No  | Scroll effect.                                                  |
| onOffsetChange<sup>11+</sup> | (offset: number) => void                                     | No  | Triggered when the scroll offset changes.                                  |

## SwipeActionItem<sup>10+</sup>

Describes the swipe action item.

For a list in vertical layout, it refers to the delete option displayed on the left (or right) of the list item when the list item is swiped right (or left).

For a list in horizontal layout, it refers to the delete option displayed below (or above) the list item when the list item is swiped up (or down).

| Name                | Type                                                    | Mandatory| Description                                                        |
| -------------------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| actionAreaDistance | [Length](ts-types.md#length) | No| Swipe distance threshold for deleting the list item.<br>Default value: **56vp**<br>**NOTE**<br>This parameter cannot be set in percentage.<br>If the value is greater than the list item width minus the width of **swipeAction**, or is less than or equal to 0, the delete area will not be set.|
| onAction | () => void | No| Callback invoked when the list item is released while in the delete area.<br>**NOTE**<br> This callback is invoked only when the list item is released in a position that meets or goes beyond the specified swipe distance threshold (which must be valid) for deleting the list item.|
| onEnterActionArea | () => void | No| Callback invoked each time the list item enters the delete area.|
| onExitActionArea | () => void | No|Callback invoked each time the list item exits the delete area.|
| builder |  [CustomBuilder](ts-types.md#custombuilder8) | No|Swipe action item displayed when the list item is swiped left or right (in vertical list layout) or up or down (in horizontal list layout).|
| onStateChange<sup>11+</sup> | (swipeActionState) => void | No|Triggered when the swipe state of the list item changes.|
## ListItemOptions<sup>10+</sup>

| Name | Type                                 | Mandatory| Description                                                        |
| ----- | ----------------------------------------- | ---- | ------------------------------------------------------------ |
| style | [ListItemStyle](#listitemstyle10) | No  | Style of the list item.<br>Default value: **ListItemStyle.NONE**<br>If this parameter is set to **ListItemStyle.NONE**, no style is applied.<br>If this parameter is set to **ListItemStyle.CARD**, the default card style is applied, but only when **ListItemGroupStyle.CARD** is set for [\<ListItemGroup>](ts-container-listitemgroup.md).<br>In the default card style, the list item has a 48 vp height and 100% width.<br>It can be in focus, hover, press, selected, or disable style depending on the state.<br>**NOTE**<br>In the default card style, the list has its **listDirection** attribute fixed at **Axis.Vertical** and<br>**alignListItem** attribute at **ListItemAlign.Center**.<br>If **ListItemStyle.CARD** is set and **ListItemGroupStyle.CARD** is not, only some card styles and functions are available.|

## SwipeActionOptions<sup>10+</sup>

| Name                        | Type                | Mandatory| Description                                                        |
| ---------------------------- | ------------------------ | ---- | ------------------------------------------------------------ |
| onOffsetChange<sup>11+</sup> | (offset: number) => void | No  | Triggered when the location of the list item changes, in vp, when it is swiped left or right (in vertical list layout) or up or down (in horizontal list layout).|

## ListItemStyle<sup>10+</sup>

| Name| Value | Description              |
| ---- | ---- | ------------------ |
| NONE | 0 | No style.          |
| CARD | 1 | Default card style.|

## SwipeActionState<sup>11+</sup>

| Name     | Value    | Description                                                        |
| --------- | --------- | ------------------------------------------------------------ |
| COLLAPSED | 0 | Collapsed state.<br>When the list item is swiped left or right (in vertical list layout) or up or down (in horizontal list layout), the swipe action item is hidden.|
| EXPANDED  | 1 | Expanded state.<br>When the list item is swiped left or right (in vertical list layout) or up or down (in horizontal list layout), the swipe action item is shown.<br>**NOTE**<br>When the list item is swiped left or right (in vertical list layout)<br>or up or down (in horizontal list layout), the swipe action item is shown.|
| ACTIONING | 2 | In-action state. The list item is in this state when it enters the delete area.<br>**NOTE**<br>A list item can enter this state only when it is released in a position that meets or goes beyond the specified swipe distance threshold (which must be valid) for deleting the list item.|

## Events

### onSelect<sup>8+</sup>

onSelect(event: (isSelected: boolean) =&gt; void)

Triggered when the selected state of the list item for multiselect changes.

**Widget capability**: Since API version 10, this API is supported in ArkTS widgets.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name    | Type   | Mandatory| Description                                                        |
| ---------- | ------- | ---- | ------------------------------------------------------------ |
| isSelected | boolean | Yes  | Returns **true** if the list item is selected for multselect; returns **false** otherwise.|

## Example

### Example 1

```ts
// xxx.ets
@Entry
@Component
struct ListItemExample {
  private arr: number[] = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

  build() {
    Column() {
      List({ space: 20, initialIndex: 0 }) {
        ForEach(this.arr, (item: number) => {
          ListItem() {
            Text('' + item)
              .width('100%')
              .height(100)
              .fontSize(16)
              .textAlign(TextAlign.Center)
              .borderRadius(10)
              .backgroundColor(0xFFFFFF)
          }
        }, (item: string) => item)
      }.width('90%')
      .scrollBar(BarState.Off)
    }.width('100%').height('100%').backgroundColor(0xDCDCDC).padding({ top: 5 })
  }
}
```

![en-us_image_0000001219864159](figures/en-us_image_0000001219864159.gif)

### Example 2


```ts
// xxx.ets
@Entry
@Component
struct ListItemExample2 {
  @State arr: number[] = [0, 1, 2, 3, 4]
  @State enterEndDeleteAreaString: string = "not enterEndDeleteArea"
  @State exitEndDeleteAreaString: string = "not exitEndDeleteArea"

  @Builder itemEnd() {
    Row() {
      Button("Delete").margin("4vp")
      Button("Set").margin("4vp")
    }.padding("4vp").justifyContent(FlexAlign.SpaceEvenly)
  }

  build() {
    Column() {
      List({ space: 10 }) {
        ForEach(this.arr, (item: number) => {
          ListItem() {
            Text("item" + item)
              .width('100%')
              .height(100)
              .fontSize(16)
              .textAlign(TextAlign.Center)
              .borderRadius(10)
              .backgroundColor(0xFFFFFF)
          }
          .transition({ type: TransitionType.Delete, opacity: 0 })
          .swipeAction({
            end: {
              builder: () => { this.itemEnd() },
              onAction: () => {
                animateTo({ duration: 1000 }, () => {
                  let index = this.arr.indexOf(item)
                  this.arr.splice(index, 1)
                })
              },
              actionAreaDistance: 56,
              onEnterActionArea: () => {
                this.enterEndDeleteAreaString = "enterEndDeleteArea"
                this.exitEndDeleteAreaString = "not exitEndDeleteArea"
              },
              onExitActionArea: () => {
                this.enterEndDeleteAreaString = "not enterEndDeleteArea"
                this.exitEndDeleteAreaString = "exitEndDeleteArea"
              }
            }
          })
        }, (item: string) => item)
      }
      Text(this.enterEndDeleteAreaString).fontSize(20)
      Text(this.exitEndDeleteAreaString).fontSize(20)
    }
    .padding(10)
    .backgroundColor(0xDCDCDC)
    .width('100%')
    .height('100%')
  }
}
```
![deleteListItem](figures/deleteListItem.gif)

### Example 3

```ts
// xxx.ets
@Entry
@Component
struct ListItemExample3 {
  build() {
    Column() {
      List({ space: "4vp", initialIndex: 0 }) {
        ListItemGroup({ style: ListItemGroupStyle.CARD }) {
          ForEach([ListItemStyle.CARD, ListItemStyle.CARD, ListItemStyle.NONE], (itemStyle: number, index?: number) => {
            ListItem({ style: itemStyle }) {
              Text("" + index)
                .width("100%")
                .textAlign(TextAlign.Center)
            }
          })
        }
        ForEach([ListItemStyle.CARD, ListItemStyle.CARD, ListItemStyle.NONE], (itemStyle: number, index?: number) => {
          ListItem({ style: itemStyle }) {
            Text("" + index)
              .width("100%")
              .textAlign(TextAlign.Center)
          }
        })
      }
      .width('100%')
      .multiSelectable(true)
      .backgroundColor(0xDCDCDC)
    }
    .width('100%')
    .padding({ top: 5 })
  }
}
```
![ListItemStyle](figures/listItem3.jpeg)
