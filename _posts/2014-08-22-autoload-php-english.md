---
layout: post
title: How does the PHP autoload work?
categories:
- PHP
- Development
tags:
- php
- development
- autoloader
status: publish
type: post
published: true
---

I know this issue is kinda old and everybody already wrote something about it,
but I think it's worth to talk about it one more time. This post is for the
PHP beginners :)

PHP source files are just plain text files with the php extension, or not
even it, if you don't want, but using an extension helps people identify the
filetype and also helps text editors and IDEs to know what syntax highlight
to use.

That said, is know that we can use some funcions to include code from other
files in a file we are working on. These are the functions:

- *include*
- *include_once*
- *require*
- *require_once*

Now, imagine we have this file tree:

- classes/
  - User.php
- index.php

In the file *classes/User.php* there is the class *User* and the file
*index.php* is the application's entry point.

If we want to use the class *Users* in index, we should do something like this:

```php
<?php

include "classes/User.php";

$u = new User();
```

No problems so far, it's just one class after all. But if we need four classes
do be loaded:

```php
<?php

include "classes/User.php";
include "classes/Customer.php";
include "classes/Order.php";
include "classes/Invoice.php";

$u = new User();
//...
```

Ok, now it's a boring job to do. Actually, this is a job for the *autoloader*.
This feature does exactly what the name says, it automatically loads a class
when it is needed.

Setting up an autoloader is pretty simple. Just create a funcion that receives
a class name do load and do the inclusion of it's file. Look at this example:

```php
<?php

function my_loader($class)
{
    $file = __DIR__ . "/classes/{$class}.php";

    if (is_file($file)) {
        include $file;
    }
}

spl_autoload_register("my_loader");

$u = new User(); // File will be autoloaded here
```

Simple, right? I created the function *my_loader()* and it receives a class name
to load. Inside the function I created a variable with the full path to the
class' file. Then I just check up if the file exists to include it.

Then I used the *spl_autoload_register()* function to let PHP know that it can
also use my *my_loader()* to find a class.

Cool, right? And pretty simple, too.

Of course this is a pretty simple way to use an autoloader and nowadays
frameworks have their own autoloaders and all you have to do is keep your files
in the right places and everything will just work.

Other well know autoloader is the
[composer's](http://getcomposer.org "Composer's page") autoloader.

There are also the PHP comunity's autoload standards. The most used are
[PSR-0](http://www.php-fig.org/psr/psr-0/)
which is kinda deprecated, and [PSR-4](http://www.php-fig.org/psr/psr-4/),
which is the most recent and accepted standard. So if you want to know how to
load the class *Awesome\\Service\\Twitter*, just check out the *PSR-4* standard.

What about you? Do you have any tips about PHP autoloaders? Share the love in the
comments.

InFog
