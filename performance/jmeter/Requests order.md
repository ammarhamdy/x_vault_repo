
To force JMeter to run HTTP requests in a specific order, you simply need to arrange the HTTP Request samplers in that desired order under a Thread Group or Controller. 

==JMeter executes elements in the order they appear from top to bottom.==

---

# Method 1: Use Samplers in Sequential Order

Under your **Thread Group**:
1. Add **HTTP Request 1** (e.g., Login)
2. Add **HTTP Request 2** (e.g., Get user info)
3. Add **HTTP Request 3** (e.g., Submit form)

JMeter will run **Request 1**, then **2**, then **3** for each virtual user.

---

# Method 2: Use a Simple Controller

If you want better grouping and visibility:
1. Right-click on **Thread Group** > Add > **Logic Controller** > **Simple Controller**
2. Add your HTTP Requests inside the controller in the correct order.

This also helps with **test plan organization**, especially for larger test cases.

---

# Method 3: Use Module Controller or Include Controller (Advanced)

For reuse and modularity النمطية across multiple Thread Groups or Test Plans:
- **Module Controller**: Lets you reference and run a specific set of requests (organized in a **Test Fragment**).
- **Include Controller**: Loads external `.jmx` files and runs them.

Useful when you want to **share login logic** or other sequences across multiple tests.