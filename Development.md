Continue Integration is the heart of this Gettingmarried development process. To enable it, this Wiki documented the necessary steps and methodologies needed to execute by each Developer.

- TDD
- CI
- PR

## TDD (test driven development)

Each PR MUST be covered by automated tests in any forms of:
- Unit Test (located in: `tests/Unit`)
- [Integration Test](https://stackoverflow.com/a/3670767) (located in: `tests/Integration`)
- Functional Test (located in: `tests/Functional`)

It depends on the PR's nature to apply different forms of tests. We usually target Unit Test / Integration Test.

### Run test

To execute all test suites:

```bash
env $(cat .env | grep -v "#" | xargs) php vendor/bin/simple-phpunit \
    --coverage-text \
    # --testsuite=unit \ # (Optional) Execute only unit test suite
```

- `.env` is the environment variables file that include infrastructure specific setups (e.g., mysql credentials)
- `env $(cat .env | grep -v "#" | xargs)` disassemble the `.env` file and assign its env vars to the `simple-phpunit` command
- Substitute `--testsuite=unit` with different suites for target scopes (`functional`, `integration`, or `unit`)

**NOTE: This command is all you need if there isn't any db error**

### Load test fixtures (i.e., test data for running test cases)

You will need to do this if you have:
- modified `src/DataFixtures`; or
- reinstalled a fresh instance (e.g., just finished running `make osx-local` or `make osx-docker-services`)

Load test fixtures:

```bash
php bin/console doctrine:fixtures:load --append
```

Note: Always use `--append` to append the data fixtures instead of deleting all data from the database first

If you want to recreate the db (for example, for a clean test), run:

```bash
$ docker stop gettingmarried_db_1; docker rm gettingmarried_db_1
$ docker-compose --file=./docker-compose.yml up -d
Creating gettingmarried_db_1 ... done
```

or simply:

```bash
$ make osx-docker-services
```
