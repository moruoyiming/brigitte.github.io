---
title: Android 基础知识总结
thumbnail: /gallery/thumbnails/sculpture.jpg
categories: 
- Android基础
tags:
- Android
- 蓝牙开发
- 面试题
---
​     **Activity生命周期**        

[img](http://www.coderror.com/wp-content/uploads/2019/11/图片-1.png)

**Fragment生命周期**

![img](http://www.coderror.com/wp-content/uploads/2019/11/图片-2.png)

**Activity****四种启动模式**

- **standard :** **标准模式**,每次启动Activity都会创建一个新的Activity实例,并且将其压入任务栈栈顶,而不管这个Activity是否已经存在。Activity的启动三回调(*onCreate()->onStart()->onResume()*)都会执行。

- **singleTop** **:** **栈顶复用模式**.这种模式下,如果新Activity已经位于任务栈的栈顶,那么此Activity不会被重新创建,所以它的启动三回调就不会执行,同时Activity的onNewIntent()方法会被回调.如果Activity已经存在但是不在栈顶,那么作用与*standard**模式*一样.

- **singleTask:** **栈内复用模式**.创建这样的Activity的时候,系统会先确认它所需任务栈已经创建,否则先创建任务栈.然后放入Activity,如果栈中已经有一个Activity实例,那么这个Activity就会被调到栈顶,onNewIntent(),并且singleTask会清理在当前Activity上面的所有Activity.(clear top)

- **singleInstance** : 加强版的singleTask模式,这种模式的Activity只能单独位于一个任务栈内,由于栈内复用的特性,后续请求均不会创建新的Activity,除非这个独特的任务栈被系统销毁了

  <!-- more -->

**Service****的生命周期与启****动****方法由什么区****别****？**

- **startService**()：开启Service，调用者退出后Service仍然存在。
- **bindService**()：开启Service，调用者退出后Service也随即退出。

**Service****生命周期：**

- 只是用startService()启动服务：onCreate() -> onStartCommand() -> onDestory
- 只是用bindService()绑定服务：onCreate() -> onBind() -> onUnBind() -> onDestory
- 同时使用startService()启动服务与bindService()绑定服务：onCreate() -> onStartCommnad() -> onBind() -> onUnBind() -> onDestory

**广播****发****送和接收的原理了解****吗****？**

1. 继承BroadcastReceiver，重写onReceive()方法。
2. 通过Binder机制向ActivityManagerService注册广播。
3. 通过Binder机制向ActivityMangerService发送广播。
4. ActivityManagerService查找符合相应条件的广播（IntentFilter/Permission）的BroadcastReceiver，将广播发送到BroadcastReceiver所在的消息队列中。
5. BroadcastReceiver所在消息队列拿到此广播后，回调它的onReceive()方法。、

### Android Handler机制是做什么的，原理了解吗

![img](http://www.coderror.com/wp-content/uploads/2019/11/图片-3.png)

主要涉及的角色如下所示：

1.**Message**:消息,分为硬件产生的消息（例如:按钮、触摸）和软件产生的消息。

**2. MessageQueue**：消息队列，主要用来向消息池添加消息和取走消息。

**3. Looper**：消息循环器，主要用来把消息分发给相应的处理者。

**4. Handler**：消息处理器，主要向消息队列发送各种消息以及处理各种消息。

整个消息的循环流程还是比较清晰的，具体说来：

**1. Handler**通过**sendMessage**()发送消息**Message**到消息队列**MessageQueue**。

**2. Looper**通过**loop**()循环提取触发**Message**,并将**Message**交给对应的**target handler**来处理。

**3. target handler**调用自身的**handleMessage**()方法来处理**Message**。

**如何自定义android控件**

1. 自定义属性的声明和获取

   1. 分析需要的自定义属性

   1. 在res/values/attrs.xml定义声明

   1. 在layout文件中进行使用

   1. 在View的构造方法中进行获取

1. 测量onMeasure(int widthMeasureSpec, int heightMeasureSpec)
2. 布局onLayout(boolean changed, int left, int top, int right, int bottom)
3. 绘制onDraw(Canvas canvas)
4. onTouchEvent
5. onInterceptTouchEvent(ViewGroup)
6. 状态的恢复与保存

**描述一下****View****的****绘****制原理？**

View的绘制流程主要分为三步：

1. **onMeasure**：测量视图的大小，从顶层父View到子View递归调用measure()方法，measure()调用onMeasure()方法，onMeasure()方法完成测量工作。
2. **onLayout**：确定视图的位置，从顶层父View到子View递归调用layout()方法，父View将上一步measure()方法得到的子View的布局大小和布局参数，将子View放在合适的位置上。
3. **onDraw**：绘制最终的视图，首先ViewRoot创建一个Canvas对象，然后调用onDraw()方法进行绘制。onDraw()方法的绘制流程为：① 绘制视图背景。② 绘制画布的图层。 ③ 绘制View内容。 ④ 绘制子视图，如果有的话。⑤ 还原图层。⑥ 绘制滚动条。

**requestLayout()****、****invalidate()****与****postInvalidate()****有什么区****别****？**

- **requestLayout**()：该方法会递归调用父窗口的requestLayout()方法，直到触发ViewRootImpl的performTraversals()方法，此时mLayoutRequestede为true，会触发onMesaure()与onLayout()方法，不一定 会触发onDraw()方法。
- **invalidate**()：该方法递归调用父View的invalidateChildInParent()方法，直到调用ViewRootImpl的invalidateChildInParent()方法，最终触发ViewRootImpl的performTraversals()方法，此时mLayoutRequestede为false，不会 触发onMesaure()与onLayout()方法，当时会触发onDraw()方法。
- **postInvalidate**()：该方法功能和invalidate()一样，只是它可以在非UI线程中调用。

### APK的打包流程

![img](http://www.coderror.com/wp-content/uploads/2019/11/图片-4.png)

**1.** 通过AAPT工具进行资源文件（包括AndroidManifest.xml、布局文件、各种xml资源等）的打包，生成R.java文件。

**2.** 通过AIDL工具处理AIDL文件，生成相应的Java文件。

**3.** 通过Javac工具编译项目源码，生成Class文件。

**4.** 通过DX工具将所有的Class文件转换成DEX文件，该过程主要完成Java字节码转换成Dalvik字节码，压缩常量池以及清除冗余信息等工作。

**5.** 通过ApkBuilder工具将资源文件、DEX文件打包生成APK文件。

**6.** 利用KeyStore对生成的APK文件进行签名。

**7.** 如果是正式版的APK，还会利用ZipAlign工具进行对齐处理，对齐的过程就是将APK文件中所有的资源文件举例文件的起始距离都偏移4字节的整数倍，这样通过内存映射访问APK文件 的速度会更快。

### APK的安装流程

![img](http://www.coderror.com/wp-content/uploads/2019/11/图片-5.png)

**1.** 复制APK到/data/app目录下，解压并扫描安装包。

**2.** 资源管理器解析APK里的资源文件。

**3.** 解析AndroidManifest文件，并在/data/data/目录下创建对应的应用数据目录。

**4.** 然后对dex文件进行优化，并保存在dalvik-cache目录下。

**5.** 将AndroidManifest文件解析出的四大组件信息注册到PackageManagerService中。

**6.** 安装完成后，发送广播。

**Android Binder****机制是做什么的，****为****什么****选****用****Binder****，原理了解****吗****？**

Android Binder是用来做进程通信的，Android的各个应用以及系统服务都运行在独立的进程中，它们的通信都依赖于Binder。

为什么选用Binder，在讨论这个问题之前，我们知道Android也是基于Linux内核，Linux现有的进程通信手段有以下几种：

1. **管道**：在创建时分配一个page大小的内存，缓存区大小比较有限；
2. **消息****队****列**：信息复制两次，额外的CPU消耗；不合适频繁或信息量大的通信；
3. **共享内存**：无须复制，共享缓冲区直接付附加到进程虚拟地址空间，速度快；但进程间的同步问题操作系统无法实现，必须各进程利用同步工具解决；
4. **套接字**：作为更通用的接口，传输效率低，主要用于不通机器或跨网络的通信；
5. **信号量**：常作为一种锁机制，防止某进程正在访问共享资源时，其他进程也访问该资源。因此，主要作为进程间以及同一进程内不同线程之间的同步手段。

\6.  **信号** : 不适用于信息交换，更适用于进程中断控制，比如非法内存访问，杀死某个进  程等；

既然有现有的IPC方式，为什么重新设计一套Binder机制呢。主要是出于以上三个方面的考量：

- 高性能：从数据拷贝次数来看Binder只需要进行一次内存拷贝，而管道、消息队列、Socket都需要两次，共享内存不需要拷贝，Binder的性能仅次于共享内存。
- 稳定性：上面说到共享内存的性能优于Binder，那为什么不适用共享内存呢，因为共享内存需要处理并发同步问题，控制负责，容易出现死锁和资源竞争，稳定性较差。而Binder基于C/S架构，客户端与服务端彼此独立，稳定性较好。
- 安全性：我们知道Android为每个应用分配了UID，用来作为鉴别进程的重要标志，Android内部也依赖这个UID进行权限管理，包括6.0以前的固定权限和6.0以后的动态权限，传荣IPC只能由用户在数据包里填入UID/PID，这个标记完全 是在用户空间控制的，没有放在内核空间，因此有被恶意篡改的可能，因此Binder的安全性更高。