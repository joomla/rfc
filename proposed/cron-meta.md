# Cron Support Meta Document

## 1. Summary

Currently there is no easy way to execute automated scripts in Joomla! without the proper server technology.

This proposal aims to define a way to enable integrators/administrators to manage cronjobs or cronjob-alike behaviours in the Joomla! backend.

## 2. Why Bother?

Having some kind of automation on web application is really helpful. Joomla! offers a CLI support but no way to execute this files in an automated way.

There are several approaches which put the burden on the developer but make it hard for the integrator/administrator to manage these scripts.

## 3. Scope

### 3.1 Goals

The goals for this proposal are to

- define a full cronjob/tab manager (com_cron) operated from the Joomla! backend
- define the API to operate with crontab when available on the server
- define the execution of "poor mans crons" without crontab available
- define 3rd party execution possibilities from e.g. hosting panels (CLI)
- define the API for 3rd party developer to integrate their scripts into the manager
- define the workflow how the crons are executed
- define a best practise example for a Joomla! Workflow cron (executing transitions)


### 3.2 Non-Goals

TBD

## 4. Approaches

### 4.1 Approach 1

#### 4.1.1 Projects Using Approach 1

### 4.2 Approach 2

#### 4.2.1 Projects Using Approach 2

### 4.3 Comparison of Approaches

### 4.4 Chosen Approach

## 5. Design Decisions

## 6. People

### 6.1 Editor(s)

* Benjamin Trenkle <benjamin.trenkle@community.joomla.org>

### 6.2 Sponsors

* 

### 6.3 Contributors

* Llewellyn van der Merwe <llewellyn.van-der-merwe@community.joomla.org>
* Niels Braczek <niels.braczek@community.joomla.org>

## 7. Votes

* **Entrance Vote:** _(not yet taken)_
* **Acceptance Vote:** _(not yet taken)_

## 8. Relevant Links

* https://github.com/joomla/joomla-cms/pull/29592#issuecomment-722257503
* https://www.drupal.org/project/poormanscron

## 9. Errata

...
