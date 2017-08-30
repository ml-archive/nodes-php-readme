# Setting up a PHP 7 project with Laravel 5.1+

We have 4 generation of PHP applications in Nodes
We expect that Laravels Homestead Vagrant Virtual machine is setup
Else follow [Link](https://github.com/nodes-php/readme/blob/master/Guides/Setup/setup-php7-local-enviroment.md)

### Checkout the project
`git clone URL` in

### Composer install
`composer install`

### Setup .env
[Example of .env](https://github.com/nodes-projects/readme/blob/master/laravel/homestead-env.md)

### Setup site in `Homestead.yaml`

```
sites:
    - map: riide.local-like.st
      to: /var/www/riide/htdocs/public 
      php: "7.0"
```
Note the `to` can be without htdocs

### Setup host file

```
192.168.10.10 riide.local-like.st
```



