!SLIDE subsection
# Content Negotiation Strategies

!SLIDE small incremental bullets
# Prior to Spring 3.2

* `@ResponseBody` used `'Accept'` header
* `@RequestMapping(produces="")` did too
* While `ContentNegotiatingViewResolver` ...
* offered many additional options

!SLIDE small incremental bullets
# `ContentNegotiationStrategy`
## (Spring 3.2)

* `'Accept'` Header
* URL extension .xml, .json, etc
* Request parameter `/accounts/1?format=json`
* Fixed, i.e. a fallback option

!SLIDE small incremental bullets
# `ContentNeogitationManager`

* Configured with one or more instances of `ContentNegotiationStrategy`
* Plugged into various places
* `RequestMappingHandlerMapping` `RequestMappingHandlerAdapter` `ExceptionHandlerExceptionResolver`
* `ContentNegotiatingViewResolver`

!SLIDE small incremental bullets
# Default Settings
## (__without__ MVC Java Config & Namespace)

* `'Accept'` header only
* Matches existing defaults for `@ResponseBody`

!SLIDE small incremental bullets
# MVC Java Config & Namespace

* Path extension 1st, `'Accept'` header 2nd
* `.json`, `.xml` auto-registered if libraries present
* Matches defaults of `ContentNegotiatingViewResolver`

!SLIDE

# References
<br>
<br>
See section on <a href="http://static.springsource.org/spring-framework/docs/3.2.0.BUILD-SNAPSHOT/reference/htmlsingle/#new-in-3.2-webmvc-content-negotiation">"Configuring Content Negotiation"</a>



