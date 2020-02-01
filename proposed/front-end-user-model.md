## 1. Summary

Currently the front-end does not have a method to display a list of Users from a certain User Group.
To make it easier for developers and integrators we should make available a method to retrieve a list of users,  
to display on the front-end of the website, without having to create a new component + model.

## 2. Why Bother?

The Users manager has Custom Fields. At the moment the full potential of this combination is not used in the front-end.

## 3. Scope

The front-end does not have a model + view to display a list of Users.
You cannot use the back-end model of com_users in the front-end because that model has some authentication so that you cannot get data from the Users table 
if you are not logged in.

Use cases:
- **Magazine websites** - Categories + Articles are already in Joomla. Display a list of all Authors (Users that are in the "Author" User Group) is not possible without using a 3rd party extensions. 
It would be great if we could display a list of selected users with just the Joomla core. 
- **Association + Portal websites** - Can display a list of their Members (including Custom Fields like Photo, membership, social media links, etc) to their own Members using a Menu Item of type Registered
- **Other case** - With a template override you could hide any Personal Data that is now available in the Users table, and only show the Custom Fields that the Users can add themselves. In that case this new front-end User Model is only used to navigate between those Custom Fields.

### 3.1 Goals

This specification aims to provide a method to retrieve Users in the front-end of Joomla.

Security related. We have to double, triple, check that the views can only be used if they are made available on purpose, via a Menu Item.
So you won't just make a list of users available on you sites front-end:
* the Lists will only show if a Menu Item has been created.
* the Menu Item of a list of Users can be set to Registered

## 9. Errata

PR already exists: https://github.com/joomla/joomla-cms/pull/25030
