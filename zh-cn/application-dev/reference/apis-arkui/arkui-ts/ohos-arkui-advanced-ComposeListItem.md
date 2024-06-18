# @ohos.arkui.advanced.ComposeListItem (列表)


列表包含一系列相同宽度的列表项。内容包括适合连续、多行呈现同类数据的组合，例如图片和文本。


> **说明：**
>
> 该组件从API Version 10开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 导入模块

```
import { ComposeListItem } from "@ohos.arkui.advanced.ComposeListItem"
```


## 子组件

无

## 属性
支持[通用属性](ts-universal-attributes-size.md)


## ComposeListItem

ComposeListItem({contentItem?: ContentItem, operateItem?: OperateItem})

**装饰器类型：**\@Component

**系统能力：** SystemCapability.ArkUI.ArkUI.Full


**参数：**


| 名称 | 类型 | 必填 | 装饰器类型 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| contentItem | [ContentItem](#contentitem) | 否 | \@Prop | 定义左侧以及中间元素。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| operateItem | [OperateItem](#operateitem) | 否 | \@Prop | 定义右侧元素。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| composeItemPadding<sup>12+</sup> | [LocalizedPadding](ts-types.md#localizedpadding12) | 否 | \@Prop | 两侧边距，作用于该组件最外层元素左右侧边距，取值范围大于等于0vp。<br/>默认值：<br/>{ start: LengthMetrics.vp(12), end: LengthMetrics.vp(12) }。|
| itemSpace<sup>12+</sup> | number | 否 | \@Prop | 组件内部元素间距，作用于左侧内容区图标与文本间距，以及左侧内容区与右侧操作区间距，取值范围大于等于0。<br/>默认值：12，单位为vp，其表示左侧内容区内图标和文字间距12vp；左侧内容区和右侧操作区间距12vp。|

## ContentItem


| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| iconStyle | [IconType](#icontype) | 否 | 左侧元素的图标样式。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| icon | [ResourceStr](ts-types.md#resourcestr) | 否 | 左侧元素的图标资源。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| primaryText | [ResourceStr](ts-types.md#resourcestr) | 否 | 中间元素的标题内容。<br/>**文字超长默认处理规则：** API version 12 以下，超出以“...”显示，API version 12及以上超出一行后换行显示。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| secondaryText | [ResourceStr](ts-types.md#resourcestr) | 否 | 中间元素的副标题内容。<br/>**文字超长默认处理规则：** API version 12 以下，超出以“...”显示，API version 12及以上超出一行后换行显示。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| description | [ResourceStr](ts-types.md#resourcestr) | 否 | 中间元素的描述内容。<br/>**文字超长默认处理规则：** API version 12 以下，超出以“...”显示，API version 12及以上超出一行后换行显示。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| iconImageModifier<sup>12+</sup> | [ImageModifier](ts-universal-attributes-attribute-modifier.md) | 否 |自定义左侧元素中的图片资源属性，包含尺寸、圆角等。|
| primaryTextModifier<sup>12+</sup> | [TextModifier](ts-universal-attributes-attribute-modifier.md) | 否 |自定义中间元素的标题内容样式属性，包含文本样式、尺寸、颜色、透明度等。|
| secondaryTextModifier<sup>12+</sup> | [TextModifier](ts-universal-attributes-attribute-modifier.md) | 否 |自定义中间元素的副标题内容样式属性，包含文本样式、尺寸、颜色、透明度等。|
| descriptionModifier<sup>12+</sup> | [TextModifier](ts-universal-attributes-attribute-modifier.md) | 否 |自定义中间元素的描述内容样式属性，包含文本样式、尺寸、颜色、透明度等。|

## IconType

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| BADGE | 1 | 左侧图标为badge类型，图标大小为8\*8dp。 |
| NORMAL_ICON | 2 | 左侧图标为小图标类型，图标大小为16\*16dp。 |
| SYSTEM_ICON | 3 | 左侧图标为系统图标类型，图标大小为24\*24dp。 |
| HEAD_SCULPTURE | 4 | 左侧图标为头像类型，图标大小为40\*40dp。 |
| APP_ICON | 5 | 左侧图标为应用图标类型，图标大小为64\*64dp。 |
| PREVIEW | 6 | 左侧图标为预览图类型，图标大小为96\*96dp。 |
| LONGITUDINAL | 7 | 左侧图标为横向特殊比例（宽比高大），保持最长边为96dp。 |
| VERTICAL | 8 | 左侧图标为竖向特殊比例（高比宽大），保持最长边为96dp。 |

## OperateItem

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| arrow | [OperateIcon](#operateicon) | 否 | 右侧元素为箭头，大小为12\*24dp。 |
| icon | [OperateIcon](#operateicon) | 否 | 右侧元素的第一个图标，大小为24\*24dp。 |
| subIcon | [OperateIcon](#operateicon) | 否 | 右侧元素的第二个图标，大小为24\*24dp。 |
| button | [OperateButton](#operatebutton) | 否 | 右侧元素为按钮。 |
| switch | [OperateCheck](#operatecheck) | 否 | 右侧元素为开关。 |
| checkbox | [OperateCheck](#operatecheck) | 否 | 右侧元素为多选框，大小为24\*24dp。 |
| radio | [OperateCheck](#operatecheck) | 否 | 右侧元素为单选，大小为24\*24dp。 |
| image | [ResourceStr](ts-types.md#resourcestr) | 否 | 右侧元素为图片，大小为48\*48dp。 |
| text | [ResourceStr](ts-types.md#resourcestr) | 否 | 右侧元素为文字。 |

## OperateIcon

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | [ResourceStr](ts-types.md#resourcestr) | 是 | 右侧图标/箭头资源。 |
| action | ()=&gt;void | 否 | 右侧图标/箭头点击事件。 |

## OperateButton

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| text | [ResourceStr](ts-types.md#resourcestr) | 否 | 右侧按钮文字。 |

## OperateCheck

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| isCheck | boolean | 否 | 右侧Switch/CheckBox/Radio选中状态。<br> isCheck默认值为false。<br> isCheck为true时，表示为选中。<br> isCheck为false时，表示为未选中。 |
| onChange | (value:&nbsp;boolean)=&gt;void | 否 | 右侧Switch/CheckBox/Radio选中状态改变时触发回调。<br> value为true时，表示从未选中变为选中。<br> value为false时，表示从选中变为未选中。 |

## 事件
支持[通用事件](ts-universal-events-click.md)

## 示例

### 示例1

```ts
// 该示例主要演示该组件的基础功能使用，包含左侧右侧元素的情况
import { IconType, ComposeListItem, promptAction } from '@kit.ArkUI';

@Entry
@Component
struct ComposeListItemExample {
  build() {
    Column() {
      List() {
        ListItem() {
          ComposeListItem({
            contentItem: ({
              iconStyle: IconType.NORMAL_ICON,
              icon: $r('sys.media.ohos_app_icon'),
              primaryText: '双行列表',
              secondaryText: '辅助文字',
              description: '描述内容文字'
            }),
            operateItem: ({
              icon: {
                value: $r('sys.media.ohos_app_icon'),
                action: () => {
                  promptAction.showToast({ message: 'icon' });
                } },
              text: '右侧文本'
            })
          })
        }
      }
    }
  }
}
```
![示例4-左右元素+文本](figures/zh-cn_image_composelistitem_demo_01.jpg)

### 示例2
```ts
// 该示例主要演示该组件在基础功能上，对图片、文字进行自定义功能
import { IconType, ComposeListItem, promptAction, LengthMetrics } from '@kit.ArkUI';
import { TextModifier, ImageModifier } from '@ohos.arkui.modifier';

@Entry
@Component
struct ComposeListItemExample {

  @State iconImageModifier: ImageModifier =
    new ImageModifier().height(16).width(16).borderRadius(4);
  @State primaryTextModifier: TextModifier =
    new TextModifier().fontSize(18).fontColor(Color.Blue);
  @State secondaryTextModifier: TextModifier =
    new TextModifier().fontSize(14).fontColor(Color.Red);
  @State descriptionModifier: TextModifier =
    new TextModifier().fontSize(12).fontColor(Color.Black);

  build() {
    Column() {
      List() {
        ListItem() {
          ComposeListItem({
            contentItem: ({
              iconStyle: IconType.NORMAL_ICON,
              icon: $r('sys.media.ohos_app_icon'),
              primaryText: '双行列表',
              secondaryText: '辅助文字',
              description: '描述内容文字',
              iconImageModifier: this.iconImageModifier,
              primaryTextModifier: this.primaryTextModifier,
              secondaryTextModifier: this.secondaryTextModifier,
              descriptionModifier: this.descriptionModifier
            }),
            operateItem: ({
              icon: {
                value: $r('sys.media.ohos_app_icon'),
                action: () => {
                  promptAction.showToast({ message: 'icon' });
                }
              },
              text: '右侧文本'
            }),
            itemSpace: 12,
            composeItemPadding: { start: LengthMetrics.vp(12), end: LengthMetrics.vp(12) }
          })
        }
      }
    }
  }
}
```
![示例4-ComposeListItem示例 左右元素+文本](figures/zh-cn_image_composelistitem_demo_02.jpg)