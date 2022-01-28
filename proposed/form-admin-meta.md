# Form Admin Meta Document

## 1. Summary

Joomla uses forms that are defined in XML and rendered using the Form class.

Although this is a flexible way and the forms can be changed using plugins, it is limited and hard-coded in some ways.

This specification aims to define an extension to the form creation process. This form editor shall allow modifying
forms, add or remove predefined fields and custom fields and change their order.

## 2. Why Bother?

Hard-coded forms are no longer state of the art. Joomla today offers a lot of flexibility, but it needs developers to
implement changes. If we can change the way we create forms, we would allow website creators to adapt Joomla to better
meet users' needs.

## 3. Scope

### 3.1 Goals

The goal is to provide a graphical user interface for creating and editing forms and views as a core component. Standard
fields and user-defined fields are to be equally supported.

When saved, user-defined fields must be included in versioning, provided the affected extension/feature supports versioning.

The functionality shall also be available for extensions.

In the course of the
implementation, [accessibility requirements and recommendations](https://accessibilitycluster.com/main-results/forms-editor)
should be taken into account.

### 3.2 Non-Goals

It is not the goal of this component to force changes to 3rd party extensions.

## 4. Approaches

The component will consist of a Visual Editor and a Form Preprocessor. The preprocessor splits the form content so that
the handler of the original form gets the data it expects and ensures the correct handling of the remaining form
content.

Database constraints are implemented through business logic within the models and not at the database level. In the
course of revising the database, this should be corrected if possible.

### 4.1 Chosen Approach

## 5. Design Decisions

## 6. People

### 6.1 Editor(s)

* Robert Deutz <rdeutz@googlemail.com>

### 6.2 Sponsors

* Niels Braczek, <nbraczek@bsds.de>

### 6.3 Contributors

* N/A

## 7. Votes

* **Entrance Vote:** _(not yet taken)_
* **Acceptance Vote:** _(not yet taken)_

## 8. Relevant Links

_**Note:** Order descending chronologically._

## 9. Errata

...
