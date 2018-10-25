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

## Code quality
New code SHOULD be covered by unit/integration tests where possible

Files MUST have a line-break at the end

Unnecessary commented code MUST be removed prior to merging

Empty declarations MUST be removed prior to merging

## Pull requests
PR MUST have a link to Jira ticket

PR MUST have a meaningful description of its purpose

PR description SHOULD be one or two sentences

PR SHOULD include screenshot(s) or recording(s) to show examples of the new work

Commits MUST be accompanied by meaningful commit messages

Automated tests run in TravisCI MUST pass successfully

PRs handling front-end work SHOULD include either screenshots, recordings, or both, to showcase the updated work. 