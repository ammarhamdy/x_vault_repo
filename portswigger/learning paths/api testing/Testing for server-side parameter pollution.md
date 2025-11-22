
To test for server-side parameter pollution in the query string, place query syntax characters like `#`, `&`, and `=` in your input and observe how the application responds.

Consider a vulnerable application that enables you to search for other users based on their username. 
When you search for a user, your browser makes the following request:

```
GET /userSearch?name=peter&back=/home
```

```
GET /users/search?name=peter&publicProfile=true
```


# Truncating query strings

You can use a URL-encoded `#` character to attempt to truncate the server-side request. 
To help you interpret the response, you could also add a string after the `#` character.

```
GET /userSearch?name=peter%23foo&back=/home
```

The front-end will try to access the following URL:
```
GET /users/search?name=peter#foo&publicProfile=true
```

Review the response for clues about whether the query has been truncated. 

For example, if the response returns the user `peter`, the server-side query may have been truncated.

If an `Invalid name` error message is returned, the application may have treated `foo` as part of the username. 
This suggests that the server-side request may not have been truncated.


# Injecting invalid parameters

You can use an URL-encoded `&` character to attempt to add a second parameter to the server-side request.

For example, you could modify the query string to the following:
```
GET /userSearch?name=peter%26foo=xyz&back=/home
```

This results in the following server-side request to the internal API:
```
GET /users/search?name=peter&foo=xyz&publicProfile=true
```



# Overriding existing parameters
To confirm whether the application is vulnerable to server-side parameter pollution, you could try to override the original parameter.

Do this by injecting a second parameter with the same name.

For example, you could modify the query string to the following:
```
GET /userSearch?name=peter%26name=carlos&back=/home
```

This results in the following server-side request to the internal API:
```
GET /users/search?name=peter&name=carlos&publicProfile=true
```

The impact of this depends on how the application processes the second parameter. 
This varies across different web technologies. 
For example:
- **`PHP`** parses the last parameter only. This would result in a user search for `carlos`.
- **`ASP.NET`** combines both parameters. This would result in a user search for `peter,carlos`, which might result in an `Invalid username` error message.
- **`Node.js`** / express parses the first parameter only. This would result in a user search for `peter`, giving an unchanged result.

