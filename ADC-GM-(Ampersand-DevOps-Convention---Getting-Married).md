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