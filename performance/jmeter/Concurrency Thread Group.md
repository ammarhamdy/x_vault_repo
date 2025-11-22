# Install the “Concurrency Thread Group” Plugin

1. Open **Plugins Manager**
2. Go to the **Available Plugins** tab
3. Search for **“Concurrency Thread Group”** (from `jmeter-plugins`)
4. Check it and click **Apply Changes and Restart JMeter**


# Add the Concurrency Thread Group to Your Test Plan

1. Right-click **Test Plan** > Add > **Threads (Users)** > **Concurrency Thread Group**
2. You'll see the CTG with several unique options:

# Concurrency Thread Group Parameters

| Parameter                       | Description                                                                      |
| ------------------------------- | -------------------------------------------------------------------------------- |
| **Target Concurrency**          | Number of virtual users (threads) to maintain concurrently.                      |
| **Ramp-Up Time**                | Time (in seconds) to reach the target concurrency. Users will gradually ramp up. |
| **Ramp-Up Steps Count**         | Number of steps into which the ramp-up period is divided.                        |
| **Hold Target Rate Time**       | How long to maintain the target concurrency.                                     |
| **Time Unit**                   | Usually seconds or minutes.                                                      |
| **Iterations Limit (optional)** | Max number of iterations per thread.                                             |
Example:
- Target Concurrency: `100`
- Ramp-Up Time: `60`
- Hold Target Rate: `120`  
    → JMeter will ramp up to 100 users over 60 seconds, then maintain that load for 2 minutes.

# Add Samplers (HTTP Requests)

Add your HTTP Requests under the Concurrency Thread Group just like in a regular thread group.

They will execute in the defined order per thread/user.


# Add Listeners, Assertions, and Timers

You can use **View Results Tree**, **Summary Report**, or **Dashboard Generation** for results.

Add **Assertions** to validate responses.

Add **Timers** (like Constant Timer) to simulate think time between requests.


