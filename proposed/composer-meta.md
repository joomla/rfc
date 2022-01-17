# Composer Meta Document

## 1. Summary

[Composer](https://getcomposer.org/)  is a tool for dependency management in PHP. It allows declaring, installing and
updating the libraries a project depends on.

Joomla's Composer support means that extensions of all kinds can be treated in the same way as libraries.

## 2. Why Bother?

Composer has long been used in Joomla to control the dependencies of libraries. The automatic comparison of the various
requirements, compatibilities and incompatibilities offers a comfort that none of the Joomla Core developers would want
to miss.

Without Composer support, it is at best very difficult for extension developers to provide their own libraries, because
they cannot know whether extensions are already installed that use libraries that may not be compatible with their own
library.

Additionally, there are groups in the Joomla ecosystem for whom the web-based installation is an obstacle because they
have to perform the same activity over and over again in a time-consuming manner. These include agencies that build many
websites, hosters who want to install Joomla at the push of a button, or cloud services and appliance providers. If
Joomla and its extensions can be managed via Composer, it will be easier and more attractive for them to offer Joomla in
their portfolio.

A large number of projects have already opened up to this market and offer the Composer-based installation of both the
main project and associated extensions:

- [TYPO3](https://docs.typo3.org/m/typo3/guide-installation/master/en-us/QuickInstall/Composer/Index.html) ([GitHub](https://github.com/TYPO3/CmsComposerInstallers))
- [Contao](https://docs.contao.org/books/manual/current/en/01-installation/installing-contao.html#installing-with-composer)
- [Drupal](https://www.drupal.org/docs/develop/using-composer/using-composer-to-install-drupal-and-manage-dependencies)
- [WinterCMS](https://wintercms.com/docs/help/using-composer) (formerly known as October CMS)
- [Kirby](https://getkirby.com/docs/cookbook/setup/composer)
- [SilverStripe](https://docs.silverstripe.org/en/4/getting_started/composer/)
- [Pico](https://picocms.org/docs/)
- [Craft CMS](https://craftcms.com/docs/3.x/installation.html)

## 3. Scope

### 3.1 Goals

Composer support is designed to help enterprise users with their work by providing the following features:

* Installing the CMS
* Installing extensions
* Updating the CMS
* Updating extensions
* Uninstalling the CMS
* Uninstalling extensions
* Integrating PHP libraries

### 3.2 Non-Goals

Composer may not be usable everywhere. Therefore, Composer support cannot and should not aim to replace the web-based
installation process.

> Blog post from 2017 on OSTraining:
> [5 Reasons Not to Require Composer in Your CMS](https://www.ostraining.com/blog/coding/composer-cms/).
> The reservations listed are quite understandable. However, they refer to Composer as a requirement without an
> alternative.

## 4. Approaches

### 4.1 Basic Usage

#### Installing Joomla

```shell
composer create-project joomla/joomla-cms <your/installation/directory> ["<version>"]
```

#### Installing an Extension

```shell
composer require <package/name> ["<version constraint>"]
```

### 4.2 Publishing Extensions

### 4.3 Comparison of Approaches

### 4.4 Chosen Approach

## 5. Design Decisions

## 6. People

### 6.1 Editor(s)

* Astrid Günther <astrid.guenther@community.joomla.org>

### 6.2 Sponsors

* Niels Braczek <niels.braczek@community.joomla.org>

### 6.3 Contributors

* N/A

## 7. Votes

* **Entrance Vote:** _(not yet taken)_
* **Acceptance Vote:** _(not yet taken)_

## 8. Relevant Links

_**Note:** Order descending chronologically._

## 9. Errata

...
