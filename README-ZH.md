# RocketXPlugin
![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![java](https://img.shields.io/badge/language-kotlin-Borange.svg)

[English Document](https://github.com/trycatchx/RocketXPlugin/blob/master/README.md)

## 描述
本插件 hook 编译流程，将所有的模块依赖修改为 aar，然后每次编译将变动的模块改成源码依赖，同时编译完成再将修改模块上传为 aar，这样可以始终做到仅有最少的模块参与源码编译，从而提升 Android 编译速度

## 编译速度对比
![编译速度对比.png](https://upload-images.jianshu.io/upload_images/2788235-ee2c3f7b9ca7862f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## AGP 版本兼容
Plugin version | Gradle version
---|---
4.0.0+ | 6.1.1+
4.1.0+ | 6.5+
4.2.0+ |6.7.1+
7.0    |7.0+

## 如何使用

#### 方式一：网络依赖

* 依赖 gradle 插件

```
buildscript {
    dependencies {
        classpath 'io.github.trycatchx:rocketx:1.0.5'
    }
}
```

* 依赖 AS 插件 android studio setting->plugins-> marketplace 搜索 RocketX 安装（搜索不到使用本地安装）

#### 方式二：本地依赖(实时使用最新的版本，网络依赖需要上传 maven 有所滞后)

下载项目中的 lib 文件夹两个 jar：

* rocketX-studio-plugin.jar 通过 android studio setting->plugins->install plugin from disk 进行安装
* rocketx.jar 通过在项目工程根目录新建文件夹Plugin，置放进去 Plugin文件夹，在根目录的build.gradle 写入 classpath fileTree(dir: './Plugin', include: ['*.jar'])

######  使用点击小火箭至喷火icon （enable 状态），选择 Assemble${flavor}${buildType} task , 点击编译器原有的 run 按钮进行编译(指定 task 好处是项目中存在多个 apply plugin: 'com.android.application'  ，也只会编译当前指定的 application module ) :
![assembleDebug](https://github.com/trycatchx/RocketXPlugin/blob/master/IMG/assembleDebug.jpeg)



## 问题
* 第一次的加速，是最慢的因为需要全量编译后，打出 aar 上传到 LocalMaven
* 如果使用了 arouter ，请使用 zPlugin 文件夹中的 本地 arouter 进行替换（查看demo 如何替换），速度更快（后期研究是否有更好的办法解决这个问题）
* 目前如果编译出错，请重新再 run 一次，出现的问题 欢迎提 issue


[Blog讲解](https://www.jianshu.com/p/59b95b5a7fab)


## 开发维护者
 名单 | 留言
--- | ---
[JustAClamber](https://github.com/JustAClamber) | 知者不惑
[louis](https://github.com/louis-lzt)| louis-lzt
[TryCatch ](https://github.com/trycatchx)   |日落西来，月向东
[FamilyCYZ](https://github.com/FamilyCYZ) | 什么也没有留下


## License

```
Copyright (C) 2021 tcler@tcl.com

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.