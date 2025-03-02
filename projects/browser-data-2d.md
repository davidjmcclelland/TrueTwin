---
icon: unity
---

# Browser Data 2D (Unity)

The ability to use Unity to invoke Javascript calls in a browser is not trivial to set up. Once working, it is a good idea to treat it as an API. I recommend using strict naming conventions to facilitate building on a foundation. Use Objects to convey commands and properties back and forth in a single consistent payload.

### OpenAPI block

GitBook's OpenAPI block is powered by [Scalar](https://scalar.com/), so you can test your APIs directly from your docs.

{% openapi src="https://petstore3.swagger.io/api/v3/openapi.json" path="/pet" method="post" %}
[https://petstore3.swagger.io/api/v3/openapi.json](https://petstore3.swagger.io/api/v3/openapi.json)
{% endopenapi %}
