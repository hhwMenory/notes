---
title: android 学习笔记
date: 2016-10-11 12:56:06
category: java
---

### 搭建环境

    JAVA_HOME：JDK  安装位置
    CLASSPATH：系统类
    PATH
    
    ADT

### 项目结构

    src java 源代码
    gen 系统自动生成的配置文件
    asssets 资源文件 不占用 apk 包的大小
    bin 编译后文件
    libs
    res 应用用到的资源 占用 apk 包的大小

      - drawable 不同密度的图片
      - layout 存放布局文件

    values 存放字符串 主题 颜色 样式等
    AndroidManifest.xml 清单文件 配置一些与应用有关的重要信息，包含包名 权限 程序组件
    
### 控件 

#### 控件常用属性

``` bash

    android:id 控件 ID    
    android:layout_width 控件宽度
    
      - wrap_content: 包裹实际文本内容
      - match_parent: 当前控件铺满父类容器  -- 2.3 api 之后添加的属性值
      -  fill_parent: 当前控件铺满父类容器  -- 2.3 api 之前的属性值

    android:layout_height 控件宽度
    android:text 文本内容
    android:textSize 文本颜色
    android:textColor 文本颜色
    android:background 控件背景
    android:hint 输入提示文本
    android:inputType 输入文本类型

```

#### TextView
#### EditView
#### ImageView
    
>　显示图片控件

``` bash
    
    android:src="@drawable/ic_launcher" --- 内容图片
    android:background="@drawable/ic_launcher" --- 背景图片，支持颜色
    
    # 底层自动识别手机的分辨率级别去 drawable_xxx 加载不同分辨率的图片

```

#### Button && ImageButton

> 按钮 && 图片按钮

``` bash

    # 共性
      - 都可以作为按钮产生一个点击效果

```







    





