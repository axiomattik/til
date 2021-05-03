# PHP Router Script

PHP's built-in web server can be provided with a file to use as a router for requests.

`php -S localhost:8000 router.php`

And the value of `$_SERVER['REQUEST_URI']` can then be used in, say, a switch statement in order to determine what the server does. For example:

```
<?php
// router.php

switch $_SERVER['REQUEST_URI'] {
	case '/':
		require 'templates/index.php';
		break;
	default:
		http_response_code(404);
		require 'templates/404.php';
		break;
}
```

However, if the `templates/index.php` contains, as one might expect, anything that makes a further request to the server, such as a link tag for a stylesheet, that request will also be subject to `router.php`.

So even if we have a directory structure that looks like:

```
.
├── assets
│   └── css
│       └── style.css
├── templates
│   ├── 404.php
│   └── index.php
└── router.php
```

A request made in `templates/index.php` by a tag like `<link rel="stylesheet" href="/assets/css/style.css">`, which refers to an existent static file, will receive a 404 response.

To prevent this and allow `router.php` to serve static files (without having to laboriously add a route for each one—which I definitely didn't start to do), we can add the following check to the top of `router.php`:

```<?php
// router.php
if (preg_match('/\.(?:png|jpg|jpeg|gif)$/', $_SERVER["REQUEST_URI"])) {
    return false;    // serve the requested resource as-is.
}
```

Obviously this shouldn't be done in production.

Oh, and this is already made quite clear in the [manual](https://www.php.net/manual/en/features.commandline.webserver.php).

