## What is rate limiter

In a network system, a rate limiter is used to control the rate of traffic sent by a client or a service. In the HTTP world, a rate limiter limits the number of client requests allowed to be sent over a specified period. If the API request count exceeds the threshold defined by the rate limiter, all the excess calls are blocked. Here are a few examples:

## What is the example usage of rate limiter

- A user can write no more than 2 posts per second.

- You can create a maximum of 10 accounts per day from the same IP address.

- You can claim rewards no more than 5 times per week from the same device.

## What are the benefits of rate limiter

### Prevent resource starvation caused by Denial of Service (DoS) attack [1].

Almost all APIs published by large tech companies enforce some form of rate limiting. For example, Twitter limits the number of tweets to 300 per 3 hours [2]. Google docs APIs have the following default limit: 300 per user per 60 seconds for read requests [3]. A rate limiter prevents DoS attacks, either intentional or unintentional, by blocking the excess calls.

### Reduce cost.

Limiting excess requests means fewer servers and allocating more resources to high priority APIs. **Rate limiting is extremely important for companies that use paid third party APIs.** For example, you are charged on a per-call basis for the following external APIs: check credit, make a payment, retrieve health records, etc. Limiting the number of calls is essential to reduce costs.

### Prevent servers from being overloaded.

To reduce server load, a rate limiter is used to filter out excess requests caused by bots or users’ misbehavior.

## Where to implement rate limiter, server-side or client-side or middleware

### Server-side rather than client-side

Intuitively, you can implement a rate limiter at either the client or server-side.
Generally speaking, client is an unreliable place to enforce rate limiting because client requests can easily be forged by malicious actors. Moreover, we might not have control over the client implementation.
If we are to implement a server-side rate limiter, we can place it at the API gateway or in the application code.

### Middleware (example: API Gateway)

Alternatively, we can implement a rate limiter as middleware between the client and the server.
Cloud microservices have become widely popular and rate limiting is usually implemented within a component called API gateway. API gateway is a fully managed service that supports rate limiting, SSL termination, authentication, IP whitelisting, servicing static content, etc. For now, we only need to know that the API gateway is a middleware that supports rate limiting.

**API Gateway:**
Client -> [Rate Limiting + Other Features(SSL termination, authentication, IP whitelisting, etc.)] -> Backend

**Dedicated Middleware:**
Client -> [Rate Limiting Only] -> API Gateway -> Backend

#### [Optional] Rate Limiting in AWS

For rate limiting specifically, AWS doesn't have a dedicated middleware service named "rate limiter". Instead, rate limiting can be implemented using various AWS services:

**WAF (Web Application Firewall)**

- Can create rate-based rules
- Works with CloudFront and API Gateway
- Can block IPs that exceed rate limits

**AWS Shield**

- DDoS protection service
- Includes some rate limiting capabilities
- More focused on security than general rate limiting

**Custom Implementation Options:**

- Using Amazon ElastiCache (Redis) for distributed rate limiting
- Using DynamoDB for tracking request counts
- Lambda functions to implement custom rate limiting logic

```
Client Request
↓
[CloudFront]
↓
[AWS WAF (Rate Rules)]
↓
[API Gateway (Throttling)]
↓
[Your Application]
```

While designing a rate limiter, an important question to ask ourselves is: where should the rate limiter be implemented, on the server-side or in a gateway? There is no absolute answer. It depends on your company’s current technology stack, engineering resources, priorities, goals, etc. Here are a few general guidelines:

- Evaluate your current technology stack, such as programming language, cache service, etc. Make sure your current programming language is efficient to implement rate limiting on the server-side.

- Identify the rate limiting algorithm that fits your business needs. When you implement everything on the server-side, you have full control of the algorithm. However, your choice might be limited if you use a third-party gateway.

- If you have already used microservice architecture and included an API gateway in the design to perform authentication, IP whitelisting, etc., you may add a rate limiter to the API gateway.

- Building your own rate limiting service takes time. If you do not have enough engineering resources to implement a rate limiter, a commercial API gateway is a better option.

## What are the algorithms for rate limiting

Rate limiting can be implemented using different algorithms, and each of them has distinct pros and cons. Even though this chapter does not focus on algorithms, understanding them at high-level helps to choose the right algorithm or combination of algorithms to fit our use cases. Here is a list of popular algorithms:

- Token bucket(widely used)

- Leaking bucket

- Fixed window counter

- Sliding window log

- Sliding window counter

## What do we have to care in high-level

**At the high-level, we need a counter to keep track of how many requests are sent from the same user, IP address, etc. If the counter is larger than the limit, the request is disallowed.**

### Where to store the counter?

- Using the database is not a good idea due to slowness of disk access
- In-memory cache is chosen because it is fast and supports time-based expiration strategy. For instance, Redis [11] is a popular option to implement rate limiting. It is an in-memory store that offers two commands: INCR and EXPIRE

### How are rate limiting rules created?

Lyft open-sourced their rate-limiting component. They are good examples to learn from.

```yaml
domain: messaging
descriptors:
  - key: message_type
    value: marketing
    rate_limit:
      unit: day
      requests_per_unit: 5
```

In the above example, the system is configured to allow a maximum of 5 marketing messages per day. Here is another example:

```yaml
domain: auth
descriptors:
  - key: auth_type
    value: login
    rate_limit:
      unit: minute
      requests_per_unit: 5
```

This rule shows that clients are not allowed to login more than 5 times in 1 minute.

### Where are the rules stored?

Rules are generally written in configuration files and saved on disk.

### What do we do when request exceeds the limit?

- **APIs return a HTTP response code 429 (too many requests) to the client.**
- **Depending on the use cases, we may enqueue the rate-limited requests to be processed later.** For example, if some orders are rate limited due to system overload, we may keep those orders to be processed later.
