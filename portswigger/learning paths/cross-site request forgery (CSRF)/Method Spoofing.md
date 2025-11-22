


**HTTP Method Spoofing** is a technique used when a client (usually a browser or frontend app) needs to send HTTP methods like `PUT`, `PATCH`, or `DELETE`, but is restricted to using only `GET` and `POST` due to browser limitations or security policies.

To bypass this, the **actual HTTP method** is sent via a special parameter, usually in the request body or headers, while the request itself is sent as a `POST` request.


```html
<form action="/users/123" method="POST">
    <input type="hidden" name="_method" value="DELETE">
    <button type="submit">Delete User</button>
</form>
```



## How HTTP Method Spoofing Works

1. The client sends a `POST` request but includes the intended HTTP method inside:
    - A **hidden form field** (`_method`).
    - A **custom request header** (`X-HTTP-Method-Override`).

2. The server reads the `_method` field or the `X-HTTP-Method-Override` header and **treats the request as if it was sent using the spoofed method** (`PUT`, `PATCH`, `DELETE`, etc.).



## `Symfony` and `Laravel` Support for Method Spoofing

- **`Symfony`** automatically handles method spoofing if you use `_method` in forms.
- **`Laravel`** has a helper method for method spoofing in Blade templates:
```html
<form action="/users/123" method="POST">
    @method('DELETE')
    @csrf
    <button type="submit">Delete</button>
</form>
```



## Why Use HTTP Method Spoofing?

Works around browser limitations (which mainly support `GET` and `POST`).  

Enables RESTful API interaction via **HTML forms**.  

Maintains compatibility with frameworks and routing systems expecting `PUT`, `PATCH`, or `DELETE` methods.