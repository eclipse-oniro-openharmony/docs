# Security Component Universal Attributes


Universal attributes of security components are basic attributes applicable to all security components.


> **NOTE**
>
> This component is supported since API version 10. Updates will be marked with a superscript to indicate their earliest API version.


## Attributes

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| iconSize | [Dimension](ts-types.md#dimension10) | No| Icon size of the security component.<br>Default value: **16vp**|
| layoutDirection | [SecurityComponentLayoutDirection](#securitycomponentlayoutdirection) | No| Direction of the icon and text on the security component.<br>Default value: **SecurityComponentLayoutDirection.HORIZONTAL**|
| position | [Position](ts-types.md#position8) | No| Absolute position of the security component, that is, the offset of the component's upper left corner relative to its parent container's.<br>Default value:<br>{<br>x: 0,<br>y: 0<br>} |
| markAnchor | [Position](ts-types.md#position8) | No| Anchor of the security component for moving the component with its upper left corner as the reference point. Generally, this attribute is used together with the **position** and **offset** attributes. When used alone, it produces an effect similar to that produced by **offset**.<br>Default value:<br>{<br>x: 0,<br>y: 0<br>} |
| offset | [Position](ts-types.md#position8) | No| Relative position of the security component, that is, the offset of the component relative to itself.<br>Default value:<br>{<br>x: 0,<br>y: 0<br>} |
| fontSize | [Dimension](ts-types.md#dimension10) | No| Font size of the text on the security component.<br>Default value: **16fp**|
| fontStyle | [FontStyle](ts-appendix-enums.md#fontstyle) | No| Font style of the text on the security component.<br>Default value: **FontStyle.Normal**|
| fontWeight | number \| [FontWeight](ts-appendix-enums.md#fontweight) \| string | No| Font weight of the text on the security component.<br>Default value: **FontWeight.Medium**|
| fontFamily | string \| [Resource](ts-types.md#resource) | No| Font family of the text on the security component.<br>Default font: **'HarmonyOS Sans'**|
| fontColor | [ResourceColor](ts-types.md#resourcecolor) | No| Font color of the text on the security component.<br>Default value: **'\#ffffffff'**|
| iconColor | [ResourceColor](ts-types.md#resourcecolor) | No| Color of the icon on the security component.<br>Default value: **'\#ffffffff'**|
| backgroundColor | [ResourceColor](ts-types.md#resourcecolor) | No| Background color of the security component.<br>Default value: **\#007dff**|
| borderStyle | [BorderStyle](ts-appendix-enums.md#borderstyle) | No| Border style of the security component.<br>By default, the border style is not set.|
| borderWidth | [Dimension](ts-types.md#dimension10) | No| Border width of the security component.<br>By default, the border width is not set.|
| borderColor | [ResourceColor](ts-types.md#resourcecolor) | No| Border color of the security component.<br>By default, the border color is not set.|
| borderRadius | [Dimension](ts-types.md#dimension10) | No| Radius of the rounded border corners of the security component.|
| padding | [Padding](ts-types.md#padding) \| [Dimension](ts-types.md#dimension10) | No| Padding of the security component.<br>Default value: 12 vp for the top and bottom paddings and 24 vp for the left and right paddings|
| textIconSpace | [Dimension](ts-types.md#dimension10) | No| Space between the icon and text on the security component.<br>Default value: **4vp**|


## SecurityComponentLayoutDirection

| Name| Description|
| -------- | -------- |
| HORIZONTAL | The icon and text on security component are horizontally arranged.|
| VERTICAL | The icon and text on security component are vertically arranged.|


## Example

```ts
// xxx.ets
@Entry
@Component
struct Index {
  build() {
    Row() {
      Column() {
        // Generate a save button and set its security component attributes.
        SaveButton()
          .fontSize(35)
          .fontColor(Color.White)
          .iconSize(30)
          .layoutDirection(SecurityComponentLayoutDirection.HORIZONTAL)
          .borderWidth(1)
          .borderStyle(BorderStyle.Dashed)
          .borderColor(Color.Blue)
          .borderRadius(20)
          .fontWeight(100)
          .iconColor(Color.White)
          .padding({left:50, top:50, bottom:50, right:50})
          .textIconSpace(20)
          .backgroundColor(0x3282f6)
      }.width('100%')
    }.height('100%')
  }
}
```

![en-us_image_0000001643038221](figures/en-us_image_0000001643038221.png)
