# REST 

* Representational state transfer
* Set of generic principles

## Architectural constraints

* Client-server model
* Stateless - each request is standalone
* Uniform interface:
    1) Identify resource (Web: URI - resource, HTTP - communication standard)
    2) Client manipulates resources through sending representations ( eg JSON )
    3) Self-descriptive messages (content type)
    4) Hypermedia:
        uniform interface, self-contained interaction,
        gives instructions to clients -> no need to change client implementation
* Caching server resources
* Layered (proxies)
* Code on demand (`<script/>` tag)

## RPC vs REST

* RPC - remote procedure call (sending messages)
    * SOAP - simple object access protocol
    * XML-RPC, JSON-RPC
        * HTTP API context: methods in URL, arguments in query string or body

* RPC - great for actions
* REST - modeling your domain and CRUD operations (GET, POST, PUT, DELETE, OPTIONS, PATCH)


## MICROSOFT WEB API DESIGN

```
PUT -> create or update ("upsert")
PATCH -> partial update through a "patch document" (JSON Merge Patch: `applications/json-patch+json`)
Media types - resource representation
Partial responses HEAD / GET   (HEAD without the body)
API versioning: URI, header, query, **media type versioning**
OpenAPI / Swagger 2.0
```
