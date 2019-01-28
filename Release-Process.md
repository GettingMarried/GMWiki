This wiki documents the GM release process. Please keep it up to date and update it as needed if any change introduced in the future.

## Overview

**Sprint size:** 2 weeks (Start from December 2018 and go on, each sprint is 2 week large)

**Cutoff time:** By the end of the sprint, all tickets in that sprint must be either merged and passed on dev, or moved to the next sprint

**version:** `major.minor.hotfix` (`major` is expected to always be 0 until we go live; each sprint release will increase `minor`)

## The Process

### Preparation

After the cutoff time (i.e., the next day after the sprint finishes (aka: the Monday of the first week of every sprint)):

- the releaser (i.e., Torrey) will merge the development branch to the qa branch, tag as a release of the sprint, and deploy to QA; and
- the PM (i.e. Martha) will tag the tickets

### Risk of delay

There is a chance that a ticket may be merged to dev and then failed and need rework. If the ticket cannot be fixed before the cutoff time, we have three options:

- A. delay the release until the issue is fixed by the developer; or worked around it
- B. go on the release and tolerate the issue
- C. pull the changes out of the codebase (this usually create a fair amount of overhead in the process)

Martha, Lissie and Torrey will be responsible to discuss and decide which option to go for according to the situation

If we go for `B`, depend on the situation, we may later introduce hotfix release base on development branch + hotfix PR before the next sprint release.

### Deliverables

- A docker image of the release is created (automatically on docker cloud) and deployed to QA environment
- The tickets (as part of the release) are tagged with the release version
- The codebase (as part of the release) is tagged with the release version

As the codebase is tagged by release, we can revert to the whatever version as needed for any environment

## To release

(To be documented)

### Generate a list of tickets of given version

Generate a ticket list for PM's reference

This command generates the list by:
- compareing between the tags `0.2.0..0.3.0` and;
- looking for merge commits which contain the keyword `GETMARRIED-` (usually in the branch name)

```bash
git log 0.2.0..0.3.0 --merges \
        --pretty=format:"%h %<(10,trunc)%aN %C(white)%<(15)%ar%Creset %C(red bold)%<(15)%D%Creset %s" \
    | grep -o 'GETMARRIED\-\d*' \
    | uniq -u

GETMARRIED-321
GETMARRIED-336
GETMARRIED-451
GETMARRIED-336
GETMARRIED-337
GETMARRIED-327
GETMARRIED-336
GETMARRIED-140
GETMARRIED-418
GETMARRIED-336
GETMARRIED-418
GETMARRIED-418
GETMARRIED-432
GETMARRIED-429
GETMARRIED-136
GETMARRIED-418
GETMARRIED-335
GETMARRIED-396
```
