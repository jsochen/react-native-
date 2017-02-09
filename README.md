
#ReactNative历代版本变化,本文档为0.15～0.27版本的新特性与增强，bug修复，不兼容的修改
## 0.27 正式版发布
### 不兼容的修改

* 移除 NavigationLegacyNavigator (ef44781) - @hedgerwang

    - NavigationLegacyNavigator 原来是用于帮助人们在不改动API的情况下迁移到新的导航库。这会使得我们不得不把那些不必要的旧API也全部迁移到新的导航库中。

    - 考虑到在产品中使用NavigationLegacyNavigator是不应该的，所以我们决定移除掉它，并会在将来把原来的Navigator改名为NavigatorDeprecated。

* 移除 NavigationExperimental Containers (14eb427) - @ericvicenti

  - NavigationExperimental中的容器并不建议使用，因为应用的状态应当被应用的架构所管理，譬如使用redux、flux或者组件状态。
  这个提交把样例修改为使用组件状态来保存的，不过也有其他很多例子用来展示如何使用NavigationAnimatedView和redux的导航器reducer。:
  https://github.com/jlyman/RN-NavigationExperimental-Redux-Example
  Switching the f8 app with redux to navigation experimental: fbsamples/f8app#14

* 移除 NavigationView (c3714d7) - @hedgerwang
  - 使用<NavigationView /> 没有明显的作用，并且维护起来非常麻烦。它的功能完全可以通过创建一个关闭了切换动画的NavigationAnimatedView来实现。它还可以被一个单纯的View和一个普通的场景渲染器来替代。

### 新特性与增强

* **Animated**: 实现了Animated的toJSON方法 (17f0807) - @wusuopu

修复BUG：使用“检查元素”功能查看动画组件时会产生报错。

* 让 RefreshControl 正确的被JS控制(9aa37e8) - @janicduplessis

修复BUG：在controlled component来控制RefreshControl时，状态显示错误

* 增加SwipeableListView (052cd7e 9b1a3c7 2a7f6ae) - @fred2028

看起来像是一个每一个项目都可以被左滑以展示功能菜单的View

* 为NavigationAnimatedView的场景渲染器增加transition属性。 (55c3086<) - @hedgerwang

为新导航器增加transition属性

* 让BugReporting支持自定义的源文件 (610cfdc) - @lexs

* 给元素检查器增加"Open file"（打开文件）按钮 (f203c5d) - @frantic

使你可以直接在元素检查器中点击元素，在电脑上直接查看对应的文件

* 给react-native的babel预配置集合增加插件 transform-react-jsx-source (858643d) - @frantic

这个插件往JSX里增加了标记信息，用于识别元素所对应的源代码位置。

* 分支 NavigationAnimatedView为 NavigationTransitioner (<tt>7db7f78</tt>) - @hedgerwang

这个新组件和原来的NavigationAnimatedView类似，稍后会废弃屌原来的NavigationAnimatedView。

不同之处：移除了属性applyAnimation，添加了新属性configureTransition, onTransitionStart和 onTransitionEnd。

* 将rnpm合并到react-native包中 (149d0b9) - @grabbou
这在将来可以用于解决各种rnpm与react-native的版本不兼容问题。

### BUG修复

1. 在初始化react实例的时候阻塞对JS模块的调用(a1ba091) - @astreet

*  修复NavigationCard的属性类型检查。 (b1cd1cb) - @hedgerwang

*  修复RefreshControl的访问冲突(fbce30) - @janicduplessis

*  NavigationExperimental: didFocus 事件应当在动画结束之后再调用。 (8975bb8) - @hedgerwang

*  修复当初次渲染RefreshControl就要求刷新的时候并没有开始刷新的问题。(cac5ce3) - @aforty

*  修复NavigationPropTypes.SceneRenderer是一个普通对象的问题(0e997c6) - @joenoon

现在拆分了SceneRenderer和SceneRendererProps，解决了类型检查时候导致的问题。

*  解决 SwipeableRow 的显示问题 (5146775) - @fred2028

默认的icon size会导致拉出的图片溢出到SwipeableRow之上。现在所有的样式都必须由调用者传入，由调用者自行控制相关的尺寸来达到最佳适应。

*  解决了95%的WindowedListView乱跳的问题 (5e91a2a) - @sahrens

*  解决了SwipeableRow在Android下闪烁和在iOS下晃动的问题(62e588b) - @fred2028

*  解决ListView的onChangeVisibleRows所汇报的行数不正确的问题(0aea74e) - @dmueller39

## 安卓

### 新特性与增强

*  为HorizontalScrollView增加pagingEnabled属性 (a3146e4) - @dmmiller

*  开源的SwipeRefreshLayoutRecordingModule (457e348) - @bestander

*  实现了TextInput的returnKeyType/returnKeyLabel (dd8caf4) - @Bhullnatik

*  为RefreshControl增加了 progressViewOffset属性 (<tt>f7ce0c1</tt>) - @UnoDeTantos

*  现在可以通过属性来禁用/锁定Android下ViewPager的滑动 (<tt>31250ad</tt>) - @kevinejohn

*  解决当React Context还未初始化完毕时点击RootView时的访问冲突问题。(fd37666) - Olivier Notteghem

*  为ScrollView增加FpsListener (b67d4a2) - Nathan Spaun

*  现在还没有实际作用不过将来这个将被用于记录和跟踪滚动条的滚动性能。

*  升级到OkHttp3 (6bbaff2) - @AndrewJack

*  解决 NetworkingModule 构造时添加拦截器(interceptors)时出现的问题 (921d0de) - @bestander

*  当忘记执行react-native start的时候，提示更友好的信息(c634ea](https://github.com/facebook/react-native/commit/bc634ea35044c84295904a6bb5f04e2d52ba688e)) - @codeheroics

### BUG修复

* 修复通过Controlled模式使用Android Picker时的问题 (0cd2904>) - @spicyj

* 使得Modal弹框时的状态栏保持沉浸式 (191d278) - @jemise111

* 为较老的Android设备增加React队列所允许的栈大小 (d4f6f61) - @nikki93

* 在发送触摸时间时携带时间戳信息，以使得反馈更为准确 (f2c1868) - @dmmiller

### iOS

### 新特性与增强

* NavigatorIOS: 导出了interactivePopGestureEnabled属性 (4d2c72b) - @rigdern

该属性可以禁用左滑返回上一页。

* 使得root view 的背景颜色更为明确(fa5d1fe) - @shaneosullivan

* 在IOSImagePicker的回调返回图片的宽高 (df40f48) - @thans

* 使得<Text>标签内可以内嵌View (fe5c0d2) - @rigdern

* 为红屏增加“复制栈”的功能 (5047f6f) - Chris Evans

### BUG修复

* 修复了LocationObserver的distanceFilter缓存问题(2310494) - @jrichardlai

* ScrollView: 触发onScroll事件时现在总是会发送最终的滚动位置(deef8aa) - @rigdern

* 当设置了scrollEventThrottle时，以前的版本并不保证最终的位置能被发送。

* 修复了在Image loader的数组中包含nil会导致崩溃的问题 (ed1ee9b) - @nicklockwood

* 隐藏软键盘时使用了正确的动画函数(03edc75) - @rigdern

* 修复 NativeEventListener注销的问题 (516bf7b) - @nicklockwood



## 0.26 正式版发布
### 新功能

1. 升级至react15.0.2
1. 支持在WebSockets中发送和接收二进制数据
1. 在CLI中添加--version
1. 在react-native bundle 中添加--reset-cache 重置文件缓存
1. 为js文件添加encode格式/哈希签名
1. Bug修复

1. 修复潜在的“Should never unset includeInLayout”不变
1. 修正初始场景渲染NavigationExperimental
1. 修正了modalbox不正确的布局
1. 修复ART模式中画边距bug
1. 使用相对路径时，修复获取文件错误bug
1. 本地修复流程定义
1. 去掉尺寸固定视图导出的常数
1. 修复package.json脚本里使用的react native CLI
1. 修正WebSocket兼容性
1. 修复JSWatchdog复位
1. 修复Animated的setValue在native正常工作
1. 固定路径再生运行时
1. 修复HMR预设
### ANDROID版

### 新功能

1. 添加ViewPager禁用滚动的能力
1. 添加揭露从Java同步JS的能力
1. 添加从文件系统加载Boost库的选项
1. 添加Animated.add支持原生动画
1. 添加支持setChildren
### Bug修复

1. 通过不再承担修复崩溃的AdsManager只有一个反应上下文存在一次
1. 修正使用弹出窗口引起的崩溃
1. 修复事件冒泡机制
1. 修复setFontWeight方法的NullPointerException
1. 修复mapView 的IndexOutOfBoundsException
1. 修复PullRefreshViewAndroid中未定义引用bug
1. 修复事件冒泡出来机制
1. 修复ReactNativeART绘弧图bug
1. 修复TextInput 的ClassCastException异常
1. 修复textShadowOffset没有宽度或高度错误
### IOS版

### 重大更改

1. 为所有签入的项目添加标志“-lc ++”
### 新功能

1. 添加在LayoutAnimation可以删除动画
1. 调度本地通知时支持添加图标数量和警报措施的支持
### Bug修复

1. 解决应用程序在启动过程中死锁
1. 修复RCTJavaScriptContextCreatedNotification
1. 修复CJK TextInput 自动完成模式
1. 修正了未设置文本大小造成RCTShadowText返回一个无限的高度bug
1. 修复ookieMap在RCTJSCExecutor导致内存泄漏bug
1. 修复与HTTP返回301时图像显示无响应
1. 修正了红盒子按一个堆栈帧无法打开，编辑



## 0.25 正式版发布
### 重大变更

在react-native中引用React的做法发生了变更（在当前版本老的做法会提出警告，如何屏蔽警告点这里。在下一版本将会报错）：

之前

import React, { Component, View } from 'react-native';

现在

import React, { Component } from 'react';
import { View } from 'react-native';
具体哪些属于React，哪些属于React Native，可以参考这篇[帖子](https://www.facebook.com/groups/reactnativeoss/permalink/1540818949548067/)（需要科学上网）。

我摘录如下：

"react":

- Children
- Component
- PropTypes
- createElement
- cloneElement
- isValidElement
- createClass
- createFactory
- createMixin

"react-native":

- hasReactNativeInitialized
- findNodeHandle
- render
- unmountComponentAtNode
- unmountComponentAtNodeAndRemoveContainer
- unstable_batchedUpdates
- View
- Text
- ListView
- ...
- 以及其他所有的原生组件。

### 新功能
1. 添加支持JavaScript的第三方调试器
2. 添加WindowedListView页脚包装
3. 添加了支持缺少XHR的响应-
4. 添加用于预读远程图像Image.prefetch的缓存
5. 添加ES2015函数到babel的变换 - 855c0cc
6. 添加重新加载非QWERTY键盘模拟器说明
7. 添加使用XMLHttpRequest Android和iOS时超时处理函数onTimeout
### 弃用
1. 弃用警告ReactNative.addons
2. 废弃区分web与移动程序的警告
### Bug修复
1. 添加刷新控制非空检查 - eac617d
2. 修复HMR在窗口不响应bug
3. 修复了PanResponder bug
4. 修复导航标题会阻止触摸左边控件bug
5. 修复本地图像从node_modules获取
6. 修正了热模块重载的边缘情况 - 41576ea
7. 修复UIExplorer示例页面的警告 - 528cf68
8. 修复PERF标签缺少key警告 - b7a3272
9. 修正了导航切换太快导致的手势丢失 - ca2fb70
10. 解决边界半径/背景的传播问题，例如井字游戏 - 97f60ad
11. 修正弹窗同时关闭/打开引发的冲突　 - 7354ff3
12. 修复ImageEditingManager没有外部缓存bug - fffcb9c
13. 修复RefreshControl刷新状态 - 93b39b7
### ANDROID版
### 新功能

1. 增加了在Android textDecorationLine风格支持
2. 增加了对Android上的图像的圆角半径的支持 - 69534a3
### Bug修复
1. 修复DrawerLayoutAndroid方法的参数 - d66b944
2. 修复DrawerLayoutAndroid无法设置不透明度 - 7851572
3. 修正了removeClippedSubviews和TextInput问题 - 89340f1
4. 添加支持的WebSocket协议 - 914f33c
5. 修复RUN_JS_BUNDLE记录系统路径的报告- 2d0051f
6. 修复promise参数必须在该方法最后一位bug - e27a27b
### IOS版
### 新功能
1. 新增的高速缓存中的ios端到端测试打包
### Bug修复
1. 修正了在iOS UIExplorer 图像示例 - a10c1b5
2. 添加缺少RCTConvert导入时的警告 - db25ab4
3. 修复ios手势交替导致不响应bug - 8efc098
4. 修复pod导入不正确库错误 - ef044e2
5. 从修复pull请求导致CSS布局的变化 - 7a1b072



## 0.24 正式版发布
### 重大更新
1. 安卓默认不再包含Stetho 3c488af
2. iOS移除RCTBridgeModuleClassIsRegistered a16771c
3. ScrollView移除内部使用的sendMomentumEvents属性。
4. StyleSheetRegistry更名为ReactNativePropRegistry，这个模块是私有的，因此它不应该影响那些使用RN的公共接口 433fb33
### 新特性
1. NavigationExperimental的增强 (by@hedgerwang:)
  - pagers的动画和手势 4f8668b
  - 在 NavigationCardStack和NavigationAnimatedView中使用相同的动画(spring库)07697d1
  - 减少NavigationHeader的额外渲染 62e80a6
2. 实验性的WindowedListView组件，对于屏幕外的列表项使用占位符渲染以提高性能，但它不是ListView的替代品 cd79e26
文档的一些改进

### Bug修复
1. 在分析工具里面使用monotonic clock替代现在的时间函数 ac03c47
2. 各种热模块的重载修复 98411f1，51b5423
3. 修复视图在列布局的时候不垂直拉伸 #2724，d957570
4. 在.flowconfig文件中使用semver，能让您在没有更新.flowconfig文件的情况下使用打补丁版本的Flow #6767
### ANDROID
### 新特性
1. 初步支持原生UI线程的代理动画命令，由@kmagiera设计和实现，由@brentvatne测试和重要的反馈，以及@astreet和@vjeux全面的代码审查。这个实现的还不完全，但是最终会让Navigation的动画从繁重的JS线程中解放出来 #6466
现在在Modal不使用onRequestClose属性将会提示警告 ce81f8b
2. 振动模式 e20e8a3
3. DrawerLayoutAndroid增加了一个新的属性 statusBackBackgroundColor，可以让DrawerLayoutAndroid覆盖在安卓原生的toolbar上。具体效果可以到PR#6218查看屏幕截图
4. ScrollView增加了一个新的属性endFillColor，当视图的大小比scrollView的content大的时候，可以设置一种颜色填充剩余的scrollView。这是一个高级的性能优化，您可以在使用之前先测试性能。4498bc8
5. TextInput现在支持selectTextOnFocus属性。 #6654
6. 在批处理结束之前创建视图以提高性能。 6a3b334
7. ReadableArray 和 ReadableHashMap 现在定义了 toArrayList 和 toHashMap 便利方法 #6639, ，#6762
8. 从BackAndroidhardwareBackPress返回true 停止调用之前注册的函数和系统默认的动作 67efe4c (恢复为 ede99ee)
### Bug修复
1. 修复嵌套滚动视图的矩形裁剪计算。 e8e3182
2. 不取消NativeRunnable构造函数使用ProGuard 393890e
3. 修复Genymotion中的获取source maps 6c22a21
4. 防止在嵌套TouchableNativeFeedback组件情况下，父视图的触发状态作用到子视图。 #6783
### IOS
### 新特性
1. 开源FBPortForwarding组件(一个类似于adb reverse，可以代理设备和你的电脑之间的网络请求)，RN没集成他，如果你有需要 FBPortForwarding : c4699d8
2. ActionSheetIOS增加一个新的message选项。#6685

### Bug修复
1. 为了遵循事件的先后顺序，特别是触摸和滚动事件，修复本地事件的合并将他们传给JS的时候。当所有的事件可以被合并的时候，他们将会尽快的处理，而不是等待下一个JS结构。一些不同来自于@majak: a496baa,a37075d,cefc5a6,7c2b397,b1b53aa,1d3db4c(恢复于144dc30 , 恢复和修复于02b6e38), 31bb85a
2. 为了线程安全，锁住对flow ID map访问：2be42ab
3. 在-[RCTJSExecutor invalidate]中停止JS run loop替代原来在dealloc中停止，可以保证它在JS线程中被停止。99c7de2
4. 阻止dev菜单当重置模拟器的方向。 6765
5. 增加dev工具的超时时间 b00c77a
6. 当需要跳到超过32MiB的profiling trampoline中的时候，使用间接跳转以支持更大的二进制文件。 2f27039
7. 让SliderIOS保留触摸响应状态。52ddfd9




## 0.23 正式版发布
### 高层变更
### 新特性
1. packager日志支持静默选项 - d5445d5
2. 当promise拒绝时可以通过console.error输出 - f87b673
3. 增加了更多的性能日志，增强了Systrace支持 - f6853b8
4. 使用NavigationExperimental初步重构 Navigator - fa5783e
5. 增加<Incremental>组件用于增量渲染 - f21da3a
### BUG修复

1. 更新node-haste，替换fast-path用来修复windows兼容问题 - fd816b1
2. 修正BUG#5604 - 未确认的可触碰信号将不在屏幕上显示 - d637621
3. 更新Layout.c修正弹性布局bug - 6c5195f
4. 在解析依赖之前进行代码转换 - 9d09efd
5. 通过 bezier-easing库重构bezier(更快更精确的实现) - b5985cf
6. 内联 __accept 调用以便source maps可以和HMR正常工作 - bcb37c0
### 安卓
### 新特性
1. Modal现在支持Android了
2. TextView增加之前缺失的textAlignVertical支持 - d20bde3
3. DrawerLayoutAndroid增加evevation支持 - 61483aa
4. 安卓增加JS压缩设置选项 - 1f94a00
5. run-android命令现在可以在所有连接的设备上运行app - 10ad47a
6. JS多上下文支持 - 872b697
7. JS perf API现在可以使用了 - 6e3710f
### BUG修复
1. 修正当置空安卓工具栏之后无法设置工具栏logo的bug - 8aa83a2
2. 增加安卓状态栏高度常量，改进了实现 - 18f38ec
3. 修正事件分发器时间戳排序的bug - f5a3490
4. 修正当负的width参数传递给RCTText的measure属性时崩溃的bug - c42fc61
5. 修正当状态栏半透明,键盘打开时，textinput没有正常滚动的bug - c76523f
6. 修正refactored bridge代码中Race条件的bug - 0cb7d16
### IOS
### 新特性
1. 增加预解析缓存和IOS8 JSC Stringref
2. Text组件增加lineBreakMode属性
3. RCTImageView增加失去焦点效果
### BUG修复
1. 修复固定头部点击处理的BUG - 688bb17
2. 更新AppState支持不活跃的状态 - ec9efb8




## 0.22 正式版发布
### 新特性
1. **React Native 0.22带来Hot Reloading（调试时不刷新热替换）特性！**
2. ListView支持自定义的ScrollView实现
3. UIExplorer中引入了NavigationExperimental(新的Navigation库可以使UIExplorer导航变的更灵活)
4. Touchable* 组件中增加了disabled属性
5. 增加了NavigationCardStack组件（可以使一列NavigationCard动起来的基本实现）
6. Animated组建增加了取余(%)运算符
7. 对packager增加消息通道，来向桥(2 / N)发送命令
8. 在packager中添加新的worker来进行代码转换，优化和依赖处理
9. NavigationCardStack中增加手势处理
10. 对传统导航器增加数据结构来处理栈
### Bug修复
1. 解决了当粘性的头部索引超出范围时，renderSeparator组件定义但返回null的问题
2. 修复了生产资源的变量名问题(图片资源应该被发布到其他文件夹，而不是js bundle文件夹)
3. 修复了当传递null到clearimmediate时的崩溃问题
4. 修复了DevTools的WebSocket的指数增长问题
### ANDROID
### 新特性
1. 增加了使用CSS技巧来创建三角形的功能
2. 增加了scalesPageToFit
3. 对Picker onValueChange的回调方法增加了position参数
4. 对run-android命令增加了root选项
5. 在event中，用nanoTime替代了currentTimeMillis
6. 给DrawerLayoutAndroid组件增加了drawerLockMode属性
7. WebWorkers: 在从workers调用或者被workers调用的本地原生路由中添加ExecutorToken
8. 给android的input text组件添加blurOnSubmit属性
9. 增加内存压力监听接口
10. 给react-native run-android命令添加选项，例如react-native run-android --option-flavor=staging
11. 增加ReactCompoundViewGroup接口来允许同时拥有虚拟和非虚拟(View)的子组件
### Bug修复
1. 修复了破碎的drawer layout组件
2. 废弃了PullToRefreshViewAndroid方法并把它从网站doc中移除了
3. 解决了当退出app时，隐身的StatusBar再次出现的问题
4. 修复了当使用透明度时的android的image组件的tintColor属性
5. 修复了Image.android.js的参数检查
6. 修复了bridge中的死锁
7. 修复了WebSocketModule的IllegalStateException崩溃
### IOS
### 新特性
1. 给本地通知的细节添加了category和alertAction属性
2. 给Picker onValueChange的调用增加了position的属性
3. 支持了通过ios的共享列表来分享图片和其他媒体
4. 增加了对屏幕、窗口或个人视图的快照支持
5. 增加Add UIManager.measureInWindow来得到窗口坐标
6. 给Linking.getInitialURL()增加了通用链接(universal links)
### Bug修复
1. 修复了带有粘性头部的ListView＋RefreshControl的问题
2. 修复RCTPerfMonitor的展示单元的问题
3. 修复了ios的WebView栗子
4. 修复了不透明缩略图会被给一个阿尔法通道的问题(使用ImageEditor剪裁图片时会给出一个阿尔法通道，即使它是不透明的)
5. 修复了RefreshControl总是旋转并且不刷新的问题
6. 修复了定位精度和缓存位置的问题 



##  0.21 正式版发布
### 安卓项目更新的重要说明：
我们简化了Android代码的发布——二进制文件现在也和JS以及Obj-C代码一样发布到npm仓库了。这意味着你必须运行react-native upgrade来更新安卓的编译文件（.gradle）。
### 新特性
1. 添加了一个新的实验性的导航组件NavigationExperimental
2. 开启Hot Module Replacement（模块实时刷新）
3. 网站文档现在可以切换版本
4. 用String.prototype.includes方法替代了String.prototype.contains
5. 改进了Chrome调试器的性能
6. 为Touchable系列组件添加了accessibility属性
7. 当Node版本小于4时，给出更明确的警告
8. 为地理定位API增加距离过滤选项
9. dataSource更新时不再自动渲染过多的行
10. 可以通过指定refresh=true来载入RefreshControl
11. 支持数字形式的颜色值
12. 调用immediatelyResetRouteStack时重渲染整个导航栏
13. 在NavigationExperimental中支持后退按钮
14. 使用onWillFocus和onDidFocus`时不再警告
15. 模块会根据transform的选项来决定是否缓存
16. 添加deprecatedCallback辅助函数
17. TouchableHighlight在没有绑定press事件时不再显示底层颜色
18. 在NetInfo中添加监听函数时，返回卸载函数
20. 添加Linux的新手指南
21. 在文档中使用ES6 import代替require
22. Packager: Remove unused support for asynchronous dependencies 7c03b16
23. Added two new apps to showcase (Choke and MyPED) 0f850b4 272096c
### Bug修复
1. 在React调试插件能正常工作前不再提示安装
2. 修复inspector显示的样式值
3. 修复multiGet的一个bug
4. 添加缺失的Chilren.toArray方法
5. 修复StyleInspector的key警告
### ANDROID
### 新特性
1. 添加Dimension.get('screen')
2. BackAndroid.addEventListener现在返回对应的卸载函数
3. 为AlertDialog添加.setItems()
4. 缓存图片资源id
5. 在getDisplayMetrics中使用新的DisplayMetrics对象
6. 在下载js bundle时提供更明确的错误信息
7. WebWorkers: Pass bridge to JS executors cf7a97c
8. 现在可以为单个角设定圆角
9. 迁移Android artifacts到npm
10. 添加Object.getPropertyNames() 和 Object.toJSONMap
11. 崩溃时正确格式化异常
12. 在发布版本时去除devsupport
13. 从文件读取脚本时，在sourceURL中添加'file://'前缀
### Bug修复
1. 修复ReactProp和ReactPropGroup的proguard模板
2. 修复滚动视图和RefreshControl的问题
3. Fix race in Catalyst tests 294185a
4. Snapshot BackAndroid event listeners while an event is dispatched 9040315
5. 修复icon处理逻辑
6. 修复"POST has no body"
### IOS
### 新特性
1. 在原生和js代码属性对不上时（一般因为更新引起），给出给明确的提示
2. 多行文本框现在支持textAlign
3. Expose flow events to JS + add JS -> Native flows c00049c
4. 现在可以监听和取消本地通知
5. 图片解码限制为2个线程
6. systrace中JS async始终设为top线程
### Bug修复
1. 添加ShadowPropTypesIOS文档
2. 修复XMLHttpRequest.abort()
3. Fix promises on iOS to no longer wrap values in Arrays c9a1956


## 0.20 正式版发布
**本版本有个bug导致无法正常运行，请参阅此贴修复 http://bbs.reactnative.cn/topic/208**
### 新特性
1. 为WebSocket添加了一个可选的option参数
2. 统一不同来源的图片的解码和缩放逻辑
3. 相册API现在使用promise
4. 剪切板(Clipboard)现在也使用promise，并对回调的用法提示警告
5. 编译js bundle时使用数字标识符来区分模块
6. 为packager添加ETag缓存处理
7. 文本输入框现在支持自动缩放
8. 开源Android版的日期与时间拾取器（Picker）
9. 添加跨平台的Linking模块
10. 添加跨平台的Picker模块
11. 重构颜色处理逻辑
12. 跨平台的状态栏API
13. 定制"babel-preset-reat-native"
14. packager现在支持非图片资源
15. 为Touchable系列组件添加accessibility属性
### Bug修复
1. 文本输入框在selectionState状态下也应调用blur和focus方法
2. 修复了默认的日志记录等级，以改进默认的错误处理
3. 修正了黄屏警告的计数错误
4. 修复了TouchNativeFeedback的一个问题，现在ripple效果可以正确从用户的触摸点开始
5. 使packager能够使用babel的严格模式转换
6. 为RCTUtils添加nullability标注
7. 正确绑定Touchable.js的setTimeout
8. 修复transform: {perspective: 0}引起的崩溃
9. 改进文档中样式属性的显示
10. breaking test and fix for browser field mapping from package to file - 191b692
11. 修复元素审查器生成的警告
12. 导航栏透明时禁用右侧按钮
13. 修复graceful-fs的bug
14. 现在可以为ColorPropTypes指定更精确的限制描述以及isRequired
15. 修复浅依赖（shallow dependency）的一个bug
16. 重构ScrollView.scrollTo()API，使其参数结构更清晰
### ANDROID
### 新特性
1. 在CatalystInstance接口中导出setGlobalVariable方法
2. Android版的AppState
3. 为图片添加overlayColor属性
4. 开源<ImageEditor>, <ImageStore>组件
5. 为ViewPagerAndroid添加onPageScrollStateChanged事件
6. 现在支持自定义的缩放类型
7. 更新Android的ScrollView.scrollTo接口，使其与JS/iOS相匹配
8. 为Android WebView添加headers属性
9. 为Android TextInput添加selectionColor属性
10. 为Android ScrollView添加scrollEnabled属性
### Bug修复
1. 针对不同架构编译时，不再生成通用的APK
2. 修复Android TextInput中textAlign的样式问题
3. reactTagForTouch方法不再触发空指针异常
4. 修复由于图片的uri不正确导致的崩溃
5. 修复每个XHR连接的超时时间设置
6. 修复timing初始化的bug
7. 修复在RecyclerViewBackedScrollView计算Y轴偏移量的bug
8. 显示设备尺寸时使用getRealMetrics方法
9. 修复在使用软键盘或硬件键盘时，键盘处理方法没能正确过滤字符的问题
10. Android ScrollView中现在可以自定义refreshControl
11. 修复removeClippedSubviews和视图折叠相关的bug
12. 修复在Android上使用refreshControl时，scrollTo方法的bug
### IOS
### 新特性
1. 添加了可以取消RCTTouchHandler 的API
2. 嵌在Text中的图片现在可以正确设置宽高了
3. 为触摸事件添加3dTouch属性
4. 为ScrollView添加indicatorStyle属性
5. 添加惯性滚动的开关属性
6. 在MapView的标注失去或得到焦点时，增加相应的回调事件
7. websocket现在可以在请求中携带cookie了
8. 为TextInput添加tintColor属性
### Bug修复
1. 修复iPhone6+上的屏幕尺寸bug
2. RCTGzipData() 可以接受nil输入，但没有标记为可能返回空结果
3. 修复当视图非原生时，RCTNavigator.m中的错误
4. 改进3D Touch的实现，并添加了示例
5. 修复当RefreshControl在刷新时，列表中的粘性头部滚动的位置问题
6. 限制showCompass属性的使用（需要iOS9+）


## 0.19 正式版发布
**本版本有个bug导致无法正常运行，请参阅此贴修复 http://bbs.reactnative.cn/topic/208**
### 新特性
1. 为ListView添加scrollTo方法
2. 添加followUserLocation属性，用于在地图上持续跟踪用户的位置变化
3. 添加一个选项，用于决定在某个模块无法解析时，是否抛出异常
4. 现在支持promise的异常捕获
5. 现在可以从XMLHttpRequest 获取服务器返回的具体地址
6. 对ScrollResponder的scrollResponderZoomTo方法添加了第二个参数，用于决定是否开启动画
7. 对Navigator的configureScene方法添加第二个参数routeStack，用于查看路由栈
8. 添加PixelRatio.pixel()方法，返回允许绘制的最细的宽度
9. 为WebView添加onLoading系列属性事件
10. 为Android和iOS添加XHR的超时设置
### Bug修复
1. 修复resolver中的lint警告
2. 在wrong-react-native脚本中返回正确的退出代码
3. 在transform管道线中正确传递异常
4. 修复packager的缓存错误
5. 修复TouchableNativeFeedback中的background警告
6. 在PushNotificationsIOS中添加手工链接相关的文档
7. 修复在iOS中，Navigator替换了第一个场景却不更新的问题
8. 在无法正确调用node的前提下不会再尝试调用npm
9. 修复了ListView中的一些临界值导致的bug
10. 在没有变换（transform）需要执行时，不再执行内部变换
11. 修复Windows上的'Error: spanw npm ENOENT'问题
12. 修复把navigationBar设为null时引起的错误
13. FormData现在可以支持非字符串和非对象的值
14. 修复了FormData只能附加字符串或带有uri属性的对象的问题
15. 修复了在windows上调用编辑器会导致红屏的问题
16. 修复滚屏时的偏移计算错误
17. 修复命令行工具的"sourcemap-output"选项
18. 对XHR的onReadyStateChange方法默认绑定this
### ANDROID
### 新特性
1. 新增AppState组件
2. 新增和iOS接口一致的Picker组件
3. 开启WebView的调试功能
4. WebWorkers：新的NativeRunnable的c++接口
5. WebWorkers：添加JSLoader API，用于根据AssetLoader引用从资源中读取脚本
6. 为ListView添加stickyHeaderIndices
7. 为@ReactProp 添加标注预处理
8. 为Android的TextInput添加onSelectionChange
9. 允许取消DevServer的刷新请求
10. 现在可以针对不同架构（arm, x86）编译
11. android现在支持alert()方法
12. react.gradle中现在支持Build Variants
13. 开源Spinner组件（又称Picker或是下拉菜单）
14. 为ReactHorizontalScrollView添加removeClippedSubviews
### Bug修复
1. 如果jsbundle是从assets目录中读取的，则会读取内置的图片等资源，否则读取和jsbundle同目录的资源（这个大概修复了打包后图片不显示的问题？）
2. Java exception snprintf off by one – 0b15418
3. 修复proguard开启时导致的编译和运行时错误
4. ProgressBarAndroid: styleAttr的默认值
5. 当不在开发模式下时，不创建DevSupportManager
6. 修复使用屏幕软键盘时，onTextInput回调的end值
7. 修复WebView的重复加载
8. 修复行内图片文本尺寸不正确的问题
9. 支持对任何类型的视图设置阴影
10. 使用Buck来编译React Native
11. 修复给ViewPagerAndroid传递空子节点时导致的崩溃
12. 增加wroker-farm的超时时间
13. 移除Android Switch组件的固定尺寸
### 重大变更
1. WebView中的属性不再带有平台后缀
2. 更改了onDropViewInstance方法的构型
### IOS
### 新特性
1. Wait for JSExecutor to tear down in RCTBridgeTests – 8772a6a
2. 添加react-native run-ios命令
3. 在UIlocalNotification中添加soundName设置
4. 添加了phone-pad类型的键盘
### Bug修复

1. 现在iOS7中也支持URL的查询方法了
2. 重新开启testUnderlyingBridgeisDeallocated
3. 修复RCTModuleData中一个潜在的死锁问题
4. 改进空url的处理逻辑
5. Fix extra native modules missing bridge after reload – 0fa1f8d
6. 更新profiler中的createView方法
7. 修复多行TextInput不折行的问题
8. 修复info.plist中NSLocationAlwaysUsageDescription被忽略的问题
9. ActionSheetIOS现在可以在modal中使用
10. 改善阴影性能
11. 在加载失败时立即终止js executor
### 重大变革
1. 在iOS上实现Android的dispatchViewManagerCommand接口
2. 将测试代码迁移到iOS9.2 / Xcode 7.2上
3. 禁止背景色样式的继承，文本节点除外



## 0.18.0-rc版发布
**正式版有一个bug无法正常运行参照http://bbs.reactnative.cn/topic/208**
### 新特性
1. 更新React等依赖
2. ListView现在支持onLayout和onContentSizeChange属性
3. Animated.multiply和Animated.add现在可以支持多个动画值
4. 新的跨平台的PullToRefreshView组件
5. <Text>现在支持阴影了
### Bug修复
1. ImmediatelyResetRouteStack现在可以正确更新Navigator的标题
2. pop()方法现在可以正确刷新navigatorBar
3. 修复由TextInput引起的应用崩溃
4. 修复把navigationBar设为null时引起的错误
5. 在transform管道线中正确传递异常
### ANDROID
### 新特性
1. 现在支持自定义的Android视图
2. 现在支持onScrollBeginDrag/End和onMomentumScrolBegin/End事件
3. 添加一个基础活动类ReactActivity
4. 为IntentAndroid添加getInitialURL方法，以获取调起当前app的深度链接
5. 为ToolbarAndroid添加contentInsetStart和contentInsetEnd属性
6. WebView现在可以控制本地存储的开启与关闭
7. 开源ART组件(一个绘图库)
8. 现在可以针对不同架构（arm, x86）编译
9. android现在支持alert()方法
### Bug修复
1. 修复了当视图位于屏幕外且被裁切移除时，调用measure方法会引起崩溃的问题
2. 修复了当WebView跳转新地址且认为加载完成时，报告的仍然是旧地址的问题
3. 修复了开发者菜单中“检查元素”选项的文本状态变化
4. 修复由于缺乏网络权限导致NetInfo崩溃的问题
5. 修复WebView无法显示UTF-8字符的问题
### IOS
### 新特性
1. MapView现在可以使用自定义的视图来做标注
2. MapView现在支持可拖拽的标注
3. SliderIOS现在可以设置最小值和最大值的轨道背景图
4. 现在支持虚线式(dashed)和点式(dotted)的边框样式
5. WebSocket现在支持二进制数据类型 (ArrayBuffer)
6. 为Image添加getSize()方法，用于在显示图片前获得图片的尺寸
7. 添加了一个方法用于获取当前状态栏的高度
### Bug修复
1. 修复getCurrentPosition
2. 修复<Image source={{ uri: null }} />会导致崩溃的问题
3. iOS7下现在可以正确获取url参数了
### 重大变更
1. 现在要在Android WebView中开启JavaScript支持的话，要使用javaScriptEnabled属性，而不再是javaScriptEnabledAndroid


## 0.17正式版发布
### 高层变更
1. 添加Android WebView
2. 新的Alert API，同时支持iOS和Android
3. 用js封装UIManager原生模块，以实现更好的抽象性
4. 暴露一个全局变量navigator.product，用来判断当前js的运行环境是否是React Native。webpack的用户请注意，由于这一特性需要读取json文件，因此你可能需要用到json-loader
5. 修复Windows 10上打包失败的问题
6. 修复在Navigator中通过ref拿不到navigationBar的引用的问题
7. 现在Babel支持for-of循环的转换了
8. 修复了packager没有正确处理assetRoots参数的问题
9. 修复了inspect无状态组件会引起崩溃的问题
10. 在iOS和Android上添加了新的剪贴板组件。之前在iOS上叫做RCTPasteboard
11. 修复了在windows上使用require("./image")的问题
### ANDROID
1. 开源SwipeRefreshLayoutAndroid组件，可用于竖直方向手势刷新（例子）
2. JSC profiler现在可以指定文件输出
3. 通过使用Android特定的elevation属性实现了视图阴影。但只能在Android 5.0+上使用。
4. 现在图片支持onLoad系列事件
5. Android的单元测试代码现已开源
6. 现在支持给FrescoModule传递ImagePipelineConfig，以改进Fresco的可配置性
7. 现在开始实验性地支持LayoutAnimation，但暂时需要通过UIManager.setLayoutAnimationEnabledExperimental手动开启
8. 修复了变换过(transformed)的视图会在原位置接受触控的问题
9. 现在支持NetInfo
10. ToolbarAndroid现在支持从右到左的文字方向RTL (right-to-left)
11. Image现在添加了loadingIndicatorSrc属性，类似于iOS的defaultSource，用于在loading时先显示点加载提示
12. 为ReactPropGroupAdded添加了double类型
13. 为视图添加了rotateX和rotateY变换
### IOS
1. 修复TextInput中包含富文本时出现的一些诡异的滚动问题
2. SliderIOS现在可以使用自定义图片
3. MapView的标注现在可以使用自定义的颜色和图片
4. MapView现在支持折线段：你可以在两点间使用自定义的颜色和宽度来绘制线段
5. 添加didSetProps回调，它会在你为视图设置props之后调用
6. 修复了多行 TextInput的onFocus/onBlur事件
7. 通过添加另一种实现修复了MapView在iOS 8中崩溃的问题
8. 为ActionSheetIOS添加了excludedActivityTypes
9. 为AlertIOS添加了secure-text和login-password的输入类型。同时修复了取消按钮的高光样式，以及OK/Cancel按钮对应的本地化表达
10. 为多行TextInput添加了blurOnSubmit属性，它模拟了在单行文本框中按回车键的行为
11. 修复了TextInput在iOS 8及更低版本系统中的一些问题
12. 修复了嵌套ScrollView中的滚动问题
13. TabBarIOS现在可以以字符串的形式指定systemIcon
14. LinkingIOS现在支持通用链接
15. PickerIOS现在支持style属性，可以自定义字体大小、颜色和对齐方式
16. ActionSheetIOS的按钮现在可以指定tintColor
### 重大变更
1. RCTRootView的initialProperties属性已被移除
2. UIManager不再支持Scrollview
3. iOS的原生模块bridge.modules现已过时，请使用bridge.moduleClasses或bridge moduleForName/Class。这一变更是为了实现原生模块的懒加载(lazy-loading)，提升效率
4. PullToRefreshLayoutAndroid组件现已更名为PullToRefreshViewAndroid




## 0.16正式版发布
### JS
1. 添加了一些辅助函数，以修复Babel 6在import语法逻辑上的变化
2. 现在可以使用For-of语法
3. 使Babel 6插件也能支持ES6模块
### ANDROID
1. 添加了PullToRefreshViewAndroid组件
2. 为Android视图添加了阴影效果
3. 现在对于transformed view可以正确处理触控操作（应该是修复了scrollable tab view一类第三方组件的问题）

## 0.16.0-rc版发布
### 高层变更
1. RGBA颜色值现在支持缩写方式（比如'rgba(255,0,0,0.5)'可以写为'#f007'）
2. Babel升级到版本6
3. Array.from方法现在作为兼容接口(polyfill)提供了，即在任何运行环境中均可使用
### ANDROID
1. Android现在支持自定义的字体了，但仅限ttf和otf格式
2. ViewPager现在可以使用setPageWithoutAnimation来禁用动画了
3. TextView中现在支持图片了，比如表情(emoji)
4. 添加了性能分析器Systrace的使用文档
### IOS
1. TextInput添加了keyboardAppearance属性，可以用来显示深色背景的键盘
2. 本地存储接口AsyncLocalStorage添加了内存缓存
3. TextInput现在支持onSelectionChange事件
4. iOS现在支持min/maxWidth以及min/maxHeight样式属性
5. 发布了RCTPasteboard组件，用来操作剪贴板
### 可能引起不兼容的变更
1. Android上的触控事件得到的坐标现在和iOS一致了
2. 默认启用YellowBox
3. 升级到Babel 6 。虽然我们在Facebook内部已经试用了相当长一段时间的Babel 6， 但如果你碰到任何与Babel相关的错误，比如某些JS特性的转换并不符合预期，请报告给我们，我们会尽快修复。
4. 在Babel合并T2645补丁之前，你还无法使用Decorator特性。
5. 由于Babel暂时的一个bugT2694，export default class Foo extends Bar语句无法使用（现阶段你可以把class声明和export声明分两行写）。
6. RCTSparseArray现在由NSDictionary代替了。有用到RCTSparseArray的模块请尽快更新。
移除RCTWebViewExecutor



## 0.15正式版发布
### 0.15 正式版更新日志（在rc版的基础上）
1. 安卓现在可以支持地理定位
2. IntentAndroid组件开源发布。从此可以在安卓上打开系统浏览器或是调用其他App了。
3. Android的网络请求现在可以保存cookie了。
### 0.15 rc版更新日志
1. 现在ReactNative基于React 0.14了。关于这件事，React 0.14更新日志值得一读。
2. Android下，横竖屏切换不会再重启App了
3. iOS增加了富文本输入(RichText)的支持
4. 在两个平台上都改善了报错弹窗（红屏）的提示。
5. Android下支持了systrace（一个Android性能调优工具）
