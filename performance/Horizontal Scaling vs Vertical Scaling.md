

https://www.techopedia.com/definition/7594/horizontal-scaling?ref=wellarchitected

**Horizontal scaling** is a term used in many different kinds of IT setups. 

The basic meaning of horizontal scaling is that systems are "built out" ==**using additional components**==. 

By contrast, the term "**vertical scaling**" ==means that extra capability and resources are added to one single component==.

----
# Vertical Scaling (Scaling Up)

## How:
- Upgrade your server to have more **CPU cores**, **RAM**, **faster SSDs**, or **network bandwidth**.

## ✅ Pros:
- Simple to implement.
- No code changes needed in most cases.

## ❌ Cons:
- **Hard limits** — you can't scale infinitely.
- **Downtime** is often required for upgrades.
- Single point of failure.


---

# Horizontal Scaling (Scaling Out)

[Horizontal scaling](https://wa.aws.amazon.com/wellarchitected/2020-07-02T19-33-23/wat.concept.horizontal-scaling.en.html)

## How:
- Add more **backend nodes**, **servers**, or **containers**.
- Use a **load balancer** to distribute traffic.

## ✅ Pros:
- Virtually limitless scaling potential.
- Redundancy and fault tolerance.
- No downtime when adding resources.

## ❌ Cons:
- Requires architecture changes.
- Harder to manage (sessions, caching, etc.).
- Needs orchestration (like Kubernetes or ECS).

## Example:
You run your backend as a containerized microservice. When traffic increases, your orchestration system (like Kubernetes) spins up 3 more instances and routes requests via a load balancer.


----
# Summary

| Feature             | **Vertical Scaling** 🏗️            | **Horizontal Scaling** 🧱                         |
| ------------------- | ----------------------------------- | ------------------------------------------------- |
| Also known as       | "Scaling up"                        | "Scaling out"                                     |
| How it works        | Increase power of a single server   | Add more servers or instances                     |
| Example             | Upgrade CPU/RAM/disk on one machine | Add more backend nodes (e.g., more app servers)   |
| Performance gain    | Limited by hardware ceiling         | Virtually unlimited                               |
| Downtime required   | Often yes (restart needed)          | Often no (instances added dynamically)            |
| Complexity          | Simpler                             | More complex (needs load balancing, coordination) |
| Cost scaling        | Can be cost-inefficient long term   | Often more cost-effective at scale                |
| Failover/redundancy | Risk of single point of failure     | Better fault tolerance                            |
| Typical use cases   | Small to medium apps, monoliths     | Distributed systems, cloud-native apps            |
