# Content Elements Meta Document

## 1. Summary

Content Elements are standardised Data Objects for presentation purposes. They 
represent content structures and element behaviour in a way independent from the
finally generated output.
 
This specification aims to define flexible and useful Content Elements for output
agnostic content structures.

## 2. Why Bother?

Using output agnostic Content Elements allows developers to compose the output they 
need for their application or extension without being limited to support just one 
JavaScript framework. The Content Elements in conjunction with an exchangeable 
renderer decouples the display layer from the application, for which it no longer 
matters, if the output uses BootStrap, Foundation, or Zurb. Other formats like 
eBooks, DocBook, or PDF will become available for all applications, as soon as the 
corresponding renderer is provided.

## 3. Scope

### 3.1 Goals

This specification aims to provide robust interfaces for Content Elements and their 
processing that are independent from the output format.

### 3.2 Non-Goals

This specification does not seek to standardise or favor any particular output 
format.

## 4. Approaches

### 4.1 Composite Pattern

[Composite Pattern]: https://en.wikipedia.org/wiki/Composite_pattern

### 4.2 Chosen Approach

This specification defines Content Elements using the [Composite Pattern][]. 
 
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
