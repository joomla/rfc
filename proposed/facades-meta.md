# Facades Meta Document

## 1. Summary

The facade pattern (also spelled façade) is a software-design pattern commonly used in object-oriented programming.
Analogous to a facade in architecture, a facade is an object that serves as a front-facing interface masking more
complex underlying or structural code. A facade can:

* improve the readability and usability of a software library by masking interaction with more complex components behind
  a single (and often simplified) API
* provide a context-specific interface to more generic functionality (complete with context-specific input validation)
* serve as a launching point for a broader refactor of monolithic or tightly-coupled systems in favor of more
  loosely-coupled code

Developers often use the facade design pattern when a system is very complex or difficult to understand because the
system has many interdependent classes or because its source code is unavailable. This pattern hides the complexities of
the larger system and provides a simpler interface to the client. It typically involves a single wrapper class that
contains a set of members required by the client. These members access the system on behalf of the facade client and
hide the implementation details. [[Wikipedia: Facade Pattern](https://en.wikipedia.org/wiki/Facade_pattern)]

## 2. Why Bother?

In Joomla, we have lots of places with code like this:

```php
$this->app->getIdentity()->authorise(...)
```

or

```php
Factory::getUser()->authorise(...);
```

While `Factory::getUser()` is deprecated, `$this->app->getIdentity()` relies on knowledge about the internal structure.
Being able to use

```php
User::authorise(...);
```

instead, would lower the cognitive load a lot. Additionally, it would make it easier for us to make changes in the
underlying code without breaking extensions that use the feature in question.
`authorise()` is just a single example here; there are several other places, where the facade pattern would simplify our lives:

* App(lication)
* Auth(orisation)
* Config
* Session
* Lang(uage)
* Doc(ument)
* Database
* Mail(er)
* Event
* Log(ger)

## 3. Scope

### 3.1 Goals

### 3.2 Non-Goals

## 4. Approaches

### 4.1 Composite Pattern

### 4.2 Chosen Approach

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
