
the best way to validate this information is to obtain information directly from a target by port or vulnerability scanning, pinging, sending HTTP requests, making API calls, and other forms of interaction with a target’s environment.


# The Active Recon Process
The active recon process should reveal any weaknesses you can use to access the system.


## Phase Zero: Opportunistic Exploitation
If you discover a vulnerability at any point in the active recon process, you should take the opportunity to attempt exploitation. 

You might discover the vulnerability in the first few seconds of scanning, after stumbling
upon a comment left in a partially developed web page, or after months of research.


## Phase One: Detection Scanning
The goal of detection scanning is to reveal potential ==starting points== for your investigation.

Begin with general scans meant to detect hosts, open ports, services running, and operating systems currently in use.


## Phase Two: Hands-on Analysis
Hands-on analysis is the act of exploring the web application using a browser and API client. 

Aim to learn about all the potential levers you can interact with and test them out. 

Practically speaking, you’ll examine the web page, intercept requests, look for API links and documentation, and develop an understanding of the business logic involved.

You should usually consider the application from three perspectives: 
+ guests:
	+ Guests are anonymous users likely visiting a site for the first time.
+ authenticated users:
	+ Authenticated users have gone through some registration process and have been granted a certain level of access.
+ and site administrators:
	+ Administrators have the privileges to manage and maintain the API.


## Phase Three: Targeted Scanning
In the targeted scanning phase, refine your scans and use tools that are specific to your target. 

Whereas detection scanning casts a wide net, targeted scanning should focus on the specific type of API, its version, the web application type, any service versions discovered, whether the app is on HTTP or `HTTPS`, any active `TCP` ports, and other information gleaned from understanding the business logic.



# Baseline Scanning with `Nmap`
`Nmap` is a powerful tool for scanning ports, searching for vulnerabilities, enumerating services, and discovering live hosts.

For API discovery, you should run two `Nmap` scans in particular: 
+ general detection and all port:
	+ The `Nmap` general detection scan uses default scripts and service enumeration against a target and then saves the output in three formats for later review:
		+ `-oX` for `XML`, 
		+ `-oN` for `Nmap`, 
		+ `-oG` for `greppable`, 
		+ or `-oA` for all three formats.
```
nmap -sC -sV <target address or network range> -oA nameofoutput
```

The `Nmap` all-port scan will quickly check all ==**65,535**== `TCP` ports for running services, application versions, and host operating system in use:
```
nmap -p- <target address> -oA allportscan.txt
```

As soon as the general detection scan begins returning results, kick off the all-port scan. 

Then begin your hands-on analysis of the results. 

You’ll most likely discover APIs by looking at the results related to HTTP traffic and other indications of web servers. 

Typically, you’ll find these running on ports 80 and 443, but an API can be hosted on all sorts of different ports.

Once you discover a web server, open a browser and begin analysis.



# Finding Hidden Paths in `Robots.txt`
Robots.txt is a common text file that tells web crawlers to omit results from the search engine findings. 

Ironically, it also serves to tell us which paths the target wants to keep secret. 

You can find the `robots.txt` file by navigating to the target’s `/robots.txt` directory 
(for example, https://www.twitter.com/robots.txt).



# Finding Sensitive Information with Chrome DevTools

**Snapshot**
With DevTools open, click the Memory tab. 
Under Select Profiling Type, choose Heap Snapshot. 
Then, under Select JavaScript VM Instance, choose the target to review. 
Next, click the Take Snapshot button.
![[Pasted image 20250114071243.png]]

**Performance**
Finally, use the Chrome DevTools Performance tab to record certain actions (such as clicking a button) and review them over a timeline broken down into milliseconds.



# Crawling URIs with OWASP ZAP

https://en.wikipedia.org/wiki/ZAP_(software)
https://www.zaproxy.org/


One of the objectives of active reconnaissance is to discover all of a web page’s directories and files, also known as URIs, or uniform resource identifiers.

There are two approaches to discovering a site’s URIs: ==crawling== and ==brute force==.

OWASP ZAP crawls web pages to discover content by scanning each page for references and links to other web pages.

![[Pasted image 20250114075220.png]]

After the automated scan commences, you can watch the live results using the Spider or Sites tab. 

You may discover API endpoints in these tabs. 

If you do not find any obvious APIs, use the Search tab
![[Pasted image 20250114075548.png]]

Once you’ve found a section of the site you want to investigate more thoroughly, begin manual exploration using the ZAP HUD to interact with the web application’s buttons and user input fields.

While you do this, ZAP will perform additional scans for vulnerabilities. 

Navigate to the Quick Start tab and select Manual Explore



# Brute-Forcing URIs with `Gobuster`

```
sudo apt install gobuster
```

`Gobuster` can be used to **==brute-force==** URIs and DNS subdomains from the command line.

In `Gobuster`, you can use wordlists for common directories and
subdomains to automatically request every item in the wordlist, send the items to a web server, and filter the interesting server responses. 

The results generated from `Gobuster` will provide you with the URL path and the HTTP status response codes.

Kali has directory wordlists stored under 
```
usr/share/wordlists/dirbuster
```
that are thorough but will take some time to complete.

The following example uses an API-specific wordlist to find the directories on an IP address:
```
gobuster dir -u http://192.168.195.132:8000 -w /home/hapihacker/api/wordlists/common_apis_160
```

Once you find API directories like the `/api` directory shown in this output, either by crawling or brute force, you can use Burp to investigate them further. 

`Gobuster` has additional options, and you can list them using the
`-h` option

If you would like to ==ignore== certain response status codes, use the option `-b`. 
If you would like to see additional status codes, use` -x`. 
You could enhance a `Gobuster` search with the following:
```
gobuster dir -u http://targetaddress/ -w /usr/share/wordlists/api_list/common_apis_160 -x
200,202,301 -b 302
```


# Discovering API Content with Kiterunner

The ==**best**== tool available for discovering API endpoints and resources.

While `Gobuster` works well for a quick scan of a web application to
discover URL paths, it typically relies on standard HTTP GET requests.

Kiterunner will not only use all HTTP request methods common with APIs (GET, POST, PUT, and DELETE) but also mimic common API path structures. 

In other words, instead of requesting `GET` `/api/v1/user/create`,
Kiterunner will try `POST` `/api/v1/user/create`, mimicking a more realistic request.
```
kr scan http://192.168.195.132:8090 -w ~/api/wordlists/data/kiterunner/routes-large.kite
```

If you want to use a text wordlist rather than a `.kite` file, use the brute option with the text file of your choice:
```
kr brute <target> -w ~/api/wordlists/data/automated/nameofwordlist.txt
```

If you have many targets, you can save a list of line-separated targets as a text file and use that file as the target.

One of the coolest Kiterunner features is the ability to replay requests.
You will also be able to dissect exactly why that request is interesting.

In order to replay a request, copy the entire line of content into Kiterunner, paste it using the `kb replay` option, and include the wordlist you used:
```
kr kb replay "GET
414 [
183,
7,
8] http://192.168.50.35:8888/api/privatisations/
count 0cf6841b1e7ac8badc6e237ab300a90ca873d571" -w ~/api/wordlists/data/kiterunner/routes-
large.kite
```


