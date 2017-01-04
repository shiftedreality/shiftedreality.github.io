---
layout: post
title:  "Stateless validators"
date:   2017-01-04 12:19:24 +0200
categories: php
tags:
- php
- mvc
---
Any developer is able to write validator. For date, time, URL, no matter.
But what's a correct way to implement it?

Let's imagine next interface:

```php
<?php

interface ValidatorInterface {

    public function isValid($value);
}
```

What's obvious implementation here?

```php
<?php

class TestValidator implements ValidatorInterface {

    public function isValid($value) {
        if (false === $value) {
            return false
        }

        return true;
    }
}
```

Ok, that's make sense. We can either return `true` or `false`.
But, let's add one more thing:

```php
<?php

class TestValidator implements ValidatorInterface {

    public function isValid($value) {
        if (fasle === $value) {
            return false
        }

        if (0 === $value) {
            return false
        }

        return true;
    }
}
```

Here we face with some kind of problem: we can not determine why our value is not valid.
Let's check how big guys do this:

https://github.com/zendframework/zend-validator/blob/master/src/ValidatorInterface.php

```php
<?php

namespace Zend\Validator;

interface ValidatorInterface
{
    /**
     * Returns true if and only if $value meets the validation requirements
     *
     * If $value fails validation, then this method returns false, and
     * getMessages() will return an array of messages that explain why the
     * validation failed.
     *
     * @param  mixed $value
     * @return bool
     * @throws Exception\RuntimeException If validation of $value is impossible
     */
    public function isValid($value);

    /**
     * Returns an array of messages that explain why the most recent isValid()
     * call returned false. The array keys are validation failure message identifiers,
     * and the array values are the corresponding human-readable message strings.
     *
     * If isValid() was never called or if the most recent isValid() call
     * returned true, then this method returns an empty array.
     *
     * @return array
     */
    public function getMessages();
}
```

Ok, that's make sense. We collect all occurred errors into array and call `getMessages()` afterwards.

## Stateless

What is stateless? It's possibility ob object to not have any state.
Stateless gives us ability to use `Dependency Injections` of our validators.
Zend Validator is not stateless, because any time when validator is called - it will collect errors or other metadata. So is it possible to write stateless validator with possibility to determine an error?

Yes

```php
<?php

class TestValidator implements ValidatorInterface {

    public function isValid($value) {
        if (fasle === $value) {
            throw new \Exception('Value is not false.');
        }

        if (0 === $value) {
            throw new \Exception('Value is not 0.');
        }

        return true;
    }
}
```

With exceptions we can not store any kind of information, but this also doesn't allow us to expect for multiple errors.
For such cases we can make decomposition of `TestValidator` into `NotFalseValidator` and `NotZeroValidator`.
Also we cannot call such methods as `isValid`, because another developer would rather expect `boolean` as return parameter. I would call it `validate`.

### Pros
- Doesn't contains any state - can be called in `DI`;
- Does not require factories.

### Cons
- Can not validate more than 1 error at the same time;
- `isValid` is not correct method name. It can be either `validate`;
- Requires copy-paste of `try-catches` in an kind of calls.





