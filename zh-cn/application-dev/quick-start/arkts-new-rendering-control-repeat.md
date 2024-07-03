# Repeat：子组件复用

>**说明：**
>
>Repeat从API version 12开始支持。
>
>当前状态管理（V2试用版）仍在逐步开发中，相关功能尚未成熟，建议开发者尝鲜试用。

Repeat组件不开启virtualScroll开关时，Repeat基于数组类型数据来进行循环渲染，需要与容器组件配合使用，且接口返回的组件应当是允许包含在Repeat父容器组件中的子组件。Repeat循环渲染和ForEach相比有两个区别，一是优化了部分更新场景下的渲染性能，二是组件生成函数的索引index由框架侧来维护。

Repeat组件开启virtualScroll开关时，Repeat将从提供的数据源中按需迭代数据，并在每次迭代过程中创建相应的组件。当在滚动容器中使用了Repeat，框架会根据滚动容器可视区域按需创建组件，当组件滑出可视区域外时，框架会缓存组件，并在下一次迭代中使用。

## 接口描述

### Repeat组件构造

```ts
declare const Repeat: <T>(arr: Array<T>) => RepeatAttribute<T>
```

参数说明：

| 参数名 | 参数类型   | 是否必填 | 参数描述                                               |
| ------ | ---------- | -------- | ------------------------------------------------------ |
| arr    | Array\<T\> | 是       | 数据源，为`Array<T>`类型的数组，由开发者决定数据类型。 |

### Repeat组件属性

```ts
declare class RepeatAttribute<T> {
  each(itemGenerator: (repeatItem: RepeatItem<T>) => void): RepeatAttribute<T>;
  key(keyGenerator: (item: T, index: number) => string): RepeatAttribute<T>;
  virtualScroll(virtualScrollOptions?: VirtualScrollOptions): RepeatAttribute<T>;
  template(type: string, itemBuilder: RepeatItemBuilder<T>, templateOptions?: TemplateOptions): RepeatAttribute<T>;
  templateId(typedFunc: TemplateTypedFunc<T>): RepeatAttribute<T>;
}
```

参数说明：

| 属性名        | 参数类型                                                     | 参数描述                                                     |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| each          | itemGenerator: (repeatItem: RepeatItem\<T\>) => void         | 组件生成函数。<br/>**说明：**<br/>- `each`属性必须有，否则运行时会报错。<br/>- `itemGenerator`的参数为`RepeatItem`，该参数将`item`和`index`结合到了一起，请勿将`RepeatItem`参数拆开使用。 |
| key           | keyGenerator: (item: T, index: number) => string             | 键值生成函数。<br/>- 为数组中的每个元素创建对应的键值。<br/>- `item`：`arr`数组中的数据项。<br/>- `index`：`arr`数组中的数据项索引。 |
| virtualScroll | virtualScrollOptions?: VirtualScrollOptions                  | `Repeat`开启虚拟滚动。<br/>-`virtualScrollOptions`：虚拟滚动配置项。 |
| template      | type: string, itemBuilder: RepeatItemBuilder\<T\>, templateOptions?: TemplateOptions | 复用模板。<br/>未开启virtualScroll时暂不支持，复用有问题。<br/>-`type`：当前模板类型。<br/>-`itemBuilder`：组件生成函数。<br/>-`templateOptions`：当前模板配置项。 |
| templateId    | typedFunc: TemplateTypedFunc\<T\>                              | 为当前数据项分配模板类型。<br/>-`typedFunc`：生成当前数据项对应的模板类型。<br/>template和templateId匹配不上的数据项走默认生成函数each。 |

### RepeatItem类型

```ts
interface RepeatItem<T> {
  item: T,
  index?: number
}
```

属性说明：

| 属性名 | 类型   | 是否必填 | 描述                                         |
| ------ | ------ | -------- | -------------------------------------------- |
| item   | T      | 是       | arr中每一个数据项。T为开发者传入的数据类型。 |
| index  | number | 否       | 当前数据项对应的索引。                       |

### VirtualScrollOptions类型

```
interface VirtualScrollOptions {
  totalCount?: number;
}
```

属性说明：

| 属性名     | 类型   | 是否必填 | 描述                                                         |
| ---------- | ------ | -------- | ------------------------------------------------------------ |
| totalCount | number | 否       | 当前数据总数，数据长度判断规则：totalCount ? max(totalCount, 数据源长度) : 数据源长度。<br/>用户可以不同步请求所有数据，从而实现正确的滚动条样式。 |

### RepeatItemBuilder类型

```
declare type RepeatItemBuilder<T> = (repeatItem: RepeatItem<T>) => void;
```

参数说明：

| 参数名     | 类型          | 是否必填      | 描述                                    |
| ---------- | ------------- | --------------------------------------- | --------------------------------------- |
| repeatItem | RepeatItem\<T\> | 是 | 将item和index结合到一起的一个状态变量。 |

### TemplateOptions类型

```
interface TemplateOptions {
  cachedCount?: number
}
```

属性说明：

| 属性名      | 类型   | 是否必填 | 描述                                                         |
| ----------- | ------ | -------- | ------------------------------------------------------------ |
| cachedCount | number | 否       | 当前模板在Repeat的缓存池中可缓存子节点的最大数量，默认值为1，仅在开启virtualScroll后生效。<br/>each方法的cache默认为1，不能修改。 |

### TemplateTypedFunc类型

```
declare type TemplateTypedFunc<T> = (item : T, index : number) => string;
```

参数说明：

| 参数名 | 类型   | 是否必填 | 描述                                         |
| ------ | ------ | -------- | -------------------------------------------- |
| item   | T      | 是       | arr中每一个数据项。T为开发者传入的数据类型。 |
| index  | number | 是       | 当前数据项对应的索引。                       |

## 使用限制

- Repeat必须在容器组件内使用，仅有[List](../reference/apis-arkui/arkui-ts/ts-container-list.md)、[ListItemGroup](../reference/apis-arkui/arkui-ts/ts-container-listitemgroup.md)、[Grid](../reference/apis-arkui/arkui-ts/ts-container-grid.md)、[Swiper](../reference/apis-arkui/arkui-ts/ts-container-swiper.md)以及[WaterFlow](../reference/apis-arkui/arkui-ts/ts-container-waterflow.md)组件支持虚拟滚动（此时配置cachedCount会生效）。其它容器组件使用Repeat时请不要打开virtualScroll开关。
- Repeat开启virtualScroll后，在每次迭代中，必须创建且只允许创建一个子组件。不开启virtualScroll没有该限制。
- 生成的子组件必须是允许包含在Repeat父容器组件中的子组件。
- 允许Repeat包含在if/else条件渲染语句中，也允许Repeat中出现if/else条件渲染语句。
- Repeat内部使用键值作为标识，因此键值生成器必须针对每个数据生成唯一的值，如果多个数据同一时刻生成的键值相同，会导致UI组件渲染出现问题。
- 未开启virtualScroll目前暂时不支持template模板，复用会有问题。

## 键值生成规则

### non-virtualScroll规则

![Repeat-Slide](./figures/Repeat-NonVirtualScroll-Key.PNG)

### virtualScroll规则

和non-virtualScroll的键值生成规则基本一致，但是不会自动处理重复的键值，需要开发者自己保证键值的唯一性。

![Repeat-Slide](./figures/Repeat-VirtualScroll-Key.PNG)

## 组件生成及复用规则

### non-virtualScroll规则

子组件在Repeat首次渲染时全部创建，在数据更新时会对原组件进行复用。

在Repeat组件进行数据更新时，它会依次对比上次的所有键值和本次更新之后的区别。若当前键值和上次的某一项键值相同，Repeat会直接复用子组件并对RepeatItem.index索引做对应的更新。

当Repeat将所有重复的键值对比完并做了相应的复用后，若上次的键值有不重复的且本次更新之后有新的键值生成需要新建子组件时，Repeat会复用上次多余的子组件并更新RepeatItem.item数据源和RepeatItem.index索引并刷新UI。

若上次的剩余>=本次新更新的数量，则组件完全复用并释放多余的未被复用的组件。若上次的剩余小于本次新更新的数量，将剩余的组件复用完后，Repeat会新建多出来的数据项对应的组件。

### virtualScroll规则

子组件在Repeat首次渲染只生成当前需要的组件，在滑动和数据更新时会缓存下屏的节点，在需要生成新的组件时，对缓存里的组件进行复用。

#### 滑动场景

滑动前节点现状如下图所示

![Repeat-Start](./figures/Repeat-Start.PNG)

当前Repeat组件templateId有a和b两种，templateId a对应的缓存池，其最大缓存值为3，templateId b对应的缓存池，其最大缓存值为4，其父组件默认预加载节点1个。这时，我们将屏幕右滑，Repeat将开始复用缓存池中的节点。

![Repeat-Slide](./figures/Repeat-Slide.PNG)

index=18的数据进入屏幕及父组件预加载的范围内，此时计算出其templateId为b，这时Repeat会从type=b的缓存池中取出一个节点进行复用，更新它的key&index&data，该子节点内部使用了该项数据及索引的其他孙子节点会根据V2状态管理的规则做同步更新。

index=10的节点划出了屏幕及父组件预加载的范围。当UI主线程空闲时，会去检测type=a的缓存池是否还有空间，此时缓存池中有四个节点，超过了额定的3个，Repeat会释放掉最后一个节点。

![Repeat-Slide-Done](./figures/Repeat-Slide-Done.PNG)

#### 数据更新场景

![Repeat-Start](./figures/Repeat-Start.PNG)

此时我们做如下更新操作，删除index=12节点，更新index=13节点的数据，更新index=14节点的templateId为a，更新index=15节点的key。

![Repeat-Update1](./figures/Repeat-Update1.PNG)

此时Repeat会通知父组件重新布局，首先会一一对比key值，若和原节点key值相同且templateId相同，则复用该节点，更新index和data，若key值不同，则复用相同的templateId缓存池中的节点，并更新key、index和data。

![Repeat-Update2](./figures/Repeat-Update2.PNG)

上图显示node13节点更新了数据data和index，node14更新了templateId，node15由于key值发生变化，于是从缓存池中取走一个复用，并同步更新key、index、data，node16和node17均只更新index。index=17的节点是新的，从缓存池中复用。

![Repeat-Update-Done](./figures/Repeat-Update-Done.PNG)

## 使用场景

### non-virtualScroll

#### 数据源变化

在Repeat组件进行非首次渲染时，它会依次对比上次的所有键值和本次更新之后的区别。若当前键值和上次的某一项键值相同，Repeat会直接复用子组件并对RepeatItem.index索引做对应的更新。

当Repeat将所有重复的键值对比完并做了相应的复用后，若上次的键值有不重复的且本次更新之后有新的键值生成需要新建子组件时，Repeat会复用上次多余的子组件并更新RepeatItem.item数据源和RepeatItem.index索引。

若上次的剩余>=本次新更新的数量，则组件完全复用，若上次的剩余小于本次新更新的数量，将剩余的组件复用完后，Repeat会新建多出来的数据项对应的组件。

```ts
@Entry
@Component
struct Parent {
  @State simpleList: Array<string> = ['one', 'two', 'three'];

  build() {
    Row() {
      Column() {
        Text('点击修改第3个数组项的值')
          .fontSize(24)
          .fontColor(Color.Red)
          .onClick(() => {
            this.simpleList[2] = 'new three';
          })

        Repeat<string>(this.simpleList)
            .each((obj: RepeatItem<string>)=>{
              ChildItem({ item: obj.item })
                .margin({top: 20})
            })
            .key((item: string) => item)
      }
      .justifyContent(FlexAlign.Center)
      .width('100%')
      .height('100%')
    }
    .height('100%')
    .backgroundColor(0xF1F3F5)
  }
}

@Component
struct ChildItem {
  @Prop item: string;

  build() {
    Text(this.item)
      .fontSize(30)
  }
}
```

Repeat非首次渲染案例运行效果图  
![ForEach-Non-Initial-Render-Case-Effect](./figures/ForEach-Non-Initial-Render-Case-Effect.gif)

第三个数组项重新渲染时会复用之前的第三项的组件，仅对数据做了刷新。

#### 索引值变化

下方例子当我们交换数组项1和2时，若键值和上次保持一致，Repeat会复用之前的组件，仅对使用了index索引值的组件做数据刷新。

```ts
@Entry
@Component
struct Parent {
  @State simpleList: Array<string> = ['one', 'two', 'three'];

  build() {
    Row() {
      Column() {
        Text('交换数组项1，2')
          .fontSize(24)
          .fontColor(Color.Red)
          .onClick(() => {
            let temp: string = this.simpleList[2]
            this.simpleList[2] = this.simpleList[1]
            this.simpleList[1] = temp
          })
          .margin({bottom: 20})

        Repeat<string>(this.simpleList)
          .each((obj: RepeatItem<string>)=>{
            Text("index: " + obj.index)
              .fontSize(30)
            ChildItem({ item: obj.item })
              .margin({bottom: 20})
          })
          .key((item: string) => item)
      }
      .justifyContent(FlexAlign.Center)
      .width('100%')
      .height('100%')
    }
    .height('100%')
    .backgroundColor(0xF1F3F5)
  }
}

@Component
struct ChildItem {
  @Prop item: string;

  build() {
    Text(this.item)
      .fontSize(30)
  }
}
```

Repeat交换数据更新index运行效果图  
![Repeat-Non-Initial-Render-Case-Exchange-Effect](./figures/Repeat-Non-Initial-Render-Case-Exchange-Effect.gif)
