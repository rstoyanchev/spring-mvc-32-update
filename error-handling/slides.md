!SLIDE subsection
# Error reporting in REST scenarios

!SLIDE small incremental bullets
# Traditional Web vs REST API

* In traditional, easy to present an error page
* In REST API more varied responses
* Communicate with status codes
* Commonly write helpful details to response body

!SLIDE small incremental bullets
# What Is Needed?

* Application-specific, application-wide strategy to write details to the response body
* Including standard (internal) Spring MVC exceptions
* Global `@ExceptionHandler`
* Some alternative to `DefaultHandlerExceptionResovler`

!SLIDE small incremental bullets
# Global `@ExceptionHandler` Methods
 
* `@ControllerAdvice` component annotation
* with `@ExceptionHandler` methods
* also `@InitBinder` and `@ModelAttribute`
* Useful for global exception handling, `DataBinder` initialization, and pre-handling
* Nothing to configure, just declare `@ControllerAdvice`

!SLIDE small incremental bullets
# `ResponseEntityExceptionHandler`

* Alternative to `DefaultHandlerExceptionResolver`
* Makes it easy to write error details to the response body
* By overriding protected methods

!SLIDE small incremental bullets
# Servlet Container Error Page

* HTML formatted error page
* For response status codes 4xx and 5xx
* Or with `response.sendError(int, String)`

!SLIDE small incremental bullets
# Custom Error Page (Servlet 3+)

* `error-page` in web.xml
* Don't map to exception type or status
* Location only (JSP page, even controller URL)
* Status and message available in request attributes `"javax.servlet.error.status_code"` `"javax.servlet.error.message"`

!SLIDE
# References

See updated section on <a href="http://static.springsource.org/spring-framework/docs/3.2.0.BUILD-SNAPSHOT/reference/htmlsingle/#mvc-exceptionhandlers">"Exception Handling"</a>









