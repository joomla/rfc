# Content Elements

This specification defines Content Elements using the [Composite Pattern][]. 
Content Elements are standardised Data Objects for presentation purposes.

[Composite Pattern]: https://en.wikipedia.org/wiki/Composite_pattern

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119][].

[RFC 2119]: http://tools.ietf.org/html/rfc2119

### References

- [Composite Pattern][] on Wikipedia
- [RFC 2119][]: Key words for use in RFCs to Indicate Requirement Levels

## 1. Specification

### 1.1 Content Element

#### Element Creation

A Content Element SHOULD accept its properties as constructor parameters.
Additionally, it MUST provide a static `from()` method that accepts associative
arrays (hashes) and objects containing the data. An optional mapping hash
tells the method, which data property corresponds to which element property.

##### Example

```php
class Element implements ContentElementInterface
{
    protected $title;
    protected $text;
    ...
}

$data = (object) [
    'headline' => 'My Element',
    'bodytext' => 'This is the text body.'
];

$element = Element::from($data, [
    'title' => 'headline',
    'text'  => 'bodytext'
]);

echo $element->get('title');

echo $element->get('text');
```
will output

```
My Element

This is the text body.
```

#### Properties

Content Elements can have arbitrary properties. They are immutable by nature, 
since they define the output required by the application. Thus for properties only 
a `get()` method is required to obtain the value of a property.

##### Example

Let `$element` have a property title = "My Element".

```php
/** @var Joomla\Content\ContentElementInterface $element */
echo $element->get('title');

echo $element->get('unknown');

echo $element->get('unknown', 'default');
```

will output

```
My Element

NULL

default
```

#### Parameters

Each Content Element provides presentation specific parameters.

##### Example

Let `$element` have parameters class = "special" and foo = "bar".

```php
/** @var Joomla\Content\ContentElementInterface $element */
print_r($element->getParameters());

echo $element->getParameter('class');

print_r($element->getParameter('unknown'));

echo $element->getParameter('unknown', 'default');
```

will output

```
Array
(
    [class] => special
    [foo] => bar
)

special

NULL

default
```

Content Elements using this standard MUST implement the following interface:

- `Joomla\Content\ContentElementInterface`

### 1.2 Composite Element

A Composite Element is the base type for Content Elements with support for
containing other Content Element instances.

Composite Elements using this standard MUST implement the following interface:

- `Joomla\Content\CompositeElementInterface`

### 1.3 Content Visitor

Content Visitors using this standard MUST implement the following interface:

- `Joomla\Content\ContentVisitorInterface`

## 2. Interfaces

### 2.1 Joomla\Content\ContentElementInterface

The following interface MUST be implemented by compatible Content Elements.

```php
namespace Joomla\Content;

interface ContentElementInterface
{
    /**
     * Create an element.
     *
     * @param array|object $data    The data container
     * @param array        $mapping The property mapping
     * @param array        $params  The presentation parameters
     *
     * @return self
     */
    public static function from($data, $mapping = [], $params = []);

    /**
     * Visit the content element.
     *
     * @param ContentVisitorInterface $visitor The Visitor
     */
    public function accept(ContentVisitorInterface $visitor);

    /**
     * Get the value of a property.
     *
     * @param string $property The property
     * @param mixed  $default  The default value
     *
     * @return mixed
     */
    public function get($property, $default = null);

    /**
     * Get the parameters for the element.
     *
     * @return array
     */
    public function getParameters();

    /**
     * Get a parameter for the content.
     *
     * @param string $key     The key
     * @param mixed  $default The default value
     *
     * @return mixed
     */
    public function getParameter($key, $default = null);
}
```

### 2.2 Joomla\Content\CompositeElementInterface

The following interface MUST be implemented by compatible Composite Types.

```php
namespace Joomla\Content;

interface CompositeElementInterface extends ContentElementInterface
{
    /**
     * Add a content element as a child.
     *
     * @param ContentElementInterface $element The content element
     */
    public function addElement(ContentElementInterface $element);

    /**
     * Remove a content element.
     *
     * @param ContentElementInterface $element The content element
     */
    public function removeElement(ContentElementInterface $element);

    /**
     * Get the child elements.
     *
     * @return ContentElementInterface[]
     */
    public function getElements();
}
```

### 2.3 Joomla\Content\ContentVisitorInterface

The following interface MUST be implemented by compatible Content Visitors.

```php
namespace Joomla\Content;

interface ContentVisitorInterface
{
    /**
     * Process the content.
     *
     * @param string                  $elementName The name of the content element
     * @param ContentElementInterface $content     The content
     */
    public function visit($elementName, ContentElementInterface $content);

    /**
     * Register a content element.
     *
     * @param string                $elementName The name of the content element
     * @param callable|array|string $handler     The handler for that element
     */
    public function registerContentType($elementName, $handler);
}
```
