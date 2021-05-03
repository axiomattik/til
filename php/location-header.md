# Location Header 

A php header call that uses the 'Location' header is one of two special cases. Unlike standard header calls it implicitly overwrites any non 201 (Created) or 3xx (redirection) status codes with 302 (Found). So:

```
<?php
http_response_code(204);
header("Location: /");
```

Would be something of a mistake and not really make much sense. The client would not receive the 204 status code because, if it did, then the redirect implicated by the 'Location' header would not occur.

However, any of the 3xx headers will be sent so:

```
<?php
http_response_code(303);
header("Location: /");
```

makes sense. The client will receive 303 (See Other).

```
<?php
http_response_code(201);
header("Location: /");
```

also works because 201 (Created) uses the 'Location' header to point to a new resource. In this case, the client probably won't redirect to the resource; it will just know where it is.

Whether or not a header call *should* implicitly overwrite non-compliant status codes is perhaps debatable.


