# 示例代码

## 新增群组关键资产

```c
#include <string.h>

#include "asset/asset_api.h"

void AddAsset() {
    static const char *SECRET = "demo_pwd";
    static const char *ALIAS = "demo_alias";
    static const char *LABEL = "demo_label";
    static const char *GROUP_ID = "demo_group_id;

    Asset_Blob secret = { (uint32_t)(strlen(SECRET)), (uint8_t *)SECRET };
    Asset_Blob alias = { (uint32_t)(strlen(ALIAS)), (uint8_t *)ALIAS };
    Asset_Blob label = { (uint32_t)(strlen(LABEL)), (uint8_t *)LABEL };
    Asset_Blob group_id = { (uint32_t)(strlen(GROUP_ID)), (uint8_t *)GROUP_ID };
    Asset_Attr attr[] = {
        { .tag = ASSET_TAG_ACCESSIBILITY, .value.u32 = ASSET_ACCESSIBILITY_DEVICE_FIRST_UNLOCKED },
        { .tag = ASSET_TAG_SECRET, .value.blob = secret },
        { .tag = ASSET_TAG_ALIAS, .value.blob = alias },
        { .tag = ASSET_TAG_DATA_LABEL_NORMAL_1, .value.blob = label },
        { .tag = ASSET_TAG_GROUP_ID, .value.blob = group_id },
    };

    int32_t ret = OH_Asset_Add(attr, sizeof(attr) / sizeof(attr[0]));
    if (ret == ASSET_SUCCESS) {
        // Asset added to the group successfully.
    } else {
        // Failed to add Asset to the group.
    }
}
```

## 删除群组关键资产

```c
#include <string.h>

#include "asset/asset_api.h"

void RemoveAsset() {
    static const char *ALIAS = "demo_alias";
    static const char *GROUP_ID = "demo_group_id";

    Asset_Blob alias = { (uint32_t)(strlen(ALIAS)), (uint8_t *)ALIAS };
    Asset_Blob group_id = { (uint32_t)(strlen(GROUP_ID)), (uint8_t *)GROUP_ID };
    Asset_Attr attr[] = {
        { .tag = ASSET_TAG_ALIAS, .value.blob = alias }, // 此处指定别名删除单条群组关键资产，也可不指定别名删除多条群组关键资产
        { .tag = ASSET_TAG_GROUP_ID, .value.blob = group_id },
    };

    int32_t ret = OH_Asset_Remove(attr, sizeof(attr) / sizeof(attr[0]));
    if (ret == ASSET_SUCCESS) {
        // Asset removed from the group successfully.
    } else {
        // Failed to remove Asset from the group.
    }
}
```

## 更新群组关键资产

```c
#include <string.h>

#include "asset/asset_api.h"

void UpdateAsset() {
    static const char *ALIAS = "demo_alias";
    static const char *SECRET = "demo_pwd_new";
    static const char *LABEL = "demo_label_new";
    static const char *GROUP_ID = "demo_group_id";
    
    Asset_Blob alias = { (uint32_t)(strlen(ALIAS)), (uint8_t *)ALIAS };
    Asset_Blob new_secret = { (uint32_t)(strlen(SECRET)), (uint8_t *)SECRET };
    Asset_Blob new_label = { (uint32_t)(strlen(LABEL)), (uint8_t *)LABEL };
    Asset_Blob group_id = { (uint32_t)(strlen(GROUP_ID)), (uint8_t *)GROUP_ID };
    Asset_Attr query[] = { 
        { .tag = ASSET_TAG_ALIAS, .value.blob = alias },
        { .tag = ASSET_TAG_GROUP_ID, .value.blob = group_id },
    };
    Asset_Attr attributesToUpdate[] = {
        { .tag = ASSET_TAG_SECRET, .value.blob = new_secret },
        { .tag = ASSET_TAG_DATA_LABEL_NORMAL_1, .value.blob = new_label },
    };

    int32_t ret = OH_Asset_Update(query, sizeof(query) / sizeof(query[0]), attributesToUpdate,
                                sizeof(attributesToUpdate) / sizeof(attributesToUpdate[0]));
    if (ret == ASSET_SUCCESS) {
        // Asset updated in the group successfully.
    } else {
        // Failed to update Asset in the group.
    }
}
```

## 查询单条群组关键资产属性

```c
#include <string.h>

#include "asset/asset_api.h"

void QueryAttributes() {
    static const char *ALIAS = "demo_alias";
    static const char *GROUP_ID = "demo_group_id";
    Asset_Blob alias = { (uint32_t)(strlen(ALIAS)), (uint8_t *)ALIAS };
    Asset_Blob group_id = { (uint32_t)(strlen(GROUP_ID)), (uint8_t *)GROUP_ID };
    Asset_Attr attr[] = {
        { .tag = ASSET_TAG_ALIAS, .value.blob = alias }, // 指定了群组关键资产别名，最多查询到一条满足条件的群组关键资产
        { .tag = ASSET_TAG_RETURN_TYPE, .value.u32 = ASSET_RETURN_ATTRIBUTES }, // 此处表示仅返回群组关键资产属性，不包含群组关键资产明文
        { .tag = ASSET_TAG_GROUP_ID, .value.blob = group_id },
    };

    Asset_ResultSet resultSet = {0};
    int32_t ret = OH_Asset_Query(attr, sizeof(attr) / sizeof(attr[0]), &resultSet);
    if (ret == ASSET_SUCCESS) {
        // Parse the result.
        for (uint32_t i = 0; i < resultSet.count; i++) {
        // Parse the data label: the data is label->blob.data, the size is label->blob.size.
            Asset_Attr *label = OH_Asset_ParseAttr(resultSet.results + i, ASSET_TAG_DATA_LABEL_NORMAL_1);
        }
    }
    OH_Asset_FreeResultSet(&resultSet);
}
```

## 批量查询群组关键资产属性

```c
#include <string.h>

#include "asset/asset_api.h"

void BatchQuery() {
    static const char *LABEL = "demo_label";
    static const char *GROUP_ID = "demo_group_id";
    Asset_Blob label = { (uint32_t)(strlen(LABEL)), (uint8_t *)LABEL };
    Asset_Blob group_id = { (uint32_t)(strlen(GROUP_ID)), (uint8_t *)GROUP_ID };

    Asset_Attr attr[] = {
        { .tag = ASSET_TAG_RETURN_TYPE, .value.u32 = ASSET_RETURN_ATTRIBUTES },
        { .tag = ASSET_TAG_DATA_LABEL_NORMAL_1, .value.blob = label },
        { .tag = ASSET_TAG_RETURN_OFFSET, .value.u32 = 5 },
        { .tag = ASSET_TAG_RETURN_LIMIT, .value.u32 = 10 },
        { .tag = ASSET_TAG_RETURN_ORDERED_BY, .value.u32 = ASSET_TAG_DATA_LABEL_NORMAL_1 },
        { .tag = ASSET_TAG_GROUP_ID, .value.blob = group_id },
    };

    Asset_ResultSet resultSet = { 0 };
    int32_t ret = OH_Asset_Query(attr, sizeof(attr) / sizeof(attr[0]), &resultSet);
    if (ret == ASSET_SUCCESS) {
        // Parse the result.
        for (uint32_t i = 0; i < resultSet.count; i++) {
            // Parse the data alias: the data is alias->blob.data, the size is alias->blob.size..
            Asset_Attr *alias = OH_Asset_ParseAttr(resultSet.results + i, ASSET_TAG_ALIAS);
        }
    }
    OH_Asset_FreeResultSet(&resultSet);
}
```