# Simple CCK Meta Document

## 1. Summary

A "Simple CCK" system is proposed here to extend the article data model with the help of custom fields and the necessary
functions to filter the contents according to any criteria and to display them in a specific sorting order.

This specification aims to enable users to create simple projects with on-board tools.

## 2. Why Bother?

Currently, if one wants to use custom fields with **Filtering** and **Ordering**, a CCK extension must be installed.
This prevents the majority of Joomla's own features (such as **Tags**, **Custom Fields**, **Categories**, 
**Multi-Language**, **Associations**, **Workflow**, etc.) as well as the majority of other third party extensions from
being used without restriction.

Adding **Filtering** and **Ordering** options based on the **Custom Fields** makes it possible to create a website with
simple custom content types that offers all the possibilities of Joomla without the hassle of a full-fledged CCK.

For example, consider a list of activities to do on weekends, with fields like "date", "free or paid", "city". We need
to be able to filter by activities in a specific city and to sort them by price or by date.

## 3. Scope

### 3.1 Goals

While **Custom Fields** and **Workflow** already give the CMS a considerable degree of flexibility, they still lack
basic functionality. The aim of this proposal is to complete the range of functions so that it meets current
expectations and thus enable users to create simple projects with on-board tools. The built-in functionality should also
enable extension developers to streamline their solutions and achieve better integration with horizontal features such
as **Tagging** and **Versioning**.

### 3.2 Non-Goals

It is not a goal of this proposal to make existing extensions obsolete.

## 4. Approaches

Already in the days of the Idea Portal, the desire for a Content Construction Kit (CCK) was high on the wish list. The
feature request continues to pop up frequently.

In Joomla 3.1, a first attempt towards universal content was made with the Unified Content Model (UCM), but this was
never really pursued. Most Joomla developers do not know how to use this concept properly - or simply ignore it.

Joomla 3.7 brought **Custom Fields** for articles and users, an integration of the DPFields extension into the CMS. As
useful as this new functionality is, it is extremely limited because there is no way to filter or sort by the value of
the **Custom Fields**.

In Joomla 3.9 ([PR#20890](https://github.com/joomla/joomla-cms/pull/20890)), custom admin menus with a lot of **
Filtering** options were added, which is another major step towards a simple CCK supporting (kind of) different content
types.

### 4.1 Provide Custom Content Types

#### 4.1.1 Custom Content Types with Unified Content Model

##### Pros

##### Cons

* UCM is not well accepted; even the core developers are hardly familiar with the concept. Some if not most features are
  not supported by UCM.

#### 4.1.2 Custom Content Types with Content Model

##### Pros

* `com_content` is a first class citizen in the core, so all core features are available to its content.

##### Cons

#### 4.1.3 Custom Content Types with Type Specific Model

##### Pros

* Features like **Filtering** and **Ordering** are easy to implement because of the dedicated database table.

##### Cons

* Core features must be supported explicitly to make them available to the content of the type specific model.

### 4.2 Add Missing Features to **Custom Fields**

The implementation of **Custom Fields** lacks support for **Filtering** and **Ordering**. This approach complements **
Custom Fields** with the missing functions.

##### Pros

* `com_content` is a first class citizen in the core, so all core features are available to its content.
* A specific set of **Custom Fields** can be considered a content type and displayed accordingly in the UI.

##### Cons

### 4.3 Comparison of Approaches

It quickly becomes apparent that the content must be managed by `com_content` so that the various content types can
benefit from the further development of the CMS. The approaches 4.1.1 and 4.1.3 are therefore immediately omitted from
further consideration. The approaches 4.1.2 and 4.2 on the other hand are not mutually exclusive; the **Custom Fields**
complement `com_content` perfectly.

### 4.4 Chosen Approach

**Custom Fields** (`com_fields`) are supplemented by the features

* **Filtering** and
* **Ordering**.

**Custom Fields** can optionally be grouped into categories; the name of the category serves as the content type.

## 5. Design Decisions

## 6. People

### 6.1 Editor(s)

* Suki Nozick <sukinoz@gmail.com>

### 6.2 Sponsors

* Niels Braczek <nbraczek@bsds.de>

### 6.3 Contributors

* N/A

## 7. Votes

* **Entrance Vote:** _(not yet taken)_
* **Acceptance Vote:** _(not yet taken)_

## 8. Relevant Links

_**Note:** Order descending chronologically._

* [Custom Admin Menus PR#20890](https://github.com/joomla/joomla-cms/pull/20890)

## 9. Errata

...
