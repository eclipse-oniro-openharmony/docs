# Graphics

自定义节点相关属性定义的详细信息。

> **说明：**
>
> 本模块首批接口从API version 11开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import { DrawContext, Size, Offset, Position, Pivot, Scale, Translation, Matrix4, Rotation, Frame } from "@ohos.arkui.node";
```

## Size

用于返回组件布局大小的宽和高，单位为vp。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称   | 类型   | 可读 | 可写 | 说明                   |
| ------ | ------ | ---- | ---- | ---------------------- |
| width  | number | 是   | 是   | 组件的宽度，单位为vp。 |
| height | number | 是   | 是   | 组件的高度，单位为vp。 |

## Position

用于设置或返回组件的位置。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称 | 类型   | 可读 | 可写 | 说明                     |
| ---- | ------ | ---- | ---- | ------------------------ |
| x    | number | 是   | 是   | 水平方向位置，单位为vp。 |
| y    | number | 是   | 是   | 垂直方向位置，单位为vp。 |

## Frame

用于设置或返回组件的布局大小和位置，单位为vp。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称   | 类型   | 可读 | 可写 | 说明                     |
| ------ | ------ | ---- | ---- | ------------------------ |
| x      | number | 是   | 是   | 水平方向位置，单位为vp。 |
| y      | number | 是   | 是   | 垂直方向位置，单位为vp。 |
| width  | number | 是   | 是   | 组件的宽度，单位为vp。   |
| height | number | 是   | 是   | 组件的高度，单位为vp。   |

## Pivot

用于设置组件的轴心坐标，轴心会作为组件的旋转/缩放中心点，影响旋转和缩放效果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称 | 类型   | 可读 | 可写 | 说明                                                                |
| ---- | ------ | ---- | ---- | ------------------------------------------------------------------- |
| x    | number | 是   | 是   | 轴心的X轴坐标。该参数为浮点数，默认值为0.5， 取值范围为[0.0, 1.0]。 |
| y    | number | 是   | 是   | 轴心的Y轴坐标。该参数为浮点数，默认值为0.5， 取值范围为[0.0, 1.0]。 |

## Scale

用于设置组件的缩放比例。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称 | 类型   | 可读 | 可写 | 说明                                         |
| ---- | ------ | ---- | ---- | -------------------------------------------- |
| x    | number | 是   | 是   | X轴的缩放参数。该参数为浮点数，默认值为1.0。 |
| y    | number | 是   | 是   | Y轴的缩放参数。该参数为浮点数，默认值为1.0。 |

## Translation

用于设置组件的平移量。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称 | 类型   | 可读 | 可写 | 说明                         |
| ---- | ------ | ---- | ---- | ---------------------------- |
| x    | number | 是   | 是   | 水平方向的平移量，单位为vp。 |
| y    | number | 是   | 是   | 垂直方向的平移量，单位为vp。 |

## Rotation

用于设置组件的旋转角度。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称 | 类型   | 可读 | 可写 | 说明                          |
| ---- | ------ | ---- | ---- | ----------------------------- |
| x    | number | 是   | 是   | x轴方向的旋转角度，单位为vp。 |
| y    | number | 是   | 是   | y轴方向的旋转角度，单位为vp。 |
| z    | number | 是   | 是   | z轴方向的旋转角度，单位为vp。 |

## Offset

用于设置组件或效果的偏移。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称 | 类型   | 可读 | 可写 | 说明                        |
| ---- | ------ | ---- | ---- | --------------------------- |
| x    | number | 是   | 是   | x轴方向的偏移量，单位为vp。 |
| y    | number | 是   | 是   | y轴方向的偏移量，单位为vp。 |

## Matrix4

用于设置组件的变换信息，该类型为一个 4x4 矩阵，使用一个长度为16的`number[]`进行表示，例如：
```ts
const transform: Matrix4 = [
  1, 0, 45, 0,
  0, 1,  0, 0,
  0, 0,  1, 0,
  0, 0,  0, 1
]
```

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

## Vector2

用于表示包含x和y两个值的向量。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称 | 类型   | 可读 | 可写 | 说明              |
| ---- | ------ | ---- | ---- | ----------------- |
| x    | number | 是   | 是   | 向量x轴方向的值。 |
| y    | number | 是   | 是   | 向量y轴方向的值。 |

## DrawContext

图形绘制上下文，提供绘制所需的画布宽度和高度。

### size

get size(): Size

获取画布的宽度和高度。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**返回值：**

| 类型          | 说明             |
| ------------- | ---------------- |
| [Size](#size) | 画布的宽度和高度。 |

### canvas

get canvas(): Canvas

获取用于绘制的画布。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**返回值：**

| 类型          | 说明             |
| ------------- | ---------------- |
| [Canvas](../apis-arkgraphics2d/js-apis-graphics-drawing.md#canvas) | 用于绘制的画布。 |

**示例：**

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

用于设置边框的属性。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称   | 类型 | 可读 | 可写 | 说明             |
| ------ | ---- | ---- | ---- | ---------------- |
| left   | T    | 是   | 是   | 左侧边框的属性。 |
| top    | T    | 是   | 是   | 顶部边框的属性。 |
| right  | T    | 是   | 是   | 右侧边框的属性。 |
| bottom | T    | 是   | 是   | 底部边框的属性。 |

## Corners<sup>12+</sup>

Corners\<T>

用于设置四个角的圆角度数。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称        | 类型 | 可读 | 可写 | 说明                   |
| ----------- | ---- | ---- | ---- | ---------------------- |
| topLeft     | T    | 是   | 是   | 左上边框的圆角属性。   |
| topRight    | T    | 是   | 是   | 右上上边框的圆角属性。 |
| bottomLeft  | T    | 是   | 是   | 左下边框的圆角属性。   |
| bottomRight | T    | 是   | 是   | 右下边框的圆角属性。   |

## CornerRadius<sup>12+</sup>

类型定义为[Corners](#corners12)[<Vector2>](#vector2)，用于设置四个角的圆角度数。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称        | 类型                | 可读 | 可写 | 说明                             |
| ----------- | ------------------- | ---- | ---- | -------------------------------- |
| topLeft     | [Vector2](#vector2) | 是   | 是   | 左上边框的圆角度数，单位为vp。   |
| topRight    | [Vector2](#vector2) | 是   | 是   | 右上上边框的圆角度数，单位为vp。 |
| bottomLeft  | [Vector2](#vector2) | 是   | 是   | 左下边框的圆角度数，单位为vp。   |
| bottomRight | [Vector2](#vector2) | 是   | 是   | 右下边框的圆角度数，单位为vp。   |

## BorderRadiuses<sup>12+</sup>

类型定义为[Corners\<number>](#corners12)，用于设置四个角的圆角度数。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称        | 类型   | 可读 | 可写 | 说明                           |
| ----------- | ------ | ---- | ---- | ------------------------------ |
| topLeft     | number | 是   | 是   | 左上边框的圆角度数，单位为vp。 |
| topRight    | number | 是   | 是   | 右上边框的圆角度数，单位为vp。 |
| bottomLeft  | number | 是   | 是   | 左下边框的圆角度数，单位为vp。 |
| bottomRight | number | 是   | 是   | 右下边框的圆角度数，单位为vp。 |

## Rect<sup>12+</sup>

用于设置矩形的形状。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称   | 类型   | 可读 | 可写 | 说明                     |
| ------ | ------ | ---- | ---- | ------------------------ |
| left   | number | 是   | 是   | 左部边的位置，单位为vp。 |
| top    | number | 是   | 是   | 顶部边的位置，单位为vp。 |
| right  | number | 是   | 是   | 右部边的位置，单位为vp。 |
| bottom | number | 是   | 是   | 底部边的位置，单位为vp。 |

## RoundRect<sup>12+</sup>

用于设置带有圆角的矩形。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称    | 类型                          | 可读 | 可写 | 说明             |
| ------- | ----------------------------- | ---- | ---- | ---------------- |
| rect    | [Rect](#rect12)                 | 是   | 是   | 设置矩形的属性。 |
| corners | [CornerRadius](#cornerradius12) | 是   | 是   | 设置圆角的属性。 |

## Circle<sup>12+</sup>

用于设置圆形的属性。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称    | 类型   | 可读 | 可写 | 说明                      |
| ------- | ------ | ---- | ---- | ------------------------- |
| centerX | number | 是   | 是   | 圆心x轴的位置，单位为vp。 |
| centerY | number | 是   | 是   | 圆心y轴的位置，单位为vp。 |
| radius  | number | 是   | 是   | 圆形的半径，单位为vp。    |

## CommandPath<sup>12+</sup>

用于设置路径绘制的指令。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称     | 类型   | 可读 | 可写 | 说明                                                                                                                |
| -------- | ------ | ---- | ---- | ------------------------------------------------------------------------------------------------------------------- |
| commands | string | 是   | 是   | 路径绘制的指令字符串，单位为px。像素单位的转换方法请参考[像素单位转换](./arkui-ts/ts-pixel-units.md#像素单位转换)。 |

## ShapeMask<sup>12+</sup>

用于设置图形遮罩。

### constructor<sup>12+</sup>

constructor()

ShapeMask的构造函数。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### setRectShape<sup>12+</sup>

setRectShape(rect: Rect): void

用于设置矩形遮罩。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型          | 必填 | 说明         |
| ------ | ------------- | ---- | ------------ |
| rect   | [Rect](#rect12) | 是   | 矩形的形状。 |

**示例：**

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

用于设置圆角矩形遮罩。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名    | 类型                    | 必填 | 说明             |
| --------- | ----------------------- | ---- | ---------------- |
| roundRect | [RoundRect](#roundrect12) | 是   | 圆角矩形的形状。 |

**示例：**

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

用于设置圆形遮罩。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型              | 必填 | 说明         |
| ------ | ----------------- | ---- | ------------ |
| circle | [Circle](#circle12) | 是   | 圆形的形状。 |

**示例：**

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

用于设置椭圆形遮罩。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型          | 必填 | 说明           |
| ------ | ------------- | ---- | -------------- |
| oval   | [Rect](#rect12) | 是   | 椭圆形的形状。 |

**示例：**

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

用于设置路径绘制指令。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型                        | 必填 | 说明           |
| ------ | --------------------------- | ---- | -------------- |
| path   | [CommandPath](#commandpath12) | 是   | 路径绘制指令。 |

**示例：**

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

遮罩的填充颜色，使用ARGB格式。

fillColor: number

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**示例：**

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

遮罩的边框颜色，使用ARGB格式。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**示例：**

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

遮罩的边框宽度，单位为vp。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**示例：**

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

用于生成边框颜色均设置为传入值的边框颜色对象。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型   | 必填 | 说明                 |
| ------ | ------ | ---- | -------------------- |
| all    | number | 是   | 边框颜色，ARGB格式。 |

**返回值：**

| 类型                     | 说明                                   |
| ------------------------ | -------------------------------------- |
| [Edges\<number>](#edges12) | 边框颜色均设置为传入值的边框颜色对象。 |

**示例：**

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

用于生成边框宽度均设置为传入值的边框宽度对象。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型   | 必填 | 说明                 |
| ------ | ------ | ---- | -------------------- |
| all    | number | 是   | 边框宽度，单位为vp。 |

**返回值：**

| 类型                     | 说明                                   |
| ------------------------ | -------------------------------------- |
| [Edges\<number>](#edges12) | 边框宽度均设置为传入值的边框宽度对象。 |

**示例：**

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

用于生成边框样式均设置为传入值的边框样式对象。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型                                                       | 必填 | 说明       |
| ------ | ---------------------------------------------------------- | ---- | ---------- |
| all    | [BorderStyle](./arkui-ts/ts-appendix-enums.md#borderstyle) | 是   | 边框样式。 |

**返回值：**

| 类型                                                                        | 说明                                   |
| --------------------------------------------------------------------------- | -------------------------------------- |
| [Edges](#edges12)<[BorderStyle](./arkui-ts/ts-appendix-enums.md#borderstyle)> | 边框样式均设置为传入值的边框样式对象。 |

**示例：**

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

用于生成边框圆角均设置为传入值的边框圆角对象。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型   | 必填 | 说明       |
| ------ | ------ | ---- | ---------- |
| all    | number | 是   | 边框圆角。 |

**返回值：**

| 类型                              | 说明                                   |
| --------------------------------- | -------------------------------------- |
| [BorderRadiuses](#borderradiuses12) | 边框圆角均设置为传入值的边框圆角对象。 |

**示例：**

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
