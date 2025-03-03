## Auto-incrementing ID in a traditional database does not work in a distributed system

- We're going for distributed system rather than a single server, following reasons:

  - Scalability: They can handle larger workloads by adding more machines rather than upgrading a single server.
  - Fault Tolerance: If one node fails, others can continue operating, preventing system-wide failures.
  - Performance: They can process requests in parallel and serve users from geographically closer locations.

- And it's difficult to use auto-incrementing ID in a distributed system because:
  - Coordinating unique ID generation across multiple databases is complex
  - There are potential delays and synchronization issues

## What are the characteristics of unique id?

- Unique
- Sortable

## For each new record, does ID increment by 1?

- No, it doesn't.
- It's not a good idea to use auto-incrementing ID in a distributed system.(As mentioned above)
- The ID increments by time but not necessarily only increments by 1. IDs created in the evening are larger than those created in the morning on the same day.

## Do IDs only contain numerical values?

- No, it doesn't.
- IDs can contain alphanumeric values.

## What is the ID length requirement?

- IDs should fit into 64-bit.

## What is the ID generation frequency?

- IDs should be generated at a rate of 1 million per second.

## Architecture

### 1. UUID

- Pros:

  - Generating UUID is simple. No coordination between servers is needed so there will not be any synchronization issues.

  - The system is easy to scale because each web server is responsible for generating IDs they consume. ID generator can easily scale with web servers.

- Cons:

  - IDs are 128 bits long, but our requirement is 64 bits.

  - IDs do not go up with time.
  - IDs could be non-numeric.

### 2. Snowflake

- Divide 64-bit into 4 parts:

  - 1 bit: Sign bit
    - It's always 0 and potentially used for future extension, like to distinguish between signed and unsigned numbers.
  - 41 bits: Timestamp
    - The timestamp is the number of milliseconds since the epoch (January 1, 2015).
  - 10 bits: Data center ID
    - The data center ID is the ID of the data center where the ID is generated.
  - 12 bits: Worker ID
    - The worker ID is the ID of the worker where the ID is generated.
  - 12 bits: Sequence number
    - The sequence number is the sequence number of the ID.

- Pros:

  - IDs are 64 bits long.
  - IDs go up with time.
  - IDs are numeric.
