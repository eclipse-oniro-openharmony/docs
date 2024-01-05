# 管理通知渠道
针对应用需要根据自身需求选择不同的提醒方式，系统提供了通知渠道的创建、获取和移除。对应用自身的通知方式进行管理。


## 渠道类型描述
| SlotType             | 取值   | 分类     | 通知中心 | 横幅 | 锁屏 | 铃声/振动 | 状态栏图标 | 自动亮屏 |
| -------------------- | ------ | --------| ------- |------|------|----------|-----------|---------|
| SOCIAL_COMMUNICATION | 1      | 社交通信 | Y | Y | Y | Y | Y | Y |
| SERVICE_INFORMATION  | 2      | 服务提醒 | Y | N | Y | Y | Y | Y |
| CONTENT_INFORMATION  | 3      | 内容资讯 | Y | N | N | N | Y | N |
| CUSTOMER_SERVICE     | 5      | 客服消息 | Y | N | N | Y | Y | N |
| OTHER_TYPES          | 0xFFFF | 其他     | Y | N | N | N | N | N |


## 接口说明
1. 通知服务提供了两种创建通知渠道类型的方法：

    - 发布通知时，在[NotificationRequest](../reference/apis/js-apis-inner-notification-notificationRequest.md#notificationrequest)的notificationSlotType字段里携带，如果notificationSlotType对应渠道不存在，通知服务会自动创建。

    - 调用接口[`addSlot()`](../reference/apis/js-apis-notificationManager.md#notificationmanageraddslot-2)显式创建，后续发布通知时填入已创建的SlotType。

2. 通知服务支持查询指定类型的通知渠道：

    - 调用接口[`getSlot()`](../reference/apis/js-apis-notificationManager.md#notificationmanagergetslot)查询，可以获取到指定类型的通知渠道是否使能。

3. 通知服务支持移除当前通知渠道类型：

    - 调用接口[`removeSlot()`](../reference/apis/js-apis-notificationManager.md#notificationmanagerremoveslot)移除，可以移除指定类型的通知渠道。



| **接口名** | **描述** |
| ---------- | -------- |
| addSlot(type: SlotType, callback: AsyncCallback\<void\>): void                 | 创建指定类型的通知渠道。使用callback异步回调。         |
| addSlot(type: SlotType): Promise\<void\>                                       | 创建指定类型的通知渠道。使用Promise异步回调。          |
| getSlot(slotType: SlotType, callback: AsyncCallback\<NotificationSlot\>): void | 获取一个指定类型的通知渠道。使用callback异步回调。      |
| getSlot(slotType: SlotType): Promise\<NotificationSlot\>                       | 获取一个指定类型的通知渠道。使用Promise异步回调。       |
| getSlots(callback: AsyncCallback\<Array\<NotificationSlot>>): void             | 获取此应用程序的所有通知渠道。使用callback异步回调。    |
| getSlots(): Promise\<Array\<NotificationSlot>>                                 | 获取此应用程序的所有通知渠道。使用Promise异步回调。     |
| removeSlot(slotType: SlotType, callback: AsyncCallback\<void\>): void          | 删除此应用程序指定类型的通知渠道。使用callback异步回调。 |
| removeSlot(slotType: SlotType): Promise\<void\>                                | 删除此应用程序指定类型的通知渠道。使用Promise异步回调。  |
| removeAllSlots(callback: AsyncCallback\<void\>): void                          | 删除此应用程序所有通知渠道。使用callback异步回调。      |
| removeAllSlots(): Promise\<void\>                                              | 删除此应用程序所有通知渠道。使用Promise异步回调。       |


## 开发步骤

1. 导入notificationManager模块。

   ```ts
   import notificationManager from '@ohos.notificationManager';
   import Base from '@ohos.base';
   ```

2. 创建指定类型的通知渠道。

    ```ts
    import Base from '@ohos.base';

    // addslot回调
    let addSlotCallBack = (err: Base.BusinessError): void => {
        if (err) {
            console.error(`addSlot failed, code is ${err.code}, message is ${err.message}`);
        } else {
            console.info("addSlot success");
        }
    }
    notificationManager.addSlot(notificationManager.SlotType.SOCIAL_COMMUNICATION, addSlotCallBack);
    ```

3. 查询指定类型的通知渠道。

    ```ts
    // getSlot回调
    let getSlotCallback = (err: Base.BusinessError, data: notificationManager.NotificationSlot): void => {
        if (err) {
            console.error(`getSlot failed, code is ${err.code}, message is ${err.message}`);
        } else {
            console.info(`getSlot success, data is ${JSON.stringify(data)}`);
        }
    }
    let slotType: notificationManager.SlotType = notificationManager.SlotType.SOCIAL_COMMUNICATION;
    notificationManager.getSlot(slotType, getSlotCallback);
    ```

4. 删除指定类型的通知渠道。

    ```ts
    // removeSlot回调
    let removeSlotCallback = (err: Base.BusinessError): void => {
    if (err) {
        console.error(`removeSlot failed, code is ${err.code}, message is ${err.message}`);
    } else {
        console.info("removeSlot success");
    }
    }
    let slotType = notificationManager.SlotType.SOCIAL_COMMUNICATION;
    notificationManager.removeSlot(slotType, removeSlotCallback);
    ```