# @ohos.app.ability.dialogRequest (dialogRequest模块)

dialogRequest模块用于处理模态弹框的能力，包括获取RequestInfo（用于绑定模态弹框）、获取RequestCallback（用于设置结果）。
模态弹框是指一个系统弹出框，其特点在于：该弹出框会拦截弹框之下的页面的鼠标、键盘、触屏等事件，销毁该弹框，才能操作下面的页面。

> **说明：**
>
>  - 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>  - 本模块接口在ServiceExtensionAbility下使用，如果ServiceExtensionAbility实现了模态弹框，则可以使用本模块的接口获取请求方的RequestInfo、RequestCallback并返回请求结果。

## 导入模块

```ts
import dialogRequest from '@ohos.app.ability.dialogRequest';
```

## dialogRequest.getRequestInfo

getRequestInfo(want: Want): RequestInfo

从Want中获取请求方的RequestInfo。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                        |
| ---- | ------ | ---- | --------------------------- |
| want  | [Want](js-apis-app-ability-want.md) | 是   | 表示发起方请求弹框时传入的want信息。 |

**返回值：**

| 类型   | 说明                     |
| ------ | ------------------------ |
| [RequestInfo](#requestinfo) | 请求方RequestInfo,用于绑定模态窗口。 |

**示例：**

```ts
   import ServiceExtensionAbility from '@ohos.app.ability.ServiceExtensionAbility';
   import Want from '@ohos.app.ability.Want';
   import rpc from '@ohos.rpc';
   import dialogRequest from '@ohos.app.ability.dialogRequest';

    const REQUEST_VALUE = 1;

    class StubTest extends rpc.RemoteObject {
      constructor(des: string) {
        super(des);
      }

      onRemoteRequest(code: number, data: rpc.MessageParcel, reply: rpc.MessageParcel, option: rpc.MessageOption) {
        if (code === REQUEST_VALUE) {
          let optFir = data.readInt();
          let optSec = data.readInt();
          reply.writeInt(optFir + optSec);
        }
        return true;
      }

      getInterfaceDescriptor() {
        return "";
      }

      getCallingPid() {
        return REQUEST_VALUE;
      }

      getCallingUid() {
        return REQUEST_VALUE;
      }

      attachLocalInterface(localInterface: rpc.IRemoteBroker, descriptor: string) {
      }
    }

    let TAG = "getRequestInfoTest";

    export default class ServiceExtAbility extends ServiceExtensionAbility {
      onCreate(want: Want) {
        console.info(TAG, `onCreate, want: ${want.abilityName}`);
      }

      onRequest(want: Want, startId: number) {
        console.info(TAG, `onRequest, want: ${want.abilityName}`);
        try {
          let requestInfo = dialogRequest.getRequestInfo(want);
        } catch (err) {
          console.error(`getRequestInfo err= ${JSON.stringify(err)}`);
        }
      }

      onConnect(want: Want) {
        console.info(TAG, `onConnect, want: ${want.abilityName}`);
        return new StubTest("test");
      }

      onDisconnect(want: Want) {
        console.info(TAG, `onDisconnect, want: ${want.abilityName}`);
      }

      onDestroy() {
        console.info(TAG, `onDestroy`);
      }
    }
   ```

## dialogRequest.getRequestCallback

getRequestCallback(want: Want): RequestCallback

从Want中获取请求方的RequestCallback。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                        |
| ---- | ------ | ---- | --------------------------- |
| want  | [Want](js-apis-app-ability-want.md) | 是   | 表示发起方请求弹框时传入的want信息。 |

**返回值：**

| 类型   | 说明                     |
| ------ | ------------------------ |
| [RequestCallback](#requestcallback) | 请求方RequestCallback,用于设置返回结果。 |

**示例：**

```ts
   import ServiceExtensionAbility from '@ohos.app.ability.ServiceExtensionAbility';
   import Want from '@ohos.app.ability.Want';
   import rpc from '@ohos.rpc';
   import dialogRequest from '@ohos.app.ability.dialogRequest';
   
   let TAG = "getRequestCallbackTest";

   const REQUEST_VALUE = 1;

    class StubTest extends rpc.RemoteObject {
      constructor(des: string) {
        super(des);
      }

      onRemoteRequest(code: number, data: rpc.MessageParcel, reply: rpc.MessageParcel, option: rpc.MessageOption) {
        if (code === REQUEST_VALUE) {
          let optFir = data.readInt();
          let optSec = data.readInt();
          reply.writeInt(optFir + optSec);
        }
        return true;
      }

      getInterfaceDescriptor() {
        return "";
      }

      getCallingPid() {
        return REQUEST_VALUE;
      }

      getCallingUid() {
        return REQUEST_VALUE;
      }

      attachLocalInterface(localInterface: rpc.IRemoteBroker, descriptor: string) {
      }
    }

   export default class ServiceExtAbility extends ServiceExtensionAbility {
     onCreate(want: Want) {
       console.info(TAG, `onCreate, want: ${want.abilityName}`);
     }

     onRequest(want: Want, startId: number) {
       console.info(TAG, `onRequest, want: ${want.abilityName}`);
       try {
            let requestCallback = dialogRequest.getRequestCallback(want);
        } catch(err) {
            console.error(`getRequestInfo err= ${JSON.stringify(err)}`);
        }
     }

     onConnect(want: Want) {
       console.info(TAG, `onConnect, want: ${want.abilityName}`);
       return new StubTest("test");
     }

     onDisconnect(want: Want) {
       console.info(TAG, `onDisconnect, want: ${want.abilityName}`);
     }

     onDestroy() {
       console.info(TAG, `onDestroy`);
     }
   }
   ```

## WindowRect<sup>10+</sup>

表示模态弹框的属性。

**模型约束**：此接口仅可在Stage模型下使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

| 名称 | 类型   | 必填 | 说明                        |
| ---- | ------ | ---- | --------------------------- |
| left  | number | 否   | 弹框边框的左上角的X坐标。 |
| top  | number | 否   | 弹框边框的左上角的Y坐标。 |
| width  | number | 否   | 弹框的宽度。 |
| height  | number | 否   | 弹框的高度。 |

## RequestInfo

表示发起方请求信息，作为窗口绑定模态弹框的入参。

**模型约束**：此接口仅可在Stage模型下使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

| 名称      | 类型       | 必填   | 说明     |
| ------------ | ------------------| ------ | ---------------------- |
| windowRect<sup>10+</sup>            | windowRect    | 否   | 表示模态弹框的位置属性。          |

**示例：**

```ts
   import ServiceExtensionAbility from '@ohos.app.ability.ServiceExtensionAbility';
   import Want from '@ohos.app.ability.Want';
   import { BusinessError } from '@ohos.base';
   import rpc from '@ohos.rpc';
   import dialogRequest from '@ohos.app.ability.dialogRequest';
   import window from '@ohos.window';
   
   let TAG = "RequestInfoTest";

   const REQUEST_VALUE = 1;

    class StubTest extends rpc.RemoteObject {
      constructor(des: string) {
        super(des);
      }

      onRemoteRequest(code: number, data: rpc.MessageParcel, reply: rpc.MessageParcel, option: rpc.MessageOption) {
        if (code === REQUEST_VALUE) {
          let optFir = data.readInt();
          let optSec = data.readInt();
          reply.writeInt(optFir + optSec);
        }
        return true;
      }

      getInterfaceDescriptor() {
        return "";
      }

      getCallingPid() {
        return REQUEST_VALUE;
      }

      getCallingUid() {
        return REQUEST_VALUE;
      }

      attachLocalInterface(localInterface: rpc.IRemoteBroker, descriptor: string) {
      }
    }

   export default class ServiceExtAbility extends ServiceExtensionAbility {
     onCreate(want: Want) {
       console.info(TAG, `onCreate, want: ${want.abilityName}`);
     }

     onRequest(want: Want, startId: number) {
       console.info(TAG, `onRequest, want: ${want.abilityName}`);
       let windowClass: window.Window | undefined = undefined;
       let config: window.Configuration = {name: "dialogWindow", windowType: window.WindowType.TYPE_DIALOG, ctx: this.context};
       try {
            let requestInfo = dialogRequest.getRequestInfo(want);
            window.createWindow(config, (err, data) => {
              if (err.code) {
                  console.error('Failed to create the window. Cause: ' + JSON.stringify(err));
                  return;
              }
              windowClass = data;
              windowClass.bindDialogTarget(requestInfo, () => {
                console.info('Dialog Window Need Destroy.');
              }, (err: BusinessError) => {
                  if (err.code) {
                      console.error(`Failed to bind dialog target. Cause: ${JSON.stringify(err)}`);
                      return;
                  }
                  console.info('Succeeded in binding dialog target.');
              });
            });
        } catch(err) {
            console.error(`getRequestInfo err= ${JSON.stringify(err)}`);
        }
     }

     onConnect(want: Want) {
       console.info(TAG, `onConnect, want: ${want.abilityName}`);
       return new StubTest("test");
     }

     onDisconnect(want: Want) {
       console.info(TAG, `onDisconnect, want: ${want.abilityName}`);
     }

     onDestroy() {
       console.info(TAG, `onDestroy`);
     }
   }
   ```

## ResultCode

模态弹框请求结果码。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

| 名称      | 值          | 说明     |
| ------------ | ------------------ | ---------------------- |
| RESULT_OK            | 0          | 表示成功。          |
| RESULT_CANCEL        | 1          | 表示失败。          |

## RequestResult
模态弹框请求结果，当前只包含结果码，即RequestResult只当前只有ResultCode这一个成员。

## 属性

**模型约束**：此接口仅可在Stage模型下使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| result | [ResultCode](#resultcode) | 是 | 是 | 表示结果码。 |
| want<sup>10+</sup> | [ResultWant](js-apis-app-ability-want.md)  | 是 | 是 | 表示Want类型信息，如ability名称，包名等。 |

## RequestCallback

用于设置模态弹框请求结果的callback接口。

**模型约束**：此接口仅可在Stage模型下使用。

### RequestCallback.setRequestResult

setRequestResult(result: RequestResult): void;

设置请求结果

**模型约束**：此接口仅可在Stage模型下使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| result | [RequestResult](#requestresult) | 是 | 模态弹框请求结果信息。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 401 | If the input parameter is not valid parameter. |

以上错误码详细介绍请参考[元能力子系统错误码](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
   import ServiceExtensionAbility from '@ohos.app.ability.ServiceExtensionAbility';
   import Want from '@ohos.app.ability.Want';
   import rpc from '@ohos.rpc';
   import dialogRequest from '@ohos.app.ability.dialogRequest';
   
   let TAG = "setRequestResultTest";

      const REQUEST_VALUE = 1;

    class StubTest extends rpc.RemoteObject {
      constructor(des: string) {
        super(des);
      }

      onRemoteRequest(code: number, data: rpc.MessageParcel, reply: rpc.MessageParcel, option: rpc.MessageOption) {
        if (code === REQUEST_VALUE) {
          let optFir = data.readInt();
          let optSec = data.readInt();
          reply.writeInt(optFir + optSec);
        }
        return true;
      }

      getInterfaceDescriptor() {
        return "";
      }

      getCallingPid() {
        return REQUEST_VALUE;
      }

      getCallingUid() {
        return REQUEST_VALUE;
      }

      attachLocalInterface(localInterface: rpc.IRemoteBroker, descriptor: string) {
      }
    }

   export default class ServiceExtAbility extends ServiceExtensionAbility {
     onCreate(want: Want) {
       console.info(TAG, `onCreate, want: ${want.abilityName}`);
     }

     onRequest(want: Want, startId: number) {
       console.info(TAG, `onRequest, want: ${want.abilityName}`);
       try {
            let requestCallback = dialogRequest.getRequestCallback(want);
            let myResult: dialogRequest.RequestResult = {
                result : dialogRequest.ResultCode.RESULT_CANCEL,
            };
            requestCallback.setRequestResult(myResult);
        } catch(err) {
            console.error(`getRequestInfo err= ${JSON.stringify(err)}`);
        }
     }

     onConnect(want: Want) {
       console.info(TAG, `onConnect, want: ${want.abilityName}`);
       return new StubTest("test");
     }

     onDisconnect(want: Want) {
       console.info(TAG, `onDisconnect, want: ${want.abilityName}`);
     }

     onDestroy() {
       console.info(TAG, `onDestroy`);
     }
   }
  ```