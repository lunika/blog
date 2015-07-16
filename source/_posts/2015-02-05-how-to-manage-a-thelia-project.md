---
title: How to manage a Thelia project
subtitle: Find the better way to create and manage your Thelia project
draft: true
untrack: true

---

# Thelia e-commerce framework

The e-commerce revolution of recent years has resulted in new products such as [Thelia](http://thelia.net) being brought to market, which 
are called e-commerce frameworks.

Today, the "online product catalog" model is dropping out of favor, and transactions are made differently: by reserving 
a room on AirBnB, or by ordering on BlaBlaCar or Uber! All of these innovative sites are the new e-commerce sites and 
their defining feature is simply that each of them has specific needs.

![Thelia techno](http://thelia.net/wp-content/uploads/2013/09/technos-okokok.jpg)

## New needs of e-commerce sites and poorly adapted generic solutions
 
Traditional e-commerce software such as Magento, Prestashop, or Shopify are a generic offer designed to serve the most 
people. They specifically target the product catalog. In spite of efforts to create a multitude of plugins, often 
available via a dedicated marketplace, they fail to precisely meet the expectations of each e-tailer. Therefore, he 
must then adapt his needs to match what is available.

Furthermore, an obsession for responding to the maximum of uses inevitably leads these solutions to being overweight, 
which directly affects their performance and stability.

A generic tool for creating a shop allows you, in the best case, to have a generic shop that is not very innovative and 
poorly adapted to the target market. This is one of the reasons that 80% of today's e-commerce sites don't sell.

At the other extreme, there are numerous companies who choose to fully develop their own e-commerce site, after not 
finding an answer in the existing generic offers. Besides the problems of maintenance and security that this choice 
entails, you can easily imagine the exorbitant cost it imposes. The back office, billing, and payment (to name a few) 
must be completely developed from scratch!

## E-commerce framework to restore agility to projects

In this context, the [Thelia](http://thelia.net) framework approach has emerged. It's a real toolbox for developers in charge of the design 
of merchant sites, and it offers the necessary modules without imposing limitations on the structure of the final project.

Driven by the ambition to achieve the "perfect framework," it uses the best technology and current "best practices." 
With an "international" orientation, it is driven by community of developers and is well documented. It doesn't attempt 
to serve everyone, and requires a certain level of technical skill to be understood.

The [Thelia](http://thelia.net) credo is : 

* Make "tailored" e-commerce sites to meet specific needs
* Install only what is needed, to improve maintenance and performance
* Gain "agility" so that the site can adapt very quickly as its market changes, and thus optimize sales!

To accomplish this, Thelia integrates modular and scalable structure. While generic solutions seek to capture their 
customers, the Thelia e-commerce framework makes the choice of interoperability by integrating a REST API.

# How to install Thelia

Since the beginning of Thelia 2 we made a lot of effort to simplify the developer life by automating lot of tasks like
the module generation, a powerful and extendable command line tools, abstraction for CRUD operations.

The last missing point was how to manage easily an installation of Thelia and how to fully (and easily) use composer for
modules or event templates. With version 2.1 this point was reached and the organisation of Thelia has a little bit change.
Let me introduce you Thelia-project

## Thelia-project

Thelia-project is the new born in the Thelia family and the answer for managing well a Thelia project. For this we extracted
part of Thelia in new github repositories and we manage them with composer. You can see [thelia/core](http://github.com/thelia/core), 
It is the core of Thelia, alone in its own git repository. With that it is now possible to start a new project and require
after all the dependencies you need in your project.


### Start a new project

The current stable version of Thelia is the 2.1.1. You need composer for working and of course all the [requirements needed
for Thelia](http://doc.thelia.net/en/documentation/installation/index.html#requirements). Once done, open your favorite terminal and
create a new project (replace `your-project-directory` by a non existing directory) : 

    $ curl -sS https://getcomposer.org/installer | php
    $ php composer.phar create-project thelia/project your-project-directory 2.1.1
    
composer will download thelia and its dependencies in the `your-project-directory` directory. 

Now we have to install the database of Thelia : 

    $ cd your-project-directory
    $ php Thelia thelia:install
    
follow the instruction and your Thelia is ready to be used. If you don't have apache installed, your can run the php built-in
webserver like this :

    $ php -S localhost:8000 -t web/
    
For more flexibility you can use variable environments for your database credentials as [explain in the documentation](http://doc.thelia.net/en/documentation/configuration/environment_variables.html).
With this you don't have to modify your database.yml file between dev and prod environment. Just put your credentials in your vhost.
    
At this step, you can initiate your git repository for your project and save all unstage files. The .gitignore is already configured.

![Thelia homepage](http://thelia.net/images/thelia_homepage.png)
    
### Install dependencies

You will certainly want to install new modules, like [Thelia studio](https://github.com/thelia-modules/TheliaStudio) for exemple.
All the modules present on [packagist](https://packagist.org/) can be installed with composer like this : 

    $ php composer.phar require thelia/thelia-studio:~1.1
    
The module and all its depencies are downloaded but not yet activated. In Thelia, a module can be present but not activated : 

    $ php Thelia module:activate TheliaStudio
    
### Manage private dependencies

In a project, some modules are public and can be host on github and register on packagist but other resources are dedicated
to your customer. For that you maybe have a gitlab instance installed on your own server or maybe private repositories on github.

You can still use composer with this private packages, the [composer documentation explain how to do that](https://getcomposer.org/doc/articles/handling-private-packages-with-satis.md).

You can also [manage your templates with composer](http://raynaud.io/2014/09/01/share-your-thelias-module-using-composer-and-packagist.html).

### Deploy your project
 
You have finished all your development and you want to deploy it on your development environment. Dedicated tools like [capistrano](http://capistranorb.com/)
can automate all of this if you want but basically you have to respect this steps :

* clone or pull your project
* install your dependencies with composer (`composer install`)
* migrate your database

### update your project

Between the beginning of your development and the moment you want to release it, we probably have released new versions of Thelia.
You can update your Thelia-project easily by using the `change-version.sh` script : 

    $ ./change-version.sh 2.1.2
    
It will update your files to version 2.1.2, update now your database with `local/setup/update.php` script.

## Conclusion

As you can see, Thelia-project will really help you to bootstrap and manage a Thelia project. Unfortunately it's not possible to migrate an existing thelia installation
to a Thelia-project.