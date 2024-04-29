# uri

uri对象，可以通过[bundleManager.queryAbilityInfo](js-apis-bundleManager-sys.md#bundleManager.queryAbilityInfo)获取，其中入参abilityFlags至少包含GET_ABILITY_INFO_WITH_SKILL。此对象在[Skill](js-apis-bundleManager-skill.md)中包含。

> **说明：**
> 本模块首批接口从API version 12 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## uri

**系统能力**: SystemCapability.BundleManager.BundleFramework.Core
| 名称            | 类型   | 可读 | 可写 | 说明                                                        |
| --------------- | ------ | ---- | ---- | ----------------------------------------------------------- |
| scheme          | String | 是   | 否   | 标识 URI 协议名，常见的有http、https、file、ftp等。                                           |
| host            | String | 是   | 否   | 标识 URI 主机地址部分，仅当 scheme 存在时有意义。            |
| port            | String | 是   | 否   | 标识 URI 端口部分，仅当 scheme 和 host 同时存在时有意义。   |
| path            | String | 是   | 否   | 标识 URI 路径部分，仅当 scheme 和 host 同时存在时有意义。   |
| pathStartWith   | String | 是   | 否   | 标识 URI 路径部分，用于前缀匹配，仅当 scheme 和 host 同时存在时有意义。 |
| pathRegex       | String | 是   | 否   | 标识 URI 路径部分，用于正则匹配，仅当 scheme 和 host 同时存在时有意义。 |
| utd             | String | 是   | 否   | 标识与 Want 相匹配的 URI 的标准化数据类型，适用于分享等场景。 |
| maxFileSupported | Number   | 是   | 否   | 对于指定类型的文件，标识一次能接收或打开的最大数量。 |
| linkFeature     | String | 是   | 否   | 标识 URI 提供的功能类型，用于实现应用间跳转, 仅在AbilityInfo中存在。 |