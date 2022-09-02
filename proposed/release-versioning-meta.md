# Release Versioning Meta Document

## 1. Summary

_This Specification describes how versions are numbered in Joomla projects._

This specification aims to help developers, code reviewers and release managers to determine, whether a new piece or a
change of code belongs to the next patch, minor or major release. It will also cover documentation requirements that are
related to versioning.

## 2. Why Bother?

Sometimes it is hard to tell bug fixes and features apart. The Release Leads want a comprehensive set of rules to be
able to make good and fast decisions about the target release of a contribution.

## 3. Scope

The specification applies to all Joomla projects, e.g., the CMS, the Framework, core extensions, ...

## 4. Considerations

### 4.1 Semantic Versioning

Joomla started to follow [Semantic Versioning](Semver) with release 3.3 in April 2014. The rules were not always
followed strictly ([Issue#16874](16874), [Issue#17583](17583), [Issue#24728](24728) to name a few). This need to change,
because the Joomla ecosystem is heavily depending on reliable information about compatibility. This is done in section 1
of the specification.

[Semver]: https://github.com/semver/semver/blob/master/semver.md

[24728]: https://issues.joomla.org/tracker/joomla-cms/24728

[17583]: https://github.com/joomla/joomla-cms/issues/17583

[16874]: https://github.com/joomla/joomla-cms/issues/16874

### 4.2 API

The main problem with Semantic Versioning seems to be to categorise code contributions as bug fixes or features. This
should be easy enough, as the Semantic Versioning specification is quite clear in that regard. Strongly simplified, it
says: Changes that do not change signatures of functions or methods of the public API and do not add new ones can go
into a patch release.

Unfortunately, Joomla has no official definition of "public API". Section 2 of the specification makes up for the
omission. It describes, how public and internal API are told apart using the `@api` and `@internal` annotations as
proposed by the draft [PSR19][]. It is recommended to add these annotations to existing code. For new code they are
required.

[PSR19]: https://github.com/php-fig/fig-standards/blob/master/proposed/phpdoc-tags.md

### 4.3 Deprecations

The core contributors have not been very cautious about deprecations in the past.
`JObject`, for example, has
been [deprecated for Joomla 3.4](https://github.com/joomla/joomla-cms/issues/6125#issuecomment-75035212), but made it
into Joomla 4 (although renamed to CMSObject) with the deprecation annotation still in place. Section 3 describes how to
handle and document deprecations. Among other things, it stipulates that a replacement must be offered and used, if the
deprecation is not phasing out a feature. This requirement serves several purposes:

- It proves that the new solution actually works where it will end up being used.
- It shows developers, who consider the code as authoritative documentation, how the new solution works and should be
  used.
- It prevents the release managers of the following major version from being surprised by the "leftovers" and maybe
  therefore not being able to meet the schedule.

The documentation requirements make sure that legacy code can easily be adopted to the new implementation.
A comparison of old and new code shall make it easier for developers to adapt their code to the new conditions and
provide sample code for documentation. It is important that the representation of the old and new code is both human-
and machine-readable.

### 4.4 User Interface

From a code point of view, improvements of the user interface do not touch the API and thus are not features in the
sense of Semantic Versioning. Template files, however, work like functions, since they rely on injected variables to
produce the output. This interface between a View and a template is a contract and as such underlies the rules of
Semantic Versioning. Section 4 provides the rules for dealing with user interface changes.

### 4.5 External Dependencies

Section 5 deals with external dependencies, a.k.a. libraries. The implementation details of external dependencies are
not under the control of the Joomla project. Therefore, the code of these dependencies is basically internal and does
not fall under Semantic Versioning. As a result, these dependencies can be updated or even exchanged without breaking
the compatibility promise. As soon as an external API officially becomes part of the public API, as in the case of
Bootstrap, the rules of Semantic Versioning do apply.

## 5. People

### 5.1 Editor(s)

* Niels Braczek <niels.braczek@community.joomla.org>

### 5.2 Sponsors

* Harald Leithner <harald.leithner@community.joomla.org>

### 5.3 Contributors

* N/A

## 6. Votes

* **Entrance Vote:** 2021-11-16 Production Team Leaders
* **Acceptance Vote:** _(not yet taken)_

## 7. Relevant Links

_**Note:** Order descending chronologically._

* [Semantic Versioning Specification](Semver)

## 8. Errata

...
