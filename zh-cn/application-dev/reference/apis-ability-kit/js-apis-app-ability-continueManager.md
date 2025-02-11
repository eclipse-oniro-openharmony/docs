# @ohos.app.ability.continueManager (continueManager)

continueManager应用跨端迁移状态通知入口，提供应用快速拉起状态通知回调的注册与注销功能。

> **说明：**
> 
> 本模块首批接口从API version 16开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import { continueManager } from '@kit.AbilityKit';
```

## continueManager.on

on(type: 'prepareContinue', context: Context, callback: AsyncCallback&lt;ContinueResultInfo&gt;): void

注册回调函数以获取快速拉起结果，使用AsyncCallback异步回调。

**系统能力**：SystemCapability.Ability.DistributedManagementService

**参数**：

  | 参数名 | 类型                                                                                              | 必填 | 说明                                       |
  | -------- |-------------------------------------------------------------------------------------------------| -------- |------------------------------------------|
  | type | string                                                                                          | 是 | 固定值：prepareContinue。                     |
  | context | [Context](../apis-ability-kit/js-apis-inner-application-baseContext.md)                                                                                         | 是 | ability的context。                         |
  | callback | AsyncCallback&lt;[ContinueResultInfo](js-apis-app-ability-continueManager.md#continueresultinfo)&gt; | 是 | AsyncCallback形式返回，应用跨端迁移时，sink端应用快速拉起结果。 |

**示例**：

  ```ts
import { AbilityConstant, UIAbility, Want, continueManager } from '@kit.AbilityKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

const TAG: string = '[MigrationAbility]';
const DOMAIN_NUMBER: number = 0xFF00;

export default class MigrationAbility extends UIAbility {
    storage : LocalStorage = new LocalStorage();

    onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
        hilog.info(DOMAIN_NUMBER, TAG, '%{public}s', 'Ability onCreate');

        // 1.已配置快速拉起功能，应用立即启动时触发应用生命周期回调
        if (launchParam.launchReason === AbilityConstant.LaunchReason.PREPARE_CONTINUATION) {
            // 注册快速拉起结果通知的回调函数
            this.registerQuickStartCallback();
            //若应用迁移数据较大，可在此处添加加载页面(页面中显示loading等)
            //可处理应用自定义跳转、时序等问题
            // ...
        }
    }
    
    async registerQuickStartCallback() : Promise<void>{
        continueManager.on("prepareContinue", this.context, (err, continueResultInfo)=>{
            if (err.code != 0) {
                console.error('register failed, cause: ' + JSON.stringify(err));
                return;
            }
            console.info('register finished, ' + JSON.stringify(continueResultInfo));
        });
    }
}
  ```

## continueManager.off

off(type: 'prepareContinue', context: Context, callback: AsyncCallback&lt;ContinueResultInfo&gt;): void

取消注册快速拉起状态的通知回调，使用AsyncCallback方式作为异步方法。

**系统能力**：SystemCapability.Ability.DistributedManagementService

**参数**：

| 参数名 | 类型                                 | 必填 | 说明                                   |
  | -------- |------------------------------------| -------- |--------------------------------------|
| type | string                             | 是 | 固定值：prepareContinue。                 |
| context | [Context](../apis-ability-kit/js-apis-inner-application-baseContext.md)                            | 是 | ability的context。                     |
| callback | AsyncCallback&lt;[ContinueResultInfo](js-apis-app-ability-continueManager.md#continueresultinfo)&gt; | 是 | AsyncCallback形式返回，取消快速拉起通知回调函数注册的结果。 |

**示例**：

  ```ts
import { AbilityConstant, UIAbility, Want, continueManager } from '@kit.AbilityKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

const TAG: string = '[MigrationAbility]';
const DOMAIN_NUMBER: number = 0xFF00;

export default class MigrationAbility extends UIAbility {
    storage : LocalStorage = new LocalStorage();

    onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
        hilog.info(DOMAIN_NUMBER, TAG, '%{public}s', 'Ability onCreate');

        // 1.已配置快速拉起功能，应用立即启动时触发应用生命周期回调
        if (launchParam.launchReason === AbilityConstant.LaunchReason.PREPARE_CONTINUATION) {
            // 注册快速拉起结果通知的回调函数
            this.registerQuickStartCallback();
            //若应用迁移数据较大，可在此处添加加载页面(页面中显示loading等)
            //可处理应用自定义跳转、时序等问题
            // ...
        }
    }
    
    async registerQuickStartCallback() : Promise<void>{
        continueManager.off("prepareContinue", this.context, (err, continueResultInfo)=>{
            if (err.code != 0) {
                console.error('register failed, cause: ' + JSON.stringify(err));
                return;
            }
            console.info('register finished, ' + JSON.stringify(continueResultInfo));
        });
    }
}
  ```

## ContinueResultInfo

注册或注销获取快速拉起结果的回调函数，收到的快速拉起结果。

**系统能力**：SystemCapability.Ability.DistributedManagementService

| 名称 | 类型                                                                            | 只读 | 可选 | 说明       |
| -------- |-------------------------------------------------------------------------------|----|----|----------|
| resultState | [ContinueStateCode](js-apis-app-ability-continueManager.md#continuestatecode) | 是  | 否  | 操作结果状态码。 |
| resultInfo | string                                                                        | 否  | 是  | 操作结果的说明。 |

## ContinueStateCode

操作结果状态码枚举值。

**系统能力**：SystemCapability.Ability.DistributedManagementService

| 名称 | 值  | 说明    | 
| -------- |----|-------|
| SUCCESS  | 0  | 操作成功。 | 
| SYSTEM_ERROR | 其它 | 操作失败。 | 

