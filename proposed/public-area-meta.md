# Public Area Meta Document

## 1. Summary

Separate server side code from publicly accessible assets. 

## 2. Why Bother?

The simplest and safest way to avoid access to arbitrary files and to restrict access only to specific files is to have
a separate directory for public files. This approach has the advantage that it works independently of the web server
used and requires no further configuration other than setting the document root.

## 3. Scope

### 3.1 Goals

### 3.2 Non-Goals

## 4. Approach

On some shared hosts it might not be possible to move DocumentRoot to a directory of the webspace. Therefore, the public
area must be optional. At the very least, there must be a way to put the public files in the webroot instead of in a
separate directory.
This has to be documented accordingly.

## 5. Design Decisions

* Introduce a config variable for the location of the public directory. The default value for updates is '/', for new
  installations it is '/public/'.
* Make the path available through `JPATH_PUBLIC`.
* If the public directory gets changed, corresponding files and directories are moved:
  * administrator/index.php
  * api/index.php
  * media/
  * index.php
  * .htaccess
  * robots.txt

> The moved files might need some adjustments.

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
