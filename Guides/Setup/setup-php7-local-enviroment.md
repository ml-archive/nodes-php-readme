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

Ex of Homestead.yaml
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
    - map: pma.local-like.st
      to: /var/www/phpmyadmin

    - map: riide.local-like.st
      to: /var/www/riide/htdocs/public
      php: "7.0"

databases:
    - homestead
```

password for the mysql on homestead is
u: homestead
p: secret

[Link to .env](https://github.com/nodes-projects/readme/blob/master/laravel/homestead-env.md)

Ex of .hosts file
```
192.168.10.10 riide.local-like.st
192.168.10.10 pma.local-like.st
```

Install PMA
```
PMA_VERSION=4.6.6 && cd /var/www && wget https://files.phpmyadmin.net/phpMyAdmin/$PMA_VERSION/phpMyAdmin-$PMA_VERSION-all-languages.zip && unzip phpMyAdmin-*-all-languages.zip && mv phpMyAdmin-*-all-languages phpmyadmin && rm ./phpMyAdmin-*-all-languages.zip
```

Install tig
```
sudo apt-get install tig
```

Install gitflow
```
sudo apt-get install git-flow
```

Install missing php extensions

_php5_
```
sudo apt-get install php5.6-mcrypt php5.6-mbstring php5.6-json php5.6-mysql php5.6-opcache php5.6-common php5.6-readline php5.6-curl php5.6-dev php5.6-zip php5.6-soap php5.6-redis -y
```

_php7_
```
sudo apt-get install php7.0 php7.0-mcrypt php7.0-mbstring php7.0-json php7.0-mysql php7.0-opcache php7.0-common php7.0-readline php7.0-curl php7.0-dev php7.0-zip php7.0-soap php7.0-xml -y
```

#### Nodes homestead - Apache instead of NGinx (Deprecated)
[Guide](https://github.com/nodes-cloud/homestead)

[Link to .env](https://github.com/nodes-projects/readme/blob/master/laravel/nhomestead-env-deprecated)



