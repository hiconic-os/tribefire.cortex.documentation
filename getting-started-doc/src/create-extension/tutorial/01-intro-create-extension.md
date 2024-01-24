# Introduction

This tutorial covers:
* Creating a _Hiconic_ application with a sample `ServiceProcessor`
* Preparing an _Eclipse_ workspace
* Running the application from _Eclipse_
* Adding more `requests` handled by the sample `ServiceProcessor`
* Unit-testing these new `requests`

**Note:** _Hiconic_ was previously called _Tribefire_ and this name or its _tf_ shortcut are used on many places, so don't get confused.


## Motivation

_Hiconic_ offers a modular architecture with a core platform as a base. Everything else comes as an extension, whether it's custom code or common features like:
* Storing data in SQL DB
* `REST` API
* Render data as HTML

Creating a _Hiconic_ application thus means creating an extension and configuring the platform and a list of extensions.


## Preconditions

* [devrock-sdk](/intro/details/devrock-sdk.md) local environment with tooling
* [dev-env](/intro/details/dev-environment.md) understanding
* [Eclipse with Devrock and Tomcat plugins](/eclipse-setup/tutorial/00.intro.md)
