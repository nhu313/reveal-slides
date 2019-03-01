# Intro to the Web

-

## What is a Server?
A server is a computer program or a device that provides functionality for other programs or devices (aka clients).

-
### What is REST?

- REST stands for **RE**presentational **S**tate **T**ransfer
* It is an architectural style that defines a set of constraints and properties based on HTTP
* It relies on a stateless, client-server, cacheable communications protocol (usually HTTP)

-

# What is REST?
* Uses HTTP verbs to get and modify data
* resources being identified by an identifier (URL)
  * `GET /user/123`

-
### Client-Server

- Concerns should be separated between clients and servers. This enables client and server components to evolve independently and in turn allows the system to scale.

-
### Stateless

- The communication between client and server should be stateless. The server need not remember the state of the client. Instead, clients must include all of the necessary information in the request so that server can understand and process it.


-
### Layered System

- Multiple hierarchical layers such as gateways, firewalls, and proxies can exist between client and server. Layers can be added, modified, reordered, or removed transparently to improve scalability.

-
### Cache

- Responses from the server must be declared as cacheable or non-cacheable. This would allow the client or its intermediary components to cache responses and reuse them for later requests. This reduces the load on the server and helps improve the performance.


-
### Uniform Interface

- All interactions between client, server, and intermediary components are based on the uniformity of their interfaces.
- This simplifies the overall architecture as components can evolve independently as long as they implement the agreed-on contract

-
### Code on Demand

- Clients can extend their functionality by downloading and executing code on demand. Examples include JavaScript scripts, Java applets, Silverlight, and so on. This is an optional constraint.

-
### URI

- Uniform Resource Identifier, or URI, for uniquely identifying resources.
- **Format:** `scheme:scheme-specific-part`
- E.g.: `http://zipcoder.io`

-
### URI Templates

- Resource links can be dynamic
- E.g.: "http://blog.zipcoder.io/**year**/posts"

-
### Representation

- RESTful resources are abstract entities, which represent a snap shot of data at a point in time.

-
-
# HTTP Methods

-
### HTTP `GET` Method

The GET method is used to retrieve information from the given server using a given URI. Requests using GET should only retrieve data and should have no other effect on the data.

-
### Idempotence

An operation is considered to be idempotent if it produces the same server state whether we apply it once or any number of times. HTTP methods such as `GET`, `HEAD` (which are also safe), `PUT`, and `DELETE` are considered to be idempotent, guaranteeing that clients can repeat a request and expect the same effect as making the request once.

-
### HTTP `POST` Method

A `POST` request is used to send data to the server, for example: customer information, file upload, etc. using HTML forms.

-
### HTTP `HEAD` Method

Same as `GET`, but transfers the status line and header section only.

-
### HTTP `PUT` Method

Replaces all current representations of the target resource with the uploaded content.

-
### HTTP `DELETE` Method

Removes all current representations of the target resource given by a URI.

-
-
# CRUD

|||
|-|-|
|Create|Read|
|Update|Delete|
|||

-
-
### HTTP Status Codes

- 1xx Informational
  - 100 Continue
- 2xx Success
  - 200 OK
- 3xx Redirection
  - 300 Multiple Choices
- 4xx Client Error
  - 400 Bad Request
- 5xx Server Error
  - 500 Internal Server Error

-
#### 1xx Informational

- 100 Continue -  
The server has received the request headers; the client should proceed to send the request body (for requests which require a body to be sent; eg: a [POST](https://en.wikipedia.org/wiki/POST_(HTTP%29) request).
- 101 Switching Protocols –  
The requester has asked the server to [switch protocols](https://en.wikipedia.org/wiki/HTTP/1.1_Upgrade_header) and the server is acknowledging that it will do so
- 102 Processing -  
As a WebDAV request may contain many sub-requests involving file operations, it may take a long time to complete the request. Indicates that the server has received and is processing the request, but no response is available yet

-
#### 2xx Success

- 200 OK
  - Standard response for successful HTTP requests.
- 201 CREATED
  - Request has been fulfilled and resulted in a new resource being created.
- 202 Accepted
  - Request has been accepted for processing, but the processing has not been completed. The request might or might not eventually be acted upon, as it might be disallowed when processing actually takes place.

-
#### 3xx Redirection

- 300 Multiple Choices
  - Indicates multiple options for the resource that the client may follow.
- 301 Moved Permanently
  - This and all future requests should be directed to the given URI
- 308 Permanent Redirect
  - The request, and all future requests should be repeated using another URI.

-
#### 4xx Client Error

- 400 Bad Request
  - The server cannot or will not process the request due to something that is perceived to be a client error

- 401 Unauthorized
  - Similar to 403 Forbidden, but specifically for use when authentication is required and has failed or has not yet been provided.
- 404 Not Found
  - The requested resource could not be found but may be available again in the future. Subsequent requests by the client are permissible

-
-
### WEB Socket

A protocol providing full-duplex communication channels over a single TCP connection.

-
### Servlet

A **servlet** is a small Java program that runs within a Web server. **Servlets** receive and respond to requests from Web clients, usually across HTTP, the HyperText Transfer Protocol.

-
-
## Spring Data JPA
- improves the implementation of data access layers by writing the boiler plate for you
