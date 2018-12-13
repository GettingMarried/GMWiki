This wiki documents the GM release process. Please keep it up to date and update it as needed if any change introduced in the future.

# Overview

**Sprint size:** 2 weeks (Start from December 2018 and go on, each sprint is 2 week large)

**Cutoff time:** By the end of the day of the 2nd-week's Thursday, all tickets in the sprint must be either merged and passed on dev, or moved to the next sprint

## Process

### Preparation

After the cutoff time (i.e., the 2nd-week's Friday morning):

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