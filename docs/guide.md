# 快速入门-准备工作

首先你应该有一个基于React Native开发的应用，我们把具有package.json的目录叫做你的"应用根目录"。

如果你还没有初始化应用，请参阅[开始使用React Native](http://reactnative.cn/docs/0.22/getting-started.html#content)。

所以我们也假设你已经拥有了开发React Native应用的一切环境，包括`Node.js`、`npm`、`XCode`、`Android SDK`等等。

如果你之前没安装过，你还必须安装[Android NDK](http://androiddevtools.cn)，并设置环境变量`ANDROID_NDK`，指向你的NDK根目录(例如`/Users/tdzl2003/Downloads/android-ndk-r10e`)。

## 安装

在你的项目根目录下运行以下命令(不要输入开头的美元符号)：

```bash
$ npm install -g react-native-update-cli rnpm
$ npm install --save react-native-update
$ rnpm link react-native-update
```

> 其中第一句，在每一台电脑上仅需运行一次。

## 配置Bundle URL(iOS)

// 文档建设中 

## 配置Bundle URL(Android)

在你的ReactActivity中增加如下代码：

```java
// ... 其它代码

import cn.reactnative.modules.update.UpdateContext;
import cn.reactnative.modules.update.UpdatePackage;

public class MainActivity extends ReactActivity {

    @Override
    protected String getJSBundleFile() {
        return UpdateContext.getBundleUrl(this);
    }
    // ... 其它代码
}
```

## 登录与创建应用

在你的项目根目录下运行以下命令：

```bash
$ pushy login
email: <输入你的注册邮箱>
password: <输入你的密码>
```

这会在项目文件夹下创建一个`.update`文件，注意不要把这个文件上传到Git等CVS系统上。你可以在`.gitignore`末尾增加一行`.update`来忽略这个文件。

登录之后可以创建应用。注意iOS平台和安卓平台需要分别创建：

```bash
$ pushy createApp --platform ios
App Name: <输入应用名字>
$ pushy createApp --platform android
App Name: <输入应用名字>
```

> 两次输入的名字可以相同，这没有关系。

如果你已经在网页端或者其它地方创建过应用，也可以直接选择应用：

```bash
$ pushy selectApp --platform ios
1) 鱼多多(ios)
3) 招财旺(ios)

Total 2 ios apps
Enter appId: <输入应用前面的编号> 
```

选择或者创建过应用后，你将可以在文件夹下看到`update.json`文件，其内容类似如下形式：

```bash
{
    "ios": {
        "appId": 1,
        "appKey": "<一串随机字符串>"
    },
    "android": {
        "appId": 2,
        "appKey": "<一串随机字符串>"
    }
}
```

你可以安全的把`update.json`上传到Git等CVS系统上，与你的团队共享这个文件，它不包含任何敏感信息。当然，他们在使用任何功能之前，都必须先进行

至此应用的创建/选择就已经成功了。下一步，你需要给代码添加相应的功能，请参阅[添加热更新功能](guide2.md)