请求Features
================

作者： `Steve Smith`_  
翻译：  谢炀(kiler)   
校对：

涉及到如何处理特定Web服务器对于HTTP请求和响应的功能已被分解成独立的接口,这些抽象化的接口被特定服务器的实现和中间件用来创建和修改应用程序的托管管道.

.. contents:: 章节:
  :local:
  :depth: 1

Feature 接口
------------------

ASP.NET Core 定义了一系列 `HTTP功能接口 <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/index.html>`_, 提供给服务器来判断哪些功能是支持的. Web服务器的最基本的特征是能够处理请求并返回应答，通过下面定义的特征接口：

`IHttpRequestFeature <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/IHttpRequestFeature/index.html>`_
  定义HTTP请求的结构, 包括协议, 路径, 查询字符串, 请求头,还有正文.

`IHttpResponseFeature <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/IHttpResponseFeature/index.html>`_
  定义HTTP响应的结构, 包括状态码, 请求头, 响应正文.

`IHttpAuthenticationFeature <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/Authentication/IHttpAuthenticationFeature/index.html>`_
  定义了基于``ClaimsPrincipal``用户验证的支持以及指定验证处理程序.

`IHttpUpgradeFeature <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/IHttpUpgradeFeature/index.html>`_
  定义`HTTP 升级 <http://tools.ietf.org/html/rfc2616#section-14.42>`_支持, 允许客户端在服务器希望切换协议的时候能够能够指定到对应的协议.

`IHttpBufferingFeature <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/IHttpBufferingFeature/index.html>`_
  定义用于禁用请求和响应的缓冲方法.

`IHttpConnectionFeature <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/IHttpConnectionFeature/index.html>`_
  定义了本地和远程地址和端口的属性。

`IHttpRequestLifetimeFeature <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/IHttpRequestLifetimeFeature/index.html>`_
  定义用于退出的连接、或者检测到一个请求已被提前终止（如客户端中断）的支持。

`IHttpSendFileFeature <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/IHttpSendFileFeature/index.html>`_
  定义异步发送文件的方法.

`IHttpWebSocketFeature <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/IHttpWebSocketFeature/index.html>`_
  定义支持Web Sockets的API。

`IHttpRequestIdentifierFeature <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/IHttpRequestIdentifierFeature/index.html>`_
  添加属性可以实现唯一标识请求。

`ISessionFeature <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/ISessionFeature/index.html>`_
  定义``ISessionFactory``和``ISession``接口支持抽象用户会话。

`ITlsConnectionFeature <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/ITlsConnectionFeature/index.html>`_
  定义检索客户端证书的API。

`ITlsTokenBindingFeature <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/ITlsTokenBindingFeature/index.html>`_
  定义用来处理TLS token绑定参数的方法。

.. 注意:: ``ISessionFeature`` 不是一个服务器功能, 但是被``SessionMiddleware``实现了 (见 :doc:`/fundamentals/app-state`).
  
Feature集合
-------------------

`HttpContext.Features <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/HttpContext/index.html#prop-Microsoft.AspNet.Http.HttpContext.Features>`_ 属性提供用于获取和设置可用的HTTP特性为当前请求的接口。由于该特征集合是可变的，即使在一个请求中间件的上下文中可用于修改集合，并添加额外的功能的支持。property provides an interface for getting and setting the available HTTP features for the current request. Since the feature collection is mutable even within the context of a request middleware can be used to modify the collection and add support for additional features.

中间件和请求特性
-------------------------------

While servers are responsible for creating the feature collection, middleware can both add to this collection and consume features from the collection. For example, the `StaticFileMiddleware  <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/StaticFiles/StaticFileMiddleware/index.html>`__ accesses the ``IHttpSendFileFeature`` feature. If the feature exists, it is used to send the requested static file from its physical path. Otherwise, a much slower workaround method is used to send the file. When available, the ``IHttpSendFileFeature`` allows the operating system to open the file and perform a direct kernel mode copy to the network card.

Additionally, middleware can add to the feature collection established by the server. Existing features can even be replaced by middleware, allowing the middleware to augment the functionality of the server. Features added to the collection are available immediately to other middleware or the underlying application itself later in the request pipeline.

.. note:: Use the `FeatureCollectionExtensions <https://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNet/Http/Features/FeatureCollectionExtensions/index.html>`__ to easily get and set features on the ``HttpContext``.

By combining custom server implementations and specific middleware enhancements, the precise set of features an application requires can be constructed. This allows missing features to be added without requiring a change in server, and ensures only the minimal amount of features are exposed, thus limiting attack surface area and improving performance.

总结
-------

Feature接口 define specific HTTP features that a given request may support. Servers define collections of features, and the initial set of features supported by that server, but middleware can be used to enhance these features.

其他资源
--------------------

- :doc:`servers`
- :doc:`middleware`
- :doc:`owin`
