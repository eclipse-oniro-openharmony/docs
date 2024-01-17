# 分段式拍照实现方案(ArkTS)

当前示例提供完整的拍照流程介绍，方便开发者了解完整的接口调用顺序。

在参考以下示例前，建议开发者查看[分段式拍照(ArkTS)](camera_deferred_photo.md)的具体章节，了解[设备输入](camera-device-input.md)、[会话管理](camera-session-management.md)、[拍照](camera-shooting.md)等单个流程。

## 开发流程

在获取到相机支持的输出流能力后，开始创建拍照流，开发流程如下。

![deferred_photo_development-process](figures/deferred_photo_development-process.png)

## 完整示例

Context获取方式请参考：[获取UIAbility的上下文信息](../application-models/uiability-usage.md#获取uiability的上下文信息)。

```ts
import camera from '@ohos.multimedia.camera';
import image from '@ohos.multimedia.image';
import { BusinessError } from '@ohos.base';
import common from '@ohos.app.ability.common';
import fs from '@ohos.file.fs';
import PhotoAccessHelper from '@ohos.file.photoAccessHelper';

let context = getContext(this);

// 写文件方式落盘真图
async function savePicture(img: image.Image) {
  let photoAccessHelper = PhotoAccessHelper.getPhotoAccessHelper(context);
  let testFileName = 'testFile' + Date.now() + '.jpg';
  //createAsset的调用需要ohos.permission.READ_IMAGEVIDEO和ohos.permission.WRITE_IMAGEVIDEO的权限
  let photoAsset = await photoAccessHelper.createAsset(testFileName);
  let buffer: ArrayBuffer;
  img.getComponent(image.ComponentType.JPEG, (errCode: BusinessError, component: image.Component): void => {
    if (errCode || component === undefined) {
      return;
    }
    if (component.byteBuffer) {
      buffer = component.byteBuffer;
    } else {
      return;
    }
  });
  fs.write(fd, buffer);
  await photoAsset.close(fd);
  img.release(); 
}

// 调用媒体库方式落盘缩略图
async function saveDeferredPhoto(proxyObj: camera.DeferredPhotoProxy) {    
  try {
    // 创建 photoAsset
    let photoAccessHelper = PhotoAccessHelper.getPhotoAccessHelper(context);
    let testFileName = 'testFile' + Date.now() + '.jpg';
    let photoAsset = await photoAccessHelper.createAsset(testFileName);
    // 将缩略图代理类传递给媒体库
    let mediaRequest: photoAccessHelper.MediaChangeRequest = new photoAccessHelper.MediaAssetChangeRequest(photoAsset);
    mediaRequest.AddResource(photoAccessHelper.ResourceTypeType.PHOTOT_PROXY, proxyObj);
    let res = await photoAccessHelper.applyChanges(mediaRequest);
    console.info('saveDeferredPhoto success.');
  } catch (err) {
    console.error(`Failed to saveDeferredPhoto. error: ${JSON.stringify(err)}`);
  }
}

async function deferredPhotoCase(baseContext: common.BaseContext, surfaceId: string): Promise<void> {
  // 创建CameraManager对象
  let cameraManager: camera.CameraManager = camera.getCameraManager(baseContext);
  if (!cameraManager) {
    console.error("camera.getCameraManager error");
    return;
  }
  // 监听相机状态变化
  cameraManager.on('cameraStatus', (err: BusinessError, cameraStatusInfo: camera.CameraStatusInfo) => {
    console.info(`camera : ${cameraStatusInfo.camera.cameraId}`);
    console.info(`status: ${cameraStatusInfo.status}`);
  });

  // 获取相机列表
  let cameraArray: Array<camera.CameraDevice> = cameraManager.getSupportedCameras();
  if (cameraArray.length <= 0) {
    console.error("cameraManager.getSupportedCameras error");
    return;
  }

  for (let index = 0; index < cameraArray.length; index++) {
    console.info('cameraId : ' + cameraArray[index].cameraId);                          // 获取相机ID
    console.info('cameraPosition : ' + cameraArray[index].cameraPosition);              // 获取相机位置
    console.info('cameraType : ' + cameraArray[index].cameraType);                      // 获取相机类型
    console.info('connectionType : ' + cameraArray[index].connectionType);              // 获取相机连接类型
  }

  // 创建相机输入流
  let cameraInput: camera.CameraInput | undefined = undefined;
  try {
    cameraInput = cameraManager.createCameraInput(cameraArray[0]);
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to createCameraInput errorCode = ' + err.code);
  }
  if (cameraInput === undefined) {
    return;
  }

  // 监听cameraInput错误信息
  let cameraDevice: camera.CameraDevice = cameraArray[0];
  cameraInput.on('error', cameraDevice, (error: BusinessError) => {
    console.error(`Camera input error code: ${error.code}`);
  })

  // 打开相机
  await cameraInput.open();

  // 获取相机设备支持的输出流能力
  let cameraOutputCap: camera.CameraOutputCapability = cameraManager.getSupportedOutputCapability(cameraArray[0]);
  if (!cameraOutputCap) {
    console.error("cameraManager.getSupportedOutputCapability error");
    return;
  }
  console.info("outputCapability: " + JSON.stringify(cameraOutputCap));

  let previewProfilesArray: Array<camera.Profile> = cameraOutputCap.previewProfiles;
  if (!previewProfilesArray) {
    console.error("createOutput previewProfilesArray == null || undefined");
  }

  let photoProfilesArray: Array<camera.Profile> = cameraOutputCap.photoProfiles;
  if (!photoProfilesArray) {
    console.error("createOutput photoProfilesArray == null || undefined");
  }

  let previewOutput: camera.PreviewOutput | undefined = undefined;
  try {
    previewOutput = cameraManager.createPreviewOutput(previewProfilesArray[0], surfaceId);
  } catch (error) {
    let err = error as BusinessError;
    console.error(`Failed to create the PreviewOutput instance. error code: ${err.code}`);
  }
  if (previewOutput === undefined) {
    return;
  }
  // 监听预览输出错误信息
  previewOutput.on('error', (error: BusinessError) => {
    console.error(`Preview output error code: ${error.code}`);
  });
  // 创建拍照输出流
  let photoOutput: camera.PhotoOutput | undefined = undefined;
  try {
    photoOutput = cameraManager.createPhotoOutput(photoProfilesArray[0]);
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to createPhotoOutput errorCode = ' + err.code);
  }
  if (photoOutput === undefined) {
    return;
  }
  //创建会话
  let captureSession: camera.CaptureSession | undefined = undefined;
  try {
    captureSession = cameraManager.createCaptureSession();
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to create the CaptureSession instance. errorCode = ' + err.code);
  }
  if (captureSession === undefined) {
    return;
  }
  // 监听session错误信息
  captureSession.on('error', (error: BusinessError) => {
    console.error(`Capture session error code: ${error.code}`);
  });

  // 开始配置会话
  try {
    captureSession.beginConfig();
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to beginConfig. errorCode = ' + err.code);
  }

  // 向会话中添加相机输入流
  try {
    captureSession.addInput(cameraInput);
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to addInput. errorCode = ' + err.code);
  }

  // 向会话中添加预览输出流
  try {
    captureSession.addOutput(previewOutput);
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to addOutput(previewOutput). errorCode = ' + err.code);
  }

  // 向会话中添加拍照输出流
  try {
    captureSession.addOutput(photoOutput);
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to addOutput(photoOutput). errorCode = ' + err.code);
  }

  // 注册原图回调监听
  photoOutPut.on('photoAvailable', (err: BusinessError, photoObj: camera.Photo): void => {
    if (err) {
      console.info(`photoAvailable error: ${JSON.stringify(err)}.`);
      return;
    }
    this.savePicture(photoObj).then(() => {
      // 落盘完成后，释放photo对象。
      photoObj.release();
    });
  });

  // 注册分段式缩略图代理回调监听
  photoOutPut.on('deferredPhotoProxyAvailable', (err: BusinessError, proxyObj: camera.DeferredPhotoProxy): void => {
    if (err) {
      console.info(`deferredPhotoProxyAvailable error: ${JSON.stringify(err)}.`);
      return;
    }
    console.info('photoOutPutCallBack deferredPhotoProxyAvailable');
    // 获取缩略图 pixelMap
    proxyObj.getThumbnail().then((thumbnail: image.PixelMap) => {
      AppStorage.setOrCreate('proxyThumbnail', thumbnail); 
    });
    // 调用媒体库接口落盘缩略图
    this.saveDeferredPhoto(proxyObj).then(() => {
      // 落盘完成后，释放代理类对象。
      proxyObj.release();
    });
  });
    
  // 判断是否支持分段式拍照能力
  let isSupportDeferred: boolean = photoOutPut.isDeferredImageDeliverySupported(camera.DeferredDeliveryImageType.PHOTO);
  console.info('isDeferredImageDeliverySupported res:' + isSupportDeferred);
  if (isSupportDeferred) {
    // 使能分段式拍照
	photoOutPut.deferImageDelivery(camera.DeferredDeliveryImageType.PHOTO);
    // 查询使能分段式结果
    let isSupportEnabled: boolean = photoOutPut.isDeferredImageDeliveryEnabled(camera.DeferredDeliveryImageType.PHOTO);
    console.info('isDeferredImageDeliveryEnabled res:' + isSupportEnabled);
  }

  // 提交会话配置
  await captureSession.commitConfig();

  // 启动会话
  await captureSession.start().then(() => {
    console.info('Promise returned to indicate the session start success.');
  });
  // 判断设备是否支持闪光灯
  let flashStatus: boolean = false;
  try {
    flashStatus = captureSession.hasFlash();
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to hasFlash. errorCode = ' + err.code);
  }
  console.info('returned with the flash light support status:' + flashStatus);

  if (flashStatus) {
    // 判断是否支持自动闪光灯模式
    let flashModeStatus: boolean = false;
    try {
      let status: boolean = captureSession.isFlashModeSupported(camera.FlashMode.FLASH_MODE_AUTO);
      flashModeStatus = status;
    } catch (error) {
      let err = error as BusinessError;
      console.error('Failed to check whether the flash mode is supported. errorCode = ' + err.code);
    }
    if(flashModeStatus) {
      // 设置自动闪光灯模式
      try {
        captureSession.setFlashMode(camera.FlashMode.FLASH_MODE_AUTO);
      } catch (error) {
        let err = error as BusinessError;
        console.error('Failed to set the flash mode. errorCode = ' + err.code);
      }
    }
  }

  // 判断是否支持连续自动变焦模式
  let focusModeStatus: boolean = false;
  try {
    let status: boolean = captureSession.isFocusModeSupported(camera.FocusMode.FOCUS_MODE_CONTINUOUS_AUTO);
    focusModeStatus = status;
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to check whether the focus mode is supported. errorCode = ' + err.code);
  }

  if (focusModeStatus) {
    // 设置连续自动变焦模式
    try {
      captureSession.setFocusMode(camera.FocusMode.FOCUS_MODE_CONTINUOUS_AUTO);
    } catch (error) {
      let err = error as BusinessError;
      console.error('Failed to set the focus mode. errorCode = ' + err.code);
    }
  }

  // 获取相机支持的可变焦距比范围
  let zoomRatioRange: Array<number> = [];
  try {
    zoomRatioRange = captureSession.getZoomRatioRange();
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to get the zoom ratio range. errorCode = ' + err.code);
  }
  if (zoomRatioRange.length <= 0) {
    return;
  }
  // 设置可变焦距比
  try {
    captureSession.setZoomRatio(zoomRatioRange[0]);
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to set the zoom ratio value. errorCode = ' + err.code);
  }
  let photoCaptureSetting: camera.PhotoCaptureSetting = {
    quality: camera.QualityLevel.QUALITY_LEVEL_HIGH, // 设置图片质量高
    rotation: camera.ImageRotation.ROTATION_0 // 设置图片旋转角度0
  }
  // 使用当前拍照设置进行拍照
  photoOutput.capture(photoCaptureSetting, (err: BusinessError) => {
    if (err) {
      console.error(`Failed to capture the photo ${err.message}`);
      return;
    }
    console.info('Callback invoked to indicate the photo capture request success.');
  });
  // 停止当前会话
  captureSession.stop();

  // 释放相机输入流
  cameraInput.close();

  // 释放预览输出流
  previewOutput.release();

  // 释放拍照输出流
  photoOutput.release();

  // 释放会话
  captureSession.release();

  // 会话置空
  captureSession = undefined;
}
```