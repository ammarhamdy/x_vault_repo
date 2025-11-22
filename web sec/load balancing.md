
**Load balancing** is the process of distributing incoming network traffic across multiple servers to ensure no single server becomes overwhelmed.

It helps improve:
- **Performance**
- **Availability (uptime)**
- **Scalability**
- **Fault tolerance**

---

# How It Works

Suppose you visit a website like `example.com`. 

Instead of sending all requests to a single server, a **load balancer** sits in front and does this:

|User Request|Load Balancer Forwards To|
|---|---|
|User A|Server 1|
|User B|Server 2|
|User C|Server 3|

The load balancer chooses which server to use based on:
- Current load (CPU, memory, etc.)
- Response time
- Round-robin rotation
- Geo-location
- Session persistence
    

---

# Types of Load Balancers

1. **Hardware Load Balancers**
    - Expensive, physical devices (e.g., `F5`, `Cisco`)
    
2. **Software Load Balancers**
    - Open-source or cloud-based (e.g., `NGINX`, `HAProxy`)
    
3. **Cloud Load Balancers**
    - Managed by providers (e.g., `AWS ELB`, `Azure Load Balancer`)

