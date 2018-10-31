# ADC-GM (Ampersand DevOps Convention for Getting Married)

This wiki is a [ADC (Ampersand DevOps Convention)](https://github.com/AmpersandHQ/devops-conventions#ampersand-devops-conventions) for Getting Married project. It documents all necessary development practices required on
Getting Married project level.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT",
"RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in
[RFC 2119].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt

## Overview

You MUST cover your code changes with automated test whenever it is possible.

## Create new entity

You MUST test ENTITY with at least one integration test.

You MUST test ENTITY relationship (powered by Doctrine) with at least one integration test.

## Create pull requests

### Change codebase

You SHOULD cover all changes with automated tests (e.g., unit, integration, ...etc)

You MUST include ONE line-break at the end of file

You SHOULD remove disabled code

You SHOULD remove empty functions / classes

You SHOULD update comment / documentation as implementation change

You SHOULD start commit messages with present or past tense form of verb (e.g, `Initialise date picker skeleton`)

### Compose pull request

You SHOULD start pull request title with present or pasts tense form of verb

You MUST append Jira ticket number to pull request title

Example:

```
Implement date picker and integrate on storybook (GETMARRIED-129)
```

You MUST include a Jira ticket link (e.g., [GETMARRIED-129](https://ampersand.atlassian.net/browse/GETMARRIED-129)) on pull request

Example:

```
[GETMARRIED-129](https://ampersand.atlassian.net/browse/GETMARRIED-129)
```

You MUST include a description on pull request

You SHOULD use one or two sentences as description on pull request

You SHOULD include at least ONE screenshot on pull request to show the result of the change

Example:

```
![Screenshot](https://user-images.githubusercontent.com/8415896/47373698-41d27800-d6e4-11e8-8a51-f6d1612a6ea9.png)
```

You SHOULD include at least ONE recording (e.g., [Recordit](http://recordit.co/BHiHXUBxC8)) on pull request to show the results of the change 

Example:

```
[Recordit](http://recordit.co/BHiHXUBxC8)
```
