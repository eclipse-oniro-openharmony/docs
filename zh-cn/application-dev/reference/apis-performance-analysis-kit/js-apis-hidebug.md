# @ohos.hidebug (Debug调试)

> **说明：**
>
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

使用hidebug，可以获取应用内存的使用情况，包括应用进程的静态堆内存（native heap）信息、应用进程内存占用PSS（Proportional Set Size）信息等；可以完成虚拟机内存切片导出，虚拟机CPU Profiling采集等操作。

## 导入模块

```ts
import hidebug from '@ohos.hidebug';
```

## hidebug.getNativeHeapSize

getNativeHeapSize(): bigint

获取本应用堆内存的总大小。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**返回值：**

| 类型   | 说明                        |
| ------ | --------------------------- |
| bigint | 返回本应用堆内存总大小，单位为Byte。 |

**示例：**

  ```ts
  let nativeHeapSize: bigint = hidebug.getNativeHeapSize();
  ```

## hidebug.getNativeHeapAllocatedSize

getNativeHeapAllocatedSize(): bigint

获取本应用堆内存的已分配内存大小。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**返回值：**

| 类型   | 说明                              |
| ------ | --------------------------------- |
| bigint | 返回本应用堆内存的已分配内存，单位为Byte。 |


**示例：**
  ```ts
  let nativeHeapAllocatedSize: bigint = hidebug.getNativeHeapAllocatedSize();
  ```

## hidebug.getNativeHeapFreeSize

getNativeHeapFreeSize(): bigint

获取本应用堆内存的空闲内存大小。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**返回值：**

| 类型   | 说明                            |
| ------ | ------------------------------- |
| bigint | 返回本应用堆内存的空闲内存，单位为Byte。 |

**示例：**
  ```ts
  let nativeHeapFreeSize: bigint = hidebug.getNativeHeapFreeSize();
  ```

## hidebug.getPss

getPss(): bigint

获取应用进程实际使用的物理内存大小。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**返回值：**

| 类型   | 说明                      |
| ------ | ------------------------- |
| bigint | 返回应用进程实际使用的物理内存大小，单位为kB。 |

**示例：**
  ```ts
  let pss: bigint = hidebug.getPss();
  ```

## hidebug.getVss<sup>11+<sup>

getVss(): bigint

获取应用进程虚拟耗用内存大小。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**返回值：**

| 类型   | 说明                                     |
| ------ | ---------------------------------------- |
| bigint | 返回应用进程虚拟耗用内存大小，单位为kB。 |

**示例：**

  ```ts
let vss: bigint = hidebug.getVss();
  ```

## hidebug.getSharedDirty

getSharedDirty(): bigint

获取进程的共享脏内存大小。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**返回值：**

| 类型   | 说明                       |
| ------ | -------------------------- |
| bigint | 返回进程的共享脏内存大小，单位为kB。 |


**示例：**
  ```ts
  let sharedDirty: bigint = hidebug.getSharedDirty();
  ```

## hidebug.getPrivateDirty<sup>9+<sup>

getPrivateDirty(): bigint

获取进程的私有脏内存大小。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**返回值：**

| 类型   | 说明                       |
| ------ | -------------------------- |
| bigint | 返回进程的私有脏内存大小，单位为kB。 |

**示例：**
  ```ts
  let privateDirty: bigint = hidebug.getPrivateDirty();
  ```

## hidebug.getCpuUsage<sup>9+<sup>

getCpuUsage(): number

获取进程的CPU使用率。

如占用率为50%，则返回0.5。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**返回值：**

| 类型   | 说明                       |
| ------ | -------------------------- |
| number | 获取进程的CPU使用率。 |


**示例：**
  ```ts
  let cpuUsage: number = hidebug.getCpuUsage();
  ```

## hidebug.getServiceDump<sup>9+<sup>

getServiceDump(serviceid : number, fd : number, args : Array\<string>) : void

获取系统服务信息。

**需要权限**: ohos.permission.DUMP

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**参数：**

| 参数名   | 类型   | 必填 | 说明                                                         |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| serviceid | number | 是   | 基于该用户输入的service id获取系统服务信息。|
| fd | number | 是   | 文件描述符，该接口会往该fd中写入数据。|
| args | Array\<string> | 是   | 系统服务的Dump接口所对应的参数列表。|

**错误码：**

以下错误码的详细介绍请参见[Hidebug错误码](errorcode-hiviewdfx-hidebug.md)。

| 错误码ID | 错误信息 |
| ------- | ----------------------------------------------------------------- |
| 11400101 | the service id is invalid                                           |
| 401 | the parameter check failed                                            |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import fs from '@ohos.file.fs';
import hidebug from '@ohos.hidebug';
import common from '@ohos.app.ability.common';
import { BusinessError } from '@ohos.base';

export default class HidebugTest extends UIAbility {
  public testfunc() {
    let applicationContext: common.Context | null = null;
    try {
      applicationContext = this.context.getApplicationContext();
    } catch (error) {
      console.info(`error code: ${(error as BusinessError).code}, error msg: ${(error as BusinessError).message}`);
    }

    let filesDir: string = applicationContext!.filesDir;
    let path: string = filesDir + "/serviceInfo.txt";
    console.info("output path: " + path);
    let file = fs.openSync(path, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
    let serviceId: number = 10;
    let args: Array<string> = new Array("allInfo");

    try {
      hidebug.getServiceDump(serviceId, file.fd, args);
    } catch (error) {
      console.info(`error code: ${(error as BusinessError).code}, error msg: ${(error as BusinessError).message}`);
    }
    fs.closeSync(file);
  }
}

let t = new HidebugTest();
t.testfunc();
```

## hidebug.startJsCpuProfiling<sup>9+</sup>

startJsCpuProfiling(filename : string) : void

启动虚拟机Profiling方法跟踪，`startJsCpuProfiling()`方法的调用需要与`stopJsCpuProfiling()`方法的调用一一对应，先开启后关闭，严禁使用`start->start->stop`，`start->stop->stop`，`start->start->stop->stop`等类似的顺序调用。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**参数：**

| 参数名   | 类型   | 必填 | 说明                                                         |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| filename | string | 是   | 用户自定义的profiling文件名，根据传入的`filename`，将在应用的`files`目录生成`filename.json`文件。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息 |
| ------- | ----------------------------------------------------------------- |
| 401 | the parameter check failed                                            |

**示例：**

```ts
import hidebug from '@ohos.hidebug';
import { BusinessError } from '@ohos.base';

try {
  hidebug.startJsCpuProfiling("cpu_profiling");
  // ...
  hidebug.stopJsCpuProfiling();
} catch (error) {
  console.info(`error code: ${(error as BusinessError).code}, error msg: ${(error as BusinessError).message}`);
}
```

## hidebug.stopJsCpuProfiling<sup>9+</sup>

stopJsCpuProfiling() : void

停止虚拟机Profiling方法跟踪，`startJsCpuProfiling()`方法的调用需要与`stopJsCpuProfiling()`方法的调用一一对应，先开启后关闭，严禁使用`start->start->stop`，`start->stop->stop`，`start->start->stop->stop`等类似的顺序调用。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**参数：**

| 参数名   | 类型   | 必填 | 说明                                                         |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| filename | string | 是   | 用户自定义的profiling文件名，根据传入的`filename`，将在应用的`files`目录生成`filename.json`文件。 |

**示例：**

```ts
import hidebug from '@ohos.hidebug';
import { BusinessError } from '@ohos.base';

try {
  hidebug.startJsCpuProfiling("cpu_profiling");
  // ...
  hidebug.stopJsCpuProfiling();
} catch (error) {
  console.info(`error code: ${(error as BusinessError).code}, error msg: ${(error as BusinessError).message}`);
}
```

## hidebug.dumpJsHeapData<sup>9+</sup>

dumpJsHeapData(filename : string) : void

虚拟机堆导出。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**参数：**

| 参数名   | 类型   | 必填 | 说明                                                         |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| filename | string | 是   | 用户自定义的虚拟机堆文件名，根据传入的`filename`，将在应用的`files`目录生成`filename.heapsnapshot`文件。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息 |
| ------- | ----------------------------------------------------------------- |
| 401 | the parameter check failed                                            |

**示例：**

```ts
import hidebug from '@ohos.hidebug';
import { BusinessError } from '@ohos.base';

try {
  hidebug.dumpJsHeapData("heapData");
} catch (error) {
  console.info(`error code: ${(error as BusinessError).code}, error msg: ${(error as BusinessError).message}`);
}
```

## hidebug.startProfiling<sup>(deprecated)</sup>

startProfiling(filename : string) : void

> **说明：** 从 API Version 9 开始废弃，建议使用[hidebug.startJsCpuProfiling](#hidebugstartjscpuprofiling9)替代。

启动虚拟机Profiling方法跟踪，`startProfiling()`方法的调用需要与`stopProfiling()`方法的调用一一对应，先开启后关闭，严禁使用`start->start->stop`，`start->stop->stop`，`start->start->stop->stop`等类似的顺序调用。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**参数：**

| 参数名   | 类型   | 必填 | 说明                                                         |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| filename | string | 是   | 用户自定义的profiling文件名，根据传入的`filename`，将在应用的`files`目录生成`filename.json`文件。 |

**示例：**

```ts
hidebug.startProfiling("cpuprofiler-20220216");
// code block
// ...
// code block
hidebug.stopProfiling();
```

## hidebug.stopProfiling<sup>(deprecated)</sup>

stopProfiling() : void

> **说明：** 从 API Version 9 开始废弃，建议使用[hidebug.stopJsCpuProfiling](#hidebugstopjscpuprofiling9)替代。

停止虚拟机Profiling方法跟踪，`stopProfiling()`方法的调用需要与`startProfiling()`方法的调用一一对应，先开启后关闭，严禁使用`start->start->stop`，`start->stop->stop`，`start->start->stop->stop`等类似的顺序调用。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**示例：**

```ts
hidebug.startProfiling("cpuprofiler-20220216");
// code block
// ...
// code block
hidebug.stopProfiling();
```

## hidebug.dumpHeapData<sup>(deprecated)</sup>

dumpHeapData(filename : string) : void

> **说明：** 从 API Version 9 开始废弃，建议使用[hidebug.dumpJsHeapData](#hidebugdumpjsheapdata9)替代。

虚拟机堆导出。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**参数：**

| 参数名   | 类型   | 必填 | 说明                                                         |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| filename | string | 是   | 用户自定义的虚拟机堆文件名，根据传入的`filename`，将在应用的`files`目录生成`filename.heapsnapshot`文件。 |

**示例：**

```ts
hidebug.dumpHeapData("heap-20220216");
```

## hidebug.getAppVMMemoryInfo<sup>12+<sup>

getAppVMMemoryInfo(): VMMemoryInfo

获取VM内存相关信息。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**返回值：**

| 类型         | 说明                                    |
| -------------| --------------------------------------- |
| VMMemoryInfo | 详情见 VMMemoryInfo 介绍                |

**示例：**

  ```ts
let vmMemory: VMMemoryInfo = hidebug.getAppVMMemoryInfo();
hilog.info(0x0000, "example", "totalHeap = %{public}d", vmMemory.totalHeap);
hilog.info(0x0000, "example", "heapUsed = %{public}d", vmMemory.heapUsed);
hilog.info(0x0000, "example", "allArraySize = %{public}d", vmMemory.allArraySize);
  ```

## hidebug.getAppThreadCpuUsage<sup>12+<sup>

getAppThreadCpuUsage(): ThreadCpuUsage[]

获取应用线程CPU使用情况

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**返回值：**

| 类型             | 说明                                                        |
| -----------------| ------------------------------------------------------------|
| ThreadCpuUsage[] | 一个数组,数组里包含的是ThreadCpuUsage,ThreadCpuUsage见下描述 |



**示例：**

  ```ts
let appThreadCpuUsage = hidebug.getAppThreadCpuUsage();
for (let ii = 0; ii < appThreadCpuUsage.length; ii++) {
    hilog.info(0x0000, "example", "threadId=%{public}d, cpuUsage=%{public}f", appThreadCpuUsage[ii].threadId,
    appThreadCpuUsage[ii].cpuUsage);
}
  ```

## hidebug.startAppTraceCapture<sup>12+</sup>

startAppTraceCapture(tags : number[], flag: TraceFlag, limitSize: number) : string

启动应用trace采集,'startAppTraceCapture()'方法的调用需要与'stopAppTraceCapture()'方法的调用一一对应，
先开启后关闭，严禁使用'start->start->stop'，'start->stop->stop'，'start->start->stop->stop'等类似的顺序调用。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                                                  |
| -------- | ------   | ---- | ------------------------------------------------------------------------------------- |
| tags     | number[] | 是   | trace的tag类型,具体tag类型见下方                                                       |
| flag     | TraceFlag| 是   | trace的flag类型,MAIN_THREAD为只采集主线程trace, ALL_THREADS为采集所有线程trace         |
| limitSize| number   | 是   | 开启trace文件大小限制,单位为Byte                                                       |

**返回值：**

| 类型             | 说明                                           |
| -----------------| -----------------------------------------------|
| string           | 返回trace文件名路径                            |

**错误码：**

以下错误码的详细介绍请参见[Hidebug错误码](errorcode-hiviewdfx-hidebug.md)。

| 错误码ID | 错误信息 |
| ------- | ----------------------------------------------------------------- |
| 401 | the parameter check failed                                            |
| 11400102 | Have already capture trace                                          |
| 11400103 | Without write permission on the file                                |
| 11400104 | The status of the trace is abnormal                                 |

**示例：**

```ts
let tags = [hidebug.tags.ABILITY_MANAGER, hidebug.tags.ACE];
let flag = hidebug.TraceFlag.MAIN_THREAD;
let limitSize = 1024 * 1024;
let fileName = hidebug.startAppTraceCapture(tags, flag, limitSize);
// code block
// ...
// code block
hidebug.stopAppTraceCapture();
```

## hidebug.stopAppTraceCapture<sup>12+</sup>

stopAppTraceCapture() : void

停止应用trace采集,'startAppTraceCapture()'方法的调用需要与'stopAppTraceCapture()'方法的调用一一对应，
先开启后关闭，严禁使用'start->start->stop'，'start->stop->stop'，'start->start->stop->stop'等类似的顺序调用。

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**错误码：**

以下错误码的详细介绍请参见[Hidebug错误码](errorcode-hiviewdfx-hidebug.md)。

| 错误码ID | 错误信息 |
| ------- | ----------------------------------------------------------------- |
| 11400104 | The status of the trace is abnormal                                |
| 11400105 |   No capture trace running                                       |

**示例：**

```ts
let tags = [hidebug.tags.ABILITY_MANAGER, hidebug.tags.ACE];
let flag = hidebug.TraceFlag.MAIN_THREAD;
let limitSize = 1024 * 1024;
let fileName = hidebug.startAppTraceCapture(tags, flag, limitSize);
// code block
// ...
// code block
hidebug.stopAppTraceCapture();
```

## hidebug.getAppMemoryLimit<sup>12+</sup>

getAppMemoryLimit() : MemoryLimit

获取应用程序进程内存限制

**系统能力**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**返回值**

| 类型  | 说明                      |
| ------ | -------------------------- |
| [MemoryLimit](#memorylimit) | 应用程序进程内存限制|

**示例**

```ts
 let appMemoryLimit:hidebug.MemoryLimit = hidebug.getAppMemoryLimit();
```
## MemoryLimit

应用程序进程内存限制

**系统能力**：SystemCapability.HiviewDFX.HiProfiler.HiDebug

| 名称      | 类型   | 必填 | 说明         |
| --------- | ------ | ---- | ------------ |
| rssLimit<sup>12+</sup>    | bigint |  是  | 应用程序进程的驻留集的限制（以字节为单位）     |
| vssLimit<sup>12+</sup>  | bigint |  是  | 进程的虚拟内存限制（以字节为单位）       |
| vmHeapLimit<sup>12+</sup> | bigint |  是  | 当前线程的 JS VM 堆大小限制（以字节为单位）      |

## VMMemoryInfo<sup>12+<sup>

描述VM内存信息。

**系统能力:** 以下各项对应的系统能力均为SystemCapability.HiviewDFX.HiProfiler.HiDebug

| 名称               | 类型    | 可读 | 可写 | 说明                                |
| -------------------| ------- | ---- | ---- | ---------------------------------- |
| totalHeap          | bigint  | 是   | 否   | 表示当前虚拟机的堆总大小            |
| heapUsed           | bigint  | 是   | 否   | 表示当前虚拟机使用的堆大小          |
| allArraySize       | bigint  | 是   | 否   | 表示当前虚拟机的所有数组对象大小    |

## ThreadCpuUsage<sup>12+</sup>

描述线程CPU使用情况

**系统能力:** 以下各项对应的系统能力均为SystemCapability.HiviewDFX.HiProfiler.HiDebug

| 名称               | 类型    | 可读 | 可写 | 说明                                |
| -------------------| ------- | ---- | ---- | ----------------------------------- |
| threadId           | number  | 是   | 否   | cpu线程Id                           |
| cpuUsage           | number  | 是   | 否   | cpu线程使用率                       |

## tags<sup>12+</sup>

**系统能力:** 以下各项对应的系统能力均为SystemCapability.HiviewDFX.HiProfiler.HiDebug

| 名称                     | 类型    |  说明                                |
| -------------------------| ------- |  ----------------------------------- |
| ABILITY_MANAGER          | number  |  Ability Manager tag.                |
| ACE                      | number  |  ACE development framework tag.      |
| ARK                      | number  |  ARK tag.                            |
| BLUETOOTH                | number  |  Bluetooth tag.                      |
| COMMON_LIBRARY           | number  |  Common library subsystem tag.       |
| DISTRIBUTED_HARDWARE_DEVICE_MANAGER | number  |  Distributed hardware device manager tag.     |
| DISTRIBUTED_AUDIO        | number  |  Distributed audio tag.              |
| DISTRIBUTED_CAMERA       | number  |  Distributed camera tag.           |
| DISTRIBUTED_DATA         | number  |  Distributed data manager module tag.        |
| DISTRIBUTED_HARDWARE_FRAMEWORK | number  |  Distributed hardware framework tag.   |
| DISTRIBUTED_INPUT        | number  |  Distributed input tag.             |
| DISTRIBUTED_SCREEN       | number  |  Distributed screen tag.            |
| DISTRIBUTED_SCHEDULER    | number  |  Distributed scheduler tag.          |
| FFRT                     | number  |  FFRT tasks.                        |
| FILE_MANAGEMENT          | number  |  File management tag.                |
| GLOBAL_RESOURCE_MANAGER  | number  |  Global resource manager tag.        |
| GRAPHICS                 | number  |  Graphics module tag.                |
| HDF                      | number  |  HDF subsystem tag.                 |
| MISC                     | number  |  MISC module tag.                    |
| MULTIMODAL_INPUT         | number  |  Multimodal input module tag.        |
| NET                      | number  |  Net tag.                            |
| NOTIFICATION             | number  |  Notification module tag.            |
| NWEB                     | number  |  NWeb tag.                           |
| OHOS                     | number  |  OHOS generic tag.                   |
| POWER_MANAGER            | number  |  Power manager tag.                   |
| RPC                      | number  |  RPC tag.                            |
| SAMGR                    | number  |  SA tag.                            |
| WINDOW_MANAGER           | number  |  Window manager tag.                |
| AUDIO                    | number  |  Audio module tag.                  |
| CAMERA                   | number  |  Camera module tag.                 |
| IMAGE                    | number  |  Image module tag.                  |
| MEDIA                    | number  |  Media module tag.                  |

## hidebug.getSystemCpuUsage<sup>12+</sup>

getSystemCpuUsage() : number

获取系统的CPU资源占用情况.

例如, 当系统资源CPU占用为 **50%**, 将返回**0.5**.

**系统能力**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**返回值**

| 类型     | 说明           |
|--------|--------------|
| number | 系统Cpu资源占用情况. |

**错误码：**

以下错误码的详细介绍请参见[Hidebug-CpuUsage错误码](errorcode-hiviewdfx-hidebug-cpuusage.md)。

| 错误码ID | 错误信息                                           |
| ------- |------------------------------------------------|
| 11400104 | The status of the system cpu usage is abnormal |

**示例**
  ```ts
  let cpuUsage: number = hidebug.getSystemCpuUsage();
  ```

## hidebug.getAppNativeMemInfo<sup>12+<sup>

getAppNativeMemInfo(): NativeMemInfo

获取应用进程耗用内存大小

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**返回值：**

| 类型   | 说明                                     |
| ------ | ---------------------------------------- |
| [NativeMemInfo](#nativeMemInfo) | 应用进程耗用内存大小|

**示例：**

  ```ts
let nativeMemInfo: NativeMemInfo = hidebug.getAppNativeMemInfo();

hilog.info(0x0000, 'testTag', "pss = %{public}d", nativeMemInfo.pss);

hilog.info(0x0000, 'testTag', "vss = %{public}d", nativeMemInfo.vss);

hilog.info(0x0000, 'testTag', "rss = %{public}d", nativeMemInfo.rss);

hilog.info(0x0000, 'testTag', "sharedDirty = %{public}d", nativeMemInfo.sharedDirty);

hilog.info(0x0000, 'testTag', "privateDirty = %{public}d", nativeMemInfo.privateDirty);

hilog.info(0x0000, 'testTag', "sharedClean = %{public}d", nativeMemInfo.sharedClean);

hilog.info(0x0000, 'testTag', "privateClean = %{public}d", nativeMemInfo.privateClean);
  ```
## NativeMemInfo

应用进程耗用内存大小

**系统能力**：SystemCapability.HiviewDFX.HiProfiler.HiDebug

| 名称      | 类型   | 必填 | 说明         |
| --------- | ------ | ---- | ------------ |
| pss<sup>12+<sup>  | bigint |  是  | 实际占用的物理内存的大小(比例分配共享库占用的内存)，以KB为单位     |
| vss<sup>12+<sup>  | bigint |  是  | 占用虚拟内存大小(包括共享库所占用的内存)，以KB为单位       |
| rss<sup>12+<sup>  | bigint |  是  | 实际占用的物理内存的大小(包括共享库占用), 以KB为单位         |
| sharedDirty<sup>12+<sup>  | bigint |  是  | 共享脏内存的大小，以KB为单位      |
| privateDirty<sup>12+<sup>  | bigint |  是  | 专用脏内存的大小，以KB为单位      |
| sharedClean<sup>12+<sup>  | bigint |  是  | 共享干净内存的大小，以KB为单位      |
| privateClean<sup>12+<sup>  | bigint |  是  | 专用干净内存的大小，以KB为单位      |

## hidebug.getSystemMemInfo<sup>12+<sup>

getSystemMemInfo(): SystemMemInfo

获取系统耗用内存大小

**系统能力：** SystemCapability.HiviewDFX.HiProfiler.HiDebug

**返回值：**

| 类型   | 说明                                     |
| ------ | ---------------------------------------- |
| [SystemMemInfo](#systemMemInfo) | 系统耗用内存大小|

**示例：**

  ```ts
let systemMemInfo: SystemMemInfo = hidebug.getSystemMemInfo();

hilog.info(0x0000, 'testTag', "totalMem = %{public}d", systemMemInfo.totalMem);

hilog.info(0x0000, 'testTag', "freeMem = %{public}d", systemMemInfo.freeMem);

hilog.info(0x0000, 'testTag', "availableMem = %{public}d", systemMemInfo.availableMem);
  ```
## SystemMemInfo

系统耗用内存大小

**系统能力**：SystemCapability.HiviewDFX.HiProfiler.HiDebug

| 名称      | 类型   | 必填 | 说明         |
| --------- | ------ | ---- | ------------ |
| totalMem<sup>12+<sup>  | bigint |  是  | 系统总的内存，以KB为单位     |
| freeMem<sup>12+<sup>  | bigint |  是  | 系统空闲的内存，以KB为单位       |
| availableMem<sup>12+<sup>  | bigint |  是  | 系统可用的内存，以KB为单位      |

## TraceFlag<sup>12+</sup>

**系统能力**：SystemCapability.HiviewDFX.HiProfiler.HiDebug

| 名称      | 说明         |
| --------- | ------------ |
| MAIN_THREAD  | Only capture main thread trace     |
| ALL_THREADS |  Capture all thread trace       |

