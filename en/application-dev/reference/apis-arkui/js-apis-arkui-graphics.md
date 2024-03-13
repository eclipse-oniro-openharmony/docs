# Graphics

The **Graphics** module provides APIs for defining attributes of a custom node.

> **NOTE**
>
> The initial APIs of this module are supported since API version 11. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```ts
import { DrawContext, Size, Offset, Position, Pivot, Scale, Translation, Matrix4, Rotation, Frame } from "@ohos.arkui.node";
```

## Size

Returns the width and height of the component, in vp.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name  | Type  | Readable| Writable| Description                  |
| ------ | ------ | ---- | ---- | ---------------------- |
| width  | number | Yes  | Yes  | Width of the component, in vp.|
| height | number | Yes  | Yes  | Height of the component, in vp.|

## Position

Sets or returns the position of the component.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name| Type  | Readable| Writable| Description                    |
| ---- | ------ | ---- | ---- | ------------------------ |
| x    | number | Yes  | Yes  | Horizontal position, in vp.|
| y    | number | Yes  | Yes  | Vertical position, in vp.|

## Frame

Sets or returns the size and position of the component, in vp.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name  | Type  | Readable| Writable| Description                    |
| ------ | ------ | ---- | ---- | ------------------------ |
| x      | number | Yes  | Yes  | Horizontal position, in vp.|
| y      | number | Yes  | Yes  | Vertical position, in vp.|
| width  | number | Yes  | Yes  | Width of the component, in vp.  |
| height | number | Yes  | Yes  | Height of the component, in vp.  |

## Pivot

Sets the pivot of the component. As the rotation or scaling center of the component, the pivot affects the rotation and scaling effects.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name| Type  | Readable| Writable| Description                                                               |
| ---- | ------ | ---- | ---- | ------------------------------------------------------------------- |
| x    | number | Yes  | Yes  | X coordinate of the pivot. The value is a floating point number in the range [0.0, 1.0], and the default value is **0.5**.|
| y    | number | Yes  | Yes  | Y coordinate of the pivot. The value is a floating point number in the range [0.0, 1.0], and the default value is **0.5**.|

## Scale

Sets the scale factor of the component.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name| Type  | Readable| Writable| Description                                        |
| ---- | ------ | ---- | ---- | -------------------------------------------- |
| x    | number | Yes  | Yes  | Scale factor along the x-axis. The value is a floating point number, and the default value is **1.0**.|
| y    | number | Yes  | Yes  | Scale factor along the y-axis. The value is a floating point number, and the default value is **1.0**.|

## Translation

Sets the translation amount of the component.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name| Type  | Readable| Writable| Description                        |
| ---- | ------ | ---- | ---- | ---------------------------- |
| x    | number | Yes  | Yes  | Horizontal translation amount, in vp.|
| y    | number | Yes  | Yes  | Vertical translation amount, in vp.|

## Rotation

Sets the rotation angle of the component.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name| Type  | Readable| Writable| Description                         |
| ---- | ------ | ---- | ---- | ----------------------------- |
| x    | number | Yes  | Yes  | Rotation angle along the x-axis, in vp.|
| y    | number | Yes  | Yes  | Rotation angle along the y-axis, in vp.|
| z    | number | Yes  | Yes  | Rotation angle along the z-axis, in vp.|

## Offset

Sets the offset of the component or effect.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name| Type  | Readable| Writable| Description                       |
| ---- | ------ | ---- | ---- | --------------------------- |
| x    | number | Yes  | Yes  | Offset along the y-axis, in vp.|
| y    | number | Yes  | Yes  | Offset along the y-axis, in vp.|

## Matrix4

Sets the transformation information of the component, which is a 4 x 4 matrix represented by a 16-bit number[]. For example:
```ts
const transform: Matrix4 = [
  1, 0, 45, 0,
  0, 1,  0, 0,
  0, 0,  1, 0,
  0, 0,  0, 1
]
```

**System capability**: SystemCapability.ArkUI.ArkUI.Full

## Vector2<sup>12+</sup>

Defines a vector that contains the x and y coordinate values.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name| Type  | Readable| Writable| Description             |
| ---- | ------ | ---- | ---- | ----------------- |
| x    | number | Yes  | Yes  | X coordinate value of the vector.|
| y    | number | Yes  | Yes  | Y coordinate value of the vector.|

## DrawContext

Graphics drawing context, which provides the canvas width and height required for drawing.

### size

get size(): Size

Obtains the width and height of the canvas.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type         | Description            |
| ------------- | ---------------- |
| [Size](#size) | Width and height of the canvas.|

### canvas

get canvas(): Canvas

Obtains the canvas used for drawing.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type         | Description            |
| ------------- | ---------------- |
| [Canvas](../apis-arkgraphics2d/js-apis-graphics-drawing.md#canvas) | Canvas for drawing.|

**Example**

```ts
import { RenderNode, FrameNode, NodeController, DrawContext } from "@ohos.arkui.node";

class MyRenderNode extends RenderNode {
  flag: boolean = false;

  draw(context: DrawContext) {
    const size = context.size;
    const canvas = context.canvas;
  }
}

const renderNode = new MyRenderNode();
renderNode.frame = { x: 0, y: 0, width: 100, height: 100 };
renderNode.backgroundColor = 0xffff0000;

class MyNodeController extends NodeController {
  private rootNode: FrameNode | null = null;

  makeNode(uiContext: UIContext): FrameNode | null {
    this.rootNode = new FrameNode(uiContext);

    const rootRenderNode = this.rootNode.getRenderNode();
    if (rootRenderNode !== null) {
      rootRenderNode.appendChild(renderNode);
    }

    return this.rootNode;
  }
}

@Entry
@Component
struct Index {
  private myNodeController: MyNodeController = new MyNodeController();

  build() {
    Row() {
      NodeContainer(this.myNodeController)
    }
  }
}
```

## Edges<sup>12+</sup>

Edges\<T>

Describes the edges.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name  | Type| Readable| Writable| Description            |
| ------ | ---- | ---- | ---- | ---------------- |
| left   | T    | Yes  | Yes  | Left edge.|
| top    | T    | Yes  | Yes  | Top edge.|
| right  | T    | Yes  | Yes  | Right edge.|
| bottom | T    | Yes  | Yes  | Bottom edge.|

## Corners<sup>12+</sup>

Corners\<T>

Describes the four corners.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name       | Type| Readable| Writable| Description                  |
| ----------- | ---- | ---- | ---- | ---------------------- |
| topLeft     | T    | Yes  | Yes  | Radius of the upper left corner.  |
| topRight    | T    | Yes  | Yes  | Radius of the upper right corner.|
| bottomLeft  | T    | Yes  | Yes  | Radius of the lower left corner.  |
| bottomRight | T    | Yes  | Yes  | Radius of the lower right corner.  |

## CornerRadius<sup>12+</sup>

Sets the radius for the four corners of the [Corners](#corners12)[<Vector2>](#vector212) type.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name       | Type               | Readable| Writable| Description                            |
| ----------- | ------------------- | ---- | ---- | -------------------------------- |
| topLeft     | [Vector2](#vector212) | Yes  | Yes  | Radius of the upper left corner, in vp.  |
| topRight    | [Vector2](#vector212) | Yes  | Yes  | Radius of the upper right corner, in vp.|
| bottomLeft  | [Vector2](#vector212) | Yes  | Yes  | Radius of the lower left corner, in vp.  |
| bottomRight | [Vector2](#vector212) | Yes  | Yes  | Radius of the lower right corner, in vp.  |

## BorderRadiuses<sup>12+</sup>

Sets the radius for the four corners of the Corners\<number>](#corners12) type.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name       | Type  | Readable| Writable| Description                          |
| ----------- | ------ | ---- | ---- | ------------------------------ |
| topLeft     | number | Yes  | Yes  | Radius of the upper left corner, in vp.|
| topRight    | number | Yes  | Yes  | Radius of the upper right corner, in vp.|
| bottomLeft  | number | Yes  | Yes  | Radius of the lower left corner, in vp.|
| bottomRight | number | Yes  | Yes  | Radius of the lower right corner, in vp.|

## Rect<sup>12+</sup>

Describes a rectangle.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name  | Type  | Readable| Writable| Description                    |
| ------ | ------ | ---- | ---- | ------------------------ |
| left   | number | Yes  | Yes  | Position of the left edge, in vp.|
| top    | number | Yes  | Yes  | Position of the top edge, in vp.|
| right  | number | Yes  | Yes  | Position of the right edge, in vp.|
| bottom | number | Yes  | Yes  | Position of the bottom edge, in vp.|

## RoundRect<sup>12+</sup>

Describes a rectangle with rounded corners.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name   | Type                         | Readable| Writable| Description            |
| ------- | ----------------------------- | ---- | ---- | ---------------- |
| rect    | [Rect](#rect12)                 | Yes  | Yes  | Attributes of the rectangle.|
| corners | [CornerRadius](#cornerradius12) | Yes  | Yes  | Attributes of rounded corners.|

## Circle<sup>12+</sup>

Describes a circle.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name   | Type  | Readable| Writable| Description                     |
| ------- | ------ | ---- | ---- | ------------------------- |
| centerX | number | Yes  | Yes  | X coordinate of the center of the circle, in vp.|
| centerY | number | Yes  | Yes  | Y coordinate of the center of the circle, in vp.|
| radius  | number | Yes  | Yes  | Radius of the circle, in vp.   |

## CommandPath<sup>12+</sup>

Describes the command for drawing a path.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name    | Type  | Readable| Writable| Description                                                                                                               |
| -------- | ------ | ---- | ---- | ------------------------------------------------------------------------------------------------------------------- |
| commands | string | Yes  | Yes  | Commands for drawing a path, in px. For details about how to convert the pixel unit, see [Pixel Unit Conversion](./arkui-ts/ts-pixel-units.md#pixel-unit-conversion).|

## ShapeMask<sup>12+</sup>

Describes the shape mask.

### constructor<sup>12+</sup>

constructor()

A constructor used to create a **ShapeMask** instance.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### setRectShape<sup>12+</sup>

setRectShape(rect: Rect): void

Sets a rectangle mask.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type         | Mandatory| Description        |
| ------ | ------------- | ---- | ------------ |
| rect   | [Rect](#rect12) | Yes  | Shape of the rectangle.|

**Example**

```ts
import { RenderNode, ShapeMask, FrameNode, NodeController } from "@ohos.arkui.node";

const mask = new ShapeMask();
mask.setRectShape({ left: 0, right: 150, top: 0, bottom: 150 });
mask.fillColor = 0X55FF0000;

const renderNode = new RenderNode();
renderNode.frame = { x: 0, y: 0, width: 150, height: 150 };
renderNode.backgroundColor = 0XFF00FF00;
renderNode.shapeMask = mask;


class MyNodeController extends NodeController {
  private rootNode: FrameNode | null = null;

  makeNode(uiContext: UIContext): FrameNode | null {
    this.rootNode = new FrameNode(uiContext);

    const rootRenderNode = this.rootNode.getRenderNode();
    if (rootRenderNode !== null) {
      rootRenderNode.appendChild(renderNode);
    }

    return this.rootNode;
  }
}

@Entry
@Component
struct Index {
  private myNodeController: MyNodeController = new MyNodeController();

  build() {
    Row() {
      NodeContainer(this.myNodeController)
    }
  }
}
```

### setRoundRectShape<sup>12+</sup>

setRoundRectShape(roundRect: RoundRect): void

Sets the mask in the shape of a rectangle with rounded corners.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name   | Type                   | Mandatory| Description            |
| --------- | ----------------------- | ---- | ---------------- |
| roundRect | [RoundRect](#roundrect12) | Yes  | Shape of the rectangle with rounded corners.|

**Example**

```ts
import { RenderNode, ShapeMask, FrameNode, NodeController, RoundRect } from "@ohos.arkui.node";

const mask = new ShapeMask();
const roundRect: RoundRect = {
  rect: { left: 0, top: 0, right: 150, bottom: 150 },
  corners: {
    topLeft: { x: 32, y: 32 },
    topRight: { x: 32, y: 32 },
    bottomLeft: { x: 32, y: 32 },
    bottomRight: { x: 32, y: 32 }
  }
}
mask.setRoundRectShape(roundRect);
mask.fillColor = 0X55FF0000;

const renderNode = new RenderNode();
renderNode.frame = { x: 0, y: 0, width: 150, height: 150 };
renderNode.backgroundColor = 0XFF00FF00;
renderNode.shapeMask = mask;


class MyNodeController extends NodeController {
  private rootNode: FrameNode | null = null;

  makeNode(uiContext: UIContext): FrameNode | null {
    this.rootNode = new FrameNode(uiContext);

    const rootRenderNode = this.rootNode.getRenderNode();
    if (rootRenderNode !== null) {
      rootRenderNode.appendChild(renderNode);
    }

    return this.rootNode;
  }
}

@Entry
@Component
struct Index {
  private myNodeController: MyNodeController = new MyNodeController();

  build() {
    Row() {
      NodeContainer(this.myNodeController)
    }
  }
}
```

### setCircleShape<sup>12+</sup>

setCircleShape(circle: Circle): void

Sets a round mask.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type             | Mandatory| Description        |
| ------ | ----------------- | ---- | ------------ |
| circle | [Circle](#circle12) | Yes  | Round shape.|

**Example**

```ts
import { RenderNode, ShapeMask, FrameNode, NodeController } from "@ohos.arkui.node";

const mask = new ShapeMask();
mask.setCircleShape({ centerY: 75, centerX: 75, radius: 75 });
mask.fillColor = 0X55FF0000;

const renderNode = new RenderNode();
renderNode.frame = { x: 0, y: 0, width: 150, height: 150 };
renderNode.backgroundColor = 0XFF00FF00;
renderNode.shapeMask = mask;


class MyNodeController extends NodeController {
  private rootNode: FrameNode | null = null;

  makeNode(uiContext: UIContext): FrameNode | null {
    this.rootNode = new FrameNode(uiContext);

    const rootRenderNode = this.rootNode.getRenderNode();
    if (rootRenderNode !== null) {
      rootRenderNode.appendChild(renderNode);
    }

    return this.rootNode;
  }
}

@Entry
@Component
struct Index {
  private myNodeController: MyNodeController = new MyNodeController();

  build() {
    Row() {
      NodeContainer(this.myNodeController)
    }
  }
}
```

### setOvalShape<sup>12+</sup>

setOvalShape(oval: Rect): void

Sets an oval mask.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type         | Mandatory| Description          |
| ------ | ------------- | ---- | -------------- |
| oval   | [Rect](#rect12) | Yes  | Oval shape.|

**Example**

```ts
import { RenderNode, ShapeMask, FrameNode, NodeController } from "@ohos.arkui.node";

const mask = new ShapeMask();
mask.setOvalShape({ left: 0, right: 150, top: 0, bottom: 100 });
mask.fillColor = 0X55FF0000;

const renderNode = new RenderNode();
renderNode.frame = { x: 0, y: 0, width: 150, height: 150 };
renderNode.backgroundColor = 0XFF00FF00;
renderNode.shapeMask = mask;


class MyNodeController extends NodeController {
  private rootNode: FrameNode | null = null;

  makeNode(uiContext: UIContext): FrameNode | null {
    this.rootNode = new FrameNode(uiContext);

    const rootRenderNode = this.rootNode.getRenderNode();
    if (rootRenderNode !== null) {
      rootRenderNode.appendChild(renderNode);
    }

    return this.rootNode;
  }
}

@Entry
@Component
struct Index {
  private myNodeController: MyNodeController = new MyNodeController();

  build() {
    Row() {
      NodeContainer(this.myNodeController)
    }
  }
}
```

### setCommandPath<sup>12+</sup>

setCommandPath(path: CommandPath): void

Sets the command for drawing a path.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type                       | Mandatory| Description          |
| ------ | --------------------------- | ---- | -------------- |
| path   | [CommandPath](#commandpath12) | Yes  | Command for drawing a path.|

**Example**

```ts
import { RenderNode, ShapeMask, FrameNode, NodeController } from "@ohos.arkui.node";

const mask = new ShapeMask();
mask.setCommandPath({ commands: "M100 0 L0 100 L50 200 L150 200 L200 100 Z" });
mask.fillColor = 0X55FF0000;

const renderNode = new RenderNode();
renderNode.frame = { x: 0, y: 0, width: 150, height: 150 };
renderNode.backgroundColor = 0XFF00FF00;
renderNode.shapeMask = mask;


class MyNodeController extends NodeController {
  private rootNode: FrameNode | null = null;

  makeNode(uiContext: UIContext): FrameNode | null {
    this.rootNode = new FrameNode(uiContext);

    const rootRenderNode = this.rootNode.getRenderNode();
    if (rootRenderNode !== null) {
      rootRenderNode.appendChild(renderNode);
    }

    return this.rootNode;
  }
}

@Entry
@Component
struct Index {
  private myNodeController: MyNodeController = new MyNodeController();

  build() {
    Row() {
      NodeContainer(this.myNodeController)
    }
  }
}
```

### fillColor<sup>12+</sup>

Describes the fill color of the mask, in ARGB format.

fillColor: number

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Example**

```ts
import { RenderNode, ShapeMask, FrameNode, NodeController } from "@ohos.arkui.node";

const mask = new ShapeMask();
mask.setRectShape({ left: 0, right: 150, top: 0, bottom: 150 });
mask.fillColor = 0X55FF0000;

const renderNode = new RenderNode();
renderNode.frame = { x: 0, y: 0, width: 150, height: 150 };
renderNode.backgroundColor = 0XFF00FF00;
renderNode.shapeMask = mask;


class MyNodeController extends NodeController {
  private rootNode: FrameNode | null = null;

  makeNode(uiContext: UIContext): FrameNode | null {
    this.rootNode = new FrameNode(uiContext);

    const rootRenderNode = this.rootNode.getRenderNode();
    if (rootRenderNode !== null) {
      rootRenderNode.appendChild(renderNode);
    }

    return this.rootNode;
  }
}

@Entry
@Component
struct Index {
  private myNodeController: MyNodeController = new MyNodeController();

  build() {
    Row() {
      NodeContainer(this.myNodeController)
    }
  }
}
```

### strokeColor<sup>12+</sup>

strokeColor: number

Sets the stroke color for the mask, in ARGB format.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Example**

```ts
import { RenderNode, ShapeMask, FrameNode, NodeController } from "@ohos.arkui.node";

const mask = new ShapeMask();
mask.setRectShape({ left: 0, right: 150, top: 0, bottom: 150 });
mask.strokeColor = 0XFFFF0000;
mask.strokeWidth = 24;

const renderNode = new RenderNode();
renderNode.frame = { x: 0, y: 0, width: 150, height: 150 };
renderNode.backgroundColor = 0XFF00FF00;
renderNode.shapeMask = mask;


class MyNodeController extends NodeController {
  private rootNode: FrameNode | null = null;

  makeNode(uiContext: UIContext): FrameNode | null {
    this.rootNode = new FrameNode(uiContext);

    const rootRenderNode = this.rootNode.getRenderNode();
    if (rootRenderNode !== null) {
      rootRenderNode.appendChild(renderNode);
    }

    return this.rootNode;
  }
}

@Entry
@Component
struct Index {
  private myNodeController: MyNodeController = new MyNodeController();

  build() {
    Row() {
      NodeContainer(this.myNodeController)
    }
  }
}
```

### strokeWidth<sup>12+</sup>

strokeWidth: number

Sets the stroke width for the mask, in vp.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Example**

```ts
import { RenderNode, ShapeMask, FrameNode, NodeController } from "@ohos.arkui.node";

const mask = new ShapeMask();
mask.setRectShape({ left: 0, right: 150, top: 0, bottom: 150 });
mask.strokeColor = 0XFFFF0000;
mask.strokeWidth = 24;

const renderNode = new RenderNode();
renderNode.frame = { x: 0, y: 0, width: 150, height: 150 };
renderNode.backgroundColor = 0XFF00FF00;
renderNode.shapeMask = mask;


class MyNodeController extends NodeController {
  private rootNode: FrameNode | null = null;

  makeNode(uiContext: UIContext): FrameNode | null {
    this.rootNode = new FrameNode(uiContext);

    const rootRenderNode = this.rootNode.getRenderNode();
    if (rootRenderNode !== null) {
      rootRenderNode.appendChild(renderNode);
    }

    return this.rootNode;
  }
}

@Entry
@Component
struct Index {
  private myNodeController: MyNodeController = new MyNodeController();

  build() {
    Row() {
      NodeContainer(this.myNodeController)
    }
  }
}
```

## edgeColors<sup>12+</sup>

function edgeColors(all: number): Edges\<number>

Generates an **edgeColors** object with the specified edge color for all edges.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type  | Mandatory| Description                |
| ------ | ------ | ---- | -------------------- |
| all    | number | Yes  | Edge color, in ARGB format.|

**Return value**

| Type                    | Description                                  |
| ------------------------ | -------------------------------------- |
| [Edges\<number>](#edges12) | **edgeColors** object whose edge colors are all at the specified value.|

**Example**

```ts
import { RenderNode, FrameNode, NodeController, edgeColors } from "@ohos.arkui.node";

const renderNode = new RenderNode();
renderNode.frame = { x: 0, y: 0, width: 150, height: 150 };
renderNode.backgroundColor = 0XFF00FF00;
renderNode.borderWidth = { left: 8, top: 8, right: 8, bottom: 8 };
renderNode.borderColor = edgeColors(0xFF0000FF);


class MyNodeController extends NodeController {
  private rootNode: FrameNode | null = null;

  makeNode(uiContext: UIContext): FrameNode | null {
    this.rootNode = new FrameNode(uiContext);

    const rootRenderNode = this.rootNode.getRenderNode();
    if (rootRenderNode !== null) {
      rootRenderNode.appendChild(renderNode);
    }

    return this.rootNode;
  }
}

@Entry
@Component
struct Index {
  private myNodeController: MyNodeController = new MyNodeController();

  build() {
    Row() {
      NodeContainer(this.myNodeController)
    }
  }
}
```

## edgeWidths<sup>12+</sup>

function edgeWidths(all: number): Edges\<number>

Generates an **edgeWidths** object with the specified edge width for all edges.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type  | Mandatory| Description                |
| ------ | ------ | ---- | -------------------- |
| all    | number | Yes  | Edge width, in vp.|

**Return value**

| Type                    | Description                                  |
| ------------------------ | -------------------------------------- |
| [Edges\<number>](#edges12) | **edgeWidths** object whose edge widths are all at the specified value.|

**Example**

```ts
import { RenderNode, FrameNode, NodeController, edgeWidths } from "@ohos.arkui.node";

const renderNode = new RenderNode();
renderNode.frame = { x: 0, y: 0, width: 150, height: 150 };
renderNode.backgroundColor = 0XFF00FF00;
renderNode.borderWidth = edgeWidths(8);
renderNode.borderColor = { left: 0xFF0000FF, top: 0xFF0000FF, right: 0xFF0000FF, bottom: 0xFF0000FF };


class MyNodeController extends NodeController {
  private rootNode: FrameNode | null = null;

  makeNode(uiContext: UIContext): FrameNode | null {
    this.rootNode = new FrameNode(uiContext);

    const rootRenderNode = this.rootNode.getRenderNode();
    if (rootRenderNode !== null) {
      rootRenderNode.appendChild(renderNode);
    }

    return this.rootNode;
  }
}

@Entry
@Component
struct Index {
  private myNodeController: MyNodeController = new MyNodeController();

  build() {
    Row() {
      NodeContainer(this.myNodeController)
    }
  }
}
```

## borderStyles<sup>12+</sup>

function borderStyles(all: BorderStyle): Edges\<BorderStyle>

Generates a **borderStyles** object with the specified border style color for all borders.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type                                                      | Mandatory| Description      |
| ------ | ---------------------------------------------------------- | ---- | ---------- |
| all    | [BorderStyle](./arkui-ts/ts-appendix-enums.md#borderstyle) | Yes  | Border style.|

**Return value**

| Type                                                                       | Description                                  |
| --------------------------------------------------------------------------- | -------------------------------------- |
| [Edges](#edges12)<[BorderStyle](./arkui-ts/ts-appendix-enums.md#borderstyle)> | **borderStyles** object whose borders are all in the specified style.|

**Example**

```ts
import { RenderNode, FrameNode, NodeController, borderStyles } from "@ohos.arkui.node";

const renderNode = new RenderNode();
renderNode.frame = { x: 0, y: 0, width: 150, height: 150 };
renderNode.backgroundColor = 0XFF00FF00;
renderNode.borderWidth = { left: 8, top: 8, right: 8, bottom: 8 };
renderNode.borderColor = { left: 0xFF0000FF, top: 0xFF0000FF, right: 0xFF0000FF, bottom: 0xFF0000FF };
renderNode.borderStyle = borderStyles(BorderStyle.Dotted);


class MyNodeController extends NodeController {
  private rootNode: FrameNode | null = null;

  makeNode(uiContext: UIContext): FrameNode | null {
    this.rootNode = new FrameNode(uiContext);

    const rootRenderNode = this.rootNode.getRenderNode();
    if (rootRenderNode !== null) {
      rootRenderNode.appendChild(renderNode);
    }

    return this.rootNode;
  }
}

@Entry
@Component
struct Index {
  private myNodeController: MyNodeController = new MyNodeController();

  build() {
    Row() {
      NodeContainer(this.myNodeController)
    }
  }
}
```

## borderRadiuses<sup>12+</sup>

function borderRadiuses(all: number): BorderRadiuses

Generates a **borderRadiuses** object with the specified radius for all border corners.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type  | Mandatory| Description      |
| ------ | ------ | ---- | ---------- |
| all    | number | Yes  | Radius of border corners.|

**Return value**

| Type                             | Description                                  |
| --------------------------------- | -------------------------------------- |
| [BorderRadiuses](#borderradiuses12) | **borderRadiuses** object whose border corners all have the specified radius.|

**Example**

```ts
import { RenderNode, FrameNode, NodeController, borderRadiuses } from "@ohos.arkui.node";

const renderNode = new RenderNode();
renderNode.frame = { x: 0, y: 0, width: 150, height: 150 };
renderNode.backgroundColor = 0XFF00FF00;
renderNode.borderRadius = borderRadiuses(32);


class MyNodeController extends NodeController {
  private rootNode: FrameNode | null = null;

  makeNode(uiContext: UIContext): FrameNode | null {
    this.rootNode = new FrameNode(uiContext);

    const rootRenderNode = this.rootNode.getRenderNode();
    if (rootRenderNode !== null) {
      rootRenderNode.appendChild(renderNode);
    }

    return this.rootNode;
  }
}

@Entry
@Component
struct Index {
  private myNodeController: MyNodeController = new MyNodeController();

  build() {
    Row() {
      NodeContainer(this.myNodeController)
    }
  }
}
```
