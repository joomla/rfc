# Content Elements


The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119][].

[RFC 2119]: http://tools.ietf.org/html/rfc2119

### References

- [RFC 2119][]: Key words for use in RFCs to Indicate Requirement Levels

## 1. Specification

### 1.1 Facade

### 1.2 Application

```php
<?php

namespace Joomla\Facade;

use \Joomla\CMS\Application\CMSApplicationInterface;
use Joomla\CMS\Factory;

class App extends Facade
{
    /**
     * @var \Joomla\CMS\Application\CMSApplicationInterface
     */
    static private $instance;

    use Mockable;

    /**
     * Get the root object behind the facade.
     *
     * @return \Joomla\CMS\Application\CMSApplicationInterface
     */
    public static function getFacadeRoot(): CMSApplicationInterface
    {
        if (self::$isMock) {
            return self::$mock;
        }

        if (self::$instance === null) {
            self::$instance = Factory::getApplication();
        }

        return self::$instance;
    }
}
```

### 1.3 Content Visitor

## 2. Interfaces, Traits and Classes

### 2.1 Joomla\Facade\Facade

```php
<?php

namespace Joomla\Facade;

use RuntimeException;

abstract class Facade
{
    /**
     * Get the root object behind the facade.
     */
    abstract public static function getFacadeRoot();

    /**
     * Handle dynamic, static calls to the object.
     *
     * @param string $method
     * @param array  $args
     *
     * @return mixed
     *
     * @throws RuntimeException
     */
    public static function __callStatic(string $method, array $args)
    {
        $instance = static::getFacadeRoot();
        if (!$instance) {
            throw new RuntimeException('A facade root has not been set.');
        }

        return $instance->$method(...$args);
    }
}
```

### 2.2 Joomla\Facade\Mockable

```php
<?php

namespace Joomla\Facade;

trait Mockable
{
    protected static $isMock = false;

    protected static $mock;

    /**
     * @param $mock
     */
    public static function setMock($mock): void
    {
        self::$mock   = $mock;
        self::$isMock = true;
    }
}
```
