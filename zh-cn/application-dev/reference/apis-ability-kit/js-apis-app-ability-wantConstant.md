# @ohos.app.ability.wantConstant (wantConstant)

wantConstant模块提供want中操作want常数和解释Flags说明的能力。

> **说明：**
>
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import wantConstant from '@ohos.app.ability.wantConstant';
```

## wantConstant.Params

want的Params操作的常量。

**系统能力**：SystemCapability.Ability.AbilityBase

| 名称                    | 值                                 | 说明                                                                           |
| ----------------------- | ---------------------------------- | ------------------------------------------------------------------------------ |
| ABILITY_BACK_TO_OTHER_MISSION_STACK   | ability.params.backToOtherMissionStack     | 表示是否支持跨任务链返回。  |
| ABILITY_RECOVERY_RESTART<sup>10+</sup> | ohos.ability.params.abilityRecoveryRestart | 指示当前Ability是否发生了故障恢复重启。 |
| CONTENT_TITLE_KEY<sup>10+</sup>       | ohos.extra.param.key.contentTitle  | 指示元服务支持分享标题的参数的操作。  |
| SHARE_ABSTRACT_KEY<sup>10+</sup>      | ohos.extra.param.key.shareAbstract | 指示元服务支持分享内容的参数的操作。  |
| SHARE_URL_KEY<sup>10+</sup>           | ohos.extra.param.key.shareUrl      | 指示元服务支持分享链接的参数的操作。  |
| SUPPORT_CONTINUE_PAGE_STACK_KEY<sup>10+</sup>    | ohos.extra.param.key.supportContinuePageStack  | 指示在跨端迁移过程中是否迁移页面栈信息，默认值为true，自动迁移页面栈信息。|
| SUPPORT_CONTINUE_SOURCE_EXIT_KEY<sup>10+</sup>  | ohos.extra.param.key.supportContinueSourceExit      | 指示跨端迁移源端应用是否退出，默认值为true，源端应用自动退出。|
| SHOW_MODE_KEY<sup>12+</sup>  | ohos.extra.param.key.showMode      | 指示展示模式，值为枚举类型wantConstant.ShowMode|
| ASSERT_FAULT_SESSION_ID<sup>12+</sup>  | ohos.ability.params.asssertFaultSessionId      | 指示AssertFault的会话ID。|

## wantConstant.Flags

Flags说明。用于表示处理Want的方式。

**系统能力**：SystemCapability.Ability.AbilityBase

| 名称                                 | 值       | 说明                                                         |
| ------------------------------------ | ---------- | ------------------------------------------------------------ |
| FLAG_AUTH_READ_URI_PERMISSION        | 0x00000001 | 指示对URI执行读取操作的授权。                                  |
| FLAG_AUTH_WRITE_URI_PERMISSION       | 0x00000002 | 指示对URI执行写入操作的授权。                                  |
| FLAG_INSTALL_ON_DEMAND               | 0x00000800 | 如果未安装指定的功能，请安装该功能。                              |
| FLAG_START_WITHOUT_TIPS<sup>11+</sup>              | 0x40000000 | 如果隐式启动能力不能匹配任何应用程序，则不会弹出提示对话框。       |

## wantConstant.ShowMode<sup>12+</sup>

ShowMode说明。用于表示拉起元服务的展示模式。

**系统能力**：SystemCapability.Ability.AbilityBase

| 名称                                | 值 | 说明           |
| ----------------------------------- |---|--------------|
| WINDOW        | 0 | 指示独立窗口拉起模式。  |
| EMBEDDED_FULL       | 1 | 指示嵌入式全屏拉起模式。 |
