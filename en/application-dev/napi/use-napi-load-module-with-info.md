# Loading a Module Using Node-API

You can use **napi_load_module_with_info** to load modules. After a module is loaded, you can use **napi_get_property** to obtain the variables exported by the module or use **napi_get_named_property** to obtain the functions exported by the module. 

The **napi_load_module_with_info** API can be used in a [newly created ArkTS runtime environment](use-napi-ark-runtime.md).

## Function Description

```cpp
napi_status napi_load_module_with_info(napi_env env,
                                       const char* path,
                                       const char* module_info,
                                       napi_value* result);
```

| Parameter           | Description         |
| :------------- | :----------------------------- |
| env            | Current VM environment.      |
| path          | Path of the file or name of the module to load.         |
| module_info   | Path composed of **bundleName** and **moduleName**.      |
| result         | Module loaded.         |

**NOTE**:

1. **bundleName** indicates the project name configured in **AppScope/app.json5**.
2. **moduleName** indicates the module name configured in **module.json5** in the HAP of the module to be loaded.
3. You can also use [napi_load_module](use-napi-load-module.md) to load modules. However, **napi_load_module** is limited to loading modules in the main thread only.

## When to Use

| Scenario           | Description          | Description                        |
| :------------- | :----------------------------- | :--------------------------- |
| Local project module  | Load a module from a local project file using the relative path to a HAP.      | The file paths must start with **moduleName**.            |
| Local HAR module  | Load a HAR module to a HAP.          | -                            |
| Remote HAR module        | Load a remote HAR module to a HAP.       | -                            |
| Remote ohpm module        | Load an ohpm package to a HAP.           | -                            |
| API        |    Load @ohos. or @system. to a HAP.         | -                            |
| Native library module  | Load **libNativeLibrary.so** to a HAP.| -                            |



## How to Use

- Loading a module from a local project file to a HAP

Load a module from a file as shown in the following ArkTS code.

```javascript
//./src/main/ets/Test.ets
let value = 123;
function test() {
  console.log("Hello OpenHarmony");
}
export {value, test};
```

1. Add the following to the **build-profile.json5** file of the project.

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

2. Use **napi_load_module_with_info** to load the **Test.ets** file, call the **test()** function, and obtain the variable values.

```cpp
static napi_value loadModule(napi_env env, napi_callback_info info) {
    napi_value result;
    // 1. Call napi_load_module_with_info to load the module from the Test.ets file.
    napi_status status = napi_load_module_with_info(env, "entry/src/main/ets/Test", "com.example.application/entry", &result);

    napi_value testFn;
    // 2. Call napi_get_named_property to obtain the test function.
    napi_get_named_property(env, result, "test", &testFn);
    // 3. Call napi_call_function to call the test function.
    napi_call_function(env, result, testFn, 0, nullptr, nullptr);

    napi_value value;
    napi_value key;
    std::string keyStr = "value";
    napi_create_string_utf8(env, keyStr.c_str(), keyStr.size(), &key);
    // 4. Call napi_get_property to obtain a variable value.
    napi_get_property(env, result, key, &value);
    return result;
}
```

- **Loading a HAR module to a HAP**

The **Index.ets** file in the HAR package is as follows:

```javascript
//library Index.ets
let value = 123;
function test() {
  console.log("Hello OpenHarmony");
}
export {value, test};
```

1. Configure dependencies in the **oh-package.json5** file.

```json
{
    "dependencies": {
        "library": "file:../library"
    }
}
```

2. Configure the source package in **build-profile.json5**.

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

3. Use **napi_load_module_with_info** to load **library**, call the **test** function, and obtain the variable values.

```cpp
static napi_value loadModule(napi_env env, napi_callback_info info) {
    napi_value result;
    // 1. Call napi_load_module_with_info to load library.
    napi_status status = napi_load_module_with_info(env, "library", "com.example.application/entry", &result);

    napi_value testFn;
    // 2. Call napi_get_named_property to obtain the test function.
    napi_get_named_property(env, result, "test", &testFn);
    // 3. Call napi_call_function to call the test function.
    napi_call_function(env, result, testFn, 0, nullptr, nullptr);

    napi_value value;
    napi_value key;
    std::string keyStr = "value";
    napi_create_string_utf8(env, keyStr.c_str(), keyStr.size(), &key);
    // 4. Call napi_get_property to obtain a variable value.
    napi_get_property(env, result, key, &value);
    return result;
}
```

- **Loading a remote HAR module to a HAP**

1. Configure dependencies in the **oh-package.json5** file.

```json
{
    "dependencies": {
        "@ohos/hypium": "1.0.16"
    }
}
```

2. Configure the source package in **build-profile.json5**.

```json
{
    "buildOption" : {
        "arkOptions" : {
            "runtimeOnly" : {
                "packages": [
                    "@ohos/hypium"
                ]
            }
        }
    }
}
```

3. Use **napi_load_module_with_info** to load **@ohos/hypium** and obtain the default variable.

```cpp
static napi_value loadModule(napi_env env, napi_callback_info info) {
    napi_value result;
    // 1. Call napi_load_module_with_info to load @ohos/hypium.
    napi_status status = napi_load_module_with_info(env, "@ohos/hypium", "com.example.application/entry", &result);

    napi_value key;
    std::string keyStr = "DEFAULT";
    napi_create_string_utf8(env, keyStr.c_str(), keyStr.size(), &key);
    // 2. Call napi_get_property to obtain the default variable.
    napi_value defaultValue;
    napi_get_property(env, result, key, &defaultValue);
    return result;
}
```

- **Loading an ohpm package to a HAP**

1. Configure dependencies in the **oh-package.json5** file.

```json
{
    "dependencies": {
        "json5": "^2.2.3"
    }
}
```

2. Configure the source package in **build-profile.json5**.

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

3. Use **napi_load_module_with_info** to load **json5** and call the **stringify** function.

```cpp
static napi_value loadModule(napi_env env, napi_callback_info info) {
    napi_value result;
    // 1. Call napi_load_module_with_info to load json5.
    napi_status status = napi_load_module_with_info(env, "json5", "com.example.application/entry", &result);

    napi_value key;
    std::string keyStr = "default";
    napi_create_string_utf8(env, keyStr.c_str(), keyStr.size(), &key);
    // 2. Call napi_get_property to obtain the default object.
    napi_value defaultValue;
    napi_get_property(env, result, key, &defaultValue);

    napi_value stringifyFn;
    // 3. Call napi_get_named_property to obtain the stringify function.
    napi_get_named_property(env, defaultValue, "stringify", &stringifyFn);
    // 4. Use napi_call_function to call the stringify function.
    napi_value argStr;
    std::string text = "call json5 stringify";
    napi_create_string_utf8(env, text.c_str(), text.size(), &argStr);
    napi_value args[1] = {argStr};

    napi_value returnValue;
    napi_call_function(env, defaultValue, stringifyFn, 1, args, &returnValue);
    return result;
}
```

- **Loading an API module to a HAP**

```cpp
static napi_value loadModule(napi_env env, napi_callback_info info) {
    // 1. Call napi_load_module_with_info to load the module @ohos.hilog.
    napi_value result;
    napi_status status = napi_load_module_with_info(env, "@ohos.hilog", nullptr, &result);
    
    // 2. Call napi_get_named_property to obtain the info function.
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
    // 3. Use napi_call_function to call the info function.
    napi_call_function(env, result, infoFn, 3, args, nullptr);
    return result;
}
```

- **Loading a native library to a HAP**

The **index.d.ts** file of **libentry.so** is as follows:

```javascript
//index.d.ts
export const add: (a: number, b: number) => number;
```

1. Configure dependencies in the **oh-package.json5** file.

```json
{
    "dependencies": {
        "libentry.so": "file../src/main/cpp/types/libentry"
    }
}
```

2. Configure the source package in **build-profile.json5**.

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

3. Use **napi_load_module_with_info** to load **libentry.so** and call the **add** function.

```cpp
static napi_value loadModule(napi_env env, napi_callback_info info) {
    napi_value result;
    // 1. Call napi_load_module_with_info to load libentry.so.
    napi_status status = napi_load_module_with_info(env, "libentry.so", "com.example.application/entry", &result);

    napi_value addFn;
    // 2. Call napi_get_named_property to obtain the add function.
    napi_get_named_property(env, result, "add", &addFn);
    
    napi_value a;
    napi_value b;
    napi_create_int32(env, 2, &a);
    napi_create_int32(env, 3, &b);
    napi_value args[2] = {a, b};
    // 3. Use napi_call_function to call the add function.
    napi_value returnValue;
    napi_call_function(env, result, addFn, 2, args, &returnValue);
    return result;
}
```
