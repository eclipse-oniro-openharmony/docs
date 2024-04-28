# 插件管理(ArkTS)

在开发一个支持数字版权保护功能的应用前，需要先查询设备是否支持DRM功能，不同的DRM方案支持的功能也有差异，需要查询设备支持哪些DRM方案，然后再创建具体的DRM对象。

在DRM Kit里DRM方案以插件形式存在，所以也叫DRM插件。

## 开发步骤

详细的API说明请参考[DRM API参考](../../reference/apis-drm-kit/js-apis-drm.md)。

1. 导入drm接口，接口中提供了drm相关的属性和方法。

   ```ts
   import drm from '@ohos.multimedia.drm';
   ```

2. 通过isMediaKeySystemSupported方法，查询设备是否支持对应的插件类型。

   > **说明：**
   >
   > 如果查询为false，说明该设备不支持对应的DRM方案。

   ```ts
   function isMediaKeySystemSupported(name: string, mimeType: string, level: ContentProtectionLevel): boolean {
     let isSupported = drm.isMediaKeySystemSupported(name);
     isSupported = drm.isMediaKeySystemSupported(name, mimeType);
     isSupported = drm.isMediaKeySystemSupported(name, mimeType, level);
     return isSupported;
   }
   ```

3. 通过drm的createMediaKeySystem(name: string)方法，创建MediaKeySystem实例，同步返回结果，创建失败，不可继续后续操作。

   > **说明：**
   >
   > 如果如果创建失败则返回undefined，说明该设备不支持DRM能力。

   ```ts
   function createMediaKeySystem(name: string): MediaKeySystem {
     let mediaKeySystem = drm.createMediaKeySystem(name);
     if (mediaKeySystem === undefined) {
       return undefined;
     }
   }
   ```

4. 通过getMediaKeySystemName方法，获取设备支持对应的插件类型的name和uuid。

   > **说明：**
   >
   > 如果查询出的map的size为null，说明该设备中不存在支持的插件。

   ```ts
   function getMediaKeySystemName(name: string): MediaKeySystem {
    try {
      let description : drm.MediaKeySystemDescripion[] = drm.getMediaKeySystemName();
    } catch (err) {
      let error = err as BusinessError;
      console.error('getMediaKeySystemName ERROR: ${error}')
    }
   }
   ```
