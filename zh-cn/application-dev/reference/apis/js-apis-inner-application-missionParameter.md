# MissionParameter

作为[startSyncRemoteMissions](js-apis-distributedMissionManager.md#distributedmissionmanagerstartsyncremotemissions)的入参，表示同步时所需参数的枚举。

> **说明：**
>
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 属性

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

| 名称          | 类型    | 可读   | 可写   | 说明          |
| ----------- | ------- | ---- | ---- | ----------- |
| deviceId    | string  | 是    | 是    | 表示设备ID。     |
| fixConflict | boolean | 是    | 是    | 表示是否存在版本冲突。 |
| tag         | number  | 是    | 是    | 表示特定的标签。    |