
```
my-locust-project/
├── locustfile.py            # Main entry point for Locust
├── locust.conf              # Optional config file
├── requirements.txt         # Python dependencies
├── users/
│   ├── __init__.py
│   ├── website_user.py      # Locust user classes
│   └── api_user.py          # Another user class
├── tasks/
│   ├── __init__.py
│   ├── main_page.py         # Task sets or reusable tasks
│   └── login.py
├── utils/
│   ├── __init__.py
│   └── data_loader.py       # Helper functions (reading CSV)
└── data/
    └── users.csv            # Data files (login credentials)
```


**Only config-file-supported keys** (like `host`, `loglevel`, and `web-host`) will be read from `locust.conf`.

```bash
locust -f locustfile.py --config locust.conf
```

```bash
locust --config locust.conf --users 2 --spawn-rate 10 --run-time 1m --headless
```
+ `locust` --> Starts the Locust load testing tool.
+ `--config locust.conf` --> Tells Locust to read settings from the locust.conf file (e.g. host, loglevel, etc.).
+ `--users 2` --> Simulate ==2 concurrent users== (virtual users). These users will repeatedly run tasks.
+ `--spawn-rate 10` --> Start 10 users per second until the total (--users) is reached. In this case, it will start both users immediately (since 2 < 10).
+ `--run-time 1m` --> Run the test for 1 minute, then automatically stop.
+ `--headless` --> Run in headless mode (no web UI). This is useful for automation, CI/CD, or when you just want console output.

---

# Cycle function 

```python
from itertools import cycle

def on_start(self):
    self.user_cycle = cycle(self.test_users)

@task
def login(self):
    user = next(self.user_cycle)
```

---

# Login then request


```python
from locust import HttpUser, task, between

class WebsiteUser(HttpUser):
    wait_time = between(1, 2)

    def login(self):
        # Perform login and get the token or session cookie
        response = self.client.post("/login", json={
            "username": "testuser",
            "password": "password123"
        })

        if response.status_code == 200:
            # Assume we get a token in the response
            token = response.json().get("token")
            return token
        else:
            print(
	            f"Login failed: {response.status_code}"
            )
            return None

    @task
    def access_dashboard(self):
        token = self.login()  # Login before every request

        if token:
            # Use the token to access a protected route
            self.client.get(
                "/dashboard",
                headers={"Authorization": f"Bearer {token}"}
            )
```