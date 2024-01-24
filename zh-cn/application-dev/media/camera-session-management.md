# 会话管理(ArkTS)

相机使用预览、拍照、录像、元数据功能前，均需要创建相机会话。

在会话中，可以完成以下功能：

- 配置相机的输入流和输出流。相机在拍摄前，必须完成输入输出流的配置。
  配置输入流即添加设备输入，对用户而言，相当于选择设备的某一摄像头拍摄；配置输出流，即选择数据将以什么形式输出。当应用需要实现拍照时，输出流应配置为预览流和拍照流，预览流的数据将显示在XComponent组件上，拍照流的数据将通过ImageReceiver接口的能力保存到相册中。

- 添加闪光灯、调整焦距等配置。具体支持的配置及接口说明请参考[Camera API参考](../reference/apis/js-apis-camera.md)。

- 会话切换控制。应用可以通过移除和添加输出流的方式，切换相机模式。如当前会话的输出流为拍照流，应用可以将拍照流移除，然后添加视频流作为输出流，即完成了拍照到录像的切换。

完成会话配置后，应用提交和开启会话，可以开始调用相机相关功能。

## 开发步骤
1. 导入相关接口，导入方法如下。
     
   ```ts
   import camera from '@ohos.multimedia.camera';
   import { BusinessError } from '@ohos.base';
   ```

2. 调用cameraManager类中的[createCaptureSession](../reference/apis/js-apis-camera.md#createcapturesessiondeprecated)方法创建一个会话。
     
   ```ts
   function getSession(cameraManager: camera.CameraManager): camera.CaptureSession | undefined {
     let session: camera.CaptureSession | undefined = undefined;
     try {
       session = cameraManager.createCaptureSession();
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to create the session instance. error: ${JSON.stringify(err)}`);
     }
     return session;
   }
   ```

3. 调用Session类中的[beginConfig](../reference/apis/js-apis-camera.md#beginconfig)方法配置会话。
     
   ```ts
   function beginConfig(session: camera.Session): void {
     try {
       session.beginConfig();
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to beginConfig. error: ${JSON.stringify(err)}`);
     }
   }
   ```

4. 使能。向会话中添加相机的输入流和输出流，调用[addInput](../reference/apis/js-apis-camera.md#addinput)添加相机的输入流；调用[addOutput](../reference/apis/js-apis-camera.md#addoutput)添加相机的输出流。以下示例代码以添加预览流previewOutput和拍照流photoOutput为例，即当前模式支持拍照和预览。

     调用Session类中的[commitConfig](../reference/apis/js-apis-camera.md#commitconfig)和[start](../reference/apis/js-apis-camera.md#start-4)方法提交相关配置，并启动会话。
     
   ```ts
   async function startSession(session: camera.Session, cameraInput: camera.CameraInput, previewOutput: camera.PreviewOutput, photoOutput: camera.PhotoOutput): Promise<void> {
     try {
       session.addInput(cameraInput);
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to addInput. error: ${JSON.stringify(err)}`);
     }
     try {
       session.addOutput(previewOutput);
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to add previewOutput. error: ${JSON.stringify(err)}`);
     }
     try {
       session.addOutput(photoOutput);
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to add photoOutput. error: ${JSON.stringify(err)}`);
     }
     try {
       await session.commitConfig();
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to commitConfig. error: ${JSON.stringify(err)}`);
     }
   
     try {
       await session.start();
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to start. error: ${JSON.stringify(err)}`);
     }
   }
   ```

5. 会话控制。调用Session类中的[stop](../reference/apis/js-apis-camera.md#stop-4)方法可以停止当前会话。调用[removeOutput](../reference/apis/js-apis-camera.md#removeoutput)和[addOutput](../reference/apis/js-apis-camera.md#addoutput)方法可以完成会话切换控制。以下示例代码以移除拍照流photoOutput，添加视频流videoOutput为例，完成了拍照到录像的切换。
     
   ```ts
   async function switchOutput(session: camera.Session, videoOutput: camera.VideoOutput, photoOutput: camera.PhotoOutput): Promise<void> {
     try {
       await session.stop();
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to stop. error: ${JSON.stringify(err)}`);
     }
   
     try {
       session.beginConfig();
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to beginConfig. error: ${JSON.stringify(err)}`);
     }
     // 从会话中移除拍照输出流
     try {
       session.removeOutput(photoOutput);
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to remove photoOutput. error: ${JSON.stringify(err)}`);
     }
     // 向会话中添加视频输出流
     try {
       session.addOutput(videoOutput);
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to add videoOutput. error: ${JSON.stringify(err)}`);
     }
   }
   ```
