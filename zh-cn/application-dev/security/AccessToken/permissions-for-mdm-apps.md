# 仅对MDM应用开放

以下权限仅对MDM（Mobile Device Management）设备管理应用开放。MDM应用的详细介绍，请参考[MDM Kit简介](../../mdm/mdm-kit-intro.md)。

## ohos.permission.ENTERPRISE_GET_DEVICE_INFO

允许应用激活设备管理应用。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_GET_NETWORK_INFO

允许设备管理应用查询网络信息。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_INSTALL_BUNDLE

允许设备管理应用安装和卸载包。

**权限级别**：system_core

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_MANAGE_SET_APP_RUNNING_POLICY

允许设备管理应用设置应用运行管理策略。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_RESET_DEVICE

允许设备管理应用恢复设备出厂设置。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_SET_ACCOUNT_POLICY

允许设备管理应用设置账户管理策略。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_SET_BUNDLE_INSTALL_POLICY

允许设备管理应用设置包安装管理策略。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_SET_DATETIME

允许设备管理应用设置系统时间。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：9

## ohos.permission.ENTERPRISE_SET_NETWORK

允许设备管理应用设置网络信息。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_SET_WIFI

允许设备管理应用设置和查询WiFi信息。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_SUBSCRIBE_MANAGED_EVENT

允许设备管理应用订阅管理事件。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：9

## ohos.permission.ENTERPRISE_RESTRICT_POLICY

允许设备管理员下发和获取限制类策略。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_SET_SCREENOFF_TIME

允许设备管理员设置系统休眠时间。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_MANAGE_USB

允许设备管理员管理USB。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_MANAGE_NETWORK

允许设备管理员管理网络。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_MANAGE_CERTIFICATE

允许设备管理员管理证书。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_GET_SETTINGS

允许设备管理员查询“设置”应用数据。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.INSTALL_ENTERPRISE_MDM_BUNDLE

允许在企业设备上安装企业MDM应用包。

**权限级别**：system_core

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.INSTALL_SELF_BUNDLE

允许企业MDM应用在企业设备上自升级。

**权限级别**：system_core

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.ENTERPRISE_SET_BROWSER_POLICY

允许设备设置/取消浏览器策略。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

## ohos.permission.SET_ENTERPRISE_INFO

允许设备管理应用设置企业信息。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：9

## ohos.permission.SET_FILE_GUARD_POLICY

允许应用下发文件管控策略。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

**变更信息**：API 10-14时，其权限级别为system_core，仅面向MDM应用开放；从API 14开始，权限级别变更为system_basic，开发范围从MDM应用变更为企业普通应用。

## ohos.permission.FILE_GUARD_MANAGER

允许应用进行公共目录扫描及设置文件扩展属性。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

**变更信息**：API 10-14时，其权限级别为system_core，仅面向MDM应用开放；从API 14开始，权限级别变更为system_basic，开发范围从MDM应用变更为企业普通应用。

## ohos.permission.ENTERPRISE_MANAGE_SECURITY

允许设备设置安全管理策略。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：11

## ohos.permission.ENTERPRISE_MANAGE_BLUETOOTH

允许设备管理应用设置和查询蓝牙信息。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：11

## ohos.permission.ENTERPRISE_MANAGE_SYSTEM

允许设备管理系统的设置参数。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：11

## ohos.permission.ENTERPRISE_MANAGE_WIFI

允许设备管理应用设置和查询WIFI信息。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：11

## ohos.permission.ENTERPRISE_MANAGE_RESTRICTIONS

允许设备管理应用管理限制策略。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：11

## ohos.permission.ENTERPRISE_MANAGE_APPLICATION

允许设备管理应用管理应用策略。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：11

## ohos.permission.ENTERPRISE_MANAGE_LOCATION

允许设备管理应用设置和查询位置信息。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：11

## ohos.permission.ENTERPRISE_REBOOT

允许设备管理应用进行关机重启操作。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：11

## ohos.permission.ENTERPRISE_LOCK_DEVICE

允许设备管理应用锁定设备。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：11

## ohos.permission.ENTERPRISE_MANAGE_SETTINGS

允许设备管理应用管理设置。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：11

## ohos.permission.ENTERPRISE_OPERATE_DEVICE

允许设备管理应用操作设备。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：12

## ohos.permission.ENTERPRISE_ADMIN_MANAGE

允许设备管理应用管理设备管理器。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：12

## ohos.permission.QUERY_AUDIT_EVENT

允许MDM应用查询安全审计事件。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：12

## ohos.permission.ENTERPRISE_RECOVERY_KEY

允许应用管理企业级恢复密钥。

**权限级别**：system_core

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：13

## ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

允许应用跨系统本地账号交互。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：7

**变更信息**：API version 7-13该权限仅向系统应用开放；从API version 14开始，开放范围从系统应用变更为企业普通应用。

## ohos.permission.GET_DOMAIN_ACCOUNTS

允许应用查询域账号信息。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：10

**变更信息**：API version 10-13该权限仅向系统应用开放；从API version 14开始，开放范围从系统应用变更为企业普通应用。

## **ohos.permission.ACCESS_ENTERPRISE_USER_TRUSTED_CERT** 

允许应用管理企业设备的用户CA证书。

在企业设备上企业应用使用私有的CA证书认证企业服务器时，该权限用于允许企业应用把私有CA证书安装到企业设备上，并对安装的CA证书进行管理操作。

**权限级别**：system_basic

**授权方式**：system_grant

<!--Del-->
**ACL使能**：true<!--DelEnd-->

**起始版本**：16
