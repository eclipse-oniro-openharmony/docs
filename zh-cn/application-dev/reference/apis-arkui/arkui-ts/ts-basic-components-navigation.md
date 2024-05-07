# Navigation

Navigation组件是路由导航的根视图容器，一般作为Page页面的根容器使用，其内部默认包含了标题栏、内容区和工具栏，其中内容区默认首页显示导航内容（Navigation的子组件）或非首页显示（[NavDestination](ts-basic-components-navdestination.md)的子组件），首页和非首页通过路由进行切换。

> **说明：**
>
> 该组件从API Version 8开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。
>
> 该组件从API Version 11开始默认支持安全区避让特性(默认值为：expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM]))，开发者可以重写该属性覆盖默认行为，API Version 11之前的版本需配合[expandSafeArea](ts-universal-attributes-expand-safe-area.md)属性实现安全区避让。


## 子组件

可以包含子组件。

从API Version 9开始，推荐与[NavRouter](ts-basic-components-navrouter.md)组件搭配使用。

从API Version 10开始，推荐使用[NavPathStack](#navpathstack10)配合navDestination属性进行页面路由。

## 接口

### Navigation

Navigation()

### Navigation<sup>10+</sup>

Navigation(pathInfos: NavPathStack)

绑定路由栈到Navigation组件。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**参数：**

| 参数名       | 参数类型                            | 必填   | 参数描述   |
| --------- | ------------------------------- | ---- | ------ |
| pathInfos | [NavPathStack](#navpathstack10) | 否    | 路由栈信息。 |

## 属性

除支持[通用属性](ts-universal-attributes-size.md)外，还支持以下属性：

### title

title(value: ResourceStr | CustomBuilder | NavigationCommonTitle | NavigationCustomTitle, options?: NavigationTitleOptions)

设置页面标题。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名  | 类型                                                         | 必填 | 说明                                                         |
| ------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value   | [ResourceStr](ts-types.md#resourcestr)<sup>10+</sup>&nbsp;\|&nbsp;[CustomBuilder](ts-types.md#custombuilder8)&nbsp;\|&nbsp;[NavigationCommonTitle](#navigationcommontitle9类型说明)<sup>9+</sup>&nbsp;\|&nbsp;[NavigationCustomTitle](#navigationcustomtitle9类型说明)<sup>9+</sup> | 是   | 页面标题，使用NavigationCustomTitle类型设置height高度时，[titleMode](#titlemode)属性不会生效。字符串超长时，如果不设置副标题，先缩小再换行（2行）最后...截断。如果设置副标题，先缩小最后...截断。 |
| options | [NavigationTitleOptions](#navigationtitleoptions11类型说明)<sup>11+</sup> | 否   | 标题栏选项。                                                   |

### subTitle<sup>(deprecated)</sup>

subTitle(value: string)

设置页面副标题。

从API Version 9开始废弃，建议使用[title](#title)代替。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明         |
| ------ | ------ | ---- | ------------ |
| value  | string | 是   | 页面副标题。 |

### menus

menus(value: Array&lt;NavigationMenuItem&gt; | CustomBuilder)

设置页面右上角菜单。不设置时不显示菜单项。使用Array<[NavigationMenuItem](#navigationmenuitem类型说明)&gt; 写法时，竖屏最多支持显示3个图标，横屏最多支持显示5个图标，多余的图标会被放入自动生成的更多图标。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明             |
| ------ | ------------------------------------------------------------ | ---- | ---------------- |
| value  | Array<[NavigationMenuItem](#navigationmenuitem类型说明)&gt;&nbsp;\|&nbsp;[CustomBuilder](ts-types.md#custombuilder8) | 是   | 页面右上角菜单。 |

### titleMode

titleMode(value: NavigationTitleMode)

设置页面标题栏显示模式。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                | 必填 | 说明                                                      |
| ------ | --------------------------------------------------- | ---- | --------------------------------------------------------- |
| value  | [NavigationTitleMode](#navigationtitlemode枚举说明) | 是   | 页面标题栏显示模式。<br/>默认值：NavigationTitleMode.Free |

### toolBar<sup>(deprecated)</sup>

toolBar(value: object | CustomBuilder)

设置工具栏内容。不设置时不显示工具栏。items均分底部工具栏，在每个均分内容区布局文本和图标，文本超长时，逐级缩小，缩小之后换行，最后...截断。

从API version 10开始，该接口不再维护，推荐使用[toolbarConfiguration](#toolbarconfiguration10)代替。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明         |
| ------ | ------------------------------------------------------------ | ---- | ------------ |
| value  | [object](#object类型说明)&nbsp;\|&nbsp;[CustomBuilder](ts-types.md#custombuilder8) | 是   | 工具栏内容。 |

### toolbarConfiguration<sup>10+</sup>

toolbarConfiguration(value: Array&lt;ToolbarItem&gt; | CustomBuilder, options?: NavigationToolbarOptions)

设置工具栏内容。不设置时不显示工具栏。

**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名  | 类型                                                         | 必填 | 说明                                                         |
| ------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value   | &nbsp;Array&lt;[ToolbarItem](#toolbaritem10类型说明)&gt; &nbsp;\|&nbsp;[CustomBuilder](ts-types.md#custombuilder8) | 是   | 工具栏内容，使用Array&lt;[ToolbarItem](#toolbaritem10类型说明)&gt;写法设置的工具栏有如下特性：<br/>工具栏所有选项均分底部工具栏，在每个均分内容区布局文本和图标。<br/>文本超长时，若工具栏选项个数小于5个，优先拓展选项的宽度，最大宽度与屏幕等宽，其次逐级缩小，缩小之后换行，最后...截断。<br/>竖屏最多支持显示5个图标，多余的图标会被放入自动生成的更多图标。横屏下必须配合menus属性的Array&lt;[NavigationMenuItem](#navigationmenuitem类型说明)&gt;使用，底部工具栏会自动隐藏，同时底部工具栏所有选项移动至页面右上角菜单。<br/>使用[CustomBuilder](ts-types.md#custombuilder8)写法为用户自定义工具栏选项，除均分底部工具栏外不具备以上功能。 |
| options | [NavigationToolbarOptions](#navigationtoolbaroptions11类型说明)<sup>11+</sup> | 否   | 工具栏选项。                                                 |

### hideToolBar

hideToolBar(value: boolean)

设置是否隐藏工具栏。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| value  | boolean | 是   | 是否隐藏工具栏。<br/>默认值：false<br/>true: 隐藏工具栏。<br/>false: 显示工具栏。 |

### hideTitleBar

hideTitleBar(value: boolean)

设置是否隐藏标题栏。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| value  | boolean | 是   | 是否隐藏标题栏。<br/>默认值：false<br/>true: 隐藏标题栏。<br/>false: 显示标题栏。 |

### hideBackButton

hideBackButton(value: boolean)

设置是否隐藏标题栏中的返回键。返回键仅针对[titleMode](#titlemode)为NavigationTitleMode.Mini时才生效。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| value  | boolean | 是   | 是否隐藏标题栏中的返回键。 <br/>默认值：false<br/>true: 隐藏返回键。<br/>false: 显示返回键。 |

### navBarWidth<sup>9+</sup>

navBarWidth(value: Length)

设置导航栏宽度。仅在Navigation组件分栏时生效。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                         | 必填 | 说明                                      |
| ------ | ---------------------------- | ---- | ----------------------------------------- |
| value  | [Length](ts-types.md#length) | 是   | 导航栏宽度。<br/>默认值：240<br/>单位：vp<br/>undefined：行为不做处理，行为不做处理，导航栏宽度与默认值保持一致。 |

### navBarPosition<sup>9+</sup>

navBarPosition(value: NavBarPosition)

设置导航栏位置。仅在Navigation组件分栏时生效。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                       | 必填 | 说明                                          |
| ------ | ------------------------------------------ | ---- | --------------------------------------------- |
| value  | [NavBarPosition](#navbarposition9枚举说明) | 是   | 导航栏位置。<br/>默认值：NavBarPosition.Start |

### mode<sup>9+</sup>

mode(value: NavigationMode)

设置导航栏的显示模式。支持Stack、Split与Auto模式。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                       | 必填 | 说明                                                         |
| ------ | ------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | [NavigationMode](#navigationmode9枚举说明) | 是   | 导航栏的显示模式。<br/>默认值：NavigationMode.Auto<br/>自适应：基于组件宽度自适应单栏和双栏。 |

### backButtonIcon<sup>9+</sup>

backButtonIcon(value: string | PixelMap | Resource)

设置标题栏中返回键图标。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明                 |
| ------ | ------------------------------------------------------------ | ---- | -------------------- |
| value  | string&nbsp;\|&nbsp;[PixelMap](../../apis-image-kit/js-apis-image.md#pixelmap7)&nbsp;\|&nbsp;[Resource](ts-types.md#resource) | 是   | 标题栏中返回键图标。 |

### hideNavBar<sup>9+</sup>

hideNavBar(value: boolean)

设置是否隐藏导航栏。设置为true时，隐藏Navigation的导航栏，包括标题栏、内容区和工具栏。如果此时路由栈中存在NavDestination页面，则直接显示栈顶NavDestination页面，反之显示空白。

从API Version 9开始到API Version 10仅在双栏模式下生效。从API Version 11开始在单栏、双栏与自适应模式均生效。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                               |
| ------ | ------- | ---- | ---------------------------------- |
| value  | boolean | 是   | 是否隐藏导航栏。<br/>默认值：false |

### navDestination<sup>10+</sup>

navDestination(builder: (name: string, param: unknown) => void)

创建NavDestination组件。使用builder函数，基于name和param构造NavDestination组件。builder下只能有一个根节点。builder中允许在NavDestination组件外包含一层自定义组件， 但自定义组件不允许设置属性和事件，否则仅显示空白。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名  | 类型                                   | 必填 | 说明                     |
| ------- | -------------------------------------- | ---- | ------------------------ |
| builder | (name: string, param: unknown) => void | 是   | 创建NavDestination组件。 |

### navBarWidthRange<sup>10+</sup>

navBarWidthRange(value: [Dimension, Dimension])

设置导航栏最小和最大宽度（双栏模式下生效）。

**规则：** 优先级规则详见说明。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名  | 类型                                                         | 必填 | 说明                                                         |
| ------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| builder | [[Dimension](ts-types.md#dimension10), [Dimension](ts-types.md#dimension10)] | 是   | 导航栏最小和最大宽度。<br/>默认值：最小默认值 240，最大默认值为组件宽度的40% ，且不大于 432，如果只设置一个值，则未设置的值按照默认值计算。<br/>单位：vp |

### minContentWidth<sup>10+</sup>

minContentWidth(value: Dimension)

设置导航栏内容区最小宽度（双栏模式下生效）。

**规则：** 优先级规则详见说明。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名  | 类型                                 | 必填 | 说明                                                         |
| ------- | ------------------------------------ | ---- | ------------------------------------------------------------ |
| builder | [Dimension](ts-types.md#dimension10) | 是   | 导航栏内容区最小宽度。<br/>默认值：360<br/>单位：vp<br/>undefined：行为不做处理，导航栏内容区最小宽度与默认值保持一致。<br/>Auto模式断点计算：默认600vp，minNavBarWidth(240vp) + minContentWidth (360vp) |

>  **说明：**
>
>  1. 仅设置navBarWidth，不支持Navigation分割线拖拽。
>
>  2. navBarWidthRange指定分割线可以拖拽范围。如果不设置值，则按照默认值处理。拖拽范围需要满足navBarWidthRange设置的范围和minContentWidth限制。
>
>  3. Navigation显示范围缩小：a. 缩小内容区大小。如果不设置minContentWidth属性，则可以缩小内容区至0， 否则最小缩小至minContentWidth。b. 缩小导航栏大小，缩小时需要满足导航栏宽度大于navBarRange的下限。c. 对显示内容进行裁切。

## 事件

### onTitleModeChange

onTitleModeChange(callback: (titleMode: NavigationTitleMode) =&gt; void)

当[titleMode](#titlemode)为NavigationTitleMode.Free时，随着可滚动组件的滑动标题栏模式发生变化时触发此回调。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名    | 类型                                                | 必填 | 说明       |
| --------- | --------------------------------------------------- | ---- | ---------- |
| titleMode | [NavigationTitleMode](#navigationtitlemode枚举说明) | 是   | 标题模式。 |

### onNavBarStateChange<sup>9+</sup>

onNavBarStateChange(callback: (isVisible: boolean) =&gt; void) 

导航栏显示状态切换时触发该回调。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名    | 类型    | 必填 | 说明                                           |
| --------- | ------- | ---- | ---------------------------------------------- |
| isVisible | boolean | 是   | isVisible为true时表示显示，为false时表示隐藏。 |

### onNavigationModeChange<sup>11+</sup>

onNavigationModeChange(callback: (mode: NavigationMode) =&gt; void) 

当Navigation首次显示或者单双栏状态发生变化时触发该回调。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名    | 类型    | 必填 | 说明                                           |
| --------- | ------- | ---- | ---------------------------------------------- |
| mode | [NavigationMode](#navigationmode9枚举说明) | 是   | NavigationMode.Split: 当前Navigation显示为双栏;<br/>NavigationMode.Stack: 当前Navigation显示为单栏。|

### customNavContentTransition<sup>11+</sup>

customNavContentTransition(delegate(from: NavContentInfo, to: NavContentInfo, operation: NavigationOperation) => NavigationAnimatedTransition | undefined)

自定义转场动画回调。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名    | 类型                                                  | 必填 | 说明                    |
| --------- | ----------------------------------------------------- | ---- | ----------------------- |
| from      | [NavContentInfo](#navcontentinfo11)                   | 是   | 退场Destination的页面。 |
| to        | [NavContentInfo](#navcontentinfo11)                   | 是   | 进场Destination的页面。 |
| operation | [NavigationOperation](#navigationoperation11枚举说明) | 是   | 转场类型。              |

**返回值：** 

| 类型                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [NavigationAnimatedTransition](#navigationanimatedtransition11)&nbsp;\|&nbsp;undefined | 自定义转场动画协议。<br/>undefined: 返回未定义，执行默认转场动效。 |

## NavPathStack<sup>10+</sup>

Navigation路由栈。

### pushPath<sup>10+</sup>

pushPath(info: NavPathInfo, animated?: boolean): void

将info指定的NavDestination页面信息入栈。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**参数：**

| 名称   | 类型                            | 必填   | 描述                   |
| ---- | ----------------------------- | ---- | -------------------- |
| info | [NavPathInfo](#navpathinfo10) | 是    | NavDestination页面的信息。 |
| animated<sup>11+</sup> | boolean | 否    | 是否支持转场动画，默认值：true。 |

### pushPathByName<sup>10+</sup>

pushPathByName(name: string, param: unknown, animated?: boolean): void

将name指定的NavDestination页面信息入栈，传递的数据为param。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**参数：**

| 名称    | 类型      | 必填   | 描述                    |
| ----- | ------- | ---- | --------------------- |
| name  | string  | 是    | NavDestination页面名称。   |
| param | unknown | 是    | NavDestination页面详细参数。 |
| animated<sup>11+</sup> | boolean | 否    | 是否支持转场动画，默认值：true。 |

### pushPathByName<sup>11+</sup>

pushPathByName(name: string, param: Object, onPop: import('../api/@ohos.base').Callback\<PopInfo>, animated?: boolean): void

将name指定的NavDestination页面信息入栈，传递的数据为param，添加onPop回调接收入栈页面出栈时的返回结果，并进行处理。

**参数：**

| 名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| name  | string  | 是    | NavDestination页面名称。   |
| param | Object | 是    | NavDestination页面详细参数。 |
| onPop | import('../api/@ohos.base').Callback\<[PopInfo](#popinfo11)> | 是 | Callback回调，用于页面出栈时触发该回调处理返回结果。 |
| animated | boolean | 否    | 是否支持转场动画，默认值：true。 |

### pushDestination<sup>11+</sup>

pushDestination(info: NavPathInfo, animated?: boolean): Promise&lt;void&gt;

将info指定的NavDestination页面信息入栈，使用Promise异步回调返回接口调用结果。

**参数：**

| 名称   | 类型                            | 必填   | 描述                   |
| ---- | ----------------------------- | ---- | -------------------- |
| info | [NavPathInfo](#navpathinfo10) | 是    | NavDestination页面的信息。 |
| animated | boolean | 否    | 是否支持转场动画，默认值：true。 |

**返回值：**

| 类型                | 说明        |
| ------------------- | --------- |
| Promise&lt;void&gt; | 异常返回结果。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../../errorcode-universal.md)和[ohos.router(页面路由)](../errorcode-router.md)错误码。

| 错误码ID   | 错误信息 |
| --------- | ------- |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2.Incorrect parameter types; 3. Parameter verification failed.   |
| 100001    | 系统内部错误。|
| 100005    | 创建NavDestination组件的builder函数未注册。 |
| 100006    | 目标页面中不存在NavDestination组件。|

### pushDestinationByName<sup>11+</sup>

pushDestinationByName(name: string, param: Object, animated?: boolean): Promise&lt;void&gt;

将name指定的NavDestination页面信息入栈，传递的数据为param，使用Promise异步回调返回接口调用结果。

**参数：**

| 名称    | 类型      | 必填   | 描述                    |
| ----- | ------- | ---- | --------------------- |
| name  | string  | 是    | NavDestination页面名称。   |
| param | Object | 是    | NavDestination页面详细参数。 |
| animated | boolean | 否    | 是否支持转场动画，默认值：true。 |

**返回值：**

| 类型                | 说明        |
| ------------------- | --------- |
| Promise&lt;void&gt; | 异常返回结果。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../../errorcode-universal.md)和[ohos.router(页面路由)](../errorcode-router.md)错误码。
| 错误码ID   | 错误信息 |
| --------- | ------- |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2.Incorrect parameter types; 3. Parameter verification failed.   |
| 100001    | 系统内部错误。|
| 100005    | 创建NavDestination组件的builder函数未注册。 |
| 100006    | 目标页面中不存在NavDestination组件。|

### pushDestinationByName<sup>11+</sup>

pushDestinationByName(name: string, param: Object, onPop: import('../api/@ohos.base').Callback\<PopInfo>, animated?: boolean): Promise&lt;void&gt;

将name指定的NavDestination页面信息入栈，传递的数据为param，并且添加用于页面出栈时处理返回结果的OnPop回调，使用Promise异步回调返回接口调用结果。

**参数：**

| 名称    | 类型      | 必填   | 描述                    |
| ----- | ------- | ---- | --------------------- |
| name  | string  | 是    | NavDestination页面名称。   |
| param | Object | 是    | NavDestination页面详细参数。 |
| onPop | import('../api/@ohos.base').Callback\<[PopInfo](#popinfo11)> | 是    | Callback回调，用于页面出栈时处理返回结果。 |
| animated | boolean | 否    | 是否支持转场动画，默认值：true。 |

**返回值：**

| 类型                | 说明        |
| ------------------- | --------- |
| Promise&lt;void&gt; | 异常返回结果。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../../errorcode-universal.md)和[ohos.router(页面路由)](../errorcode-router.md)错误码。

| 错误码ID   | 错误信息 |
| --------- | ------- |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2.Incorrect parameter types; 3. Parameter verification failed.   |
| 100001    | 系统内部错误。|
| 100005    | 创建NavDestination组件的builder函数未注册。 |
| 100006    | 目标页面中不存在NavDestination组件。|

### replacePath<sup>11+</sup>

replacePath(info: NavPathInfo, animated?: boolean): void

将当前页面栈栈顶退出，将info指定的NavDestination页面信息入栈。

**参数：**

| 名称   | 类型                            | 必填   | 描述                   |
| ---- | ----------------------------- | ---- | -------------------- |
| info | [NavPathInfo](#navpathinfo10) | 是    | 新栈顶页面参数信息 |
| animated<sup>11+</sup> | boolean | 否    | 是否支持转场动画，默认值：true。 |

### replacePathByName<sup>11+</sup>

replacePathByName(name: string, param: Object, animated?: boolean): void

将当前页面栈栈顶退出，将name指定的页面入栈。

**参数：**

| 名称    | 类型      | 必填   | 描述                    |
| ----- | ------- | ---- | --------------------- |
| name  | string  | 是    | NavDestination页面名称。   |
| param | Object | 是    | NavDestination页面详细参数。 |
| animated<sup>11+</sup> | boolean | 否    | 是否支持转场动画，默认值：true。 |

### removeByIndexes<sup>11+</sup>

removeByIndexes(indexes: Array<number\>): number

将页面栈内索引值在indexes中的NavDestination页面删除。

**参数：**

| 名称    | 类型      | 必填   | 描述                    |
| ----- | ------- | ---- | --------------------- |
| indexes  | Array<number\>  | 是    | 待删除NavDestination页面的索引值数组。   |

**返回值：**

| 类型          | 说明                       |
| ----------- | ------------------------ |
| number | 返回删除的NavDestination页面数量。 |

### removeByName<sup>11+</sup>

removeByName(name: string): number

将页面栈内指定name的NavDestination页面删除。

**参数：**

| 名称    | 类型      | 必填   | 描述                    |
| ----- | ------- | ---- | --------------------- |
| name  | string  | 是    | 删除的NavDestination页面的名字。   |

**返回值：**

| 类型          | 说明                       |
| ----------- | ------------------------ |
| number | 返回删除的NavDestination页面数量。 |

### pop<sup>10+</sup>

pop(animated?: boolean): NavPathInfo | undefined

弹出路由栈栈顶元素。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**参数：**

| 名称   | 类型                            | 必填   | 描述                   |
| ---- | ----------------------------- | ---- | -------------------- |
| animated<sup>11+</sup> | boolean | 否    | 是否支持转场动画，默认值：true。 |

**返回值：**

| 类型          | 说明                       |
| ----------- | ------------------------ |
| [NavPathInfo](#navpathinfo10) | 返回栈顶NavDestination页面的信息。 |
| undefined   | 当路由栈为空时返回undefined。      |

### pop<sup>11+</sup>

pop(result: Object, animated?: boolean): NavPathInfo | undefined

弹出路由栈栈顶元素，并触发onPop回调传入页面处理结果。

**参数：**

| 名称   | 类型                            | 必填   | 描述                   |
| ---- | ----------------------------- | ---- | -------------------- |
| result | Object | 是 | 页面自定义处理结果。 |
| animated | boolean | 否    | 是否支持转场动画，默认值：true。 |

**返回值：**

| 类型          | 说明                       |
| ----------- | ------------------------ |
| [NavPathInfo](#navpathinfo10) | 返回栈顶NavDestination页面的信息。 |
| undefined   | 当路由栈为空时返回undefined。      |

### popToName<sup>10+</sup>

popToName(name: string, animated?: boolean): number

回退路由栈到由栈底开始第一个名为name的NavDestination页面。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**参数：**

| 名称   | 类型     | 必填   | 描述                  |
| ---- | ------ | ---- | ------------------- |
| name | string | 是    | NavDestination页面名称。 |
| animated<sup>11+</sup> | boolean | 否    | 是否支持转场动画，默认值：true。 |

**返回值：**

| 类型     | 说明                                       |
| ------ | ---------------------------------------- |
| number | 如果栈中存在名为name的NavDestination页面，则返回由栈底开始第一个名为name的NavDestination页面的索引，否则返回-1。 |

### popToName<sup>11+</sup>

popToName(name: string, result: Object, animated?: boolean): number

回退路由栈到由栈底开始第一个名为name的NavDestination页面，并触发onPop回调传入页面处理结果。

**参数：**

| 名称   | 类型     | 必填   | 描述                  |
| ---- | ------ | ---- | ------------------- |
| name | string | 是    | NavDestination页面名称。 |
| result | Object | 是 | 页面自定义处理结果。 |
| animated | boolean | 否    | 是否支持转场动画，默认值：true。 |

**返回值：**

| 类型     | 说明                                       |
| ------ | ---------------------------------------- |
| number | 如果栈中存在名为name的NavDestination页面，则返回由栈底开始第一个名为name的NavDestination页面的索引，否则返回-1。 |

### popToIndex<sup>10+</sup>

popToIndex(index: number, animated?: boolean): void

回退路由栈到index指定的NavDestination页面。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**参数：**

| 名称    | 类型     | 必填   | 描述                     |
| ----- | ------ | ---- | ---------------------- |
| index | number | 是    | NavDestination页面的位置索引。 |
| animated<sup>11+</sup> | boolean | 否    | 是否支持转场动画，默认值：true。 |

### popToIndex<sup>11+</sup>

popToIndex(index: number, result: Object, animated?: boolean): void

回退路由栈到index指定的NavDestination页面，并触发onPop回调传入页面处理结果。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**参数：**

| 名称    | 类型     | 必填   | 描述                     |
| ----- | ------ | ---- | ---------------------- |
| index | number | 是    | NavDestination页面的位置索引。 |
| result | Object | 是 | 页面自定义处理结果。 |
| animated | boolean | 否    | 是否支持转场动画，默认值：true。 |

### moveToTop<sup>10+</sup>

moveToTop(name: string, animated?: boolean): number

将由栈底开始第一个名为name的NavDestination页面移到栈顶。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**参数：**

| 名称   | 类型     | 必填   | 描述                  |
| ---- | ------ | ---- | ------------------- |
| name | string | 是    | NavDestination页面名称。 |
| animated<sup>11+</sup> | boolean | 否    | 是否支持转场动画，默认值：true。 |

**返回值：**

| 类型     | 说明                                       |
| ------ | ---------------------------------------- |
| number | 如果栈中存在名为name的NavDestination页面，则返回由栈底开始第一个名为name的NavDestination页面的当前索引，否则返回-1。 |

### moveIndexToTop<sup>10+</sup>

moveIndexToTop(index: number, animated?: boolean): void

将index指定的NavDestination页面移到栈顶。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**参数：**

| 名称    | 类型     | 必填   | 描述                     |
| ----- | ------ | ---- | ---------------------- |
| index | number | 是    | NavDestination页面的位置索引。 |
| animated<sup>11+</sup> | boolean | 否    | 是否支持转场动画，默认值：true。 |

### clear<sup>10+</sup>

clear(animated?: boolean): void

清除栈中所有页面。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**参数：**

| 名称    | 类型     | 必填   | 描述                     |
| ----- | ------ | ---- | ---------------------- |
| animated<sup>11+</sup> | boolean | 否    | 是否支持转场动画，默认值：true。 |

### getAllPathName<sup>10+</sup>

getAllPathName(): Array<string\>

获取栈中所有NavDestination页面的名称。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**返回值：**

| 类型             | 说明                         |
| -------------- | -------------------------- |
| Array<string\> | 返回栈中所有NavDestination页面的名称。 |

### getParamByIndex<sup>10+</sup>

getParamByIndex(index: number): unknown | undefined

获取index指定的NavDestination页面的参数信息。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**参数：**

| 名称    | 类型     | 必填   | 描述                     |
| ----- | ------ | ---- | ---------------------- |
| index | number | 是    | NavDestination页面的位置索引。 |

**返回值：**

| 类型        | 说明                         |
| --------- | -------------------------- |
| unknown   | 返回对应NavDestination页面的参数信息。 |
| undefined | 传入index无效时返回undefined。     |

### getParamByName<sup>10+</sup>

getParamByName(name: string): Array<unknown\>

获取全部名为name的NavDestination页面的参数信息。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**参数：**

| 名称   | 类型     | 必填   | 描述                  |
| ---- | ------ | ---- | ------------------- |
| name | string | 是    | NavDestination页面名称。 |

**返回值：**

| 类型              | 说明                                |
| --------------- | --------------------------------- |
| Array<unknown\> | 返回全部名为name的NavDestination页面的参数信息。 |

### getIndexByName<sup>10+</sup>

getIndexByName(name: string): Array<number\>

获取全部名为name的NavDestination页面的位置索引。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**参数：**

| 名称   | 类型     | 必填   | 描述                  |
| ---- | ------ | ---- | ------------------- |
| name | string | 是    | NavDestination页面名称。 |

**返回值：**

| 类型             | 说明                                |
| -------------- | --------------------------------- |
| Array<number\> | 返回全部名为name的NavDestination页面的位置索引。 |

### size<sup>10+</sup>

size(): number

获取栈大小。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**返回值：**

| 类型     | 说明     |
| ------ | ------ |
| number | 返回栈大小。 |

### disableAnimation<sup>11+</sup>

disableAnimation(value: boolean): void

关闭（true）或打开（false）当前Navigation中所有转场动画。

**参数：**

| 名称    | 类型     | 必填   | 描述                     |
| ----- | ------ | ---- | ---------------------- |
| value | boolean | 否    | 是否关闭转场动画，默认值：false。 |

### getParent<sup>11+</sup>

getParent(): NavPathStack | null

获取父NavPathStack。<br/>当出现Navigation嵌套Navigation的情况时（可以是直接嵌套，也可以是间接嵌套），内部Navigation的NavPathStack能够获取到外层Navigation的NavPathStack。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**返回值：**

| 类型     | 说明     |
| ------ | ------ |
| [NavPathStack](#navpathstack10) \| null | 如果当前NavPathStack所属Navigation的外层有另外的一层Navigation，则能够获取到外层Navigation的NavPathStack。否则获取不到NavPathStack，返回null。 |

### setInterception<sup>12+</sup>

setInterception(interception: NavigationInterception): void

设置Navigation页面跳转拦截回调。

**参数：**

| 名称    | 类型     | 必填   | 描述                     |
| ---- | ---- | --- | ---|
|interception| [NavigationInterception](#navigationinterception12)| 是 | 设置Navigation跳转拦截对象。|

## NavPathInfo<sup>10+</sup>

路由页面信息。

### constructor

constructor(name: string, param: unknown)

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**参数：**

| 名称    | 类型      | 必填   | 描述                    |
| ----- | ------- | ---- | --------------------- |
| name  | string  | 是    | NavDestination页面名称。   |
| param | unknown | 是    | NavDestination页面详细参数。 |
| onPop<sup>11+</sup> | import('../api/@ohos.base').Callback\<[PopInfo](#popinfo11)> | 否 | NavDestination页面触发pop时返回的回调。 |

## PopInfo<sup>11+</sup>

下一个页面返回的回调信息载体。

**参数：**

| 名称 | 类型 | 必填 | 描述 |
|------|-----|-----|-----|
| info | [NavPathInfo](#navpathinfo10) | 是 | 页面触发返回时的当前页面信息，系统自动获取填入，无需开发者传入。 |
| result | Object | 是 | 页面触发返回时的结果，开发者自定义对象。 |

## NavContentInfo<sup>11+</sup>

跳转Destination信息。

**参数：**

| 名称  | 类型  | 必填  | 描述  |
|-------|-------|------|-------|
| name | string | 否 | NavDestination名称，如果为根视图(NavBar)，则返回值为undefined。|
| index | number | 是 | NavDestination在NavPathStack中的序号， 如果为根视图(NavBar)，则返回值为 -1。|
| mode | [NavDestinationMode](ts-basic-components-navdestination.md#navdestinationmode枚举说明) | 否 | NavDestination的模式，如果是根视图(NavBar)，则返回值为undefined。|

## NavigationAnimatedTransition<sup>11+</sup>

自定义转场动画协议，开发者需实现该协议来定义Navigation路由跳转的跳转动画。

**参数：**
| 名称 | 类型 | 必填 | 描述 |
|------|-----|-----|------|
| timeout | number | 否 | 动画超时结束时间。<br> 单位：ms。<br> 默认值：1000ms。|
| transition | (transitionProxy : [NavigationTransitionProxy](#navigationtransitionproxy-11)): void | 是 | 自定义转场动画执行回调。<br> transitionProxy: 自定义转场动画代理对象。|
| onTransitionEnd | (success: boolean):void | 否 | 转场完成回调。<br> success: 转场是否成功。 |

## NavigationTransitionProxy <sup>11+</sup>

自定义转场动画代理对象。

**参数：**

| 名称 | 类型  | 必填 | 描述  |
|------|-------|-----|-------|
| from | [NavContentInfo](#navcontentinfo11) | 是 | 退场页面信息。|
| to | [NavContentInfo](#navcontentinfo11) | 是 | 进场页面信息。|

### finishTransition

结束本次自定义转场动画，开发者需要主动触发该方法来结束本次转场，否则系统会在timeout的时间后结束本次转场。

## NavigationInterception<sup>12+</sup>

Navigation跳转拦截对象。

| 名称    | 类型     | 必填 | 描述    |
| ---- | ----- | ----- | ----   |
| willShow | (from: [NavDestinationContext](ts-basic-components-navdestination.md#navdestinationcontext11类型说明) \|"navBar",<br> to: [NavDestinationContext](ts-basic-components-navdestination.md#navdestinationcontext11类型说明) \|"navBar",<br> operation: [NavigationOperation](#navigationoperation11枚举说明),<br> isAnimated: boolean) =&gt;void | 否 | 页面跳转前拦截，允许操作栈，在当前跳转中生效。<br> from: 页面跳转之前的栈顶页面信息。参数值为navBar，则表示跳转前的页面为Navigation首页。<br> to: 页面跳转之后的栈顶页面信息。参数值为navBar，则标题跳转的目标页面为Navigation首页。<br> operation: 当前页面跳转类型。<br> isAnimated: 页面跳转是否有动画。 |
| didShow | (from: [NavDestinationContext](ts-basic-components-navdestination.md#navdestinationcontext11类型说明) \|"navBar",<br> to: [NavDestinationContext](ts-basic-components-navdestination.md#navdestinationcontext11类型说明) \|"navBar",<br> operation: [NavigationOperation](#navigationoperation11枚举说明),<br> isAnimated: boolean) =&gt;void | 否 | 页面跳转后回调。在该回调中操作栈在下一次跳转中刷新。<br> from: 页面跳转之前的栈顶页面信息。参数值为navBar，则表示跳转前页面为Navigation首页。<br> to: 页面跳转之后的栈顶页面信息。参数值为NavBar，则表示跳转目标页为Navigation首页。<br> operation: 当前页面跳转类型。<br> isAnimated: 页面跳转是否有动画。 | 否 | 发生页面跳转后回调。|
| modeChange | (mode: [NavigationMode](#navigationmode9枚举说明)) =&gt;void | 否 | Navigation单双栏显示状态发生变更时触发该回调。|

## NavigationMenuItem类型说明

| 名称     | 类型            | 必填   | 描述              |
| ------ | ------------- | ---- | --------------- |
| value  | string        | 是    | API Version 9: 显示菜单栏单个选项的文本。<br> API Version 10: 不显示菜单栏单个选项的文本。  <br/>**元服务API：** 从API version 11开始，该接口支持在元服务中使用。 |
| icon   | string        | 否    | 菜单栏单个选项的图标资源路径。 <br/>**元服务API：** 从API version 11开始，该接口支持在元服务中使用。 |
| isEnabled<sup>12+</sup>   | boolean        | 否    | 使能状态，默认使能（false未使能，true使能）。 |
| action | () =&gt; void | 否    | 当前选项被选中的事件回调。   <br/>**元服务API：** 从API version 11开始，该接口支持在元服务中使用。 |

## object类型说明

| 名称     | 类型            | 必填   | 描述              |
| ------ | ------------- | ---- | --------------- |
| value  | string        | 是    | 工具栏单个选项的显示文本。   |
| icon   | string        | 否    | 工具栏单个选项的图标资源路径。 |
| action | () =&gt; void | 否    | 当前选项被选中的事件回调。   |

## ToolbarItem<sup>10+</sup>类型说明

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

| 名称         | 类型                                       | 必填   | 描述                                       |
| ---------- | ---------------------------------------- | ---- | ---------------------------------------- |
| value      | ResourceStr                              | 是    | 工具栏单个选项的显示文本。                            |
| icon       | ResourceStr                              | 否    | 工具栏单个选项的图标资源路径。                          |
| action     | () =&gt; void                            | 否    | 当前选项被选中的事件回调。                            |
| status     | [ToolbarItemStatus](#toolbaritemstatus10枚举说明) | 否    | 工具栏单个选项的状态。<br/>默认值：ToolbarItemStatus.NORMAL |
| activeIcon | ResourceStr                              | 否    | 工具栏单个选项处于ACTIVE态时的图标资源路径。                |

## ToolbarItemStatus<sup>10+</sup>枚举说明

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

| 名称       | 描述                                       |
| -------- | ---------------------------------------- |
| NORMAL   | 设置工具栏单个选项为NORMAL态，该选项显示默认样式，可以触发Hover，Press，Focus事件并显示对应的多态样式。 |
| DISABLED | 设置工具栏单个选项为DISABLED态， 该选项显示DISABLED态样式，并且不可交互。 |
| ACTIVE   | 设置工具栏单个选项为ACTIVE态， 该选项通过点击事件可以将icon图标更新为activeIcon对应的图片资源。 |

## NavigationTitleMode枚举说明

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

| 名称   | 描述                                       |
| ---- | ---------------------------------------- |
| Free | 当内容为满一屏的可滚动组件时，标题随着内容向上滚动而缩小（子标题的大小不变、淡出）。向下滚动内容到顶时则恢复原样。<br/>**说明：** <br/>标题随着内容滚动大小联动的动效在title设置为ResourceStr和NavigationCommonTitle时生效，设置成其余自定义节点类型时字体样式无法变化，下拉时只影响标题栏偏移。<br/>可滚动组件不满一屏时，如果想使用联动效果，就要使用滚动组件提供的[edgeEffect](ts-container-list.md#属性)接口将options参数设置为true。 |
| Mini | 固定为小标题模式。                                |
| Full | 固定为大标题模式。                                |

## NavigationCommonTitle<sup>9+</sup>类型说明

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

| 名称   | 类型     | 必填   | 描述     |
| ---- | ------ | ---- | ------ |
| main | string | 是    | 设置主标题。 |
| sub  | string | 是    | 设置副标题。 |

## NavigationCustomTitle<sup>9+</sup>类型说明

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

| 名称      | 类型                                       | 必填   | 描述       |
| ------- | ---------------------------------------- | ---- | -------- |
| builder | [CustomBuilder](ts-types.md#custombuilder8) | 是    | 设置标题栏内容。 |
| height  | [TitleHeight](#titleheight9枚举说明) \| [Length](ts-types.md#length) | 是    | 设置标题栏高度。 |

## NavBarPosition<sup>9+</sup>枚举说明

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

| 名称    | 描述               |
| ----- | ---------------- |
| Start | 双栏显示时，主列在主轴方向首部。 |
| End   | 双栏显示时，主列在主轴方向尾部。 |

## NavigationMode<sup>9+</sup>枚举说明

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

| 名称  | 描述                                                         |
| ----- | ------------------------------------------------------------ |
| Stack | 导航栏与内容区独立显示，相当于两个页面。                     |
| Split | 导航栏与内容区分两栏显示。<br/>以下navBarWidthRange的值用[minNavBarWidth,maxNavBarWidth]表示<br/>1.当navBarWidth属性的值，在navBarWidthRange属性的值范围以外时，navBarWidth按如下规则显示：<br/>navBarWidth < minNavBarWidth时，navBarWidth修正为minNavBarWidth;<br/>navBarWidth > maxNavBarWidth，且组件宽度 - minContentWidth - 分割线宽度(1vp) > maxNavBarWidth时，navBarWidth修正为maxNavBarWidth;<br/>navBarWidth > maxNavBarWidth，且组件宽度 - minContentWidth - 分割线宽度(1vp) < minNavBarWidth时，navBarWidth修正为minNavBarWidth;<br/>navBarWidth > maxNavBarWidth，且组件宽度 - minContentWidth - 分割线宽度(1vp)在navBarWidthRange范围内，navBarWidth修正为组件宽度 - 分割线宽度(1vp) - minContentWidth。<br/>2.当navBarWidth属性的值，在navBarWidthRange属性的值范围以内时，navBarWidth按如下规则显示：<br/>minNavBarWidth + minContentWidth + 分割线宽度(1vp) >= 组件宽度时，navBarWidth修正为minNavBarWidth；<br/>minNavBarWidth + minContentWidth + 分割线宽度(1vp) < 组件宽度，且navBarWidth + minContentWidth + 分割线宽度(1vp) >= 组件宽度时，navBarWidth修正为组件宽度 - 分割线宽度(1vp) - minContentWidth;<br/>minNavBarWidth + minContentWidth + 分割线宽度(1vp) < 组件宽度，且navBarWidth + minContentWidth + 分割线宽度(1vp) < 组件宽度时，navBarWidth为设置的值。<br/>3.缩小组件尺寸时，先缩小内容区的尺寸至minContentWidth，然后再缩小导航栏的尺寸至minNavBarWidth。若继续缩小，先缩小内容区，内容区消失后再缩小导航栏。<br/>4.设置导航栏为固定尺寸时，若持续缩小组件尺寸，导航栏最后压缩显示。<br/>5.若只设置了navBarWidth属性，则导航栏宽度为navBarWidth，且分割线不可拖动。 |
| Auto  | API version 9之前：窗口宽度>=520vp时，采用Split模式显示；窗口宽度<520vp时，采用Stack模式显示。<br/>API version 10及以上：窗口宽度>=600vp时，采用Split模式显示；窗口宽度<600vp时，采用Stack模式显示，600vp等于minNavBarWidth(240vp) + minContentWidth (360vp)。 |

## TitleHeight<sup>9+</sup>枚举说明

| 名称          | 描述                         |
| ----------- | -------------------------- |
| MainOnly    | 只有主标题时标题栏的推荐高度（56vp）。      |
| MainWithSub | 同时有主标题和副标题时标题栏的推荐高度（82vp）。 |

## NavigationOperation<sup>11+</sup>枚举说明
| 名称    | 描述  |
|---------|------|
|PUSH | 本次转场为页面进场。|
|POP | 本次转场为页面退场。|
| REPLACE | 本次转场为页面替换。|

## NavigationTitleOptions<sup>11+</sup>类型说明

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

| 名称     | 类型            | 必填   | 描述              |
| ------ | ------------- | ---- | --------------- |
| backgroundColor | [ResourceColor](ts-types.md#resourcecolor)  | 否    | 标题栏背景颜色，不设置时为系统默认颜色。 |
| backgroundBlurStyle   | [BlurStyle](ts-appendix-enums.md#blurstyle9)        | 否    | 标题栏背景模糊样式，不设置时关闭背景模糊效果。 |

## NavigationToolbarOptions<sup>11+</sup>类型说明

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

| 名称     | 类型            | 必填   | 描述              |
| ------ | ------------- | ---- | --------------- |
| backgroundColor | [ResourceColor](ts-types.md#resourcecolor)  | 否    | 工具栏背景颜色，不设置时为系统默认颜色。 |
| backgroundBlurStyle   | [BlurStyle](ts-appendix-enums.md#blurstyle9)        | 否    | 工具栏背景模糊样式，不设置时关闭背景模糊效果。 |

## 示例

### 示例1

```ts
// xxx.ets
class A {
  text: string = ''
  num: number = 0
}

@Entry
@Component
struct NavigationExample {
  private arr: number[] = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
  @State currentIndex: number = 0

  @Builder NavigationTitle() {
    Column() {
      Text('Title')
        .fontColor('#182431')
        .fontSize(30)
        .lineHeight(41)
        .fontWeight(700)
      Text('subtitle')
        .fontColor('#182431')
        .fontSize(14)
        .lineHeight(19)
        .opacity(0.4)
        .margin({ top: 2, bottom: 20 })
    }.alignItems(HorizontalAlign.Start)
  }

  @Builder NavigationMenus() {
    Row() {
      Image('resources/base/media/ic_public_add.svg')
        .width(24)
        .height(24)
      Image('resources/base/media/ic_public_add.svg')
        .width(24)
        .height(24)
        .margin({ left: 24 })
      Image('common/ic_public_more.svg')
        .width(24)
        .height(24)
        .margin({ left: 24 })
    }
  }

  build() {
    Column() {
      Navigation() {
        TextInput({ placeholder: 'search...' })
          .width('90%')
          .height(40)
          .backgroundColor('#FFFFFF')
          .margin({ top: 8 })

        List({ space: 12, initialIndex: 0 }) {
          ForEach(this.arr, (item: number) => {
            ListItem() {
              Text('' + item)
                .width('90%')
                .height(72)
                .backgroundColor('#FFFFFF')
                .borderRadius(24)
                .fontSize(16)
                .fontWeight(500)
                .textAlign(TextAlign.Center)
            }
          }, (item: number) => item.toString())
        }
        .height(324)
        .width('100%')
        .margin({ top: 12, left: '10%' })
      }
      .title(this.NavigationTitle)
      .menus(this.NavigationMenus)
      .titleMode(NavigationTitleMode.Full)
      .toolbarConfiguration([
        {
          value: $r("app.string.navigation_toolbar_add"),
          icon: $r("app.media.ic_public_highlightsed")
        },
        {
          value: $r("app.string.navigation_toolbar_app"),
          icon: $r("app.media.ic_public_highlights")
        },
        {
          value: $r("app.string.navigation_toolbar_collect"),
          icon: $r("app.media.ic_public_highlights")
        }
      ])
      .hideTitleBar(false)
      .hideToolBar(false)
      .onTitleModeChange((titleModel: NavigationTitleMode) => {
        console.info('titleMode' + titleModel)
      })
    }.width('100%').height('100%').backgroundColor('#F1F3F5')
  }
}
```

![zh-cn_image_navigation](figures/zh-cn_image_navigation.png)



### 示例2
```ts
// Index.ets

@Entry
@Component
struct NavigationExample {
  pageInfos: NavPathStack = new NavPathStack()
  isUseInterception: boolean = false;

  registerInterception() {
    this.pageInfos.setInterception({
      willShow: (from: NavDestinationContext | "navBar", to: NavDestinationContext | "navBar",
                 operation: NavigationOperation, animated: boolean) => {
        if (!this.isUseInterception) {
          return;
        }
        if (typeof to === "string") {
          console.log("target page is navigation home");
          return;
        }
        // redirect target page.Change pageTwo to pageOne.
        let target: NavDestinationContext = to as NavDestinationContext;
        if (target.pathInfo.name === 'pageTwo') {
          target.pathStack.pop();
          target.pathStack.pushPathByName('pageOne', null);
        }
      },
      didShow: (from: NavDestinationContext | "navBar", to: NavDestinationContext | "navBar",
                operation: NavigationOperation, isAnimated: boolean) => {
        if (!this.isUseInterception) {
          return;
        }
        if (typeof from === "string") {
          console.log("current transition is from navigation home");
        } else {
          console.log(`current transition is from  ${(from as NavDestinationContext).pathInfo.name}`)
        }
        if (typeof to === "string") {
          console.log("current transition to is navBar");
        } else {
          console.log(`current transition is to ${(to as NavDestinationContext).pathInfo.name}`);
        }
      },
      modeChange: (mode: NavigationMode) => {
        if (!this.isUseInterception) {
          return;
        }
        console.log(`current navigation mode is ${mode}`);
      }
    })
  }

  build() {
    Navigation(this.pageInfos) {
      Column() {
        Button('pushPath', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pageInfos.pushPath({ name: 'pageOne' }) //将name指定的NavDestination页面信息入栈
          })
        Button('use interception', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.isUseInterception = !this.isUseInterception;
            if (this.isUseInterception) {
              this.registerInterception();
            } else {
              this.pageInfos.setInterception(undefined);
            }
          })
      }
    }.title('NavIndex')
  }
}
```
```ts
// PageOne.ets
class TmpClass{
  count:number=10
}

@Builder
export function PageOneBuilder(name: string, param: Object) {
  PageOne()
}

@Component
export struct PageOne {

  pageInfos: NavPathStack = new NavPathStack()

  build() {
    NavDestination() {
      Column() {
        Button('pushPathByName', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            let tmp = new TmpClass()
            this.pageInfos.pushPathByName('pageTwo', tmp) //将name指定的NavDestination页面信息入栈，传递的数据为param
          })
        Button('popToname', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pageInfos.popToName('pageTwo') //回退路由栈到第一个名为name的NavDestination页面
            console.log('popToName' + JSON.stringify(this.pageInfos), '返回值' + JSON.stringify(this.pageInfos.popToName('pageTwo')))
          })
        Button('popToIndex', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pageInfos.popToIndex(1) // 回退路由栈到index指定的NavDestination页面
            console.log('popToIndex' + JSON.stringify(this.pageInfos))
          })
        Button('moveToTop', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pageInfos.moveToTop('pageTwo') // 将第一个名为name的NavDestination页面移到栈顶
            console.log('moveToTop' + JSON.stringify(this.pageInfos), '返回值' + JSON.stringify(this.pageInfos.moveToTop('pageTwo')))
          })
        Button('moveIndexToTop', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pageInfos.moveIndexToTop(1) // 将index指定的NavDestination页面移到栈顶
            console.log('moveIndexToTop' + JSON.stringify(this.pageInfos))
          })
        Button('clear', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pageInfos.clear() //清除栈中所有页面
          })
        Button('get', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            console.log('-------------------')
            console.log('获取栈中所有NavDestination页面的名称', JSON.stringify(this.pageInfos.getAllPathName()))
            console.log('获取index指定的NavDestination页面的参数信息', JSON.stringify(this.pageInfos.getParamByIndex(1)))
            console.log('获取全部名为name的NavDestination页面的参数信息', JSON.stringify(this.pageInfos.getParamByName('pageTwo')))
            console.log('获取全部名为name的NavDestination页面的位置索引', JSON.stringify(this.pageInfos.getIndexByName('pageOne')))
            console.log('获取栈大小', JSON.stringify(this.pageInfos.size()))
          })
      }.width('100%').height('100%')
    }.title('pageOne')
    .onBackPressed(() => {
      const popDestinationInfo = this.pageInfos.pop() // 弹出路由栈栈顶元素
      console.log('pop' + '返回值' + JSON.stringify(popDestinationInfo))
      return true
    }).onReady((context: NavDestinationContext) => {
      this.pageInfos = context.pathStack
    })
  }
}
```
```ts
// PageTwo.ets
@Builder
export function PageTwoBuilder(name: string, param: Object) {
  PageTwo()
}

@Component
export struct PageTwo {
  pathStack: NavPathStack = new NavPathStack()

  private menuItems: Array<NavigationMenuItem> = [
    {
      value: "1",
      icon: 'resources/base/media/undo.svg',
    },
    {
      value: "2",
      icon: 'resources/base/media/redo.svg',
      isEnabled: false,
    },
    {
      value: "3",
      icon: 'resources/base/media/ic_public_ok.svg',
      isEnabled: true,
    }
  ]

  build() {
    NavDestination() {
      Column() {
        Button('pushPathByName', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pathStack.pushPathByName('pageOne', null)
          })
      }.width('100%').height('100%')
    }.title('pageTwo')
    .menus(this.menuItems)
    .onBackPressed(() => {
      this.pathStack.pop()
      return true
    })
    .onReady((context: NavDestinationContext) => {
      this.pathStack = context.pathStack;
      console.log("current page config info is " + JSON.stringify(context.getConfigInRouteMap()))
    })
  }
}
```

```json
// 工程配置文件module.json5中配置 {"routerMap": "$profile:route_map"}
// route_map.json
{
  "routerMap": [
    {
      "name": "pageOne",
      "pageSourceFile": "src/main/ets/pages/PageOne.ets",
      "buildFunction": "PageOneBuilder",
      "data": {
        "description": "this is pageOne"
      }
    },
    {
      "name": "pageTwo",
      "pageSourceFile": "src/main/ets/pages/PageTwo.ets",
      "buildFunction": "PageTwoBuilder"
    }
  ]
}
```
![navigation.gif](figures/navigation.gif)

### 示例3

该示例主要演示设置每个NavDestination子页面的自定义转场动画。

```ts
// Index.ets
import { CustomTransition, AnimateCallback } from './CustomNavigationUtils'

@Entry
@Component
struct NavigationExample {
  pageInfos: NavPathStack = new NavPathStack()

  aboutToAppear() {
    if (this.pageInfos === undefined) {
      this.pageInfos = new NavPathStack();
    }
    this.pageInfos.pushPath({name: 'pageOne'}, false)
  }

  build() {
    Navigation(this.pageInfos) {
    }.title('NavIndex')
    .hideNavBar(true)
    .customNavContentTransition((from: NavContentInfo, to: NavContentInfo, operation: NavigationOperation) => {
      if (from.mode == NavDestinationMode.DIALOG || to.mode == NavDestinationMode.DIALOG) {
        return undefined;
      }
      console.log(`current info: ${to.name}, index: ${to.index}, mode: ${to.mode}`);
      console.log(`pre info: ${from.name}, index: ${from.index}, mode: ${from.mode}`);
      console.log(`operation: ${operation}`)
      if (from.index === -1 || to.index === -1) {
        return undefined;
      }
      let customAnimation: NavigationAnimatedTransition = {
        onTransitionEnd: (isSuccess: boolean)=>{
          console.log(`current transition result is ${isSuccess}`);
        },
        timeout: 700,
        // 转场开始时系统调用该方法，并传入转场上下文代理对象
        transition: (transitionProxy: NavigationTransitionProxy)=>{
          console.log("trigger transition callback");
          // 从封装类CustomTransition中根据子页面的序列获取对应的转场动画回调
          let fromParam: AnimateCallback = CustomTransition.getInstance().getAnimateParam(from.index);
          let toParam: AnimateCallback = CustomTransition.getInstance().getAnimateParam(to.index);
          if (fromParam.start != undefined) {
            fromParam.start(operation == NavigationOperation.PUSH, true);
          }
          if (toParam.start != undefined) {
            toParam.start(operation == NavigationOperation.PUSH, false);
          }
          animateTo({duration: 400, onFinish: ()=>{
            if (fromParam.onFinish != undefined) {
              fromParam.onFinish(operation === NavigationOperation.PUSH, true);
            }
            if (toParam.onFinish != undefined) {
              toParam.onFinish(operation === NavigationOperation.PUSH, true);
            }
            transitionProxy.finishTransition();
          }}, ()=>{
            if (fromParam.finish != undefined) {
              fromParam.finish(operation === NavigationOperation.PUSH, true);
            }
            if (toParam.finish != undefined) {
              toParam.finish(operation === NavigationOperation.PUSH, false);
            }
          })
        }
      };
      return customAnimation;
    })
  }
}
```

```ts
// PageOne.ets
import {CustomTransition} from './CustomNavigationUtils'

@Builder
export function PageOneBuilder(name: string, param: Object) {
  PageOne()
}

@Component
export struct PageOne {
  pageInfos: NavPathStack = new NavPathStack()
  @State x: number = 0
  @State scaleVal: number = 1
  pageId: number = 0;

  aboutToAppear() {
    this.pageId = this.pageInfos.getAllPathName().length - 1;
    CustomTransition.getInstance().registerNavParam(this.pageId, (isPush: boolean, isExit: boolean) => {
      this.x = isExit ? 0 : 300;
    }, (isPush: boolean, isExit: boolean)=> {
      this.x = isExit ? -300 : 0;
    }, (isPush: boolean, isExit: boolean) => {
      this.x = 0;
    }, 200);
  }

  build() {
    NavDestination() {
      Column() {
        Button('pushPathByName', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pageInfos.pushPathByName('pageTwo', null) //将name指定的NavDestination页面信息入栈，传递的数据为param
          })
      }.width('100%').height('100%')
    }.title('pageOne')
    .mode(NavDestinationMode.STANDARD)
    .onBackPressed(() => {
      const popDestinationInfo = this.pageInfos.pop() // 弹出路由栈栈顶元素
      console.log('pop' + '返回值' + JSON.stringify(popDestinationInfo))
      return true
    })
    .onDisAppear(()=>{
      CustomTransition.getInstance().unRegisterNavParam(this.pageId)
    })
    .onReady((context: NavDestinationContext) => {
      this.pageInfos = context.pathStack
    })
    .translate({x: this.x, y: 0, z: 0})
    .backgroundColor(Color.White)
  }
}
```
```ts
// PageTwo.ets
import {CustomTransition} from './CustomNavigationUtils'

@Builder
export function PageTwoBuilder(name: string, param: Object) {
  PageTwo()
}

@Component
export struct PageTwoTemp {
  pathInfo: NavPathStack = new NavPathStack()
  @State x: number = 300
  pageId: number = 0

  aboutToAppear() {
    this.pageId = this.pageInfos.getAllPathName().length - 1;
    CustomTransition.getInstance().registerNavParam(this.pageId, (isPush: boolean, isExit: boolean)=>{
      console.log("current page is pageOne")
      this.x = isExit ? 0 : isPush ? 300 : -300;
    }, (isPush: boolean, isExit: boolean)=>{
      this.x = isExit ? isPush ? -300 : 300 : 0;
    }, (isPush: boolean, isExit: boolean) => {
      this.x = 0;
    }, 2000)
  }

  build() {
    NavDestination() {
      Column() {
        Button('pushPathByName', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pageInfos.pushPathByName('pageOne', null) //将name指定的NavDestination页面信息入栈，传递的数据为param
          })
      }.width('100%').height('100%')
    }.title('pageTwo')
    .onBackPressed(() => {
      const popDestinationInfo = this.pageInfos.pop() // 弹出路由栈栈顶元素
      console.log('pop' + '返回值' + JSON.stringify(popDestinationInfo))
      return true
    })
    .onDisAppear(()=>{
      CustomTransition.getInstance().unRegisterNavParam(this.pageId)
    })
    .onReady((context: NavDestinationContext) => {
      this.pageInfos = context.pathStack;
    })
    .opacity(0.5)
    .translate({x: this.x})
    .backgroundColor(Color.White)
  }
}
```
```ts
// CustomNavigationUtils.ts
// 自定义接口，用来保存某个页面相关的转场动画回调和参数
export interface AnimateCallback {
  finish: ((isPush: boolean, isExit: boolean) => void | undefined) | undefined;
  start: ((isPush: boolean, isExit: boolean) => void | undefined) | undefined;
  onFinish: ((isPush: boolean, isExit: boolean) => void | undefined) | undefined;
  timeout: (number | undefined) | undefined;
}
const customTransitionMap: Map<number, AnimateCallback> = new Map()
export class CustomTransition {
  private constructor() {

  }

  static delegate = new CustomTransition();

  static getInstance() {
    return CustomTransition.delegate;
  }

  // 注册某个页面的动画回调
  // startCallback：用来设置动画开始时页面的状态
  // endCallback：用来设置动画结束时页面的状态
  // onFinish：用来执行动画结束后页面的其他操作
  // timeout：转场结束的超时时间
  registerNavParam(name: number, startCallback: (operation: boolean, isExit: boolean) => void,
                   endCallback:(operation: boolean, isExit: boolean) => void,
                   onFinish: (opeation: boolean, isExit: boolean) => void, timeout: number): void {

    if (customTransitionMap.has(name)) {
      let param = customTransitionMap.get(name);
      if (param != undefined) {
        param.start = startCallback;
        param.finish = endCallback;
        param.timeout = timeout;
        param.onFinish = onFinish;
        return;
      }
    }
    let params: AnimateCallback = {timeout: timeout, start: startCallback, finish: endCallback, onFinish: onFinish};
    customTransitionMap.set(name, params);
  }

  unRegisterNavParam(name: number): void {
    customTransitionMap.delete(name);
  }

  getAnimateParam(name: number): AnimateCallback {
    let result: AnimateCallback = {
      start: customTransitionMap.get(name)?.start,
      finish: customTransitionMap.get(name)?.finish,
      timeout: customTransitionMap.get(name)?.timeout,
      onFinish: customTransitionMap.get(name)?.onFinish
    };
    return result;
  }
}
```
```json
// 工程配置文件module.json5中配置 {"routerMap": "$profile:route_map"}
// route_map.json
{
  "routerMap": [
    {
      "name": "pageOne",
      "pageSourceFile": "src/main/ets/pages/PageOne.ets",
      "buildFunction": "PageOneBuilder",
      "data": {
        "description": "this is pageOne"
      }
    },
    {
      "name": "pageTwo",
      "pageSourceFile": "src/main/ets/pages/PageTwo.ets",
      "buildFunction": "PageTwoBuilder"
    }
  ]
}
```

![customNavigation.gif](figures/customNavigation.gif)

### 示例4
```ts
// Index.ets

@Entry
@Component
struct NavigationExample {
  pageInfo: NavPathStack = new NavPathStack()

  build() {
    Navigation(this.pageInfo) {
      Column() {
        Button('StartTest', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pageInfo.pushPath({ name: 'pageOne' }); // 将name指定的NavDestination页面信息入栈。
          })
      }
    }.title('NavIndex')
  }
}
```
```ts
// PageOne.ets
import { BusinessError } from '@ohos.base';

class TmpClass{
  count:number = 10
}

class ParamWithOp {
  operation: number = 1
  count: number = 10
}

@Builder
export function PageOneBuilder(name: string, param: Object) {
  PageOne()
}

@Component
export struct PageOne {
  pageInfo: NavPathStack = new NavPathStack();
  @State message: string = 'Hello World'

  build() {
    NavDestination() {
      Column() {
        Text(this.message)
          .width('80%')
          .height(50)
          .margin(10)

        Button('pushPath', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(10)
          .onClick(()=>{
            this.pageInfo.pushPath({name: 'pageTwo', param: new ParamWithOp(), onPop: (popInfo: PopInfo)=>{
              this.message = '[pushPath]last page is: ' + popInfo.info.name + ', result: ' + JSON.stringify(popInfo.result);
            }}); // 将name指定的NavDestination页面信息入栈，传递的数据为param，添加接收处理结果的onPop回调。
          })

        Button('pushPathByName', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(10)
          .onClick(() => {
            let tmp = new TmpClass()
            this.pageInfo.pushPathByName('pageTwo', tmp, (popInfo)=>{
              this.message = '[pushPathByName]last page is: ' + popInfo.info.name + ', result: ' + JSON.stringify(popInfo.result);
            }); // 将name指定的NavDestination页面信息入栈，传递的数据为param，添加接收处理结果的onPop回调。
          })

        Button('pushDestination', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(10)
          .onClick(()=>{
            let tmp = new TmpClass()
            // 将name指定的NavDestination页面信息入栈，传递的数据为param，添加接收处理结果的onPop回调。
            this.pageInfo.pushDestination({name: 'pageTwo', param: new ParamWithOp(), onPop: (popInfo: PopInfo)=>{
              this.message = '[pushDestination]last page is: ' + popInfo.info.name + ', result: ' + JSON.stringify(popInfo.result);
            }}).catch((error: BusinessError)=>{
              console.error(`[pushDestination]failed, error code = ${error.code}, error.message = ${error.message}.`);
            }).then(()=>{
              console.error('[pushDestination]success.');
            });
          })

        Button('pushDestinationByName', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(10)
          .onClick(()=>{
            let tmp = new TmpClass()
            // 将name指定的NavDestination页面信息入栈，传递的数据为param，添加接收处理结果的onPop回调。
            this.pageInfo.pushDestinationByName('pageTwo', tmp, (popInfo)=>{
              this.message = '[pushDestinationByName]last page is: ' + popInfo.info.name + ', result: ' + JSON.stringify(popInfo.result);
            }).catch((error: BusinessError)=>{
              console.error(`[pushDestinationByName]failed, error code = ${error.code}, error.message = ${error.message}.`);
            }).then(()=>{
              console.error('[pushDestinationByName]success.');
            });
          })

        Button('pushPathWithoutOnPop', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(10)
          .onClick(()=>{
            this.pageInfo.pushPath({name: 'pageTwo', param: new ParamWithOp()}); // 将name指定的NavDestination页面信息入栈。
          })

        Button('pushPathByNameWithoutOnPop', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(10)
          .onClick(() => {
            let tmp = new TmpClass()
            this.pageInfo.pushPathByName('pageTwo', tmp); // 将name指定的NavDestination页面信息入栈，传递的数据为param。
          })

        Button('pushDestinationWithoutOnPop', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(10)
          .onClick(()=>{
            let tmp = new TmpClass()
            // 将name指定的NavDestination页面信息入栈，传递的数据为param，添加接收处理结果的onPop回调。
            this.pageInfo.pushDestination({name: 'pageTwo', param: new ParamWithOp()})
              .catch((error: BusinessError)=>{
              console.error(`[pushDestinationWithoutOnPop]failed, error code = ${error.code}, error.message = ${error.message}.`);
            }).then(()=>{
              console.error('[pushDestinationWithoutOnPop]success.');
            });
          })

        Button('pushDestinationByNameWithoutOnPop', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(10)
          .onClick(() => {
            let tmp = new TmpClass()
            // 将name指定的NavDestination页面信息入栈，传递的数据为param。
            this.pageInfo.pushDestinationByName('pageTwo', tmp)
              .catch((error: BusinessError)=>{
                console.error(`[pushDestinationByNameWithoutOnPop]failed, error code = ${error.code}, error.message = ${error.message}.`);
              }).then(()=>{
              console.error('[pushDestinationByNameWithoutOnPop]success.');
            });
          })

        Button('clear', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(10)
          .onClick(() => {
            this.pageInfo.clear(); // 清除栈中所有页面。
          })
      }.width('100%').height('100%')
    }.title('pageOne')
    .onBackPressed(() => {
      this.pageInfo.pop({number: 1}) // 弹出路由栈栈顶元素。
      return true
    }).onReady((context: NavDestinationContext) => {
      this.pageInfo = context.pathStack;
    })
  }
}
```
```ts
// PageTwo.ets

class resultClass {
  constructor(count: number) {
    this.count = count;
  }
  count: number = 10
}

@Builder
export function PageTwoBuilder(name: string, pram: Object) {
  PageTwo()
}

@Component
export struct PageTwo {
  pathStack: NavPathStack = new NavPathStack()

  build() {
    NavDestination() {
      Column() {
        Button('pop', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pathStack.pop(new resultClass(1)); // 回退到上一个页面，将处理结果传入push的onPop回调中。
          })

        Button('popToName', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pathStack.popToName('pageOne', new resultClass(11)); // 将第一个名为name的NavDestination页面移到栈顶，将处理结果传入push的onPop回调中。
          })

        Button('popToIndex', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pathStack.popToIndex(0, new resultClass(111)); // 将index指定的NavDestination页面移到栈顶，将处理结果传入push的onPop回调中。
          })

        Button('popWithoutResult', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pathStack.pop();
          })

        Button('popToNameWithoutResult', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pathStack.popToName('pageOne');
          })

        Button('popToIndexWithoutResult', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.pathStack.popToIndex(0);
          })
      }.width('100%').height('100%')
    }.title('pageTwo')
    .onBackPressed(() => {
      this.pathStack.pop(new resultClass(0)); // 回退到上一个页面，将处理结果传入push的onPop回调。
      return true;
    }).onReady((context: NavDestinationContext) => {
      this.pathStack = context.pathStack
    })
  }
}
```
```json
// 工程配置文件module.json5中配置 {"routerMap": "$profile:route_map"}
// route_map.json
{
  "routerMap": [
    {
      "name": "pageOne",
      "pageSourceFile": "src/main/ets/pages/PageOne.ets",
      "buildFunction": "PageOneBuilder",
      "data": {
        "description": "this is pageOne"
      }
    },
    {
      "name": "pageTwo",
      "pageSourceFile": "src/main/ets/pages/PageTwo.ets",
      "buildFunction": "PageTwoBuilder"
    }
  ]
}
```
![navigationWithOnPop.gif](figures/navigationWithOnPop.gif)

### 示例5

```ts
// 该示例主要演示设置Navigation的标题栏和工具栏的背景颜色和背景模糊效果。
@Entry
@Component
struct NavigationExample {
  @State pathStack: NavPathStack = new NavPathStack();
  @State switchColor: boolean = false;
  @State switchBlur: boolean = false;

  @Builder
  BackgroundBuilder() {
    Row() {
      Column() {}
      .layoutWeight(1)
      .height('100%')
      .backgroundColor(Color.Red)
      Column() {}
      .layoutWeight(1)
      .height('100%')
      .backgroundColor(Color.Green)
      Column() {}
      .layoutWeight(1)
      .height('100%')
      .backgroundColor(Color.Blue)
    }
    .height('100%')
  }

  build() {
    Navigation(this.pathStack) {
      Column() {
        Button('switch color', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            console.log(`testTag switchColor`)
            this.switchColor = !this.switchColor;
          })
        Button('switch blur', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            console.log(`testTag switchBlur`)
            this.switchBlur = !this.switchBlur;
          })
      }
      .width('100%')
      .height('100%')
    }
    // 使用定制化的背景能够凸显背景模糊的效果
    .background(this.BackgroundBuilder)
    .width('100%')
    .height('100%')
    // 开发者可以设置标题栏的背景颜色和背景模糊效果
    .title("NavTitle", {
      backgroundColor: this.switchColor ? "#90D1D2D3" : "#90121314",
      backgroundBlurStyle: this.switchBlur ? BlurStyle.BACKGROUND_THICK : BlurStyle.BACKGROUND_THIN
    })
    // 开发者可以设置工具栏的背景颜色和背景模糊效果
    .toolbarConfiguration([
      {value: 'a'},
      {value: 'b'},
      {value: 'c'},
    ], {
      backgroundColor: this.switchColor ? "#90D1D2D3" : "#90121314",
      backgroundBlurStyle: this.switchBlur ? BlurStyle.BACKGROUND_THICK : BlurStyle.BACKGROUND_THIN
    })
  }
}
```
![navigationColorBlur.gif](figures/navigationColorBlur.gif)

### 示例6

```ts
// 该示例主要演示在嵌套Navigation场景下，如何获取父NavPathStack。
@Entry
@Component
struct NavigationExample1 {
  @State childNavStack: NavPathStack = new NavPathStack();

  build() {
    Navigation() {
      Stack({alignContent: Alignment.Center}) {
        Navigation(this.childNavStack) {
          Button('push Path to parent Navigation', { stateEffect: true, type: ButtonType.Capsule })
            .width('80%')
            .height(40)
            .margin(20)
            .onClick(() => {
              // 可以获取父NavPathStack
              let parentStack = this.childNavStack.getParent();
              parentStack?.pushPath({ name: "pageOne"})
            })
        }
        .clip(true)
        .backgroundColor(Color.Orange)
        .width('80%')
        .height('80%')
        .title('ChildNavigation')
      }
      .width('100%')
      .height('100%')
    }
    .backgroundColor(Color.Green)
    .width('100%')
    .height('100%')
    .title('ParentNavigation')
  }
}
```
```ts
// PageOne.ets
  @Builder
  export function PageOneBuilder(name: string) {
    NavDestination() {
      Text("this is " + name)
    }
    .title(name)
  }
```
```json
// 工程配置文件module.json5中配置 {"routerMap": "$profile:route_map"}
// route_map.json
{
  "routerMap": [
    {
      "name": "pageOne",
      "pageSourceFile": "src/main/ets/pages/PageOne.ets",
      "buildFunction": "PageOneBuilder",
      "data": {
        "description": "this is pageOne"
      }
    }
  ]
}
```
![navPathStackGetParent.gif](figures/navPathStackGetParent.gif)

### 示例7

```ts
// 该示例主要演示如下两点功能：
// 1. NavPathStack无需声明为状态变量，也可以实现页面栈操作功能；
// 2. NavDestination通过onReady事件能够拿到对应的NavPathInfo和所属的NavPathStack。
class PageParam {
  constructor(num_: number) {
    this.num = num_;
  }
  num: number = 0;
}

@Builder
export function PageOneBuilder(name: string, param: Object) {
  PageOne()
}

@Component
struct PageOne {
  private stack: NavPathStack | null = null;
  private name: string = "";
  private paramNum: number = 0;

  build() {
    NavDestination() {
      Column() {
        Text("NavPathInfo: name: " + this.name + ", paramNum: " + this.paramNum)
        Button('pushPath', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            if (this.stack) {
              let p = new PageParam(this.paramNum + 1);
              this.stack.pushPath({name: "pageOne", param: p});
            }
          })
        Button('pop', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.stack?.pop()
          })
      }
      .width('100%')
      .height('100%')
    }
    .title('pageOne')
    .onReady((ctx: NavDestinationContext) => {
      // 在NavDestination中能够拿到传来的NavPathInfo和当前所处的NavPathStack
      try {
        this.name = ctx?.pathInfo?.name;
        this.paramNum = (ctx?.pathInfo?.param as PageParam)?.num;
        this.stack = ctx.pathStack;
      } catch (e) {
        console.log(`testTag onReady catch exception: ${JSON.stringify(e)}`)
      }
    })
  }
}

@Entry
@Component
struct NavigationExample2 {
  private stack : NavPathStack = new NavPathStack();

  build() {
    Navigation(this.stack) {
      Stack({alignContent: Alignment.Center}) {
        Button('pushPath', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            let p = new PageParam(1);
            this.stack.pushPath({ name: "pageOne", param: p })
          })
      }
      .width('100%')
      .height('100%')
    }
    .width('100%')
    .height('100%')
    .title('Navigation')
  }
}
```
```json
// 工程配置文件module.json5中配置 {"routerMap": "$profile:route_map"}
// route_map.json
{
  "routerMap": [
    {
      "name": "pageOne",
      "pageSourceFile": "src/main/ets/pages/Index.ets",
      "buildFunction": "PageOneBuilder",
      "data": {
        "description": "this is pageOne"
      }
    }
  ]
}
```
![navigationOnReady1.gif](figures/navigationOnReady1.gif)

### 示例8

```ts
// 该示例演示NavDestination的生命周期时序。
@Builder
export function PageOneBuilder(name: string, param: Object) {
  PageOneComponent()
}

@Component
struct PageOneComponent {
  private stack: NavPathStack | null = null;
  @State eventStr: string = "";

  build() {
    NavDestination() {
      Column() {
        Text("event: " + this.eventStr)
        Button('pushPath', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            if (this.stack) {
              this.stack.pushPath({name: "pageOne"});
            }
          })
        Button('pop', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.stack?.pop()
          })
      }
      .width('100%')
      .height('100%')
    }
    .title('pageOne')
    .onAppear(() => { this.eventStr += "<onAppear>"; })
    .onDisAppear(() => { this.eventStr += "<onDisAppear>"; })
    .onShown(() => { this.eventStr += "<onShown>"; })
    .onHidden(() => { this.eventStr += "<onHidden>"; })
    // onReady会在onAppear之前调用
    .onReady((ctx: NavDestinationContext) => {
      try {
        this.eventStr += "<onReady>";
        this.stack = ctx.pathStack;
      } catch (e) {
        console.log(`testTag onReady catch exception: ${JSON.stringify(e)}`)
      }
    })
  }
}

@Entry
@Component
struct NavigationExample3 {
  private stack : NavPathStack = new NavPathStack();

  build() {
    Navigation(this.stack) {
      Stack({alignContent: Alignment.Center}) {
        Button('pushPath', { stateEffect: true, type: ButtonType.Capsule })
          .width('80%')
          .height(40)
          .margin(20)
          .onClick(() => {
            this.stack.pushPath({ name: "pageOne" })
          })
      }
      .width('100%')
      .height('100%')
    }
    .width('100%')
    .height('100%')
    .title('Navigation')
  }
}
```
```json
// 工程配置文件module.json5中配置 {"routerMap": "$profile:route_map"}
// route_map.json
{
  "routerMap": [
    {
      "name": "pageOne",
      "pageSourceFile": "src/main/ets/pages/Index.ets",
      "buildFunction": "PageOneBuilder",
      "data": {
        "description": "this is pageOne"
      }
    }
  ]
}
```
![navigationOnReady2.gif](figures/navigationOnReady2.gif)
