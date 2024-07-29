# AVPlayer


## 概述

为媒体源提供播放能力的API。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11


## 汇总


### 文件

| 名称 | 描述 | 
| -------- | -------- |
| [avplayer.h](avplayer_8h.md) | 定义avplayer接口。使用AVPlayer提供的Native API播放媒体源。 | 
| [avplayer_base.h](avplayer__base_8h.md) | 定义AVPlayer的结构体和枚举。 | 


### 结构体

| 名称 | 描述 | 
| -------- | -------- |
| [AVPlayerCallback](_a_v_player_callback.md) | OH_AVPlayer中所有回调函数指针的集合。 | 


### 类型定义

| 名称 | 描述 | 
| -------- | -------- |
| [AVPlayerState](#avplayerstate) | 播放状态 | 
| [AVPlayerSeekMode](#avplayerseekmode) | 跳转模式 | 
| [AVPlaybackSpeed](#avplaybackspeed) | 播放速度 | 
| [AVPlayerOnInfoType](#avplayeroninfotype) | OnInfo类型 | 
| (\*[OH_AVPlayerOnInfo](#oh_avplayeroninfo)) (OH_AVPlayer \*player, [AVPlayerOnInfoType](#avplayeroninfotype) type, int32_t extra) | 收到播放器消息时调用。 | 
| (\*[OH_AVPlayerOnError](#oh_avplayeronerror)) (OH_AVPlayer \*player, int32_t errorCode, const char \*errorMsg) | 在API 9以上的版本发生错误时调用 | 
| [AVPlayerCallback](#avplayercallback) | OH_AVPlayer中所有回调函数指针的集合。 | 


### 枚举

| 名称 | 描述 | 
| -------- | -------- |
| [AVPlayerState](#avplayerstate) {<br/>AV_IDLE = 0, <br/>AV_INITIALIZED = 1, <br/>AV_PREPARED = 2, <br/>AV_PLAYING = 3,<br/>AV_PAUSED = 4, <br/>AV_STOPPED = 5, <br/>AV_COMPLETED = 6, <br/>AV_RELEASED = 7,<br/>AV_ERROR = 8<br/>} | 播放状态 | 
| [AVPlayerSeekMode](#avplayerseekmode) { <br/>AV_SEEK_NEXT_SYNC = 0, <br/>AV_SEEK_PREVIOUS_SYNC, <br/>AV_SEEK_CLOSEST = 2<br/>} | 跳转模式 | 
| [AVPlaybackSpeed](#avplaybackspeed) {<br/>AV_SPEED_FORWARD_0_75_X, <br/>AV_SPEED_FORWARD_1_00_X, <br/>AV_SPEED_FORWARD_1_25_X, <br/> AV_SPEED_FORWARD_1_75_X,<br/>AV_SPEED_FORWARD_2_00_X<br/>} | 播放速度 | 
| [AVPlayerOnInfoType](#avplayeroninfotype) {<br/>AV_INFO_TYPE_SEEKDONE = 0, <br/>AV_INFO_TYPE_SPEEDDONE = 1, <br/>AV_INFO_TYPE_BITRATEDONE = 2, <br/>AV_INFO_TYPE_EOS = 3,<br/>AV_INFO_TYPE_STATE_CHANGE = 4, <br/>AV_INFO_TYPE_POSITION_UPDATE = 5, <br/>AV_INFO_TYPE_MESSAGE = 6, <br/>AV_INFO_TYPE_VOLUME_CHANGE = 7,<br/>AV_INFO_TYPE_RESOLUTION_CHANGE = 8, <br/>AV_INFO_TYPE_BUFFERING_UPDATE = 9, <br/>AV_INFO_TYPE_BITRATE_COLLECT = 10, <br/>AV_INFO_TYPE_INTERRUPT_EVENT = 11,<br/>AV_INFO_TYPE_DURATION_UPDATE = 12, <br/>AV_INFO_TYPE_IS_LIVE_STREAM = 13, <br/>AV_INFO_TYPE_TRACKCHANGE = 14, <br/>AV_INFO_TYPE_TRACK_INFO_UPDATE = 15,<br/>AV_INFO_TYPE_SUBTITLE_UPDATE = 16, AV_INFO_TYPE_AUDIO_OUTPUT_DEVICE_CHANGE = 17<br/>} | OnInfo类型 | 


### 函数

| 名称 | 描述 | 
| -------- | -------- |
| OH_AVPlayer \*[OH_AVPlayer_Create](#oh_avplayer_create) (void) | 创建播放器。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode)  [OH_AVPlayer_SetURLSource](#oh_avplayer_seturlsource) (OH_AVPlayer \*player, const char \*url) | 设置播放器的播放源。对应的源可以是http url。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode)  [OH_AVPlayer_SetFDSource](#oh_avplayer_setfdsource) (OH_AVPlayer \*player, int32_t fd, int64_t offset, int64_t size) | 设置播放器的播放媒体文件描述符来源。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode)  [OH_AVPlayer_Prepare](#oh_avplayer_prepare) (OH_AVPlayer \*player) | 准备播放环境，异步缓存媒体数据。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode)  [OH_AVPlayer_Play](#oh_avplayer_play) (OH_AVPlayer \*player) | 开始播放。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_Pause](#oh_avplayer_pause) (OH_AVPlayer \*player) | 暂停播放。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_Stop](#oh_avplayer_stop) (OH_AVPlayer \*player) | 停止播放。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_Reset](#oh_avplayer_reset) (OH_AVPlayer \*player) | 将播放器恢复到初始状态。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_Release](#oh_avplayer_release) (OH_AVPlayer \*player) | 异步释放播放器资源。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_ReleaseSync](#oh_avplayer_releasesync) (OH_AVPlayer \*player) | 同步释放播放器资源。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_SetVolume](#oh_avplayer_setvolume) (OH_AVPlayer \*player, float leftVolume, float rightVolume) | 设置播放器的音量。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_Seek](#oh_avplayer_seek) (OH_AVPlayer \*player, int32_t mSeconds, [AVPlayerSeekMode](#avplayerseekmode) mode) | 改变播放位置。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_GetCurrentTime](#oh_avplayer_getcurrenttime) (OH_AVPlayer \*player, int32_t \*currentTime) | 获取播放位置，精确到毫秒。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_GetVideoWidth](#oh_avplayer_getvideowidth) (OH_AVPlayer \*player, int32_t \*videoWidth) | 获取视频宽度。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_GetVideoHeight](#oh_avplayer_getvideoheight) (OH_AVPlayer \*player, int32_t \*videoHeight) | 获取视频高度。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_SetPlaybackSpeed](#oh_avplayer_setplaybackspeed) (OH_AVPlayer \*player, [AVPlaybackSpeed](#avplaybackspeed) speed) | 设置播放器播放速率。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_GetPlaybackSpeed](#oh_avplayer_getplaybackspeed) (OH_AVPlayer \*player, [AVPlaybackSpeed](#avplaybackspeed) \*speed) | 获取当前播放器播放速率。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_SelectBitRate](#oh_avplayer_selectbitrate) (OH_AVPlayer \*player, uint32_t bitRate) | 设置hls播放器使用的码率。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_SetVideoSurface](#oh_avplayer_setvideosurface) (OH_AVPlayer \*player, OHNativeWindow \*window) | 设置播放画面窗口。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_GetDuration](#oh_avplayer_getduration) (OH_AVPlayer \*player, int32_t \*duration) | 获取媒体文件的总时长，精确到毫秒。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_GetState](#oh_avplayer_getstate) (OH_AVPlayer \*player, [AVPlayerState](#avplayerstate) \*state) | 获取当前播放状态。 | 
| bool [OH_AVPlayer_IsPlaying](#oh_avplayer_isplaying) (OH_AVPlayer \*player) | 判断播放器是否在播放。 | 
| bool [OH_AVPlayer_IsLooping](#oh_avplayer_islooping) (OH_AVPlayer \*player) | 判断是用循环播放。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_SetLooping](#oh_avplayer_setlooping) (OH_AVPlayer \*player, bool loop) | 设置循环播放。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_SetPlayerCallback](#oh_avplayer_setplayercallback) (OH_AVPlayer \*player, [AVPlayerCallback](_a_v_player_callback.md) callback) | 设置播放器回调方法。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_SelectTrack](#oh_avplayer_selecttrack) (OH_AVPlayer \*player, int32_t index) | 选择音频轨道。该接口在当前版本暂不支持，将在后续版本开放能力。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_DeselectTrack](#oh_avplayer_deselecttrack) (OH_AVPlayer \*player, int32_t index) | 取消选择当前音频轨道。该接口在当前版本暂不支持，将在后续版本开放能力。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_GetCurrentTrack](#oh_avplayer_getcurrenttrack) (OH_AVPlayer \*player, int32_t trackType, int32_t \*index) | 获取当前有效的轨道索引。该接口在当前版本暂不支持，将在后续版本开放能力。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_SetMediaKeySystemInfoCallback](#oh_avplayer_setmediakeysysteminfocallback) (OH_AVPlayer \*player, Player_MediaKeySystemInfoCallback callback) | 设置播放器媒体密钥系统信息回调的方法。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_GetMediaKeySystemInfo](#oh_avplayer_getmediakeysysteminfo) (OH_AVPlayer \*player, [DRM_MediaKeySystemInfo](../apis-drm-kit/_d_r_m___media_key_system_info.md) \*mediaKeySystemInfo) | 获取媒体密钥系统信息以创建媒体密钥会话。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_SetDecryptionConfig](#oh_avplayer_setdecryptionconfig) (OH_AVPlayer \*player, [MediaKeySession](../apis-drm-kit/_drm.md#mediakeysession) \*mediaKeySession, bool secureVideoPath) | 设置解密信息。 | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_SetAudioRendererInfo](#oh_avplayer_setaudiorendererinfo) (OH_AVPlayer \*player, [OH_AudioStream_Usage](../apis-audio-kit/_o_h_audio.md#oh_audiostream_usage) streamUsage) | 设置player音频流类型。  | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_SetAudioInterruptMode](#oh_avplayer_setaudiointerruptmode) (OH_AVPlayer \*player, [OH_AudioInterrupt_Mode](../apis-audio-kit/_o_h_audio.md#oh_audiointerrupt_mode) interruptMode) | 设置player音频流的打断模式。  | 
| [OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode) [OH_AVPlayer_SetAudioEffectMode](#oh_avplayer_setaudioeffectmode) (OH_AVPlayer \*player, [OH_AudioStream_AudioEffectMode](../apis-audio-kit/_o_h_audio.md#oh_audiostream_audioeffectmode) effectMode) | 设置player音频流的音效模式。  | 



### 变量

| 名称 | 描述 | 
| -------- | -------- |
| [AVPlayerCallback::onInfo](#oninfo) | 监听AVPlayer过程信息，参考[OH_AVPlayerOnInfo](#oh_avplayeroninfo)。 | 
| [AVPlayerCallback::onError](#onerror) | 监听AVPlayer操作错误，参考[OH_AVPlayerOnError](#oh_avplayeronerror)。 | 


## 类型定义说明


### AVPlaybackSpeed

```
typedef enum AVPlaybackSpeed AVPlaybackSpeed
```

**描述**

播放速度

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11


### AVPlayerCallback

```
typedef struct AVPlayerCallback AVPlayerCallback
```

**描述**

OH_AVPlayer中所有回调函数指针的集合，包含[onError](#onerror)和[onInfo](#oninfo)两个成员。应用需注册此实例结构体到OH_AVPlayer实例中，并对回调上报的信息进行处理，保证AVPlayer的正常运行。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11


### AVPlayerOnInfoType

```
typedef enum AVPlayerOnInfoType AVPlayerOnInfoType
```

**描述**

OnInfo类型

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11


### AVPlayerSeekMode

```
typedef enum AVPlayerSeekMode AVPlayerSeekMode
```

**描述**

跳转模式

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11


### AVPlayerState

```
typedef enum AVPlayerState AVPlayerState
```

**描述**

播放状态

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11


### OH_AVPlayerOnError

```
typedef void(* OH_AVPlayerOnError) (OH_AVPlayer *player, int32_t errorCode, const char *errorMsg)
```

**描述**

在API9以上的版本发生错误时调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| errorCode | 错误码，具体请参考[Media错误码](errorcode-media.md) | 
| errorMsg | 错误消息 | 


### OH_AVPlayerOnInfo

```
typedef void(* OH_AVPlayerOnInfo) (OH_AVPlayer *player, AVPlayerOnInfoType type, int32_t extra)
```

**描述**

收到播放器消息时调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针。 | 
| type | 信息类型。具体请参见[AVPlayerOnInfoType](#avplayeroninfotype-1)。 | 
| extra | 其他信息，如播放文件的开始时间位置。 | 


## 枚举类型说明


### AVPlaybackSpeed

```
enum AVPlaybackSpeed
```

**描述**

播放速度

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

| 枚举值 | 描述 | 
| -------- | -------- |
| AV_SPEED_FORWARD_0_75_X | 0.75倍速播放 | 
| AV_SPEED_FORWARD_1_00_X | 正常播放 | 
| AV_SPEED_FORWARD_1_25_X | 1.25倍速播放 | 
| AV_SPEED_FORWARD_1_75_X | 1.75倍速播放 | 
| AV_SPEED_FORWARD_2_00_X | 2.0倍速播放 | 
| AV_SPEED_FORWARD_0_50_X | 0.5倍速播放<br>**起始版本：** 12 | 
| AV_SPEED_FORWARD_1_50_X | 1.5倍速播放<br>**起始版本：** 12 | 


### AVPlayerOnInfoType

```
enum AVPlayerOnInfoType
```

**描述**

OnInfo类型

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

| 枚举值 | 描述 |
| -------- | -------- |
| AV_INFO_TYPE_SEEKDONE | 跳转到对应播放位置时返回消息，extra表示seek到的位置。 |
| AV_INFO_TYPE_SPEEDDONE | 播放倍速设置完成时返回消息，extra表示播放倍速信息，具体请参考[AVPlaybackSpeed](#avplaybackspeed-1)。 |
| AV_INFO_TYPE_BITRATEDONE | 比特率设置完成时返回消息，extra表示比特率信息。 |
| AV_INFO_TYPE_EOS | 播放完成时返回消息，extra表示是否设置循环播放，0表示设置循环，1表示未设置循环。|
| AV_INFO_TYPE_STATE_CHANGE | 状态改变时返回消息，extra表示当前播放状态，具体请参见[AVPlayerState](#avplayerstate-1)。 |
| AV_INFO_TYPE_POSITION_UPDATE | 返回当前播放位置，extra表示当前位置。 |
| AV_INFO_TYPE_MESSAGE | 视频开始渲染时返回消息，extra表示视频首帧渲染。 |
| AV_INFO_TYPE_VOLUME_CHANGE | 音量改变时返回消息，此场景extra未定义。 |
| AV_INFO_TYPE_RESOLUTION_CHANGE | 首次获取视频大小或视频大小更新时返回消息，此场景extra未定义。 |
| AV_INFO_TYPE_BUFFERING_UPDATE | 返回多队列缓冲时间，extra表示视频时长。 |
| AV_INFO_TYPE_BITRATE_COLLECT | 返回hls比特率，此场景extra未定义。 |
| AV_INFO_TYPE_INTERRUPT_EVENT | 音频焦点改变时返回消息，extra表示音频打断提示，具体请参见[OH_AudioInterrupt_Hint](../apis-audio-kit/_o_h_audio.md#oh_audiointerrupt_hint)，应用可决定是否根据打断提示作进一步处理。 |
| AV_INFO_TYPE_DURATION_UPDATE | 返回播放时长，extra表示视频时长。 |
| AV_INFO_TYPE_IS_LIVE_STREAM | 播放为直播流时返回消息，extra表示是否为直播流，0表示非直播流，1表示直播流。 |
| AV_INFO_TYPE_TRACKCHANGE | 轨道改变时返回消息，此场景extra未定义。 |
| AV_INFO_TYPE_TRACK_INFO_UPDATE | 轨道更新时返回消息，此场景extra未定义。 |
| AV_INFO_TYPE_SUBTITLE_UPDATE | 字幕信息更新时返回消息，此场景extra未定义。 |
| AV_INFO_TYPE_AUDIO_OUTPUT_DEVICE_CHANGE | 音频输出设备改变时返回消息，extra表示设备改变原因，具体请参见[OH_AudioStream_DeviceChangeReason](../apis-audio-kit/_o_h_audio.md#oh_audiostream_devicechangereason)。 |


### AVPlayerSeekMode

```
enum AVPlayerSeekMode
```

**描述**

跳转模式

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

| 枚举值 | 描述 | 
| -------- | -------- |
| AV_SEEK_NEXT_SYNC | 同步到时间点之后的关键帧。 | 
| AV_SEEK_PREVIOUS_SYNC | 同步到时间点之前的关键帧。 | 
| AV_SEEK_CLOSEST | 同步到距离指定时间点最近的帧。<br/>**起始版本：** 12 | 


### AVPlayerState

```
enum AVPlayerState
```

**描述**

播放状态

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

| 枚举值 | 描述 | 
| -------- | -------- |
| AV_IDLE | 空闲 | 
| AV_INITIALIZED | 初始化 | 
| AV_PREPARED | 准备 | 
| AV_PLAYING | 播放 | 
| AV_PAUSED | 暂停 | 
| AV_STOPPED | 停止 | 
| AV_COMPLETED | 结束 | 
| AV_RELEASED | 释放 | 
| AV_ERROR | 错误 | 


## 函数说明


### OH_AVPlayer_Create()

```
OH_AVPlayer* OH_AVPlayer_Create (void)
```
**描述**
创建播放器。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**返回：**

如果创建成功返回指向OH_AVPlayer实例的指针，否则返回空指针。

可能的失败原因：

1. PlayerFactory::CreatePlayer执行失败；
2. new PlayerObject执行失败。


### OH_AVPlayer_DeselectTrack()

```
OH_AVErrCode OH_AVPlayer_DeselectTrack (OH_AVPlayer *player, int32_t index)
```
**描述**
取消选择当前音频轨道。该接口在当前版本暂不支持，将在后续版本开放能力。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| index | 索引  | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功取消。

AV_ERR_INVALID_VAL：输入player为空指针、player DeselectTrack执行失败。


### OH_AVPlayer_GetCurrentTime()

```
OH_AVErrCode OH_AVPlayer_GetCurrentTime (OH_AVPlayer *player, int32_t *currentTime)
```
**描述**
获取播放位置，精确到毫秒。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| currentTime | 播放位置 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：获取当前位置。

AV_ERR_INVALID_VAL：输入player为空指针、player GetCurrentTime执行失败。


### OH_AVPlayer_GetCurrentTrack()

```
OH_AVErrCode OH_AVPlayer_GetCurrentTrack (OH_AVPlayer *player, int32_t trackType, int32_t *index)
```
**描述**
获取当前有效的轨道索引。该接口在当前版本暂不支持，将在后续版本开放能力。

请将其设置为准备/正在播放/暂停/完成状态。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| trackType | 媒体类型。0：音频，1：视频 | 
| index | 索引 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功获取。

AV_ERR_INVALID_VAL：输入player为空指针、player GetCurrentTrack执行失败。


### OH_AVPlayer_GetDuration()

```
OH_AVErrCode OH_AVPlayer_GetDuration (OH_AVPlayer *player, int32_t *duration)
```
**描述**
获取媒体文件的总时长，精确到毫秒。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| duration | 媒体文件的总时长 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：获取当前时长。

AV_ERR_INVALID_VAL：输入player为空指针、player GetDuration执行失败。


### OH_AVPlayer_GetMediaKeySystemInfo()

```
OH_AVErrCode OH_AVPlayer_GetMediaKeySystemInfo (OH_AVPlayer *player, DRM_MediaKeySystemInfo *mediaKeySystemInfo)
```
**描述**
获取媒体密钥系统信息以创建媒体密钥会话。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 12

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 |
| mediaKeySystemInfo | 媒体密钥系统信息 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功设置。

AV_ERR_INVALID_VAL：输入player为空指针、内存不足。

### OH_AVPlayer_GetPlaybackSpeed()

```
OH_AVErrCode OH_AVPlayer_GetPlaybackSpeed (OH_AVPlayer *player, AVPlaybackSpeed *speed)
```
**描述**
获取当前播放器播放速率。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| speed | 可以获取的速率模式[AVPlaybackSpeed](#avplaybackspeed) | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功获取播放速率。

AV_ERR_INVALID_VAL：输入player为空指针、player GetPlaybackSpeed执行失败。


### OH_AVPlayer_GetState()

```
OH_AVErrCode OH_AVPlayer_GetState (OH_AVPlayer *player, AVPlayerState *state)
```
**描述**
获取当前播放状态。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| state | 当前播放状态 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：获取当前播放状态。

AV_ERR_INVALID_VAL：输入player为空指针、player GetState执行失败。


### OH_AVPlayer_GetVideoHeight()

```
OH_AVErrCode OH_AVPlayer_GetVideoHeight (OH_AVPlayer *player, int32_t *videoHeight)
```
**描述**
获取视频高度。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| videoHeights | 视频高度 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功获取视频高度。

AV_ERR_INVALID_VAL：输入player为空指针。


### OH_AVPlayer_GetVideoWidth()

```
OH_AVErrCode OH_AVPlayer_GetVideoWidth (OH_AVPlayer *player, int32_t *videoWidth)
```
**描述**
获取视频宽度。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| videoWidth | 视频宽度 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功获取视频宽度。

AV_ERR_INVALID_VAL：输入player为空指针。


### OH_AVPlayer_IsLooping()

```
bool OH_AVPlayer_IsLooping (OH_AVPlayer *player)
```
**描述**
判断是否循环播放。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 

**返回：**

如果循环播放，则返回true；如果不是循环播放或者输入player为空指针则返回false。


### OH_AVPlayer_IsPlaying()

```
bool OH_AVPlayer_IsPlaying (OH_AVPlayer *player)
```
**描述**
判断播放器是否在播放。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 

**返回：**

如果正在播放，则返回true；如果不在播放或者输入player为空指针则返回false。


### OH_AVPlayer_Pause()

```
OH_AVErrCode OH_AVPlayer_Pause (OH_AVPlayer *player)
```
**描述**
暂停播放。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功将**Pause**添加到任务队列中。

AV_ERR_INVALID_VAL：输入player为空指针、player Pause执行失败。


### OH_AVPlayer_Play()

```
OH_AVErrCode OH_AVPlayer_Play (OH_AVPlayer *player)
```
**描述**
开始播放。

此函数必须在**Prepare**之后调用。如果播放器状态为&lt;Prepared&gt;。调用此函数开始播放。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：开始播放。

AV_ERR_INVALID_VAL：输入player为空指针、player Play执行失败。


### OH_AVPlayer_Prepare()

```
OH_AVErrCode OH_AVPlayer_Prepare (OH_AVPlayer *player)
```
**描述**
准备播放环境，异步缓存媒体数据。

此函数必须在**SetSource**之后调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功将**Prepare**添加到任务队列中。

AV_ERR_INVALID_VAL：输入player为空指针、player Prepare执行失败。


### OH_AVPlayer_Release()

```
OH_AVErrCode OH_AVPlayer_Release (OH_AVPlayer *player)
```
**描述**
异步释放播放器资源。

异步释放保证性能，但无法保证是否释放了播放画面的surfacebuffer。调用者需要保证播放画面窗口的生命周期安全。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功将**Release**添加到任务队列中。

AV_ERR_INVALID_VAL：输入player为空指针、player Release执行失败。


### OH_AVPlayer_ReleaseSync()

```
OH_AVErrCode OH_AVPlayer_ReleaseSync (OH_AVPlayer *player)
```
**描述**
同步释放播放器资源。

同步过程保证了播放画面的显示缓存释放，但这个过程花费时间较长，要求调用者自己设计异步机制。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：播放被释放。

AV_ERR_INVALID_VAL：输入player为空指针、player ReleaseSync执行失败。

### OH_AVPlayer_Reset()

```
OH_AVErrCode OH_AVPlayer_Reset (OH_AVPlayer *player)
```
**描述**
将播放器恢复到初始状态。

函数调用完成后，调用**SetSource**添加播放源。调用**Prepare**后，调用**Play**重新开始播放。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功将**reset**添加到任务队列。

AV_ERR_INVALID_VAL：输入player为空指针、player Reset执行失败。


### OH_AVPlayer_Seek()

```
OH_AVErrCode OH_AVPlayer_Seek (OH_AVPlayer *player, int32_t mSeconds, AVPlayerSeekMode mode)
```
**描述**
改变播放位置。

此函数可以在播放或暂停时使用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针。 | 
| mSeconds | 播放目标位置，精确到毫秒。 | 
| mode | 播放器的跳转模式。具体请参考[AVPlayerSeekMode](#avplayerseekmode)。 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：完成跳转。

AV_ERR_INVALID_VAL：输入player为空指针、player Seek执行失败。


### OH_AVPlayer_SelectBitRate()

```
OH_AVErrCode OH_AVPlayer_SelectBitRate (OH_AVPlayer *player, uint32_t bitRate)
```
**描述**
设置hls播放器使用的码率。

播放比特率，以比特/秒为单位，以比特/秒为单位。 仅对HLS协议网络流有效。默认情况下， 播放器会根据网络连接情况选择合适的码率和速度。 通过INFO_TYPE_BITRATE_COLLECT上报有效码率链表 设置并选择指定的码率，选择小于和最接近的码率 到指定的码率播放。准备好后，读取它以查询当前选择的比特率。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| bitRate | 码率，单位为bps | 

**返回：**

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：设置码率成功。

AV_ERR_INVALID_VAL：输入player为空指针、player SelectBitRate执行失败。


### OH_AVPlayer_SelectTrack()

```
OH_AVErrCode OH_AVPlayer_SelectTrack (OH_AVPlayer *player, int32_t index)
```
**描述**
选择音频轨道。该接口在当前版本暂不支持，将在后续版本开放能力。

默认播放第一个带数据的音频流。设置生效后，原曲目将失效。将音轨设置为准备状态。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| index | 索引 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功选择。

AV_ERR_INVALID_VAL：输入player为空指针、player SelectTrack执行失败。


### OH_AVPlayer_SetAudioEffectMode()

```
OH_AVErrCode OH_AVPlayer_SetAudioEffectMode (OH_AVPlayer *player, OH_AudioStream_AudioEffectMode effectMode)
```
**描述**
设置player音频流的音效模式。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 12

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针。  | 
| interruptMode | player音频流使用的音效模式[OH_AudioStream_AudioEffectMode](../apis-audio-kit/_o_h_audio.md#oh_audiostream_audioeffectmode)。  | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功设置。

AV_ERR_INVALID_VAL：输入player为空指针或者effectMode值无效。


### OH_AVPlayer_SetAudioInterruptMode()

```
OH_AVErrCode OH_AVPlayer_SetAudioInterruptMode (OH_AVPlayer *player, OH_AudioInterrupt_Mode interruptMode)
```
**描述**
设置player音频流的打断模式。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 12

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针。  | 
| interruptMode | player音频流使用的打断模式[OH_AudioStream_Usage](../apis-audio-kit/_o_h_audio.md#oh_audiostream_usage)。  | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功设置。

AV_ERR_INVALID_VAL：输入player为空指针或者interruptMode值无效。


### OH_AVPlayer_SetAudioRendererInfo()

```
OH_AVErrCode OH_AVPlayer_SetAudioRendererInfo (OH_AVPlayer *player, OH_AudioStream_Usage streamUsage)
```
**描述**
设置player音频流类型。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 12

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针。  | 
| streamUsage | player音频流设置的类型[OH_AudioStream_Usage](../apis-audio-kit/_o_h_audio.md#oh_audiostream_usage)。  | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功设置。

AV_ERR_INVALID_VAL：输入player为空指针或者streamUsage值无效。


### OH_AVPlayer_SetDecryptionConfig()

```
OH_AVErrCode OH_AVPlayer_SetDecryptionConfig (OH_AVPlayer *player, MediaKeySession *mediaKeySession, bool secureVideoPath)
```
**描述**
设置解密信息。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 12

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针。 | 
| mediaKeySession | 具有解密功能的媒体密钥会话实例。 | 
| secureVideoPath | 是否需要安全解码器。 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功设置。

AV_ERR_INVALID_VAL：输入player为空指针、player SetDecryptionConfig执行失败。


### OH_AVPlayer_SetFDSource()

```
OH_AVErrCode OH_AVPlayer_SetFDSource (OH_AVPlayer *player, int32_t fd, int64_t offset, int64_t size)
```
**描述**
设置播放器的播放媒体文件描述符来源。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| fd | 媒体源的文件描述符 | 
| offset | 媒体源在文件描述符中的偏移量 | 
| size | 表示媒体源的大小 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：fd设置成功。

AV_ERR_INVALID_VAL：输入player为空指针、player SetFdSource执行失败。


### OH_AVPlayer_SetLooping()

```
OH_AVErrCode OH_AVPlayer_SetLooping (OH_AVPlayer *player, bool loop)
```
**描述**
设置循环播放。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| loop | 循环播放开关 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：循环播放设置成功。

AV_ERR_INVALID_VAL：输入player为空指针、player SetLooping执行失败。


### OH_AVPlayer_SetMediaKeySystemInfoCallback()

```
OH_AVErrCode OH_AVPlayer_SetMediaKeySystemInfoCallback (OH_AVPlayer *player, Player_MediaKeySystemInfoCallback callback)
```
**描述**
设置播放器媒体密钥系统信息回调的方法。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 12

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针。 | 
| callback | 对象指针。 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：设置成功。

AV_ERR_INVALID_VAL：输入player为空指针、callback为空指针、player SetDrmSystemInfoCallback，SetDrmSystemInfoCallback或SetDrmSystemInfoCallback执行失败。


### OH_AVPlayer_SetPlaybackSpeed()

```
OH_AVErrCode OH_AVPlayer_SetPlaybackSpeed (OH_AVPlayer *player, AVPlaybackSpeed speed)
```
**描述**
设置播放器播放速率。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| speed | 可以设置速率模式[AVPlaybackSpeed](#avplaybackspeed) | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功设置播放速率。

AV_ERR_INVALID_VAL：输入player为空指针。


### OH_AVPlayer_SetPlayerCallback()

```
OH_AVErrCode OH_AVPlayer_SetPlayerCallback (OH_AVPlayer *player, AVPlayerCallback callback)
```
**描述**
设置播放器回调方法。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| callback | 回调对象指针 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功设置播放器回调。

AV_ERR_INVALID_VAL：输入player为空指针、callback.onInfo或onError为空、player SetPlayerCallback执行失败。


### OH_AVPlayer_SetURLSource()

```
OH_AVErrCode OH_AVPlayer_SetURLSource (OH_AVPlayer *player, const char *url)
```
**描述**
设置播放器的播放源。对应的源可以是http url。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| url | 播放源 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：设置成功。

AV_ERR_INVALID_VAL：输入player为空指针、url为空、player SetUrlSource执行失败。


### OH_AVPlayer_SetVideoSurface()

```
OH_AVErrCode OH_AVPlayer_SetVideoSurface (OH_AVPlayer *player, OHNativeWindow *window)
```
**描述**
设置播放画面窗口。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| window | 指向OHNativeWindow实例的指针 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：设置播放画面窗口成功。

AV_ERR_INVALID_VAL：输入player为空指针、输入window为空指针、player SetVideoSurface执行失败。


### OH_AVPlayer_SetVolume()

```
OH_AVErrCode OH_AVPlayer_SetVolume (OH_AVPlayer *player, float leftVolume, float rightVolume)
```
**描述**
设置播放器的音量。

可以在播放或暂停的过程中使用。&lt;0&gt;表示无声音，&lt;1&gt;为原始值。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 
| leftVolume | 要设置的左声道目标音量 | 
| rightVolume | 要设置的右声道目标音量 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：设置音量成功。

AV_ERR_INVALID_VAL：输入player为空指针、player SetVolume执行失败。


### OH_AVPlayer_Stop()

```
OH_AVErrCode OH_AVPlayer_Stop (OH_AVPlayer *player)
```
**描述**
停止播放。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| player | 指向OH_AVPlayer实例的指针 | 

**返回：**

函数结果代码[OH_AVErrCode](../apis-avcodec-kit/_core.md#oh_averrcode-1)：

AV_ERR_OK：成功将**stop**添加到任务队列。

AV_ERR_INVALID_VAL：输入player为空指针、player Stop执行失败。


## 变量说明


### onError

```
OH_AVPlayerOnError AVPlayerCallback::onError
```

**描述**

监听AVPlayer操作错误，参考[OH_AVPlayerOnError](#oh_avplayeronerror)。


### onInfo

```
OH_AVPlayerOnInfo AVPlayerCallback::onInfo
```

**描述**

监听AVPlayer过程信息，参考[OH_AVPlayerOnInfo](#oh_avplayeroninfo)。
