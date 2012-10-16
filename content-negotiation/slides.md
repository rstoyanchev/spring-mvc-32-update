!SLIDE subsection
# Content Negotiation Strategies

!SLIDE small incremental bullets
# Prior to Spring 3.2

* `@ResponseBody` used `'Accept'` header
* `@RequestMapping(produces="")` did likewise
* While `ContentNegotiatingViewResolver` ...
* offered many additional options

!SLIDE small incremental bullets
# `ContentNegotiationStrategy`
## (Spring 3.2)

* By `'Accept'` Header
* By URL extension (.xml, .json, etc)
* By Request parameter, i.e. `/accounts/1?format=json`
* Fixed content type, i.e. a fallback option

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
See section on [Configuring Content Negotiation](http://static.springsource.org/spring-framework/docs/3.2.0.BUILD-SNAPSHOT/reference/htmlsingle/#new-in-3.2-webmvc-content-negotiation) in reference docs
<br>
URL extension for content negotiation in [Spring MVC Showcase](https://github.com/springsource/spring-mvc-showcase)



