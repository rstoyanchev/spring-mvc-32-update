!SLIDE subsection
# Servlet 3 Async Support

!SLIDE smaller bullets incremental
# HTTP Request-Response Semantics

* Client makes a request
* Server handles it and responds

!SLIDE smaller bullets incremental
# Ajax Requests

* Obtain new data without reloading entire page
* Pages appear more dynamic and live
* Still the same request-response semantics

!SLIDE smaller bullets incremental
# Varying Degrees of "Live"-ness

* Sometimes okay for client to poll every few minutes
* Mail, Twitter, even "breaking" news 
* In other cases, it's just not real-time enough
* Chat, collaboration, trading/finance

!SLIDE smaller bullets incremental
# Long Polling

* Client sends request and waits...
* Server holds and doesn't respond until new data arrives
* Client sends request and waits...
* Server holds and doesn't respond until new data arrives
* and so on

!SLIDE smaller bullets incremental
# Long Polling Effect

* Simulates server-side push
* In most cases more effective than polling while using identical HTTP request-response semantics
* However requests remain open for much longer

!SLIDE smaller bullets incremental
# Servlet Containers

* Traditionally thread-per-request
* Long polling would quickly exhaust container threads
* Hence the need for Servlet 3 async support

!SLIDE small
# Servlet Thread Model

      [Servlet Thread]
          Start processing
          Do some work 
          Send response

!SLIDE small
# Servlet 3 Async Thread Model

      [Servlet Thread]
          Start processing
          Switch to async mode
          Exit thread leaving response open

      
      
      
    
      
        
        
      .

!SLIDE small
# Servlet 3 Async Thread Model

      [Servlet Thread]
          Start processing
          Switch to async mode
          Exit thread leaving response open

      [Application Thread]
          Produce or receive result
          Dispatch to container to resume processing
    



      .

!SLIDE small
# Servlet 3 Async Thread Model

      [Servlet Thread]
          Start processing
          Switch to async mode
          Exit thread leaving response open

      [Application Thread]
          Produce or receive result
          Dispatch to container to resume processing
    
      [Servlet Thread]
          Start processing
          Process result from application thread
          Send response

!SLIDE small bullets incremental
# Why Not Send Response From Application Thread?

* We tried that in milestone 1
* HttpServletRequest not usable in non-container thread
* Cannot forward (e.g. no JSP rendering) or rely on various other request properties
* Response should really be finalized within container

!SLIDE 
# Servlet 3 Async Support<br> in Spring MVC

!SLIDE small bullets incremental
# `@RequestMapping` return values

* `java.util.concurrent.Callable`
* `DeferredResult`
* `AsyncTask`

!SLIDE small bullets incremental
# java.util.concurrent.Callable

* Produce value from `@RequestMapping` asynchronously
* In thread __managed by__ Spring MVC
* Long-running DB job, 3rd party REST API call, ...

!SLIDE small bullets incremental
# DeferredResult

* Produce value from `@RequestMapping` asynchronously
* In thread __managed outside__ Spring MVC 
* JMS or AMQP listener, another HTTP request

!SLIDE small bullets incremental
# AsyncTask

* Same as returning `Callable` with extras
* Override timeout value for async processing
* Select specific `AsyncTaskExecutor`

!SLIDE
# Demo

## _Async request execution and log output_

[Spring MVC Showcase](https://github.com/springsource/spring-mvc-showcase)

!SLIDE small bullets incremental
# Exceptions From `Callable`

* Saved and handled after the dispatch
* Through the `HandlerExceptionResolver` mechanism
* Like any exception from `@RequestMapping` methods

!SLIDE small bullets incremental
# Exceptions with `DeferredResult`

* `DeferredResult` provides `setErrorResult(Object)`
* Set an Exception or some alternative error value
* Exception handled after the dispatch
* Through the `HandlerExceptionResolver` mechanism

!SLIDE small bullets incremental
# Servlet Filters

* Must have the `async-supported` flag in web.xml
* Can be executed from more than one thread
* `OncePerRequestFilter` (+ all Spring MVC filters)<br> have been updated

!SLIDE small bullets incremental
# Handler Interception

* `AsyncHandlerInterceptor`
* Intercept handler execution in container threads
* `afterConcurrentHandlingStarted` vs `postProcess`/`afterCompletion`

!SLIDE small bullets incremental
# Configuring Async Support

* MVC Java Config<br> `WebMvcConfigurer.configureAsyncSupport`
* MVC namespace<br> `async-support` sub-element of `annotation-driven`

!SLIDE small bullets incremental
# What Can Be Configured?

* Async timeout value (milliseconds)
* `AsyncTaskExecutor` for `Callable` processing

!SLIDE small bullets incremental
# `web.xml` Configuration

* `async-supported` flag on all Filters and Servlet
* `dispatcher-type` of `ASYNC` for Filters
* Can be a bit repetitive

!SLIDE small bullets incremental
# `WebApplicationInitializer`
## Abstract Class Hierarchy

* Servlet 3+ Java-based, container initialization
* Registers a DispatcherServlet
* Takes care of boilerplate
* Sets `async-supported` flag and `dispatcher-type`

!SLIDE smaller

    @@@ java
    public class DispatcherServletInitializer extends
          AbstractAnnotationConfigDispatcherServletInitializer {

      protected Class<?>[] getRootConfigClasses() {
        return new Class<?>[] { RootConfig.class };
      }

      protected Class<?>[] getServletConfigClasses() {
          return new Class<?>[] { WebMvcConfig.class };
      }

      protected String[] getServletMappings() {
          return new String[] { "/" };
      }

      protected Filter[] getServletFilters() {
          return new Filter[] { new OpenSessionInViewFilter() };
      }

    }

!SLIDE
# References
<br>
Async tab in [Spring MVC Showcase](https://github.com/springsource/spring-mvc-showcase)
<br>
[Chat Sample](https://github.com/rstoyanchev/spring-mvc-chat)
<br>
[Spring AMQP Stocks](https://github.com/SpringSource/spring-amqp-samples/tree/spring-mvc-async)
<br>
[Blog series](http://blog.springsource.org/2012/05/06/spring-mvc-3-2-preview-introducing-servlet-3-async-support/)



