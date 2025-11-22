
## Encode data on output

Encoding should be applied directly before user-controllable data is written to a page, because the context you're writing into determines what kind of encoding you need to use. For example, values inside a JavaScript string require a different type of escaping to those in an HTML context.

In an HTML context, you should convert non-whitelisted values into HTML entities:
- `<` converts to: `&lt;`
- `>` converts to: `&gt;`


In a JavaScript string context, non-alphanumeric values should be Unicode-escaped:
- `<` converts to: `\u003c`
- `>` converts to: `\u003e`

Sometimes you'll need to apply multiple layers of encoding, in the correct order. 
For example, to safely embed user input inside an event handler, you need to deal with both the ==JavaScript context and the HTML context==. 
So you need to first ==Unicode-escape the input==, and then ==HTML-encode it==:
```
<a href="#" onclick="x='This string needs two layers of escaping'">test</a>

```



## Validate input on arrival
Examples of input validation include:
- If a user submits a URL that will be returned in responses, validating that it starts with a safe protocol such as HTTP and HTTPS. Otherwise someone might exploit your site with a harmful protocol like `javascript` or `data`.
- If a user supplies a value that it expected to be numeric, validating that the value actually contains an integer.
- Validating that input contains only an expected set of characters.


### Whitelisting vs blacklisting
Input validation should generally employ whitelists rather than blacklists.
Instead of trying to make a list of all harmful protocols (`javascript`, `data`, etc.), simply make a list of safe protocols (HTTP, HTTPS) and disallow anything not on the list.



## How to prevent XSS using a template engine
Many modern websites use server-side template engines such as Twig and Freemarker to embed dynamic content in HTML. 

These typically define their own escaping system. 

For example, in Twig, you can use the `e()` filter, with an argument defining the context:
```
{{ user.firstname | e('html') }}
```

Some other template engines, such as Jinja and React, escape dynamic content by default which effectively prevents most occurrences of XSS.



## How to prevent XSS in PHP
In PHP there is a built-in function to encode entities called `htmlentities`. 

You should call this function to escape your input when inside an HTML context. 

The function should be called with three arguments:
- Your input string.
- `ENT_QUOTES`, which is a flag that specifies all quotes should be encoded.
- The character set, which in most cases should be `UTF-8`.

```php
<?php echo htmlentities($input, ENT_QUOTES, 'UTF-8');?>
```

When in a JavaScript string context, you need to Unicode-escape input as already described.
Unfortunately, ==PHP **doesn't** provide an API to Unicode-escape a string==.



## How to prevent XSS client-side in JavaScript
To escape user input in an HTML context in JavaScript, you need your own HTML encoder because JavaScript doesn't provide an API to encode HTML. 

Here is some example JavaScript code that converts a string to HTML entities:
```js
function htmlEncode(str){
    return String(str).replace(/[^\w. ]/gi, function(c){
        return '&#'+c.charCodeAt(0)+';';
    });
}
```
You would then use this function as follows:
```html
<script>
	document.body.innerHTML = htmlEncode(untrustedValue)
</script>
```

If your input is inside a JavaScript string, you need an encoder that performs Unicode escaping. 
Here is a sample Unicode-encoder:
```js
function jsEscape(str){
    return String(str).replace(/[^\w. ]/gi, function(c){
        return '\\u'+('0000'+c.charCodeAt(0).toString(16)).slice(-4);
    });
}
```
You would then use this function as follows:
```html
<script>
	document.write(
		'<script>x="'+jsEscape(untrustedValue)+'";<\/script>'
	)
</script>

```


## How to prevent XSS in jQuery
The most common form of XSS in jQuery is when you pass user input to a jQuery selector. 

Web developers would often use `location.hash` and pass it to the selector which would cause XSS as jQuery would render the HTML. 

jQuery recognized this issue and patched their selector logic to check if input begins with a hash. 

Now jQuery will only render HTML if the first character is a `<`. 

If you pass untrusted data to the jQuery selector, ensure you correctly escape the value using the `jsEscape` function above.


## Mitigating XSS using content security policy (CSP)
Content security policy (CSP) is the last line of defense against cross-site scripting.
If your XSS prevention fails, you can use CSP to mitigate XSS by restricting what an attacker can do.

CSP lets you control various things, such as whether external scripts can be loaded and whether inline scripts will be executed. 
To deploy CSP you need to include an HTTP response header called `Content-Security-Policy` with a value containing your policy.

An example CSP is as follows:
```http
default-src 'self'; script-src 'self'; object-src 'none'; frame-src 'none'; base-uri 'none';
```
This policy specifies that resources such as images and scripts can only be loaded from the same origin as the main page. 
So even if an attacker can successfully inject an XSS payload they can only load resources from the current origin. 
This greatly reduces the chance that an attacker can exploit the XSS vulnerability.

If you require loading of external resources, ensure you only allow scripts that do not aid an attacker to exploit your site.