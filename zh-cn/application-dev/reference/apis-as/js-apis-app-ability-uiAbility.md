# @ohos.app.ability.UIAbility (UIAbility)

UIAbility是包含UI界面的应用组件，继承自[Ability](js-apis-app-ability-ability.md)，提供组件创建、销毁、前后台切换等生命周期回调。

> **说明：**
>
> 本模块首批接口从API version 9 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 本模块接口仅可在Stage模型下使用。

## 导入模块

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
```

## 属性

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| context | [UIAbilityContext](js-apis-inner-application-uiAbilityContext.md) | 是 | 否 | 上下文。 |
| launchWant | [Want](js-apis-app-ability-want.md) | 是 | 否 | UIAbility启动时的参数。 |
| lastRequestWant | [Want](js-apis-app-ability-want.md) | 是 | 否 | UIAbility最后请求时的参数。|

## UIAbility.onCreate

onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void

UIAbility实例处于完全关闭状态下被创建完成后进入该生命周期回调，执行初始化业务逻辑操作。即UIAbility实例[冷启动](../../application-models/uiability-intra-device-interaction.md#目标uiability冷启动)时进入该生命周期回调。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-app-ability-want.md) | 是 | 当前UIAbility的Want类型信息，包括ability名称、bundle名称等。 |
| param | [AbilityConstant.LaunchParam](js-apis-app-ability-abilityConstant.md#abilityconstantlaunchparam) | 是 | 创建&nbsp;ability、上次异常退出的原因信息。 |

**示例：**

  ```ts
  import UIAbility from '@ohos.app.ability.UIAbility';
  import AbilityConstant from '@ohos.app.ability.AbilityConstant';
  import Want from '@ohos.app.ability.Want';

  class MyUIAbility extends UIAbility {
      onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
          console.log('onCreate, want: ${want.abilityName}');
      }
  }
  ```


## UIAbility.onWindowStageCreate

onWindowStageCreate(windowStage: window.WindowStage): void

当WindowStage创建后调用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| windowStage | [window.WindowStage](js-apis-window.md#windowstage9) | 是 | WindowStage相关信息。 |

**示例：**

  ```ts
  import UIAbility from '@ohos.app.ability.UIAbility';
  import window from '@ohos.window';

  class MyUIAbility extends UIAbility {
      onWindowStageCreate(windowStage: window.WindowStage) {
          console.log('onWindowStageCreate');
      }
  }
  ```


## UIAbility.onWindowStageDestroy

onWindowStageDestroy(): void

当WindowStage销毁后调用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**示例：**

  ```ts
  import UIAbility from '@ohos.app.ability.UIAbility';

  class MyUIAbility extends UIAbility {
      onWindowStageDestroy() {
          console.log('onWindowStageDestroy');
      }
  }
  ```


## UIAbility.onWindowStageRestore

onWindowStageRestore(windowStage: window.WindowStage): void

当迁移多实例ability时，恢复WindowStage后调用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| windowStage | [window.WindowStage](js-apis-window.md#windowstage9) | 是 | WindowStage相关信息。 |

**示例：**

  ```ts
  import UIAbility from '@ohos.app.ability.UIAbility';
  import window from '@ohos.window';

  class MyUIAbility extends UIAbility {
      onWindowStageRestore(windowStage: window.WindowStage) {
          console.log('onWindowStageRestore');
      }
  }
  ```


## UIAbility.onDestroy

onDestroy(): void | Promise&lt;void&gt;

UIAbility生命周期回调，在销毁时回调，执行资源清理等操作。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**示例：**


  ```ts
  import UIAbility from '@ohos.app.ability.UIAbility';

  class MyUIAbility extends UIAbility {
      onDestroy() {
          console.log('onDestroy');
      }
  }
  ```

在执行完onDestroy生命周期回调后，应用可能会退出，从而可能导致onDestroy中的异步函数未能正确执行，比如异步写入数据库。可以使用异步生命周期，以确保异步onDestroy完成后再继续后续的生命周期。

  ```ts
import UIAbility from '@ohos.app.ability.UIAbility';

class MyUIAbility extends UIAbility {
    async onDestroy() {
        console.log('onDestroy');
        // 调用异步函数...
    }
}
  ```

## UIAbility.onForeground

onForeground(): void

UIAbility生命周期回调，当应用从后台转到前台时触发。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**示例：**

  ```ts
  import UIAbility from '@ohos.app.ability.UIAbility';

  class MyUIAbility extends UIAbility {
      onForeground() {
          console.log('onForeground');
      }
  }
  ```


## UIAbility.onBackground

onBackground(): void

UIAbility生命周期回调，当应用从前台转到后台时触发。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**示例：**

  ```ts
  import UIAbility from '@ohos.app.ability.UIAbility';

  class MyUIAbility extends UIAbility {
      onBackground() {
          console.log('onBackground');
      }
  }
  ```


## UIAbility.onContinue

onContinue(wantParam: Record&lt;string, Object&gt;): AbilityConstant.OnContinueResult

当Ability准备迁移时触发，保存数据。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| wantParam | Record&lt;string,&nbsp;Object&gt; | 是 | want相关参数。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [AbilityConstant.OnContinueResult](js-apis-app-ability-abilityConstant.md#abilityconstantoncontinueresult) | 继续的结果。 |

**示例：**

  ```ts
  import UIAbility from '@ohos.app.ability.UIAbility';
  import AbilityConstant from '@ohos.app.ability.AbilityConstant';

  class MyUIAbility extends UIAbility {
      onContinue(wantParams: Record<string, Object>) {
          console.log('onContinue');
          wantParams['myData'] = 'my1234567';
          return AbilityConstant.OnContinueResult.AGREE;
      }
  }
  ```


## UIAbility.onNewWant

onNewWant(want: Want, launchParam: AbilityConstant.LaunchParam): void

UIAbility实例已经启动并在前台运行过，由于某些原因切换到后台，再次启动该UIAbility实例时会回调执行该方法。即UIAbility实例[热启动](../../application-models/uiability-intra-device-interaction.md#目标uiability热启动)时进入该生命周期回调。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-app-ability-want.md) | 是 | Want类型参数，如ability名称，包名等。 |
| launchParam | [AbilityConstant.LaunchParam](js-apis-app-ability-abilityConstant.md#abilityconstantlaunchparam) | 是 | UIAbility启动的原因、上次异常退出的原因信息。 |

**示例：**

  ```ts
  import UIAbility from '@ohos.app.ability.UIAbility';
  import AbilityConstant from '@ohos.app.ability.AbilityConstant';
  import Want from '@ohos.app.ability.Want';

  class MyUIAbility extends UIAbility {
      onNewWant(want: Want, launchParam: AbilityConstant.LaunchParam) {
          console.log(`onNewWant, want: ${want.abilityName}`);
          console.log(`onNewWant, launchParam: ${JSON.stringify(launchParam)}`);
      }
  }
  ```

## UIAbility.onDump

onDump(params: Array\<string>): Array\<string>

转储客户端信息时调用，可用于转储非敏感信息。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| params | Array\<string> | 是 | 表示命令形式的参数。|

**示例：**

  ```ts
  import UIAbility from '@ohos.app.ability.UIAbility';

  class MyUIAbility extends UIAbility {
      onDump(params: Array<string>) {
          console.log(`dump, params: ${JSON.stringify(params)}`);
          return ['params'];
      }
  }
  ```


## UIAbility.onSaveState

onSaveState(reason: AbilityConstant.StateType, wantParam: Record&lt;string, Object&gt;): AbilityConstant.OnSaveResult

该API配合[appRecovery](js-apis-app-ability-appRecovery.md)使用。在应用故障时，如果使能了自动保存状态，框架将回调onSaveState保存UIAbility状态。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| reason | [AbilityConstant.StateType](js-apis-app-ability-abilityConstant.md#abilityconstantstatetype) | 是 | 回调保存状态的原因。 |
| wantParam | Record&lt;string,&nbsp;Object&gt; | 是 | want相关参数。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [AbilityConstant.OnSaveResult](js-apis-app-ability-abilityConstant.md#abilityconstantonsaveresult) | 是否同意保存当前UIAbility的状态。 |

**示例：**

  ```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';

class MyUIAbility extends UIAbility {
    onSaveState(reason: AbilityConstant.StateType, wantParam: Record<string, Object>) {
        console.log('onSaveState');
        wantParam['myData'] = 'my1234567';
        return AbilityConstant.OnSaveResult.RECOVERY_AGREE;
    }
}
  ```

## UIAbility.onShare<sup>10+</sup>

onShare(wantParam: Record&lt;string, Object&gt;): void

在跨端分享场景下，在UIAbility中设置分享方设备要分享的数据。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| wantParam | Record&lt;string,&nbsp;Object&gt; | 是 | 待分享的数据。 |

**示例：**

  ```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';

class MyUIAbility extends UIAbility {
    onShare(wantParams: Record<string, Object>) {
        console.log('onShare');
        wantParams['ohos.extra.param.key.shareUrl'] = 'example.com';
    }
}
  ```

## UIAbility.onPrepareToTerminate<sup>10+</sup>

onPrepareToTerminate(): boolean

UIAbility生命周期回调，当系统预关闭开关打开后（配置系统参数persist.sys.prepare_terminate为true打开），在UIAbility关闭时触发，可在回调中定义操作来决定是否继续执行关闭UIAbility的操作。如果UIAbility在退出时需要与用户交互确认是否关闭UIAbility，可在此生命周期回调中定义预关闭操作配合[terminateSelf](js-apis-inner-application-uiAbilityContext.md#uiabilitycontextterminateself)接口退出，如弹窗确认是否关闭，并配置预关闭生命周期返回true取消正常关闭。

**需要权限**：ohos.permission.PREPARE_APP_TERMINATE

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**返回值：**

| 类型 | 说明 |
| -- | -- |
| boolean | 是否执行UIAbility关闭操作，返回true表示本次UIAbility关闭流程取消，不再退出，返回false表示UIAbility继续正常关闭。 |

**示例：**

  ```ts
  import UIAbility from '@ohos.app.ability.UIAbility';
  import Want from '@ohos.app.ability.Want';
  import { BusinessError } from '@ohos.base';

  export default class EntryAbility extends UIAbility {
    onPrepareToTerminate() {
      // 开发者定义预关闭动作
      // 例如拉起另一个ability，根据ability处理结果执行异步关闭
      let want: Want = {
        bundleName: "com.example.myapplication",
        moduleName: "entry",
        abilityName: "SecondAbility"
      }
      this.context.startAbilityForResult(want)
        .then((result)=>{
          // 获取ability处理结果，当返回结果的resultCode为0关闭当前UIAbility
          console.log('startAbilityForResult success, resultCode is ' + result.resultCode);
          if (result.resultCode === 0) {
            this.context.terminateSelf();
          }
        }).catch((err: BusinessError)=>{
          // 异常处理
          console.log('startAbilityForResult failed, err:' + JSON.stringify(err));
          this.context.terminateSelf();
        })

      return true; // 已定义预关闭操作后，返回true表示UIAbility取消关闭
    }
  }
  ```

## UIAbility.onBackPressed<sup>10+</sup>

onBackPressed(): boolean

UIAbility生命周期回调，当UIAbility侧滑返回时触发。根据返回值决定是否销毁UIAbility，默认为销毁UIAbility。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**返回值：**

| 类型 | 说明 |
| -- | -- |
| boolean | 返回true表示UIAbility将会被移到后台不销毁，返回false表示UIAbility将正常销毁。 |

**示例：**

  ```ts
  import UIAbility from '@ohos.app.ability.UIAbility';

  export default class EntryAbility extends UIAbility {
    onBackPressed() {
      return true;
    }
  }
  ```