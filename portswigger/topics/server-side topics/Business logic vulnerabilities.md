

**Users won't always supply mandatory input**

One misconception is that users will always supply values for mandatory input fields. 

Browsers may prevent ordinary users from submitting a form without a required input, but as we know, attackers can tamper with parameters in transit. 

This even extends to removing parameters entirely.

In this case, the presence or absence of a particular parameter may determine which code is executed. 

Removing parameter values may allow an attacker to access code paths that are supposed to be out of reach.

When probing for logic flaws, you should try removing each parameter in turn and observing what effect this has on the response. 
You should make sure to:

- Only remove one parameter at a time to ensure all relevant code paths are reached.
- Try deleting the name of the parameter as well as the value. The server will typically handle both cases differently.
- Follow multi-stage processes through to completion. Sometimes tampering with a parameter in one step will have an effect on another step further along in the workflow.

---


Making assumptions about the sequence of events can lead to a wide range of issues even within the same workflow or functionality. 

Using tools like Burp Proxy and Repeater, once an attacker has seen a request, they can replay it at will and use forced browsing to perform any interactions with the server in any order they want.

For example, you might skip certain steps, access a single step more than once, return to earlier steps, and so on. 

==Take note of how different steps are accessed.==

Although you often just submit a `GET` or `POST` request to a specific URL, sometimes you can access steps by submitting different sets of parameters to the same URL. 

As with all logic flaws, try to identify what assumptions the developers have made and where the attack surface lies. 

You can then look for ways of violating (انتهاك) these assumptions.


---

# Domain-specific flaws

In many cases, you will encounter logic flaws that are specific to the business domain or the purpose of the site.

The ==discounting functionality== of online shops is a classic attack surface when hunting for logic flaws. 
This can be a potential gold mine for an attacker, with all kinds of basic logic flaws occurring in the way discounts are applied.

**For example**, consider an online shop that offers a 10% discount on orders over $1000. 

This could be vulnerable to abuse if the business logic fails to check whether the order was changed after the discount is applied.

In this case, an attacker could simply add items to their cart until they hit the $1000 threshold, then remove the items they don't want before placing the order. 

They would then receive the discount on their order even though it no longer satisfies the ==intended criteria==.


To identify these vulnerabilities, you need to think carefully about what objectives an attacker might have and try to find different ways of achieving this using the provided functionality.

This may require a certain level of domain-specific knowledge in order to understand what might be advantageous in a given context. 

To use a simple example, you need to understand social media to understand the benefits of forcing a large number of users to follow you.


Without this knowledge of the domain, you may dismiss dangerous behavior because you simply aren't aware of its potential knock-on effects. 

Likewise, you may struggle to join the dots and notice how two functions can be combined in a harmful way. 
For simplicity, the examples used in this topic are specific to a domain that all users will already be familiar with, namely an online shop. 

However, whether you're bug bounty hunting, pen-testing, or even just a developer trying to write more secure code, you may at some point encounter applications from less familiar domains. 
In this case, you should read as much documentation as possible and, where available, talk to subject-matter experts from the domain to get their insight. 
This may sound like a lot of work, but the more obscure the domain is, the more likely other testers will have missed plenty of bugs.


---

# Providing an encryption oracle

Dangerous scenarios can occur when user-controllable input is encrypted and the resulting ciphertext is then made available to the user in some way. 


This kind of input is sometimes known as an "encryption oracle". 

An attacker can use this input to encrypt arbitrary data using the correct algorithm and asymmetric key.

This becomes dangerous when there are other user-controllable inputs in the application that expect data encrypted with the same algorithm. 

In this case, an attacker could potentially use the encryption oracle to generate valid, encrypted input and then pass it into other sensitive functions.


This issue can be compounded if there is another user-controllable input on the site that provides the reverse function. 

This would enable the attacker to decrypt other data to identify the expected structure. 

This saves them some of the work involved in creating their malicious data but is not necessarily required to craft a successful exploit.



-----

# Authentication bypass via encryption oracle

https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-authentication-bypass-via-encryption-oracle


