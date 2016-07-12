How to implement end user reset password feature:

NOTE: By using the nodes/scaffolding repo, this can be added auto 

* Set your user model in config: 

```
'nodes.api.auth.model'
```

for instance:

```
'model' => Project\Models\Users\User::class,
```

* In your controller inject 

```
Nodes\Api\Auth\ResetPassword\ResetPasswordRepository
```

* In controller method call the following method to send password reset email:

```
$resetPasswordRepository->sendResetPasswordEmail(['email' => $request['email']]);
```

* Install nodes/api package and run:

```
php artisan vendor:publish --provider="Nodes\Api\ServiceProvider" 
```
