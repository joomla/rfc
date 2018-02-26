# Authorisation Service

This document describes ...

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119][].

[RFC 2119]: http://tools.ietf.org/html/rfc2119

### References

- [RFC 2119][]: Key words for use in RFCs to Indicate Requirement Levels

## 1. Specification

### 1.1 Spec A

### 1.2 Spec B

## 2. Interfaces

### 2.1 AuthorisationInterface

The following interface MUST be implemented by compatible Authorisation Services.

```php
namespace Joomla\Service\Authorisation

use Joomla\DI\ServiceProviderInterface;

/**
 * AuthorisationServiceInterface
 */
interface AuthorisationServiceInterface extends ServiceProviderInterface
{
    /**
     * Check if a particular user is allowed to take a particular action on a particular class or object.
     *
     * @param  UserInterface  $user           The user that will take action
     * @param  string         $action         The action to be taken
     * @param  string|object  $classOrObject  The class or object to act on.
     *
     * @return bool
     */
    public function isAllowed($user, $action, $classOrObject): bool;
      
    /**
     * Get a list of users that are allowed to take an action on a particular class or object.
     *
     * @param  string         $action         The action to be taken
     * @param  string|object  $classOrObject  The class or object to act on.
     *
     * @return UserInterface[]
     */
    public function getUsers($action, $classOrObject): array;

    /**
     * Get a list of actions that a particular user is allowed to take on a particular class or object.
     *
     * @param  UserInterface  $user           The user that will take action
     * @param  string|object  $classOrObject  The class or object to act on.
     *
     * @return string[]
     */
    public function getActions($user, $classOrObject): array;

    /**
     * Get a list of objects that a particular user is allowed to take a particular action on.
     *
     * @param  UserInterface  $user    The role or user that will take action
     * @param  string         $action  The action to be taken
     * @param  string         $class   Optionally restrict to a particular class.
     *
     * @return object[]
     */
    public function getObjects($roleOrUser, $action, $class = null): array;
}
```
