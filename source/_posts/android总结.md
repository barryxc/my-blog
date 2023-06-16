---
title: Android总结
date: 2020-04-24 09:58:19
tags:
  - android
password: "#159357"
category: android
---

## 基础

- `activity`生命周期与启动模式

  ```
  standard & singletask & singletop & singleInstance
  ```

- `service`生命周期 startservice`&`bindservice 区别和使用场景

- `contentprovider`

- [`view`事件分发机制](https://blog.csdn.net/w1070216393/article/details/84261996)

- `activity`启动过程

- `view`绘制流程

  ```kotlin
  //页面加载
  setContentView()
  //重新布局
  requestLayout()
  //重新绘制
  invalidate()
  postInvalidate()

  //遍历过程
  fun performTraversals(){
    performMeasure()
    performLayout()
    performDraw()
  }
  ```

  <!-- more -->

- `ANR`常见的发生原因&解决方案

  产生原因：

  ```
  1.keyDispatchTimeout（5秒内，用户事件未响应）
  2.broadcastTimeout（10秒内onReceive()函数未处理完成）
  3.serviceTimeout(20秒内服务生命周期函数未处理完成)
  ```

  - 问题场景：

    ```
    应用程序UI线程存在io耗时操作、应用程序UI线程等待子线程释放某个锁、耗时的动画需要大量的计算，导致cpu负载过重，UI线程得不到cpu时间片
    ```

  - 定位分析：

    ```
    通过logcat和/data/anr/traces.txt文件定位和分析
    ```

  - 避免和检测：

    ```
    blockcanary性能监控。基本原理是利用主线程的消息队列处理机制，通过对比消息分发开始和结束的时间点来判断是否超过设定的时间。
    ```

- `handler`机制原理

  ```shell
  - handler.post(Runnable r)
  - Looper.prepare()
  - Looper.myLooper()
  - Looper.loop()
  - messageQueue.addIdleHandler(IdleHandler handler)
  ```

- [动态换肤原理](https://www.jianshu.com/p/53ed7ba95722)

- `ListView`&`RecylerView`的区别

- `AMS`

- `WMS`

- `PMS`

## [kotlin](https://www.jianshu.com/p/06703abc56b1)

- 协程原理
- Jetpack

## Ipc 通信机制

- **传统解决方案：socket & 管道 & 消息队列**
- 非实时方案：**文件共享**
- **android 解决方案 binder**

  - **aidl**

  - **messenger**
  - **bundle**
  - **ContentProvider**

```
binder优点：传统ipc方案，用户空间数据拷贝到内核空间，内核空间再次拷贝到另一个用户空间，2次拷贝。binder采用mmap内存映射机制（将用户空间地址拷贝到内核空间，没有直接拷贝数据，在调用时，通过mmu&中断机制，将a用户空间数据拷贝到b用户空间），1次数据拷贝，更高效
```

## 多线程 🤡

- **线程池原理**

  ![188580-202ba87b6a285694](https://raw.githubusercontent.com/barryxc/pictures/main/img188580-202ba87b6a285694.png)

- [**synchronized 锁的底层实现**](https://zhuanlan.zhihu.com/p/75880892)&`reentrantlock`区别

  - java 对象内存区域划分

    - 对象头：HotSpot 虚拟机的对象头分为两部分信息：数组分为三部分

      - Mark Word 存储对象的哈希码、GC 分代年龄、锁信息等
      - 32 位/64 位 Class MetaData Address 指向对象类型数据的指针
      - （数组） 32 位/64 位 数组长度

    - 实例数据

    - 对齐部分

- **锁膨胀**

  - 无锁状态
  - 偏向锁状态
  - 轻量级锁状态（当有第二个线程申请资源时，不一定存在竞争）
  - 自旋锁&**自适应自旋锁**（自旋次数不固定）
  - 重量级锁（系统 mutex 调用）

- **锁消除**

- **锁粗化**

- **[乐观锁和悲观锁](https://blog.csdn.net/caisongcheng_good/article/details/79916873)**&CAS 原子操作

- **volatile 关键字**

  可以保证内存可见性，防止寄存器缓存

  防止指令重排：指令重排不会影响单个程序的运行，但会影响线程并发执行的正确性

  <u>无法保证原子性：</u>

## 数据库

基本概念：

1. 存储过程
2. 索引实现原理
   - 密集索引
   - 稀松索引
3. 事务特性

优化方案：

```
一般来说，在系统设计阶段就应该根据业务耦合松紧来确定垂直分库，垂直分表方案，在数据量及访问压力不是特别大的情况，首先考虑缓存、读写分离、索引技术等方案。若数据量极大，且持续增长，再考虑水平分库水平分表方案。
```

1. 索引的实现原理
2. 分库分表机制
3. 缓存机制
4. 读写分离机制

## 性能优化

- **冷启动优化：**

  ```
  冷启动流程：appliction:oncreate()->activity:oncreate()->activity-onresume() 在第一个页面加载完成之前，wms会预先启动个预览窗口。
  1.减少application:oncreate()耗时：懒加载，异步加载
  2.设置apptheme:windowbackground,使得预览窗口非白屏或者黑屏，提升视觉启动体验
  3.减少xml布局层级,优化启动页xml布局。
  4.Activity启动优化 onCreate，onStart，onResume中耗时较短但非必要的代码可以放到IdleHandler中执行，减少启动时间
  ```

- **布局优化 ：**

  - include 标签共享布局

  - viewStub 标签延迟加载

  - merge 标签减少布局层次

  - 尽量使用 compoundDrawable 代替 imageview 和 textview 组合

  - 布局加载性能监控

    ```java
    LayoutInflaterCompat.setFactory(getLayoutInflater(), new LayoutInflaterFactory() {
            @Override
            public View onCreateView(View parent, String name, Context context, AttributeSet attrs)
            {
                long startTime = System.currentTimeMillis();
                View view = null;
                try {
                    view = getLayoutInflater().createView(name, null, attrs);
                } catch (ClassNotFoundException e) {
                    e.printStackTrace();
                }
                long cost = System.currentTimeMillis() - startTime;
                map.put(parent,new Hodler(parent,view,name,cost));
                Log.d("=========", "加载布局：" + name + "耗时：" + cost);
                return view;
            }
        });
        super.onCreate(savedInstanceState);
    ```

- **电量优化**

- **数据库优化**

- **内存优化：**

  - 集合容器对象使用 WeakReference 引用
  - 长生命周期对象如 application、单例对象不要存储大数据
  - 防止 activity 内部非静态内部类实例引用外部 this 指针导致内存泄漏
  - 频繁创建的短生命周期的小对象可以使用对象池复用技术
  - 限制网络，图片，数据库内存缓存大小
  - 消息队列使用有界队列，防止生产和消费不平衡导致背压

- **弱网络优化：**

  - 避免 dns 解析和劫持
  - 业务层合并网络多个类似的请求
  - 预先加载数据
  - 避免轮询
  - 使用 http 缓存-http 协议（静态资源使用 http cache）
  - 压缩数据大小 (压缩 content)
  - cdn 内容网络分发加速

- **代码优化：**

  - 避免创建非必要对象
  - 频繁创建的短生命周期对象使用对象池
  - 常量使用 static final 修饰符
  - 避免内部使用 setters/getters
  - 防止内存泄漏，使用 leakcanary 监控内存泄漏
  - 使用 blockcanary 监控主线程耗时

- **图片优化:**

  ```
  使用压缩工具对PNG资源图片进行压缩、尽量使用.9.png图片格式
  ```

## gradle 构建流程

```
待补充
```

## apk 打包和签名 ☺️

- **apk 打包流程**

  ```shell
  #合并资源文件
  gradle merge task

  appt

  aidl

  javac

  dx

  apkbuilder

  jarsigner

  zipalign
  ```

  ![v2-e15390bbaf18d21f98cd742e3dcec99b_r](https://raw.githubusercontent.com/barryxc/pictures/main/imgv2-e15390bbaf18d21f98cd742e3dcec99b_r.jpg)

- **apk 签名流程**

  ```
  META-INF:MANIFEST.MF&CERT.SF&CERT.RSA
  ```

## [java 内存区域模型（JMM）](http://tutorials.jenkov.com/java-concurrency/java-memory-model.html)

- **内存区域划分:**

  - 程序计数器&java 虚拟机栈&堆&本地方法栈&方法区
  - 运行时堆内存的划分：新生代和老年代。新生代的又划分为：eden&from survior&to survior

- **jvm 垃圾回收机制：**
  - 如何确定对象是否可回收？ 引用计数法&可达性分析算法
  - 如何回收垃圾对象？标记-清除算法&复制算法&标记-整理算法&分代收集算法

## AOP 切面编程

- **APT&注解技术**

  ```
  （运行时注解）javapoet(.java源码生成工具)
  ```

- **javassist、asm**

  ```
  （字节码织入,编译时通过gradle&运行时，类装载之前替换）
  ```

- **反射&动态代理**

  ```
  Proxy & InvocationHandler
  ```

## 类加载机制和反射

- java 类加载机制

  ```
  全盘负责、双亲委派（父类委托）、缓存机制
  ```

- 反射

- 插件化原理

  ```
   宿主apk如何调启插件apk:
   - 字节码替换
   - 资源替换
   - so库替换
  ```

- 热修复原理

  - Nuwa
  - Andfix、Dexposed

  ```
  两种方案原理：
  - 类加载时，动态修改字节码.class文件格式（需要重新启动）
  - 运行时，动态替换class类型对象的内存结构（不需要重新启动）
  ```

## 依赖注入

```
待补充
```

## 数据结构

- 数组

  ```
  Array、ArrayList
  ```

- 链表（栈和队列）

  ```
  LinkedList、ArrayDeque、Stack
  ```

- 哈希表

  ```java
  HashMap、LinkedHashMap、LRU、ConcurrentHashMap
  ```

- 二叉树

  > 深度、广度、镜像

- 红黑树

  > 自平衡二叉搜索树

- B 树（多路平衡搜索树）

- B+树

- B\*树

## 算法

- 十大内部排序

  - 直接选择排序
  - 插入排序
  - 折半插入排序
  - 希尔排序
  - 冒泡排序
  - 快速排序
  - 堆排序
  - 归并排序
  - 桶排序
  - 基数排序

- 动态规划

- 贪心算法

- 多指针

## [Hybrid 技术原理](https://www.cnblogs.com/peakleo/p/10572749.html)

```
Hybrid App的本质，其实是在原生的 App 中，使用 WebView 作为容器直接承载 Web页面。因此，最核心的点就是 Native端 与 H5端 之间的双向通讯层，其实这里也可以理解为我们需要一套 跨语言通讯方案，来完成 Native(Java/Objective-c/...) 与 JavaScript 的通讯。实现的关键，便是作为容器的 WebView，一切的原理都是基于 WebView 的机制。
```

#### native 调用 js

1. `loadUrl`无法直接获取返回值

   ```java
   mWebView.loadUrl("javascript: 方法名('参数需要转为字符串')");
   ```

2. `evaluateJavascript`4.4+版本

   ```java
   mWebView.evaluateJavascript("javascript: 方法名('参数需要转为字符串')", new ValueCallback<String>() {
   		@Override
   		public void onReceiveValue(String value) {
         // 这里的value即为对应JS方法的返回值
   		}
   });
   ```

#### js 调用 native

1. `WebView URL Scheme` 跳转拦截
2. `WebView` 中的`prompt/console/alert`拦截：通常使用`prompt`，因为这个方法在前端中使用频率低，比较不会出现冲突
3. `WebView API`注入：原理其实就是 Native 获取 JavaScript 环境上下文，并直接在上面挂载对象或者方法，使 js 可以直接调用，Android 与 IOS 分别拥有对应的挂载方式

## 异常处理

- **java 层 crash 捕获机制**

  ```java
  //设置指定线程的异常捕获处理器
  Thread.currentThread().setUncaughtExceptionHandler();
  //设置全局的异常捕获处理器
  Thread.setDefaultUncaughtExceptionHandler(new Thread.UncaughtExceptionHandler() {
      @Override
      public void uncaughtException(@NonNull Thread t, @NonNull Throwable e) {

      }
  });
  ```

- **native 层 crash 捕获机制**

  ```java
  c++层代码错误可以分为两种：
  
  1. std::exception 异常：
  2. fatal signal异常：
  
     常见的软中断信号：
       -	SIGFPE 浮点异常
       -	SIGSEGV 无效的内存引用 (segmentation violation)
       -	SIGILL 非法指令
  
    如何捕获？
    	注册信号处理函数，然后向java层发送消息，通知抓取logcat日志信息。然后通过addr2line等工具对dump文件函数地址转换为对应的代码行数。
  ```

## 网络安全

### 对称秘钥密码体制

- DES（Data Encryption Standard）
- [AES](https://www.pianshen.com/article/92851078995/)（Advanced Encryption Standard）

  1. [**电码本模式**（Electronic Codebook Book (ECB)）](http://www.361way.com/aes/5830.html)

  2. [**密码分组链接模式**（Cipher Block Chaining (CBC)）](https://www.cnblogs.com/eleven-elv/p/7289579.html)

  3. 计算器模式（Counter (CTR)）

  4. 密码反馈模式（Cipher FeedBack (CFB)）

  5. 输出反馈模式（Output FeedBack (OFB)）

### 公钥密码体制

- RSA

  ```
  RSA公开密钥密码体制的原理是：根据数论，寻求两个大素数比较简单，而将它们的乘积进行因式分解却极其困难，因此可以将乘积公开作为加密密钥
  ```

- ECC（椭圆曲线加密算法）

- DH（秘钥交换算法）

### 散列算法

- MD5 （消息摘要）
- SHA 安全散列算法（Secure Hash Algorithm）

### 签名算法

- [HMAC](https://www.liaoxuefeng.com/wiki/1016959663602400/1183198304823296)（Hash-based Message Authentication Code）
- 非对称加密（两组秘钥双向加密解密）
- MD5+加盐

## IP

```
待补充
```

## TCP😁

- 报文格式

  ![27194088468_4cb0141fc8_b](https://raw.githubusercontent.com/barryxc/pictures/main/img27194088468_4cb0141fc8_b.jpg)

- 滑动窗口

  ```
  滑动窗口大小：用来告知发送端接收端的缓存区大小，以此控制发送端发送数据的速率，从而达到流量控制。窗口大小时一个16bit字段，因而窗口大小最大为65535
  ```

## [HTTP 协议](https://www.cnblogs.com/heluan/p/8620312.html)

- **tcp 三次握手 🤝+四次挥手 👋**

- **tls 握手流程**

  - **client_hello**
  - **server_hello**
  - **证书校验**
  - **秘钥协商**(DH 算法)

- **http1.1 和 1.0 区别：**

  - 带宽优化及网络连接的使用:

    ```
    在HTTP1.0中主要使用header里的If-Modified-Since,Expires来做为缓存判断的标准，HTTP1.1则引入了更多的缓存控制策略例如Entity tag，If-Unmodified-Since, If-Match, If-None-Match等更多可供选择的缓存头来控制缓存策略。
    ```

  - 支持长连接:

    ```
    HTTP 1.1支持长连接（PersistentConnection）和请求的流水线（Pipelining）处理，在一个TCP连接上可以传送多个HTTP请求和响应，减少了建立和关闭连接的消耗和延迟，在HTTP1.1中默认开启Connection： keep-alive，一定程度上弥补了HTTP1.0每次请求都要创建连接的缺点
    ```

  - 支持 host 域

    ```
    在HTTP1.0中认为每台服务器都绑定一个唯一的IP地址，因此，请求消息中的URL并没有传递主机名（hostname）。但随着虚拟主机技术的发展，在一台物理服务器上可以存在多个虚拟主机（Multi-homed Web Servers），并且它们共享一个IP地址。HTTP1.1的请求消息和响应消息都应支持Host头域，且请求消息中如果没有Host头域会报告一个错误（400 Bad Request）。
    ```

  - 缓存处理增强

    ```
    在HTTP1.0中主要使用header里的If-Modified-Since,Expires来做为缓存判断的标准，HTTP1.1则引入了更多的缓存控制策略例如Entity tag，If-Unmodified-Since, If-Match, If-None-Match等更多可供选择的缓存头来控制缓存策略。
    ```

  - 错误通知管理

    ```
    在HTTP1.1中新增了24个错误状态响应码，如409（Conflict）表示请求的资源与资源的当前状态发生冲突；410（Gone）表示服务器上的某个资源被永久性的删除。
    ```

- **http1.1 和 2.0 的区别**：

  - **新的二进制格式（Binary Format）**

    ```
    HTTP1.x的解析是基于文本。基于文本协议的格式解析存在天然缺陷，文本的表现形式有多样性，要做到健壮性考虑的场景必然很多，二进制则不同，只认0和1的组合。基于这种考虑HTTP2.0的协议解析决定采用二进制格式，实现方便且健壮。
    ```

  - **多路复用**（MultiPlexing)

    ```
    即连接共享，即每一个request都是是用作连接共享机制的。一个request对应一个id，这样一个连接上可以有多个request，每个连接的request可以随机的混杂在一起，接收方可以根据request的 id将request再归属到各自不同的服务端请求里面
    ```

  - **header 压缩**

    ```
    如上文中所言，对前面提到过HTTP1.x的header带有大量信息，而且每次都要重复发送，HTTP2.0使用encoder来减少需要传输的header大小，通讯双方各自cache一份header fields表，既避免了重复header的传输，又减小了需要传输的大小。
    ```

  - **服务端推送**（server push）

    ```
    HTTP2.0也具有server push功能。
    ```

- **http 状态码：**

  | **消息**                |     |
  | :---------------------- | --- |
  | 100 Continue            |     |
  | 101 Switching Protocols |     |

  | **成功**            |     |
  | :------------------ | --- |
  | 200 OK              |     |
  | 204 No Content      |     |
  | 206 Partial Content |     |

  | 重定向                 |     |
  | ---------------------- | --- |
  | 300 Multiple Choices   |     |
  | 301 Moved Permanently  |     |
  | 302 Move Temporarily   |     |
  | 304 Not Modified       |     |
  | 305 Use Proxy          |     |
  | 307 Temporary Redirect |     |

  | 请求错误               |     |
  | ---------------------- | --- |
  | 400 Bad Request        |     |
  | 401 Unauthorized       |     |
  | 403 Forbidden          |     |
  | 404 Not Found          |     |
  | 405 Method Not Allowed |     |
  | 408 Request Timeout    |     |
  | 409 Conflict           |     |
  | 410 Gone               |     |

  | 服务器错误                     |     |
  | ------------------------------ | --- |
  | 500 Internal Server Error      |     |
  | 501 Not Implemented            |     |
  | 502 Bad Gateway                |     |
  | 503 Service Unavailable        |     |
  | 504 Gateway Timeout            |     |
  | 505 HTTP Version Not Supported |     |

- **HTTP/1.1 协议中共定义了八种方法（有时也叫“动作”），来表明 Request-URL 指定的资源不同的操作方式**

  | 请求方法 | 描述                                                                                                       |
  | -------- | ---------------------------------------------------------------------------------------------------------- |
  | GET      | 请求指定页面信息，并返回实体主体；                                                                         |
  | POST     | 指定资源提交数据并进行处理请求，数据被包含在请求体中，POST 请求可能会导致新的资源的建立或已有资源的修改    |
  | HEAD     | 类似 GET 请求，只不过返回的响应中没有具体内容，用于获取报头                                                |
  | OPTIONS  | 返回服务器针对特定资源所支持的 HTML 请求方法 或 web 服务器发送\*测试服务器功能（允许客户端查看服务器性能） |
  | PUT      | 从客服端向服务器传送的数据取代指定的文档内容                                                               |
  | DELETE   | 请求服务器删除指定的内容                                                                                   |
  | TRACE    | 回显服务器收到的请求，用于测试和诊断                                                                       |
  | CONNECT  | HTTP1.1 协议中预留给能够将连接改为管道方式的代理服务器                                                     |

- **GET 和 POST 区别**

  - 关于编码
  - 参数传递
  - 长度限制
  - 语义
  - 安全性

  - GET 产生一个 TCP 数据包，POST 产生两个 TCP 数据包。

    ```
    对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200（返回数据）；
    而对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 ok（返回数据）。
    ```

## 常用技术栈

- `HashMap` 哈希表原理
- `LinkedHashMap`
- **`ConcurrentHashMap`** 线程安全哈希表
- `LruCache` 最近最少使用缓存
- `DiskLruCache`
- **`ReentrantLock`** 可重入锁
- `SharedPreferences` key&value 缓存存储框架（缺点）
- `CopyOnWriteArrayList` 读写分离
- `Fragment`
- `Lifecycle`
- `LiveData` 动态可观察数据
- `ArrayBlockingQueue ` 阻塞队列
- `LinkedBlockingQueue`
- `Glide`
- **`EventBus`**优缺点
- `OkHttpClient`
- `Retrofit`
- `LeakCanary` 内存泄漏监控
- `BlockCanary ` 主线程耗时监控
- `Startup` 启动库
- `GreenDao`

## 六大设计原则和 23 种设计模式

### 六大设计原则（SOLID）

1. **开闭原则**：软件实体应当对扩展开放，对修改关闭(OCP)
2. **里氏替换原则**：继承必须确保超类所拥有的性质在子类中仍然成立(LSP)
3. **依赖倒置原则**：高层模块不应该依赖低层模块，两者都应该依赖其抽象；抽象不应该依赖细节，细节应该依赖抽象。其核心思想是：要面向接口编程，不要面向实现编程。(DIP)
4. **单一职责原则**：单一职责原则规定一个类应该有且仅有一个引起它变化的原因，否则类应该被拆分(SRP)
5. **接口隔离原则**：客户端不应该被迫依赖于它不使用的方法(ISP)
6. **迪米特法则**：只与你的直接朋友交谈，不跟“陌生人”说话（Talk only to your immediate friends and not to strangers）。(LOD)

$$
**合成复用原则**：它要求在软件复用时，要尽量先使用组合或者聚合等关联关系来实现，其次才考虑使用继承关系来实现

### **23种设计模式**

- **创建型设计模式**

  - 原型
  - 单例
  - 构造者模式
  - 工厂方法
  - 抽象工厂

- **结构型设计模式**
  - 代理
  - 适配器
  - 装饰
  - 组合
  - 桥接
  - 外观
  - 享元
- **行为型设计模式**
  - 模板方法
  - 观察者
  - 策略
  - 职责链
  - 命令
  - 中介者
  - 迭代器
  - 备忘录
  - 访问者
  - 解释器
  - 状态

## 遇到的问题和解决方案
$$
