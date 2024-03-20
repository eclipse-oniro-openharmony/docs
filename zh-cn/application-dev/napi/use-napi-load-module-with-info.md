# ʹ��NAPI�ӿ���C++�´������߳��н���ģ�����

Node-API�е�napi_load_module_with_info�ӿڵĹ�������C++�´������߳��н���ģ��ļ��أ���ģ����س���֮�󣬿���ʹ�ú���napi_get_property��ȡģ�鵼���ı�����Ҳ����ʹ��napi_get_named_property��ȡģ�鵼���ĺ�����Ŀǰ֧�����³�����
- ����ϵͳģ��
- ����etsĿ¼���ļ��е�ģ��
- ����HAR��(��̬�����)
- ���ر���so��

## ����ϵͳģ��ʹ��ʾ��
```cpp
static napi_value loadModule(napi_env env, napi_callback_info info) {
    //1. ʹ��napi_load_module����ģ��@ohos.hilog
    napi_value result;
    napi_status status = napi_load_module_with_info(env, "@ohos.hilog", nullptr, &result);
    
    //2. ʹ��napi_get_named_property��ȡinfo����
    napi_value infoFn;
    napi_get_named_property(env, result, "info", &infoFn);
    
    napi_value tag;
    std::string formatStr = "test";
    napi_create_string_utf8(env, formatStr.c_str(), formatStr.size(), &tag);
    
    napi_value outputString;
    std::string str = "Hello OpenHarmony";
    napi_create_string_utf8(env, str.c_str(), str.size(), &outputString);
    
    napi_value flag;
    napi_create_int32(env, 0, &flag);

    napi_value args[3] = {flag, tag, outputString};
    //3. ʹ��napi_call_function����info����
    napi_call_function(env, result, infoFn, 3, args, nullptr);
    return result
}
```

## ����ArkTs�ļ��е�ģ��ʹ��ʾ��

�������ļ��е�ģ��ʱ��������ArkTS���룺
```javascript
//./src/main/ets/Test.ets
let value = 123;
function test() {
  console.log("Hello OpenHarmony");
}
export {value, test};
```

1. ��Ҫ�ڹ��̵�build-profile.json5�ļ��н�����������
```json
{
    "buildOption" : {
        "arkOptions" : {
            "runtimeOnly" : {
                "sources": [
                    "./src/main/ets/Test.ets"
                ]
            }
        }
    }
}
```


2. ʹ��napi_load_module_with_info����Test�ļ������ú���test�Լ���ȡ����value

```cpp
static napi_value loadModule(napi_env env, napi_callback_info info) {
    napi_value result;
    //1. ʹ��napi_load_module����Test�ļ��е�ģ��
    napi_status status = napi_load_module_with_info(env, "entry/src/main/ets/Test", "com.example.application/entry", &result);

    napi_value testFn;
    //2. ʹ��napi_get_named_property��ȡtest����
    napi_get_named_property(env, result, "test", &testFn);
    //3. ʹ��napi_call_function���ú���test
    napi_call_function(env, result, testFn, 0, nullptr, nullptr);

    napi_value value;
    napi_value key;
    std::string keyStr = "value";
    napi_create_string_utf8(env, keyStr.c_str(), keyStr.size(), &key);
    //4. ʹ��napi_get_property��ȡ����value
    napi_get_property(env, result, key, &value);
    return result
}
```

## ����HAR��(��̬�����)

### ���ر���HAR��,
HAR��Index.ets�ļ�����
```javascript
//library Index.ets
let value = 123;
function test() {
  console.log("Hello OpenHarmony");
}
export {value, test};
```
1. �ڼ��ر���HAR��ʱ��������Ҫ��oh-package.json5�ļ�������dependencies��
```json
{
    "dependencies": {
        "library": "file:../library"
    }
}
```
2. ��Σ�����Ҫ��build-profile.json5�н�������
```json
{
    "buildOption" : {
        "arkOptions" : {
            "runtimeOnly" : {
                "packages": [
                    "library"
                ]
            }
        }
    }
}
```

3. ��napi_load_module_with_info����library�����ú���test�Լ���ȡ����value
```cpp
static napi_value loadModule(napi_env env, napi_callback_info info) {
    napi_value result;
    //1. ʹ��napi_load_module����Test�ļ��е�ģ��
    napi_status status = napi_load_module_with_info(env, "library", "com.example.application/entry", &result);

    napi_value testFn;
    //2. ʹ��napi_get_named_property��ȡtest����
    napi_get_named_property(env, result, "test", &testFn);
    //3. ʹ��napi_call_function���ú���test
    napi_call_function(env, result, testFn, 0, nullptr, nullptr);

    napi_value value;
    napi_value key;
    std::string keyStr = "value";
    napi_create_string_utf8(env, keyStr.c_str(), keyStr.size(), &key);
    //4. ʹ��napi_get_property��ȡ����value
    napi_get_property(env, result, key, &value);
    return result
}
```
### ���ص�����HAR��

1. �ڼ��ص�����HAR��ʱ��������Ҫ��oh-package.json5�ļ�������dependencies��
```json
{
    "dependencies": {
        "json5": "^2.2.3"
    }
}
```
2. ��Σ�����Ҫ��build-profile.json5�н�������
```json
{
    "buildOption" : {
        "arkOptions" : {
            "runtimeOnly" : {
                "packages": [
                    "json5"
                ]
            }
        }
    }
}
```

3. ��napi_load_module_with_info����json5�����ú���stringify
```cpp
static napi_value loadModule(napi_env env, napi_callback_info info) {
    napi_value result;
    //1. ʹ��napi_load_module����json5
    napi_status status = napi_load_module_with_info(env, "json5", "com.example.application/entry", &result);

    napi_value key;
    std::string keyStr = "default";
    napi_create_string_utf8(env, keyStr.c_str(), keyStr.size(), &key);
    //2. ʹ��napi_get_property��ȡdefault����
    napi_value defaultValue;
    napi_get_property(env, result, key, &defaultValue);

    napi_value stringifyFn;
    //3. ʹ��napi_get_named_property��ȡstringify����
    napi_get_named_property(env, defaultValue, "stringify", &stringifyFn);
    //4. ʹ��napi_call_function���ú���stringify
    napi_value argStr;
    std::string info = "call json5 stringify";
    napi_create_string_utf8(env, info.c_str(), info.size(), &argStr);
    napi_value args[1] = {argStr};

    napi_value returnValue;
    napi_call_function(env, result, stringifyFn, 1, args, &returnValue);
    return result
}
```

## ���ر���so��
libentry.so��index.d.ts�ļ�����
```javascript
//index.d.ts
export const add: (a: number, b: number) => number;

```
1. �ڼ��ر���so��ʱ��������Ҫ��oh-package.json5�ļ�������dependencies��
```json
{
    "dependencies": {
        "libentry.so": "file../src/main/cpp/types/libentry"
    }
}
```
2. ��Σ�����Ҫ��build-profile.json5�н�������
```json
{
    "buildOption" : {
        "arkOptions" : {
            "runtimeOnly" : {
                "packages": [
                    "libentry.so"
                ]
            }
        }
    }
}
```

3. ��napi_load_module_with_info����libentry.so�����ú���add
```cpp
static napi_value loadModule(napi_env env, napi_callback_info info) {
    napi_value result;
    //1. ʹ��napi_load_module����libentry.so
    napi_status status = napi_load_module_with_info(env, "libentry.so", "com.example.application/entry", &result);

    napi_value addFn;
    //2. ʹ��napi_get_named_property��ȡadd����
    napi_get_named_property(env, result, "add", &result);
    
    napi_value a;
    napi_value b;
    napi_create_int32(env, 2, &a);
    napi_create_int32(env, 3, &b);
    napi_value args[1] = {a, b};
    //3. ʹ��napi_call_function���ú���add
    napi_value returnValue;
    napi_call_function(env, result, addFn, 2, args, &returnValue);
    return result
}
```