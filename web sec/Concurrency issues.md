
# Race condition

A **race condition** happens when the behavior of a program depends on the timing or order of events — and multiple things are trying to access or change the same data at the same time.


If the timing changes (even slightly), the program might behave differently, often in unexpected or incorrect ways.

## Key points

- **Where it happens:** Usually in concurrent systems — multithreading, multiprocessing, or multiple programs accessing shared resources.
    
- **Why it happens:** Two (or more) “racing” operations read or write the same data without proper synchronization.
    
- **Result:** Inconsistent or unpredictable output.

```less
ThreFour conditions for deadlockFour conditions for deadlockad A reads counter (value = 10)
Thread B reads counter (value = 10)
Thread A adds 1 → writes back 11
Thread B adds 1 → writes back 11
```

## Prevention

- Use **locks**, **mutexes**, or **synchronization primitives** to ensure only one operation can modify shared data at a time.
    
- Avoid unnecessary shared state.
    
- In some systems, use **atomic operations**.


---

# Dead lock

A **deadlock** is when two or more processes (or threads) are stuck **waiting for each other forever**, and none of them can proceed.

## Classic example

Two threads and two resources:

1. **Thread A** locks **Resource 1**.
    
2. **Thread B** locks **Resource 2**.
    
3. **Thread A** tries to lock **Resource 2** — but it’s already held by Thread B.
    
4. **Thread B** tries to lock **Resource 1** — but it’s already held by Thread A.

Both are now **waiting forever**.


## Prevention strategies

- **Avoid circular wait**: Always request resources in a fixed global order.
    
- **Timeouts**: Cancel the request if it takes too long.
    
- **Lock hierarchy**: Define the order in which locks must be acquired.
    
- **Deadlock detection**: Monitor and kill/restart one process to break the cycle.


## Four conditions for deadlock (Coffman’s conditions)

For a deadlock to occur, all of these must happen:

1. **Mutual exclusion** — a resource can only be held by one process at a time.
    
2. **Hold and wait** — a process is holding one resource while waiting for another.
    
3. **No preemption** — resources can’t be forcibly taken away.
    
4. **Circular wait** — a closed loop where each process waits for the next.

----
# Rate limit

A **rate limit** is a rule that restricts how often something can happen in a given period of time.


## Where it’s used

- **APIs**: A server might allow only _100 requests per minute_ from one user to prevent overload or abuse.
    
- **Networking**: Limit data packets per second to avoid congestion.
    
- **Security**: Slow down login attempts to prevent brute-force attacks.
    
- **Services**: Email providers may cap the number of emails sent per hour.


## Why it exists

1. **Protect resources** — prevent servers from being overwhelmed.
    
2. **Fair usage** — keep one user from hogging all the bandwidth.
    
3. **Prevent abuse** — block spam or automated attacks.


## Common methods

- **Fixed window**: Allow X actions per fixed time frame (e.g., per minute).
    
- **Sliding window**: Track usage over the last N seconds/minutes dynamically.
    
- **Token bucket / leaky bucket**: Allow bursts of activity but enforce an average rate.


## Example

If an API has a limit of **60 requests per minute**:

- You send 60 requests in the first 30 seconds — OK.
    
- You try the 61st request before the minute resets — server says **429 Too Many Requests**.
    
- Wait until the window resets to send more.


----
# Summery 

> **Race condition** – _Two people try to grab the same chair at the same time; sometimes one wins, sometimes the other, sometimes they both fall._
> 
> **Deadlock** – _Two people each have one half of a sandwich and refuse to trade until they get the other half — so nobody eats._
> 
> **Rate limit** – _The cafeteria says “Only 5 sandwiches per minute” so even if you’re hungry, you have to wait for the clock._

It’s basically:
- **Race condition** → unpredictable results
- **Deadlock** → nothing happens forever
- **Rate limit** → enforced waiting even if nothing else is wrong

