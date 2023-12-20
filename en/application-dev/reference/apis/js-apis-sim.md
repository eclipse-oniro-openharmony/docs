# @ohos.telephony.sim (SIM Management)

The **sim** module provides basic SIM card management functions. You can obtain the name, number, ISO country code, home PLMN number, service provider name, SIM card status, type, installation status, activation status, and lock status of the SIM card in the specified slot. Besides, you can set the name, number, and lock status of the SIM card, activate or deactivate the SIM card, and change the PIN or unlock the PIN or PUK of the SIM card.

>**NOTE**
>
>The initial APIs of this module are supported since API version 6. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>

## Modules to Import

```ts
import sim from '@ohos.telephony.sim';
```

## sim.isSimActive<sup>7+</sup>

isSimActive\(slotId: number, callback: AsyncCallback\<boolean\>\): void

Checks whether the SIM card in the specified slot is activated. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                       | Mandatory| Description                                  |
| -------- | --------------------------- | ---- | -------------------------------------- |
| slotId   | number                      | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback&lt;boolean&gt; | Yes  | Callback used to return the result. Boolean value indicating whether the SIM card in the specified slot is activated. The value **true** means yes and the value **false** means no.                            |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.isSimActive(0, (err: BusinessError, data: boolean) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.isSimActive<sup>7+</sup>

isSimActive\(slotId: number\): Promise\<boolean\>

Checks whether the SIM card in the specified slot is activated. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                 | Description                              |
| --------------------- | ---------------------------------- |
| Promise&lt;boolean&gt; | Promise used to return the result. The value **true** indicates that the SIM card in the specified slot is activated, and the value **false** indicates the opposite.|

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.isSimActive(0).then((data: boolean) => {
    console.log(`isSimActive success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`isSimActive failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.isSimActiveSync<sup>10+</sup>

isSimActiveSync\(slotId: number\): boolean

Checks whether the SIM card in the specified slot is activated.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                 | Description                              |
| --------------------- | ---------------------------------- |
| boolean | Boolean value indicating whether the SIM card in the specified slot is activated. The value **true** means yes and the value **false** means no.|

**Example**

```js
let isSimActive = sim.isSimActiveSync(0);
console.log(`the sim is active:` + isSimActive);
```


## sim.getDefaultVoiceSlotId<sup>7+</sup>

getDefaultVoiceSlotId\(callback: AsyncCallback\<number\>\): void

Obtains the default slot ID of the SIM card that provides voice services. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                       | Mandatory| Description      |
| -------- | --------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;number&gt; | Yes  | Callback used to return the result.<br>- **0**: card slot 1<br>- **1**: card slot 2<br>- **-1**: card slot not set or service not unavailable|

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getDefaultVoiceSlotId((err: BusinessError, data: number) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getDefaultVoiceSlotId<sup>7+</sup>

getDefaultVoiceSlotId\(\): Promise\<number\>

Obtains the default slot ID of the SIM card that provides voice services. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Return value**

| Type             | Description                                   |
| ----------------- | --------------------------------------- |
| Promise\<number\> | Promise used to return the result.<br>- **0**: card slot 1<br>- **1**: card slot 2<br>- **-1**: card slot not set or service not unavailable|

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getDefaultVoiceSlotId().then((data: number) => {
    console.log(`getDefaultVoiceSlotId success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getDefaultVoiceSlotId failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.hasOperatorPrivileges<sup>7+</sup>

hasOperatorPrivileges\(slotId: number, callback: AsyncCallback\<boolean\>\): void

Checks whether the application (caller) has been granted the operator permission. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                    | Mandatory| Description                                    |
| -------- | ------------------------ | ---- | ---------------------------------------- |
| slotId   | number                   | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<boolean\> | Yes  | Callback used to return the result.                               |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.hasOperatorPrivileges(0, (err: BusinessError, data: boolean) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```

## sim.hasOperatorPrivileges<sup>7+</sup>

hasOperatorPrivileges\(slotId: number\): Promise\<boolean\>

Checks whether the application (caller) has been granted the operator permission. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                    |
| ------ | ------ | ---- | ---------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type              | Description                                                       |
| :----------------- | :---------------------------------------------------------- |
| Promise\<boolean\> | Promise used to return the result. The value **true** indicates that the application (caller) has been granted the carrier permission, and the value **false** indicates the opposite.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.hasOperatorPrivileges(0).then((data: boolean) => {
    console.log(`hasOperatorPrivileges success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`hasOperatorPrivileges failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getISOCountryCodeForSim

getISOCountryCodeForSim\(slotId: number, callback: AsyncCallback\<string\>\): void

Obtains the ISO country code of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                   | Mandatory| Description                                    |
| -------- | ----------------------- | ---- | ---------------------------------------- |
| slotId   | number                  | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2  |
| callback | AsyncCallback\<string\> | Yes  | Callback used to return the result, which is an ISO country code, for example, **CN** (China).|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getISOCountryCodeForSim(0, (err: BusinessError, data: string) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getISOCountryCodeForSim

getISOCountryCodeForSim\(slotId: number\): Promise\<string\>

Obtains the ISO country code of the SIM card in the specified slot. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type             | Description                                                        |
| ----------------- | ------------------------------------------------------------ |
| Promise\<string\> | Promise used to return the result, which is an ISO country code, for example, **CN** (China).|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getISOCountryCodeForSim(0).then((data: string) => {
    console.log(`getISOCountryCodeForSim success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getISOCountryCodeForSim failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getISOCountryCodeForSimSync<sup>10+</sup>

getISOCountryCodeForSimSync\(slotId: number\): string

Obtains the ISO country code of the SIM card in the specified slot.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type             | Description                                                        |
| ----------------- | ------------------------------------------------------------ |
| string | ISO country code of the SIM card in the specified card slot, for example, **CN** (China).|


**Example**

```js
let countryCode = sim.getISOCountryCodeForSimSync(0);
console.log(`the country ISO is:` + countryCode);
```


## sim.getSimOperatorNumeric

getSimOperatorNumeric\(slotId: number, callback: AsyncCallback\<string\>\): void

Obtains the home public land mobile network (PLMN) ID of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                   | Mandatory| Description                                  |
| -------- | ----------------------- | ---- | -------------------------------------- |
| slotId   | number                  | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<string\> | Yes  | Callback used to return the result.                           |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getSimOperatorNumeric(0, (err: BusinessError, data: string) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getSimOperatorNumeric

getSimOperatorNumeric\(slotId: number\): Promise\<string\>

Obtains the home PLMN ID of the SIM card in the specified slot. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type             | Description                                            |
| ----------------- | ------------------------------------------------ |
| Promise\<string\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getSimOperatorNumeric(0).then((data: string) => {
    console.log(`getSimOperatorNumeric success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getSimOperatorNumeric failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getSimOperatorNumericSync<sup>10+</sup>

getSimOperatorNumericSync\(slotId: number\): string

Obtains the home PLMN ID of the SIM card in the specified slot. 

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type             | Description                                            |
| ----------------- | ------------------------------------------------ |
| string | Home PLMN number of the SIM card in the specified slot.|


**Example**

```js
let numeric = sim.getSimOperatorNumericSync(0);
console.log(`the sim operator numeric is:` + numeric);
```


## sim.getSimSpn

getSimSpn\(slotId: number, callback: AsyncCallback\<string\>\): void

Obtains the service provider name (SPN) of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                   | Mandatory| Description                                  |
| -------- | ----------------------- | ---- | -------------------------------------- |
| slotId   | number                  | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<string\> | Yes  | Callback used to return the result.                              |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getSimSpn(0, (err: BusinessError, data: string) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getSimSpn

getSimSpn\(slotId: number\): Promise\<string\>

Obtains the SPN of the SIM card in the specified slot. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type             | Description                                     |
| ----------------- | ----------------------------------------- |
| Promise\<string\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getSimSpn(0).then((data: string) => {
    console.log(`getSimSpn success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getSimSpn failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getSimSpnSync<sup>10+</sup>

getSimSpnSync\(slotId: number\): string

Obtains the SPN of the SIM card in the specified slot.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type             | Description                                     |
| ----------------- | ----------------------------------------- |
| string | SPN of the SIM card in the specified slot.|


**Example**

```js
let spn = sim.getSimSpnSync(0);
console.log(`the sim card spn is:` + spn);
```


## sim.getSimState

getSimState\(slotId: number, callback: AsyncCallback\<SimState\>\): void

Obtains the state of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                  | Mandatory| Description                                  |
| -------- | -------------------------------------- | ---- | -------------------------------------- |
| slotId   | number                                 | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<[SimState](#simstate)\> | Yes  | Callback used to return the result. For details, see [SimState](#simstate). |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getSimState(0, (err: BusinessError, data: sim.SimState) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getSimState

getSimState\(slotId: number\): Promise\<SimState\>

Obtains the state of the SIM card in the specified slot. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                            | Description                                      |
| -------------------------------- | ------------------------------------------ |
| Promise\<[SimState](#simstate)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getSimState(0).then((data: sim.SimState) => {
    console.log(`getSimState success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getSimState failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getSimStateSync<sup>10+</sup>

getSimStateSync\(slotId: number\): SimState

Obtains the state of the SIM card in the specified slot.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                        | Description                                      |
| ---------------------------- | ------------------------------------------ |
| [SimState](#simstate) | State of the SIM card in the specified slot.|


**Example**

```js
let simState = sim.getSimStateSync(0);
console.log(`The sim state is:` + simState);
```

## sim.getCardType<sup>7+</sup>

getCardType\(slotId: number, callback: AsyncCallback\<CardType\>\): void

Obtains the type of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                   | Mandatory| Description                                  |
| -------- | ----------------------- | ---- | -------------------------------------- |
| slotId   | number                  | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<[CardType](#cardtype7)\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getCardType(0, (err: BusinessError, data: sim.CardType) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getCardType<sup>7+</sup>

getCardType\(slotId: number\): Promise\<CardType\>

Obtains the type of the SIM card in the specified slot. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type             | Description                                                        |
| ----------------- | ------------------------------------------------------------ |
| Promise\<[CardType](#cardtype7)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getCardType(0).then((data: sim.CardType) => {
    console.log(`getCardType success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getCardType failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getCardTypeSync<sup>10+</sup>

getCardTypeSync\(slotId: number\): CardType

Obtains the type of the SIM card in the specified slot. 

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type             | Description                                                        |
| ----------------- | ------------------------------------------------------------ |
| [CardType](#cardtype7) | Type of the SIM card in the specified slot.|


**Example**

```js
let cardType = sim.getCardTypeSync(0);
console.log(`the card type is:` + cardType);
```


## sim.hasSimCard<sup>7+</sup>

hasSimCard\(slotId: number, callback: AsyncCallback\<boolean\>\): void

Checks whether the SIM card in the specified slot is installed. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                       | Mandatory| Description                                  |
| -------- | --------------------------- | ---- | -------------------------------------- |
| slotId   | number                      | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback&lt;boolean&gt; | Yes | Callback used to return the result. The value **true** indicates that the SIM card in the specified slot is installed, and the value **false** indicates the opposite.                          |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.hasSimCard(0, (err: BusinessError, data: boolean) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.hasSimCard<sup>7+</sup>

hasSimCard\(slotId: number\): Promise\<boolean\>

Checks whether the SIM card in the specified slot is installed. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                 | Description                              |
| --------------------- | ---------------------------------- |
| Promise&lt;boolean&gt; | Promise used to return the result. The value **true** indicates that the SIM card in the specified slot is installed, and the value **false** indicates the opposite.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.hasSimCard(0).then((data: boolean) => {
    console.log(`hasSimCard success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`hasSimCard failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.hasSimCardSync<sup>10+</sup>

hasSimCardSync\(slotId: number\): boolean

Checks whether the SIM card in the specified slot is installed.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                 | Description                              |
| --------------------- | ---------------------------------- |
| boolean | Boolean value indicating whether the SIM card in the specified slot is installed. The value **true** means yes and the value **false** means no.|

**Example**

```js
let hasSimCard = sim.hasSimCardSync(0);
console.log(`has sim card: ` + hasSimCard);
```

## sim.getSimAccountInfo<sup>10+</sup>

getSimAccountInfo\(slotId: number, callback: AsyncCallback\<IccAccountInfo\>\): void

Obtains account information of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

>**NOTE**
>
>If you do not have the **GET_TELEPHONY_STATE** permission, the ICCID and number information is empty.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                               | Mandatory| Description                                  |
| -------- | --------------------------------------------------- | ---- | -------------------------------------- |
| slotId   | number                                              | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<[IccAccountInfo](#iccaccountinfo10)\> | Yes  | Callback used to return the result.                              |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getSimAccountInfo(0, (err:BusinessError , data: sim.IccAccountInfo) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getSimAccountInfo<sup>10+</sup>

getSimAccountInfo\(slotId: number\): Promise\<IccAccountInfo\>

Obtains account information of the SIM card in the specified slot. This API uses a promise to return the result.

>**NOTE**
>
>If you do not have the **GET_TELEPHONY_STATE** permission, the ICCID and number information is empty.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                                        | Description                                      |
| -------------------------------------------- | ------------------------------------------ |
| Promise<[IccAccountInfo](#iccaccountinfo10)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getSimAccountInfo(0).then((data: sim.IccAccountInfo) => {
    console.log(`getSimAccountInfo success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getSimAccountInfo failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getActiveSimAccountInfoList<sup>10+</sup>

getActiveSimAccountInfoList\(callback: AsyncCallback\<Array\<IccAccountInfo\>\>\): void

Obtains the list of activated SIM card accounts. This API uses an asynchronous callback to return the result.

>**NOTE**
>
>If you do not have the **GET_TELEPHONY_STATE** permission, the ICCID and number information is empty.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                       | Mandatory| Description      |
| -------- | ----------------------------------------------------------- | ---- | ---------- |
| callback | AsyncCallback\<Array<[IccAccountInfo](#iccaccountinfo10)\>\> | Yes  | Callback used to return the result.  |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getActiveSimAccountInfoList((err: BusinessError, data: Array<sim.IccAccountInfo>) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getActiveSimAccountInfoList<sup>10+</sup>

getActiveSimAccountInfoList\(\): Promise\<Array\<IccAccountInfo\>\>

Obtains the list of activated SIM card accounts. This API uses a promise to return the result.

>**NOTE**
>
>If you do not have the **GET_TELEPHONY_STATE** permission, the ICCID and number information is empty.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Return value**

| Type                                                | Description                                          |
| ---------------------------------------------------- | ---------------------------------------------- |
| Promise<Array<[IccAccountInfo](#iccaccountinfo10)\>\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getActiveSimAccountInfoList().then((data: Array<sim.IccAccountInfo>) => {
    console.log(`getActiveSimAccountInfoList success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getActiveSimAccountInfoList failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.setDefaultVoiceSlotId<sup>7+</sup>

setDefaultVoiceSlotId\(slotId: number, callback: AsyncCallback\<void\>\): void

Sets the default slot ID of the SIM card that provides voice services. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                     | Mandatory| Description                                                        |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| slotId   | number                    | Yes  | SIM card slot ID. <br>- **0**: card slot 1<br>- **1**: card slot 2<br>- **-1**: Clears the default configuration.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                                                  |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301001  | SIM card is not activated.                   |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.setDefaultVoiceSlotId(0, (err: BusinessError) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## sim.setDefaultVoiceSlotId<sup>7+</sup>

setDefaultVoiceSlotId\(slotId: number\): Promise\<void\>

Sets the default slot ID of the SIM card that provides voice services. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| slotId | number | Yes  | SIM card slot ID. <br>- **0**: card slot 1<br>- **1**: card slot 2<br>- **-1**: Clears the default configuration.|

**Return value**

| Type           | Description                           |
| --------------- | ------------------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301001  | SIM card is not activated.                   |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.setDefaultVoiceSlotId(0).then(() => {
    console.log(`setDefaultVoiceSlotId success.`);
}).catch((err: BusinessError) => {
    console.error(`setDefaultVoiceSlotId failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.setShowName<sup>8+</sup>

setShowName\(slotId: number, name: string, callback: AsyncCallback\<void\>\): void

Sets a display name for the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                     | Mandatory| Description                                  |
| -------- | ------------------------- | ---- | -------------------------------------- |
| slotId   | number                    | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| name     | string                    | Yes  | SIM card name.                             |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let name: string = "ShowName";
sim.setShowName(0, name, (err: BusinessError) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```

## sim.setShowName<sup>8+</sup>

setShowName\(slotId: number, name: string\): Promise\<void\>

Sets a display name for the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| name   | string | Yes  | SIM card name.                             |

**Return value**

| Type           | Description                           |
| --------------- | ------------------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let name: string = "ShowName";
sim.setShowName(0, name).then(() => {
    console.log(`setShowName success.`);
}).catch((err: BusinessError) => {
    console.error(`setShowName failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getShowName<sup>8+</sup>

getShowName\(slotId: number, callback: AsyncCallback\<string\>\): void

Obtains the name of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                       | Mandatory| Description                                  |
| -------- | --------------------------- | ---- | -------------------------------------- |
| slotId   | number                      | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback&lt;string&gt; | Yes  | Callback used to return the result.                              |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getShowName(0, (err: BusinessError, data: string) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getShowName<sup>8+</sup>

getShowName\(slotId: number\): Promise\<string\>

Obtains the name of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                 | Description                                  |
| --------------------- | -------------------------------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getShowName(0).then((data: string) => {
    console.log(`getShowName success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getShowName failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.setShowNumber<sup>8+</sup>

setShowNumber\(slotId: number, number: string, callback: AsyncCallback\<void\>\): void

Sets a display number for the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                     | Mandatory| Description                                  |
| -------- | ------------------------- | ---- | -------------------------------------- |
| slotId   | number                    | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| number   | string                    | Yes  | SIM card number.                             |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let number: string = '+861xxxxxxxxxx';
sim.setShowNumber(0, number, (err: BusinessError) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## sim.setShowNumber<sup>8+</sup>

setShowNumber\(slotId: number, number: string\): Promise\<void\>

Sets a display number for the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| number | string | Yes  | SIM card number.                             |

**Return value**

| Type          | Description                           |
| -------------- | ------------------------------- |
| Promise<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let number: string = '+861xxxxxxxxxx';
sim.setShowNumber(0, number).then(() => {
    console.log(`setShowNumber success.`);
}).catch((err: BusinessError) => {
    console.error(`setShowNumber failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getShowNumber<sup>8+</sup>

getShowNumber\(slotId: number, callback: AsyncCallback\<string\>): void

Obtains the display number of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                       | Mandatory| Description                                  |
| -------- | --------------------------- | ---- | -------------------------------------- |
| slotId   | number                      | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback&lt;string&gt; | Yes  | Callback used to return the result.                              |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getShowNumber(0, (err: BusinessError, data: string) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getShowNumber<sup>8+</sup>

getShowNumber\(slotId: number\): Promise\<string\>

Obtains the display number of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                 | Description                             |
| --------------------- | --------------------------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getShowNumber(0).then((data: string) => {
    console.log(`getShowNumber success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getShowNumber failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.activateSim<sup>8+</sup>

activateSim\(slotId: number, callback: AsyncCallback\<void\>\): void

Activates a SIM card in a specified card slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                     | Mandatory| Description                                  |
| -------- | ------------------------- | ---- | -------------------------------------- |
| slotId   | number                    | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.activateSim(0, (err: BusinessError) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## sim.activateSim<sup>8+</sup>

activateSim\(slotId: number\): Promise\<void\>

Activates the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type           | Description                           |
| --------------- | ------------------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.activateSim(0).then(() => {
    console.log(`activateSim success.`);
}).catch((err: BusinessError) => {
    console.error(`activateSim failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.deactivateSim<sup>8+</sup>

deactivateSim\(slotId: number, callback: AsyncCallback\<void\>\): void

Disables the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                     | Mandatory| Description                                  |
| -------- | ------------------------- | ---- | -------------------------------------- |
| slotId   | number                    | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.deactivateSim(0, (err: BusinessError) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## sim.deactivateSim<sup>8+</sup>

deactivateSim\(slotId: number\): Promise\<void\>

Disables the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type           | Description                           |
| --------------- | ------------------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.deactivateSim(0).then(() => {
    console.log(`deactivateSim success.`);
}).catch((err: BusinessError) => {
    console.error(`deactivateSim failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.setLockState<sup>7+</sup>

setLockState\(slotId: number, options: LockInfo, callback: AsyncCallback\<LockStatusResponse\>\): void

Sets the lock status of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                       | Mandatory| Description                                                        |
| -------- | ----------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| slotId   | number                                                      | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2                      |
| callback | AsyncCallback\<[LockStatusResponse](#lockstatusresponse7)\> | Yes  | Callback used to return the result.                                                  |
| options  | [LockInfo](#lockinfo8)                                      | Yes  | Lock information.<br>- lockType: [LockType](#locktype8)<br>- password: string<br>- state: [LockState](#lockstate8) |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let lockInfo: sim.LockInfo = {
    lockType: sim.LockType.PIN_LOCK,
    password: "1234",
    state: sim.LockState.LOCK_OFF
};
sim.setLockState(0, lockInfo, (err: BusinessError, data: sim.LockStatusResponse) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.setLockState<sup>7+</sup>

setLockState\(slotId: number, options: LockInfo\): Promise\<LockStatusResponse\>

Sets the lock status of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name | Type                  | Mandatory| Description                                                        |
| ------- | ---------------------- | ---- | ------------------------------------------------------------ |
| slotId  | number                 | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2                      |
| options | [LockInfo](#lockinfo8) | Yes  | Lock information.<br>- lockType: [LockType](#locktype8)<br>- password: string<br>- state: [LockState](#lockstate8) |

**Return value**

| Type                                                | Description                                        |
| ---------------------------------------------------- | -------------------------------------------- |
| Promise<[LockStatusResponse](#lockstatusresponse7)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let lockInfo: sim.LockInfo = {
    lockType: sim.LockType.PIN_LOCK,
    password: "1234",
    state: sim.LockState.LOCK_OFF
};
sim.setLockState(0, lockInfo).then((data: sim.LockStatusResponse) => {
    console.log(`setLockState success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`setLockState failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getLockState<sup>8+</sup>

getLockState\(slotId: number, lockType: LockType, callback: AsyncCallback\<LockState\>\): void

Obtains the lock status of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                     | Mandatory| Description                                   |
| -------- | ----------------------------------------- | ---- | --------------------------------------- |
| slotId   | number                                    | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2 |
| callback | AsyncCallback\<[LockState](#lockstate8)\> | Yes  | Callback used to return the result.                             |
| options  | [LockType](#locktype8)                    | Yes  | Lock type.<br>- **1**: PIN lock<br>- **2**: PIN 2 lock|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getLockState(0, 1, (err: BusinessError, data: sim.LockState) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getLockState<sup>8+</sup>

getLockState\(slotId: number, lockType: LockType\): Promise\<LockState\>

Obtains the lock status of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name | Type                  | Mandatory| Description                                   |
| ------- | ---------------------- | ---- | --------------------------------------- |
| slotId  | number                 | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2 |
| options | [LockType](#locktype8) | Yes  | Lock type.<br>- **1**: PIN lock<br>- **2**: PIN 2 lock|

**Return value**

| Type                              | Description                                        |
| ---------------------------------- | -------------------------------------------- |
| Promise<[LockState](#lockstate8)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getLockState(0, 1).then((data: sim.LockState) => {
    console.log(`getLockState success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getLockState failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.alterPin<sup>7+</sup>

alterPin\(slotId: number, newPin: string, oldPin: string, callback: AsyncCallback\<LockStatusResponse\>\): void

Changes the PIN of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                       | Mandatory| Description                                  |
| -------- | ----------------------------------------------------------- | ---- | -------------------------------------- |
| slotId   | number                                                      | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<[LockStatusResponse](#lockstatusresponse7)\> | Yes  | Callback used to return the result.                            |
| newPin   | string                                                      | Yes  | New PIN.                              |
| oldPin   | string                                                      | Yes  | Old PIN.                              |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.alterPin(0, "1234", "0000", (err: BusinessError, data: sim.LockStatusResponse) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.alterPin<sup>7+</sup>

alterPin\(slotId: number, newPin: string, oldPin: string\): Promise\<LockStatusResponse\>

Changes the PIN of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| newPin | string | Yes  | New PIN.                              |
| oldPin | string | Yes  | Old PIN.                              |

**Return value**

| Type                                                | Description                                         |
| ---------------------------------------------------- | --------------------------------------------- |
| Promise<[LockStatusResponse](#lockstatusresponse7)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.alterPin(0, "1234", "0000").then((data: sim.LockStatusResponse) => {
    console.log(`alterPin success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`alterPin failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.alterPin2<sup>8+</sup>

alterPin2\(slotId: number, newPin2: string, oldPin2: string, callback: AsyncCallback\<LockStatusResponse\>\): void

Changes PIN 2 of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                       | Mandatory| Description                                  |
| -------- | ----------------------------------------------------------- | ---- | -------------------------------------- |
| slotId   | number                                                      | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<[LockStatusResponse](#lockstatusresponse7)\> | Yes  | Callback used to return the result.                            |
| newPin2  | string                                                      | Yes  | New PIN.                              |
| oldPin2  | string                                                      | Yes  | Old PIN.                              |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.alterPin2(0, "1234", "0000", (err: BusinessError, data: sim.LockStatusResponse) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.alterPin2<sup>8+</sup>

alterPin2\(slotId: number, newPin2: string, oldPin2: string\): Promise\<LockStatusResponse\>

Changes PIN 2 of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name | Type  | Mandatory| Description                                  |
| ------- | ------ | ---- | -------------------------------------- |
| slotId  | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| newPin2 | string | Yes  | New PIN.                              |
| oldPin2 | string | Yes  | Old PIN.                              |

**Return value**

| Type                                                | Description                                         |
| ---------------------------------------------------- | --------------------------------------------- |
| Promise<[LockStatusResponse](#lockstatusresponse7)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.alterPin2(0, "1234", "0000").then((data: sim.LockStatusResponse) => {
    console.log(`alterPin2 success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`alterPin2 failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.unlockPin<sup>7+</sup>

unlockPin\(slotId: number, pin: string, callback: AsyncCallback\<LockStatusResponse\>\): void

Unlocks the PIN of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                  |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------------- |
| slotId   | number                                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| pin      | string                                                       | Yes  | PIN of the SIM card.                           |
| callback | AsyncCallback&lt;[LockStatusResponse](#lockstatusresponse7)> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let pin: string = '1234';
sim.unlockPin(0, pin, (err: BusinessError, data: sim.LockStatusResponse) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.unlockPin<sup>7+</sup>

unlockPin\(slotId: number, pin: string\): Promise\<LockStatusResponse\>

Unlocks the PIN of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| pin    | string | Yes  | PIN of the SIM card.                           |

**Return value**

| Type                                                | Description                                              |
| ---------------------------------------------------- | -------------------------------------------------- |
| Promise\<[LockStatusResponse](#lockstatusresponse7)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let pin: string = '1234';
sim.unlockPin(0, pin).then((data: sim.LockStatusResponse) => {
    console.log(`unlockPin success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`unlockPin failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.unlockPuk<sup>7+</sup>

unlockPuk\(slotId: number, newPin: string, puk: string, callback: AsyncCallback\<LockStatusResponse\>\): void

Unlocks the PUK of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                  |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------------- |
| slotId   | number                                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| newPin   | string                                                       | Yes  | New PIN.                       |
| puk      | string                                                       | Yes  | PUK of the SIM card.                   |
| callback | AsyncCallback&lt;[LockStatusResponse](#lockstatusresponse7)&gt; | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let puk: string = '1xxxxxxx';
let newPin: string = '1235';
sim.unlockPuk(0, newPin, puk, (err: BusinessError, data: sim.LockStatusResponse) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.unlockPuk<sup>7+</sup>

unlockPuk\(slotId: number, newPin: string, puk: string\): Promise\<LockStatusResponse\>

Unlocks the PUK of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| newPin | string | Yes  | New PIN.                       |
| puk    | string | Yes  | PUK of the SIM card.                   |

**Return value**

| Type                                                | Description                                              |
| ---------------------------------------------------- | -------------------------------------------------- |
| Promise\<[LockStatusResponse](#lockstatusresponse7)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let puk: string = '1xxxxxxx';
let newPin: string = '1235';
sim.unlockPuk(0, newPin, puk).then((data: sim.LockStatusResponse) => {
    console.log(`unlockPuk success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`unlockPuk failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.unlockPin2<sup>8+</sup>

unlockPin2\(slotId: number, pin2: string, callback: AsyncCallback\<LockStatusResponse\>\): void

Unlocks the PIN of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                  |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------------- |
| slotId   | number                                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| pin2     | string                                                       | Yes  | PIN of the SIM card.                           |
| callback | AsyncCallback&lt;[LockStatusResponse](#lockstatusresponse7)&gt; | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let pin2: string = '1234';
sim.unlockPin2(0, pin2, (err: BusinessError, data: sim.LockStatusResponse) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.unlockPin2<sup>8+</sup>

unlockPin2\(slotId: number, pin2: string\): Promise\<LockStatusResponse\>

Unlocks the PIN of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| pin2   | string | Yes  | PIN of the SIM card.                           |

**Return value**

| Type                                                 | Description                                              |
| ----------------------------------------------------- | -------------------------------------------------- |
| Promise\<[LockStatusResponse](#lockstatusresponse7)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let pin2: string = '1234';
sim.unlockPin2(0, pin2).then((data: sim.LockStatusResponse) => {
    console.log(`unlockPin2 success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`unlockPin2 failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.unlockPuk2<sup>8+</sup>

unlockPuk2\(slotId: number, newPin2: string, puk2: string, callback: AsyncCallback\<LockStatusResponse\>\): void

Unlocks the PUK of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                  |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------------- |
| slotId   | number                                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| newPin2  | string                                                       | Yes  | New PIN 2.                       |
| puk2     | string                                                       | Yes  | PUK of the SIM card.                   |
| callback | AsyncCallback&lt;[LockStatusResponse](#lockstatusresponse7)&gt; | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let puk2: string = '1xxxxxxx';
let newPin2: string = '1235';
sim.unlockPuk2(0, newPin2, puk2, (err: BusinessError, data: sim.LockStatusResponse) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.unlockPuk2<sup>8+</sup>

unlockPuk2\(slotId: number, newPin2: string, puk2: string\): Promise\<LockStatusResponse\>

Unlocks the PUK of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name | Type  | Mandatory| Description                                  |
| ------- | ------ | ---- | -------------------------------------- |
| slotId  | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| newPin2 | string | Yes  | New PIN 2.                       |
| puk2    | string | Yes  | PUK of the SIM card.                   |

**Return value**

| Type                                                | Description                                              |
| ---------------------------------------------------- | -------------------------------------------------- |
| Promise\<[LockStatusResponse](#lockstatusresponse7)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let puk2: string = '1xxxxxxx';
let newPin2: string = '1235';
sim.unlockPuk2(0, newPin2, puk2).then((data: sim.LockStatusResponse) => {
    console.log(`unlockPuk2 success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`unlockPuk2 failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getMaxSimCount<sup>7+</sup>

getMaxSimCount\(\): number

Obtains the number of card slots.

**System capability**: SystemCapability.Telephony.CoreService

**Return value**

| Type             | Description                                                        |
| ----------------- | ------------------------------------------------------------ |
| number | Number of card slots.|

**Example**

```ts
import sim from '@ohos.telephony.sim';

console.log("Result: "+ sim.getMaxSimCount());
```

## sim.getSimIccId<sup>7+</sup>

getSimIccId\(slotId: number, callback: AsyncCallback\<string\>\): void

Obtains the ICCID of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                  | Mandatory| Description                                  |
| -------- | ---------------------- | ---- | -------------------------------------- |
| slotId   | number                 | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback<string\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getSimIccId(0, (err: BusinessError, data: string) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getSimIccId<sup>7+</sup>

getSimIccId\(slotId: number\): Promise\<string\>

Obtains the ICCID of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type            | Description                                       |
| ---------------- | ------------------------------------------- |
| Promise<string\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getSimIccId(0).then((data:string) => {
    console.log(`getSimIccId success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getSimIccId failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getVoiceMailIdentifier<sup>8+</sup>

getVoiceMailIdentifier\(slotId: number, callback: AsyncCallback\<string\>\): void

Obtains the voice mailbox alpha identifier of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                  | Mandatory| Description                                  |
| -------- | ---------------------- | ---- | -------------------------------------- |
| slotId   | number                 | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback<string\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getVoiceMailIdentifier(0, (err: BusinessError, data: string) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getVoiceMailIdentifier<sup>8+</sup>

getVoiceMailIdentifier\(slotId: number\): Promise\<string\>

Obtains the voice mailbox alpha identifier of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type            | Description                                             |
| ---------------- | ------------------------------------------------- |
| Promise<string\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getVoiceMailIdentifier(0).then((data: string) => {
    console.log(`getVoiceMailIdentifier success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getVoiceMailIdentifier failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getVoiceMailNumber<sup>8+</sup>

getVoiceMailNumber\(slotId: number, callback: AsyncCallback\<string\>): void

Obtains the voice mailbox number of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                  | Mandatory| Description                                  |
| -------- | ---------------------- | ---- | -------------------------------------- |
| slotId   | number                 | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback<string\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getVoiceMailNumber(0, (err: BusinessError, data: string) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getVoiceMailNumber<sup>8+</sup>

getVoiceMailNumber\(slotId: number\): Promise\<string\>

Obtains the voice mailbox number of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type            | Description                                            |
| ---------------- | ------------------------------------------------ |
| Promise<string\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getVoiceMailNumber(0).then((data: string) => {
    console.log(`getVoiceMailNumber success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getVoiceMailNumber failed, promise: err->${JSON.stringify(err)}`);
});
```


## sim.setVoiceMailInfo<sup>8+</sup>

setVoiceMailInfo\(slotId: number, mailName: string, mailNumber: string, callback: AsyncCallback\<void\>\): void

Sets voice mailbox information for the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name    | Type                | Mandatory| Description                                  |
| ---------- | -------------------- | ---- | -------------------------------------- |
| slotId     | number               | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| mailName   | string               | Yes  | Voice mailbox name.                              |
| mailNumber | string               | Yes  | Voice mailbox number.                              |
| callback   | AsyncCallback<void\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.setVoiceMailInfo(0, "mail", "xxx@xxx.com", (err: BusinessError) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## sim.setVoiceMailInfo<sup>8+</sup>

setVoiceMailInfo\(slotId: number, mailName: string, mailNumber: string\): Promise\<void\>

Sets voice mailbox information for the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name    | Type  | Mandatory| Description                                  |
| ---------- | ------ | ---- | -------------------------------------- |
| slotId     | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| mailName   | string | Yes  | Voice mailbox name.                              |
| mailNumber | string | Yes  | Voice mailbox number.                              |

**Return value**

| Type          | Description                   |
| -------------- | ----------------------- |
| Promise<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.setVoiceMailInfo(0, "mail", "xxx@xxx.com").then(() => {
    console.log(`setVoiceMailInfo success.`);
}).catch((err: BusinessError) => {
    console.error(`setVoiceMailInfo failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getSimTelephoneNumber<sup>8+</sup>

getSimTelephoneNumber\(slotId: number, callback: AsyncCallback\<string\>\): void

Obtains the MSISDN of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_PHONE_NUMBERS

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                  | Mandatory| Description                                  |
| -------- | ---------------------- | ---- | -------------------------------------- |
| slotId   | number                 | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback<string\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getSimTelephoneNumber(0, (err: BusinessError, data: string) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getSimTelephoneNumber<sup>8+</sup>

getSimTelephoneNumber\(slotId: number\): Promise\<string\>

Obtains the MSISDN of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_PHONE_NUMBERS

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type            | Description                                        |
| ---------------- | -------------------------------------------- |
| Promise<string\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getSimTelephoneNumber(0).then((data: string) => {
    console.log(`getSimTelephoneNumber success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getSimTelephoneNumber failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getSimGid1<sup>7+</sup>

getSimGid1\(slotId: number, callback: AsyncCallback\<string\>\): void

Obtains the group identifier level 1 (GID1) of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                   | Mandatory| Description                                  |
| -------- | ----------------------- | ---- | -------------------------------------- |
| slotId   | number                  | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<string\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getSimGid1(0, (err: BusinessError, data: string) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getSimGid1<sup>7+</sup>

getSimGid1\(slotId: number\): Promise\<string\>

Obtains the GID1 of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type            | Description                                             |
| ---------------- | ------------------------------------------------- |
| Promise<string\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getSimGid1(0).then((data: string) => {
    console.log(`getSimGid1 success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getSimGid1 failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getIMSI

getIMSI\(slotId: number, callback: AsyncCallback\<string\>\): void

Obtains the international mobile subscriber identity (IMSI) of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                   | Mandatory| Description                                  |
| -------- | ----------------------- | ---- | -------------------------------------- |
| slotId   | number                  | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<string\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getIMSI(0, (err: BusinessError, data: string) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getIMSI

getIMSI\(slotId: number\): Promise\<string\>

Obtains the IMSI of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type            | Description                                       |
| ---------------- | ------------------------------------------- |
| Promise<string\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getIMSI(0).then((data: string) => {
    console.log(`getIMSI success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getIMSI failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getOperatorConfigs<sup>8+</sup>

getOperatorConfigs\(slotId: number, callback: AsyncCallback\<Array\<OperatorConfig\>\>\): void

Obtains the carrier configuration of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                     | Mandatory| Description                                  |
| -------- | --------------------------------------------------------- | ---- | -------------------------------------- |
| slotId   | number                                                    | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback<Array<[OperatorConfig](#operatorconfig8)\>> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getOperatorConfigs(0, (err: BusinessError, data: Array<sim.OperatorConfig>) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.getOperatorConfigs<sup>8+</sup>

getOperatorConfigs\(slotId: number\): Promise\<Array\<OperatorConfig\>\>

Obtains the carrier configuration of the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                                               | Description                         |
| --------------------------------------------------- | ----------------------------- |
| Promise<Array<[OperatorConfig](#operatorconfig8)\>> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getOperatorConfigs(0).then((data: Array<sim.OperatorConfig>) => {
    console.log(`getOperatorConfigs success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getOperatorConfigs failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.queryIccDiallingNumbers<sup>8+</sup>

queryIccDiallingNumbers\(slotId: number, type: ContactType, callback: AsyncCallback\<Array\<DiallingNumbersInfo\>\>\): void

Queries contact numbers of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

>**NOTE**
>
>A cache mechanism is available for SIM card contacts. When a contact is added, deleted, or modified, a SIM card contact cache is maintained based on the corresponding card slot ID and contact type. Therefore, when calling **sim.queryIccDiallingNumbers** to query contact numbers, you must pass the card slot ID and contact type to generate a a SIM card contact cache first. If no cache is generated, the attempt to call the **sim.addIccDiallingNumbers**, **sim.delIccDiallingNumbers**, or **sim.updateIccDiallingNumbers** API will fail.
>

**System API**: This is a system API.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                                      |
| -------- | ------------------------------------------------------------ | ---- | ---------------------------------------------------------- |
| slotId   | number                                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2                    |
| type     | [ContactType](#contacttype8)                                 | Yes  | Contact type.<br>- **1**: GENERAL_CONTACT<br>- **2**: FIXED_DIALING|
| callback | AsyncCallback<Array<[DiallingNumbersInfo](#diallingnumbersinfo8)\>> | Yes  | Callback used to return the result.                                         |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.queryIccDiallingNumbers(0, 1, (err: BusinessError, data: Array<sim.DiallingNumbersInfo>) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.queryIccDiallingNumbers<sup>8+</sup>

queryIccDiallingNumbers\(slotId: number, type: ContactType\): Promise\<Array\<DiallingNumbersInfo\>\>

Queries contact numbers of the SIM card in the specified slot. This API uses a promise to return the result.

>**NOTE**
>
>A cache mechanism is available for SIM card contacts. When a contact is added, deleted, or modified, a SIM card contact cache is maintained based on the corresponding card slot ID and contact type. Therefore, when calling **sim.queryIccDiallingNumbers** to query contact numbers, you must pass the card slot ID and contact type to generate a a SIM card contact cache. If no cache is generated, the attempt to call the **sim.addIccDiallingNumbers**, **sim.delIccDiallingNumbers**, or **sim.updateIccDiallingNumbers** API will fail.
>

**System API**: This is a system API.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type       | Mandatory| Description                                                      |
| ------ | ----------- | ---- | ---------------------------------------------------------- |
| slotId | number      | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2                    |
| type   | [ContactType](#contacttype8)  | Yes  | Contact type.<br>- **1**: GENERAL_CONTACT<br>- **2**: FIXED_DIALING|

**Return value**

| Type                                                        | Description                          |
| ------------------------------------------------------------ | ------------------------------ |
| Promise<Array<[DiallingNumbersInfo](#diallingnumbersinfo8)\>> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.queryIccDiallingNumbers(0, 1).then((data:  Array<sim.DiallingNumbersInfo>) => {
    console.log(`queryIccDiallingNumbers success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`queryIccDiallingNumbers failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.addIccDiallingNumbers<sup>8+</sup>

addIccDiallingNumbers\(slotId: number, type: ContactType, diallingNumbers: DiallingNumbersInfo, callback: AsyncCallback\<void\>\): void

Adds contact numbers to the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

>**NOTE**
>
>A cache mechanism is available for SIM card contacts. When a contact is added, deleted, or modified, a SIM card contact cache is maintained based on the corresponding card slot ID and contact type. Therefore, when calling **sim.queryIccDiallingNumbers** to query contact numbers, you must pass the card slot ID and contact type to generate a a SIM card contact cache. If no cache is generated, the attempt to call the **sim.addIccDiallingNumbers**, **sim.delIccDiallingNumbers**, or **sim.updateIccDiallingNumbers** API will fail.
>

**System API**: This is a system API.

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name         | Type                                        | Mandatory| Description                                                      |
| --------------- | -------------------------------------------- | ---- | ---------------------------------------------------------- |
| slotId          | number                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2                    |
| type            | [ContactType](#contacttype8)                 | Yes  | Contact type.<br>- **1**: GENERAL_CONTACT<br>- **2**: FIXED_DIALING |
| diallingNumbers | [DiallingNumbersInfo](#diallingnumbersinfo8) | Yes  | Contact number information.                                              |
| callback        | AsyncCallback<void\>                         | Yes  | Callback used to return the result.                                                  |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let diallingNumbersInof: sim.DiallingNumbersInfo = {
    alphaTag: "alpha",
    number: "138xxxxxxxx",
    pin2: "1234"
};
sim.addIccDiallingNumbers(0, sim.ContactType.GENERAL_CONTACT, diallingNumbersInof, (err: BusinessError) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## sim.addIccDiallingNumbers<sup>8+</sup>

addIccDiallingNumbers\(slotId: number, type: ContactType, diallingNumbers: DiallingNumbersInfo\): Promise\<void\>

Adds contact numbers to the SIM card in the specified slot. This API uses a promise to return the result.

>**NOTE**
>
>A cache mechanism is available for SIM card contacts. When a contact is added, deleted, or modified, a SIM card contact cache is maintained based on the corresponding card slot ID and contact type. Therefore, when calling **sim.queryIccDiallingNumbers** to query contact numbers, you must pass the card slot ID and contact type to generate a a SIM card contact cache. If no cache is generated, the attempt to call the **sim.addIccDiallingNumbers**, **sim.delIccDiallingNumbers**, or **sim.updateIccDiallingNumbers** API will fail.
>

**System API**: This is a system API.

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name         | Type                                        | Mandatory| Description                                                      |
| --------------- | -------------------------------------------- | ---- | ---------------------------------------------------------- |
| slotId          | number                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2                    |
| type            | [ContactType](#contacttype8)                 | Yes  | Contact type.<br>- **1**: GENERAL_CONTACT<br>- **2**: FIXED_DIALING |
| diallingNumbers | [DiallingNumbersInfo](#diallingnumbersinfo8) | Yes  | Contact number information.                                              |

**Return value**

| Type          | Description                       |
| -------------- | --------------------------- |
| Promise<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let diallingNumbersInof: sim.DiallingNumbersInfo = {
    alphaTag: "alpha",
    number: "138xxxxxxxx"
};
sim.addIccDiallingNumbers(0, sim.ContactType.GENERAL_CONTACT, diallingNumbersInof).then(() => {
    console.log(`addIccDiallingNumbers success.`);
}).catch((err: BusinessError) => {
    console.error(`addIccDiallingNumbers failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.delIccDiallingNumbers<sup>8+</sup>

delIccDiallingNumbers\(slotId: number, type: ContactType, diallingNumbers: DiallingNumbersInfo, callback: AsyncCallback\<void\>\): void

Deletes contact numbers from the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

>**NOTE**
>
>A cache mechanism is available for SIM card contacts. When a contact is added, deleted, or modified, a SIM card contact cache is maintained based on the corresponding card slot ID and contact type. Therefore, when calling **sim.queryIccDiallingNumbers** to query contact numbers, you must pass the card slot ID and contact type to generate a a SIM card contact cache. If no cache is generated, the attempt to call the **sim.addIccDiallingNumbers**, **sim.delIccDiallingNumbers**, or **sim.updateIccDiallingNumbers** API will fail.
>

**System API**: This is a system API.

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name         | Type                                        | Mandatory| Description                                                      |
| --------------- | -------------------------------------------- | ---- | ---------------------------------------------------------- |
| slotId          | number                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2                    |
| type            | [ContactType](#contacttype8)                 | Yes  | Contact type.<br>- **1**: GENERAL_CONTACT<br>- **2**: FIXED_DIALING |
| diallingNumbers | [DiallingNumbersInfo](#diallingnumbersinfo8) | Yes  | Contact number information.                                              |
| callback        | AsyncCallback<void\>                         | Yes  | Callback used to return the result.                                                  |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let diallingNumbersInof: sim.DiallingNumbersInfo = {
    alphaTag: "alpha",
    number: "138xxxxxxxx",
    recordNumber: 123,
    pin2: "1234"
};
sim.delIccDiallingNumbers(0, sim.ContactType.GENERAL_CONTACT, diallingNumbersInof, (err: BusinessError) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## sim.delIccDiallingNumbers<sup>8+</sup>

delIccDiallingNumbers\(slotId: number, type: ContactType, diallingNumbers: DiallingNumbersInfo\): Promise\<void\>

Deletes contact numbers from the SIM card in the specified slot. This API uses a promise to return the result.

>**NOTE**
>
>A cache mechanism is available for SIM card contacts. When a contact is added, deleted, or modified, a SIM card contact cache is maintained based on the corresponding card slot ID and contact type. Therefore, when calling **sim.queryIccDiallingNumbers** to query contact numbers, you must pass the card slot ID and contact type to generate a a SIM card contact cache. If no cache is generated, the attempt to call the **sim.addIccDiallingNumbers**, **sim.delIccDiallingNumbers**, or **sim.updateIccDiallingNumbers** API will fail.
>

**System API**: This is a system API.

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name         | Type                                        | Mandatory| Description                                                      |
| --------------- | -------------------------------------------- | ---- | ---------------------------------------------------------- |
| slotId          | number                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2                    |
| type            | [ContactType](#contacttype8)                 | Yes  | Contact type.<br>- **1**: GENERAL_CONTACT<br>- **2**: FIXED_DIALING |
| diallingNumbers | [DiallingNumbersInfo](#diallingnumbersinfo8) | Yes  | Contact number information.                                              |

**Return value**

| Type          | Description                       |
| -------------- | --------------------------- |
| Promise<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let diallingNumbersInof: sim.DiallingNumbersInfo = {
    alphaTag: "alpha",
    number: "138xxxxxxxx"
};
sim.delIccDiallingNumbers(0, sim.ContactType.GENERAL_CONTACT, diallingNumbersInof).then(() => {
    console.log(`delIccDiallingNumbers success.`);
}).catch((err: BusinessError) => {
    console.error(`delIccDiallingNumbers failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.updateIccDiallingNumbers<sup>8+</sup>

updateIccDiallingNumbers\(slotId: number, type: ContactType, diallingNumbers: DiallingNumbersInfo, callback: AsyncCallback\<void\>\): void

Updates contact numbers for the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

>**NOTE**
>
>A cache mechanism is available for SIM card contacts. When a contact is added, deleted, or modified, a SIM card contact cache is maintained based on the corresponding card slot ID and contact type. Therefore, when calling **sim.queryIccDiallingNumbers** to query contact numbers, you must pass the card slot ID and contact type to generate a a SIM card contact cache. If no cache is generated, the attempt to call the **sim.addIccDiallingNumbers**, **sim.delIccDiallingNumbers**, or **sim.updateIccDiallingNumbers** API will fail.
>

**System API**: This is a system API.

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name         | Type                                        | Mandatory| Description                                                      |
| --------------- | -------------------------------------------- | ---- | ---------------------------------------------------------- |
| slotId          | number                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2                    |
| type            | [ContactType](#contacttype8)                 | Yes  | Contact type.<br>- **1**: GENERAL_CONTACT<br>- **2**: FIXED_DIALING |
| diallingNumbers | [DiallingNumbersInfo](#diallingnumbersinfo8) | Yes  | Contact number information.                                              |
| callback        | AsyncCallback<void\>                         | Yes  | Callback used to return the result.                                                  |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let diallingNumbersInof: sim.DiallingNumbersInfo = {
    alphaTag: "alpha",
    number: "138xxxxxxxx",
    recordNumber: 123,
    pin2: "1234"
};
sim.updateIccDiallingNumbers(0, sim.ContactType.GENERAL_CONTACT, diallingNumbersInof, (err: BusinessError) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## sim.updateIccDiallingNumbers<sup>8+</sup>

updateIccDiallingNumbers\(slotId: number, type: ContactType, diallingNumbers: DiallingNumbersInfo\): Promise\<void\>

Updates contact numbers for the SIM card in the specified slot. This API uses a promise to return the result.

>**NOTE**
>
>A cache mechanism is available for SIM card contacts. When a contact is added, deleted, or modified, a SIM card contact cache is maintained based on the corresponding card slot ID and contact type. Therefore, when calling **sim.queryIccDiallingNumbers** to query contact numbers, you must pass the card slot ID and contact type to generate a a SIM card contact cache. If no cache is generated, the attempt to call the **sim.addIccDiallingNumbers**, **sim.delIccDiallingNumbers**, or **sim.updateIccDiallingNumbers** API will fail.
>

**System API**: This is a system API.

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name         | Type                                        | Mandatory| Description                                                      |
| --------------- | -------------------------------------------- | ---- | ---------------------------------------------------------- |
| slotId          | number                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2                    |
| type            | [ContactType](#contacttype8)                 | Yes  | Contact type.<br>- **1**: GENERAL_CONTACT<br>- **2**: FIXED_DIALING |
| diallingNumbers | [DiallingNumbersInfo](#diallingnumbersinfo8) | Yes  | Contact number information.                                              |

**Return value**

| Type          | Description                         |
| -------------- | ----------------------------- |
| Promise<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let diallingNumbersInof: sim.DiallingNumbersInfo = {
    alphaTag: "alpha",
    number: "138xxxxxxxx",
    recordNumber: 123
};
sim.updateIccDiallingNumbers(0, sim.ContactType.GENERAL_CONTACT, diallingNumbersInof).then(() => {
    console.log(`updateIccDiallingNumbers success.`);
}).catch((err: BusinessError) => {
    console.error(`updateIccDiallingNumbers failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.sendEnvelopeCmd<sup>8+</sup>

sendEnvelopeCmd\(slotId: number, cmd: string, callback: AsyncCallback\<void\>\): void

Sends an envelope command to the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                | Mandatory| Description                                  |
| -------- | -------------------- | ---- | -------------------------------------- |
| slotId   | number               | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| cmd      | string               | Yes  | Envelope command.                                  |
| callback | AsyncCallback<void\> | Yes  | Callback used to return the result.                                    |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.sendEnvelopeCmd(0, "ls", (err: BusinessError) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## sim.sendEnvelopeCmd<sup>8+</sup>

sendEnvelopeCmd\(slotId: number, cmd: string\): Promise\<void\>

Sends an envelope command to the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| cmd    | string | Yes  | Envelope command.                                  |

**Return value**

| Type          | Description                       |
| -------------- | --------------------------- |
| Promise<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.sendEnvelopeCmd(0, "ls").then(() => {
    console.log(`sendEnvelopeCmd success.`);
}).catch((err: BusinessError) => {
    console.error(`sendEnvelopeCmd failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.sendTerminalResponseCmd<sup>8+</sup>

sendTerminalResponseCmd\(slotId: number, cmd: string, callback: AsyncCallback\<void\>\): void

Sends a terminal response command to the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                | Mandatory| Description                                  |
| -------- | -------------------- | ---- | -------------------------------------- |
| slotId   | number               | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| cmd      | string               | Yes  | Envelope command.                                  |
| callback | AsyncCallback<void\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.sendTerminalResponseCmd(0, "ls", (err: BusinessError) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## sim.sendTerminalResponseCmd<sup>8+</sup>

sendTerminalResponseCmd\(slotId: number, cmd: string\): Promise\<void\>

Sends a terminal response command to the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| cmd    | string | Yes  | Envelope command.                                  |

**Return value**

| Type          | Description                       |
| -------------- | --------------------------- |
| Promise<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.sendTerminalResponseCmd(0, "ls").then(() => {
    console.log(`sendTerminalResponseCmd success.`);
}).catch((err: BusinessError) => {
    console.error(`sendTerminalResponseCmd failed, promise: err->${JSON.stringify(err)}`);
});
```


## sim.unlockSimLock<sup>8+</sup>

unlockSimLock\(slotId: number, lockInfo: PersoLockInfo, callback: AsyncCallback\<LockStatusResponse\>\): void

Unlocks the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                      | Mandatory| Description                                  |
| -------- | ---------------------------------------------------------- | ---- | -------------------------------------- |
| slotId   | number                                                     | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| lockInfo | [PersoLockInfo](#persolockinfo8)                           | Yes  | Personalized lock information.                        |
| callback | AsyncCallback<[LockStatusResponse](#lockstatusresponse7)\> | Yes  | Callback used to return the result.                              |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let persoLockInfo: sim.PersoLockInfo = {
    lockType: sim.PersoLockType.PN_PIN_LOCK,
    password: "1234"
};
sim.unlockSimLock(0, persoLockInfo, (err: BusinessError, data: sim.LockStatusResponse) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## sim.unlockSimLock<sup>8+</sup>

unlockSimLock\(slotId: number, lockInfo: PersoLockInfo\): Promise\<LockStatusResponse\>

Unlocks the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                            | Mandatory| Description                                  |
| -------- | -------------------------------- | ---- | -------------------------------------- |
| slotId   | number                           | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| lockInfo | [PersoLockInfo](#persolockinfo8) | Yes  | Personalized lock information.                        |

**Return value**

| Type                                                | Description                     |
| ---------------------------------------------------- | ------------------------- |
| Promise<[LockStatusResponse](#lockstatusresponse7)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301002  | SIM card operation error.                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let persoLockInfo: sim.PersoLockInfo = {
    lockType: sim.PersoLockType.PN_PIN_LOCK,
    password: "1234"
};
sim.unlockSimLock(0, persoLockInfo).then((data: sim.LockStatusResponse) => {
    console.log(`unlockSimLock success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`unlockSimLock failed, promise: err->${JSON.stringify(err)}`);
});
```

## sim.getOpKey<sup>9+</sup>

getOpKey\(slotId: number, callback: AsyncCallback\<string\>): void

Obtains the opkey of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                  | Mandatory| Description                                  |
| -------- | ---------------------- | ---- | -------------------------------------- |
| slotId   | number                 | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback<string\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 801      | Capability not supported.                    |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

try {
    sim.getOpKey(0, (err: BusinessError, data: string) => {
    if (err) {
      console.error("getOpKey failed, err: " + JSON.stringify(err));
    } else {
      console.log('getOpKey successfully, data: ' + JSON.stringify(data));
    }
  });
} catch (err) {
  console.error("getOpKey err: " + JSON.stringify(err));
}
```


## sim.getOpKey<sup>9+</sup>

getOpKey\(slotId: number\): Promise\<string\>

Obtains the opkey of the SIM card in the specified slot. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type            | Description                                     |
| ---------------- | ----------------------------------------- |
| Promise<string\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 801      | Capability not supported.                    |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

try {
    let data: Promise<string> = sim.getOpKey(0);
    console.log(`getOpKey success, promise: data->${JSON.stringify(data)}`);
} catch (error) {
    console.error(`getOpKey failed, promise: err->${JSON.stringify(error)}`);
}
```

## sim.getOpKeySync<sup>10+</sup>

getOpKeySync\(slotId: number\): string

Obtains the opkey of the SIM card in the specified slot.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type            | Description                                     |
| ---------------- | ----------------------------------------- |
| string | opkey of the SIM card in the specified slot.|


**Example**

```js
let data = sim.getOpKeySync(0);
console.log(`getOpKey success, promise: data->${JSON.stringify(data)}`);
```

## sim.getOpName<sup>9+</sup>

getOpName\(slotId: number, callback: AsyncCallback\<string\>\): void

Obtains the OpName of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                  | Mandatory| Description                                  |
| -------- | ---------------------- | ---- | -------------------------------------- |
| slotId   | number                 | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback<string\> | Yes  | Callback used to return the result.                              |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 801      | Capability not supported.                    |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

try {
    sim.getOpName(0, (err: BusinessError, data: string) => {
    if (err) {
      console.error("getOpName failed, err: " + JSON.stringify(err));
    } else {
      console.log('getOpName successfully, data: ' + JSON.stringify(data));
    }
  });
} catch (err) {
  console.error("getOpName err: " + JSON.stringify(err));
}
```


## sim.getOpName<sup>9+</sup>

getOpName\(slotId: number\): Promise\<string\>

Obtains the OpName of the SIM card in the specified slot. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type            | Description                                      |
| ---------------- | ------------------------------------------ |
| Promise<string\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 801      | Capability not supported.                    |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

try {
    let data: Promise<string> = sim.getOpName(0);
    console.log(`getOpName success, promise: data->${JSON.stringify(data)}`);
} catch (error) {
    console.error(`getOpName failed, promise: err->${JSON.stringify(error)}`);
}
```

## sim.getOpNameSync<sup>10+</sup>

getOpNameSync\(slotId: number\): string

Obtains the OpName of the SIM card in the specified slot.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type            | Description                                      |
| ---------------- | ------------------------------------------ |
| string | OpName of the SIM card in the specified slot.|


**Example**

```js
let data = sim.getOpNameSync(0);
console.log(`getOpName success, promise: data->${JSON.stringify(data)}`);
```

## sim.getDefaultVoiceSimId<sup>10+</sup>

getDefaultVoiceSimId\(callback: AsyncCallback\<number\>\): void

Obtains the default slot ID of the SIM card that provides voice services. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                       | Mandatory| Description      |
| -------- | --------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;number&gt; | Yes  | Callback used to return the result.<br>The return value is bound to the SIM card and increases from 1.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301001  | SIM card is not activated.                   |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

sim.getDefaultVoiceSimId((err: BusinessError, data: number) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```

## sim.getDefaultVoiceSimId<sup>10+</sup>

getDefaultVoiceSimId\(\): Promise\<number\>

Obtains the default slot ID of the SIM card that provides voice services. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Return value**

| Type             | Description                                   |
| ----------------- | --------------------------------------- |
| Promise\<number\> | Promise used to return the result.<br>The return value is bound to the SIM card and increases from 1.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301001  | SIM card is not activated.                   |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import sim from '@ohos.telephony.sim';

let promise = sim.getDefaultVoiceSimId();
promise.then((data: number) => {
    console.log(`getDefaultVoiceSimId success, promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
    console.error(`getDefaultVoiceSimId failed, promise: err->${JSON.stringify(err)}`);
});
```

## SimState

Enumerates SIM card states.

**System capability**: SystemCapability.Telephony.CoreService

| Name                 | Value  | Description                                                      |
| --------------------- | ---- | ---------------------------------------------------------- |
| SIM_STATE_UNKNOWN     | 0    | The SIM card is in **unknown** state; that is, the SIM card status cannot be obtained.                     |
| SIM_STATE_NOT_PRESENT | 1    | The SIM card is in **not present** state; that is, no SIM card is inserted into the card slot.     |
| SIM_STATE_LOCKED      | 2    | The SIM card is in **locked** state; that is, the SIM card is locked by the personal identification number (PIN), PIN unblocking key (PUK), or network.  |
| SIM_STATE_NOT_READY   | 3    | The SIM card is in **not ready** state; that is, the SIM card has been installed but cannot work properly.   |
| SIM_STATE_READY       | 4    | The SIM card is in **ready** state; that is, the SIM card has been installed and is working properly.           |
| SIM_STATE_LOADED      | 5    | The SIM card is in **loaded** state; that is, the SIM card is present and all its files have been loaded.|

## CardType<sup>7+</sup>

Enumerates SIM card types.

**System capability**: SystemCapability.Telephony.CoreService

| Name| Value| Description|
| ----- | ----- | ----- |
|UNKNOWN_CARD | -1 | Unknown type.|
|SINGLE_MODE_SIM_CARD | 10 | Single-card (SIM).|
|SINGLE_MODE_USIM_CARD | 20 | Single-card (USIM).|
|SINGLE_MODE_RUIM_CARD | 30 | Single-card (RUIM).|
|DUAL_MODE_CG_CARD | 40 | Dual-card (CDMA+GSM).|
|CT_NATIONAL_ROAMING_CARD | 41 | China Telecom internal roaming card.|
|CU_DUAL_MODE_CARD | 42 | China Unicom dual-mode card.|
|DUAL_MODE_TELECOM_LTE_CARD | 43 | China Telecom dual-mode LTE card.|
|DUAL_MODE_UG_CARD | 50 | Dual-mode card (UMTS+GSM).|
|SINGLE_MODE_ISIM_CARD<sup>8+</sup> | 60 | Single-card (ISIM).|

## LockType<sup>8+</sup>

Enumerates lock types.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name    | Value  | Description       |
| -------- | ---- | ----------- |
| PIN_LOCK | 1    | SIM card password lock.|
| FDN_LOCK | 2    | Fixed dialing lock. |

## LockState<sup>8+</sup>

Enumerates lock states.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name    | Value  | Description      |
| -------- | ---- | ---------- |
| LOCK_OFF | 0    | The lock is off.|
| LOCK_ON  | 1    | The lock is on.|

## PersoLockType<sup>8+</sup>

Enumerates personalized lock types.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name        | Value  | Description                                            |
| ------------ | ---- | ------------------------------------------------ |
| PN_PIN_LOCK  | 0    | Personalized network PIN lock. For details, see *3GPP TS 22.022 [33]*.        |
| PN_PUK_LOCK  | 1    | Personalized network PUK lock.                                  |
| PU_PIN_LOCK  | 2    | Personalized network subset PIN lock. For details, see *3GPP TS 22.022 [33]*.    |
| PU_PUK_LOCK  | 3    | Personalized network subset PUK lock.                              |
| PP_PIN_LOCK  | 4    | Personalized service provider PIN lock. For details, see *3GPP TS 22.022 [33]*.  |
| PP_PUK_LOCK  | 5    | Personalized service provider PUK lock.                             |
| PC_PIN_LOCK  | 6    | Personalized corporate PIN lock. For details, see *3GPP TS 22.022 [33]*.        |
| PC_PUK_LOCK  | 7    | Personalized corporate PUK lock.                                   |
| SIM_PIN_LOCK | 8    | Personalized SIM card PIN lock. For details, see *3GPP TS 22.022 [33]*.       |
| SIM_PUK_LOCK | 9    | Personalized SIM card PUK lock.                                  |

## LockStatusResponse<sup>7+</sup>

Defines the personalized lock information.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name           | Type  | Mandatory| Description                 |
| --------------- | ------ | ---- | --------------------- |
| result          | number |  Yes | Operation result.     |
| remain          | number |  No | Remaining attempts (can be null).|

## LockInfo<sup>8+</sup>

Defines the personalized lock information.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name    |           Type          | Mandatory|   Description  |
| -------- | ------------------------ | ---- | -------- |
| lockType | [LockType](#locktype8)   |  Yes | Lock type.|
| password | string                   |  Yes | Password.  |
| state    | [LockState](#lockstate8) |  Yes | Lock state.|

## PersoLockInfo<sup>8+</sup>

Defines the personalized lock information.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name    |               Type              | Mandatory|      Description    |
| -------- | -------------------------------- | ---- | ------------- |
| lockType | [PersoLockType](#persolocktype8) |  Yes | Personalized lock type.|
| password | string                           |  Yes | Password.       |

## IccAccountInfo<sup>10+</sup>

ICC account information.

**System capability**: SystemCapability.Telephony.CoreService

| Name      | Type   | Mandatory| Description            |
| ---------- | ------- | ---- | ---------------- |
| simId      | number  |  Yes | SIM card ID.         |
| slotIndex  | number  |  Yes | Card slot ID.          |
| isEsim     | boolean |  Yes | Whether the SIM card is an eSim card.|
| isActive   | boolean |  Yes | Whether the card is activated.    |
| iccId      | string  |  Yes | ICCID number.       |
| showName   | string  |  Yes | SIM card display name.   |
| showNumber | string  |  Yes | SIM card display number.   |

## OperatorConfig<sup>8+</sup>

Defines the carrier configuration.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name | Type  | Mandatory| Description|
| ----- | ------ | ---- | ---- |
| field | string |  Yes | Field name.|
| value | string |  Yes | Field value.  |

## DiallingNumbersInfo<sup>8+</sup>

Defines the contact number information.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name        | Type  | Mandatory|    Description   |
| ------------ | ------ | ---- | ---------- |
| alphaTag     | string |  Yes | Tag.    |
| number       | string |  Yes | Call transfer number.    |
| recordNumber | number |  No | Record number.|
| pin2         | string |  Yes | PIN 2.|

## ContactType<sup>8+</sup>

Enumerates contact types.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name           | Value  | Description      |
| --------------- | ---- | ---------- |
| GENERAL_CONTACT | 1    | Common contact number.|
| FIXED_DIALING   | 2    | Fixed dialing number.  |

## OperatorConfigKey<sup>9+</sup>

Enumerates carrier configuration keys.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

|                             Name                       |                             Value                        |         Description        |
| ------------------------------------------------------- | ------------------------------------------------------ | -------------------- |
| KEY_VOICE_MAIL_NUMBER_STRING                            | "voice_mail_number_string"                             | Voice mailbox number.      |
| KEY_IMS_SWITCH_ON_BY_DEFAULT_BOOL                       | "ims_switch_on_by_default_bool"                        | Fixed dialing number.          |
| KEY_HIDE_IMS_SWITCH_BOOL                                | "hide_ims_switch_bool"                                 | Whether to hide the IMS switch.   |
| KEY_VOLTE_SUPPORTED_BOOL                                | "volte_supported_bool"                                 | Whether to support VoLTE. |
| KEY_NR_MODE_SUPPORTED_LIST_INT_ARRAY                    | "nr_mode_supported_list_int_array"                     | List of supported NR modes.  |
| KEY_VOLTE_PROVISIONING_SUPPORTED_BOOL                   | "volte_provisioning_supported_bool"                    | Whether to support VoLTE provisioning. |
| KEY_SS_OVER_UT_SUPPORTED_BOOL                           | "ss_over_ut_supported_bool"                            | Whether SS over UT is supported.  |
| KEY_IMS_GBA_REQUIRED_BOOL                               | "ims_gba_required_bool"                                | Whether GBA is required for IMS.    |
| KEY_UT_PROVISIONING_SUPPORTED_BOOL                      | "ut_provisioning_supported_bool"                       | Whether to support UT provisioning.    |
| KEY_IMS_PREFER_FOR_EMERGENCY_BOOL                       | "ims_prefer_for_emergency_bool"                        | IMS preferences for emergency.     |
| KEY_CALL_WAITING_SERVICE_CLASS_INT                      | "call_waiting_service_class_int"                       | Call waiting service.      |
| KEY_CALL_TRANSFER_VISIBILITY_BOOL                       | "call_transfer_visibility_bool"                        | Call transfer visibility.    |
| KEY_IMS_CALL_DISCONNECT_REASON_INFO_MAPPING_STRING_ARRAY| "ims_call_disconnect_reason_info_mapping_string_array" | List of IMS call disconnection reasons.|
| KEY_FORCE_VOLTE_SWITCH_ON_BOOL                          | "force_volte_switch_on_bool"                           | Whether to forcibly turn on VoLTE.     |
| KEY_ENABLE_OPERATOR_NAME_CUST_BOOL                      | "enable_operator_name_cust_bool"                       | Whether to display the carrier name.|
| KEY_OPERATOR_NAME_CUST_STRING                           | "operator_name_cust_string"                            | Carrier name.        |
| KEY_SPN_DISPLAY_CONDITION_CUST_INT                      | "spn_display_condition_cust_int"                       | SPN display rule.       |
| KEY_PNN_CUST_STRING_ARRAY                               | "pnn_cust_string_array"                                | PLMN name          |
| KEY_OPL_CUST_STRING_ARRAY                               | "opl_cust_string_array"                                | PLMN information of the carrier.    |
| KEY_EMERGENCY_CALL_STRING_ARRAY                         | "emergency_call_string_array"                          | Emergency call list.      |
