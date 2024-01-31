# 组件内隐式共享元素转场（geometryTransition）

geometryTransition用于组件内隐式共享元素转场，在组件显示切换过程中提供平滑过渡效果。通用transition机制提供了opacity、scale等转场动效，geometryTransition通过id绑定in/out组件(in指入场组件、out指出场组件)，使得组件原本独立的transition动画在空间位置上发生联系，从而将视觉焦点由出场组件位置引导到入场组件位置。

> **说明：**
>
> 从API Version 7开始支持，从API Version 10开始生效。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。

## 属性

| 名称               | 参数类型                                                     | 参数描述                                                     |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| geometryTransition | id: string, <br />options<sup>11+</sup>?: { follow?: boolean <br />} | -id：用于设置绑定关系，id置""清除绑定关系避免参与共享行为，id可更换重新建立绑定关系。同一个id只能有两个组件绑定且是in/out不同类型角色，不能多个组件绑定同一个id。<br />-follow：仅用于if范式下标记始终在组件树上的组件是否跟随做共享动画，默认值：false。 |

> **说明：**
>
> [geometryTransition](ts-transition-animation-geometrytransition.md)必须配合[animateTo](ts-explicit-animation.md)使用才有动画效果，动效时长、曲线跟随[animateTo](ts-explicit-animation.md)中的配置，不支持[animation](ts-animatorproperty.md)隐式动画。

## 示例

```ts
// xxx.ets
@Entry
@Component
struct Index {
  @State isShow: boolean = false

  build() {
    Stack({ alignContent: Alignment.Center }) {
      if (this.isShow) {
        Image($r('app.media.pic'))
          .autoResize(false)
          .clip(true)
          .width(300)
          .height(400)
          .offset({ y: 100 })
          .geometryTransition("picture")
          .transition(TransitionEffect.OPACITY)
      } else {
        // geometryTransition此处绑定的是容器，那么容器内的子组件需设为相对布局跟随父容器变化，
        // 套多层容器为了说明相对布局约束传递
        Column() {
          Column() {
            Image($r('app.media.icon'))
              .width('100%').height('100%')
          }.width('100%').height('100%')
        }
        .width(80)
        .height(80)
        // geometryTransition会同步圆角，但仅限于geometryTransition绑定处，此处绑定的是容器
        // 则对容器本身有圆角同步而不会操作容器内部子组件的borderRadius
        .borderRadius(20)
        .clip(true)
        .geometryTransition("picture")
        // transition保证组件离场不被立即析构，可设置其他转场效果
        .transition(TransitionEffect.OPACITY)
      }
    }
    .onClick(() => {
      animateTo({ duration: 1000 }, () => {
        this.isShow = !this.isShow
      })
    })
  }
}
```
![geometrytransition](figures/geometrytransition.gif)


