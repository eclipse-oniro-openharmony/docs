# FormLink

The **\<FormLink>** component is provided for interactions between static widgets and widget providers. It supports three types of events: router, message, and call.

> **NOTE**
>
> - This component is supported since API version 10. Updates will be marked with a superscript to indicate their earliest API version.
>
> - This component can be used only in static widgets.
>

## Required Permissions

None

## Child Components

This component supports only one child component.

## APIs

FormLink(value: {
  action: string;
  moduleName?: string;
  bundleName?: string;
  abilityName?: string;
  uri?: string;
  params?: Object;
})

**Parameters**

| Name     | Type| Mandatory| Description                                                    |
| ----------- | -------- | ---- | ------------------------------------------------------------ |
| action      | string   | Yes  | Action type.<br>- **"router"**: redirection to the specified UIAbility of the widget provider.<br>- **"message"**: custom message. If this type of action is triggered, the [onFormEvent()](../apis/js-apis-app-form-formExtensionAbility.md#onformevent) lifecycle callback of the provider FormExtensionAbility is called.<br>- **"call"**: launch of the widget provider in the background. If this type of action is triggered, the specified UIAbility (whose launch type must be [singleton](../../application-models/uiability-launch-type.md#singleton)) of the widget provider is started in the background, but not displayed in the foreground. This action type requires that the widget provider should have the [ohos.permission.KEEP_BACKGROUND_RUNNING](../../security/AccessToken/permissions-for-all.md#ohospermissionkeep_background_running) permission.<br>**NOTE**<br>Whenever possible, avoid using the router event to refresh the widget UI.|
| moduleName  | string   | No  | Name of the target module when **action** is **"router"** or **"call"**. |
| bundleName  | string   | No  | Name of the target bundle when **action** is **"router"** or **"call"**.   |
| abilityName | string   | No  | Name of the target UIAbility when **action** is **"router"** or **"call"**.|
| uri<sup>11+</sup> | string   | No  | URI of the target UIAbility when **action** is **"router"** or **"call"**.|
| params      | Object   | No  | Additional parameters carried in the current action. The value is a key-value pair in JSON format. For the **"call"** action type, the **method** parameter (optional) can be set and its value type must be string.<br>**NOTE**<br>Whenever possible, avoid using **params** to transfer internal state variables of widgets.|

## Attributes

The [universal attributes](ts-universal-attributes-size.md) are supported.

## Events

The [universal events](ts-universal-events-click.md) are not supported.

## Example

```ts
@Entry
@Component
struct FormLinkDemo {
  build() {
    Column() {
      Text("This is a static widget").fontSize(20).margin(10)

      // The router event is used to redirect to the specified UIAbility from the static widget.
      FormLink({
        action: "router",
        abilityName: "EntryAbility",
        params: {
          'message': 'testForRouter' // Customize the message to send.
        }
      }) {
        Button("router event").width(120)
      }.margin(10)


      // The message event triggers the onFormEvent callback of FormExtensionAbility.
      FormLink({
        action: "message",
        abilityName: "EntryAbility",
        params: {
          'message': 'messageEvent' // Customize the message to send.
        }
      }) {
        Button("message event").width(120)
      }.margin(10)


      // The call event is used to call the specified method in the UIAbility.
      FormLink({
        action: "call",
        abilityName: "EntryAbility",
        params: {
          'method': 'funA', // Set the name of the method to call in the EntryAbility.
          'num': 1 // Set other parameters to be passed in.
        }
      }) {
        Button("call event").width(120)
      }.margin(10)
    }
    .justifyContent(FlexAlign.Center)
    .width('100%').height('100%')
  }
}
```

![FormLink](figures/formLink.jpeg)
