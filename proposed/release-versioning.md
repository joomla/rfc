# Release Versioning

This specification describes how versions are numbered in Joomla projects. It also defines documentation requirements
related to versioning.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119][].

[RFC 2119]: https://www.rfc-editor.org/rfc/rfc2119.html

### Definitions

* "Structural Element" is a collection of Programming Constructs which MAY be preceded by a DocBlock. The collection
  contains the following constructs:
    * class
    * interface
    * trait
    * function (including methods)
    * property
    * constant
    * variables, both local and global scope.

### References

- [RFC 2119][]: Key words for use in RFCs to Indicate Requirement Levels

## Specification

### 1 Semantic Versioning

1. All releases in all Joomla projects MUST strictly follow the [Semantic Versioning](Semver) specification in its
   current version.

[Semver]: https://github.com/semver/semver/blob/master/semver.md

### 2 API

Because Semantic Versioning applies to public API only, a distinction between public and internal API is needed.

#### 2.1 Public API

"Public API" describes the sum of structural elements that MAY be used by extension developers.

1. Changes to the public API are subject to the rules of semantic versioning.
2. In order to distinguish these elements from the internal elements, the following applies:
    1. Existing public structural elements SHOULD be annotated with `@api` in the corresponding DocBlock.
    1. Newly introduced public structural elements MUST be annotated with `@api` in the corresponding DocBlock.
    2. Public structural elements MUST be included in the official documentation.

#### 2.2 Internal API

The "Internal API" comprises the structural elements that are supportive for the core and SHOULD NOT be used by
extension developers.

1. Changes to the internal API are not subject to the rules of semantic versioning.
2. In order to distinguish these elements from the public elements, the following applies:
    1. Existing internal structural elements SHOULD be annotated with `@internal` in the corresponding DocBlock.
    1. Newly introduced structural elements MUST be annotated with `@internal` in the corresponding DocBlock.
    2. Structural elements with the access modifier `private` and structural elements in final classes with the access
       modifier `protected` MUST be treated as internal.
    3. Internal structural elements MUST NOT be included in the official documentation. All documentation needed by core
       developers SHOULD be available in the corresponding DocBlock.

### 3 Deprecations

Deprecating existing functionality is a normal part of software development and is often required to make forward
progress. There are two reasons to deprecate code: (1) architectural changes or (2) removal of features. This section
applies to public API only.

#### 3.1 Architectural Changes

1. The official documentation MUST be updated to let users know about the change.
    1. The DocBlock MUST be annotated to document the replacement for the deprecated element. The deprecation annotation
       SHOULD be supplemented by a usage example for the replacement. Example:
       ```php
       /**
        * ...
        * @deprecated X.Y  Will be removed in X+1.0. Use <replacement> instead. 
        *                  Before (version < X.Y):
        *                  <sample code with deprecated element>
        *                  After (version >= X.Y):
        *                  <sample code using the replacement>
        */
       ```
       with X.Y being the minor version introducing the deprecation.
2. A new minor release MUST be issued with the deprecation in place. That release MUST NOT use the deprecated code
   anywhere.
3. The deprecated code MUST be removed in the next major release.

#### 3.2 Phasing out Features

1. The official documentation MUST be updated to let users know about the change.
    1. The DocBlock MUST be annotated to document the replacement for the deprecated element. The deprecation annotation
       SHOULD be supplemented by a recommendation for an alternative. Example:
       ```php
       /**
        * ...
        * @deprecated X.Y  Will be removed in X+1.0 without replacement. 
        *                  Please consider using <solution A> or <solution B> instead.
        */
       ```
       with X.Y being the minor version introducing the deprecation.
2. A new minor release MUST be issued with the deprecation in place. That release MUST NOT use the deprecated code
   anywhere.
3. The deprecated code MUST be removed in the next major release.

### 4 User Interface

1. Changes to the user interface are considered compatible if they do not affect the public API.
2. If variables passed to or required by template files change, it MUST be treated as a change of the public API.

### 5 External Dependencies

1. Updating external dependencies is considered compatible since it does not affect the public API.
2. The API of the dependencies is not part of the project's API, unless explicitly stated in the official documentation.
3. Extension developers MUST NOT rely on the presence of dependencies that are not covered in the official documentation.
