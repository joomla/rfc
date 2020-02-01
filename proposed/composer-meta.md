# \<Subject> Meta Document

## 1. Summary

_What is Subject about?_

[Composer](https://getcomposer.org/) is a dependency manager for PHP.  
Composer allows developers to specify project dependencies in a 
`composer.json` file and then Composer automatically handles the rest.  

![joomacomposer](https://user-images.githubusercontent.com/9974686/73594821-2de60a80-4512-11ea-8e97-91e28b66ba12.png)

Composer makes it easier to keep vendor libraries out of your repo, 
meaning that only application code goes in the git repository.  

It also makes maintaining the latest versions of all required libraries 
easier because you can simply run `composer update` to get the latest 
compatible packages.  

Additionally, you can use Composer to manage extensions.  

Composer has become an essential part of web development:
- [Install TYPO3 via composer](https://docs.typo3.org/m/typo3/guide-installation/master/en-us/QuickInstall/Composer/Index.html)  
- [Contao - Installing with Composer](https://docs.contao.org/books/manual/current/en/01-installation/installing-contao.html#installing-with-composer)
- [Using Composer to Install Drupal](https://www.drupal.org/docs/develop/using-composer/using-composer-to-install-drupal-and-manage-dependencies)
- ... Install Joomla via Composer is missing 


## 2. Why Bother?

In short:  

It can help you and all Joomlers improve how you  

- develop, 
- share, 
- make use of, 
and 
- deploy  

your Joomla code and whole site stacks.  

## 3. Scope

**Currently**, Composer is only used to maintain external libraries shipped together with the CMS.  
Joomla is distributing the `composer.json` file 
through [Github](https://github.com/joomla/joomla-cms) but not through 
the [downloadable packages](https://downloads.joomla.org/). 

### 3.1 Goals

- **Dependency Management**  
If you are working on a project with a framework, you will need 
to update it. As they release new versions with  
o bug fixes and  
o new features,  
you should keep the framework up to date for  
o security,  
o performance and  
o other reasons.  
However, it is tedious to manually download it every time, 
replace the existing files, and retest things. 
Working on legacy projects is something we all want to avoid, isn't it? 
So Dependency Management is the solution.
- **Project directory size**  
The size of the project directory used to be very big. With Composer the 
size reduces. We can get away without keeping the dependencies in 
the project and avoid version mismatches at the same time 
thanks to `composer.lock` file.
- **Autoloading**  
As the project grows in size, so does the number of files we need to include 
in each of the file. PHP autoloading came to the rescue but still it 
was comparatively hard to setup and maintain as dependencies grow. 
A powerful feature of Composer is Autoloading.
- **Platform Requirements**  
The code of our  Joomla package may support only latest PHP versions 
or depend on specific PHP extensions.    
And we can inform Composer about this resulting in prevention 
of package downloads on the systems that don't meet the requirements.
- **Maintaining a library/package**  
Composer highly recommends [Semantic Versioning](https://semver.org/spec/v2.0.0.html) and following that, 
package maintainers can keep focus on actual development without 
worrying about the distribution.

### 3.2 Non-Goals

- **Use Composer on a Production Server** 
 It may be that Composer is entirely safe on a production server, 
but personally my thoughts are that having a program that can write files to 
the server from remote servers would seem to open up a potential security risk, 
and therefore it’s likely better to not have Composer on a production server.

## 4. Approaches

### 4.1 Approach 1

We use Composer to install external libraries. 
We can also use it to install Joomla extensions. 
If we are creating an extension and installing these 
we should take care to use proper version numbers for the libraries so composer 
can handle conflicts for us during composer install or update.


#### 4.1.1 Projects Using Approach 1

https://www.joomlatools.com/developer/tools/composer

### 4.2 Approach 2

In addition to installing the extensions, we can also install Joomla through Composer.

For this we disconnect Joomla as a product from Joomla-Git repository and provide a 
mechanism to create a composer-enabled Joomla installation.

The following `composer.json` file loads Joomla into the package.

```
{
	"name": "vendor/my_joomla_website",
	"description": "Testing to install Joomla via composer",
	"type": "project",
	"license": "GNU",
	"authors": [
		{
			"name": "author",
			"email": "info@author.de"
		}
	],
	"repositories": [
		{
			"type": "git",
			"url": "https://github.com/joomla/joomla-cms.git"
		}
	],
	"require": {
		"joomla/joomla-cms": "4.0.0-alpha12"
	},
	"minimum-stability": "dev",
	"prefer-stable": true
}
```

#### 4.2.1 Projects Using Approach 2

https://www.drupal.org/project/ideas/issues/2958021

### 4.3 Comparison of Approaches

Both approaches can exist side by side. They build on each other. 
We should first decide which is more important and which should be started.

### 4.4 Chosen Approach

## 5. Design Decisions

## 6. People

### 6.1 Editor(s)

* Astrid Günther

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
