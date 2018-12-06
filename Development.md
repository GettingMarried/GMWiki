Continue Integration is the heart of this Gettingmarried development process. To enable it, this Wiki documented the necessary steps and methodologies needed to execute by each Developer.

- TDD
- BDD
- CI
- PR

If you are [New to Symfony](https://github.com/AmpersandHQ/gettingmarried/wiki/New-to-Symfony-4.x), have a look at the wiki, it documents the basic and best practices for developers.

## TDD (test driven development)

Each PR MUST be covered by automated tests in any forms of:

- Unit Test (located in: `tests/Unit`)

    This is test which DO NOT need symfony kernel to run

- Integration Test (located in: `tests/Integration`)

    This is test which DO need symfony kernel to run; however DO NOT run on http request level

- Functional Test (located in: `tests/Functional`)

    This is test which DO need symfony kernel to run; and DO run on http request level

- Feature Test (aka: Behaviour Test / driven by Behat / located in `tests/features`)

    This is functional test but implemented with Behat for clear test scenarios and reusability

It depends on the PR's nature to apply different forms of tests. We usually target Unit Test / Integration Test.

### Run test

To execute all test suites:

```bash
make test
```

or:

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

## BDD (Behaviour Driven Development)

BDD share the same idea of TDD, having the test build and failed before we actually implement it. The main difference between them is, BDD writes test with **text**, in domain specific language, which aims at understandable by stakeholders.

However, the reason we do BDD isn't because of domain specific language. Instead, is to increase the maintainability of API test cases as they usually have multiple states to confirm or execute before test cases can execute. We use [Behat](http://behat.org/) to test API.

### Define steps

A test case is called feature and it looks like this:

```feature
Given there is a "Sith Lord Lightsaber", which costs £5
When there is a "Sith Lord Lightsaber", which costs £10
Then there is an 'Anakin Lightsaber', which costs £10
And there is a Lightsaber, which costs £2
But there is a Lightsaber, which costs £25
```

This is a step:

```feature
Given there is a "Sith Lord Lightsaber", which costs £5
```

How does Behat know what to do when it sees a step?

```php
/**
 * @Given there is a(n) :arg1, which costs £:arg2
 */
public function thereIsAWhichCostsPs($arg1, $arg2)
{
    throw new PendingException();
}
```

For details, see [defining-steps](http://behat.org/en/latest/quick_start.html#defining-steps)

Api-platform has implemented api [related steps](https://api-platform.com/docs/distribution/testing/#testing-and-specifying-the-api) out of the box and we only need to maintain the minimal customisation (if any)