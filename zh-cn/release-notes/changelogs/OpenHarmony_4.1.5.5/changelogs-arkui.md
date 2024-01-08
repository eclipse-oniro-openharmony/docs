# ArkUI子系统变更说明

## cl.arkui.1 Slider设置showTips方法显示效果变更

**访问级别**

公开接口

**变更原因**

该变更为兼容性变更，约束了Silder气泡的使用，优化了slider气泡的样式。

**变更影响**

Slider通过设置showTips方法，显示气泡。该方法有两个参数，参数1:boolean类型，表示是否显示气泡；参数2:ResourceStr类型，表示气泡中的文本内容。
具体受影响的场景见下文：

a) showTips 第一个参数设置为true显示气泡，气泡样式变化

变更前气泡样式：

![Alt text](figures/oldVertical.png)![Alt text](figures/oldHorizontal.png)

变更后气泡样式：

![Alt text](figures/newVertical.png)![Alt text](figures/newHorizontal.png)

b) showTips 第二个参数设置文本内容时，文本内容可能产生变化

变更前：根据栅格化宽度，可多行显示文本，全量显示文本。

变更后：单行显示文本，文本最大宽度36vp，即最大显示2个中文字符或4个数字。

**API Level**

7

**变更发生版本**

从OpenHarmony SDK 4.1.5.5开始。

**变更的接口/组件**

滑动条（Slider）

**适配指导**

默认行为变更，不涉及适配。

## cl.Arkui.2 Progress组件的默认颜色变更

**访问级别**

公开接口

**变更原因**

当前Progress组件的默认进度条前景色、默认进度条底色和默认内描边颜色不符合UX规范，因此依照UX规范对相关默认颜色做出变更。

**变更影响**

该变更为兼容性变更，改变了组件默认情况下的显示颜色，提升了组件的默认显示效果。

**API Level**

8

**变更发生版本**

从OpenHarmony SDK 4.1.5.5开始。

**变更的接口/组件**

API 11前，胶囊样式进度条默认前景色是系统资源中的`ohos_id_color_emphasize_contrary`，默认内描边颜色是系统资源中的`ohos_id_color_emphasize_contrary`，环形样式进度条默认进度条底色是系统资源中的`ohos_id_color_component_normal`。

API 11及以后，胶囊样式进度条默认前景色是系统资源中的`ohos_id_color_emphasize`，前景色不透明度为系统资源中的`ohos_id_alpha_highlight_bg`，默认内描边颜色是系统资源中的`ohos_id_color_emphasize`，内描边颜色不透明度为系统资源中的`ohos_id_alpha_highlight_bg`，环形样式进度条默认进度条底是系统资源中的`ohos_id_color_button_normal`。

**适配指导**

默认颜色变更，不涉及适配。

## cl.Arkui.3 LoadingProgress组件的默认颜色变更

**访问级别**

公开接口

**变更原因**

当前LoadingProgress组件的默认前景色不符合UX规范，因此依照UX规范对相关默认前景色做出变更。

**变更影响**

该变更为兼容性变更，改变了组件默认情况下的显示颜色，提升了组件的默认显示效果。

**API Level**

8

**变更发生版本**

从OpenHarmony SDK 4.1.5.5开始。

**变更的接口/组件**

API 11前，默认前景色不透明度为0.6，默认前景色是“#99666666”。

API 11及以后，默认前景色不透明度为1.0，默认前景色是“#ff666666”。

**适配指导**

默认颜色变更，不涉及适配。

## cl.arkui.4 Image组件colorFilter属性默认行为变更

**访问级别**

公开接口

**变更原因**

用户对于Image组件colorFilter属性设置异常值时，使用默认值

**变更影响**

该变更为非兼容性变更。

变更前，当开发者对Image组件的colorFilter属性设置为异常值时，采用不操作处理。

变更后，当开发者对Image组件的colorFilter属性设置为异常值时，采用对角线为 $1$ 其余值为 $0$ 的 $4 \times 5$ 的矩阵来处理。

**API Level**

11

**变更发生版本**

从OpenHarmony SDK 4.1.5.5 开始。

**变更的接口/组件**

受影响的组件有：Image。

**适配指导**

默认行为变更，不涉及适配。

## cl.arkui.5 Image组件fillColor属性默认行为变更

**访问级别**

公开接口

**变更原因**

用户对于Image组件fillColor属性设置异常值时，使用默认值

**变更影响**

该变更为非兼容性变更。

变更前，当开发者对Image组件的fillColor属性设置为异常值时，采用不操作处理。

变更后，当开发者对Image组件的fillColor属性设置为异常值时，采用系统默认颜色来处理。

**API Level**

11

**变更发生版本**

从OpenHarmony SDK 4.1.5.5 开始。

**变更的接口/组件**

受影响的组件有：Image。

**适配指导**

默认行为变更，不涉及适配。


## cl.Arkui.6 Datapanel组件的默认阴影模糊半径变更

**访问级别**

公开接口

**变更原因**

当前Datapanel组件的默认阴影模糊半径为5vp、UX检视时发现模糊半径过小，因此依照UX规范增加阴影模糊半径到20vp。

**变更影响**

该变更为兼容性变更，改变了组件默认情况下的阴影模糊半径，提升了组件的默认显示效果。

**API Level**

10

**变更发生版本**

从OpenHarmony SDK 4.1.5.5开始。

**变更的接口/组件**

API 11前，Datapanel组件的默认阴影模糊半径为5vp。

API 11及以后，Datapanel组件的默认阴影模糊半径为20vp。

**适配指导**

默认阴影效果变更，不涉及适配。

## cl.Arkui.7 Dialog组件内容的默认对齐方式变更

**访问级别**

公开接口

**变更原因**

当前Dialog组件内容的默认对齐方式不符合UX规范，因此依照UX规范对对齐方式做出变更。

**变更影响**

该变更为兼容性变更，改变了Dialog无标题且内容多行情况下的对齐方式，提升了组件的默认显示效果。

**API Level**

7

**变更发生版本**

从OpenHarmony SDK 4.1.5.5开始。

**变更的接口/组件**

API 11前，默认Dialog的内容区对齐方式在无标题情况下为居中对齐。

API 11及以后，默认Dialog的内容区对齐方式在无标题且内容只有一行的情况下为居中对齐，默认Dialog的内容区对齐方式在无标题且内容有多行的情况下为左对齐。

**适配指导**

默认对齐方式变更，不涉及适配。

## cl.Arkui.8 弹窗类组件背板的默认视觉效果变更为模糊材质

**访问级别**

公开接口

**变更原因**

增强视觉效果。

**变更影响**

该变更为兼容性变更。在统一渲染模式下，弹窗类组件背板的默认视觉效果变更为模糊材质。

**API Level**

11

**变更发生版本**

从OpenHarmony SDK 4.1.5.5开始。

**变更的接口/组件**

涉及到警告弹窗（AlertDialog）、列表选择弹窗（ActionSheet）、日历选择器弹窗（CalendarPickerDialog）、日期滑动选择器弹窗（DatePickerDialog）、时间滑动选择器弹窗（TimePickerDialog）、文本滑动选择器弹窗（TextPickerDialog）、promptAction中showDialog方法

API 11前，弹窗类组件背板显示为主题色。

API 11及以后，弹窗类组件背板显示为模糊材质。

**适配指导**

默认背板效果变更，不涉及适配。

## cl.Arkui.9 Dialog组件内容区Text默认分词方式变更

**访问级别**

公开接口

**变更原因**

当前Dialog组件内容的默认分词方式不符合UX规范，因此依照UX规范对分词方式做出变更。

**变更影响**

该变更为兼容性变更，改变了Dialog内容区Text默认分词方式，提升了组件的默认显示效果。

**API Level**

7

**变更发生版本**

从OpenHarmony SDK 4.1.5.5开始。

**变更的接口/组件**

API 11前，默认Dialog的内容区分词方式为BREAK_WORD。

API 11及以后，默认Dialog的内容区分词方式为BREAK_ALL。

关于BREAK_WORD和BREAK_ALL的区别，详见[WordBreak](../../../application-dev/reference/arkui-ts/ts-appendix-enums.md#wordbreak11)

**适配指导**

默认分词方式变更，不涉及适配。
## cl.arkui.10 Image组件autoResize interpolation属性默认行为变更

**访问级别**

公开接口

**变更原因**

应用侧需要设置autoResize为false、 interpolation设置为LOW来解决图片锯齿问题

**变更影响**

该变更为非兼容性变更。

变更前，Image组件的autoResize默认值为true， interpolation为None。

变更后，Image组件的autoResize默认值为false， interpolation为LOW，该修改会提升图片显示效果，但是image组件在大图显示成小组件时，默认内存会上涨，需要应用根据实际情况进行内存优化。
说明：该修改不影响大桌面效果。

**API Level**

11

**变更发生版本**

从OpenHarmony SDK 4.1.5.5 开始。

**变更的接口/组件**

受影响的组件有：Image。

**适配指导**

默认行为变更，不涉及适配。