# CQQ项目目录

## 2016-08-18

### 练手--重构项目之一：项目选择

根据目前项目组项目情况，选择实名客户端进行项目重构。

该项目相对简单，结构清晰，适合基于重构练手。

后续iOS客户端应该选择该项目进行重构练手。

### 练手--重构项目之二：重构项目框架准备工作

#### 架构选择

使用Google官方提供的MVP设计模式，实现项目重构开发。

> 注：这里需要强调，请严格遵守官方实现方式，进行MVP设计。

#### 开源库选择

##### Google Guava

Google Guava官方教程（中文版）：http://ifeve.com/google-guava/

##### 网络请求

Retrofit(需要评估服务端接口是否支持) + OkHttp

##### 图片相关（应该是不需要的）

Glide 

glide-transformations

> 注：由于该功能库，有多个，所以为了后续方便切换，应该在开源库的基础上，二次封装一次接口。

##### Rx支持

RxJava + RxAndroid + RxLifeCycle + RxBinding

##### 依赖注入

Dagger2

##### 数据库相关

GreenDao

##### 日志

Logger

##### 内存溢出检测

LeakCanary 内存泄漏检测工具

##### 程序崩溃日志获取

ACRA 可以指定email进行日志发送  Android应用程序崩溃报告

##### 数据库查看

DBinspector

##### 数据解析

JSON解析：Gson

HTML解析：HtmlPaser、jsoup

##### 事件总线

Otto  一个基于Guava的增强的事件总线

##### 缓存

DiskLruCache

Android DiskLruCache完全解析，硬盘缓存的最佳方案：http://www.tuicool.com/articles/JB7RNj

##### 调试框架（使用Chrome调试）

Stetho 调试Android应用的桥梁，使得可以利用Chrome开发者工具进行调试

##### 测试框架

JUnit4 
Mockito
Espresso


#### 其他说明

##### 版本兼容性

重构工程最低支持Android4.4

##### 系统效果

使用沉浸状态栏 + MD 界面设计模式

##### 列表控件实现

列表相关控件统一使用RecyclerView实现，包括：ListView、GridView等

##### 菜单功能

使用ActionBar + 侧滑菜单

##### 使用 MultiDex 解决 64K 限制

Android 项目开发填坑记 - 使用 MultiDex 解决 64K 限制：http://likfe.com/2016/08/17/android-multiDex/



## 2016-08-11

### Mockito
Mockito 简明教程：http://www.tuicool.com/articles/J7BFr2A

Mockito官网：http://mockito.org/

GitHub：https://github.com/mockito/mockito

### Android单元测试专题

Android单元测试专题：http://chriszou.com/

Android单元测试: 首先，从是什么开始：http://chriszou.com/2016/04/13/android-unit-testing-start-from-what.html

Android单元测试（二）：再来谈谈为什么：http://chriszou.com/2016/04/16/android-unit-testing-about-why.html

Android单元测试(三)：JUnit单元测试框架的使用：http://chriszou.com/2016/04/18/android-unit-testing-junit.html

Android单元测试（四）：Mock以及Mockito的使用：http://chriszou.com/2016/04/29/android-unit-testing-mockito.html

Android单元测试（五）：依赖注入，将mock方便的用起来：http://chriszou.com/2016/05/06/android-unit-testing-di.html

Android单元测试（六）：使用dagger2来做依赖注入，以及在单元测试中的应用：http://chriszou.com/2016/05/10/android-unit-testing-di-dagger.html

Android单元测试（七）：Robolectric，在JVM上调用安卓的类：http://chriszou.com/2016/06/05/robolectric-android-on-jvm.html

关于安卓单元测试，你需要知道的一切：http://chriszou.com/2016/06/07/android-unit-testing-everything-you-need-to-know.html

安卓单元测试(八)：Junit Rule的使用：http://chriszou.com/2016/07/09/junit-rule.html

安卓单元测试（九）：使用Mockito Annotation快速创建Mock：http://chriszou.com/2016/07/16/mockito-annotation.html

Android单元测试(十)：DaggerMock：The Power of Dagger2, The Ease of Mockito The Old Way：http://chriszou.com/2016/07/24/android-unit-testing-daggermock.html

安卓单元测试(十一)：异步代码怎么测试：http://chriszou.com/2016/08/06/android-unit-testing-async.html


### 插播

(MVP+RxJava+Retrofit)解耦+Mockito单元测试 经验分享：http://www.jianshu.com/p/cdfeb6c3d099#

从源码一次彻底理解Android的消息机制：http://blog.csdn.net/ghost_programmer/article/details/52038201

一步步理解Android事件分发机制：http://blog.csdn.net/ghost_programmer/article/details/51985692


MVP 模式简单易懂的介绍方式；http://kaedea.com/2015/10/11/android-mvp-pattern/

RxJava快速入门：http://www.jianshu.com/p/6a6f7a4be38d

给 Android 开发者的 RxJava 详解：http://gank.io/post/560e15be2dca930e00da1083

## 2016-08-02

创建本人笔记文件