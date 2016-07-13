#Chapter 1
##REST - What You Didn't Know

###Topics
* A brief history of REST
* REST with HTTP
* RESTFUL versus SOAP-based Services
* Taking advantage of existing infrastructure

###Principle 1 - everything is a resource
Data is a specific format, not a file. image/jpeg, video/mpg, text/html. 

###Principle 2 - each resource is identifable by a unique identifier
URI keeps data self-descriptive. Make it human-readable. Examples:

* http://www.mydatastore.com/images/vacation/2014/summer
* http://www.mydatastore.com/videos/vacation/2014/winter
* http://www.mydatastore.com/data/documents/balance?format=xml 
*  http://www.mydatastore.com/data/archives/2014

###Principle 3 - use the standard HTTP methods
* GET
* PUT
* POST
* DELETE

###Principle 4 - resources can have multiple representations
REST endpoints if supported can take multiple formats like xml and json

###Principle 5 - communicate statelessly
All modifications should be carried out in HTTP request in isolation. After the request execution, the resource is left in a final state, no partial updates. (B.L: This is not pragmatic IMO, you are going to need to do partial updates)

###Separation of the representation and the resource
Caller responsible to set the content-type header of http request. Server responsibility to return HTTP status code in the right format.

* HTTP 200 OK in the case of success
* HTTP 400 Bad requst if a unsupported content type is requested, or for any other invalid request
* HTTP 500 Internal Server error when something unexpected happens during the request processing

Example request
```
   GET /data/balance/22082014 HTTP/1.1
   Host: my-computer-hostname
   Accept: application/json
```

Example response:
```
HTTP/1.1 200 OK
   Content-Type: application/json
   Content-Length: 120
   {
    "balance": {
       "date": "22082014",
       "Item": "Sample item",
       "price": {
         "-currency": "EUR",
         "#text": "100"
       }
   } 
}
```

###Visibility

* HTTP method is safe when provided the request, it doesn't modify or cause side effects on state of resource
* HTTP method is idempotent if response is always the same no matter how many times it is requested

HTTP Method  | Safe | Idempotent |
:-----------:|:----:|:----------:|
GET 	     | Yes  | Yes        |
POST         | No   | No         |
PUT          | No   | No         |
DELETE       | No   | No         |

###Scalability and performance

Scalability accomplished by REST in best-case scenario would just require you to put another piece of hardware for your load balancer. This is different from performance which is measured by the time needed for a single request to be process, but related to the total number of requests an app can handle.

###Working with WADL

XML description of the interface of the service. It is described using resource elements. Each resource contains param elements to describe the inputs and method elements which describe the request and response
[Wiki for WADL](https://en.wikipedia.org/wiki/Web_Application_Description_Language)


