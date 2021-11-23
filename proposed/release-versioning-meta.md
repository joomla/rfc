# Release Versioning Meta Document

## 1. Summary

_This Specification describes how versions are numbered in Joomla projects._

This specification aims to help developers, code reviewers and release leads to determine, whether a new piece or a
change of code belongs to the next patch, minor or major release. It will also cover documentation requirements that are
related to versioning.

## 2. Why Bother?

Sometimes it is hard to tell bug fixes and features apart. The Release Leads want a comprehensive set of rules to be
able to make good and fast decisions about the target release of a contribution.

## 3. Scope

The specification applies to all Joomla projects, e.g., the CMS, the Framework, core extensions, ...

## 4. Considerations

### 4.1 Semantic Versioning

Joomla started to follow [Semantic Versioning](Semver) with release 3.3 in April 2014. The rules were not always
followed strictly ([Issue#16874](16874), [Issue#17583](17583), [Issue#24728](24728) to name a few). This need to change,
because the Joomla ecosystem is heavily depending on reliable information about compatibility. This is done in section 1
of the specification.

[Semver]: https://github.com/semver/semver/blob/master/semver.md

[24728]: https://issues.joomla.org/tracker/joomla-cms/24728

[17583]: https://github.com/joomla/joomla-cms/issues/17583

[16874]: https://github.com/joomla/joomla-cms/issues/16874

### 4.2 API

The main problem with Semantic Versioning seems to be to categorise code contributions as bug fixes or features. This
should be easy enough, as the Semantic Versioning specification is quite clear in that regard. Strongly simplified, it
says: Changes that do not change signatures of functions or methods of the public API and do not add new ones can go
into a patch release.

Unfortunately, Joomla has no official definition of "public API". Section 2 of the specification makes up for the
omission. It describes, how public and internal API are told apart using the `@api` and `@internal` annotations as
proposed by the draft [PSR19][]. It is recommended to add these annotations to existing code. For new code they are
required.

[PSR19]: https://github.com/php-fig/fig-standards/blob/master/proposed/phpdoc-tags.md

### 4.3 Deprecations

The core contributors have not been very cautious about deprecations in the past.
`JObject`, for example, has
been [deprecated for Joomla 3.4](https://github.com/joomla/joomla-cms/issues/6125#issuecomment-75035212), but made it
into Joomla 4 (although renamed to CMSObject) with the deprecation annotation still in place. Section 3 describes how to
handle and document deprecations. Among other things, it stipulates that a replacement must be offered and used, if the
deprecation is not phasing out a feature. This requirement serves several purposes:

- It proves that the new solution actually works where it will end up being used.
- It shows developers, who consider the code as authoritative documentation, how the new solution works and should be
  used.
- It prevents the release lead of the following major version from being surprised by the "leftovers" and maybe
  therefore not being able to meet the schedule.

The documentation requirements make sure that legacy code can easily be adopted to the new implementation.

### 4.4 User Interface

From a code point of view, improvements of the user interface do not touch the API and thus are not features in the
sense of Semantic Versioning. Template files, however, work like functions, since they rely on injected variables to
produce the output. This interface between a View and a template is a contract and as such underlies the rules of
Semantic Versioning. Section 4 provides the rules for dealing with user interface changes.

### 4.5 External Dependencies

Section 5 deals with external dependencies, a.k.a. libraries. The implementation details of external dependencies are
not under the control of the Joomla project. Therefore, the code of these dependencies is basically internal and does
not fall under Semantic Versioning. As a result, these dependencies can be updated or even exchanged without breaking
the compatibility promise. As soon as an external API officially becomes part of the public API, as in the case of
Bootstrap, the rules of Semantic Versioning do apply.

## 5. Examples

To illustrate the rules of the specification, here are a few examples. The starting point is this class, which prepares
a fresh Earl Grey tea:

```php
// Old version
class CupOfTea
{
    /**
     * Brew a fresh cup of Earl Grey tea
     *
     * @param   bool  $addSugar  Set to true, if you want sugar in the tea.
     * @param   bool  $addMilk   Set to true, if you want milk in the tea.
     *
     * @return  Cup
     */
    public function makeTea($addSugar = false, $addMilk = false)
    {
        $boiler = new Boiler();
        $boiler->addWater(0.5);
        $boiler->cook(97.7778); // heat up to 97.7778 °C

        $tea = new Tea('earl grey');

        $cup = new Cup();
        $cup->addIngredient($tea);
        $cup->addIngredient($boiler->getWater());

        if ($addSugar) {
            $sugar = new Sugar(4); // get 4 gram sugar
            $cup->addIngredient($sugar);
        }

        if ($addMilk) {
            $milk = new Milk(100); // get 100 ml milk
            $cup->addIngredient($milk);
        }

        return $cup;
    }
}
```

### 5.1 Scenario 1 - Using New PHP Features

Let's assume that PHP 8.1 introduces a native function `php_make_caffeine_drink()` to make all kinds of caffeinated hot
drinks. This function does a lot of work for us, so we can greatly simplify `CupOfTea::makeTea()`. However, we still
need to support PHP versions before 8.1. This is where a so-called feature switch comes into play.

```php
// PHP 8.1 version using native php_make_caffeine_drink() function
class CupOfTea 
{
    /**
     * Brew a fresh cup of Earl Grey tea
     *
     * @api
     * @param   bool  $addSugar  Set to true, if you want sugar in the tea.
     * @param   bool  $addMilk   Set to true, if you want milk in the tea.
     *
     * @return  Cup
     */
    public function makeTea($addSugar = false, $addMilk = false)
    {
        // Feature switch
        if (compare_version(PHP_VERSION, '8.1', '>=')) {
            $tea = php_make_caffeine_drink(type: 'earl grey', amount: '0.5', sugar: $sugar ? 4 : 0, milk: $milk ? 100 : 0);
            $cup = new Cup();
            $cup->addIngredient($tea);
            return $cup;
        }

        // Fall back to old code for PHP < 8.1
        $boiler = new Boiler();
        $boiler->addWater(0.5);
        $boiler->cook(97.7778); // heat up to 97.7778 °C

        $tea = new Tea('earl grey');

        $cup = new Cup();
        $cup->addIngredient($tea);
        $cup->addIngredient($boiler->getWater());

        if ($addSugar) {
            $sugar = new Sugar(4); // get 4 gram sugar
            $cup->addIngredient($sugar);
        }

        if ($addMilk) {
            $milk = new Milk(100); // get 100 ml milk
            $cup->addIngredient($milk);
        }

        return $cup;
    }
}
```

Since this change does not affect existing code that uses the `CupOfTea::makeTea()` method in any way (nothing needs to
be adjusted there to continue working, after all), it can be released with the next patch release. As soon as official
support for PHP versions < 8.1 ceases, the old code can (must) be removed:

```php
// PHP 8.1 version using native php_make_caffeine_drink() function
class CupOfTea 
{
    /**
     * Brew a fresh cup of Earl Grey tea
     *
     * @api
     * @param   bool  $addSugar  Set to true, if you want sugar in the tea.
     * @param   bool  $addMilk   Set to true, if you want milk in the tea.
     *
     * @return  Cup
     */
    public function makeTea($addSugar = false, $addMilk = false)
    {
        $tea = php_make_caffeine_drink(type: 'earl grey', amount: '0.5', sugar: $sugar ? 4 : 0, milk: $milk ? 100 : 0);
        $cup = new Cup();
        $cup->addIngredient($tea);
        return $cup;
    }
}
```

### 5.2 Scenario 2 - Using New PHP Features Adding Functionality

The PHP function `php_make_caffeine_drink()` in scenario 1 is a function for all caffeinated hot drinks, not just Earl
Grey tea. This opens up the chance for us to also offer other tea varieties such as Darjeeling. We can even go as far as
allowing coffee.

Here we have to make a fundamental decision: Do we want to build a separate class for coffee? Or would we rather build a
more general version that brews caffeinated hot drinks?

#### a. Two Separate Classes

In the first case, the class `CupOfTea` will be enabled to produce different types of tea. Unfortunately, we can't just
change the signature of `makeTea()` - there might be developers who have derived from this class because it wasn't
declared as `final`, and PHP throws an `E_WARNING` if the signatures of parent class and child class don't match. It can
make sense to accept these warnings, but this should be thoroughly considered, justified and documented. Here we choose
the way to replace the `makeTea()` function.

```php
// PHP 8.1 version using native php_make_caffeine_drink() function
class CupOfTea 
{
    /**
     * Supported types of tea
     * @api
     */
    public const EARL_GREY  = 'earl grey';
    public const DARJEELING = 'darjeeling';

    /**
     * Brew a fresh cup of Earl Grey tea
     *
     * @api
     * @param   bool  $addSugar  Set to true, if you want sugar in the tea.
     * @param   bool  $addMilk   Set to true, if you want milk in the tea.
     *
     * @return  Cup
     *
     * @deprecated 4.2  Will be removed in 5.0. Use CupOfTea::getTea() instead. 
     *                  Before (version < 4.2):
     *                    $brewer = new CupOfTea(); 
     *                    $tea = $brewer->makeTea($addSugar, $addMilk);
     *                  After (version >= 4.2):
     *                    $brewer = new CupOfTea(); 
     *                    $tea = $brewer->getTea(CupOfTea::EARL_GREY, $addSugar, $addMilk);
     */
    public function makeTea($addSugar = false, $addMilk = false) 
    {
        trigger_error('Method ' . __METHOD__ . ' is deprecated', E_USER_DEPRECATED);

        return $this->getTea(self::EARL_GREY, $addSugar, $addMilk);
    }

    /**
     * Brew a fresh cup of tea
     *
     * @api
     * @param   string  $type      The type of tea, one of the CupOfTea::* constants.
     * @param   bool    $addSugar  Set to true, if you want sugar in the tea.
     * @param   bool    $addMilk   Set to true, if you want milk in the tea.
     *
     * @return  Cup A cup of tea
     * @since   4.2
     */
    public function getTea($type, $addSugar = false, $addMilk = false) 
    {
        if (compare_version(PHP_VERSION, '8.1', '>=')) {
            $drink = php_make_caffeine_drink(type: $type, amount: '0.5', sugar: $sugar ? 4 : 0, milk: $milk ? 100 : 0);
            $cup = new Cup();
            $cup->addIngredient($drink);
            return $cup;
        }

        // Fall back to old code for PHP < 8.1
        $boiler = new Boiler();
        $boiler->addWater(0.5);
        $boiler->cook(97.7778); // heat up to 97.7778 °C

        $tea = new Tea($type);

        $cup = new Cup();
        $cup->addIngredient($tea);
        $cup->addIngredient($boiler->getWater());

        if ($addSugar) {
            $sugar = new Sugar(4); // get 4 gram sugar
            $cup->addIngredient($sugar);
        }

        if ($addMilk) {
            $milk = new Milk(100); // get 100 ml milk
            $cup->addIngredient($milk);
        }

        return $cup;
    }
}

class CupOfCoffee
{
    /**
     * Supported types of coffee 
     * @api
     */
    public const ROBUSTA = 'robusta';
    public const ARABICA = 'arabica';

    /**
     * Constructor.
     * 
     * This constructor can be removed, once the PHP minimum requirement is 8.1 or above.
     * 
     * @api
     * @since  4.2
     */
    public function __construct()
    {
        if (compare_version(PHP_VERSION, '8.1', '<')) {
            throw new \RuntimeException('This class requires PHP >= 8.1');
        }
    }

    /**
     * Brew a fresh cup of coffee
     *
     * @api
     * @param   string  $type      The type of coffee, one of the CupOfCoffee::* constants.
     * @param   bool    $addSugar  Set to true, if you want sugar in the coffee.
     * @param   bool    $addMilk   Set to true, if you want milk in the coffee.
     *
     * @return  Cup
     * @since   4.2
     */
    public function getCoffee($type, $addSugar = false, $addMilk = false)
    {
        $tea = php_make_caffeine_drink(type: $type, amount: '0.5', sugar: $sugar ? 4 : 0, milk: $milk ? 50 : 0);
        $cup = new Cup();
        $cup->addIngredient($tea);
        return $cup;
    }
}
```

Because you can now make teas other than Earl Grey, and even coffee, the change is considered a feature and therefore
belongs in a minor release.

#### b. One General Class

Since the methods `CupOfTea::getTea()` and `CupOfCoffee::getCoffee()` are very similar in end effect, it probably makes
sense in this case to provide a more general solution: a class that makes hot drinks. With the introduction of this new
class, `CupOfTea` becomes redundant and therefore deprecated.

```php
class CupOfHotDrink
{
    /**
     * Supported types of hot drinks 
     * @api
     */
    public const EARL_GREY  = 'earl grey';
    public const DARJEELING = 'darjeeling';
    public const ROBUSTA    = 'robusta';
    public const ARABICA    = 'arabica';

    /**
     * Brew a fresh hot drink
     *
     * @api
     * @param   string  $type      The type of hot drink, one of the CupOfHotDrink::* constants.
     * @param   bool    $addSugar  Set to true, if you want sugar in the hot drink.
     * @param   bool    $addMilk   Set to true, if you want milk in the hot drink.
     *
     * @return  Cup
     * @since   4.2
     */
    public function getHotDrink($type, $addSugar = false, $addMilk = false)
    {
        if (compare_version(PHP_VERSION, '8.1', '<')) {
            $tea = php_make_caffeine_drink(type: $type, amount: '0.5', sugar: $sugar ? 4 : 0, milk: $milk ? 50 : 0);
            $cup = new Cup();
            $cup->addIngredient($tea);
            return $cup;
        }
        
        if ($type !== self::EARL_GREY) {
            throw new \RuntimeException('To brew hot drinks other than Earl Gray tea you need PHP 8.1 or above.');
        }

        // Fall back to old code for PHP < 8.1
        $boiler = new Boiler();
        $boiler->addWater(0.5);
        $boiler->cook(97.7778); // heat up to 97.7778 °C

        $tea = new Tea('earl grey');

        $cup = new Cup();
        $cup->addIngredient($tea);
        $cup->addIngredient($boiler->getWater());

        if ($addSugar) {
            $sugar = new Sugar(4); // get 4 gram sugar
            $cup->addIngredient($sugar);
        }

        if ($addMilk) {
            $milk = new Milk(100); // get 100 ml milk
            $cup->addIngredient($milk);
        }

        return $cup;
    }
}

/**
 * @deprecated 4.2  Will be removed in 5.0. Use CupOfHotDrink instead. 
 */
class CupOfTea 
{
    /**
     * Brew a fresh cup of Earl Grey tea
     *
     * @api
     * @param   bool  $addSugar  Set to true, if you want sugar in the tea.
     * @param   bool  $addMilk   Set to true, if you want milk in the tea.
     *
     * @return  Cup
     *
     * @deprecated 4.2  Will be removed in 5.0. Use CupOfHotDrink::getHotDrink() instead. 
     *                  Before (version < 4.2):
     *                    $brewer = new CupOfTea(); 
     *                    $tea = $brewer->makeTea($addSugar, $addMilk);
     *                  After (version >= 4.2):
     *                    $brewer = new CupOfHotDrink(); 
     *                    $tea = $brewer->getHotDrink(CupOfHotDrink::EARL_GREY, $addSugar, $addMilk);
     */
    public function makeTea($addSugar = false, $addMilk = false) 
    {
        trigger_error('Method ' . __METHOD__ . ' is deprecated. Use CupOfHotDrink::getHotDrink() instead.', E_USER_DEPRECATED);

        $brewer = new CupOfHotDrink();
        return $brewer->getHotDrink(CupOfHotDrink::EARL_GREY, $addSugar, $addMilk);
    }
}
```

This solution will maintain the functionality `CupOfTea` until the next major version. From the next minor release that
includes this change, users in a modern environment will be able to use the new possibilities immediately. For those in
older environments, no functionality will be lost.

## 6. People

### 6.1 Editor(s)

* Niels Braczek <niels.braczek@community.joomla.org>

### 6.2 Sponsors

* Harald Leithner <harald.leithner@community.joomla.org>

### 6.3 Contributors

* N/A

## 7. Votes

* **Entrance Vote:** 2021-11-16 Production Team Leaders
* **Acceptance Vote:** _(not yet taken)_

## 8. Relevant Links

_**Note:** Order descending chronologically._

* [Semantic Versioning Specification](Semver)

## 9. Errata

...
