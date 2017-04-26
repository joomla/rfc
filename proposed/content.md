# Content Types

This document describes a common standard for Content Types using the Composite
Pattern.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119).

### References

- [RFC 2119](http://tools.ietf.org/html/rfc2119)

## 1. Specification

A Content Type is ...

Simple Content Types using this standard MUST implement the following interface:

- `Joomla\Content\ContentTypeInterface`

### 1.1 Compound Content Types

Compound Content Types using this standard MUST implement the following interface:

- `Joomla\Content\CompoundTypeInterface`

### 1.2 Content Type Visitor

## 2. Interfaces

### 2.1 Joomla\Content\ContentTypeInterface

The following interface MUST be implemented by compatible Content Types.

```php
namespace Joomla\Content;

interface ContentTypeInterface
{
    /**
     * Visits the content type.
     *
     * @param   ContentTypeVisitorInterface $visitor The Visitor
     *
     * @return  void
     */
    public function accept(ContentTypeVisitorInterface $visitor);

    /**
     * Gets the identifier for the content
     *
     * @return  string
     */
    public function getId();

    /**
     * Gets the title for the content
     *
     * @return  string
     */
    public function getTitle();

    /**
     * Gets the parameters for the content
     *
     * @return  array
     */
    public function getParameters();

    /**
     * Gets the parameters for the content
     *
     * @param   string  $key     The key
     * @param   mixed   $default The default value
     *
     * @return  mixed
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
     * Add a content element as a child
     *
     * @param   ContentTypeInterface $content The content element
     *
     * @return  void
     */
    public function add(ContentTypeInterface $content);
}
```

### 2.3 Joomla\Content\ContentTypeVisitorInterface

The following interface MUST be implemented by compatible Content Type Visitors.

```php
namespace Joomla\Content;

interface ContentTypeVisitorInterface
{
    /**
     * Render content.
     *
     * @param   string               $contentType The name of the content type
     * @param   ContentTypeInterface $content     The content
     *
     * @return  void
     */
    public function visit($contentType, ContentTypeInterface $content);

    /**
     * Register a content type.
     *
     * @param   string                $type    The content type
     * @param   callable|array|string $handler The handler for that type
     *
     * @return  void
     */
    public function registerContentType($type, $handler);
}
```
