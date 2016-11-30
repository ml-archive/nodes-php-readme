After running nodes create project follow these steps to setup rest of you project

### Get project running
- Add the project to your hosts file (192.168.10.15 demo.local-like.st)
- pa key:generate (will generate the APP_KEY in your env file, remember to add this to nstack.like.st)

Project is now running!

###Setup composer
#### Minimum requirements
- https://github.com/nodes-php/core
- https://github.com/nodes-php/bugsnag
- Add following to config/app.php
```
  /**
   * Orchestra Service Providers
   */
  Orchestra\Debug\DebugServiceProvider::class,
  Orchestra\Debug\CommandServiceProvider::class,
  
  /**
   * IDE helper
   */
  
  Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class,
```
- dump
- pa debug (now works, to check your sql queries in runtime, use full tool always use it)
- php artisan vendor:publish --provider="Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider" --tag=config (publish ide-helper config)
- change ide-helper.php in /config (since our models are never in app/models)
```
  'model_locations' => array(
      'project/Models',
  ),
```

#### Setup Backend
- https://github.com/nodes-php/backend

#### Setup Api
 - There can be issues with composer require, you can try to add it manually, and above laravel in composer, can help:)
 - https://github.com/nodes-php/api
 - API scaffolding is located in it's own repository: https://github.com/nodes-php/api-scaffolding (see docs on repository on how to execute the scaffolding commands)
 
#### Setup CORS for web projects
 - Follow the instructions in [the CORS guide](https://github.com/nodes-php/readme/blob/master/Guides/cors.md)
 
#### .gitignore
```
.idea/
/vendor
/node_modules
/bower_components
Homestead.yaml
Homestead.json
.env

tests/_output/*
storage/framework/browscap/*
storage/exports/*
```

##### Add global .gitignore file to your git configuration
```
git config --global core.excludesfile '~/path/to/.gitignore'
```
=======
####Set up backend, using cache, validation, database & assets
- https://github.com/nodes-php/backend
