# Drop Cookies for non logged in users

## 1. Summary

Non logged in users should not get a cookie created from Joomla.

## 2. Why Bother?

The EU law states that whenever cookies are used the use MUST be informed. Actually the law states that whenever a website requires storing data in the filesytem of the user's computer, the user must be informed, so also local storage, indexedDB, etc are also affected. Joomla should not create by default a cookie for non logged in users, the state of the client should remain in the client side. If extensions need to sync the state with the server they should use the Joomla API (eg: com_ajax) and localsession. If the extension needs to persist the client side further (localsession is alive as long as the browser tab is alive) they should ask for permission to do so and only if the permission is given then a cookie should be created.
The TL:DR; here is that:
- Joomla should not create a cookie by default for non logged in users
- This will eliminate the need to ask for permission to store data in the client side as the first interaction with any Joomla site (extremely bad UX)
- The state of the client should remain in the client side
- Extensions should use the Joomla API (eg: com_ajax) and local session for the user state
- Defer asking for permission to store data in the client side until the user intends to log in or do anything that requires the client side to be persisted. It goes without saying that the user be redirected to a page explaining why the can't continue (and probably could change their permissions) if they refuse the perimission to store cookies.

## 3. Scope

### 3.1 Goals

- The session should NOT create a cookie for non logged in users.
- API for syncing the client side state with the server
- Defer asking for permission to store data in the client side until the user intends to log in or do anything that requires the client side to be persisted.
- An end point for the refused permision for cookies

### 3.2 Non-Goals


## 4. Approaches

### 4.1 Composite Pattern

### 4.2 Chosen Approach
 
## 5. Design Decisions

## 6. People

### 6.1 Editor(s)

Dimitris Grammatikogiannis

### 6.2 Sponsors

### 6.3 Contributors

## 7. Votes

* **Entrance Vote:** _(not yet taken)_
* **Acceptance Vote:** _(not yet taken)_

## 8. Relevant Links

## 9. Errata
