After running nodes create project follow these steps to setup rest of you project

### Get project running
- Add the project to your hosts file (192.168.10.15 demo.local-like.st)
- Run vagrant provisining (will load the project on your vagrant)
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
