---
layout: post
title: Auto Complete with PHPSpec
summary: Unit testing with PHPSpec is GREAT! Unfortunately it is missing some nice to haves
comments: true
---

What is **PHPSpec**, from their documentation:

> phpspec is a tool which can help you write clean and working PHP code using behaviour driven development or BDD. BDD is a technique derived from test-first development.

> BDD is a technique used at story level and spec level. phpspec is a tool for use at the spec level or SpecBDD. The technique is to first use a tool like phpspec to describe the behaviour of an object you are about to write. Next you write just enough code to meet that specification and finally you refactor this code.

This is not an introduction to **PHPSpec**, this assumes you already know & use **PHPSpec**. When using **PHPSpec** you will notice that because of the *magic* the Class Under Test (CUT) does not auto complete. This is easily fixed with using **PHPStorm's** *Mixin* Annotation (`@mixin \Class\Name`).

Doing this will turn this screenshot:

![Without intellisense on PHPSpec CUT](/assets/2015-05-10-phpspec-auto-complete/phpspec-no-itellisense.png)

Into this:

![With intellisense on PHPSpec CUT](/assets/2015-05-10-phpspec-auto-complete/phpspec-with-itellisense.png)

Thus giving the usual IDE intellisense / code completion on the CUT with **PHPSpec**.

*Note: using PHPStorm v8, PHPSpec v2*

### Reference: Information discovered by [@schrotty](https://twitter.com/schrotty) at [@PHPUCEU](https://twitter.com/phpuceu)

---

### You will notice that the PHPSpec methods are not auto completing.

There is yet to be a clean solution to this.

The best solution to date for this is to put a *mixin* on the CUT (class under test) to a template class which contains the **PHPSpec** mthods. Hopefully a better solution will present itself in the near future.

Simple example (namespaces removed for simplicity):

```php
/**
 * Class Dashboard
 *
 * @mixin Template
 */
class Dashboard
{

    /**
     * @var int
     */
    protected $id;

    // ...
}
```


```php
// PHPSpec template
class Template
{

    /**
     * @param string $type
     */
    public function shouldHaveType($type) {}

    // ...
}
```
This is still not ideal, because now your Source Code Classes have auto complete to the **PHPSpec** template - so now you have it in your Specs but also in your Source Code...the world is not perfect.
