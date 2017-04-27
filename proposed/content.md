# Content Types

This document describes a common specification for Content Types using the
[Composite Pattern][]. Content Types are standardised Data Objects for presentation
purposes.

[Composite Pattern]: https://en.wikipedia.org/wiki/Composite_pattern

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119][].

[RFC 2119]: http://tools.ietf.org/html/rfc2119

### References

- [Composite Pattern][] on Wikipedia
- [RFC 2119][]: Key words for use in RFCs to Indicate Requirement Levels

## 1. Specification

### 1.1 Content Type

#### Id and Title

Each Content Type provides at least an ID and a title.

##### Example

Let `$element` have ID = 42 and title = "My Element".

```php
/** @var Joomla\Content\ContentTypeInterface $element */
echo $element->getId();

echo $element->getTitle();
```

will output

```
42 

My Element
```

#### Parameters

Each Content Type provides presentation specific parameters.

##### Example

Let `$element` have parameters class = "special" and foo = "bar".

```php
/** @var Joomla\Content\ContentTypeInterface $element */
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

Content Types using this standard MUST implement the following interface:

- `Joomla\Content\ContentTypeInterface`

### 1.2 Compound Content Type

A Compound Content Type is the base type for Content Types with support for
containing other Content Type instances.

Compound Content Types using this standard MUST implement the following interface:

- `Joomla\Content\CompoundTypeInterface`

### 1.3 Content Type Visitor

Content Type Visitors using this standard MUST implement the following interface:

- `Joomla\Content\ContentTypeVisitorInterface`

## 2. Interfaces

### 2.1 Joomla\Content\ContentTypeInterface

The following interface MUST be implemented by compatible Content Types.

```php
namespace Joomla\Content;

interface ContentTypeInterface
{
    /**
     * Visit the content type.
     *
     * @param ContentTypeVisitorInterface $visitor The Visitor
     */
    public function accept(ContentTypeVisitorInterface $visitor);

    /**
     * Get the identifier for the content.
     *
     * @return string
     */
    public function getId();

    /**
     * Get the title for the content.
     *
     * @return string
     */
    public function getTitle();

    /**
     * Get the parameters for the content.
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

### 2.2 Joomla\Content\CompoundTypeInterface

The following interface MUST be implemented by compatible Compound Types.

```php
namespace Joomla\Content;

interface CompoundTypeInterface extends ContentTypeInterface
{
    /**
     * Add a content element as a child.
     *
     * @param ContentTypeInterface $content The content element
     */
    public function addChild(ContentTypeInterface $content);

    /**
     * Remove a content element.
     *
     * @param ContentTypeInterface $content The content element
     */
    public function removeChild(ContentTypeInterface $content);

    /**
     * Get the child elements.
     *
     * @return ContentTypeInterface[]
     */
    public function getChildren();
}
```

### 2.3 Joomla\Content\ContentTypeVisitorInterface

The following interface MUST be implemented by compatible Content Type Visitors.

```php
namespace Joomla\Content;

interface ContentTypeVisitorInterface
{
    /**
     * Process content.
     *
     * @param string               $contentType The name of the content type
     * @param ContentTypeInterface $content     The content
     */
    public function visit($contentType, ContentTypeInterface $content);

    /**
     * Register a content type.
     *
     * @param string                $contentType The name of the content type
     * @param callable|array|string $handler     The handler for that type
     */
    public function registerContentType($contentType, $handler);
}
```
