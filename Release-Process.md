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

### Smoke test development environment

Before releasing to QA, developer must smoke test the dev environment to ensure nothing obvious will break QA.
Smoke test should include the following tasks:
- Homepage
- Couple login, register and logout
- Wedding website pages ( `/wedding/guest/1` and `/wedding/couple` )
- CMS page
- Admin login and logout
- Admin package list and form
- Admin audit

If the development environment failed testing, identify the issue by SSH-ing into the web container in Cloud 66 and debug or investigate the logs.

_Note: you may need to download the [Cloud 66 Toolbelt](https://help.cloud66.com/skycap/quickstarts/using-cloud66-toolbelt.html) to be able to SSH from your laptop._

### Create release pull request

Create a pull request from `development` branch to the `qa` branch.
Go through the PR diff to make sure only related tickets are being deployed.
Make sure travis is passing and don't merge the PR until all checks have passed successfully.

If travis failed for any reason, identify the issue by re-running the travis build in debug mode and run each command as described in the [documentation](https://docs.travis-ci.com/user/running-build-in-debug-mode/#things-to-do-once-you-are-inside-the-debug-vm) to get more information.

### Generate a list of tickets of given version

Generate a ticket list for PM's reference

This command generates the list by:
- compareing between the tags `0.2.0..0.3.0` and;
- looking for merge commits which contain the keyword `GETMARRIED-` (usually in the branch name)

```bash
git log 0.2.0..0.3.0 --merges \
        --pretty=format:"%h %<(10,trunc)%aN %C(white)%<(15)%ar%Creset %C(red bold)%<(15)%D%Creset %s" \
    | grep -o 'GETMARRIED\-\d*' \
    | sort | uniq

GETMARRIED-136
GETMARRIED-140
GETMARRIED-321
GETMARRIED-327
GETMARRIED-332
GETMARRIED-335
GETMARRIED-336
GETMARRIED-337
GETMARRIED-396
GETMARRIED-418
GETMARRIED-429
GETMARRIED-432
GETMARRIED-451
GETMARRIED-509
```

### Deploy

Once all checks on the PR have passed ✅, you can merge the PR.

Merging the PR will automatically trigger the deployment process, no manual trigger required.
You can monitor the progress via Docker cloud and Cloud 66 live logs.

**Once the PR is merged, make sure to create a new tag for the repository with the version number on the deployment ticket!**

### Post deployment checks

Once the deployment is done, you should smoke test the qa website (same steps as on dev) to insure that the website is functional and contain the changes in the release.

If the deployment requires new database fixtures, this can be done after the deployment by following these steps:
- Re-deploy the database container from Cloud 66 (to get a new and empty copy)
- SSH into the web container by running:
```
cx ssh -s 'gettingmarried' -e development master
docker exec -u www-data -it $(docker ps -q -f name=web_web) bash
```bash
- Make sure the database is empty by running `mysql -uroot -hdb gettingmarried` and `show tables;`
- Run `make auth` to insure environment variables are set
- Run `composer install -o` to install dev dependencies
- Run `rm -rf var/cache/` and `php bin/console redis:flushall` to flush the caches
- Run the following command to re-install the data:
```bash
php bin/console doctrine:migrations:migrate --quiet
php bin/console doctrine:phpcr:repository:init
php bin/console doctrine:phpcr:node:dump
php bin/console doctrine:phpcr:fixtures:load
APP_ENV=dev php bin/console doctrine:fixtures:load --append #dev mode is required while running this command
```
- Finally, re-deploy the web container via Cloud 66 to remove the dev dependancies

### Deployment Gotcha
- Sometimes, when caches are missed significantly due to changes in dependencies, a new `prebuilt` docker image is required, see https://github.com/AmpersandHQ/gettingmarried/blob/development/Dockerfile-prebuilt on how it is built.
- Some deployments will depend on environment variables, make sure to set these variables in Cloud 66 for each environment before deploying. If the deployment is done already, set the missing variables and re-deploy.