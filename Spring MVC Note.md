# Spring MVC Servlet
![image](https://github.com/optor666/spring-webmvc-5.3.18-examples/assets/32811372/be7c6889-3a23-4459-a847-9dc6c4bd4bfe)

## HttpServletBean
HttpServletBean 直接继承自 Java 的 HttpServlet，其作用是将 Servlet 中配置的参数设置到相应的属性；

## FrameworkServlet
FrameworkServlet 初始化了 WebApplicationContext；

## DispatcherServlet
DispatcherServlet 初始化了自身的 9 个组件；

# Spring MVC 核心概念
1. Handler: 处理器，直接对应着 MVC 中的 C，也就是 Controller 层。它的具体表现形式有很多，可以是类，也可以是方法，如果你能想到别的表现形式
   也可以使用，它的类型是 Object。标注了 @RequestMapping 的所有方法都可以看成一个 Handler。只要可以实际处理请求就可以是 Handler。
2. HandlerMapping: 用来查找 Handler 的。接收到一个请求后，使用哪个 Handler 来处理呢？这就是 HandlerMapping 要做的事情。
3. HandlerAdapter: Handler 的适配器。因为 Spring MVC 中的 Handler 可以是任意的形式，只要能处理请求就 OK，但是 Servlet 需要处理方法的
   结构是固定的，都是以 request 和 response 为参数的方法（如 doService 方法）。怎么让固定的 Servlet 处理方法调用灵活的 Handler 来进行处理呢？
   这就是 HandlerAdapter 要做的事情。在九大组件中 HandlerAdapter 是最复杂的。
4. View 和 ViewResolver 的原理与 Handler 和 HandlerMapping 的原理类似。View 是用来展示数据的，而 ViewResolver 用来查找 View。
   View 可以说是展示数据的模板，内容就是 Model 里面的数据。

# 请求处理流程
1. HttpServlet#service(ServletRequest req, ServletResponse res)
2. FrameworkServlet#service(HttpServletRequest req, HttpServletResponse resp)
3. HttpServlet#service(HttpServletRequest req, HttpServletResponse resp)
4. FrameworkServlet#doGet(HttpServletRequest req, HttpServletResponse resp)
5. FrameworkServlet#processRequest(HttpServletRequest req, HttpServletResponse resp)
6. DispatcherServlet#doService(HttpServletRequest req, HttpServletResponse resp)
7. DispatcherServlet#doDispatch(HttpServletRequest req, HttpServletResponse resp)
```java
class DispatcherServlet {
    public void doDispatch(HttpServletRequest req, HttpServletResponse resp) {
        // Determine handler for the current request. ① 根据 Request 找到 Handler
        HandlerExecutionChain mappedHandler = getHandler(processedRequest);
        // Determine handler adapter for the current request. ② 根据 Handler 找到对应的 handlerAdapter
        HandlerAdapter ha = getHandlerAdapter(mappedHandler.getHandler());
        // Actually invoke the handler. ③ 用 HandlerAdapter 处理 Handler
        ModelAndView mv = ha.handle(processedRequest, response, mappedHandler.getHandler());
        // ④ 调用 processDispatchResult 方法处理上面处理之后的结果（包含找到 View，并渲染输出给用户）
        processDispatchResult(processedRequest, response, mappedHandler, mv, dispatchException);
    }
}
```
8. 请求处理流程图（左边是 Interceptor 相关方法的调用位置、中间是 doDispatch 处理流程图、右边是 doDispatch 方法处理过程中所涉及的组件):
![image](https://github.com/optor666/spring-framework/assets/32811372/475ee244-e796-453c-88d3-505f8fe8c6a1)
![image](https://github.com/optor666/spring-framework/assets/32811372/b0fbad3f-dda3-47b0-83bb-596bf469234e)
![image](https://github.com/optor666/spring-framework/assets/32811372/53eb24ac-969b-44a0-b738-87effab6a115)



