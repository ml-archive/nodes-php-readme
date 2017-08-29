# Setting up a PHP project

We have 4 generation of PHP applications in Nodes

1) PHP 5.5 CakePHP 2x (Lokalbolig, Ironman)
2) PHP 5.5 Laravel 4.2 (Covington, 2BeFound)
3) PHP 5.5 Laravel 5.0 -> 5.1 packages from private github (Issl5, most others have been updated)
4) PHP 7.0 Laravel 5.1 -> 5.4 public packages

### Projects in generation 1-3 needs to run on 
https://github.com/nodes-projects/ndev-php55-vagrant

git clone the project 
use the nodes command to "fix project" which sets up apache config and database

### Projects in generation 4 can run on 
https://laravel.com/docs/5.4/homestead

Follow the guide to homestead

Notes:

VirtualBox 5.1 is preffered

ex of .yaml file with mapping to old urls (local-like.st)
```
---
ip: "192.168.10.10"
memory: 4096
cpus: 2
provider: virtualbox

authorize: ~/.ssh/id_rsa.pub

keys:
    - ~/.ssh/id_rsa

folders:
    - map: ~/nodes-projects
      to: /var/www

sites:
    - map: riide.local-like.st
      to: /var/www/riide/htdocs/public

databases:
    - homestead

# blackfire:
#     - id: foo
#       token: bar
#       client-id: foo
#       client-token: bar

# ports:
#     - send: 50000
#       to: 5000
#     - send: 7777
#       to: 777
#       protocol: udp

```

Note: if you have the Nodes forked homestead, it works fine also [private file sorry]
https://github.com/nodes-cloud/homestead

### .env
Needing .env file [private file sorry]
https://github.com/nodes-projects/readme/blob/master/laravel/env.md

