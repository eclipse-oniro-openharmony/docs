# SceneNode
本模块提供3D图形中场景资源结点的的类型及操作方法。

> **说明：** 
> - 本模块首批接口从API version 12开始支持，后续版本的新增接口，采用上角标标记接口的起始版本。

## 导入模块
```ts
import scene3d from '@ohos.graphics.scene'
```
## LayerMask
用于定义结点的图层掩码。

### getEnabled
getEnabled(index: number): boolean

获取指定图层下标图层掩码的使能状态。

**系统能力：** SystemCapability.ArkUi.Graphics3D

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| ---- | ---- | ---- | ---- |
| index | number | 是 | 要使能图层的下标，值域为大于等于0的整数。 |

**返回值：**
| 类型 | 说明 |
| ---- | ---- |
| boolean | 返回特定下标的图层是否使能，true表示使用图层掩码，false表示不使用。 |

**示例：**
```ts
function layerMask() : void {
  let scene: Promise<scene3d.Scene> = scene3d.Scene.load($rawfile("gltf/CubeWithFloor/glTF/AnimatedCube.gltf"));
  scene.then(async (result: scene3d.Scene) => {
    if (result) {
      let node : scene3d.Node | null = result.getNodeByPath("rootNode/Scene/");
      if (node) {
          // 获取掩码的使能状态
          let enabled: Boolean = node.layerMask.getEnabled(1);
      }
    }
  });
}
```

### setEnabled

setEnabled(index: number, enabled: boolean): boolean

将特定下标的图层掩码使能。

**系统能力：** SystemCapability.ArkUi.Graphics3D

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| ---- | ---- | ---- | ---- |
| index | number | 是 | 要使能图层的下标，值域为大于等于0的整数。 |
| enabled | boolean | 是 | 要设置的使能状态，true表示使用图层掩码，false表示不使用。 |

**返回值：**
| 类型 | 说明 |
| ---- | ---- |
| boolean | 设置使能是否成功。 |

**示例：**
```ts
function layerMask() : void {
  let scene: Promise<scene3d.Scene> = scene3d.Scene.load($rawfile("gltf/CubeWithFloor/glTF/AnimatedCube.gltf"));
  scene.then(async (result: scene3d.Scene) => {
    if (result) {
      let node : scene3d.Node | null = result.getNodeByPath("rootNode/Scene/");
      if (node) {
          // 设置掩码状态
          node.layerMask.setEnabled(1, true);
      }
    }
  });
}
```

## NodeType
结点类型枚举。

**系统能力：** SystemCapability.ArkUi.Graphics3D
| 名称 | 值 | 说明 |
| ---- | ---- | ---- |
| NODE | 1 | 结点是空结点。 |
| GEOMETRY | 2 | 几何类型结点。 |
| CAMERA | 3 | 相机类型结点。 |
| LIGHT | 4 | 灯光类型结点。 |

## Container\<T>
定义场景对象的容器。容器提供了一种将场景对象分组到层次结构中的方法。

### append
append(item T): void

追加一个对象到容器。

**系统能力：** SystemCapability.ArkUi.Graphics3D

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| ---- | ---- | ---- | ---- |
| item | T | 是 | T类型对象。 |

**示例：**
```ts
function append() : void {
  let scene: Promise<scene3d.Scene> = scene3d.Scene.load($rawfile("gltf/CubeWithFloor/glTF/AnimatedCube.gltf"));
  scene.then(async (result: scene3d.Scene) => {
    if (result) {
      let node : scene3d.Node | null = result.getNodeByPath("rootNode/Scene/");
      // append 节点
      result.root?.children.get(0)?.children.append(node);
    }
  });
}
```


### insertAfter
insertAfter(item: T, sibling: T | null): void

在兄弟结点后面插入对象。

**系统能力：** SystemCapability.ArkUi.Graphics3D

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| ---- | ---- | ---- | ---- |
| item | T | 是 | 要插入结点。 |
| sibling | T \| null | 是 | 兄弟结点。 |

**示例：**
```ts
function insertAfter() : void {
  let scene: Promise<scene3d.Scene> = scene3d.Scene.load($rawfile("gltf/CubeWithFloor/glTF/AnimatedCube.gltf"));
  scene.then(async (result: scene3d.Scene) => {
    if (result) {
      let node : scene3d.Node | null = result.getNodeByPath("rootNode/Scene/");
      // insertAfter 节点
      result.root?.children.get(0)?.children.insertAfter(node, null);
    }
  });
}
```

### remove
remove(item T): void

移除指定对象。

**系统能力：** SystemCapability.ArkUi.Graphics3D

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| ---- | ---- | ---- | ---- |
| item | T | 是 | 要移除的对象。 |

**示例：**
```ts
function remove() : void {
  let scene: Promise<scene3d.Scene> = scene3d.Scene.load($rawfile("gltf/CubeWithFloor/glTF/AnimatedCube.gltf"));
  scene.then(async (result: scene3d.Scene) => {
    if (result) {
      let node : scene3d.Node | null = result.getNodeByPath("rootNode/Scene/");
      // remove 节点
      result.root?.children.remove(node);
    }
  });
}
```

### get
get(index: number): T | null

获取特定下标对象，获取不到则返回空。

**系统能力：** SystemCapability.ArkUi.Graphics3D

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| ---- | ---- | ---- | ---- |
| index | number | 是 | 要获取对象的下标，取值范围是大于等于0的整数。 |

**返回值：**
| 类型 | 说明 |
| ---- | ---- |
| T \| null | 返回获取到的对象，获取不到则返回空值。 |

**示例：**
```ts
function get() : void {
  let scene: Promise<scene3d.Scene> = scene3d.Scene.load($rawfile("gltf/CubeWithFloor/glTF/AnimatedCube.gltf"));
  scene.then(async (result: scene3d.Scene) => {
    if (result) {
      let node : scene3d.Node | null = result.getNodeByPath("rootNode/Scene/");
      // 从children中get 0号节点
      result.root?.children.get(0)?.children.insertAfter(node, null);
    }
  });
}
```

### clear
clear(): void

清空容器内的所有对象。

**系统能力：** SystemCapability.ArkUi.Graphics3D

**示例：**
```ts
function clear() : void {
  let scene: Promise<scene3d.Scene> = scene3d.Scene.load($rawfile("gltf/CubeWithFloor/glTF/AnimatedCube.gltf"));
  scene.then(async (result: scene3d.Scene) => {
    if (result) {
      let node : scene3d.Node | null = result.getNodeByPath("rootNode/Scene/");
      // 清空children节点
      result.root?.children.clear();
    }
  });
}
```

### count
count(): number

获取容器中对象的数量。

**系统能力：** SystemCapability.ArkUi.Graphics3D

**返回值：**
| 类型 | 说明 |
| ---- | ---- |
| number | 返回容器中对象个数。 |

**示例：**
```ts
function count() : void {
  let scene: Promise<scene3d.Scene> = scene3d.Scene.load($rawfile("gltf/CubeWithFloor/glTF/AnimatedCube.gltf"));
  scene.then(async (result: scene3d.Scene) => {
    if (result) {
      let node : scene3d.Node | null = result.getNodeByPath("rootNode/Scene/");
      let container: scene3d.Container<scene3d.Node> = node.children;
      // 获取children中的节点数
      let count: number = container.count();
    }
  });
}
```

## Node
3D场景由树状层次结构的结点组成，其中每个结点都实现了Node接口。继承自[SceneResource](js-apis-inner-scene-resources.md#sceneresource)。

### 属性

**系统能力：** SystemCapability.ArkUi.Graphics3D

| 名称 | 类型 | 只读 | 必填 | 说明 |
| ---- | ---- | ---- | ---- | ---- |
| position | [Position3](js-apis-inner-scene-types.md#position3) | 否 | 是 | 结点位置。 |
| rotation | [Quaternion](js-apis-inner-scene-types.md##quaternion) | 否 | 是 | 结点旋转角度。 |
| scale | [Scale3](js-apis-inner-scene-types.md##scale3) | 否 | 是 | 结点缩放。 |
| visible | boolean | 否 | 是 | 结点是否可见，true表示该节点可见，false表示不可见。 |
| nodeType | [NodeType](#nodetype) | 是 | 是 | 结点类型。 |
| layerMask | [LayerMask](#layermask) | 是 | 是 | 结点的图层掩码。 |
| path | string | 是 | 是 | 结点路径。 |
| parent | [Node](#node) \| null | 是 | 是 | 结点的父结点，不存在则为空值。 |
| children | [Container](#container)\<Node> | 是 | 是 | 结点的结点，不存在则为空值。 |

### getNodeByPath
getNodeByPath(path: string): Node | null

根据路径获取结点，如果获取不到则返回空。

**系统能力：** SystemCapability.ArkUi.Graphics3D

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| ---- | ---- | ---- | ---- |
| path | string | 是 | 场景结点层次中的路径。每层之间使用'/'符号进行分割。|

**返回值：**
| 类型 | 说明 |
| ---- | ---- |
| [Node](#node) \| null | 返回结点对象。 |

**示例：**
```ts
function getNode() : void {
  let scene: Promise<scene3d.Scene> = scene3d.Scene.load($rawfile("gltf/CubeWithFloor/glTF/AnimatedCube.gltf"));
  scene.then(async (result: scene3d.Scene) => {
    if (result && result.root) {
      // 查找节点
      let geo : scene3d.Node | null = result.root.getNodeByPath("scene/node");
    }
  });
}
```

## Geometry
几何类型，继承自Node。

### 属性

**系统能力：** SystemCapability.ArkUi.Graphics3D

| 名称 | 类型 | 只读 | 必填 | 说明 |
| ---- | ---- | ---- | ---- | ---- |
| mesh | [Mesh](js-apis-inner-scene-resources.md#mesh) | 是 | 是 | 网格属性。 |


## LightType
光源类型枚举。

**系统能力：** SystemCapability.ArkUi.Graphics3D

| 名称 | 值 | 说明 |
| ---- | ---- | ---- |
| DIRECTIONAL | 1 | 平行光类型。 |
| SPOT | 2 | 点光源类型。 |

## Light
光源，继承自Node。

### 属性

**系统能力：** SystemCapability.ArkUi.Graphics3D

| 名称 | 类型 | 只读 | 必填 | 说明 |
| ---- | ---- | ---- | ---- | ---- |
| lightType | [LightType](js-apis-inner-scene-nodes.md#lighttype) | 是 | 是 | 光源类型。 |
| color | [Color](js-apis-inner-scene-types.md#color) | 否 | 是 | 颜色。 |
| intensity | number | 否 | 是 | 光照密度，取值范围是大于0的实数。 |
| shadowEnabled | boolean | 否 | 是 | 是否使能阴影，true表示添加阴影，false表示没有阴影效果。 |
| enabled | boolean | 否 | 是 | 是否使能光源，true表示使用光源，false表示不使用。 |

## SpotLight
点光源类型，继承自Light。

## DirectionalLight
平行光类型，继承自Light。

### 属性

**系统能力：** SystemCapability.ArkUi.Graphics3D

| 名称 | 类型 | 只读 | 必填 | 说明 |
| ---- | ---- | ---- | ---- | ---- |
| nearPlane | number | 否 | 是 | 场景中的近平面，值域为(0, 1)。 |

## Camera
相机类型，Camera继承自Node。

### 属性

**系统能力：** SystemCapability.ArkUi.Graphics3D

| 名称 | 类型 | 只读 | 必填 | 说明 |
| ---- | ---- | ---- | ---- | ---- |
| fov | number | 否 | 是 | 视场。 |
| nearPlane | number | 否 | 是 | 近平面，取值在0到1之间。 |
| farPlane | number | 否 | 是 | 远平面，取值在0到1之间。 |
| viewPort | [Rect](js-apis-inner-scene-types.md#rect) | 否 | 是 | 视口。 |
| renderResolution | [Vec2](js-apis-inner-scene-types.md#vec2) | 否 | 是 | 渲染分辨率。 |
| postProcess | [PostProcessSettings](js-apis-inner-scene-post-process-settings.md#postprocesssettings) \| null | 否 | 是 | 后处理设置。 |
| clearColor | [Color](js-apis-inner-scene-types.md#color) \| null | 否 | 是 | 将渲染目标（render target）清空后的特定颜色。 |
