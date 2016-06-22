After running nodes create project follow these steps to setup rest of you project

### Get project running
- Add the project to your hosts file (192.168.10.15 demo.local-like.st)
- pa key:generate (will generate the APP_KEY in your env file, remember to add this to nstack.like.st)

Project is now running!

###Setup composer
#### Minimum requirements
- https://github.com/nodes-php/core
- https://github.com/nodes-php/bugsnag
- Add to .env BUGSNAG_API_KEY=NO (Will make sure bugsnag is not crashing local, this env will be set when pushing live)
- Add following to config/app.php
```
  /**
   * Orchesra Service Providers
   */
  Orchestra\Debug\DebugServiceProvider::class,
  Orchestra\Debug\CommandServiceProvider::class,
  
  /**
   * IDE helper
   */
  
  Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class,
```
- pa dump
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
 - Right now all the scaffolding is disabled for API. But you can find the files in the vendor/nodes/api - Morten is working on getting the command up again, else take it from another project 
 
#### .gitignore
```
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
