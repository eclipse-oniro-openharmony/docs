# @ohos.app.ability.errorManager (ErrorManager)

ErrorManager模块提供对错误观察器的注册和注销的能力。

> **说明：**
> 
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块
```ts
import errorManager from '@ohos.app.ability.errorManager';
```

## ErrorManager.on

on(type: 'error', observer: ErrorObserver): number

注册错误观测器。注册后可以捕获到应用产生的js crash，应用崩溃时进程不会退出。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**
 
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 填写'error'，表示错误观察器。 |
| observer | [ErrorObserver](js-apis-inner-application-errorObserver.md) | 是 | 错误观察器。 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | number | 观察器的index值，和观察器一一对应。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000003 | Id does not exist. |

以上错误码详细介绍请参考[元能力子系统错误码](errorcode-ability.md)。

**示例：**
    
```ts
import errorManager from '@ohos.app.ability.errorManager';
import { BusinessError } from '@ohos.base';

let observer: errorManager.ErrorObserver = {
    onUnhandledException(errorMsg) {
        console.log('onUnhandledException, errorMsg: ', errorMsg);
    },
    onException(errorObj) {
        console.log('onException, name: ', errorObj.name);
        console.log('onException, message: ', errorObj.message);
        if (typeof(errorObj.stack) === 'string') {
            console.log('onException, stack: ', errorObj.stack);
        }
    }
};
let observerId = -1;
try {
    observerId = errorManager.on('error', observer);
} catch (paramError) {
    let code = (paramError as BusinessError).code;
    let message = (paramError as BusinessError).message;
    console.error(`error: ${code}, ${message}`);
}
```

## ErrorManager.off

off(type: 'error', observerId: number,  callback: AsyncCallback\<void>): void

注销错误观测器。使用callback异步返回。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**
 
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 填写'error'，表示错误观察器。 |
| observerId | number | 是 | 由on方法返回的观察器的index值。 |
| callback | AsyncCallback\<void> | 是 | 表示指定的回调方法。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000003 | Id does not exist. |

以上错误码详细介绍请参考[元能力子系统错误码](errorcode-ability.md)。

**示例：**
    
```ts
import errorManager from '@ohos.app.ability.errorManager';
import { BusinessError } from '@ohos.base';

let observerId = 100;

function unregisterErrorObserverCallback(err: BusinessError) {
    if (err) {
        console.error('------------ unregisterErrorObserverCallback ------------', err);
    }
}
try {
    errorManager.off('error', observerId, unregisterErrorObserverCallback);
} catch (paramError) {
    let code = (paramError as BusinessError).code;
    let message = (paramError as BusinessError).message;
    console.error(`error: ${code}, ${message}`);
}
```

## ErrorManager.off

off(type: 'error', observerId: number): Promise\<void>

注销错误观测器。使用Promise异步返回。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**
 
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 填写'error'，表示错误观察器。 |
| observerId | number | 是 | 由on方法返回的观察器的index值。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<void> | Promise对象。无返回结果的Promise对象。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000003 | Id does not exist. |

以上错误码详细介绍请参考[元能力子系统错误码](errorcode-ability.md)。

**示例：**
    
```ts
import errorManager from '@ohos.app.ability.errorManager';
import { BusinessError } from '@ohos.base';

let observerId = 100;
try {
    errorManager.off('error', observerId)
        .then((data) => {
            console.log('----------- unregisterErrorObserver success ----------', data);
        })
        .catch((err: BusinessError) => {
            console.error('----------- unregisterErrorObserver fail ----------', err);
    });
} catch (paramError) {
    let code = (paramError as BusinessError).code;
    let message = (paramError as BusinessError).message;
    console.error(`error: ${code}, ${message}`);
}
```

## ErrorManager.on<sup>12+</sup>

on(type: 'loopObserver', timeout: number, observer: LoopObserver): void

注册主线程消息处理耗时监听器。注册后可以捕获到应用主线程处理消息的具体执行时间。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**
 
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 填写'loopObserver'，表示注册主线程消息处理耗时监听器。 |
| timeout | number | 是 |  表示事件执行阈值（单位：毫秒）。 阈值必须大于0。 |
| observer | [LoopObserver](js-apis-inner-application-loopObserver.md) | 是 | 注册主线程消息处理耗时监听器。 |

**示例：**
    
```ts
import errorManager from '@ohos.app.ability.errorManager';

let observer: errorManager.LoopObserver = {
    onLoopTimeOut(timeout: number) {
        console.log('Duration timeout: ' + timeout);
    }
};
errorManager.on("loopObserver", 1, observer);
```

## ErrorManager.on<sup>12+</sup>

on(type: 'unhandledRejection', observer: UnhandledRejectionObserver): void

注册主线程被拒绝promise监听器。注册后可以捕获到应用主线程中未被捕获到的promise rejection。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**
 
| 参数名                   | 类型                                                          | 必填 | 说明                                       |
|-----------------------|-------------------------------------------------------------| -------- |------------------------------------------|
| type                  | string                                                      | 是 | 填写'unhandledRejection'，表示注册主线程被拒绝promise监听器。 |
| observer              | [UnhandledRejectionObserver](#unhandledrejectionobserver12) | 是 | 注册主线程被拒绝promise监听器。                          |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16200001 | If the caller is invalid. |

以上错误码详细介绍请参考[元能力子系统错误码](errorcode-ability.md)。

**示例：**
    
```ts
import errorManager from '@ohos.app.ability.errorManager';

let observer: errorManager.UnhandledRejectionObserver = (reason: Error, promise: Promise<void>) => {
  if (promise === promise1) {
    console.log("promise1 is rejected");
  }
  console.log("reason.name: ", reason.name);
  console.log("reason.message: ", reason.message);
  if (reason.stack) {
      console.log("reason.stack: ", reason.stack);
  }
};

errorManager.on("unhandledRejection", observer);

let promise1 = new Promise<void>(() => {}).then(() => {
    throw new Error("uncaught error")
})
```

## ErrorManager.off<sup>12+</sup>

off(type: 'loopObserver', observer?: LoopObserver): void

注销主线程消息处理监听器。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**
 
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 填写'loopObserver'，表示应用主线程观察器。 |
| observer | [LoopObserver](js-apis-inner-application-loopObserver.md) | 否 | 应用主线程观察器标志。 |

**示例：**
    
```ts
import errorManager from '@ohos.app.ability.errorManager';

errorManager.off("loopObserver");
```

## ErrorManager.off<sup>12+</sup>

off(type: 'unhandledRejection', observer?: UnhandledRejectionObserver): void

注销主线程被拒绝promise监听器。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名                   | 类型                              | 必填 | 说明                                           |
|-----------------------|---------------------------------|----|----------------------------------------------|
| type                  | string                          | 是  | 填写'unhandledRejection'，表示注册主线程被拒绝promise监听器。 |
| observer              | [UnhandledRejectionObserver](#unhandledrejectionobserver12) | 否  | 注册了的主线程被拒绝promise监听器。                        |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16200001 | Invalid caller. |
| 16300004 | observer not found. |

以上错误码详细介绍请参考[元能力子系统错误码](errorcode-ability.md)。

**示例：**
    
```ts
import errorManager from '@ohos.app.ability.errorManager';

let observer: errorManager.UnhandledRejectionObserver = (reason: Error, promise: Promise<void>) => {
  if (promise === promise1) {
    console.log("promise1 is rejected");
  }
  console.log("reason.name: ", reason.name);
  console.log("reason.message: ", reason.message);
  if (reason.stack) {
    console.log("reason.stack: ", reason.stack);
  }
};

errorManager.on("unhandledRejection", observer);

let promise1 = new Promise<void>(() => {}).then(() => {
  throw new Error("uncaught error")
})

errorManager.off("unhandledRejection");
```
或者
```ts
import errorManager from '@ohos.app.ability.errorManager';

let observer: errorManager.UnhandledRejectionObserver = (reason: Error, promise: Promise<void>) => {
  if (promise === promise1) {
    console.log("promise1 is rejected");
  }
  console.log("reason.name: ", reason.name);
  console.log("reason.message: ", reason.message);
  if (reason.stack) {
    console.log("reason.stack: ", reason.stack);
  }
};

errorManager.on("unhandledRejection", observer);

let promise1 = new Promise<void>(() => {}).then(() => {
  throw new Error("uncaught error")
})

errorManager.off("unhandledRejection", observer);
```

## UnhandledRejectionObserver<sup>12+</sup>

type UnhandledRejectionObserver = (reason: Error | any, promise: Promise\<any>) => void

将在js运行时应用主线程中用户未捕获到的rejection。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名    | 类型            | 必填 | 说明 |
|--------|---------------|---| -------- |
| reason | Error \| any  | 是 | 通常是`Error`类型，表示被拒绝的理由。 |
| promise | Promise\<any> | 否 | 被拒绝的promise。 |
