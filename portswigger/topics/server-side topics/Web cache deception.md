https://portswigger.net/web-security/web-cache-deception

----
# Web caches

A web cache is a system that sits between the origin server and the user. 

When a client requests a static resource, the request is first directed to the cache. 

If the cache doesn't contain a copy of the resource (known as a cache miss), the request is forwarded to the origin server, which processes and responds to the request. 

The response is then sent to the cache before being sent to the user. The cache uses a pre-configured set of rules to determine whether to store the response.

When a request for the same static resource is made in the future, the cache serves the stored copy of the response directly to the user (known as a cache hit).

Caching has become a common and crucial aspect of delivering web content, particularly with the widespread use of Content Delivery Networks (`CDNs`), which use caching to store copies of content on distributed servers all over the world. 

`CDNs` speed up delivery by serving content from the server closest to the user, reducing load times by minimizing the distance data travels.

