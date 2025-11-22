
Access control vulnerabilities happen when a system fails to properly enforce **who can do what** — meaning attackers can access resources or perform actions they shouldn’t be allowed to.

Here’s a breakdown of the most common types:

* * *

# 1. Broken Access Control

When restrictions on what authenticated (or unauthenticated) users can do are not properly enforced.

* **Example:**  
    A user changes `/user/profile/123` to `/user/profile/124` and can view or edit another user’s profile.
    
* **Impact:**  
    Data leaks, privilege escalation, or full account takeover.
    

* * *

# 2. Vertical Privilege Escalation

When a low-privilege user can perform actions meant for higher-privilege users.

* **Example:**  
    A normal user can access `/admin/deleteUser` without being an admin.
    

* * *

# 3. Horizontal Privilege Escalation

When a user can access or modify another user’s resources at the same privilege level.

* **Example:**  
    A customer views another customer’s order history by changing the `order_id`.
    

* * *

# 4. Insecure Direct Object References (IDOR)

When an app exposes an internal object identifier without proper authorization checks.

* **Example:**  
    Accessing `/invoices/1234.pdf` returns another user’s invoice without verifying ownership.
    

* * *

# 5. Missing Function Level Access Control

When back-end APIs allow restricted operations without checking the user’s role.

* **Example:**  
    JavaScript hides the "Delete User" button for non-admins, but the API still allows the request if called directly.
    

* * *

# 6. Client-Side Only Access Control

Relying solely on front-end restrictions (JavaScript, HTML) instead of enforcing them server-side.

* **Example:**  
    Disabling a menu button in HTML but not blocking the related API endpoint.
    

* * *

# 7. Unrestricted File or Data Access

When users can access files, data, or configurations without checks.

* **Example:**  
    A web server allows browsing `/backup/` containing database dumps.
    

* * *

# 8. Forced Browsing

Manually guessing or brute-forcing URLs or resources that are not linked but still accessible.

* **Example:**  
    Navigating to `/admin/hidden-panel` without authentication.
    

* * *

# Mitigation best practices:

* Enforce **role-based access control (RBAC)** on the server side.

* Always verify user identity and ownership for each request.

* Use **deny-by-default** rules.

* Avoid relying solely on obscurity (e.g., hidden URLs).

* Test using tools like **Burp Suite**, **OWASP ZAP**, or manual parameter tampering.
    

* * *

If you want, I can make you a **table of vulnerabilities + examples + how to test them** so it’s easier to remember for security testing.

