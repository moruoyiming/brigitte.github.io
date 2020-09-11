---
title: Android 项目中so文件丢失
thumbnail: /gallery/thumbnails/plant.jpg
categories: 
- Android基础
tags:
- Android
- so文件
- ndk
---
项目运行时提示缺少so文件，需要在App项目中build.gradle增加支持的so 文件类型.在defaultConfig下增加下方代码
```
  ndk {
            abiFilters "armeabi",'x86', 'armeabi-v7a', 'armeabi-v8a', 'arm64-v8a'
        }
```

<!-- more -->
完整代码

```
 defaultConfig {
        applicationId "..."
        minSdkVersion versions.minSdk
        targetSdkVersion versions.targetSdk
        versionCode versions.appVerCode
        versionName versions.appVerName
        multiDexEnabled true 

        ndk {
            abiFilters "armeabi",'x86', 'armeabi-v7a', 'armeabi-v8a', 'arm64-v8a'
        }
        javaCompileOptions {
            annotationProcessorOptions {
                arguments = [AROUTER_MODULE_NAME: project.getName()]
            }
        }
    }
```
从新编译应用，并在build/outputs/apk下查看编译成功的apk 文件中的libs 已经将so文件成功编译进去。
