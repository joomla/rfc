# Form Admin Meta Document

## 1. Summary

Joomla uses forms based on XML and rendered with the help of the Form class.

While this is a flexible way and the forms can be changed with plugins, it is limited and in some way hard coded. Database constraints are implemented through business logic within the models and not on the database level.
 
This specification aims to define an extension of the form building process. After implementation it allows site builder the change the core forms. Adding and removing fields should be possible and core form building and custom fields are merged. 

## 2. Why Bother?

Hard coded forms are not state of the art. Joomla! allows today a lot of flexibility but it is up to developers to implement. If we can change the way we are creating forms we would allow site builders to change Joomla that it fulfils the needs of clients better.  

## 3. Scope

Planned feature for Joomla5.

### 3.1 Goals

Having a core component that allows configuration of forms and views. This includes custom fields and a migration from Joomla4.

Respect versioning for custom fields.

Creating a API for 3rd part components to use the functionality.

### 3.2 Non-Goals

Migration of 3rd part components to the new way of form rendering. 

## 4. Approaches

### 4.1 Chosen Approach

TBD
 
## 5. Design Decisions

None at this state

## 6. People

### 6.1 Editor(s)

* Robert Deutz <rdeutz@googlemail.com>

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
