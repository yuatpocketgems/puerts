![Logo](./pic/puerts_logo.png)

[![license](http://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/Tencent/puerts/blob/master/LICENSE)
[![release](https://img.shields.io/badge/release-v1.0.0-blue.svg)](https://github.com/Tencent/puerts/releases)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-blue.svg)](https://github.com/Tencent/puerts/pulls)
![CI](https://github.com/Tencent/puerts/workflows/CI/badge.svg)

## 概览 <!-- omit in toc -->
Puerts是游戏引擎下的TypeScript编程解决方案。
* 它为Unreal Engine以及Unity提供JavaScript运行时。
* 它提供通过TypeScript访问宿主引擎的能力（JavaScript层面的绑定以及TypeScript声明生成）

## Overview <!-- omit in toc -->
Puerts enables scripting using JavaScript and TypeScript in Unreal Engine and Unity.
* It supplies a JS runtime
* It exposes host methods to JS scripts.

- [优势](#优势)
- [Advantages](#advantages)
- [编程样例 Examples](#编程样例-examples)
  - [Unity](#unity)
  - [Unreal Engine](#unreal-engine)
- [安装](#安装)
- [Installation](#installation)
- [示例 Examples](#示例-examples)
- [详细信息](#详细信息)
- [Additional Info](#additional-info)
- [技术支持](#技术支持)

## 优势
* JavaScript生态有众多的库和工具链，结合专业商业引擎的渲染能力，快速打造游戏
* 相比游戏领域常用的lua脚本，TypeScript的静态类型检查有助于编写更健壮，可维护性更好的程序
* 支持多个引擎
  * Unreal Engine 4.22 以上版本
  * Unity 5 以上版本
* 支持多平台
  * iOS
  * Android
  * Windows
  * MacOS
* 支持任意.NET环境
* 全引擎，全平台支持反射Binding，无需额外（生成代码）步骤即可开发
* 全引擎，全平台支持静态Binding，兼顾了高性能的场景

## Advantages
* Brings an abundance of libraries and tools available in the JavaScript ecosystem to professional game engines.
* Unlike the popular Lua script, statically typed TypeScript assists developers to create robust and maintainable systems.
* Multi-engine support
  * Unreal Engine 4.22 +
  * Unity 5 +
* Multi-platform support
  * iOS
  * Android
  * Windows
  * MacOS
* Supports all .NET runtime
* Supports dynamic binding between JS and C# via reflection. Objects are exposed both ways.
* Supports static binding for improved performance.

## 编程样例 Examples
### Unity
    ```typescript
    import {UnityEngine} from 'csharp'

    UnityEngine.Debug.Log('hello world');
    let gameObject = new UnityEngine.GameObject("testobject");
    console.log(gameObject.name);
    gameObject.transform.position = new UnityEngine.Vector3(1, 2, 3);
    ```

### Unreal Engine
    ```typescript
    import * as UE from 'ue'
    import {argv} from 'puerts';
    let world = argv.getByName("World") as UE.World;
    let actor = world.SpawnActor(UE.MainActor.StaticClass(),
        undefined, UE.ESpawnActorCollisionHandlingMethod.Undefined, undefined, undefined) as UE.MainActor;
    console.log(actor.GetName());
    console.log(actor.K2_GetActorLocation().ToString());
    ```

## 安装
1. 运行`git clone https://github.com/Tencent/puerts.git`
1. 拷贝插件到您项目
    - Unreal Engine
        + 拷贝`puerts/unreal`下的Puerts目录到您项目的`Plugins`目录下，可以参考[unreal demo](https://github.com/chexiongsheng/puerts_unreal_demo)
    
    - Unity
        + 拷贝puerts/unity/Assets下的所有内容到您项目的`Assets`目录下，可以参考[unity demo](https://github.com/chexiongsheng/puerts_unity_demo)
        + 提示：Plugins需要从[releases](https://github.com/Tencent/puerts/releases)单独下载，或者自行编译

## Installation
1. Run `git clone https://github.com/Tencent/puerts.git`
1. Copy Puerts into your project
   - Unreal Engine
     - Copy the folder `puerts/unreal/Puerts` to Plugins. See [unreal demo](https://github.com/chexiongsheng/puerts_unreal_demo) for example.
   - Unity
     - Copy everything under `puerts/unity/Assets` to `Assets`. See [unity demo](https://github.com/chexiongsheng/puerts_unity_demo) for example.
     - NOTE: Contents for `Plugins` are available from [releases](https://github.com/Tencent/puerts/releases). Or you may compile it yourself.

## 示例 Examples
* [Unreal Engine demo](https://github.com/chexiongsheng/puerts_unreal_demo)
* [Unity demo](https://github.com/chexiongsheng/puerts_unity_demo)

## 详细信息
本项目有针对各个平台更细节的信息。例如：
- 调试
- 常见问题
  
[Unreal Engine详情](doc/unreal)
[Unity详情](doc/unreal)

## Additional Info
There are engine specific details that are documented in their corresponding directory. These details include:
- Debugging
- FAQ

[Unreal Engine details](doc/unreal)
[Unity details](doc/unreal)

## 技术支持
QQ群：942696334
UE4专属群：689643903
