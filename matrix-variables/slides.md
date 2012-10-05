!SLIDE subsection
# Matrix Variables

!SLIDE small incremental bullets
# What Are They?

* Originally mentioned in <a href="http://www.w3.org/DesignIssues/MatrixURIs.html">Tim Berners-Lee post</a>
* The term is not used in RFC URI spec
* However it is most commonly used

!SLIDE small
# <a href="http://www.ietf.org/rfc/rfc2396.txt">RFC 2396</a> section 3.3
## "Each path segment may include a sequence of parameters, indicated by the semicolon ";" character. The parameters are not significant to the parsing of relativeb references."

!SLIDE small
# <a href="http://tools.ietf.org/html/rfc3986#section-3.3">RFC 3986 (section 3.3)</a>
## "The semicolon (";") and equals ("=") reserved characters are __often used to__ delimit parameters and parameter values applicable to that segment.  The comma (",") reserved character is __often used for__ similar purposes."

!SLIDE small incremental bullets
# Two Types of Usage

* As path segment name-value pairs
* <a href="http://wiki.jfrog.org/confluence/display/RTF/Using+Properties+in+Deployment+and+Resolution">JFrog API</a><br>
`/qa-releases;buildNumber=135;revision=3.2`
* As delimited list path segment
* <a href="http://api.stackexchange.com/docs/comments-on-answers">StackExchange API</a><br>
`/answers/id1;id2;id3;id4/comments`

!SLIDE small incremental bullets
# How To Use In @MVC

* If you expect ";" content in a path segment
* Represent the path segment with a URI variable
* Declare one or more `@MatrixVariable` args

!SLIDE smaller
# The Common Case

    @@@ java
    // GET /pets/42;q=11;r=22

    @RequestMapping(value = "/pets/{petId}")
    public void findPet(
        @PathVariable String petId, @MatrixVariable int q) {

      // petId == 42
      // q == 11

    }

!SLIDE smaller
# Obtain All Matrix Variables

    @@@ java
    // GET /owners/42;q=11;r=12/pets/21;q=22;s=23

    @RequestMapping(value = "/owners/{ownerId}/pets/{petId}")
    public void findPet(
        @MatrixVariable Map<String, String> matrixVars) {

        // matrixVars: ["q" : [11,22], "r" : 12, "s" : 23]

    }

!SLIDE smaller
# Qualify Path Segment

    @@@ java
    // GET /owners/42;q=11/pets/21;q=22

    @RequestMapping(value = "/owners/{ownerId}/pets/{petId}")
    public void findPet(
        @MatrixVariable(value="q", pathVar="ownerId") int q1,
        @MatrixVariable(value="q", pathVar="petId") int q2) {    
      
      // q1 == 11
      // q2 == 22

    }

!SLIDE
# References
<br>
<br>
Section on <a href="http://static.springsource.org/spring-framework/docs/3.2.0.BUILD-SNAPSHOT/reference/htmlsingle/#mvc-ann-matrix-variables">"Matrix Variables"</a>

