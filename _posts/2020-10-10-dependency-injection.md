---
layout: post
title: 什么是依赖注入
tags: dependencyInjection
---
依赖注入讲白了
```
就是不在使用类的内部创建被使用的对象，而是通过传递被使用对象作为构造函数参数，将其注入到使用类中
```

```php
class User
{
  function __construct($storage)
  {
    $this->storage = $storage;
  }

  // ...
}
```
在上面这个例子中，`$storage`作为被使用对象注入到`User`类中
```php
$storage = new SessionStorage('SESSION_ID');
$user = new User($storage);
```

我们看一下不使用依赖注入的写法对比一下
```php
class User
{
  function __construct()
  {
    $this->storage = new SessionStorage('SESSION_ID');
  }

  // ...
}
```
##进阶，依赖注入容器
>大多数时候，我们不需要依赖注入容器就能从依赖注入中获益

那什么时候我们需要呢？当我们需要管理大量的对象和很多依赖关系的时候
```
依赖注入容器管理对象：从它们的实例化到它们的配置。
```
来看一个简单的例子，这个容器提供了如何获取一个邮件对象`getMailer()`及配置（硬编码方式）。
当使用容器时，我们只需要请求一个邮件发送器对象，**我们不需要再知道如何创建它**。

所有关于如何创建邮件发送器实例的知识现在都嵌在容器中了。由于`getMailTransport()`的调用，邮件传输依赖将由容器自动注入。
```php
class Container
{
  public function getMailTransport()
  {
    return new Zend_Mail_Transport_Smtp('smtp.gmail.com', array(
      'auth'     => 'login',
      'username' => 'foo',
      'password' => 'bar',
      'ssl'      => 'ssl',
      'port'     => 465,
    ));
  }

  public function getMailer()
  {
    $mailer = new Zend_Mail();
    $mailer->setDefaultTransport($this->getMailTransport());

    return $mailer;
  }
}
```