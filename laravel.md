---
title: git
category: tool
date:
tags:
---

``` bash

    # public/index.php
      bootstrap
        autoload:composer
        app __construct($basePath)
          register base bindings
            - app       => $this
            - container => $this
          register base service providers
          set base path

      app => kernel
               handle => responce4794
                           send


Container
  aliases   = [];   # save alias name
  instances = [];   # save instance
  bindings  = [];

  # 在容器中注册一个已存在的实例
  instance($abstract = [abstract => alias], $instance)
  # 调用服务提供者(ServiceProvider)的 register 和 boot 注册一个服务到容器
  register($provider, $option = [], $force = false) # force 强制
  # resolve  解析
  # compiles 编译
  singleton => bind
  bind 

ServiceProvider
  - app    # Object  应用实例
  - defer  # Boolean 是否延迟加载

```

<!-- more -->
