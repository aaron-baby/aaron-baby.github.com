---
layout: post
title: 三种调用DI服务的方法
tags: Phalcon 技术
---
## {{page.title}} ##
从容器中获取服务，最直观的一种就是直接调用get方法

    <?php $request = $di->get("request");

或者通过魔术方法get*Service_name*的方式

    <?php
    $request = $di->getRequest();

也可以使用取数组元素的语法

    <?php
    $request = $di['request'];