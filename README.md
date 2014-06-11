## Try Yii2 with Vagrant VM + Ansible provisioning

> Tested on Ubuntu Linux host machine. But should work on Windows host too as Ansible is being installed on VM, not on Host.

## Out of the box...

* Ubuntu 14.04 64 bit ( + bulk of system soft like `mc`, `curl`, etc.)
* PHP-FPM 5.5 ( + modules `intl`, `gd`, `xdebug` etc.)
* Nginx 1.6
* MySQL 5.5
* Composer
* phpMyAdmin 4.0
* Adminer 4.1.0
* Redis 2.8 ( + PhpRedis)
* MongoDB 2.6.1 ( + php_mongo)
* PostgreSQL 9.3
* Sqlite 2.8.17
* Memcached 1.4.14 ( + php5_memcached)
* Sphinx 2.1
* Elastic Search 1.2
* CUBRID 9.3
* Imported [Sakila DB](http://dev.mysql.com/doc/sakila/en/) for playing around
* And of course Yii2 Advanced Project template imported
* Local IP loop on Host machine `/etc/hosts` and Virtual hosts in Nginx already set up too !

## Quick start

### Install

* [Virtualbox 4.3+](https://www.virtualbox.org/) + VirtualBox Extension Pack
*  [Vagrant 1.6+](http://www.vagrantup.com/)
additional Vagrant modules (optional, but provide full automation) :

* `vagrant plugin install vagrant-hostsupdater`
* `vagrant plugin install vagrant-vbguest`
* `vagrant plugin install vagrant-cachier`

> You don't need to have Ansible installed on host machine. It will be installed on VM and self-provisioning will be launched. So it is possible to run everything on Windows machine. 

### RUN

* Clone this sources from Git
* Run `vagrant up`.
* It will start VM creation and Provisioning. Could take some time 15-30 min... Drink coffee and get back for complete virtual server with Yi2 project ready for play !

### PLAY

Ok, now if everything went fine you can access these Urls in your browser

* [http://yii2.local/](http://yii2.local/)  -  frontend app
* [http://admin.yii2.local/](http://admin.yii2.local/)  -  backend app
* [http://phpmyadmin.yii2.local/](http://phpmyadmin.yii2.local/) - phpMyAdmin
* [http://adminer.yii2.local/](http://adminer.yii2.local/) - Adminer (Lightweight and simple GUI manager for MySQL, PostgreSQL, SQLite, MS SQL, Oracle, SimpleDB, Elasticsearch and MongoDB)

* Gii code generator should be called like this [http://yii2.local/index.php?r=gii](http://yii2.local/index.php?r=gii)

### Let's make something

* [Go to Gii](http://yii2.local/index.php?r=gii)
* [Go to Model Generator](http://yii2.local/index.php?r=gii/default/view&id=model)

~~~
Input there ...  
Table Name : actor  
Model Class : Actor  
Namespace : frontend\models

Press - Preview and then Generate
~~~

* [Go to CRUD Generator](http://yii2.local/index.php?r=gii/default/view&id=crud)

~~~
Input there ...  
Model Class : frontend\models\Actor  
Search Model Class : frontend\models\ActorSearch  
Controller Class : frontend\controllers\ActorController

Press - Preview and then Generate
~~~

* And now your Actor CRUD page is generated. You can access it here [http://yii2.local/index.php?r=actor](http://yii2.local/index.php?r=actor)
* Continue playing with other Models, modify code (on your host machine in folder `.../try-yii2/yii2-app-advanced`) make relations between Models etc. Whatever you wish!


## Getting deeper ...

* In `try-yii2` folder run `vagrant ssh` to access virtual dev server via SSH. You can modify and setup additionally anything you want.
* Or modify Ansible provisioning YML files (if you are familiar with it) and run `vagrant provision` to update server config (WARNING! I can't guarantee that your changes will not be overwritten!)

## TODO :

#### Complete Ansible provisioning scripts for all software stack Yii2 works out of the box

* Make option for yii-basic-template checkout

### Made by [Evgeniy Kuzminov](http://stdout.in). Thanks for support to [Anton Logvinenko](http://anton.logvinenko.name/).
