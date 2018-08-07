Getting Married is developed with Symfony 4.x and this Wiki is going to document the things commonly interesting to developers about it

# PHPStorm

Install the PHPStorm plugin according to the IDE version
https://github.com/Haehnchen/idea-php-symfony2-plugin/blob/master/CHANGELOG.md#version-names

Down the distributable `.jar` file from [PHPStorm Plugin Page](https://plugins.jetbrains.com/plugin/7219-symfony-plugin)

This plugin offers integration like type hints on DI container like below. Hard-coded `$doctrineRegistry` type hint is no longer necessary and the IDE will resolve and interpret it automatically

```diff
- /** @var \Symfony\Bridge\Doctrine\RegistryInterface $doctrineRegistry */
$doctrineRegistry = $kernel->getContainer()->get('doctrine');
```

# Best Practices

Symfony 4.x has a shift of best practice recommendations comparing to its predecessors (e.g., 3.x).

- A [blog](http://fabien.potencier.org/) of the Symfony author - Fabien Potencier, has documented the philosophies behind Symfony
- Official Symfony [best practices doc](http://symfony.com/doc/current/best_practices/creating-the-project.html#application-bundles)

Here are some highlights:

- [Do Bundle-less application](http://fabien.potencier.org/symfony4-monolith-vs-micro.html#bundle-less-applications)

    Don't create bundle (i.e., equivalent to Magento module) for application logic. The only reason to create bundle is for reusability

- [Use environment variables](http://fabien.potencier.org/symfony4-best-practices.html#environment-variables) or `.env` for setting up infrastructure specific configs (e.g., mysql credentials)

    Avoid `config.yaml`

    Deprecate `parameters.yaml` and use `.env` or environment variables instead

- [Use ORM annotation](https://symfony.com/doc/current/best_practices/business-logic.html#doctrine-mapping-information)

    Avoid `doctrine.yaml`, `.xml`, or `.php` which break up ORM metadata from domain Entity

- More...

# Generate code (e.g., entity, controller, and more)

Thanks to Symfony 4, many skeleton boiler pate code can be generated.

For example, to generate an `WeddingEvent` entity:

```bash
$ php bin/console make:entity WeddingEvent
```

Once an entity is updated / created, we need to reflect the changes in the database schema. Generate and execute migrate:

```bash
# Generate migration script
$ php bin/console make:migration

           
  Success! 
           

 Next: Review the new migration "src/Migrations/Version20180806133408.php"
 Then: Run the migration with php bin/console doctrine:migrations:migrate
 See https://symfony.com/doc/current/bundles/DoctrineMigrationsBundle/index.html

# Execute migration scropt
$ php bin/console doctrine:migrations:migrate
```

Alternative, for a quick and dirty local testing, force the database schema to update:

```bash
# Force database update regardless of migration script
$ php bin/console doctrine:schema --force
```

Note: this is for local testing only. You should always generate migration script and commit to the PR.

# Upgrade application

After pulled latest changes from remote repo, run migrate command to install database changes:

```bash
# Migrate (aka upgrade)
$ php bin/console doctrine:migrations:migrate --quiet
```

# Upgrade Symfony Core

Symfony offers a clear backward compatibility matrix and promise [backward compatibility](http://symfony.com/doc/current/contributing/code/bc.html) for **minor release**.

Upgrading from `4.1.x` to `4.x` is effortless.

```bash
$ composer update "symfony/*" --with-all-dependencies
```

See: https://symfony.com/doc/current/setup/upgrade_minor.html

Symfony 4 is supported until `11/2023`. Until its end of life, we are not expecting any major effort on upgrading it.

https://github.com/AmpersandHQ/gettingmarried/issues/1

# Install from scratch

**Important: we don't usually need to start from scratch as we stick with persisted docker image. This information however is useful for setting up production environment.** 

```bash
# (TBC) Set environment variables
# - need to consult system admin when production environment is ready and find the best way to set them up
# - for the environment variables list, please see ".env.dist"
# $ source .env

# Create database
$ php bin/console doctrine:database:create
Created database `gettingmarried` for connection named default

# Migrate (aka upgrade)
$ php bin/console doctrine:migrations:migrate --quiet
```