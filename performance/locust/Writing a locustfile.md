
```python
import time
from locust import HttpUser, task, between

"""
Here we define a class for the users that we will be simulating.
It inherits from HttpUser which gives each user a client attribute, which is an instance of HttpSession.
When a test starts, locust will create an instance of this class for every user that it simulates,
and each of these users will start running within their own green gevent thread.
"""
class QuickStartUser(HttpUser):
    """
    Our class defines a wait_time that will make the simulated users
    wait between 1 and 5 seconds after each task.
    When a task has finished executing, the User will then sleep for its
    specified wait time (in this case between 1 and 5 seconds).
    Then it will pick a new task.
    """
    wait_time = between(1, 5)

    """
    For every running User, Locust creates a greenlet 
    (a coroutine or “micro-thread”), that will call those methods.
    Code within a task is executed sequentially 
    (it is just regular Python code)
    """
    @task
    def hello_world(self):
        """
        The self.client attribute makes it possible to make HTTP 
        calls that will be logged by Locust.
        """
        self.client.get("https://basam.codlop.sa/")

    """
    Tasks are picked at random, but you can give them 
    different weighting.
    The above configuration will make Locust three times more likely 
    to pick view_items than hello_world.
    """
    @task(3)
    def view_items(self):
        for i_id in range(110, 151+1):
            self.client.get(
	            f"https://basam.codlop.sa/dashboard/contact-us/{i_id}"
	        )
            time.sleep(1)

    """
    Additionally we’ve declared an on_start method. 
    A method with this name will be called for each simulated user 
    when they start.
    """
    def on_start(self):
        credentials = {
	        "username": "admin@admin.com", 
	        "password": "123456789"
	    }
        self.client.post(
	        "https://basam.codlop.sa/dashboard/login", 
	        credentials
	    )
```

## User class
A user class represents one type of user/scenario for your system. 
When you do a test run you specify the number of concurrent users you want to simulate and Locust will create an instance per user.

### wait_time attribute
A User’s [`wait_time`](https://docs.locust.io/en/stable/api.html#locust.User.wait_time "locust.User.wait_time") method makes it easy to introduce delays after each task execution. 
If no wait_time is specified, the next task will be executed as soon as one finishes.
- [`constant`](https://docs.locust.io/en/stable/api.html#locust.wait_time.constant "locust.wait_time.constant") for a fixed amount of time
- [`between`](https://docs.locust.io/en/stable/api.html#locust.wait_time.between "locust.wait_time.between") for a random time between a min and max value
- [`constant_throughput`](https://docs.locust.io/en/stable/api.html#locust.wait_time.constant_throughput "locust.wait_time.constant_throughput") for an adaptive time that ensures the task runs (at most) X times per second.
- [`constant_pacing`](https://docs.locust.io/en/stable/api.html#locust.wait_time.constant_pacing "locust.wait_time.constant_pacing") for an adaptive time that ensures the task runs (at most) once every X seconds (it is the mathematical inverse of constant_throughput).

### @task decorator
The easiest way to add a task for a User is by using the [`task`](https://docs.locust.io/en/stable/api.html#locust.task "locust.task") decorator.
**@task** takes an optional weight argument that can be used to specify the task’s execution ratio.

## Send post request 
```python
import json
from locust import HttpUser, task, between


large_data = {
    "key1": "value1",
    "key2": ["item1", "item2", "item3"],
    "key3": {
        "nested_key1": "nested_value1",
        "nested_key2": 12345
    },
    # ... add your large JSON data here ...
}
json_data = json.dumps(large_data)


class MyUser(HttpUser):
    host = "http://your-target-api.com"
    wait_time = between(1, 2.5)

    @task
    def send_large_json(self):
        headers = { 'Content-Type': 'application/json' }
        self.client.post(
	        "/your-endpoint", 
	        data=json_data, 
	        headers=headers
	    )


```

```python
from locust import HttpUser, task  
  
  
class SimpleUser(HttpUser):  
    host = "https://sadiq-eltajer.sa/"  
  
    @task  
    def home_page(self):  
        self.client.get("/")
```

----

# Run


```sh
locust -f file_name.py
```

![[Pasted image 20250623092027.png]]
Ramping to 700 users at a rate of 1.00 per second

![[Pasted image 20250623092316.png]]


![[total_requests_per_second_1744031823.751.png]]
`PRS` -> Request per second 
`percentile` -> (%) it tells you the percentage of values that are _less than_ or _equal to_ a particular value.
