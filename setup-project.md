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

Follow the guide to setup projects

VirtualBox 5.1 is preffered

Note: if you have the Nodes forked homestead, it works fine also [private file sorry]
https://github.com/nodes-cloud/homestead

### .env
Needing .env file [private file sorry]
https://github.com/nodes-projects/readme/blob/master/laravel/env.md

