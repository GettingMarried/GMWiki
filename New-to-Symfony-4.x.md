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

    Deprecate `config.yaml`

- More...