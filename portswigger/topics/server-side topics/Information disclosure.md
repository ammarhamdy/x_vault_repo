

# Information disclosure vulnerabilities

Learning to find and exploit information disclosure is a vital skill for any tester.

----

# What is information disclosure?

Information disclosure, also known as information leakage, is when a website unintentionally reveals sensitive information to its users. 

Depending on the context, websites may leak all kinds of information to a potential attacker, including:
- Data about other users, such as usernames or financial information
- Sensitive commercial or business data
- Technical details about the website and its infrastructure

----

# Examples of information disclosure

Some basic examples of information disclosure are as follows:

- Revealing the names of hidden directories, their structure, and their contents via a `robots.txt` file or directory listing

- Providing access to source code files via temporary backups

- Explicitly mentioning database table or column names in error messages

- Unnecessarily (بلا داعٍ) exposing highly sensitive information, such as credit card details

- Hard-coding API keys, IP addresses, database credentials, and so on in the source code

- Hinting at the existence or absence of resources, usernames, and so on via subtle differences in application behavior

----

# How do information disclosure vulnerabilities arise?

Information disclosure vulnerabilities can arise in countless different ways, but these can broadly be categorized as follows:

**Failure to remove internal content from public content**. 
For example, developer comments in markup are sometimes visible to users in the production environment.

**Insecure configuration of the website and related technologies**. 
For example, failing to disable debugging and diagnostic features can sometimes provide attackers with useful tools to help them obtain sensitive information.
Default configurations can also leave websites vulnerable, for example, by displaying overly verbose error messages.

**Flawed design and behavior of the application**. 
For example, if a website returns distinct (متميز) responses when different error states occur, this can also allow attackers to [enumerate sensitive data](https://portswigger.net/web-security/authentication/password-based#username-enumeration), such as valid user credentials.

---

# How to test for information disclosure vulnerabilities

Generally speaking, it is important not to develop "tunnel vision" during testing. 
In other words, you should avoid focussing too narrowly on a particular vulnerability. 

Sensitive data can be leaked in all kinds of places, so it is important not to miss anything that could be useful later. 

You will often find sensitive data while testing for something else. 

A key skill is being able to recognize interesting information whenever and wherever you do come across it.

The following are some examples of high-level techniques and tools that you can use to help identify information disclosure vulnerabilities during testing.
- [Fuzzing](https://portswigger.net/web-security/information-disclosure/exploiting#fuzzing)
- [Using Burp Scanner](https://portswigger.net/web-security/information-disclosure/exploiting#using-burp-scanner)
- [Using Burp's engagement tools](https://portswigger.net/web-security/information-disclosure/exploiting#using-burp-s-engagement-tools)
- [Engineering informative responses](https://portswigger.net/web-security/information-disclosure/exploiting#engineering-informative-responses)

---

## Common sources of information disclosure

Information disclosure can occur in a wide variety of contexts within a website. 

The following are some common examples of places where you can look to see if sensitive information is exposed.
- [Files for web crawlers](https://portswigger.net/web-security/information-disclosure/exploiting#files-for-web-crawlers)
- [Directory listings](https://portswigger.net/web-security/information-disclosure/exploiting#directory-listings)
- [Developer comments](https://portswigger.net/web-security/information-disclosure/exploiting#developer-comments)
- [Error messages](https://portswigger.net/web-security/information-disclosure/exploiting#error-messages) LABS
- [Debugging data](https://portswigger.net/web-security/information-disclosure/exploiting#debugging-data) LABS
- [User account pages](https://portswigger.net/web-security/information-disclosure/exploiting#user-account-pages) LABS
- [Backup files](https://portswigger.net/web-security/information-disclosure/exploiting#source-code-disclosure-via-backup-files) LABS
- [Insecure configuration](https://portswigger.net/web-security/information-disclosure/exploiting#information-disclosure-due-to-insecure-configuration) LABS
- [Version control history](https://portswigger.net/web-security/information-disclosure/exploiting#version-control-history) LABS

## Files for web crawlers

Many websites provide files at `/robots.txt` and `/sitemap.xml` to help crawlers navigate their site. 
Among other things, these files often list specific directories that the crawlers should skip, for example, because they may contain sensitive information.

## Source code disclosure via backup files

Obtaining source code access makes it much easier for an attacker to understand the application's behavior and construct high-severity attacks. 

Sensitive data is sometimes even hard-coded within the source code.

Typical examples of this include API keys and credentials for accessing back-end components.

If you can identify that a particular open-source technology is being used, this provides easy access to a limited amount of source code.

Occasionally أحياناً, it is even possible to cause the website to expose its own source code. 

When mapping out a website, you might find that some source code files are referenced explicitly. 

Unfortunately, requesting them does not usually reveal the code itself. 

When a server handles files with a particular extension, such as `.php`, ==it will typically execute the code, rather than simply sending it to the client as text==. 

However, in some situations, ==you can trick a website into returning the contents of the file instead==. 

For example, text editors often generate temporary backup files while the original file is being edited. 

These temporary files are usually indicated in some way, such as by appending a tilde (`~`) to the filename or adding a different file extension.

Requesting a code file using a backup file extension can sometimes allow you to read the contents of the file in the response.

## Information disclosure due to insecure configuration

Developers might forget to disable various debugging options in the production environment. 

For example, the HTTP `TRACE` method is designed for diagnostic purposes. 

If enabled, the web server will respond to requests that use the `TRACE` method by echoing in the response the exact request that was received. 

This behavior is often harmless, but occasionally leads to information disclosure, such as the name of internal authentication headers that may be appended to requests by reverse proxies.

### HTTP trace method

The **HTTP TRACE** method is one of the lesser-known HTTP request methods. 

It’s primarily used for **diagnostic purposes**, ==allowing the client to see what is being received at the other end of the request chain==.

When a client sends a TRACE request to a server:
- The server **==reflects the request==** back to the client exactly as it received it.
- This allows the client to examine what changes (if any) were made to the request by intermediate servers (like proxies or gateways).

**Example**
```http
TRACE /example HTTP/1.1
Host: example.com
```
If the server supports TRACE, it might respond with:
```http
HTTP/1.1 200 OK
Content-Type: message/http

TRACE /example HTTP/1.1
Host: example.com
```

### Lab: Authentication bypass via information disclosure

In Burp Repeater, browse to `GET /admin`.
Send the request again, but this time use the `TRACE` method (not GET method):
```http
Trace /admin
```
https://www.youtube.com/watch?v=Hta21EADKqw&t=529s

## Version control history

Virtually all websites are developed using some form of version control system, such as Git. 
By default, a Git project stores all of its version control data in a folder called `.git`. 

Occasionally أحياناً, websites expose this directory in the production environment. 
In this case, you might be able to access it by simply browsing to `/.git`.

---


