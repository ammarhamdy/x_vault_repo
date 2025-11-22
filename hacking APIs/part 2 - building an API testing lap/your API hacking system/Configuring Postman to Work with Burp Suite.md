

Postman is useful for interacting with APIs, and Burp Suite is a powerhouse for web application testing. 

If you combine these applications, you can configure and test an API in Postman and then proxy the traffic over to Burp Suite to brute-force directories, tamper with parameters, and fuzz all the things.


As when you set up `FoxyProxy`, you’ll need to configure the Postman proxy to send traffic over to Burp Suite using the following steps

1. Open Postman settings by pressing CTRL-, (comma) or navigating to File > Settings.
2. Click the Proxy tab.
3. Click the checkbox for adding a custom proxy configuration.
4. Make sure to set the proxy server to `127.0.0.1`.
5. Set the proxy server port to `8080`.
6. Select the General tab and turn `SSL` certificate verification Off.
7. In Burp Suite, select the Proxy tab.
8. Click the button to turn Intercept On.

Try sending a request using Postman; if it is intercepted by Burp Suite, you’ve properly configured everything.
