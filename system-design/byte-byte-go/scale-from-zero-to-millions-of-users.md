# Scale from Zero to Millions of Users

Reference : https://bytebytego.com/courses/system-design-interview/scale-from-zero-to-millions-of-users

## 1. Single Server Setup

1. User makes a request to DNS(Domain Name System) to resolve the domain name to an IP address.
2. DNS returns the IP(Internet Protocol) address to the user's browser. (DNS is usually a paid 3rd party service and not hosted on our server)
3. Using the IP address, the browser makes a HTTP(Hypertext Transfer Protocol) request to our web server.
4. The web server processes the request and returns the response to the browser.
5. The browser renders the response and displays the website.

## 2. Single Server Setup with Caching

1. User makes a request to DNS(Domain Name System) to resolve the domain name to an IP address.
2. DNS returns the IP(Internet Protocol) address to the user's browser. (DNS is usually a paid 3rd party service and not hosted on our server)
3. The browser makes a request to the web server using the IP address.
4. The web server processes the request and returns the response to the browser. It usually contains HTML pages(HTML, CSS, JavaScript) or JSON data.
5. The browser renders the response and displays the website. (How browser renders the response? For now take a look at https://blog.logrocket.com/how-browser-rendering-works-behind-scenes/)

## 3. Database

Usually we need another server to host the database.
It sounds too much common nowadays to separate the database and the web server, but the benefit of it is that we can scale the database independently from the web server.

### Different types of databases

- Relational Database(SQL)

- NoSQL Database(Non-relational)

Usually Relational Database is the go-to for most of the developers, but in the cases below Non-relational DB can be a better choice.

- When application requires super high latency.
- Data is not structured and don't have relationships.
- Need to store massive amount of data.

## 4. Vertical Scaling vs Horizontal Scaling

Vertical scaling is the process of adding more power(CPU, RAM, etc.) to the existing server.
On the other hand, horizontal scaling is the process of adding more servers to the pool of resources.

### Pros and Cons of Vertical Scaling

- Pros:
  - Good when the traffic is not that high
    - Simple to implement
- Cons:
  - Limited by the hardware. It's impossible to add infinite amount of power to the existing server.
  - Vertical scaling doesn't have a failover and redundancy. If one server goes down, the application will be down.

### Pros and Cons of Horizontal Scaling

- Pros:
  - Better scalability.
    - No limit to the number of servers.
    -
- Cons:
  - More complex to implement.

## 5. Load Balancer

Load balancer is a server that distributes the incoming requests to the available servers.

## 6. Database Replication

Create two type s of databases:

- Master database: Only supports write operations.
- Slave database: Copy of the master database that only supports read operations.

All the data-modifying commands like insert, delete, or update must be sent to the master database.
Most applications require a much higher ratio of reads to writes; thus, the number of slave databases in a system is usually larger than the number of master databases.

### Advantages of database replication:

- Better performance: In the master-slave model, all writes and updates happen in master nodes; whereas, read operations are distributed across slave nodes. This model improves performance because it allows more queries to be processed in parallel.

- Reliability: If one of your database servers is destroyed by a natural disaster, such as a typhoon or an earthquake, data is still preserved. You do not need to worry about data loss because data is replicated across multiple locations.

- High availability: By replicating data across different locations, your website remains in operation even if a database is offline as you can access data stored in another database server.

### In case of database goes offline

- If only one slave database is available and it goes offline, read operations will be directed to the master database temporarily. As soon as the issue is found, a new slave database will replace the old one. In case multiple slave databases are available, read operations are redirected to other healthy slave databases. A new database server will replace the old one.

- If the master database goes offline, a slave database will be promoted to be the new master. All the database operations will be temporarily executed on the new master database. A new slave database will replace the old one for data replication immediately. In production systems, promoting a new master is more complicated as the data in a slave database might not be up to date. The missing data needs to be updated by running data recovery scripts.

## 7. Caching

A cache is a temporary storage that stores the results of expensive responses or frequently accessed data so that the next time the same data is requested, the data can be served from the cache instead of the original source, making the response faster.

### Cache tier (Cache layer, Cache as a service, read-through cache)

The cache tier is a temporary data store layer, much faster than the database. The benefits of having a separate cache tier include better system performance, ability to reduce database workloads, and the ability to scale the cache tier independently.

After receiving a request, a web server first checks if the cache has the available response. If it has, it sends data back to the client. If not, it queries the database, stores the response in cache, and sends it back to the client. This caching strategy is called a read-through cache

### Considerations on using cache

- Decide when to use cache.**Consider using cache when data is read frequently but modified infrequently**. Since cached data is stored in volatile memory, a cache server is not ideal for persisting data. For instance, if a cache server restarts, all the data in memory is lost. Thus, **important data should be saved in persistent data stores.**

- Expiration policy. It is a good practice to implement an expiration policy. Once cached data is expired, it is removed from the cache. When there is no expiration policy, cached data will be stored in the memory permanently. It is advisable not to make the expiration date too short as this will cause the system to reload data from the database too frequently. Meanwhile, it is advisable not to make the expiration date too long as the data can become stale.

- Consistency: This involves keeping the data store and the cache in sync. Inconsistency can happen because data-modifying operations on the data store and cache are not in a single transaction. When scaling across multiple regions, maintaining consistency between the data store and cache is challenging. For further details, refer to the paper titled “Scaling Memcache at Facebook” published by Facebook [7].

- Mitigating failures: A single cache server represents a potential single point of failure (SPOF), defined in Wikipedia as follows: “A single point of failure (SPOF) is a part of a system that, if it fails, will stop the entire system from working” [8]. As a result, multiple cache servers across different data centers are recommended to avoid SPOF. Another recommended approach is to overprovision the required memory by certain percentages. This provides a buffer as the memory usage increases.

- Eviction Policy: Once the cache is full, any requests to add items to the cache might cause existing items to be removed. This is called cache eviction. Least-recently-used (LRU) is the most popular cache eviction policy. Other eviction policies, such as the Least Frequently Used (LFU) or First in First Out (FIFO), can be adopted to satisfy different use cases.

- Redis as cache layer:https://www.youtube.com/watch?v=-5RTyEim384

## 8. Content Delivery Network (CDN)

https://qiita.com/ymd65536/items/01a2c1df61250c3f5d83
A CDN is a network of geographically dispersed servers used to deliver static content. CDN servers cache static content like images, videos, CSS, JavaScript files, etc.

1. User A tries to get image.png by using an image URL. The URL’s domain is provided by the CDN provider. The following two image URLs are samples used to demonstrate what image URLs look like on Amazon and Akamai CDNs:

https://mysite.cloudfront.net/logo.jpg

https://mysite.akamai.com/image-manager/img/logo.jpg

2. If the CDN server does not have image.png in the cache, the CDN server requests the file from the origin, which can be a web server or online storage like Amazon S3.

3. The origin returns image.png to the CDN server, which includes optional HTTP header Time-to-Live (TTL) which describes how long the image is cached.

4. The CDN caches the image and returns it to User A. The image remains cached in the CDN until the TTL expires.

5. User B sends a request to get the same image.

6. The image is returned from the cache as long as the TTL has not expired.

### Considerations on using CDN

- Cost: CDNs are run by third-party providers, and you are charged for data transfers in and out of the CDN. Caching infrequently used assets provides no significant benefits so you should consider moving them out of the CDN.

- Setting an appropriate cache expiry: For time-sensitive content, setting a cache expiry time is important. The cache expiry time should neither be too long nor too short. If it is too long, the content might no longer be fresh. If it is too short, it can cause repeat reloading of content from origin servers to the CDN.

- CDN fallback: You should consider how your website/application copes with CDN failure. If there is a temporary CDN outage, clients should be able to detect the problem and request resources from the origin.

- Invalidating files: You can remove a file from the CDN before it expires by performing one of the following operations:

  - Invalidate the CDN object using APIs provided by CDN vendors.
  - Use object versioning to serve a different version of the object. To version an object, you can add a parameter to the URL, such as a version number. For example, version number 2 is added to the query string: image.png?v=2.

- Use object versioning to serve a different version of the object. To version an object, you can add a parameter to the URL, such as a version number. For example, version number 2 is added to the query string: image.png?v=2.

## Stateful vs Stateless architecture

https://qiita.com/yutoo89/items/6b24ae9013bde35a132b#%E3%82%B9%E3%83%86%E3%83%BC%E3%83%88%E3%83%AC%E3%82%B9%E3%82%B5%E3%83%BC%E3%83%90

### Stateful architecture

User A’s session data and profile image are stored in Server 1. To authenticate User A, HTTP requests must be routed to Server 1. If a request is sent to other servers like Server 2, authentication would fail because Server 2 does not contain User A’s session data. Similarly, all HTTP requests from User B must be routed to Server 2; all requests from User C must be sent to Server 3.

The issue is that every request from the same client must be routed to the same server. This can be done with sticky sessions in most load balancers [10]; however, this adds the overhead. Adding or removing servers is much more difficult with this approach. It is also challenging to handle server failures.

### Stateless architecture

In this stateless architecture, HTTP requests from users can be sent to any web servers, which fetch state data from a shared data store. State data is stored in a shared data store(could be a relational database, Memcached/Redis, NoSQL, etc) and kept out of web servers. A stateless system is simpler, more robust, and scalable.
