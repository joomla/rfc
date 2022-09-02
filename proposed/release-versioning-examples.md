# Release Versioning Examples

This document contains a collection of examples to illustrate the rules of the Release Versioning specification.

* [Case: Utilising a New PHP Feature](#case-1)
    * [Scenario 1 - Using the New PHP Feature to Replace Code](#case-1-1)
    * [Scenario 2 - Using the New PHP Feature to Extend Functionality](#case-1-2)

More cases may be added over time.

<a name="case-1"></a>

## Case: Utilising a New PHP Feature

The starting point is this class, which prepares a fresh Earl Grey tea:

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

<a id="case-1-1"></a>

### Scenario 1 - Using the New PHP Feature to Replace Code

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
        if (version_compare(PHP_VERSION, '8.1', '>=')) {
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

<a id="case-1-2"></a>

## Scenario 2 - Using the New PHP Feature to Extend Functionality

The PHP function `php_make_caffeine_drink()` in scenario 1 is a function for all caffeinated hot drinks, not just Earl
Grey tea. This opens up the chance for us to also offer other tea varieties such as Darjeeling. We can even go as far as
allowing coffee.

Here we have to make a fundamental decision: Do we want to build a separate class for coffee? Or would we rather build a
more general version that brews caffeinated hot drinks?

### a. Two Separate Classes

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
     * @deprecated 4.2  Will be removed in 6.0. Use CupOfTea::getTea() instead. 
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
        if (version_compare(PHP_VERSION, '8.1', '>=')) {
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
        if (version_compare(PHP_VERSION, '8.1', '<')) {
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

### b. One General Class

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
        if (version_compare(PHP_VERSION, '8.1', '>=')) {
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
 * @deprecated 4.2  Will be removed in 6.0. Use CupOfHotDrink instead. 
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
     * @deprecated 4.2  Will be removed in 6.0. Use CupOfHotDrink::getHotDrink() instead. 
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
