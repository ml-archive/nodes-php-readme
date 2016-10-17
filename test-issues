## Middleware not loaded during tests

If you have custom middleware on a project, and you are running tests, you will face something like: 

`Class 'riide.api' not found`

There is an issue with Dingo that's causing this, and the quick workaround is simple:

- Go to config/app.php
- Find the service providers
- Load the `Nodes\Api\ServiceProvider::class` **JUST BEFORE** the `App\Providers\RouteServiceProvider::class`

This will solve the issue.
