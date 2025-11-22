
https://www.locust.cloud/blog/performance-testing-part-1

---

#  Gather performance requirements and discover your limits

Some companies have known performance requirements (such as ==supporting a certain number of transactions per second== and a ==maximum acceptable response time==). 

Sometimes you can estimate your load requirements based on past data or market analysis, but it’s equally common that you won’t know exactly what your requirements are. 

A lot of the time you’ll want to aim for ___discovering your limit___ (sometimes called ==**break-point testing**==), not just testing to meet a specific requirement.

# Reproduce a performance problem

In many cases production issues emerge برز only when there is an unusual amount of load (such as **Black Friday**, a product launch, a sporting event, etc). 

With load testing you can reproduce the behavior in a test environment to gather more information and validate a fix.

# Validate performance of new features or changes

You can also use load testing to check if an architectural change the team has been working on performs as expected, or validate that a change improves performance.


# Test scalability

When load testing, it’s important not just to test absolute performance, but also scalability: you may have the ability to spin up تدور another instance of a service when under demand, but do you know if the service is actually twice as fast with two instances? ==Sometimes throwing extra resources at a problem doesn’t actually solve performance problems==. 

Also, in a lot of cases, some part of your system might not be [horizontally scalable](https://wa.aws.amazon.com/wellarchitected/2020-07-02T19-33-23/wat.concept.horizontal-scaling.en.html), and ends up becoming the new bottleneck as you ramp up additional instances of your service.




