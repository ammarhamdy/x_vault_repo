
# Kali Linux

https://www.kali.org/docs/installation.

install Git, Python 3, and Golang (Go), which you’ll need to use
some of the other tools in your hacking box:
```
$ sudo apt-get install git python3 golang
```



# Analyzing Web Apps with DevTools


## DevTools Panels

**Elements** 
Allows you to view the current page’s CSS and Document Object
Model (DOM), which enables you to inspect the HTML that constructs the web page.

**Console**
Provides you with alerts and lets you interact with the JavaScript
debugger to alter the current web page.

**Sources**
Contains the directories that make up the web application and the
content of the source files.

**Network**
Lists all the source file requests that make up the client’s perspective of the web application.

**Performance**
Provides a way to record and analyze all the events that take place
when loading a web page.

**Memory**
Lets you record and analyze how the browser is interacting with your system’s memory.

**Application**
Provides you with the application manifest, storage items (like **cookies** and session information), cache, and background services.

**Security**
Provides insight regarding the transit encryption, source content origins, and certificate details.

For more information about DevTools, check out the Google Developers documentation at:
https://developers.google.com/web/tools/chrome-devtools.



# Capturing and Modifying Requests with Burp Suite

Burp Suite is a magnificent set of web application–testing tools developed and continuously improved on by `PortSwigger`. 

All web app cybersecurity professionals, bug bounty hunters, and API hackers should learn to use Burp, which allows you to 
+ capture API requests, 
+ spider web applications, 
+ fuzz APIs, 
+ and so much more.

## Spidering, or web crawling

Spidering, or web crawling, is a method that bots use to automatically detect the URL paths and resources of a host. 

Typically, spidering is done by scanning the HTML of web pages for hyperlinks. Spidering is a good way to get a basic idea of the contents of a web page, but it won’t be able to find hidden paths, or the ones that do not have links found within web pages. 

To find hidden paths, we’ll need to use a tool like **`Kiterunner`** that effectively performs directory brute-force attacks. 

In such an attack, an application will request various possible URL  paths and validate whether they actually exist based on the host’s responses.


visit:
https://portswigger.net/burp/communitydownload.
https://portswigger.net/web-security/getting-started.



# Setting Up FoxyProxy

One of Burp Suite’s key features is the ability to intercept HTTP requests.

In other words, Burp Suite receives your requests before forwarding them to the server and then receives the server’s responses before sending them to the browser, allowing you to view and interact with those requests and responses. 

For this feature to work, we’ll need to regularly send requests from the browser to Burp Suite. 
This is done with the use of a web proxy.

The proxy is a way for us to reroute web browser traffic to Burp before it is sent to the API provider. 

To simplify this process, we’ll add a tool called `FoxyProxy` to our browsers to help us proxy traffic with a click of a button.

We’ll use a browser add-on called `FoxyProxy` that lets you switch your proxy on and off with a simple click of a button.



# Adding the Burp Suite Certificate

==**HTTP Strict Transport Security (HSTS)**== is a common web application security policy that prevents Burp Suite from being able to intercept requests.

Whether using Burp Suite CE or Burp Suite Pro, you will need to install Burp Suite’s certificate authority (CA) certificate. 

To add this certificate, follow these steps:

1. Start Burp Suite.
2. Open your browser of choice.
3. Using FoxyProxy, select the Hackz proxy. 
	+ Navigate to http://burpsuite, 
	+ and click CA Certificate. 
	+ This will initiate the download of the Burp Suite CA certificate.
4. Save the certificate somewhere you can find it.
5. Open your browser and import the certificate.

![[Pasted image 20250105080649.png]]

Now that you have the PortSwigger CA certificate added to your
browser, you should be able to intercept traffic without experiencing issues.



# Navigating Burp Suite

**Dashboard**
The Dashboard gives you an overview of the event log and scans you have run against your targets.


**Target**
In the Target tab, we can see a **==site’s map==** and manage the targets we intend to attack. 

You can also use this tab to configure the **==scope==** of your testing by selecting the Scope tab and including or excluding URLs.

Including URLs within scope will limit the URLs being attacked to only those you have authorization to attack.

While using the Target tab, you should be able to locate the Site Map, where you can see all the URLs Burp Suite has detected during your current Burp Suite session.

As you perform scans, crawl, and proxy traffic, Burp Suite will start compiling a list of the target web applications and discovered directories.


**Proxy**
The Proxy tab is where we will begin capturing requests and responses from your web browser and Postman.

From Proxy we will forward the request or response to other modules for interaction and [tampering](https://translate.google.com/?sl=en&tl=ar&text=tampering&op=translate).


**Intruder**
The Intruder tab is where we’ll perform fuzzing and brute-force attacks against web applications. 

Once you’ve captured an HTTP request, you can forward it to Intruder, where you can select the exact parts of the request that you want to replace with the payload of your choice before  ending it to the server.


**Repeater**
The Repeater is a module that lets you make hands-on djustments to HTTP requests, send them to the targeted web server, and  analyze the content of the HTTP response.


**Sequencer**
The Sequencer tool will ==automatically== send hundreds of requests and then perform an analysis of [entropy](https://translate.google.com/?sl=en&tl=ar&text=entropy&op=translate) to determine how random a given string is.

==We will primarily use this tool to analyze whether cookies, tokens,
keys, and other parameters are actually random.==


**Decoder**
The Decoder is a quick way to encode and decode HTML, base64, ASCII hex, hexadecimal, octal, binary, and Gzip.


**Comparer**
The Comparer can be used to compare different requests. 

Most often, ==you’ll want to compare two similar requests and find the sections of the request that have been removed, added, and modified.==



# Intercepting Traffic

Start Burp Suite and change the Intercept option to Intercept is on

In your browser, select the Hackz proxy using FoxyProxy and browse to your target, such as https://twitter.com
This web page will not load in the browser because it was never sent to the server; instead, the request should be waiting for you in Burp Suite.

In Burp Suite, you should see something much like:
![[Pasted image 20250105094702.png]]
This should let you know that you’ve successfully intercepted an HTTP request.

==Once you’ve captured a request, you can select an action to perform with it, such as forwarding the intercepted request to the various Burp Suite modules.==

The Repeater module is the best way to see how a web server responds to a single request. 

This is useful for seeing what sort of response you can expect to get from an API before initiating an attack. 

It’s also helpful when you need to make minor changes to a request and want to see how the server responds.



# Altering Requests with Intruder

==We’ve already mentioned that Intruder is a web application fuzzing and scanning tool==.

It works by letting you create variables within an intercepted HTTP request, replace those variables with different sets of payloads, and send a series of requests to an API provider.

Any part of a captured HTTP request can be transformed into a variable, or attack position, by surrounding it with `§` symbols.

Payloads can be anything from a word-list to a set of numbers, symbols, and any other type of input that will help you test how an API provider will respond.

![[Pasted image 20250105101056.png]]


Based on the payload list shown here, Intruder will perform one
request per payload listed for a total of 5 requests.

When an attack is started, each of the strings under Payload Options will replace **`+741+741`** in turn and generate a request to the API provider.

The Intruder attack types determine how the payloads are processed.

As you can see:
![[Pasted image 20250105101330.png]]
there are four different attack types: 
+ **sniper**,
+ [battering ram](https://translate.google.com/?sl=en&tl=ar&text=battering%20ram&op=translate), 
+ [pitchfork](https://translate.google.com/?sl=en&tl=ar&text=pitchfork&op=translate), 
+ and [cluster bomb](https://translate.google.com/?sl=en&tl=ar&text=cluster%20bomb&op=translate).

**Sniper attack**
Sniper is the simplest attack type; it replaces the added attack position with a string provided from a single set of payloads. 

A sniper attack is limited to using a single payload, but it can have several attack positions.

A sniper attack will replace one attack position per request, cycling through the different attack positions in each request. 

If you were attacking three different variables with a single payload, it would look something like this:
```
§Variable1§, §variable2§, §variable3§

Request 1: Payload1, variable2, variable3
Request 2: Variable1, payload1, variable3
Request 3: Variable1, variable2, payload1
```

**Battering ram**
Battering ram is like the sniper attack in that it also uses one payload, but it will use that payload across all attack positions in a request. 

If you were testing for SQL injection across several input positions within a request, you could fuzz them all simultaneously with battering ram.

**Pitchfork**
Pitchfork is used for testing multiple payload combinations at the same time. 

For example, if you have a list of leaked usernames and password combinations, you could use two payloads together to test whether any of the credentials were used with the application being tested. 

However, this attack doesn’t try out different combinations of payloads; it will only cycle through the payload sets like this: 
```
user1:pass1, user2:pass2, user3:pass3
```


**Cluster bomb**
Cluster bomb will cycle through all possible combinations of the payloads provided. 

If you provide two usernames and three passwords, the payloads
would be used in the following pairs: 
```
user1:pass1, 
user1:pass2, 
user1:pass3,
user2:pass1, 
user2:pass2, 
user2:pass3.
```


## Choice attack type

The attack type to use depends on your situation.

If you’re fuzzing a single attack position, use sniper. 

If you’re fuzzing several attack positions at once, use battering ram. 

When you need to test set combinations of pay loads, use pitchfork. 

For password-spraying efforts, use cluster bomb.


## Intruder very help

Intruder should help you find API vulnerabilities such as broken object level authorization, excessive data exposure, broken authentication, broken function level authorization, mass assignment, injection, and improper assets management. 

Intruder is essentially a smart fuzzing tool that provides a list
of results containing the individual requests and responses. 

You can interact with the request you’d like to fuzz and replace the attack position with the input of your choice. 

==These API vulnerabilities are typically discovered by sending the right payload to the right location.==



# EXTENDING THE POWER OF BURP SUITE

One of the major benefits of Burp Suite is that you can install custom extensions.

To install extensions, use the search bar to find the one you’re looking for and then click the Install button. 

Some extensions require additional resources and have more complex installation requirements. 

Make sure you follow the install instructions for each extension. 

I recommend adding the following ones.

## `AUTORIZE`

`Autorize` is an extension that helps automate authorization testing, particularly for BOLA vulnerabilities. 

You can add the tokens of `UserA` and `UserB` accounts and then perform a bunch of actions to create and interact with resources as `UserA`. 

Also, `Autorize` can automatically attempt to interact with `UserA`’s resources with the `UserB` account. 

`Autorize` will highlight any interesting requests that may be vulnerable to BOLA.


## `JSON WEB TOKENS`

The JSON Web Tokens extension helps you dissect and attack JSON Web Tokens.


## `InQL SCANNER`

`InQL` is an extension that will aid us in our attacks against GraphQL APIs.

## `IP ROTATE`

IP Rotate allows you to alter the IP address you are attacking from to indicate different cloud hosts in different regions. 

This is extremely useful against API providers that simply block attacks based on IP address.


## `BYPASS WAF`

The WAF Bypass extension adds some basic headers to your requests in order to bypass some web application firewalls (WAFs). 

Some WAFs can be tricked by the inclusion of certain IP headers in the request. 

WAF Bypass saves you from manually adding headers such as 
+ `X-Originating-IP`, 
+ `X-Forwarded-For`,
+ `X-Remote-IP`, 
+ and `X-Remote-Addr`. 
 
These headers normally include an IP address, and you can specify an address that you believe to be permitted, such as the
target’s external IP address (127.0.0.1) or an address you suspect to be trusted.


To learn more about Burp Suite, visit the `PortSwigger` `WebSecurity` Academy at: 
https://portswigger.net/web-security 
or consult the Burp Suite documentation at 
https://portswigger.net/burp/documentation.


