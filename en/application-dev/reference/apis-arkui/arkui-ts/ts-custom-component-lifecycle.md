# Custom Component Lifecycle

The lifecycle callbacks of a custom component are used to notify users of the lifecycle of the component. These callbacks are private and are invoked by the development framework at a specified time at runtime. They cannot be manually invoked from applications.

>**NOTE**
>
>- The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>- Promise and asynchronous callback functions can be used in lifecycle functions, for example, network resource getters and timer setters.


## aboutToAppear

aboutToAppear?(): void

Invoked after a new instance of the custom component is created and before its **build** function is executed. You can change state variables in the **aboutToAppear** function. The change will take effect when you execute the **build** function next time.

Since API version 9, this API is supported in ArkTS widgets.

## aboutToDisappear

aboutToDisappear?(): void

Invoked before the destructor of the custom component is consumed. Do not change state variables in the **aboutToDisappear** function as doing this can cause unexpected errors. For example, the modification of the **@Link** decorated variable may cause unstable application running.

Since API version 9, this API is supported in ArkTS widgets.

## onPageShow

onPageShow?(): void

Invoked each time the page is displayed, for example, during page redirection or when the application is switched to the foreground. It works only for the custom components decorated by **@Entry**.


## onPageHide

onPageHide?(): void

Invoked each time the page is hidden, for example, during page redirection or when the application is switched to the background. It works only for the custom components decorated by **@Entry**.


## onBackPress

onBackPress?(): void | boolean

Invoked when the user clicks the Back button. It works only for the custom components decorated by @Entry. The value **true** means that the page executes its own return logic instead of the , and **false** (default) means that the default return logic is used.


```ts
// xxx.ets
@Entry
@Component
struct IndexComponent {
  @State textColor: Color = Color.Black;

  onPageShow() {
    this.textColor = Color.Blue;
    console.info('IndexComponent onPageShow');
  }

  onPageHide() {
    this.textColor = Color.Transparent;
    console.info('IndexComponent onPageHide');
  }

  onBackPress() {
    this.textColor = Color.Red;
    console.info('IndexComponent onBackPress');
  }

  build() {
    Column() {
      Text('Hello World')
        .fontColor(this.textColor)
        .fontSize(30)
        .margin(30)
    }.width('100%')
  }
}
```
![en-us_image_lifecycle](figures/en-us_image_lifecycle.gif)

## onLayout<sup>(deprecated)</sup>

onLayout?(children: Array&lt;LayoutChild&gt;, constraint: ConstraintSizeOptions): void

Invoked when the custom component lays out its child components. Through this callback the component receives its child component layout information and size constraint from the ArkUI framework. The state variable cannot be changed in the **onLayout** callback.

This API is supported since API version 9 and deprecated since API version 10. You are advised to use [onPlaceChildren](#onplacechildren10) instead.

**Parameters**

| Name       | Type                                                        | Description              |
|------------|------------------------------------------------------------|------------------|
| children   | Array&lt;[LayoutChild](#layoutchilddeprecated)&gt;                  | Child component layout information.        |
| constraint | [ConstraintSizeOptions](ts-types.md#constraintsizeoptions) | Size constraint information of the parent component.|

## onPlaceChildren<sup>10+</sup>

onPlaceChildren?(selfLayoutInfo: GeometryInfo, children: Array&lt;Layoutable&gt;, constraint: ConstraintSizeOptions):void

Invoked when the custom component lays out its child components. Through this callback the component receives its child component size constraint from the ArkUI framework. The state variable cannot be changed in the **onPlaceChildren** callback.

Since API version 10, this API is supported in ArkTS widgets.

**Parameters**

| Name           | Type                                                        | Description              |
|----------------|------------------------------------------------------------|------------------|
| selfLayoutInfo | [GeometryInfo](#geometryinfo10)                            | Layout information of the parent component.        |
| children       | Array&lt;[Layoutable](#layoutable10)&gt;                   | Child component layout information.        |
| constraint     | [ConstraintSizeOptions](ts-types.md#constraintsizeoptions) | Size constraint information of the parent component.|

## onMeasure<sup>(deprecated)</sup>

onMeasure?(children: Array&lt;LayoutChild&gt;, constraint: ConstraintSizeOptions): void

Invoked when the custom component needs to determine its size. Through this callback the component receives its child component layout information and size constraint from the ArkUI framework. The state variable cannot be changed in the **onMeasure** callback.

This API is supported since API version 9 and deprecated since API version 10. You are advised to use [onMeasureSize](#onmeasuresize10) instead.

**Parameters**

| Name       | Type                                                        | Description              |
|------------|------------------------------------------------------------|------------------|
| children   | Array&lt;[LayoutChild](#layoutchilddeprecated)&gt;                  | Child component layout information.        |
| constraint | [ConstraintSizeOptions](ts-types.md#constraintsizeoptions) | Size constraint information of the parent component.|

## onMeasureSize<sup>10+</sup>

onMeasureSize?(selfLayoutInfo: GeometryInfo, children: Array&lt;Measurable&gt;, constraint: ConstraintSizeOptions):[SizeResult](#sizeresult10)

Invoked when the custom component needs to determine its size. Through this callback the component receives its child component layout information and size constraint from the ArkUI framework. The state variable cannot be changed in the **onMeasureSize** callback.

Since API version 10, this API is supported in ArkTS widgets.

**Parameters**

| Name           | Type                                                        | Description              |
|----------------|------------------------------------------------------------|------------------|
| selfLayoutInfo | [GeometryInfo](#geometryinfo10)                            | Layout information of the parent component.        |
| children       | Array&lt;[Measurable](#measurable10)&gt;                   | Child component layout information.        |
| constraint     | [ConstraintSizeOptions](ts-types.md#constraintsizeoptions) | Size constraint information of the parent component.|

## aboutToReuse<sup>10+</sup>

aboutToReuse?(params: { [key: string]: unknown }): void

Invoked when a reusable custom component is re-added to the node tree from the reuse cache to receive construction parameters of the component.

Since API version 10, this API is supported in ArkTS widgets.

**Parameters**

| Name   | Type                        | Description        |
|--------|----------------------------|------------|
| params | { [key: string]: unknown } | Construction parameters of the custom component.|

```ts
// xxx.ets
export class Message {
  value: string | undefined;

  constructor(value: string) {
    this.value = value
  }
}

@Entry
@Component
struct Index {
  @State switch: boolean = true

  build() {
    Column() {
      Button('Hello World')
        .fontSize(50)
        .fontWeight(FontWeight.Bold)
        .onClick(() => {
          this.switch = !this.switch
        })
      if (this.switch) {
        Child({ message: new Message('Child') })
      }
    }
    .height("100%")
    .width('100%')
  }
}

@Reusable
@Component
struct Child {
  @State message: Message = new Message('AboutToReuse');

  aboutToReuse(params: Record<string, ESObject>) {
    console.info("Recycle Child")
    this.message = params.message as Message
  }

  build() {
    Column() {
      Text(this.message.value)
        .fontSize(20)
    }
    .borderWidth(2)
    .height(100)
  }
}
```

## LayoutChild<sup>(deprecated)</sup>

Child component layout information.

This API is supported since API version 9 and deprecated since API version 10. It is supported in ArkTS widgets.


| Name        | Type                                                              | Description                 |
|------------|--------------------------------------------------------------------|---------------------|
| name       | string                                                             | Name of the child component.             |
| id         | string                                                             | ID of the child component.             |
| constraint | [ConstraintSizeOptions](ts-types.md#constraintsizeoptions)         | Constraint size of the child component.           |
| borderInfo | [LayoutBorderInfo](#layoutborderinfodeprecated)                             | Provides the border information of the child component.       |
| position   | [Position](ts-types.md#position8)                                   | Position coordinates of the child component.           |
| measure    | (childConstraint: [ConstraintSizeOptions](ts-types.md#constraintsizeoptions)) =&gt; void                            | Method called to apply the size constraint to the child component.|
| layout     | (LayoutInfo: [LayoutInfo](#layoutinfodeprecated)) =&gt; void | Method called to apply the layout information to the child component.|

## LayoutBorderInfo<sup>(deprecated)</sup>

Provides the border information of the child component.

This API is supported since API version 9 and deprecated since API version 10. It is supported in ArkTS widgets.

| Name         | Type                                | Description                     |
|-------------|--------------------------------------|-------------------------|
| borderWidth | [EdgeWidths](ts-types.md#edgewidths9) | Edge widths in different directions of the component.|
| margin      | [Margin](ts-types.md#margin)         | Margins in different directions of the component.  |
| padding     | [Padding](ts-types.md#padding)       | Paddings in different directions of the component.  |

## LayoutInfo<sup>(deprecated)</sup>

Provides the layout information of the child component.

This API is supported since API version 9 and deprecated since API version 10. It is supported in ArkTS widgets.

| Name        | Type                                                      | Description      |
|------------|------------------------------------------------------------|----------|
| position   | [Position](ts-types.md#position8)                           | Position coordinates of the child component.|
| constraint | [ConstraintSizeOptions](ts-types.md#constraintsizeoptions) | Constraint size of the child component.|

```ts
// xxx.ets
@Entry
@Component
struct Index {
  build() {
    Column() {
      CustomLayout() {
        ForEach([1, 2, 3], (index: number) => {
          Text('Sub' + index)
            .fontSize(30)
            .borderWidth(2)
        })
      }
    }
  }
}


@Component
struct CustomLayout {
  @Builder
  doNothingBuilder() {
  };

  @BuilderParam builder: () => void = this.doNothingBuilder;

  onLayout(children: Array<LayoutChild>, constraint: ConstraintSizeOptions) {
    let pos = 0;
    children.forEach((child) => {
      child.layout({ position: { x: pos, y: pos }, constraint: constraint })
      pos += 70;
    })
  }

  onMeasure(children: Array<LayoutChild>, constraint: ConstraintSizeOptions) {
    let size = 100;
    children.forEach((child) => {
      child.measure({ minHeight: size, minWidth: size, maxWidth: size, maxHeight: size })
      size += 50;
    })
  }

  build() {
    this.builder()
  }
}
```

![en-us_image_0000001511900496](figures/en-us_image_0000001511900496.png)

## GeometryInfo<sup>10+</sup>

Layout information of the parent component.

This API is supported since API version 10 and is supported in ArkTS widgets.

| Name         | Type     | Description                 |
|-------------|-----------|---------------------|
| borderWidth | [EdgeWidth](ts-types.md#edgewidths9) | Border width of the parent component.<br>Unit: vp           |
| margin      | [Margin](ts-types.md#margin)       | Margin of the parent component.<br>Unit: vp      |
| padding     | [Padding](ts-types.md#padding)   | Padding of the parent component.<br>Unit: vp|
| width  | number | Width obtained from the measurement result.<br>Unit: vp<br> **NOTE**<br>If the value is empty, the component width in percentage is returned.|
| height | number | Height obtained from the measurement result.<br>Unit: vp<br> **NOTE**<br>If the value is empty, the component height in percentage is returned.|


## Layoutable<sup>10+</sup>

Provides the child component layout information.

This API is supported since API version 10 and is supported in ArkTS widgets.

| Name        | Type                                                   | Description                 |
|------------|---------------------------------------------------------|---------------------|
| measureResult| [MeasureResult](#measureresult10)      | Measurement result of the child component.<br>Unit: vp    |
| layout     | (position: [Position](ts-types.md#position8)) =&gt; void | Method called to apply the layout information to the child component.|

## Measurable<sup>10+</sup>

Provides the child component location information.

This API is supported since API version 10 and is supported in ArkTS widgets.

| Name        | Type                                                                            | Description                                   |
|------------|----------------------------------------------------------------------------------|---------------------------------------|
| measure    | (childConstraint: [ConstraintSizeOptions](ts-types.md#constraintsizeoptions)) =&gt; [MeasureResult](#measureresult10) | Method called to apply the size constraint to the child component.<br>Return value: measurement result of the child component.|

## MeasureResult<sup>10+</sup>

Provides the measurement result of the component.

Since API version 10, this API is supported in ArkTS widgets.

| Name    | Type  | Description   |
|--------|--------|-------|
| width  | number | Width obtained from the measurement result.<br>Unit: vp|
| height | number | Height obtained from the measurement result.<br>Unit: vp|


## SizeResult<sup>10+</sup>

Provides the component size information.

Since API version 10, this API is supported in ArkTS widgets.

| Name    | Type  | Description   |
|--------|--------|-------|
| width  | number | Width obtained from the measurement result.<br>Unit: vp|
| height | number | Height obtained from the measurement result.<br>Unit: vp|

> **NOTE**
>
>- The custom layout does not support the LazyForEach syntax.
>- When a custom layout is created in builder mode, only **this.builder()** is allowed in the **build()** method of a custom component, as shown in the recommended example below.
>- The size configuration of the child component, except **aspectRatio**, is at a lower priority than that specified by **onMeasureSize**.
>- The position configuration of the child component, except **offset** and **position**, is at a lower priority than that specified by **onPlaceChildren**.
>- When using the custom layout method, you must call **onMeasureSize** and **onPlaceChildren** at the same time for the layout to display properly.
>- After **onPlaceChildren** is called, some universal attributes that affect the layout of child components, such as **align**, become ineffective.

```
// xxx.ets
@Entry
@Component
struct Index {
  build() {
    Column() {
      CustomLayout({ builder: ColumnChildren })
    }
  }
}

@Builder
function ColumnChildren() {
  ForEach([1, 2, 3], (index: number) => {// LazyForEach is not supported.
    Text('S' + index)
      .fontSize(30)
      .width(100)
      .height(100)
      .borderWidth(2)
      .offset({ x: 10, y: 20 })
  })
}

@Component
struct CustomLayout {
  @Builder
  doNothingBuilder() {
  };

  @BuilderParam builder: () => void = this.doNothingBuilder;
  @State startSize: number = 100;
  result: SizeResult = {
    width: 0,
    height: 0
  };

  onPlaceChildren(selfLayoutInfo: GeometryInfo, children: Array<Layoutable>, constraint: ConstraintSizeOptions) {
    let startPos = 300;
    children.forEach((child) => {
      let pos = startPos - child.measureResult.height;
      child.layout({ x: pos, y: pos })
    })
  }

  onMeasureSize(selfLayoutInfo: GeometryInfo, children: Array<Measurable>, constraint: ConstraintSizeOptions) {
    let size = 100;
    children.forEach((child) => {
      let result: MeasureResult = child.measure({ minHeight: size, minWidth: size, maxWidth: size, maxHeight: size })
      size += result.width / 2
      ;
    })
    this.result.width = 100;
    this.result.height = 400;
    return this.result;
  }

  build() {
    this.builder()
  }
}
```

![custom_layout10.png](figures/custom_layout10.png)
