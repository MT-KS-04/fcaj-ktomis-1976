---
title: "Week 3 Worklog"
date: 2026-05-18
weight: 3
chapter: false
pre: " <b> 3.1. </b> "
---

### Week 3 Goals:

- Learn about NoSQL databases with Amazon DynamoDB and caching with ElastiCache.
- Understand content delivery with CloudFront and edge computing with Lambda@Edge.
- Reinforce advanced networking knowledge and build highly available web applications.

### Activities Implemented During the Week:

| Day | Activities                                                                                                                                                                                                                                                                                          | Start Date | Completion Date | Reference                          |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ---------------------------------- |
| 2   | - Explored Amazon DynamoDB: <br>&emsp; + Table, Item, Attribute <br>&emsp; + Partition key, Sort key <br>&emsp; + Capacity mode (On-Demand / Provisioned) <br>&emsp; + GSI, LSI <br> - **Hands-on:** <br>&emsp; + Created a table with AWS CLI <br>&emsp; + Performed put-item, get-item operations | 18/05/2026 | 18/05/2026      | <https://000060.awsstudygroup.com> |
| 3   | - Explored Amazon ElastiCache: <br>&emsp; + Redis and Memcached engines <br>&emsp; + Cache-aside model <br>&emsp; + The role of caching in reducing database load <br> - **Hands-on:** <br>&emsp; + Created an ElastiCache cluster                                                                  | 19/05/2026 | 19/05/2026      | <https://000061.awsstudygroup.com> |
| 4   | - Explored Amazon CloudFront: <br>&emsp; + Edge Location <br>&emsp; + Distribution, Origin <br>&emsp; + Cache behavior, TTL <br> - **Hands-on:** <br>&emsp; + Created a distribution with an S3 origin <br>&emsp; + Created an invalidation to refresh the cache                                    | 20/05/2026 | 20/05/2026      | <https://000094.awsstudygroup.com> |
| 5   | - Explored Lambda@Edge: <br>&emsp; + The concept of edge computing <br>&emsp; + The 4 trigger types (viewer/origin request & response) <br> - **Hands-on:** <br>&emsp; + Reviewed an example function that customizes the response                                                                  | 21/05/2026 | 21/05/2026      | <https://000130.awsstudygroup.com> |
| 6   | - Networking on AWS Workshop: <br>&emsp; + Reviewed VPC, subnet, routing <br>&emsp; + Advanced networking scenarios <br> - **Hands-on:** <br>&emsp; + Configured networking following the workshop guide                                                                                            | 22/05/2026 | 22/05/2026      | <https://000092.awsstudygroup.com> |
| 7   | - Building Highly Available Web Applications: <br>&emsp; + Combined multiple AZs <br>&emsp; + Auto Scaling and load balancing <br> - **Hands-on:** <br>&emsp; + Built a highly available web architecture <br> - Summarized the Explore phase knowledge                                             | 23/05/2026 | 23/05/2026      | <https://000101.awsstudygroup.com> |

### Achievements During Week 3:

- Learned about the NoSQL database Amazon DynamoDB:
  - Distinguished partition key and sort key
  - Understood On-Demand and Provisioned capacity modes
  - The role of GSI and LSI when querying by other fields
  - Manipulated data via CLI: create-table, put-item, get-item
  - Understood that table design must start from the access pattern

- Understood the role of caching with Amazon ElastiCache:
  - Distinguished Redis and Memcached
  - The cache-aside model
  - How caching reduces database load and speeds up queries

- Learned how to distribute content with Amazon CloudFront:
  - The role of the Edge Location network
  - Configured distribution, origin, cache behavior
  - Understood TTL and how to use invalidation to refresh content

- Understood the concept of edge computing with Lambda@Edge:
  - The significance of running code at Edge Locations
  - Distinguished the 4 trigger types and their use cases

- Reinforced and advanced AWS networking knowledge through the Networking Workshop.

- Built a highly available web application, understanding how to combine:
  - Multiple Availability Zones
  - Auto Scaling
  - Load balancing
  - Monitoring

- Completed the Explore AWS Services section, gaining an overall view of the foundational services.
