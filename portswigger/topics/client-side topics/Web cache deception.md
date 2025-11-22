
# Web cache deception خداع

Web cache deception is a vulnerability that enables an attacker to trick a web cache into storing sensitive, dynamic content. 
It's caused by discrepancies التناقضات between how the cache server and origin server handle requests.

In a web cache deception attack, an attacker persuades يقنع a victim to visit a malicious URL, inducing the victim's browser to make an ambiguous request for sensitive content. 
The cache misinterprets يسيء التفسير this as a request for a static resource and stores the response. 
The attacker can then request the same URL to access the cached response, gaining unauthorized access to private information.


![[Pasted image 20251028122208.png]]

----

