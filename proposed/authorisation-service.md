# Authorisation Service

This document describes ...

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119][].

[RFC 2119]: http://tools.ietf.org/html/rfc2119

### References

- [RFC 2119][]: Key words for use in RFCs to Indicate Requirement Levels

## 1. Specification

### 1.1 Basic Authorisation Service

### 1.2 Extended Authorisation Service

## 2. Interfaces

### 2.1 AuthorisationServiceInterface

The following interface MUST be implemented by compatible Basic Authorisation Services.

```php
namespace Joomla\Service\Authorisation

/**
 * Basic Authorisation Service Interface
 */
interface AuthorisationServiceInterface
{
    /**
     * Check if a particular user is allowed to take a particular action on a particular class or object.
     *
     * @param  UserInterface  $actor   The user that will take action
     * @param  string         $action  The action to be taken
     * @param  string|object  $target  The class or object to act on.
     *                                 May be omitted, if `$action` does not require an object.
     *
     * @return bool
     */
    public function isAllowed($actor, $action, $target = null): bool;
}
```

### 2.2 ExtendedAuthorisationServiceInterface

The following interface MUST be implemented by compatible Extended Authorisation Services.

```php
namespace Joomla\Service\Authorisation

/**
 * Extended Authorisation Service Interface
 */
interface ExtendedAuthorisationServiceInterface
{
    /**
     * Get a list of actors (users) that are allowed to take an action on a particular target (class or object).
     *
     * @param  string         $action  The action to be taken
     * @param  string|object  $target  The class or object to act on.
     *                                 May be omitted, if `$action` does not require an object.
     *
     * @return UserInterface[]
     */
    public function getActors($action, $target = null): array;

    /**
     * Get a list of actions that a particular actor (user) is allowed to take on a particular target (class or object).
     *
     * @param  UserInterface  $actor   The user that will take action
     * @param  string|object  $target  The class or object to act on.
     *                                 May be omitted, if `$action` does not require an object.
     *
     * @return string[]
     */
    public function getActions($actor, $target = null): array;

    /**
     * Get a list of targets (objects) that a particular actor (user) is allowed to take a particular action on.
     *
     * @param  UserInterface  $actor        The role or user that will take action
     * @param  string         $action       The action to be taken
     * @param  string         $targetClass  Optionally restrict to a particular entity class.
     *
     * @return object[]
     */
    public function getObjects($actor, $action, $targetClass = null): array;
}
```
