---
layout: post
title:  "PHP and Temporal Coupling"
date:   2017-01-03 19:15:24 +0200
categories: php
---
About the architecture of applications in PHP it was written more than a dozen items, but on this issue, more than emphasize the designers of Java and C #. Its essence lies in the rigid dependence of the properties on the other.

Let's imagine the following situation:

```php
<?php

class Page
{
    /**
     * @var string
     */
    private $content;

    /**
     * @param $content
     */
    public function setContent($content)
    {
        $this->content = $content;
    }
}

class PageBuilder
{
    /**
     * @var Page
     */
    private $page;

    /**
     * @param $page
     */
    public function setPage($page)
    {
        $this->page = $page;
    }

    /**
     * @param $content
     * @return $this
     */
    public function setContent($content)
    {
        $this->page->setContent($content);

        return $this;
    }

    /**
     * @return Page
     */
    public function build()
    {
        return $this->page;
    }
}

$pageBuilder = new PageBuilder();
$pageBuilder->setPage(new Page());
$pageBuilder->setContent('Test content');
$pageBuilder->build();
```

This example shows that the `$pageBuilder->build()` is potentially dangerous and can result in a fatal error if `$pageBuilder->setPage(new Page())` has not been previously called.
Another common mistake - using methods `init()` or `initialization()`

```php
<?php

class Page
{
    // Class
}

class PageBuilder
{
    /**
     * @var Page
     */
    private $page;

    /**
     * Initialization
     */
    public function init()
    {
        $this->page = new Page();
    }

    /**
     * @param $content
     * @return $this
     */
    public function setContent($content)
    {
        $this->page->setContent($content);

        return $this;
    }

    /**
     * @return Page
     */
    public function build()
    {
        return $this->page;
    }
}

$pageBuilder = new PageBuilder();
$pageBuilder->init();
$pageBuilder->setContent('Test content');
$pageBuilder->build();
```

If we forget to call the `init()` method, we are also waiting for trouble. This code is an excellent example of poor application architecture. Methods-initializers are trying to behave as constructors, whether they are not.

To avoid Temporal Coupling must always use rules:

* instance of the class must be ready for use immediately after creation;
* constructors should not  perform any logic except of initialization of class properties;

## Dependency injection via constructor

This solution is optimal and preferred in most cases. We can use Dependency Injection mechanism of Symfony, Laravel or other modern frameworks.

```php
<?php

class Page
{
    // Class
}

class PageBuilder
{
    /**
     * @var Page
     */
    private $page;

    /**
     * PageBuilder constructor.
     * @param Page $page
     */
    public function __construct(Page $page)
    {
        $this->page = $page;
    }

   // Setter methods
}

$pageBuilder = new PageBuilder(new Page());
$pageBuilder->setContent('Test content');
$pageBuilder->build();
```

## Abstract factory

Slightly modify our code, adding an abstract factory:

```php
<?php

class Page
{
    // Class
}

class PageBuilder
{
    /**
     * @var Page
     */
    private $page;

    /**
     * PageBuilder constructor.
     * @param Page $page
     */
    public function __construct(Page $page)
    {
        $this->page = $page;
    }

    /**
     * @param $content
     * @return $this
     */
    public function setContent($content)
    {
        $this->page->setContent($content);

        return $this;
    }

    /**
     * @return Page
     */
    public function build()
    {
        return $this->page;
    }
}

class PageBuilderFactory implements FactoryInterface
{
    /**
     * @param Page|null $page
     * @return PageBuilder
     */
    public function create(Page $page = null)
    {
        if (null === $page) {
            $page = new Page();
        }

        return new PageBuilder($page);
    }
}

$pageBuilderFactory = new PageBuilderFactory();
$pageBuilder = $pageBuilderFactory->create();
$pageBuilder->setContent('Test content');
$pageBuilder->build();
```

As you can see, the instance Page created without an explicit call and will be available to our Builder.

## Conclusion

Temporal Coupling must always be avoided, regardless of the complexity of the application, the effect of code-review or other factors. Also remember that the designers have to perform only the logic associated with the injections. Otherwise, you run the risk of deterioration in performance on the stage of creating instances of the class.

## Useful links

- [Design Smell](http://blog.ploeh.dk/2011/05/24/DesignSmellTemporalCoupling/)
- [Temporal Coupling Between Method Calls](http://www.yegor256.com/2015/12/08/temporal-coupling-between-method-calls.html)
- [Symfony DI](http://symfony.com/doc/current/components/dependency_injection/introduction.html)
