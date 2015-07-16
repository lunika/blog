---
title: share your Thelia’s module using composer and packagist
subtitle: How to use the custom installer developed for Thelia in your project

---

[Composer](http://getcomposer.org/) is an awesome tool for managing dependencies in a project and [Packagist][1] is a public composer repository, in fact it’s THE public repository for composer.

I’ve been wanting to manage thelia’s module with composer for a while but I thought that it was not possible because you can’t choose your vendor directory. I was wrong. Last week I discovered that it was possible to develop [custom installer](https://getcomposer.org/doc/articles/custom-installers.md) for a specific package type. First, a developer from Thelia’s community discovered the composer/installers package and decided to fork it to add thelia in the list of supports package types. But finally this morning I developed a custom installer dedicated for Thelia and maintained by Thelia’s community. Having our own installer is more flexible for us.

With this custom installer (see [thelia/installer](https://packagist.org/packages/thelia/installer)), you can of course manage modules but also templates (for front-office, back-office, pdf and email). For that 5 types are declared :

* thelia-module for modules, installed in local/modules
* thelia-frontoffice-template for a front-office template, installed in template/frontOffice
* thelia-backoffice-template for a back-office template, installed in template/backOffice
* thelia-pdf-template for a pdf template, installed in template/pdf
* thelia-email-template for an email template, installed in template/email

The installer comes with another custom parameter. You can specify the name of the directory where your package is installed. This is useful because you can’t set a name with [uppercase character on packagist](https://packagist.org/about) .

## How to use this installer ?

Using this installer is really simple. You just have to require it in your composer.json file and specify the type of your package with one of the list above and of course if needed, all the dependencies you need. Example from [thelia/hooktest-module](https://github.com/thelia/HookTest-module) :

    {
        "name": "thelia/hooktest-module",
        "type": "thelia-module",
        "require": {
            "thelia/installer": "~1.0"
        },
        "extra": {
            "installer-name": "HookTest"
        }
    }

Here I declare that the name of my module is « thelia/hooktest-module » but, in the end, I want the name of the directory to be « HookTest » so I use the « installer-name » extra parameter.

Now I just have to share this module on [packagist][1] and then require it in the main composer.json file of thelia. Be careful, never use composer update command for now, you will have issues with propel, use require :

    composer require "thelia/hooktest-module":"1.0"

Your module is now in local/modules/HookTest and if it requires dependecies you can find them in core/vendor directory.

Now you have a powerfull tool for developing and sharing module or template for Thelia.
 
[1]: https://packagist.org/