
# No auth

No authorization


# API key

With API key `auth`, you send a key-value pair to the API either in the request headers or query parameters.



# Bearer token
[[2. the anatomy of web APIs]]
Bearer tokens enable requests to authenticate using an access key, such as a JSON Web Token (JWT). 

==The token is a text string, included in the request header.==


# JWT bearer

The JWT token Supported algorithms include:
- **HS** - `HMAC` with SHA
- **RS** - `RSA` (`RSASSA-PKCS1-v1_5`) with SHA
- **ES** - `ECDSA` with SHA
- **PS** - `RSA` (`RSASSA-PSS`) with SHA



# OAuth 2.0

With OAuth 2.0, you first retrieve an access token for the API, then use that token to authenticate future requests. 

Access tokens are typically short-lived, but the authorization server can also provide a long-lived refresh token. 

A client application can use the refresh token to automatically

Accessing data with OAuth 2.0 varies greatly between API service providers, but typically involves a few requests back and forth between client application, user, and API.

An example OAuth 2.0 flow could run as follows:

- A client application makes a request for the user to authorize access to their data.

- If the user grants access, the application then requests an access token from the service provider, passing the access grant from the user and authentication details to identify the client.

- The service provider validates these details and returns a short-lived access token and a long-lived refresh token.

- The client uses the access token to request the user data with the service provider.

- When the access token expires, the client can use the refresh token to automatically request a new access token.