# Authorisation Service Meta Document

## 1. Summary

Authorization is the function of specifying access rights/privileges to resources related to information security and computer security in general and to access control in particular. More formally, "to authorize" is to define an access policy. [Wikipedia](https://en.wikipedia.org/wiki/Authorization)

This specification aims to define a minimal interface for a service allowing to use Role Based Access Control in components, if they need to.

## 2. Why Bother?

While standard permissions can be implemented in way that components do not need to address it themselves, some components might need a more fine grained access to the permissions. A standardised interface enables 3PD to develop authorisation services which can be consumed by those components without having to deal with implementation details.

## 3. Scope

### 3.1 Goals

This specification aims to provide robust interfaces for querying permissions and related information from Authorisation Services that are independent from the particular implementation.

### 3.2 Non-Goals

This specification does not seek to standardise or favor any particular implementation.
The setup and creation of roles and permissions is up to the implementation and not part of this specification.

## 4. Approaches

### 4.1 Access Control in the User Object

#### Examples
 
##### Zizaco/[Entrust][]:

```php
$allowed = $user->hasRole('admin');
$allowed = $user->can('edit-user');
```

##### Joomla 3.7:

```php
$allowed = JFactory::getUser()->authorise('core.delete', 'com_content.article.' . (int) $record->id)
```

#### 4.1.1 Projects Using Access Control in the User Object

  * Joomla 3
  * Zizaco/[Entrust][] (Laravel 5 Package)
  
[Entrust]: https://github.com/Zizaco/entrust

### 4.2 Separated Access Control

#### 4.2.1 Projects Using Separated Access Control

### 4.3 Comparison of Approaches

While having Access Control in the User Object seems very convenient, it requires the user object to support access control explicitly, which violates the Separation of Concern Principle.
 
### 4.4 Chosen Approach

This specification follows the Separated Access Control approach.

## 5. Design Decisions

## 6. People

### 6.1 Editor(s)

* Niels Braczek, <nbraczek@bsds.de>

### 6.2 Sponsors

* N/A

### 6.3 Contributors

* N/A

## 7. Votes

* **Entrance Vote:** _(not yet taken)_
* **Acceptance Vote:** _(not yet taken)_

## 8. Relevant Links

_**Note:** Order descending chronologically._

## 9. Errata

...
