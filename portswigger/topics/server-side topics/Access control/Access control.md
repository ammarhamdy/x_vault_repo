
https://portswigger.net/web-security/access-control
---
# Access control vulnerabilities and privilege escalation

## What is access control?

Access control is the application of constraints on who or what is authorized to perform actions or access resources. 

In the context of web applications, access control is dependent on authentication and session management:

- **Authentication** ==confirms that the user is who they say they are==.

- **Session management** identifies which subsequent HTTP requests are being made by that same user.

- **Access control** determines whether the user is allowed to carry out the action that they are attempting to perform.

Broken access controls are common and often present a critical security vulnerability. 

Design and management of access controls is a complex and dynamic problem that applies business, organizational, and legal constraints to a technical implementation. 

Access control design decisions have to be made by humans so the potential for errors is high.

### Vertical access controls

Vertical access controls are mechanisms that restrict access to **sensitive functionality** to specific types of users.

With vertical access controls, different types of users have access to different application functions. 

**For example**, an administrator might be able to modify or delete any user's account, while an ordinary user has no access to these actions. 

Vertical access controls can be more fine-grained implementations of security models designed to enforce business policies such as separation of duties and least privilege.

### Horizontal access controls

Horizontal access controls are mechanisms that restrict access to **resources** to specific users.

With horizontal access controls, different users have access to a subset of resources of the same type. 

**For example**, a banking application will allow a user to view transactions and make payments from their own accounts, but not the accounts of any other user.

### Context-dependent access controls

Context-dependent access controls restrict access to functionality and resources based upon the state of the application or the user's interaction with it.

Context-dependent access controls prevent a user performing actions in the **wrong order**. 

**For example**, a retail website might prevent users from modifying the contents of their shopping cart after they have made payment.



## Examples of broken access controls

Broken access control vulnerabilities exist when a user can access resources or perform actions that they are not supposed to be able to.

### Vertical privilege escalation

If a user can gain access to functionality that they are not permitted to access then this is vertical privilege escalation.

**For example**, if a non-administrative user can gain access to an admin page where they can delete user accounts, then this is vertical privilege escalation.

#### Unprotected functionality

At its most basic, vertical privilege escalation arises where an application does not enforce any protection for sensitive functionality. 

For example, administrative functions might be linked from an administrator's welcome page but not from a user's welcome page. 

However, a user might be able to access the administrative functions by browsing to the relevant admin URL.

For example, a website might host sensitive functionality at the following URL:
```
https://insecure-website.com/admin
```

In some cases, sensitive functionality is concealed by giving it a less predictable URL. 

This is an example of so-called "==security by obscurity==". 

However, hiding sensitive functionality does not provide effective access control because users might discover the obfuscated URL in a number of ways.

Imagine an application that hosts administrative functions at the following URL:
```
https://insecure-website.com/administrator-panel-yb556
```
 The URL might be disclosed in JavaScript that constructs the user interface based on the user's role:

```js
<script>
	var isAdmin = false;
	if (isAdmin) {
		...
		var adminPanelTag = document.createElement('a');
		adminPanelTag.setAttribute(
			'href', 
			'https://insecure-website.com/administrator-panel-yb556'
			);
		adminPanelTag.innerText = 'Admin panel';
		...
	}
</script>
```


#### Parameter-based access control methods

Some applications determine the user's access rights or role at login, and then store this information in a user-controllable location. 

This could be:
- A hidden field.
- A cookie.
- A preset query string parameter.

The application makes access control decisions based on the submitted value. 
**For example**:
```http
https://insecure-website.com/login/home.jsp?admin=true https://insecure-website.com/login/home.jsp?role=1
```

This approach is insecure because a user can modify the value and access functionality they're not authorized to, such as administrative functions.

#### Broken access control resulting from platform misconfiguration

Some applications enforce access controls at the platform layer. 
they do this by restricting access to specific URLs and HTTP methods based on the user's role. 

For example, an application might configure a rule as follows:
```
DENY: POST, /admin/deleteUser, managers
```

This rule denies access to the `POST` method on the URL `/admin/deleteUser`, for users in the managers group. 

Various things can go wrong in this situation, leading to access control bypasses.

Some application frameworks support various non-standard HTTP headers that can be used to override the URL in the original request, such as `X-Original-URL` and `X-Rewrite-URL`.

If a website uses rigorous front-end controls to restrict access based on the URL, but the application allows the URL to be overridden via a request header, then it might be possible to bypass the access controls using a request like the following:

```http
POST / HTTP/1.1 
X-Original-URL: /admin/deleteUser
```

```
Send the request to Burp Repeater. 

Change the URL in the request line to `/` and add the HTTP header `X-Original-URL: /invalid`. 

Observe that the application returns a "not found" response. 

This indicates that the back-end system is processing the URL from the `X-Original-URL` header.
```

![[Pasted image 20250522143944.png]]
Or 
![[Pasted image 20250522144029.png]]


#### Broken access control resulting from URL-matching discrepancies

Websites can vary in how strictly they match the path of an incoming request to a defined endpoint. 

For example, they may tolerate inconsistent capitalization, so a request to `/ADMIN/DELETEUSER` ==may== still be mapped to the `/admin/deleteUser` endpoint. 

==If the access control mechanism is less tolerant, it may treat these as two different endpoints and fail to enforce the correct restrictions as a result==.

Similar discrepancies التناقضات can arise if developers using the Spring framework have enabled the `useSuffixPatternMatch` option. 

==This allows paths with an arbitrary file extension to be mapped to an equivalent endpoint with no file extension==. 

In other words, a request to `/admin/deleteUser.anything` would still match the `/admin/deleteUser` pattern. 

Prior to Spring 5.3, this option is enabled by default.

On other systems, you may encounter discrepancies in whether `/admin/deleteUser` and `/admin/deleteUser/` are treated as distinct endpoints. In this case, you may be able to bypass access controls by appending a trailing slash to the path.


### Horizontal privilege escalation

Horizontal privilege escalation occurs if a user is able to gain access to resources belonging to another user, instead of their own resources of that type. 

For example, if an employee can access the records of other employees as well as their own, then this is horizontal privilege escalation.

Horizontal privilege escalation attacks may use similar types of exploit methods to vertical privilege escalation. 
For example, a user might access their own account page using the following URL:
```http
https://insecure-website.com/myaccount?id=123
```
If an attacker modifies the `id` parameter value to that of another user, they might gain access to another user's account page, and the associated data and functions.
This is an example of an insecure direct object reference (`IDOR`) vulnerability.

In some applications, the exploitable parameter does not have a predictable value. 

For example, instead of an incrementing number, an application might use ==globally unique identifiers== (GUIDs) to identify users. 

This may prevent an attacker from guessing or predicting another user's identifier. 

However, the GUIDs belonging to other users might be disclosed elsewhere in the application where users are referenced, such as user messages or reviews.

### Insecure direct object references

==Insecure direct object references== (`IDORs`) are a subcategory of access control vulnerabilities. 

`IDORs` occur if an application uses user-supplied input to access objects directly and an attacker can modify the input to obtain unauthorized access.

It was popularized by its appearance in the OWASP 2007 Top Ten. 
More about `IDORs`: https://portswigger.net/web-security/access-control/idor

### Referer-based access control

Some websites base access controls on the `Referer` header submitted in the HTTP request. 
The `Referer` header can be added to requests by browsers to indicate which page initiated a request.

For example, an application robustly enforces access control over the main administrative page at `/admin`, but for sub-pages such as `/admin/deleteUser` only inspects the `Referer` header. 

If the `Referer` header contains the main `/admin` URL, then the request is allowed.

In this case, the `Referer` header can be fully controlled by an attacker. 

This means that they can forge direct requests to sensitive sub-pages by supplying the required `Referer` header, and gain unauthorized access.

---
# Method-based access control can be circumvented

Lap: https://portswigger.net/web-security/access-control/lab-method-based-access-control-can-be-circumvented


---

## How to prevent access control vulnerabilities

Access control vulnerabilities can be prevented by taking a defense-in-depth approach and applying the following principles:

- Never rely on obfuscation التعتيم alone for access control.

- Unless a resource is intended to be publicly accessible, ==deny access by default==.

- Wherever possible, use a single application-wide mechanism for enforcing access controls.

- At the code level, make it mandatory for developers to declare the access that is allowed for each resource, and deny access by default.

- Thoroughly audit and test access controls to ensure they work as designed.


----
# Insecure direct object references (IDOR)


Insecure direct object references (IDOR) are a type of access control vulnerability that arises when an application uses user-supplied input to access objects directly. 

The term IDOR was popularized by its appearance in the OWASP 2007 Top Ten.

IDOR vulnerabilities are most commonly associated with horizontal privilege escalation, but they can also arise in relation to vertical privilege escalation.

## IDOR examples

There are many examples of access control vulnerabilities where user-controlled parameter values are ==used to access resources or functions directly==.

### IDOR vulnerability with direct reference to database objects

Consider a website that uses the following URL to access the customer account page, by retrieving information from the back-end database:

```http
https://insecure-website.com/customer_account?customer_number=132355
```

Here, the customer number is used directly as a record index in queries that are performed on the back-end database. 

If no other controls are in place, an attacker can simply modify the `customer_number` value, bypassing access controls to view the records of other customers. 

This is an example of an IDOR vulnerability leading to horizontal privilege escalation.

### IDOR vulnerability with direct reference to static files

IDOR vulnerabilities often arise when sensitive resources are located in static files on the server-side filesystem. 

For example, a website might save chat message transcripts to disk using an incrementing filename, and allow users to retrieve these by visiting a URL like the following:

```http
https://insecure-website.com/static/12144.txt
```

In this situation, an attacker can simply modify the filename to retrieve a transcript created by another user and potentially obtain user credentials and other sensitive data.