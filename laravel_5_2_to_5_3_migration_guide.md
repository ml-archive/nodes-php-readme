### Migrate project from Laravel 5.2.* to 5.3.*

#
 Most projects can be migrated in 1h, so do it!


#### Require new laravel packages:
`laravel/framework": "5.3.*`
`laravelcollective/html": "5.3.*`

##### Update: 

```shell
-> composer update
```

**NB: Composer update will fail**

#### Update providers
##### Remove boot() param in `app/Providers/EventServiceProvider.php`

```php
    /**
     * Register any other events for your application.
     *
     * @return void
     */
    public function boot()
    {
        parent::boot();
    }
```

##### Remove boot() param in `app/Providers/RouteServiceProvider.php`

```php
    /**
     * Define your route model bindings, pattern filters, etc.
     *
     */
    public function boot()
    {
        parent::boot();
    }
```

##### Update
```shell
-> composer update
```

#### Additional notes
 - If you are still using an Mcrypt based cipher in your config/app.php configuration file, you should update the cipher to AES-256-CBC and set your key to a random 32 byte string which may be securely generated using php artisan key:generate.
 - Changed all queue closures to dispatch(new MyJob())
 - The old “sometimes” validation rule for fields that can be null, no longer works. It should be changed to “nullable".
 - Mail::send is a void, so don't check the return of that anymore
 - If you are using the Maatwebsite/Laravel-Excel package (https://github.com/Maatwebsite/Laravel-Excel) for handling import and export of excel/csv files you need to remove the LaravelCollective/bus package required by the laravel 5.2 branch. Simply remove the provider in config/app.php
 
```php
/**
 * Excel
 */
// Collective\Bus\BusServiceProvider::class,
Maatwebsite\Excel\ExcelServiceProvider::class,
```

```shell
-> composer remove laravelcollective/bus
```
