
PHP was created in 1994 and is one of the foundational technologies of modern web development. 

Given all the new technologies used today, is there still a place for PHP? 
PHP remains one of the widest used server-side technologies on the internet.

PHP contains built-in functionality for interacting with web data, _Vanilla PHP_, or PHP without any other tools, can be used on its own to create web application back-ends. 

But we don’t have to reinvent the wheel every time! Once we’re comfortable with the basics of the PHP language, we have our pick of powerful PHP frameworks to choose from! These frameworks provide scaffolding and solutions to common problems in back-end web development. 

Some popular PHP frameworks are [`Laravel`](https://laravel.com/), [`CakePHP`](https://cakephp.org/), and [`Symfony`](https://symfony.com/).


---

# Install PHP
```sh
sudo apt install php-cli
```

# Write a PHP file
```sh
<?php
echo "Hello, Ubuntu!\n";
?>
```
**Run your PHP script**
```sh
php hello.php
```

# Run PHP with a local web server

If you want to test PHP in a browser:
1. Install PHP and its built-in web server (already included in `php-cli`).
2. Go to your project folder and start a PHP server::
```sh
php -S localhost:8000
```
3. Open your browser and visit: http://localhost:8000/hello.php


---

# PHP echo

In order to create this dynamic behavior, PHP was designed to work closely with HTML. 

PHP can be used directly in-line with an HTML document.

When the web site is delivered from the back-end to the front-end, the PHP content is executed and added to the HTML to form one HTML document. 

The start of in-line PHP is denoted with `<?php` and the end is denoted with `?>`.

```php
<p>This HTML will get delivered as is</p>
<?php echo "<p>But this code is interpreted by PHP and turned into HTML</p>";?>
```

In PHP, the `echo` keyword is used to output text. The text in this case is everything between the double quotes (`"`). 

An instruction written in PHP is called a _statement_. A semicolon (`;`) is required at the end of each statement in PHP.


---

# How is PHP Executed?

PHP is flexible and can also be executed from the terminal. 

We can use PHP as a general purpose programming language to write programs that give simple instructions to the computer without involving HTML or the web.

When writing a PHP script file, we still need to denote that we are beginning our PHP code using `<?php`, but the closing tag is no longer required.

Unlike many other languages, PHP is not always case-sensitive, so `Echo` is a valid statement in PHP.

However, it’s best practice to use standard casing – in this case, `echo`.

---
