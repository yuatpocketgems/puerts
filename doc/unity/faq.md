# 常见问题

- [常见问题](#常见问题)
  - [invalid arguments to XYZ](#invalid-arguments-to-xyz)
  - [setInterval没回调](#setinterval没回调)
  - [如何调试](#如何调试)
  - [can not find delegate bridge for XXX](#can-not-find-delegate-bridge-for-xxx)
  - [maOS10.15以上,启动unity的时候提示"puerts.bundle损坏,移动到废纸篓"](#maos1015以上启动unity的时候提示puertsbundle损坏移动到废纸篓)
- [FAQ](#faq)
  - [Why is callback of setInterval never triggered?](#why-is-callback-of-setinterval-never-triggered)
  - [How to debug?](#how-to-debug)
  - [How to solve "puerts.bundle is broken, move to trash"?](#how-to-solve-puertsbundle-is-broken-move-to-trash)

## invalid arguments to XYZ
如果你用js，可能是输错参数了。
如果你用typescript，可能是子类同名，但不同参数的函数覆盖了父类。以`System.Text.Encoding.UTF8.GetBytes`为例，你直接调用会报错。

```csharp
System.Text.Encoding.UTF8.GetBytes("你好");
```

`System.Text.Encoding.UTF8`指向的对象`System.Text.UTF8Encoding`，有`GetBytes`的其它重载，按目前的实现找到当前类有同名函数就不再找基类导致的。这时候你可以手动指定下用其基类接口访问该对象。

```javascript
Object.setPrototypeOf(System.Text.Encoding.UTF8, System.Text.Encoding.prototype);//只需要调用过一次即可。后续调用GetBytes都不用再调用。
System.Text.Encoding.UTF8.GetBytes("你好");
```

## setInterval没回调

可能是没调用`JsEnv.Tick`。

## 如何调试

VSCode的调试教程[在这里](vscode_debug.md)。如需使用其它IDE，请参照相应IDE调试NodeJS的教程。

## can not find delegate bridge for XXX

你将一个js函数映射为一个delegate有时会报这错误，XXX就是要映射的delegate，可能的情况如下：

* 该delegate带了值类型参数或者返回值，解决办法：如果没有返回值，用JsEnv.UsingAction声明下，有返回值就用JsEnv.UsingFunc声明。

* 参数数量超过4个，解决办法：官方目前只支持4个，如果有需要，可以依葫芦画瓢写更多的参数支持。

* 参数含ref，out的修饰，目前尚未支持，解决办法：填写issues来提需求

## maOS10.15以上,启动unity的时候提示"puerts.bundle损坏,移动到废纸篓"

执行

```bash
sudo xattr -r -d com.apple.quarantine puerts.bundle
```

# FAQ
## Why is callback of setInterval never triggered?

Make sure to call `JsEnv.Tick()` periodically.

## How to debug?
Debug setup for VSCode is documented [here](vscode_debug.md). For other IDEs, setup the IDE for debugging NodeJS, and consult VSCode's documentation to setup Puerts.

## How to solve "puerts.bundle is broken, move to trash"?
This error occurs on MacOS 10.15+. Run `sudo xattr -r -d com.apple.quarantine puerts.bundle` to fix.
