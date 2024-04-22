# TextInput

单行文本输入框组件。

>  **说明：**
>
>  该组件从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 子组件

无


## 接口

TextInput(value?: TextInputOptions)

**参数：**

| 参数名 |类型|必填|说明|
|-----|-----|----|----|
| value | [TextInputOptions](#textinputoptions对象说明) | 否  | TextInput组件参数。 |

## TextInputOptions对象说明
| 参数名                     | 参数类型                                     | 必填   | 参数描述                                     |
| ----------------------- | ---------------------------------------- | ---- | ---------------------------------------- |
| placeholder             | [ResourceStr](ts-types.md#resourcestr)   | 否    | 设置无输入时的提示文本。                             |
| text                    | [ResourceStr](ts-types.md#resourcestr)   | 否    | 设置输入框当前的文本内容。</br>建议通过onChange事件将状态变量与文本实时绑定，</br>避免组件刷新时TextInput中的文本内容异常。<br />从API version 10开始，该参数支持[$$](../../../quick-start/arkts-two-way-sync.md)双向绑定变量。 |
| controller<sup>8+</sup> | [TextInputController](#textinputcontroller8) | 否    | 设置TextInput控制器。                          |

## 属性

除支持[通用属性](ts-universal-attributes-size.md)和[文本通用属性](ts-universal-attributes-text-style.md)的fontColor、fontSize、fontStyle、fontWeight、fontFamily外，还支持以下属性：

### type

type(value: InputType)

设置输入框类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                            | 必填 | 说明                                      |
| ------ | ------------------------------- | ---- | ----------------------------------------- |
| value  | [InputType](#inputtype枚举说明) | 是   | 输入框类型。<br/>默认值：InputType.Normal |

### contentType<sup>12+</sup>

contentType(value: ContentType)

设置自动填充类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型                                  | 必填 | 说明           |
| ------ | ------------------------------------- | ---- | -------------- |
| value  | [ContentType](#contenttype12枚举说明) | 是   | 自动填充类型。 |

### placeholderColor

placeholderColor(value: ResourceColor)

设置placeholder文本颜色。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                       | 必填 | 说明                                         |
| ------ | ------------------------------------------ | ---- | -------------------------------------------- |
| value  | [ResourceColor](ts-types.md#resourcecolor) | 是   | placeholder文本颜色。<br/>默认值：跟随主题。 |

### placeholderFont

placeholderFont(value?: Font)

设置placeholder文本样式，包括字体大小，字体粗细，字体族，字体风格。目前仅支持默认字体族。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                     | 必填 | 说明                  |
| ------ | ------------------------ | ---- | --------------------- |
| value  | [Font](ts-types.md#font) | 否   | placeholder文本样式。 |

### enterKeyType

enterKeyType(value: EnterKeyType)

设置输入法回车键类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                             | 必填 | 说明                                             |
| ------ | ------------------------------------------------ | ---- | ------------------------------------------------ |
| value  | [EnterKeyType](ts-types.md#enterkeytype枚举说明) | 是   | 输入法回车键类型。<br/>默认值：EnterKeyType.Done |

### caretColor

caretColor(value: ResourceColor)

设置输入框光标颜色。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                       | 必填 | 说明                                   |
| ------ | ------------------------------------------ | ---- | -------------------------------------- |
| value  | [ResourceColor](ts-types.md#resourcecolor) | 是   | 输入框光标颜色。<br/>默认值：'#007DFF' |

>  **说明：**     
>   从API version 12开始，此接口支持设置文本手柄颜色，光标和文本手柄颜色保持一致。

### maxLength

maxLength(value: number)

设置文本的最大输入字符数。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| value  | number | 是   | 文本的最大输入字符数。<br/>默认值：Infinity，可以无限输入。<br/>**说明：** <br/>当不设置该属性或设置异常值时，取默认值，设置小数时，取整数部分。 |

### inputFilter<sup>8+</sup>

inputFilter(value: ResourceStr, error?: (value: string) => void)

通过正则表达式设置输入过滤器。匹配表达式的输入允许显示，不匹配的输入将被过滤。仅支持单个字符匹配，不支持字符串匹配。

从API version 11开始，设置inputFilter且输入的字符不为空字符，会导致设置输入框类型(即type接口)附带的文本过滤效果失效。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                   | 必填 | 说明                               |
| ------ | -------------------------------------- | ---- | ---------------------------------- |
| value  | [ResourceStr](ts-types.md#resourcestr) | 是   | 正则表达式。                       |
| error  | (value: string) => void                | 否   | 正则匹配失败时，返回被过滤的内容。 |

### copyOption<sup>9+</sup>

copyOption(value: CopyOptions)

设置输入的文本是否可复制。设置CopyOptions.None时，当前TextInput中的文字无法被复制或剪切，仅支持粘贴。

copyOption对于拖拽，只限制是否选中，不涉及拖拽范围。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                             | 必填 | 说明                                                         |
| ------ | ------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | [CopyOptions](ts-appendix-enums.md#copyoptions9) | 是   | 输入的文本是否可复制。<br/>默认值：CopyOptions.LocalDevice，支持设备内复制。 |

### showPasswordIcon<sup>9+</sup>

showPasswordIcon(value: boolean)

设置当密码输入模式时，输入框末尾的图标是否显示。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                        |
| ------ | ------- | ---- | ----------------------------------------------------------- |
| value  | boolean | 是   | 密码输入模式时，输入框末尾的图标是否显示。<br/>默认值：true |

### style<sup>9+</sup>

style(value: TextInputStyle &nbsp;|&nbsp;TextContentStyle)

设置输入框为默认风格或内联输入风格，内联输入风格只支持InputType.Normal类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | [TextInputStyle](#textinputstyle9枚举说明)&nbsp;\|&nbsp;[TextContentStyle](ts-appendix-enums.md#textcontentstyle10) | 是   | 输入框为默认风格或内联输入风格。<br/>默认值：TextInputStyle.Default |

### textAlign<sup>9+</sup>

textAlign(value: TextAlign)

设置文本在输入框中的水平对齐方式。

仅支持TextAlign.Start、TextAlign.Center和TextAlign.End。

可通过[align](ts-universal-attributes-location.md)属性控制文本段落在垂直方向上的位置，此组件中不可通过align属性控制文本段落在水平方向上的位置，即align属性中Alignment.TopStart、Alignment.Top、Alignment.TopEnd效果相同，控制内容在顶部，Alignment.Start、Alignment.Center、Alignment.End效果相同，控制内容垂直居中，Alignment.BottomStart、Alignment.Bottom、Alignment.BottomEnd效果相同，控制内容在底部。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                        | 必填 | 说明                                                       |
| ------ | ------------------------------------------- | ---- | ---------------------------------------------------------- |
| value  | [TextAlign](ts-appendix-enums.md#textalign) | 是   | 文本在输入框中的水平对齐方式。<br/>默认值：TextAlign.Start |

### selectedBackgroundColor<sup>10+</sup>

selectedBackgroundColor(value: ResourceColor)

设置文本选中底板颜色。如果未设置不透明度，默认为20%不透明度。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                       | 必填 | 说明                                       |
| ------ | ------------------------------------------ | ---- | ------------------------------------------ |
| value  | [ResourceColor](ts-types.md#resourcecolor) | 是   | 文本选中底板颜色。<br/>默认为20%不透明度。 |

### caretStyle<sup>10+</sup>

caretStyle(value: CaretStyle)

设置光标风格。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                | 必填 | 说明         |
| ------ | ----------------------------------- | ---- | ------------ |
| value  | [CaretStyle](#caretstyle10对象说明) | 是   | 光标的风格。 |

### caretPosition<sup>10+</sup>

caretPosition(value: number)

设置光标位置。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明         |
| ------ | ------ | ---- | ------------ |
| value  | number | 是   | 光标的位置。 |

### showUnit<sup>10+</sup>

showUnit(value: CustomBuilder)

设置控件作为文本框单位。需搭配showUnderline使用，当[showUnderline](#showunderline10)为true时生效。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                        | 必填 | 说明                           |
| ------ | ------------------------------------------- | ---- | ------------------------------ |
| value  | [CustomBuilder](ts-types.md#custombuilder8) | 是   | 文本输入时，文本框的显示单位。 |

### showError<sup>10+</sup>

showError(value?: string | undefined)

设置错误状态下提示的错误文本或者不显示错误状态。

当参数类型为string并且输入内容不符合定义规范时，提示错误文本。当参数类型为undefined时，不显示错误状态。请参考[示例2](#示例2)。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                          | 必填 | 说明                                                         |
| ------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| value  | string&nbsp;\|&nbsp;undefined | 否   | 错误状态下提示的错误文本或者不显示错误状态。<br/>默认不显示错误状态。 |

### showUnderline<sup>10+</sup>

showUnderline(value: boolean)

设置是否开启下划线。下划线默认颜色为'#33182431'，默认粗细为1px，文本框尺寸48vp，下划线只支持InputType.Normal类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                               |
| ------ | ------- | ---- | ---------------------------------- |
| value  | boolean | 是   | 是否开启下划线。<br/>默认值：false |

### underlineColor<sup>12+</sup>

underlineColor(value: ResourceColor|UnderlineColor|undefined)

开启下划线时，支持配置下划线颜色。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | [ResourceColor](ts-types.md#resourcecolor) \| [UnderlineColor](#underlinecolor12对象说明) \| undefined | 是   | 设置下划线颜色。<br/>当设置下划线颜色模式时，修改下划线颜色。当只设定非特殊状态下的颜色，可以直接输入ResourceColor。设定值为undefined、null、无效值时，所有下划线恢复为默认值。<br/>默认值：主题配置的下划线颜色。主题配置的默认下滑颜色为'#33182431'。 |

### passwordIcon<sup>10+</sup>

passwordIcon(value: PasswordIcon)

设置当密码输入模式时，输入框末尾的图标。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                    | 必填 | 说明                                                         |
| ------ | --------------------------------------- | ---- | ------------------------------------------------------------ |
| value  | [PasswordIcon](#passwordicon10对象说明) | 是   | 密码输入模式时，输入框末尾的图标。<br/>默认为系统提供的密码图标。 |

### enableKeyboardOnFocus<sup>10+</sup>

enableKeyboardOnFocus(value: boolean)

设置TextInput通过点击以外的方式获焦时，是否绑定输入法。

从API version 10开始，获焦默认绑定输入法。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                        |
| ------ | ------- | ---- | ----------------------------------------------------------- |
| value  | boolean | 是   | 通过点击以外的方式获焦时，是否绑定输入法。<br/>默认值：true |

### selectionMenuHidden<sup>10+</sup>

selectionMenuHidden(value: boolean)

设置长按、双击输入框或者右键输入框时，是否不弹出文本选择菜单。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| value  | boolean | 是   | 长按、双击输入框或者右键输入框时，是否不弹出文本选择菜单。<br />默认值：false |

### barState<sup>10+</sup>

barState(value: BarState)

设置内联输入风格编辑态时滚动条的显示模式。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                      | 必填 | 说明                                                         |
| ------ | ----------------------------------------- | ---- | ------------------------------------------------------------ |
| value  | [BarState](ts-appendix-enums.md#barstate) | 是   | 内联输入风格编辑态时滚动条的显示模式。<br/>默认值：BarState.Auto |

### maxLines<sup>10+</sup>

maxLines(value: number)

设置内联输入风格编辑态时文本可显示的最大行数。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                      | 必填 | 说明                                                         |
| ------ | ----------------------------------------- | ---- | ------------------------------------------------------------ |
| value  | number | 是   | 内联输入风格编辑态时文本可显示的最大行数。<br/>默认值：3 <br/>取值范围：(0, +∞) |

### customKeyboard<sup>10+</sup>

customKeyboard(value: CustomBuilder, options?: KeyboardOptions)

设置自定义键盘。

当设置自定义键盘时，输入框激活后不会打开系统输入法，而是加载指定的自定义组件。

自定义键盘的高度可以通过自定义组件根节点的height属性设置，宽度不可设置，使用系统默认值。

自定义键盘采用覆盖原始界面的方式呈现，不会对应用原始界面产生压缩或者上提。

自定义键盘无法获取焦点，但是会拦截手势事件。

默认在输入控件失去焦点时，关闭自定义键盘，开发者也可以通过[TextInputController](#textinputcontroller8).[stopEditing](#stopediting10)方法控制键盘关闭。

如果设备支持拍摄输入，设置自定义键盘后，该输入框会不支持拍摄输入。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名                | 类型                                        | 必填 | 说明                             |
| --------------------- | ------------------------------------------- | ---- | -------------------------------- |
| value                 | [CustomBuilder](ts-types.md#custombuilder8) | 是   | 自定义键盘。                     |
| options<sup>12+</sup> | [KeyboardOptions](#keyboardoptions12)       | 否   | 设置自定义键盘是否支持避让功能。 |

### enableAutoFill<sup>11+</sup>

enableAutoFill(value: boolean)

设置是否启用自动填充。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| value  | boolean | 是   | 是否启用自动填充。<br/>true表示启用，false表示不启用。<br/>默认值：true |

### passwordRules<sup>11+</sup>

passwordRules(value: string)

定义生成密码的规则。在触发自动填充时，所设置的密码规则会透传给密码保险箱，用于新密码的生成。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                 |
| ------ | ------ | ---- | -------------------- |
| value  | string | 是   | 定义生成密码的规则。 |

### cancelButton<sup>11+</sup>

cancelButton(value: { style?: CancelButtonStyle, icon?: IconOptions })

设置右侧清除按钮样式。不支持内联模式。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | {<br/>style? : [CancelButtonStyle](ts-basic-components-search.md#cancelbuttonstyle10枚举说明)<br/>icon?: [IconOptions](ts-basic-components-search.md#iconoptions10对象说明) <br/>} | 是   | 右侧清除按钮样式。<br />默认值：<br />{<br />style: CancelButtonStyle.INPUT<br />} |

### selectAll<sup>11+</sup>

selectAll(value: boolean)

设置当初始状态，是否全选文本。不支持内联模式。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                              |
| ------ | ------- | ---- | --------------------------------- |
| value  | boolean | 是   | 是否全选文本。<br />默认值：false |

### showCounter<sup>11+</sup>

showCounter(value: boolean, options?: InputCounterOptions)

设置当通过InputCounterOptions输入的字符数超过阈值时显示计数器。

参数value为true时，才能设置options，文本框开启计数下标功能，需要配合maxLength（设置最大字符限制）一起使用。字符计数器显示的效果是当前输入字符数/最大可输入字符数。

当输入字符数大于最大字符数乘百分比值时，显示字符计数器。如果用户设置计数器时不设置InputCounterOptions，那么当前输入字符数达到最大字符数时，边框和计数器下标将变为红色。用户同时设置参数value为true和InputCounterOptions，当thresholdPercentage数值在有效区间内，且输入字符数超过最大字符数时，边框和计数器下标将变为红色，框体抖动。highlightBorder设置为false，则不显示红色边框，计数器默认显示红色边框。

TextInput组件显示边框需要设置为下划线模式，内联模式和密码模式下字符计数器不显示。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名                | 类型                                                  | 必填 | 说明             |
| --------------------- | ----------------------------------------------------- | ---- | ---------------- |
| value                 | boolean                                               | 是   | 是否显示计数器。 |
| options<sup>11+</sup> | [InputCounterOptions](#inputcounteroptions11对象说明) | 否   | 计数器的百分比。 |

>  **说明：**    
>  默认情况下，通用属性[padding](ts-universal-attributes-size.md#padding)的默认值为：<br>{<br>&nbsp;top: 8 vp,<br>&nbsp;right: 16 vp,<br>&nbsp;bottom: 8 vp,<br>&nbsp;left: 16 vp<br> } 
>  
>  输入框开启下划线模式时，通用属性padding的默认值为：<br>{<br>&nbsp;top: 12 vp,<br>&nbsp;right: 0 vp,<br>&nbsp;bottom: 12 vp,<br>&nbsp;left: 0 vp<br> }
>
>   从API version 10开始，单行输入框可设置.width('auto')使组件宽度自适应文本宽度，自适应时组件宽度受constraintSize属性以及父容器传递的最大最小宽度限制，其余使用方式参考[尺寸设置](ts-universal-attributes-size.md#属性)。

### lineHeight<sup>12+</sup>

lineHeight(value: number | string | Resource)

设置文本的文本行高，设置值不大于0时，不限制文本行高，自适应字体大小，number类型时单位为fp。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型                                                         | 必填 | 说明             |
| ------ | ------------------------------------------------------------ | ---- | ---------------- |
| value  | number&nbsp;\|&nbsp;string&nbsp;\|&nbsp;[Resource](ts-types.md#resource) | 是   | 文本的文本行高。 |

### decoration<sup>12+</sup>

decoration(value: TextDecorationOptions)

设置文本装饰线样式及其颜色。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | [TextDecorationOptions](#textdecorationoptions12对象说明) | 是   | 文本装饰线样式及其颜色。<br />默认值：{<br/>type:&nbsp;TextDecorationType.None,<br/>color：Color.Black<br/>} |

### letterSpacing<sup>12+</sup>

letterSpacing(value: number | string | Resource)

设置文本字符间距。设置该值为百分比时，按默认值显示。设置该值为0时，按默认值显示。

当取值为负值时，文字会发生压缩，负值过小时会将组件内容区大小压缩为0，导致无内容显示。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型                       | 必填 | 说明           |
| ------ | -------------------------- | ---- | -------------- |
| value  | number&nbsp;\|&nbsp;string&nbsp;\|&nbsp;[Resource](ts-types.md#resource) | 是   | 文本字符间距。 |

### fontFeature<sup>12+</sup>

fontFeature(value: string)

设置文字特性效果，比如数字等宽的特性。

格式为：normal \| \<feature-tag-value\>

\<feature-tag-value\>的格式为：\<string\> \[ \<integer\> \| on \| off ]

\<feature-tag-value\>的个数可以有多个，中间用','隔开。

例如，使用等宽数字的输入格式为："ss01" on。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明           |
| ------ | ------ | ---- | -------------- |
| value  | string | 是   | 文字特性效果。 |

设置 Font Feature 属性，Font Feature 是 OpenType 字体的高级排版能力，如支持连字、数字等宽等特性，一般用在自定义字体中，其能力需要字体本身支持。
更多 Font Feature 能力介绍可参考 https://www.w3.org/TR/css-fonts-3/#font-feature-settings-prop 和 https://sparanoid.com/lab/opentype-features/

>  **说明：**
>  type属性中InputType枚举为Password、NEW_PASSWORD和NUMBER_PASSWORD等密码模式时，暂时不支持fontFeature设置文本样式。

### wordBreak<sup>12+</sup>

wordBreak(value: WordBreak)

设置文本断行规则。该属性在组件设置内联模式时样式生效，但对placeholder文本无效。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                          | 必填 | 说明                                          |
| ------ | --------------------------------------------- | ---- | --------------------------------------------- |
| value  | [WordBreak](ts-appendix-enums.md#wordbreak11) | 是   | 内联输入风格编辑态时断行规则。 <br />默认值：WordBreak.BREAK_WORD |

>  **说明：**
>
>  组件不支持clip属性设置，设置该属性任意枚举值对组件文本截断无影响。

### textOverflow<sup>12+</sup>

textOverflow(value: TextOverflow)

设置文本超长时的显示方式。仅在内联模式的编辑态、非编辑态下支持。

文本截断是按字截断。例如，英文以单词为最小单位进行截断，若需要以字母为单位进行截断，可在字母间添加零宽空格：\u200B。建议优先组合wordBreak属性设置为WordBreak.BREAK_ALL方式实现字母为单位进行截断。

当overflow设置TextOverflow.None与TextOverflow.Clip效果一样。

**卡片能力：** 该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                          | 必填 | 说明                                                                                                |
| ------ | ------------------------------------------------------------ | ---- | -------------------------------------------------------------------------------------------------- |
| value  | [TextOverflow](ts-appendix-enums.md#textoverflow)            | 是   | 文本超长时的显示方式。<br/>内联模式编辑态下默认值：TextOverflow.Ellipsis <br/>内联模式编辑态下默认值：TextOverflow.Clip                     |

>  **说明：**  
>   TextInput组件不支持设置TextOverflow.MARQUEE模式,当设置为TextOverflow.MARQUEE模式时 内联模式非编辑态下显示为TextOverflow.Ellipsis，内联模式编辑态下以及非内联模式下显示为TextOverflow.Clip

### textIndent<sup>12+</sup>

textIndent(value: Dimension)

设置首行文本缩进。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                  | 必填 | 说明                         |
| ------ | ------------------------------------ | ---- | ---------------------------- |
| value  | [Dimension](ts-types.md#dimension10) | 是   | 首行文本缩进。<br/>默认值：0 |

### minFontSize<sup>12+</sup>

minFontSize(value: number | string | Resource)

设置文本最小显示字号。

需配合[maxFontSize](#maxfontsize12)以及[maxLines](#maxlines10)(组件设置为内联输入风格且编辑态时使用)或布局大小限制使用，单独设置不生效。

自适应字号生效时，fontSize设置不生效。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型                                                         | 必填 | 说明               |
| ------ | ------------------------------------------------------------ | ---- | ------------------ |
| value  | number&nbsp;\|&nbsp;string&nbsp;\|&nbsp;[Resource](ts-types.md#resource) | 是   | 文本最小显示字号。 |

### maxFontSize<sup>12+</sup>

maxFontSize(value: number | string | Resource)

设置文本最大显示字号。

需配合[minFontSize](#minfontsize12)以及[maxLines](#maxlines10)(组件设置为内联输入风格且编辑态时使用)或布局大小限制使用，单独设置不生效。

自适应字号生效时，fontSize设置不生效。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型                                                         | 必填 | 说明               |
| ------ | ------------------------------------------------------------ | ---- | ------------------ |
| value  | number&nbsp;\|&nbsp;string&nbsp;\|&nbsp;[Resource](ts-types.md#resource) | 是   | 文本最大显示字号。 |

### heightAdaptivePolicy<sup>12+</sup>

heightAdaptivePolicy(value: TextHeightAdaptivePolicy)

设置文本自适应高度的方式。

当设置为TextHeightAdaptivePolicy.MAX_LINES_FIRST时，优先使用[maxLines](#maxlines10)属性(组件设置为内联输入风格且编辑态时使用)来调整文本高度。如果使用maxLines属性的布局大小超过了布局约束，则尝试在[minFontSize](#minfontsize12)和[maxFontSize](#maxfontsize12)的范围内缩小字体以显示更多文本。
组件设置为内联输入风格，编辑态与非编辑态存在字体大小不一致情况。

当设置为TextHeightAdaptivePolicy.MIN_FONT_SIZE_FIRST时，优先使用minFontSize属性来调整文本高度。如果使用minFontSize属性可以将文本布局在一行中，则尝试在minFontSize和maxFontSize的范围内增大字体并使用最大可能的字体大小。

当设置为TextHeightAdaptivePolicy.LAYOUT_CONSTRAINT_FIRST时，优先使用布局约束来调整文本高度。如果布局大小超过布局约束，则尝试在minFontSize和maxFontSize的范围内缩小字体以满足布局约束。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | [TextHeightAdaptivePolicy](ts-appendix-enums.md#textheightadaptivepolicy10) | 是   | 文本自适应高度的方式。<br/>默认值：TextHeightAdaptivePolicy.MAX_LINES_FIRST |

## CaretStyle<sup>10+</sup>对象说明
| 参数名 | 类型  | 必填 | 说明  |
| ------ | -------- | ---- | ------------------------------------------- |
| width  | [Length](ts-types.md#length) | 否  | 光标尺寸，不支持百分比设置。 |

## TextDecorationOptions<sup>12+</sup>对象说明

| 名称    | 参数类型                                                    | 必填 | 描述                                                         |
| ------- | ----------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| type  | [TextDecorationType](ts-appendix-enums.md#textdecorationtype) | 是   | 设置文本装饰线样式。 |
| color  | &nbsp;[ResourceColor](ts-types.md#resourcecolor) | 否   | 设置文本装饰线颜色。 |

## InputType枚举说明

| 名称                                 | 描述                                       |
| ---------------------------------- | ---------------------------------------- |
| Normal                             | 基本输入模式，无特殊限制。                            |
| Password                           | 密码输入模式。支持输入数字、字母、下划线、空格、特殊字符。密码显示小眼睛图标，默认输入文字短暂显示后变成圆点，特定设备上输入文字直接显示为圆点。密码输入模式不支持下划线样式。在已启用密码保险箱的情况下，支持用户名、密码的自动保存和自动填充。 |
| Email                              | 邮箱地址输入模式。支持数字，字母，下划线，小数点，以及@字符（只能存在一个@字符）。 |
| Number                             | 纯数字输入模式。                                 |
| PhoneNumber<sup>9+</sup>           | 电话号码输入模式。<br/>支持输入数字、空格、+ 、-、*、#、(、)，长度不限。      |
| USER_NAME<sup>11+<sup>             | 用户名输入模式。在已启用密码保险箱的情况下，支持用户名、密码的自动保存和自动填充。                |
| NEW_PASSWORD<sup>11+<sup>          | 新密码输入模式。密码显示小眼睛图标，默认输入文字短暂显示后变成圆点，特定设备上输入文字直接显示为圆点。在已启用密码保险箱的情况下，支持自动生成新密码。                                 |
| NUMBER_PASSWORD<sup>11+</sup>      | 纯数字密码输入模式。密码显示小眼睛图标，默认输入文字短暂显示后变成圆点，特定设备上输入文字直接显示为圆点。密码输入模式不支持下划线样式。 |
| NUMBER_DECIMAL<sup>11+</sup>       | 带小数点的数字输入模式。支持数字，小数点（只能存在一个小数点）。         |

## ContentType<sup>12+</sup>枚举说明

自动填充类型。

| 名称                       | 值   | 描述                                                         |
| -------------------------- | ---- | ------------------------------------------------------------ |
| USER_NAME                  | 0    | 【用户名】在已启用密码保险箱的情况下，支持用户名的自动保存和自动填充。 |
| PASSWORD                   | 1    | 【密码】在已启用密码保险箱的情况下，支持密码的自动保存和自动填充。 |
| NEW_PASSWORD               | 2    | 【新密码】在已启用密码保险箱的情况下，支持自动生成新密码。   |
| FULL_STREET_ADDRESS        | 3    | 【详细地址】在已启用情景化自动填充的情况下，支持详细地址的自动保存和自动填充。 |
| HOUSE_NUMBER               | 4    | 【门牌号】在已启用情景化自动填充的情况下，支持门牌号的自动保存和自动填充。 |
| DISTRICT_ADDRESS           | 5    | 【区/县】在已启用情景化自动填充的情况下，支持区/县的自动保存和自动填充。 |
| CITY_ADDRESS               | 6    | 【市】在已启用情景化自动填充的情况下，支持市的自动保存和自动填充。 |
| PROVINCE_ADDRESS           | 7    | 【省】在已启用情景化自动填充的情况下，支持省的自动保存和自动填充。 |
| COUNTRY_ADDRESS            | 8    | 【国家】在已启用情景化自动填充的情况下，支持国家的自动保存和自动填充。 |
| PERSON_FULL_NAME           | 9    | 【姓名】在已启用情景化自动填充的情况下，支持姓名的自动保存和自动填充。 |
| PERSON_LAST_NAME           | 10   | 【姓氏】在已启用情景化自动填充的情况下，支持姓氏的自动保存和自动填充。 |
| PERSON_FIRST_NAME          | 11   | 【名字】在已启用情景化自动填充的情况下，支持名字的自动保存和自动填充。 |
| PHONE_NUMBER               | 12   | 【手机号】在已启用情景化自动填充的情况下，支持手机号的自动保存和自动填充。 |
| PHONE_COUNTRY_CODE         | 13   | 【国家代码】在已启用情景化自动填充的情况下，支持国家代码的自动保存和自动填充。 |
| FULL_PHONE_NUMBER          | 14   | 【包含国家代码的手机号】在已启用情景化自动填充的情况下，支持包含国家代码的手机号的自动保存和自动填充。 |
| EMAIL_ADDRESS              | 15   | 【邮箱地址】在已启用情景化自动填充的情况下，支持邮箱地址的自动保存和自动填充。 |
| BANK_CARD_NUMBER           | 16   | 【银行卡号】在已启用情景化自动填充的情况下，支持银行卡号的自动保存和自动填充。 |
| ID_CARD_NUMBER             | 17   | 【身份证号】在已启用情景化自动填充的情况下，支持身份证号的自动保存和自动填充。 |
| NICKNAME                   | 23   | 【昵称】在已启用情景化自动填充的情况下，支持昵称的自动保存和自动填充。 |
| DETAIL_INFO_WITHOUT_STREET | 24   | 【无街道地址】在已启用情景化自动填充的情况下，支持无街道地址的自动保存和自动填充。 |
| FORMAT_ADDRESS             | 25   | 【标准地址】在已启用情景化自动填充的情况下，支持标准地址的自动保存和自动填充。 |

## TextInputStyle<sup>9+</sup>枚举说明

| 名称      | 描述                                       |
| ------- | ---------------------------------------- |
| Default | 默认风格，光标宽1.5vp，光标高度与文本选中底板高度和字体大小相关。      |
| Inline  | 内联输入风格。文本选中底板高度与输入框高度相同。<br/>内联输入是在有明显的编辑态/非编辑态的区分场景下使用，例如：文件列表视图中的重命名。<br/>不支持showError属性。 |

## PasswordIcon<sup>10+</sup>对象说明

| 名称         | 类型                                       | 必填   | 描述                        |
| ---------- | ---------------------------------------- | ---- | ------------------------- |
| onIconSrc  | string&nbsp;\|&nbsp;[Resource](ts-types.md#resource类型) | 否    | 密码输入模式时，能够切换密码隐藏的显示状态的图标。 |
| offIconSrc | string&nbsp;\|&nbsp;[Resource](ts-types.md#resource类型) | 否    | 密码输入模式时，能够切换密码显示的隐藏状态的图标。 |

## 事件

除支持[通用事件](ts-universal-events-click.md)外，还支持以下事件：

### onChange

onChange(callback:&nbsp;(value:&nbsp;string)&nbsp;=&gt;&nbsp;void)

输入内容发生变化时，触发该回调。

触发该事件的条件：

1、键盘输入。

2、粘贴、剪切。

3、键盘快捷键Ctrl+v。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                 |
| ------ | ------ | ---- | -------------------- |
| value  | string | 是   | 当前输入的文本内容。 |

### onSubmit

onSubmit(callback:&nbsp;(enterKey:&nbsp;EnterKeyType,&nbsp;event:&nbsp;SubmitEvent&nbsp;=&gt;&nbsp;void)

按下输入法回车键触发该回调。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名              | 类型                                             | 必填 | 说明                                                         |
| ------------------- | ------------------------------------------------ | ---- | ------------------------------------------------------------ |
| enterKey            | [EnterKeyType](ts-types.md#enterkeytype枚举说明) | 是   | 输入法回车键类型，类型为EnterKeyType.NEW_LINE时不触发onSubmit。 |
| event<sup>11+</sup> | [SubmitEvent](ts-types.md#submitevent11)         | 是   | 提交事件。                                                   |

### onEditChanged<sup>(deprecated)</sup>

onEditChanged(callback:&nbsp;(isEditing:&nbsp;boolean)&nbsp;=&gt;&nbsp;void)

输入状态变化时，触发该回调。

从API 8开始废弃，建议使用onEditChange。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名    | 类型    | 必填 | 说明                 |
| --------- | ------- | ---- | -------------------- |
| isEditing | boolean | 是   | 为true表示正在输入。 |

### onEditChange<sup>8+</sup>

onEditChange(callback:&nbsp;(isEditing:&nbsp;boolean)&nbsp;=&gt;&nbsp;void)

输入状态变化时，触发该回调。有光标时为编辑态，无光标时为非编辑态。isEditing为true表示正在输入。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名    | 类型    | 必填 | 说明                 |
| --------- | ------- | ---- | -------------------- |
| isEditing | boolean | 是   | 为true表示正在输入。 |

### onCopy<sup>8+</sup>

onCopy(callback:(value:&nbsp;string)&nbsp;=&gt;&nbsp;void)

长按输入框内部区域弹出剪贴板后，点击剪切板复制按钮，触发该回调。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名    | 类型    | 必填 | 说明             |
| --------- | ------- | ---- | ---------------- |
| value | string | 是   | 复制的文本内容。 |

### onCut<sup>8+</sup>

onCut(callback:(value:&nbsp;string)&nbsp;=&gt;&nbsp;void)

长按输入框内部区域弹出剪贴板后，点击剪切板剪切按钮，触发该回调。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名    | 类型    | 必填 | 说明             |
| --------- | ------- | ---- | ---------------- |
| value | string | 是   | 剪切的文本内容。 |

### onPaste

onPaste(callback:(value:&nbsp;string, event:&nbsp;PasteEvent)&nbsp;=&gt;&nbsp;void)

长按输入框内部区域弹出剪贴板后，点击剪切板粘贴按钮，触发该回调。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名              | 类型                                                         | 必填 | 说明                   |
| ------------------- | ------------------------------------------------------------ | ---- | ---------------------- |
| value               | string                                                       | 是   | 粘贴的文本内容。       |
| event<sup>11+</sup> | [PasteEvent](ts-basic-components-richeditor.md#pasteevent11) | 否   | 用户自定义的粘贴事件。 |

### onTextSelectionChange<sup>10+</sup>

onTextSelectionChange(callback: (selectionStart: number, selectionEnd: number) => void)

文本选择的位置发生变化时，触发该回调。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名         | 类型   | 必填 | 说明                                    |
| -------------- | ------ | ---- | --------------------------------------- |
| selectionStart | number | 是   | 所选文本的起始位置，文字的起始位置为0。 |
| selectionEnd   | number | 是   | 所选文本的结束位置。                    |

### onContentScroll<sup>10+</sup>

onContentScroll(callback: (totalOffsetX: number, totalOffsetY: number) => void)

文本内容滚动时，触发该回调。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名       | 类型   | 必填 | 说明                               |
| ------------ | ------ | ---- | ---------------------------------- |
| totalOffsetX | number | 是   | 文本在内容区的横坐标偏移，单位px。 |
| totalOffsetY | number | 是   | 文本在内容区的纵坐标偏移，单位px。 |

## TextInputController<sup>8+</sup>

TextInput组件的控制器。

### 导入对象
```
controller: TextInputController = new TextInputController()
```
### caretPosition<sup>8+</sup>

caretPosition(value:&nbsp;number): void

设置输入光标的位置。

**参数：**

| 参数名   | 参数类型   | 必填   | 参数描述                |
| ----- | ------ | ---- | ------------------- |
| value | number | 是    | 从字符串开始到光标所在位置的字符长度。 |
### setTextSelection<sup>10+</sup>

setTextSelection(selectionStart:&nbsp;number, selectionEnd:&nbsp;number, options?:&nbsp;SelectionOptions): void

设置文本选择区域并高亮显示。

**参数：**

| 参数名            | 参数类型   | 必填   | 参数描述                      |
| -------------- | ------ | ---- | ------------------------- |
| selectionStart | number | 是    | 文本选择区域起始位置，文本框中文字的起始位置为0。 |
| selectionEnd   | number | 是    | 文本选择区域结束位置。               |
| options<sup>12+</sup>   | [SelectionOptions](#selectionoptions12) | 否    | 选中文字时的配置。<br />默认值：MenuPolicy.DEFAULT。 |
>  **说明：**
>
>  如果selectionStart或selectionEnd被赋值为undefined时，当作0处理。
>
>  如果selectionMenuHidden被赋值为true或设备为2in1时，即使options被赋值为MenuPolicy.ALWAYS，调用setTextSelection也不弹出菜单。

### stopEditing<sup>10+</sup>

stopEditing(): void

退出编辑态。

### getTextContentRect<sup>10+</sup>

getTextContentRect(): [RectResult](#rectresult10)

获取已编辑文本内容区域相对组件的位置和大小，返回值单位为像素。

**返回值：**

| 类型                          | 说明                  |
| --------------------------- | ------------------- |
| [RectResult](#rectresult10) | 已编辑文本内容的相对组件的位置和大小。 |

> **说明：**
>
> - 初始不输入文本时，返回值中有相对组件的位置信息，大小为0。
> - 返回值中的位置信息是第一个字符相对于可编辑组件的位置。

### RectResult<sup>10+</sup>

位置和大小，单位均为像素。

| 参数     | 类型     | 描述       |
| ------ | ------ | -------- |
| x      | number | 水平方向横坐标。 |
| y      | number | 竖直方向纵坐标。 |
| width  | number | 内容宽度大小。  |
| height | number | 内容高度大小。  |


### getTextContentLineCount<sup>10+</sup>

getTextContentLineCount(): number

获取已编辑文本内容的行数。

**返回值：**

| 类型     | 说明         |
| ------ | ---------- |
| number | 已编辑文本内容行数。 |
### getCaretOffset<sup>11+</sup>

getCaretOffset(): CaretOffset

返回当前光标所在位置信息。

**返回值：**

| 类型                                | 说明          |
| --------------------------------- | ----------- |
| [CaretOffset](#caretoffset11对象说明) | 光标相对输入框的位置。 |

> **说明：**
>
> - 在当前帧更新光标位置同时调用该接口，该接口不生效。

## CaretOffset<sup>11+</sup>对象说明
| 参数名   | 类型     | 描述             |
| ----- | ------ | -------------- |
| index | number | 光标所在位置的索引值。    |
| x     | number | 光标相对输入框的x坐标位值，单位px。 |
| y     | number | 光标相对输入框的y坐标位值，单位px。 |

## InputCounterOptions<sup>11+</sup>对象说明

| 参数名              | 类型    | 描述                                                         |
| ------------------- | ------- | ------------------------------------------------------------ |
| thresholdPercentage | number  | thresholdPercentage是可输入字符数占最大字符限制的百分比值。字符计数器显示的样式为当前输入字符数/最大字符数。当输入字符数大于最大字符数乘百分比值时，显示字符计数器。thresholdPercentage值的有效值区间为[1,100]，数值为小数时，向下取整，如果设置的number超出有效值区间内，不显示字符计数器。thresholdPercentage设置为undefined，显示字符计数器，但此参数不生效。 |
| highlightBorder     | boolean | 如果用户设置计数器时不设置InputCounterOptions，那么当前输入字符数达到最大字符数时，边框和计数器下标将变为红色。如果用户设置显示字符计数器同时thresholdPercentage参数数值在有效区间内，那么当输入字符数超过最大字符数时，边框和计数器下标将变成红色。如果此参数为true，则显示红色边框。计数器默认显示红色边框。 |

## SelectionOptions<sup>12+</sup>

setTextSelection选中文字时的配置。

| 名称       | 类型                        | 必填 | 说明             |
| ---------- | --------------------------- | ---- | ---------------- |
| menuPolicy | [MenuPolicy](#menupolicy12) | 否   | 菜单弹出的策略。 |

## MenuPolicy<sup>12+</sup>

菜单弹出的策略。

| 名称    | 描述                     |
| ------- | ------------------------ |
| DEFAULT | 按照底层默认逻辑决定是否弹出菜单。 |
| NEVER   | 始终不弹出菜单。         |
| ALWAYS  | 始终弹出菜单。           |

## UnderlineColor<sup>12+</sup>对象说明

| 参数名  | 类型                                                         | 必填 | 描述                                                         |
| ------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| typing  | [ResourceColor](ts-types.md#resourcecolor) \| undefined | 否   | 键入时下划线颜色。不填写、undefined、null、无效值时恢复默认。 |
| normal  | [ResourceColor](ts-types.md#resourcecolor) \| undefined | 否   | 非特殊状态时下划线颜色。不填写、undefined、null、无效值时恢复默认。 |
| error   | [ResourceColor](ts-types.md#resourcecolor) \| undefined | 否   | 错误时下划线颜色。不填写、undefined、null、无效值时恢复默认。此选项会修改showCounter属性中达到最大字符数时的颜色。 |
| disable | [ResourceColor](ts-types.md#resourcecolor) \| undefined | 否   | 禁用时下划线颜色。不填写、undefined、null、无效值时恢复默认。 |

## KeyboardOptions<sup>12+</sup>

设置自定义键盘是否支持避让功能。

| 名称            | 类型              | 必填   | 描述                               |
| --------------- | ---------------  |---- | ------------------------------------  |
| supportAvoidance |  boolean      | 否 | 设置自定义键盘是否支持避让功能；默认值为false不支持避让，true为支持避让。 |

## 示例

### 示例1

```ts
// xxx.ets
@Entry
@Component
struct TextInputExample {
  @State text: string = ''
  @State positionInfo: CaretOffset = { index: 0, x: 0, y: 0 }
  controller: TextInputController = new TextInputController()

  build() {
    Column() {
      TextInput({ text: this.text, placeholder: 'input your word...', controller: this.controller })
        .placeholderColor(Color.Grey)
        .placeholderFont({ size: 14, weight: 400 })
        .caretColor(Color.Blue)
        .width('95%')
        .height(40)
        .margin(20)
        .fontSize(14)
        .fontColor(Color.Black)
        .inputFilter('[a-z]', (e) => {
          console.log(JSON.stringify(e))
        })
        .onChange((value: string) => {
          this.text = value
        })
      Text(this.text)
      Button('Set caretPosition 1')
        .margin(15)
        .onClick(() => {
          // 将光标移动至第一个字符后
          this.controller.caretPosition(1)
        })
      Button('Get CaretOffset')
        .margin(15)
        .onClick(() => {
          this.positionInfo = this.controller.getCaretOffset()
        })
      // 密码输入框
      TextInput({ placeholder: 'input your password...' })
        .width('95%')
        .height(40)
        .margin(20)
        .type(InputType.Password)
        .maxLength(9)
        .showPasswordIcon(true)
      // 邮箱地址自动填充类型
      TextInput({ placeholder: 'input your email...' })
        .width('95%')
        .height(40)
        .margin(20)
        .contentType(ContentType.EMAIL_ADDRESS)
        .maxLength(9)
      // 内联风格输入框
      TextInput({ text: 'inline style' })
        .width('95%')
        .height(50)
        .margin(20)
        .borderRadius(0)
        .style(TextInputStyle.Inline)
    }.width('100%')
  }
}
```

![TextInput](figures/TextInput.png)

### 示例2

```ts
@Entry
@Component
struct TextInputExample {
  @State PassWordSrc1: Resource = $r('app.media.onIcon')
  @State PassWordSrc2: Resource = $r('app.media.offIcon')
  @State TextError: string = ''
  @State Text: string = ''
  @State NameText: string = 'test'

  @Builder itemEnd() {
    Select([{ value: 'KB' },
      { value: 'MB' },
      { value: 'GB' },
      { value: 'TB', }])
      .height("48vp")
      .borderRadius(0)
      .selected(2)
      .align(Alignment.Center)
      .value('MB')
      .font({ size: 20, weight: 500 })
      .fontColor('#182431')
      .selectedOptionFont({ size: 20, weight: 400 })
      .optionFont({ size: 20, weight: 400 })
      .backgroundColor(Color.Transparent)
      .responseRegion({ height: "40vp", width: "80%", x: '10%', y: '6vp' })
      .onSelect((index: number) => {
        console.info('Select:' + index)
      })
  }

  build() {
    Column({ space: 20 }) {
      // 自定义密码显示图标
      TextInput({ placeholder: 'user define password icon' })
        .type(InputType.Password)
        .width(380)
        .height(60)
        .passwordIcon({ onIconSrc: this.PassWordSrc1, offIconSrc: this.PassWordSrc2 })
      // 下划线模式
      TextInput({ placeholder: 'underline style' })
        .showUnderline(true)
        .width(380)
        .height(60)
        .showError('Error')
        .showUnit(this.itemEnd)

      Text(`用户名：${this.Text}`)
        .width('95%')
      TextInput({ placeholder: '请输入用户名', text: this.Text })
        .showUnderline(true)
        .width(380)
        .showError(this.TextError)
        .onChange((value: string) => {
          this.Text = value
        })
        .onSubmit(() => { // 用户名不正确会清空输入框和用户名并提示错误文本
          if (this.Text == this.NameText) {
            this.TextError = ''
          } else {
            this.TextError = '用户名输入错误'
            this.Text = ''
          }
        })

    }.width('100%')
  }
}
```

![TextInputError](figures/TextInputError.png)

### 示例3

```ts
// xxx.ets
@Entry
@Component
struct TextInputExample {
  controller: TextInputController = new TextInputController()
  @State inputValue: string = ""

  // 自定义键盘组件
  @Builder CustomKeyboardBuilder() {
    Column() {
      Button('x').onClick(() => {
        // 关闭自定义键盘
        this.controller.stopEditing()
      })
      Grid() {
        ForEach([1, 2, 3, 4, 5, 6, 7, 8, 9, '*', 0, '#'], (item:number|string) => {
          GridItem() {
            Button(item + "")
              .width(110).onClick(() => {
              this.inputValue += item
            })
          }
        })
      }.maxCount(3).columnsGap(10).rowsGap(10).padding(5)
    }.backgroundColor(Color.Gray)
  }

  build() {
    Column() {
      TextInput({ controller: this.controller, text: this.inputValue })
        // 绑定自定义键盘
        .customKeyboard(this.CustomKeyboardBuilder()).margin(10).border({ width: 1 }).height('48vp')
    }
  }
}
```

![customKeyboard](figures/textInputCustomKeyboard.png)


### 示例4

```ts
// xxx.ets
@Entry
@Component
struct ClearNodeExample {
  @State text: string = ''
  controller: TextInputController = new TextInputController()

  build() {
    Column() {
      TextInput({ placeholder: 'input ...', controller: this.controller })
        .width(380)
        .height(60)
        .cancelButton({
          style: CancelButtonStyle.CONSTANT,
          icon: {
            size: 45,
            src: $r('app.media.icon'),
            color: Color.Blue
          }
        })
        .onChange((value: string) => {
          this.text = value
        })
    }
  }
}
```

![cancelButton](figures/TextInputCancelButton.png)

### 示例5

```ts
// xxx.ets
@Entry
@Component
struct TextInputExample {
  @State text: string = ''
  controller: TextInputController = new TextInputController()

  build() {
    Column() {
      TextInput({ text: this.text, controller: this.controller })
        .placeholderFont({ size: 16, weight: 400 })
        .width(336)
        .height(56)
        .maxLength(6)
        .showUnderline(true)
		.showCounter(true, { thresholdPercentage: 50, highlightBorder: true })
		//计数器显示效果为用户当前输入字符数/最大字符限制数。最大字符限制数通过maxLength()接口设置。
        //如果用户当前输入字符数达到最大字符限制乘50%（thresholdPercentage）。字符计数器显示。
        //用户设置highlightBorder为false时，配置取消红色边框。不设置此参数时，默认为true。
        .onChange((value: string) => {
          this.text = value
        })
    }.width('100%').height('100%').backgroundColor('#F1F3F5')
  }
}
```

![TextInputCounter](figures/TextInputShowCounter.jpg)


### 示例6
本示例展示如何在TextInput上将电话号码格式化为XXX XXXX XXXX
```ts
@Entry
@Component
struct phone_example {
  @State submitValue: string = ''
  @State text : string = ''

  public readonly NUM_TEXT_MAXSIZE_LENGTH = 14;

  isEmpty(str?: string): boolean {
    return str == 'undefined' || !str || !new RegExp("[^\\s]").test(str);
  }

  checkNeedNumberSpace(numText: string) {
    let isSpace: RegExp = new RegExp('[\\+;,#\\*]', 'g');
    let isRule: RegExp = new RegExp('^\\+.*');

    if (isSpace.test(numText)) {
      // 如果电话号码里有特殊字符，就不加空格
      if (isRule.test(numText)) {
        return true;
      } else {
        return false;
      }
    }
    return true;
  }

  removeSpace(str: string): string {
    if (this.isEmpty(str)) {
      return '';
    }
    return str.replace(new RegExp("[\\s]", "g"), '');
  }

  build() {
    Column() {
        Row() {
          TextInput({ text: `${this.text}` }).type(InputType.PhoneNumber).height('48vp')
            .onChange((number: string) => {
              let teleNumberNoSpace: string = this.removeSpace(number);
              if (teleNumberNoSpace.length > this.NUM_TEXT_MAXSIZE_LENGTH - 2) {
                this.text = teleNumberNoSpace;
              } else if (this.checkNeedNumberSpace(number)) {
                if (teleNumberNoSpace.length <= 3) {
                  this.text = teleNumberNoSpace;
                } else {
                  let split1: string = teleNumberNoSpace.substring(0, 3);
                  let split2: string = teleNumberNoSpace.substring(3);
                  this.text = split1 + ' ' + split2;
                  if (teleNumberNoSpace.length > 7) {
                    split2 = teleNumberNoSpace.substring(3, 7);
                    let split3: string = teleNumberNoSpace.substring(7);
                    this.text = split1 + ' ' + split2 + ' ' + split3;
                  }
                }
              } else if (teleNumberNoSpace.length > 8) {
                let split4 = teleNumberNoSpace.substring(0, 8);
                let split5 = teleNumberNoSpace.substring(8);
                this.text = split4 + ' ' + split5;
              } else {
                this.text = number;
              }
            })
        }
    }
    .width('100%')
    .height("100%")
  }
}

```
![phone_example](figures/phone_number.PNG)

### 示例7

本示例展示如何在下划线开启时，设置下划线颜色。

```ts
@Entry
@Component
struct Index {

  build() {
    Row() {
      Column() {
        TextInput({placeholder:'提示文本内容'})
          .showUnderline(true)
          .underlineColor({normal:Color.Orange,typing:Color.Green,error:Color.Red,disable:Color.Gray});
        TextInput({placeholder:'提示文本内容'})
          .showUnderline(true)
          .underlineColor(Color.Gray);
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

![UnderlineColor](figures/UnderlineColor.png)


### 示例8
示例展示设置不同wordBreak属性的TextInput样式。

```ts
// xxx.ets
@Entry
@Component
struct TextInputExample {
  build() {
    Column() {
      Text("TextInput为inline模式，WordBreakType属性为NORMAL的样式：").fontSize(16).fontColor(0xFF0000)
      TextInput({
        text: 'This is set wordBreak to WordBreak text Taumatawhakatangihangakoauauotamateaturipukakapikimaungahoronukupokaiwhenuakitanatahu.'
      })
        .fontSize(16)
        .style(TextInputStyle.Inline) // Inline模式
        .wordBreak(WordBreak.NORMAL) // 非Inline模式该属性无效

      Text("TextInput为inline模式，英文文本，WordBreakType属性为BREAK_ALL的样式：").fontSize(16).fontColor(0xFF0000)
      TextInput({
        text: 'This is set wordBreak to WordBreak text Taumatawhakatangihangakoauauotamateaturipukakapikimaungahoronukupokaiwhenuakitanatahu.'
      })
        .fontSize(16)
        .style(TextInputStyle.Inline)
        .wordBreak(WordBreak.BREAK_ALL)

      Text("TextInput为inline模式，中文文本，WordBreakType属性为BREAK_ALL的样式：").fontSize(16).fontColor(0xFF0000)
      TextInput({
        text: '多行文本输入框组件，当输入的文本内容超过组件宽度时会自动换行显示。\n高度未设置时，组件无默认高度，自适应内容高度。宽度未设置时，默认撑满最大宽度。'
      })
        .fontSize(16)
        .style(TextInputStyle.Inline)
        .wordBreak(WordBreak.BREAK_ALL)

      Text("TextInput为inline模式，WordBreakType属性为BREAK_WORD的样式：").fontSize(16).fontColor(0xFF0000)
      TextInput({
        text: 'This is set wordBreak to WordBreak text Taumatawhakatangihangakoauauotamateaturipukakapikimaungahoronukupokaiwhenuakitanatahu.'
      })
        .fontSize(16)
        .style(TextInputStyle.Inline)
        .wordBreak(WordBreak.BREAK_WORD)
    }
  }
}
```
![TextInputWordBreak](figures/TextInputWordBreak.jpeg)

### 示例9

该示例实现了使用lineHeight设置文本的文本行高，使用letterSpacing设置文本字符间距，使用decoration设置文本装饰线样式。

```ts
@Entry
@Component
struct TextInputExample {
  build() {
    Row() {
      Column() {
        Text('lineHeight').fontSize(9).fontColor(0xCCCCCC)
        TextInput({text: 'lineHeight unset'})
          .border({ width: 1 }).padding(10).margin(5)
        TextInput({text: 'lineHeight 15'})
          .border({ width: 1 }).padding(10).margin(5).lineHeight(15)
        TextInput({text: 'lineHeight 30'})
          .border({ width: 1 }).padding(10).margin(5).lineHeight(30)

        Text('letterSpacing').fontSize(9).fontColor(0xCCCCCC)
        TextInput({text: 'letterSpacing 0'})
          .border({ width: 1 }).padding(5).margin(5).letterSpacing(0)
        TextInput({text: 'letterSpacing 3'})
          .border({ width: 1 }).padding(5).margin(5).letterSpacing(3)
        TextInput({text: 'letterSpacing -1'})
          .border({ width: 1 }).padding(5).margin(5).letterSpacing(-1)

        Text('decoration').fontSize(9).fontColor(0xCCCCCC)
        TextInput({text: 'LineThrough, Red'})
          .border({ width: 1 }).padding(5).margin(5)
          .decoration({type: TextDecorationType.LineThrough, color: Color.Red})
        TextInput({text: 'Overline, Red'})
          .border({ width: 1 }).padding(5).margin(5)
          .decoration({type: TextDecorationType.Overline, color: Color.Red})
        TextInput({text: 'Underline, Red'})
          .border({ width: 1 }).padding(5).margin(5)
          .decoration({type: TextDecorationType.Underline, color: Color.Red})
      }.height('90%')
    }
    .width('90%')
    .margin(10)
  }
}
```

![TextInputDecoration](figures/textinput_decoration.png)

### 示例10

fontFeature属性使用示例，对比了fontFeature使用ss01属性和不使用ss01属性的效果。

```ts
@Entry
@Component
struct textInput {
  @State text1: string = 'This is ss01 on : 0123456789'
  @State text2: string = 'This is ss01 off: 0123456789'


  build() {
    Column(){
      TextInput({text: this.text1})
        .fontSize(20)
        .margin({top:200})
        .fontFeature("\"ss01\" on")
      TextInput({text : this.text2})
        .margin({top:10})
        .fontSize(20)
        .fontFeature("\"ss01\" off")
    }
    .width("90%")
    .margin("5%")
  }
}
```

![fontFeature](figures/textInputFontFeature.png)

### 示例11

自定义键盘弹出发生避让示例

```ts
@Entry
@Component
struct Input {
  controller: TextInputController = new TextInputController()
  @State inputValue: string = ""
  @State height1:string|number = '80%'
  @State supportAvoidance:boolean = true;
  // 自定义键盘组件
  @Builder CustomKeyboardBuilder() {
    Column() {
      Row(){
        Button('x').onClick(() => {
          // 关闭自定义键盘
          this.controller.stopEditing()
        }).margin(10)
      }
      Grid() {
        ForEach([1, 2, 3, 4, 5, 6, 7, 8, 9, '*', 0, '#'], (item:number|string) => {
          GridItem() {
            Button(item + "")
              .width(110).onClick(() => {
              this.inputValue += item
            })
          }
        })
      }.maxCount(3).columnsGap(10).rowsGap(10).padding(5)
    }.backgroundColor(Color.Gray)
  }
  build() {
    Column() {
      Row(){
        Button("20%")
          .fontSize(24)
          .onClick(()=>{
            this.height1 = "20%"
          })
        Button("80%")
          .fontSize(24)
          .margin({left:20})
          .onClick(()=>{
            this.height1 = "80%"
          })
      }
      .justifyContent(FlexAlign.Center)
      .alignItems(VerticalAlign.Bottom)
      .height(this.height1)
      .width("100%")
      .padding({bottom:50})
      TextInput({ controller: this.controller, text: this.inputValue })
        // 绑定自定义键盘
        .customKeyboard(this.CustomKeyboardBuilder(),{ supportAvoidance: this.supportAvoidance }).margin(10).border({ width: 1 })

    }
  }
}
```

![CustomTextInputType](figures/textInputCustomKeyboard.gif)

### 示例12

该示例实现了使用minFontSize，maxFontSize及heightAdaptivePolicy设置文本自适应字号。

```ts
@Entry
@Component
struct TextInputExample {
  build() {
    Row() {
      Column() {
        Text('heightAdaptivePolicy').fontSize(9).fontColor(0xCCCCCC)
        TextInput({text: 'This is the text without the height adaptive policy set'})
          .width('80%').height(50).borderWidth(1).margin(1)
        TextInput({text: 'This is the text with the height adaptive policy set'})
          .width('80%').height(50).borderWidth(1).margin(1)
          .minFontSize(4)
          .maxFontSize(40)
          .maxLines(3)
          .heightAdaptivePolicy(TextHeightAdaptivePolicy.MAX_LINES_FIRST)
        TextInput({text: 'This is the text with the height adaptive policy set'})
          .width('80%').height(50).borderWidth(1).margin(1)
          .minFontSize(4)
          .maxFontSize(40)
          .maxLines(3)
          .heightAdaptivePolicy(TextHeightAdaptivePolicy.MIN_FONT_SIZE_FIRST)
        TextInput({text: 'This is the text with the height adaptive policy set'})
          .width('80%').height(50).borderWidth(1).margin(1)
          .minFontSize(4)
          .maxFontSize(40)
          .maxLines(3)
          .heightAdaptivePolicy(TextHeightAdaptivePolicy.LAYOUT_CONSTRAINT_FIRST)
      }.height('90%')
    }
    .width('90%')
    .margin(10)
  }
}
```

![TextInputAdaptFont](figures/textinput_adapt_font.png)
