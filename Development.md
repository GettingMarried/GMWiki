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
DATABASE_URL=mysql://root:@127.0.0.1:23322/gettingmarried \
    php vendor/bin/simple-phpunit \
    --coverage-text \
    # --testsuite=unit \ # (Optional) Execute only unit test suite
```

Note: Substitute `--testsuite=unit` with different suites for target scopes (`functional`, `integration`, or `unit`)

**NOTE: This command is all you need if there isn't any db error**

### Set up perquisites for integration / functional test

For database state specific tests, a test db is required to run the test suites.

An error may occur if an expected state is not met:

```diff
$ php vendor/bin/simple-phpunit
+ SQLSTATE[3D000]: Invalid catalog name: 1046 No database selected
```

When this happens, follow below sections to set it up.

#### Make sure test-db is up

A `test-db` is created and exposed with port `23322` locally for Integration Test and Functional Test, which rely on database state. It is a vanilla `ampco/mysql` with no data.

```diff
$ docker ps --format="table {{.Image}}\t{{.Names}}\t{{.Ports}}" | grep gettingmarried        
+ ampco/mysql                                           gettingmarried_test-db_1         0.0.0.0:23322->3306/tcp
gettingmarried_varnish                                gettingmarried_varnish_1         0.0.0.0:8102->80/tcp
redis                                                 gettingmarried_redis_1           0.0.0.0:6387->6379/tcp
ampco/mysql                                           gettingmarried_db_1              0.0.0.0:23321->3306/tcp
```

If you want to recreate the test-db (for example, for a clean test), run:

```bash
$ docker stop gettingmarried_test-db_1; docker rm gettingmarried_test-db_1
$ docker-compose --file=./docker-compose.yml up -d
Creating gettingmarried_test-db_1 ... done
```

#### Set up test-db

1. Install database to test-db

    ```bash
    $ DATABASE_URL=mysql://root:@127.0.0.1:23322/gettingmarried \
        php bin/console doctrine:database:create
    Created database `gettingmarried` for connection named default
    ```

2. Install tables to test-db

    ```bash
    $ DATABASE_URL=mysql://root:@127.0.0.1:23322/gettingmarried \
        php bin/console doctrine:migrations:migrate --quiet
    ```

3. Load fixtures to test-db (i.e., test data for running test cases)

    ```bash
    DATABASE_URL=mysql://root:@127.0.0.1:23322/gettingmarried \
        php bin/console doctrine:fixtures:load --quiet
    ```

    NOTE: Integration / functional tests usually depend on database state. This loads the fixtures into database to offer the required test data.