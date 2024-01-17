# Publishing a Basic Notification

You can publish basic notifications to send SMS messages, prompt messages, and advertisements. Available content types of basic notifications include normal text, long text, multi-line text, picture-attached, and live view.

**Table 1** Basic notification content types

| Type| Description|
| -------- | -------- |
| NOTIFICATION_CONTENT_BASIC_TEXT | Normal text notification.|
| NOTIFICATION_CONTENT_LONG_TEXT | Long text notification.|
| NOTIFICATION_CONTENT_MULTILINE | Multi-line text notification.|
| NOTIFICATION_CONTENT_PICTURE | Picture-attached notification.|
| NOTIFICATION_CONTENT_SYSTEM_LIVE_VIEW | System live view (for system applications only). |
| NOTIFICATION_CONTENT_LIVE_VIEW | Common live view.|


Notifications are displayed in the notification panel, which is the only supported subscriber to notifications. Below you can see two examples of the basic notification.
> **NOTE**
> 
> The figures are for reference only. The actual effect may vary.

**Figure 1** Examples of the basic notification

![en-us_image_0000001466462305](figures/en-us_image_0000001466462305.png)


## Available APIs

The following table describes the APIs for notification publishing. You specify the notification type by setting the [NotificationRequest](../reference/apis/js-apis-inner-notification-notificationRequest.md#notificationrequest) parameter in the APIs.

| Name| Description|
| -------- | -------- |
| publish(request: NotificationRequest, callback: AsyncCallback&lt;void&gt;): void | Publishes a notification.                |
| cancel(id: number, label: string, callback: AsyncCallback&lt;void&gt;): void | Cancels a notification.          |
| cancelAll(callback: AsyncCallback&lt;void&gt;): void; | Cancels all notifications published by the application.|


## How to Develop

1. [Enable notification](notification-enable.md). An application can use the notification feature only after being authorized by the user.

2. Import the module.
   
   ```ts
   import notificationManager from '@ohos.notificationManager';
   import Base from '@ohos.base';
   import { logger } from '../util/Logger';
   ```

3. Create a **NotificationRequest** object and publish a progress notification.
   - A normal text notification consists of the **title**, **text**, and **additionalText** parameters, of which **title** and **text** are mandatory. The value of these parameters contains less than 200 bytes.
     
      ```ts
      let notificationRequest: notificationManager.NotificationRequest = {
        id: 1,
        content: {
          notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT, // Basic notification
          normal: {
            title: 'test_title',
            text: 'test_text',
            additionalText: 'test_additionalText',
          }
        }
      };
      notificationManager.publish(notificationRequest, (err:Base.BusinessError) => {
        if (err) {
          logger.error(`Failed to publish notification. Code is ${err.code}, message is ${err.message}`);
          return;
        }
        logger.info('Succeeded in publishing notification.');
      });
      ```

      Below is an example of the normal text notification. 
     ![en-us_image_0000001466782033](figures/en-us_image_0000001466782033.png)
   - In addition to the parameters in the normal text notification, the long text notification provides the **longText**, **briefText**, and **expandedTitle** parameters. The value of **longText** contains a maximum of 1024 bytes, while that of any other parameters contains less than 200 bytes. By default, a long-text notification looks in the same way as a normal text notification. When expanded, the notification displays the title and content specified in **expandedTitle** and **longText**, respectively.
     
      ```ts
      let notificationRequest: notificationManager.NotificationRequest = {
        id: 2,
        content: {
          notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_LONG_TEXT, // Long-text notification
          longText: {
            title: 'test_title',
            text: 'test_text',
            additionalText: 'test_additionalText',
            longText: 'test_longText',
            briefText: 'test_briefText',
            expandedTitle: 'test_expandedTitle',
          }
        }
      };
      // Publish the notification.
      notificationManager.publish(notificationRequest, (err:Base.BusinessError) => {
        if (err) {
          logger.error(`Failed to publish notification. Code is ${err.code}, message is ${err.message}`);
          return;
        }
        logger.info('Succeeded in publishing notification.');
      });
      ```
   
      Below is an example of the long-text notification. 
     ![en-us_image_0000001416745530](figures/en-us_image_0000001416745530.png)
   - In addition to the parameters in the normal text notification, the multi-line text notification provides the **lines**, **briefText**, and **longTitle** parameters. The value of these parameters contains less than 200 bytes. By default, a multi-line notification looks in the same way as a normal text notification. When expanded, the notification displays the title and content specified in **longTitle** and **lines**, respectively.
     
      ```ts
      let notificationRequest: notificationManager.NotificationRequest = {
        id: 3,
        content: {
          notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_MULTILINE, // Multi-line text notification
          multiLine: {
            title: 'test_title',
            text: 'test_text',
            briefText: 'test_briefText',
            longTitle: 'test_longTitle',
            lines: ['line_01', 'line_02', 'line_03', 'line_04'],
          }
        }
      };
      // Publish the notification.
      notificationManager.publish(notificationRequest, (err:Base.BusinessError) => {
        if (err) {
          logger.error(`Failed to publish notification. Code is ${err.code}, message is ${err.message}`);
          return;
        }
        logger.info('Succeeded in publishing notification.');
      });
      ```
   
      Below is an example of the multi-line notification. 
     ![en-us_image_0000001417062446](figures/en-us_image_0000001417062446.png)
   - In addition to the parameters in the normal text notification, the picture-attached text notification provides the **picture**, **briefText**, and **expandedTitle** parameters. The value of **picture** is a [PixelMap](../reference/apis/js-apis-image.md#pixelmap7) object that does not exceed 2 MB.
     
      ```ts
      import image from '@ohos.multimedia.image';

      let imagePixelMap: image.PixelMap | undefined = undefined; // The image pixel map information needs to be obtained.
      let color = new ArrayBuffer(4);
      image.createPixelMap(color, {
        size: {
          height: 1,
          width: 1
        }
      }).then((data: image.PixelMap) => {
        imagePixelMap = data;
      }).catch((err: Base.BusinessError) => {
        console.log(`createPixelMap failed, error: ${err}`);
      })
      if (imagePixelMap !== undefined) {
        let notificationRequest: notificationManager.NotificationRequest = {
          id: 4,
          content: {
            notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_PICTURE,
            picture: {
              title: 'test_title',
              text: 'test_text',
              additionalText: 'test_additionalText',
              briefText: 'test_briefText',
              expandedTitle: 'test_expandedTitle',
              picture: imagePixelMap
            }
          }
        };
        // Publish the notification.
        notificationManager.publish(notificationRequest, (err:Base.BusinessError) => {
          if (err) {
            logger.error(`Failed to publish notification. Code is ${err.code}, message is ${err.message}`);
            return;
          }
          logger.info('Succeeded in publishing notification.');
        });
      }
      ```
   
      Below is an example of the picture-attached notification. 
     ![en-us_image_0000001466582045](figures/en-us_image_0000001466582045.png)
   - In addition to the parameters in the normal text notification, the system live view provides the **typeCode**, **capsule**, **button**, **time**, and **progress** parameters. For details, see [NotificationSystemLiveViewContent](../reference/apis/js-apis-inner-notification-notificationContent.md#notificationsystemliveviewcontent).
     
      ```ts
      import image from '@ohos.multimedia.image';
      import notificationSubscribe from '@ohos.notificationSubscribe';

      let imagePixelMap: image.PixelMap | undefined = undefined; // The image pixel map information needs to be obtained.
      let color = new ArrayBuffer(4);
      image.createPixelMap(color, {
        size: {
          height: 1,
          width: 1
        }
      }).then((data: image.PixelMap) => {
        imagePixelMap = data;
      }).catch((err: Base.BusinessError) => {
        console.log(`createPixelMap failed, error: ${err}`);
      })
      if(imagePixelMap !== undefined) {
        let notificationRequest: notificationManager.NotificationRequest = {
          notificationSlotType: notificationManager.SlotType.LIVE_VIEW, // Live view
          id: 0, // Notification ID. The default value is 0.
          content: {
            notificationContentType : notificationManager.ContentType.NOTIFICATION_CONTENT_SYSTEM_LIVE_VIEW,
            systemLiveView: {
              title: "test_title",
              text:"test_text",
              typeCode: 1, // Type of the invoking service.
              // Button
              button: {
                names: ["buttonName1"],
                icons: [imagePixelMap],
              },
              // Capsule
              capsule: {
                title: "testTitle",
                icon: imagePixelMap,
                backgroundColor: "testColor",
              },
              // Progress. To update the progress, you only need to modify the progress value and publish the notification again.
              progress: {
                maxValue: 100,
                currentValue: 21,
                isPercentage: false,
              },
              // Time
              time: {
                initialTime: 12,
                isCountDown: true,
                isPaused: true,
                isInTitle: false,
              }
            }
          }
        };
        // subscribe callback
        let subscribeCallback = (err: Base.BusinessError): void => {
          if (err) {
            console.error(`subscribe failed, code is ${err.code}, message is ${err.message}`);
          } else {
            console.info("subscribe success");
          }
        };
        // publish callback
        let publishCallback = (err: Base.BusinessError): void => {
          if (err) {
            console.error(`publish failed, code is ${err.code}, message is ${err.message}`);
          } else {
            console.info("publish success");
          }
        };
        // Button callback (It is returned when the button is touched. You can determine how to process the callback.)
        let onResponseCallback = (id:number, option:notificationManager.ButtonOptions) => {
          console.info("response callback: " + JSON.stringify(option) + "notificationId" + id);
        }
        let systemLiveViewSubscriber: notificationManager.SystemLiveViewSubscriber  = {
          onResponse: onResponseCallback
        };
        // Invoked when the subscriber cancels the notification.
        let onCancelCallback = (data: notificationSubscribe.SubscribeCallbackData) => {
          console.info("Cancel callback: " + JSON.stringify(data));
        }
        let notificationSubscriber: notificationSubscribe.NotificationSubscriber = {
          onCancel: onCancelCallback
        };
        let info: notificationSubscribe.NotificationSubscribeInfo = {
          bundleNames: ["bundleName1"],
          userId: 123
        };
        // Subscribe to the notification. This is a system API and cannot be called by third-party applications.
        notificationSubscribe.subscribe(notificationSubscriber, info, subscribeCallback);
        // Subscribe to the system live view notification (button). This is a system API and cannot be called by third-party applications.
        notificationManager.subscribeSystemLiveView(systemLiveViewSubscriber);
        // Publish the notification.
        notificationManager.publish(notificationRequest, publishCallback);
      }
      ```

   - In addition to the parameters in the normal text notification, the common live view provides the **status**, **version**, **extraInfo**, and **pictureInfo** parameters. For details, see [NotificationLiveViewContent](../reference/apis/js-apis-inner-notification-notificationContent.md#notificationliveviewcontent11).

      ```ts
      import Want from '@ohos.app.ability.Want';
      import wantAgent, {WantAgent as _wantAgent} from '@ohos.app.ability.wantAgent';

      let wantAgentInfo: wantAgent.WantAgentInfo = {
        wants: [
            {
                deviceId: '',
                bundleName: 'com.example.myapplication',
                abilityName: 'EntryAbility',
                action: '',
                entities: [],
                uri: '',
                parameters: {}
            }
        ],
        operationType: wantAgent.OperationType.START_ABILITY,
        requestCode: 0,
        wantAgentFlags: [wantAgent.WantAgentFlags.CONSTANT_FLAG]
      }
      let notificationRequest: notificationManager.NotificationRequest = {
        id: 1,
        content: {
          notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_LIVE_VIEW,
          liveView: {
            status: notificationManager.LiveViewStatus.LIVE_VIEW_CREATE,
            version: 1,
            extraInfo: {
              "event": "TAXI",
              "isMute": false,
              "primaryData.title": "primary title",
              "primaryData.content": [{ text: "text1", textColor: "#FFFFFFFF"}, { text: "text2", textColor: "#FFFFFFFF"}],
              "primaryData.keepTime": 60,
              "primaryData.extend.text": "extendData text",
              "primaryData.extend.type": 1,
              "PickupLayout.layoutType": 4,
              "PickupLayout.title": "layout title",
              "PickupLayout.content": "layout content",
              "PickupLayout.underlineColor": "#FFFFFFFF",
              "CapsuleData.status": 1,
              "CapsuleData.type": 1,
              "CapsuleData.backgroundColor": "#FFFFFFFF",
              "CapsuleData.title": "capsule title",
              "CapsuleData.content": "capsule content",
              "TimerCapsule.content": "capsule title",
              "TimerCapsule.initialtime": 7349485944,
              "TimerCapsule.isCountdown": false,
              "TimerCapsule.isPause": true
            }
          }
        },
        notificationSlotType: notificationManager.SlotType.LIVE_VIEW,
        isOngoing: true,
        isUnremovable: false,
        autoDeletedTime: 500,
        wantAgent: await WantAgent.getWantAgent(WantAgentInfo),
        extraInfo: {
          'testKey': 'testValue'
        },
      }

      notificationManager.publish(notificationRequest, (err:Base.BusinessError) => {
        if (err) {
          console.error(`Failed to publish notification. Code is ${err.code}, message is ${err.message}`);
          return;
        }
        console.info('Succeeded in publishing notification.');
      });
      ```
