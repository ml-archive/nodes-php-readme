# Cors

For all web projects setting up CORS is needed for browsers to communicate with APIS located on a different domain

Setup this plugin:
https://github.com/barryvdh/laravel-cors

## 1) composer require

## 2) Setup Service provider

## 3) Copy config

Consider using widcares in all configs ['*'] to make it as easy as possible
```
<?php

return [
    /*
     |--------------------------------------------------------------------------
     | Laravel CORS
     |--------------------------------------------------------------------------
     |

     | allowedOrigins, allowedHeaders and allowedMethods can be set to array('*')
     | to accept any value.
     |
     */
    'supportsCredentials' => false,
    'allowedOrigins' => ['*'],
    'allowedHeaders' => ['*'],
    'allowedMethods' => ['*'],
    'exposedHeaders' => [],
    'maxAge' => 0,
    'hosts' => [],
];

```

## 4) Setup middleware

Global middleware is the easist solution, else if you have a api group

in app/Http/Kernel.php
```
protected $middleware = [
    \Barryvdh\Cors\HandleCors::class
];
```
## 5) Test
[Native js cors tester](http://codepen.io/dennishn/pen/BLbYyJ)
