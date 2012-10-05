!SLIDE subsection
# Other Improvements

!SLIDE smaller bullets incremental
# `GenericHttpMessageConverter`

* Read `HttpInputMessage` to generic target type
* Supported with Jackson JSON library
* Also `Jaxb2CollectionHttpMessageConverter`

!SLIDE smaller
# `RestTemplate`
## Response with Generic Type

    @@@ java
 

    ParameterizedTypeReference<List<Integer>> listOfInts =
        new ParameterizedTypeReference<List<Integer>>() {};


    ResponseEntity<List<Integer>> result =
        restTemplate.exchange(
            "http://example.com/accounts",
            HttpMethod.GET, null, listOfInts);

!SLIDE smaller
# `@RequestBody`
## Generic Method Argument

    @@@ java

    @RequestMapping
    public void handle(@RequestBody List<Integer> ints) {
      
    }

!SLIDE smaller
# HTTP PATCH method

!SLIDE smaller
# Jackson JSON 2

!SLIDE smaller
# `JacksonObjectMapperFactoryBean`


