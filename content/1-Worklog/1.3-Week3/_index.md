---
title: "Week 3 Worklog"
date: 2026-05-17
weight: 3
chapter: false
pre: " <b> 3.1. </b> "
---

## General Information

| Content         | Details                                                                                     |
| --------------- | ------------------------------------------------------------------------------------------- |
| Duration        | 05/17/2026 - 05/23/2026                                                                     |
| Internship Week | Week 3                                                                                      |
| Phase           | Explore AWS Services (Advanced)                                                             |
| Program         | First Cloud Journey                                                                         |
| Main Topics     | NoSQL, caching, CDN, edge computing, advanced networking, and highly available applications |
| Weekly Goals    | Master DynamoDB, ElastiCache, CloudFront, Lambda@Edge, advanced networking, and HA web apps |

## Week 3 Learning Orientation

Week 3 concludes the **Explore AWS Services** phase with heavier workshops: NoSQL databases (DynamoDB), caching (ElastiCache), content delivery (CloudFront), edge computing (Lambda@Edge), advanced networking, and a comprehensive exercise on highly available web applications. These topics were noticeably more difficult than the previous two weeks, so I spent more time reading carefully and left the two heaviest tasks for the weekend.

## Week 3 Learning Objectives

- Explore NoSQL Database Essentials with Amazon DynamoDB.
- Explore In-Memory Caching with Amazon ElastiCache.
- Explore Content Delivery with Amazon CloudFront.
- Explore Edge Computing with CloudFront and Lambda@Edge.
- Explore Networking on AWS Workshop.
- Explore Building Highly Available Web Applications.

## Activities Implemented During the Week

### Day 1 - Monday, 05/18/2026

Topic: **NoSQL Database Essentials with Amazon DynamoDB**.
Implemented Activities:

- Read about DynamoDB: tables, items, partition keys, and sort keys.
- Learned about capacity modes (On-Demand and Provisioned) and GSI/LSI indexes.
- Followed a workshop to create a table and tested inserting, reading, and deleting items.

I created a table via CLI with the partition key `UserId`:

```bash
aws dynamodb create-table \
  --table-name Users \
  --attribute-definitions AttributeName=UserId,AttributeType=S \
  --key-schema AttributeName=UserId,KeyType=HASH \
  --billing-mode PAY_PER_REQUEST
```

Added and retrieved an item:

```bash
aws dynamodb put-item --table-name Users \
  --item '{"UserId": {"S": "u001"}, "Name": {"S": "Nam"}}'

aws dynamodb get-item --table-name Users \
  --key '{"UserId": {"S": "u001"}}'
```

```json
{
  "Item": {
    "Name": { "S": "Nam" },
    "UserId": { "S": "u001" }
  }
}
```

Once I tried `get-item` with `Name` as the key instead of `UserId` and got an error:

```
An error occurred (ValidationException): The provided key element does not match the schema
```

At this point, I realized that DynamoDB only allows querying by defined keys. To search by other fields, you must consider GSIs from the table design phase.

Achieved Results:

- Understood that DynamoDB requires a completely different mindset than relational databases; it requires thinking about access patterns.
- Was able to create and manipulate data in a table at a basic level.
- Memorized the `put-item` / `get-item` command structures and the lesson of properly choosing keys from the start.

### Day 2 - Tuesday, 05/19/2026

Topic: **In-Memory Caching with Amazon ElastiCache**.
Implemented Activities:

- Read about ElastiCache and the two engines: Redis and Memcached.
- Learned why caching reduces database load and speeds up queries (cache-aside model).
- Reviewed a tutorial on creating a cluster to visualize how it works.

Achieved Results:

- Understood the role of caching and when to use ElastiCache.
- Distinguished between Redis and Memcached at a high level.

### Day 3 - Wednesday, 05/20/2026

Topic: **Content Delivery with Amazon CloudFront**.
Implemented Activities:

- Read about CloudFront and the Edge Location network.
- Learned about distributions, origins, cache behaviors, and TTL.
- Followed a workshop to create a distribution with an S3 bucket (created in week 1) as the origin.

After modifying a file on S3, the CloudFront page still showed the old version. I created an invalidation to clear the cache:

```bash
aws cloudfront create-invalidation \
  --distribution-id E123ABC456DEF --paths "/*"
```

```json
{
  "Invalidation": {
    "Status": "InProgress",
    "InvalidationBatch": {
      "Paths": { "Quantity": 1, "Items": ["/*"] }
    }
  }
}
```

Waited for the status to change to `Completed`, and then the new content appeared. That's when I understood why "modifying a file didn't update the web page" — the TTL was still effective at the Edge.

Achieved Results:

- Understood that CloudFront distributes content closer to users to reduce latency.
- Successfully created a simple distribution following the guide.
- Memorized the `create-invalidation` command to force cache updates after modifying content.

### Day 4 - Thursday, 05/21/2026

Topic: **Edge Computing with CloudFront and Lambda@Edge**.
Implemented Activities:

- Read about Lambda@Edge and the concept of running code directly at Edge Locations.
- Learned about the 4 trigger types: viewer request/response, origin request/response.
- Reviewed an example of a small function customizing responses to understand how it's applied.

Achieved Results:

- Grasped the concept of edge computing and the role of Lambda@Edge.
- Gained a preliminary understanding of the 4 trigger types.

### Day 5 - Friday, 05/22/2026

Topic: **Networking on AWS Workshop**.
Implemented Activities:

- Reread and expanded on the networking section: VPCs, subnets, and routing in more complex scenarios than week 1.
- Followed the step-by-step workshop to reinforce networking knowledge.

Achieved Results:

- Became more confident with networking concepts compared to when I first learned about VPCs.

### Day 6 - Saturday, 05/23/2026

Topic: **Building Highly Available Web Applications**.
Implemented Activities:

- Read a comprehensive guide on building highly available web apps.
- Followed instructions to combine multiple AZs, Auto Scaling, and load balancing.
- Summarized the knowledge from the entire week and the Explore phase.

Achieved Results:

- Visualized how the previously learned services integrate into a highly available system.
- Saw a clearer connection between the disparate concepts learned earlier.

## Week 3 Knowledge Summary

| Knowledge Group   | Learned Content                                       |
| ----------------- | ----------------------------------------------------- |
| NoSQL Database    | DynamoDB, partition/sort key, capacity mode, GSI/LSI  |
| Caching           | ElastiCache, Redis, Memcached, cache-aside            |
| Content Delivery  | CloudFront, distribution, origin, cache behavior, TTL |
| Edge Computing    | Lambda@Edge, trigger types                            |
| Networking        | Networking on AWS Workshop                            |
| High Availability | Building Highly Available Web Applications            |

## Achievements During the Week

- Successfully created and manipulated data in DynamoDB.
- Understood the role of ElastiCache and how to create a cluster.
- Created a CloudFront distribution and understood the purpose of Lambda@Edge.
- Reinforced advanced networking concepts.
- Learned how to build a highly available web app following a workshop.

## Challenges Encountered

- DynamoDB was the most frustrating part this week. Having a relational table mindset caused me to incorrectly design partition keys, forcing me to rethink based on query patterns.
- After caching with CloudFront, I modified a file and it didn't update. It turned out to be the TTL, and I had to perform an invalidation to see the changes.
- The highly available web app tutorial had too many components. I couldn't remember everything after one read and had to draw diagrams to keep track.

## Lessons Learned

- I realized DynamoDB isn't just a matter of changing names from SQL; it requires thinking about how data will be queried.
- Caching speeds things up but can be confusing if you don't understand TTL, so it requires careful configuration.
- Comprehensive exercises at the end of the Explore phase helped connect the fragmented concepts, revealing the bigger picture.

## Plan for Week 4

- Transition to the Migrate to AWS phase: VM Import/Export, DMS + SCT, Elastic Disaster Recovery.
- Begin the Optimize - Operations phase: Systems Manager, Session Manager, Tags & Resource Groups.

## End of Week Review

Week 3 was the heaviest among the first three weeks, especially DynamoDB and the highly available web app tutorial. However, after finishing the Explore phase, I feel I have a fairly comprehensive view of foundational services, enough to confidently move to the Migrate and Optimize phases.
