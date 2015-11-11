学习慕课网《Spring MVC起步》教程的笔记。
本篇文档记录简单的MVC概念，流程。还有Maven的介绍最后用一个简单的例子说明了MVC和Maven。


----------

目录
====
[TOC]

<br/>
## 1-1 课程简介

<br/>
## 1-2 前端控制器
MVC处理流程：用户请求通过HTTP协议到达**前端控制器(Front Controller)**，前端控制器寻找具体处理请求的**控制器(Controller)**，控制器调用业务逻辑的**service**，并生成了业务数据，同时**返回到前端控制器(Front Controller)**。由前端控制器把业务数据分发给**业务视图(View template)**，有业务视图呈现**最终的用户页面**。在返回到前端控制器，在返回到用户浏览器。
**前端控制器(Front Controller)：**类似分发器。
**MVC的本质：**业务数据的抽取和业务数据呈现相分离。

_前端控制器的流程_：
```sequence
# participants
participant Request
participant Front Controller
participant Controller
participant View Template
# the procedure
Request->Front Controller: Incoming Request
Front Controller->Controller: Delegate Request
Controller->Controller: Handle Request\nand\nCreate Model
Controller-->Front Controller: Delegate rendering\nof response(Model)
Front Controller->View Template: Render Response
View Template-->Front Controller: Return response
Front Controller-->Request: Return response
```

<br/>
## 1-3 MVC概念
**M** odel - **V** iew - **C** ontroller。
**View：**视图层，更关注视图的呈现，重点是数据的呈现方式与形式。
**Model：**业务层，业务数据的信息显示，数据的结构，可理解为**数据库的表**。
**Controller：**控制层，调用合适的业务逻辑产生合适的数据，再传递给视图层进行呈现。连接Model和View。
MVC是一种架构模式，也是一种思考方式。

<br/>
## 2-1 静态概念
**DispatcherServlet**：就是前面提到的**前端控制器**。如图：
```sequence
Title: 仅仅就是显示一下。
DispatcherServlet->Controller:
Controller-->DispatcherServlet:
DispatcherServlet->Model:
Model-->DispatcherServlet:
DispatcherServlet->View:
View-->DispatcherServlet:
```
+ **HandlerAdapter：**这是在DispatcherServlet内部使用的类，DispatcherServlet用过使用HandlerAdapter来调用具体的Controller。
+ **HandlerInterceptor：**拦截器，拦截的是调用Controller的请求。同时可以实现在调用Controller之前和之后添加自己的方法。
+ **HandlerMapping：**前端控制器和Controller之间的映射关系。DispatcherServlet通过HandlerMapping来寻找具体处理的Controller。
+ **HandlerExecutionChain：**链的执行是利用Java中的**反射机制**实现的。
+ **ModelAndView：** Model的具体表现形式。
+ **ViewResolver：**视图解析器。
+ **View：**呈现的页面。

<br/>
## 2-2 动态概念
就是上面的具体的工作流程。

<br/>
## 3-1 Maven介绍
Maven的重要：**POM(Project Object Model), Dependency Management, Coordinates**

## 3-2 Maven安装

## 3-3 Maven配置

## 3-4 用Maven创建项目

## 3-5 Hello Spring MVC
配置servlet.xml中，需要配置ViewResolver，配置视图解析器的功能「配置前缀和后缀」。

## 4-1 从配置文件开始
**web.xml**
在servlet.xml中`<mvc:annotation-driven/>`，可以将请求参数绑定到控制器参数中。

## 4-2 Controller基础代码
配置和编写controller，model，service，impl，resource等。

## 4-3 Controller现代方式
通过@RequestParameter方式获取参数。

## 4-4 Controller传统方式
HttpRequestServlet方式获取参数。

## 4-5 Binding
Binding(绑定)：名称匹配，页面的name属性和Model的成员变量的名称一致。
请求的参数不需要自己特定的配置，就可以映射到Controller中的参数中。也可以添加@ModelAttribute标签进行绑定。

## 4-6 FileUpload 单文件上传
配置Bean：`class="org.springframework.web.multipart.commons.CommonsMultipartResolver"`。同时还有几个属性设置。
**利用Spring实现文件的上传功能。**

## 4-7 JSON(上)
JSON(JavaScript Object Notation)：是一种轻量级的数据交换格式。
SpringMVC使用ViewReslover处理数据的不同呈现格式如HTML或JSON等。

## 4-7 JSON(中)
@ResponseBody注解表明这个返回的对象被响应所使用，*可以把对象转换成JSON格式*。

## 4-7 JSON(下)

## 5-1 总结

