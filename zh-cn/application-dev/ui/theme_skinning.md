# 设置主题换肤

## 概述

针对应用，构建ArkUI应用级和页面级主题设置能力，并提供局部深浅色模式设置、动态换肤等功能。
本文提供如下场景：
- [自定义品牌色](#自定义品牌色)
- [应用级自定义品牌色](#设置应用级自定义品牌色)
- [局部页面自定义主题风格](#设置应用局部页面自定义主题风格)
- [局部深浅色](#设置应用页面局部深浅色)


## 自定义品牌色
[CustomTheme](../reference/apis-arkui/js-apis-arkui-theme.md#customtheme)用于自定义主题，属性可选，只需要复写修改的部分，未修改内容继承于系统。请参考：

  ```ts
    import { CustomColors, CustomTheme } from '@ohos.arkui.theme'

    export class AppColors implements CustomColors {
      //自定义品牌色
      brand: ResourceColor = '#FF75D9';
    }

    export class AppTheme implements CustomTheme {
      public colors: AppColors = new AppColors()
    }
    
    export let gAppTheme: CustomTheme = new AppTheme()
  ```

## 设置应用级自定义品牌色
- 可在页面入口处统一设置，需要在页面build前执行[ThemeControl](../reference/apis-arkui/js-apis-arkui-theme.md#themecontrol)。
其中，[onWillApplyTheme](../reference/apis-arkui/arkui-ts/ts-custom-component-lifecycle.md#onwillapplytheme12)回调函数用于自定义组件获取当前生效的Theme对象。

  ```ts
    import { Theme, ThemeControl } from '@ohos.arkui.theme'
    import { gAppTheme } from './AppTheme'
    
    //在页面build前执行ThemeControl
    ThemeControl.setDefaultTheme(gAppTheme)

    @Entry
    @Component
    struct DisplayPage {
      @State menuItemColor: ResourceColor = $r('sys.color.background_primary')
      
      onWillApplyTheme(theme: Theme) {
        this.menuItemColor = theme.colors.backgroundPrimary;
      }
    
      build() {
        Column() {
          List({ space: 10 }) {
            ListItem() {
              Column({ space: '5vp' }) {
                Text('Color mode')
                  .margin({ top: '5vp', left: '14fp' })
                  .width('100%')
                Row() {
                  Column() {
                    Text('Light')
                      .fontSize('16fp')
                      .textAlign(TextAlign.Start)
                      .alignSelf(ItemAlign.Center)
                    Radio({ group: 'light or dark', value: 'light' })
                      .checked(true)
                  }
                  .width('50%')

                  Column() {
                    Text('Dark')
                      .fontSize('16fp')
                      .textAlign(TextAlign.Start)
                      .alignSelf(ItemAlign.Center)
                    Radio({ group: 'light or dark', value: 'dark' })
                  }
                  .width('50%')
                }
              }
              .width('100%')
              .height('90vp')
              .borderRadius('10vp')
              .backgroundColor(this.menuItemColor)
            }

            ListItem() {
              Column() {
                Text('Brightness')
                  .width('100%')
                  .margin({ top: '5vp', left: '14fp' })
                Slider({ value: 40, max: 100 })
              }
              .width('100%')
              .height('70vp')
              .borderRadius('10vp')
              .backgroundColor(this.menuItemColor)
            }

            ListItem() {
              Column() {
                Row() {
                  Column({ space: '5vp' }) {
                    Text('Touch sensitivity')
                      .fontSize('16fp')
                      .textAlign(TextAlign.Start)
                      .width('100%')
                    Text('Increase the touch sensitivity of your screen' +
                      ' for use with screen protectors')
                      .fontSize('12fp')
                      .fontColor(Color.Blue)
                      .textAlign(TextAlign.Start)
                      .width('100%')
                  }
                  .alignSelf(ItemAlign.Center)
                  .margin({ left: '14fp' })
                  .width('75%')
    
                  Toggle({ type: ToggleType.Switch, isOn: true })
                    .margin({ right: '14fp' })
                    .alignSelf(ItemAlign.Center)
                    .width('25%')
                }
                .width('100%')
                .height('80vp')
              }
              .width('100%')
              .borderRadius('10vp')
              .backgroundColor(this.menuItemColor)
            }
          }
        }
        .padding('10vp')
        .backgroundColor('#dcdcdc')
        .width('100%')
        .height('100%')
      }
    }
  ```

- 在Ability中设置[ThemeControl](../reference/apis-arkui/js-apis-arkui-theme.md#themecontrol)，需要在onWindowStageCreate()方法中[setDefaultTheme](../reference/apis-arkui/js-apis-arkui-theme.md#setdefaulttheme)。

  ```ts
    import AbilityConstant from '@ohos.app.ability.AbilityConstant';
    import hilog from '@ohos.hilog';
    import UIAbility from '@ohos.app.ability.UIAbility';
    import Want from '@ohos.app.ability.Want';
    import window from '@ohos.window';
    import { CustomColors, ThemeControl } from '@ohos.arkui.theme';

    class AppColors implements CustomColors {
      fontPrimary = 0xFFD53032
      iconOnPrimary = 0xFFD53032
      iconFourth = 0xFFD53032
    }
    
    const abilityThemeColors = new AppColors();
    
    export default class EntryAbility extends UIAbility {
      onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
        hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onCreate');
      }
    
      onDestroy() {
        hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onDestroy');
      }
    
      onWindowStageCreate(windowStage: window.WindowStage) {
        // Main window is created, set main page for this ability
        hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onWindowStageCreate');
      
        windowStage.loadContent('pages/Index', (err, data) => {
          if (err.code) {
            hilog.error(0x0000, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err) ?? '');
            return;
          }
          hilog.info(0x0000, 'testTag', 'Succeeded in loading the content. Data: %{public}s', JSON.stringify(data) ?? '');
          // 在onWindowStageCreate()方法中setDefaultTheme
          ThemeControl.setDefaultTheme({ colors: abilityThemeColors })
          hilog.info(0x0000, 'testTag', '%{public}s', 'ThemeControl.setDefaultTheme done');
        });
      }
    
    }
  ```
  
注：如果setDefaultTheme的参数为undefined时，默认token值对应的色值如下：

| 场景类别          | 语义Token                       | Light模式色值 | Dark模式色值  |
|---------------|-------------------------------|-----------|-----------|
| 文本            | fontEmphasize                 | #000000   | #FFFFFF   |
| 文本反色          | fontOn                        | #FFFFFF   | #FFFFFF   |
| 图标            | icon                          | #000000   | #FFFFFF   |
| 图标反色          | iconOn                        | #FFFFFF   | #FFFFFF   |
| 一级文本          | fontPrimary                   | #E5000000 | #E5FFFFFF |
| 二级文本          | fontSecondary                 | #99000000 | #99FFFFFF | 
| 三级文本          | fontTertiary                  | #66000000 | #66FFFFFF |
| 四级文本          | fontFourth                    | #33000000 | #33FFFFFF | 
| 高亮文本          | fontEmphasize                 | #0A59F7   | #5291FF   |
| 一级文本反色        | fontOnPrimary                 | #FFFFFF   | #FFFFFF   |
| 二级文本反色        | fontOnSecondary               | #99FFFFFF | #99FFFFFF | 
| 三级文本反色        | fontOnTertiary                | #66FFFFFF | #66FFFFFF |
| 四级文本反色        | fontOnFourth                  | #33FFFFFF | #33FFFFFF |
| 一级图标          | iconPrimary                   | #E5000000 | #E5FFFFFF |
| 二级图标          | iconSecondary                 | #99000000 | #99FFFFFF | 
| 三级图标          | iconTertiary                  | #66000000 | #66FFFFFF |
| 四级图标          | iconFourth                    | #33000000 | #33FFFFFF | 
| 高亮图标          | iconEmphasize                 | #0A59F7   | #5291FF   |
| 高亮辅助图标        | iconSubEmphasize              | #660A59F7 | #665291FF |
| 一级图标反色        | iconOnPrimary                 | #FFFFFF   | #FFFFFF   |
| 二级图标反色        | iconOnSecondary               | #99FFFFFF | #99FFFFFF | 
| 三级图标反色        | iconOnTertiary                | #66FFFFFF | #66FFFFFF |
| 四级图标反色        | iconOnFourth                  | #33FFFFFF | #33FFFFFF |
| 一级背景（实色/不透明色） | backgroundPrimary             | #19000000 | #19000000 |
| 二级背景（实色/不透明色） | backgroundSecondary           | #F1F3F5   | #000000   |
| 三级背景（实色/不透明色） | backgroundTertiary            | #E5E5EA   | #202224   |
| 四级背景（实色/不透明色） | backgroundFourth              | #D1D1D6   | #2E3033   |
| 高亮背景（实色/不透明色） | backgroundEmphasize           | #0A59F7   | #19000000 |
| 前背景           | compForegroundPrimary         | #000000   | #E5E5E5   |
| 白色背景          | compBackgroundPrimary         | #FFFFFF   | #202224   |
| 白色透明背景        | compBackgroundPrimaryTrans    | #FFFFFF   | #33FFFFFF |
| 常亮背景          | compBackgroundPrimaryContrary | #FFFFFF   | #E5E5E5   |
| 灰色背景          | compBackgroundPrimaryGray     | #F1F3F5   | #000000   |
| 二级背景          | compBackgroundSecondary            | #19000000 | #19FFFFFF |
| 三级背景          | compBackgroundTertiary       | #0C000000 | #0CFFFFFF |
| 高亮背景          | compBackgroundEmphasize | #0A59F7   | #317AF7   |
| 黑色中性高亮背景      | compBackgroundNeutral | #000000   | #FFFFFF   |
| 20%高亮背景       | compEmphasizeSecondary | #330A59F7 | #33317AF7 |
| 10%高亮背景       | compEmphasizeTertiary | #190A59F7 | #19317AF7 |
| 分割线颜色         | compDivider | #33000000 | #33FFFFFF |
| 通用反色          | compCommonContrary | #FFFFFF   | #000000   |
| 获焦态背景色        | compBackgroundFocus | #F1F3F5   | #F1F3F5   |
| 获焦态一级反色       | compFocusedPrimary | #E5000000 | #E5FFFFFF |
| 获焦态二级反色       | compFocusedSecondary | #99000000 | #99FFFFFF |
| 获焦态三级反色       | compFocusedTertiary | #66000000 | #66FFFFFF |
| 通用悬停交互式颜色 | interactiveHover | #0C000000 | #0CFFFFFF |
| 通用按压交互式颜色 | interactivePressed | #19000000 | #19FFFFFF |
| 通用获焦交互式颜色 | interactiveFocus | #0A59F7   | #317AF7   |
| 通用激活交互式颜色 | interactiveActive | #0A59F7   | #317AF7   |
| 通用选择交互式颜色 | interactiveSelect | #33000000 | #33FFFFFF |
| 通用点击交互式颜色 | interactiveClick | #19000000 | #19FFFFFF |

![systemTheme](figures/systemTheme.png)

## 设置应用局部页面自定义主题风格
将自定义Theme的配色通过设置[WithTheme](../reference/apis-arkui/arkui-ts/ts-container-with-theme.md#withetheme)作用于内组件缺省样式，WithTheme作用域内组件配色跟随Theme的配色生效。
在下面示例中，通过WithTheme({ theme: this.myTheme })将作用域内的组件配色设置为自定义主题风格。后续可通过更改this.myTheme更换主题风格。
[onWillApplyTheme](../reference/apis-arkui/arkui-ts/ts-custom-component-lifecycle.md#onwillapplytheme12)回调函数用于自定义组件获取当前生效的Theme对象。

  ```ts
    import { CustomColors, CustomTheme, Theme } from '@ohos.arkui.theme'

    class AppColors implements CustomColors {
      fontPrimary: ResourceColor = $r('app.color.brand_purple')
      backgroundEmphasize: ResourceColor = $r('app.color.brand_purple')
    }
    
    class AppColorsSec implements CustomColors {
      fontPrimary: ResourceColor = $r('app.color.brand')
      backgroundEmphasize: ResourceColor = $r('app.color.brand')
    }
    
    class AppTheme implements CustomTheme {
      public colors: AppColors = new AppColors()
    }
    
    class AppThemeSec implements CustomTheme {
      public colors: AppColors = new AppColorsSec()
    }
    
    @Entry
    @Component
    struct DisplayPage {
      @State customTheme: CustomTheme = new AppTheme()
      @State message: string = '设置应用局部页面自定义主题风格'
      count = 0;
    
      build() {
        WithTheme({ theme: this.customTheme }) {
          Row(){
            Column() {
              Text('WithTheme')
                .fontSize(30)
                .margin({bottom: 10})
              Text(this.message)
                .margin({bottom: 10})
              Button('change theme').onClick(() => {
                this.count++;
                if (this.count > 1) {
                  this.count = 0;
                }
                switch (this.count) {
                  case 0:
                    this.customTheme = new AppTheme();
                    break;
                  case 1:
                    this.customTheme = new AppThemeSec();
                    break;
                }
              })
            }
            .width('100%')
          }
          .height('100%')
          .width('100%')
        }
      }
    }
  ```

![customTheme](figures/customTheme.gif)

## 设置应用页面局部深浅色
通过[WithTheme](../reference/apis-arkui/arkui-ts/ts-container-with-theme.md#withetheme)可以设置深浅色模式，[ThemeColorMode](../reference/apis-arkui/arkui-ts/ts-appendix-enums.md#themecolormode10)有三种模式，ThemeColorMode.SYSTEM模式表示跟随系统模式，ThemeColorMode.LIGHT模式表示浅色模式，ThemeColorMode.DARK模式表示深色模式。</br>
在WithTheme作用域内，组件的样式资源取值跟随指定的模式读取对应的深浅色模式系统和应用资源值，WithTheme作用域内的组件配色跟随指定的深浅模式生效。</br>
在下面的示例中，通过WithTheme({ colorMode: ThemeColorMode.DARK })将作用域内的组件设置为深色模式。

  ```ts
    @Entry
    @Component
    struct DisplayPage {
      @State message: string = 'Hello World';
      @State colorMode: ThemeColorMode = ThemeColorMode.DARK;

      build() {
        WithTheme({ colorMode: this.colorMode }) {
          Row() {
            Column() {
              Text(this.message)
                .fontSize(50)
                .fontWeight(FontWeight.Bold)
              Button('Switch ColorMode').onClick(() => {
                if (this.colorMode === ThemeColorMode.LIGHT) {
                  this.colorMode = ThemeColorMode.DARK;
                } else if (this.colorMode === ThemeColorMode.DARK) {
                  this.colorMode = ThemeColorMode.LIGHT;
                }
              })
            }
            .width('100%')
          }
          .backgroundColor($r('sys.color.background_primary'))
          .height('100%')
          .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.END, SafeAreaEdge.BOTTOM, SafeAreaEdge.START])
        }
      }
    }
  ```

![lightDarkMode](figures/lightDarkMode.png)
