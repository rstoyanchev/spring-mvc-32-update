!SLIDE subsection
# Spring MVC Test Framework

!SLIDE small bullets incremental
# `MockHttpServletRequest/Response`

* Stub implementations
* `spring-test` module
* Very commonly used in controller unit tests

!SLIDE small bullets incremental
# Better Controller Unit Tests

* Take existing controller unit tests
* Invoke controllers through `DispatcherServlet`
* Using fluent API
* Based on actual Spring MVC configuration
* Without a Servlet container

!SLIDE small
# Example
 
    @@@ java

    mockMvc.perform(get("/foo").accept("application/json"))
      .andExpect(status().isOk())
      .andExpect(content().mimeType("application/json"))
      .andExpect(jsonPath("$.name").value("Lee"));

!SLIDE

Tests in [Spring MVC Showcase](https://github.com/SpringSource/spring-mvc-showcase/tree/master/src/test/java/org/springframework/samples/mvc)
<br>
<br>
[Client](https://github.com/SpringSource/spring-framework/tree/master/spring-test-mvc/src/test/java/org/springframework/test/web/mock/client/samples) and [Server](https://github.com/SpringSource/spring-framework/tree/master/spring-test-mvc/src/test/java/org/springframework/test/web/mock/servlet/samples) sample tests in the Spring Framework 
<br>
<br>
[Testing Web Applications with Spring 3.2](http://www.springone2gx.com/conference/washington/2012/10/session?id=27664)

(Thursday 10:15)


