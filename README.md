## Try Yii2 with Vagrant VM + Ansible provisioning

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
* Imported [Sakila DB](http://dev.mysql.com/doc/sakila/en/) for playing around
* And of course Yii2 Advanced Project template imported
* Local IP loop on Host machine `/etc/hosts` and Virtual hosts in Nginx already set up too !

## Quick start

### Install

* [Virtualbox 4.3+](https://www.virtualbox.org/) + VirtualBox Extension Pack
* [Vagrant 1.7+](http://www.vagrantup.com/)
additional Vagrant modules will be installed automatically (vagrant-hostmanager, vagrant-vbguest, vagrant-cachier)`
* Install Vagrant plugins  
`vagrant plugin install vagrant-hostmanager vagrant-vbguest vagrant-cachier`  
(these plugins will be checked and installed automatically, but `vagrant up` will fail on the first run, just re-run it if you'll get ` Unknown configuration section` error)
> You don't need to have Ansible installed on host machine. It will be installed on VM and self-provisioning will be launched. So it is possible to run everything on Windows machine. 

### RUN

* Clone this sources from Git
* Run `vagrant up`.
* It will start VM creation and Provisioning. Could take some time 15-30 min... Drink coffee and get back for complete virtual server with Yi2 project ready for play !

### Supported Host OS :

* **Ubuntu-based Linux 14.04+** - main tests and development, works the best 
* **Windows 7 Home** - rarely tested to bring some compatibility, but additional Your experience with Vagrant on Windows could be required
* **MacOS** - not tested by maintainer, but assumed to work fine as there is no know big issues with Vagrant on MacOS 

#### Note for Windows OS users

* Windows Firewall or any Antivirus software can cause some blocks on Vagrant start process. First of all to 'hosts' file modification. Be sure you turned them off (temporary) or set them up properly.
* In case you get `default: warning: connection refused. Retying...` messages and Vagrant never boot successfully - it seems to be a VirtualBox issue. Try to install some older VBox version. It is tested to work on Virtual Box 4.3.6.  
* On Windows 8 some issues are reported due to `Hyper-V` enabled. You should disable it if you experience issues with VirtualBox machines.
* use Git Bash if possible to make `vagrant ssh` working out of the box.

### PLAY

Ok, now if everything went fine you can access these Urls in your browser

* [http://yii2.local/](http://yii2.local/)  -  frontend app
* [http://admin.yii2.local/](http://admin.yii2.local/)  -  backend app
* [http://phpmyadmin.yii2.local/](http://phpmyadmin.yii2.local/) - phpMyAdmin
* [http://adminer.yii2.local/](http://adminer.yii2.local/) - Adminer (Lightweight and simple GUI manager for MySQL, PostgreSQL, SQLite, MS SQL, Oracle, SimpleDB, Elasticsearch and MongoDB)

* Gii code generator should be called like this [http://yii2.local/index.php?r=gii](http://yii2.local/index.php?r=gii)

**Note :** These local domains `.local` will be available on your host machine only if `hosts` file was modified correctly. It should 
be done automatically by `vagrant-hostsmanager` plugin. But if url `http://yii2.local/` or other is not found by your browser - make sure
your `hosts` file contain correct assignment of VM IP and local domains:  
It should have such lines :
```
192.168.33.33 yii2.local
192.168.33.33 admin.yii2.local
192.168.33.33 phpmyadmin.yii2.local
192.168.33.33 adminer.yii2.local
```

> File location. On Linux `/etc/hosts`. On Windows `%SystemRoot%\system32\drivers\etc\hosts`

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

* Sphinx
* Elastic Search
* CUBRID
* yii-basic-template checkout (http://basic.yii2.local)
* automatic Model / CRUD generation via Cli command
* a way to specify GitHub Token to prevent Composer requests limitation

### Made by [Evgeniy Kuzminov](http://stdout.in). Thanks for support to [Anton Logvinenko](http://anton.logvinenko.name/).
