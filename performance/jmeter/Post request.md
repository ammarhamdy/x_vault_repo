
In Apache JMeter, to create a POST request that uses **different parameters for each virtual user** during a test run, you typically use a **CSV Data Set Config** element to feed in dynamic values for each user.


# **Create a CSV File with Your Test Data**
Create a `.csv` file that holds the parameter values you want to vary per user.

# Add a CSV Data Set Config Element

Right-click on **Test Plan** > Add > **Config Element** > **CSV Data Set Config**

Configure it as follows:
- **Filename**: `user_data.csv` (full path if not in same directory as `.jmx` file)
- **Variable Names**: `username,password,email` (comma-separated, must match column headers or positions)
- **Delimiter**: `,`
- **Recycle on EOF?**: `False` (or `True` if you want to reuse data)
- **Stop thread on EOF?**: `True` (if you want threads to stop when data runs out)
- **Sharing mode**: `All Threads` (unless you're doing something specific)

# Add an HTTP Request Sampler (POST Request)

* Right-click on **Thread Group** > Add > **Sampler** > **HTTP Request**
* Configure:
	* **Method**: `POST`
	* **Server Name or IP**: `your.server.com`
	* **Path**: `/your/api/endpoint`
In **Body Data** or **Parameters**:
If using `Parameters` tab:
```plaintext
Name: username | Value: ${username}
Name: password | Value: ${password}
Name: email    | Value: ${email}
```
If using `Body Data` (raw JSON):
```json
{
	"username": "${username}",
	"password": "${password}",
	"email": "${email}"
}
```
* Also, ensure **"Content-Type: application/json"** is set in the **HTTP Header Manager**.
