---
title: Why we choose Smarty in Thelia ?
subtitle: During the development of Thelia we look for a standalone template engine. Here I explain why we choose Smarty instead of other libraries

---

When we started the development of Thelia 2 in august 2012, we first refactor the existing template engine from Thelia 1.
We modernized it, we followed the PSR 0, 1 and 2 and we made a standalone library. It was possible to use it outside of Thelia
without any dependencies from Thelia. We named it Tpex (T => Thelia, pex => parser/lexer) and it sounds like the brand 
[Tipp-Ex](https://en.wikipedia.org/wiki/Tipp-Ex).

After some weeks of development and some improvements in Tpex we realized that we were reinventing the wheel, all this work 
was already existing in other libraries like Smarty or Twig.

At this point, we already spent lot of time learning new development methods and new libraries. We take the time to learn
them deeply (like the DI and IoC concept). Some of us already knew Smarty. We looked its features, how it works, if it was possible
to configure and extend it easily. All of this was possible. It was also the case for Twig. We can also argue that Smarty is 
already well known in the e-commerce ecosystem.

### What about a technical argumentation ?

Smarty and Twig have more or less the same features. In fact Twig was much better than Smarty but before the version 3.1
of Smarty. Since version 3.1 they are "equals" : 

* objected oriented
* template inheritance
* auto escaping of variables
* extensions system (maybe better in Twig)
* hosted on github and available on packagist

The performance in Smarty are not bad, the library performance was hardly improve in version 3.1. With the same features (block, inheritance, loop and file inclusion) we have more 
or less the same results between Smarty and Twig (it was a real surprise).

We made everything we wanted with Smarty in Thelia, we developed a lot of extensions deeply linked to Thelia behaviour.

One point for Twig : Smarty doesn't have a C extension.

### Yes, but Twig is the default symfony template engine !

True !

But keep in mind that we use some of Symfony components and **not** the fullstack framework. So we don't have access to the 
FrameworkBundle or the TwigBridge. 

We made the choice to take the libraries we need for having the structure we want ! And we are free to use the ORM or the
template engine we want. We are not linked to a software or an other one.

### Why not, but I want to use Twig

Good news, since version 2.1 Thelia is template engine agnostic.

Implement the [ParserInterface](https://github.com/thelia/thelia/blob/master/core/lib/Thelia/Core/Template/ParserInterface.php) and the [ParserHelperInterface](https://github.com/thelia/thelia/blob/master/core/lib/Thelia/Core/Template/ParserHelperInterface.php).
Then declare the *thelia.parser* service in your container, this service must implement the ParserInterface.

If you want an example, take a look at the [TheliaSmarty](https://github.com/thelia-modules/TheliaSmarty) module

## Conclusion

Smarty is not evil ! If you learn it you will look that it is a good library. Twig is certainly better but Smarty, since version
3.1, is still here, in active development and can be used in modern projects.

Don't have preconceived ideas about a library. Test it, learn it. In Thelia Smarty works like a charm.