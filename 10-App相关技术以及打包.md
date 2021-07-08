## 1.开发App的相关技术使用

目前市面上的移动互联开发技术主要分为三种，NativeAPP（基于本地操作系统运行）、Web APP（基于手机浏览器运行）与HybridApp（混合模式移动应用）。

### 1.1.原生开发

​	原生开发目前的主流技术包含iOS与Android开发，使用的是Apple与Google自家的开发语言。

​	[Apple开发者网站](https://developer.apple.com)

​	[Android开发者网站](https://developer.android.google.cn)

#### 	原生App开发特点：

​        - 每一种移动操作系统都需要独立的开发项目

​		- 每种平台都需要独立的开发语言。iOS(Objective-C, swift)，Android(Kotlin，Java)

​		- 需要使用各自的软件开发包，开发工具以及各自的控件;iOS(Xcode)，Android(Android Studio)

​		- iOS开发对系统依赖性较强，只能在MacOS与iPadOS(21年九月后)系统下进行编程上架

#### 	能力方面：

​		- 能够与移动硬件设备的底层功能，比如个人信息，摄像头以及重力加速器等等

#### 	获取方法

​		-  直接下载到设备

​		- 以独立的应用程序运行(并不需要浏览器)

​		- 用户必须手动去下载并安装这些原生App

​		- 有一些商店与卖场来帮助用户寻找你的App，目前app市场不计其数

#### 	版本控制

​		- 用户可以自由地选择是否更新软件版本，所以会出现不同用户同时使用不同版本的情况

#### 	优势

​		- 比移动WebApp运行快

​		- 一些商店与卖场会帮助用户寻找原生App

​		- 官方卖场的应用审核流程会保证让用户得到高质量以及安全的App

​		- 官方会发布很多开发工具或者人工支持来帮助你的开发

#### 	劣势

​		- 开发成本高，尤其是当需要多种移动设备来测试时

​		- 因为是不同的开发语言，所以开发，维护成本也高

​		- 因为用户使用的App版本不同，所以你维护起来很困难

​		- 官方卖场审核流程复杂且慢，会严重影响你的发布进程

### 1.2.Web App开发

​	使用前端技术进行App的开发，主要技术有H5，Vue等，相当于讲前端技术放在原生的webView中去执行

#### 	Web App开发特点

​		- 因为运行在移动设备的浏览器上，所以只需要一个开发项目

​		- 这种应用可以使用HTML5,CSS3以及JavaScript以及服务器端语言来完成（Java,Python,PHP等）

​		- 这里没有标准的SDK，可以选择跨平台开发工具进行打包发布，比如PhoneGap, Cordova等

#### 	能力方面

​		- 只能使用有限的移动硬件设备功能。

#### 	获取方法

​		- 从移动设备上的浏览器访问

​		- 不需要安装额外的软件

​		- 软件更新只需要服务器就够了

​		- 可以使用打包工具进行App打包，发布到iOS与Android软件市场

#### 	版本控制

​		- 所有的用户都是用同样的版本

#### 	优势

​		- HTML5具有很强的兼容性，原来必须要用原生技术去做的效果或者功能现在基本都可以通过简单的		  		  HTML5开发技术实现

​		- 跨平台开发

​		- 使用现有组件库或框架进行快速开发

​		- 开发成本低，掌握前端技术便可很快上手

​		- 如果你已经有了一个WebApp，你可以使用 responsive web design来辅助改进

​		- 迭代更容易

#### 	劣势

​		- 无法使用很多移动硬件设备的独特功能

​		- 要同时支持多种移动设备的浏览器让开发维护的成本也不低

​		- 如果用户使用更多的新型浏览器，那问题就更不好处理了

### 1.3.混合式开发

​	是指介于web-app、native-app这两者之间的app，兼具“Native App良好用户交互体验的优势”和“Web App跨平台开发的优势”。

#### 	混合式开发主流技术

##### 		React Native(facebook开源的基于reactJs的RN)

##### 		优点：

​			- 能够在Javascript和React的基础上获得完全一致的开发体验，构建世界一流的原生APP。

​			- 仅需学习一次，编写任何平台。(Learn once, write anywhere)

##### 		缺点：

​			- 初次学习成本高

​			- 必须在不同平台下写两套代码，依赖暴露的接口



#### 	谷歌 Flutter(Flutter是谷歌的移动UI框架, [Dart](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.dartlang.org%2F) 语言)

​		Flutter是谷歌的移动UI框架，可以快速在iOS和Android上构建高质量的原生用户界面。 Flutter可以与现		有的代码一起工作。

##### 		优点：

​			- 快速开发，Flutter的热重载可帮助您快速地进行测试、构建UI、添加功能并更快地修复错误。在iOS			和Android模拟器或真机上可以在亚秒内重载，并且不会丢失状态

​			- UI界面比较漂亮，使用Flutter内置美丽的Material Design和Cupertino（iOS风格）widget、丰富的			motion API、平滑而自然的滑动效果和平台感知，为您的用户带来全新体验。

​			- 不会原生可以直接开发

​			- 原生性能比较好

#### 		缺点：

​			- 目前仍然处于技术更新完善阶段

​			- 脱离不开原生，开发人员需要具备原生（Android、iOS）基础开发能力

​			- 适配问题，开发工具版本升级后，修改量大

#### 	阿里weex(阿里巴巴开源的基于Vue.js)

​		Weex是2016年6月由阿里巴巴推出的一个动态化的高扩展跨平台解决方案，支持iOS、安卓、YunOS及		Web等多端开发部署。

#### 		优点：

​			- Weex 的结构是解耦的，渲染引擎与语法层是分开的，也不依赖任何特定的前端框架

​			- 目前主要支持 [Vue.js](https://links.jianshu.com/go?to=https%3A%2F%2Fvuejs.org%2F) 和 [Rax](https://links.jianshu.com/go?to=https%3A%2F%2Falibaba.github.io%2Frax%2F) 这两个前端框架。

​			- 渲染 Weex 页面时和渲染原生页面一样。

​			- 一套基础的内置组件

​			- 不需要安装复杂的环境，运行环境简洁、调试工具也还好，容易做降级处理，特别适合开发单个页面

#### 		缺点：

​			- 文档更新不及时，资料不多

​			- 坑比较多，前端

## 2.使用HBuilderX打包Web App

​	下载HBuilderX工具，打包Web App https://www.dcloud.io/

#### 打包步骤

1.在项目根目录下新建vue.config.js文件，写入如下配置

![Snip20210703_48](/Users/Zach/Desktop/Snip20210703_48.png)

```js
module.exports = {
  publicPath: './',
  outputDir: 'dist',
  assetsDir: 'static'
}
```

2.在src/router/index.js下，将路由history模式注释掉

![image-20210703213210296](/Users/Zach/Library/Application Support/typora-user-images/image-20210703213210296.png)

3.在项目路径下执行命令npm run build，生成dist打包文件

![image-20210703213334422](/Users/Zach/Library/Application Support/typora-user-images/image-20210703213334422.png)

4.打开HBuilder，新建项目，选择H5+App，输入项目名称，选择项目路径，点击创建

![image-20210703213535591](/Users/Zach/Library/Application Support/typora-user-images/image-20210703213535591.png)

![image-20210703213652544](/Users/Zach/Library/Application Support/typora-user-images/image-20210703213652544.png)

5.了解目录结构

![image-20210703214524872](/Users/Zach/Library/Application Support/typora-user-images/image-20210703214524872.png)

6.找打打包生成的dist文件，放入到项目中，替换已经存在的index.html文件

![image-20210703214708567](/Users/Zach/Library/Application Support/typora-user-images/image-20210703214708567.png)

![image-20210703214809316](/Users/Zach/Library/Application Support/typora-user-images/image-20210703214809316.png)

![image-20210703214826666](/Users/Zach/Library/Application Support/typora-user-images/image-20210703214826666.png)

![image-20210703214904723](/Users/Zach/Library/Application Support/typora-user-images/image-20210703214904723.png)

7.基础配置

![image-20210703215937089](/Users/Zach/Library/Application Support/typora-user-images/image-20210703215937089.png)

8.图标配置

![image-20210703220939971](/Users/Zach/Library/Application Support/typora-user-images/image-20210703220939971.png)

9.如需配置App启动图片，可以自行配置

![image-20210703221134027](/Users/Zach/Library/Application Support/typora-user-images/image-20210703221134027.png)

10.配置SDK

![image-20210703235812896](/Users/Zach/Library/Application Support/typora-user-images/image-20210703235812896.png)

11.根据自己的需求，进行权限配置使用

![image-20210703221450474](/Users/Zach/Library/Application Support/typora-user-images/image-20210703221450474.png)

12.App常用其他设置

![image-20210703221637657](/Users/Zach/Library/Application Support/typora-user-images/image-20210703221637657.png)

13.源码视图

![image-20210703222054332](/Users/Zach/Library/Application Support/typora-user-images/image-20210703222054332.png)

```json
"statusbar":{ // 应用可视区域到系统状态栏下透明显示效果
  "immersed": true
}
```

14.原生App-云打包

![image-20210703222348019](/Users/Zach/Library/Application Support/typora-user-images/image-20210703222348019.png)

![image-20210703222545619](/Users/Zach/Library/Application Support/typora-user-images/image-20210703222545619.png)

![image-20210703222712169](/Users/Zach/Library/Application Support/typora-user-images/image-20210703222712169.png)

![image-20210703223922438](/Users/Zach/Library/Application Support/typora-user-images/image-20210703223922438.png)

进入网站填写手机号验证

![image-20210703225905182](/Users/Zach/Library/Application Support/typora-user-images/image-20210703225905182.png)

15.打包成功后，找到对应apk使用即可

![image-20210703230256646](/Users/Zach/Library/Application Support/typora-user-images/image-20210703230256646.png)