<p align="center">
    <a href="https://github.com/yiisoft" target="_blank">
        <img src="https://github.com/yiisoft.png" height="100px">
    </a>
    <h1 align="center">Yii Db Migration</h1>
    <br>
</p>

The package implementing migration for [yiisoft/db](https://github.com/yiisoft/db).

[![Latest Stable Version](https://poser.pugx.org/yiisoft/yii-db-migration/v/stable.png)](https://packagist.org/packages/yiisoft/yii-db-migration)
[![Total Downloads](https://poser.pugx.org/yiisoft/yii-db-migration/downloads.png)](https://packagist.org/packages/yiisoft/yii-db-migration)
[![Build status](https://github.com/yiisoft/yii-db-migration/workflows/build/badge.svg)](https://github.com/yiisoft/yii-db-migration/actions?query=workflow%3Abuild)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/yiisoft/yii-db-migration/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/yiisoft/yii-db-migration/?branch=master) [![Code Coverage](https://scrutinizer-ci.com/g/yiisoft/yii-db-migration/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/yiisoft/yii-db-migration/?branch=master)
[![Mutation testing badge](https://img.shields.io/endpoint?style=flat&url=https%3A%2F%2Fbadge-api.stryker-mutator.io%2Fgithub.com%2Fyiisoft%2Fyii-db-migration%2Fmaster)](https://dashboard.stryker-mutator.io/reports/github.com/yiisoft/yii-db-migration/master)
[![static analysis](https://github.com/yiisoft/yii-db-migration/workflows/static%20analysis/badge.svg)](https://github.com/yiisoft/yii-db-migration/actions?query=workflow%3A%22static+analysis%22)
[![type-coverage](https://shepherd.dev/github/yiisoft/yii-db-migration/coverage.svg)](https://shepherd.dev/github/yiisoft/yii-db-migration)

## Installation

The package could be installed via composer:

```php
composer require yiisoft/yii-db-migration
```

**Note: You must install the repository of the implementation to use.**

Example:

```php
composer require yiisoft/db-sqlite
```

## Configuration

Example using [yiisoft/app](https://github.com/yiisoft/app).

Di-Container:

config/common.php
```php
<?php

declare(strict_types=1);

use Yiisoft\Db\Connection\ConnectionInterface;
use Yiisoft\Db\Sqlite\Connection as SqliteConnection;

return [
    ConnectionInterface::class => [
        '__class' => SqliteConnection::class,
        '__construct()' => [
            'dsn' => 'sqlite:' . __DIR__ . '/Data/yiitest.sq3'
        ]
    ]
];
```

config/console.php
```php
<?php

declare(strict_types=1);

use Yiisoft\Yii\Db\Migration\Service\MigrationService;

return [
    MigrationService::class => [
        '__class' => MigrationService::class,
        'createNamespace()' => [fn () => $params['yiisoft/yii-db-migration']['createNameSpace']],
        'updateNamespace()' => [
            fn () => $params['yiisoft/yii-db-migration']['updateNameSpace']
        ]
    ]
];
```

Now the `MigrationService::class` uses the `View` of the application that is already registered in `yiisoft/view`.

Execute `composer du` in console config its rebuild.

Now we have the `yiisoft/yii-db-migration` package configured and it can be called in the console.

View the list of available commands execute in console: `vendor/bin/yii list`

```
Available commands:
  database/list    Lists all tables in the database.
  generate/create  Generate migration template.
  help             Displays help for a command
  list             Lists commands
  migrate/down     Downgrades the application by reverting old migrations.
  migrate/history  Displays the migration history.
  migrate/new      Displays the first 10 new migrations.
  migrate/redo     Redoes the last few migrations.
  migrate/up       Upgrades the application by applying new migrations.
  serve            Runs PHP built-in web server
```

Help simple command execute in console `vendor/bin/yii generate/create --help`.

```
Description:
  Generate migration template.

Usage:
  generate/create [options] [--] <name>

Arguments:
  name                         Table name for generate migration.

Options:
  -c, --command[=COMMAND]      Command to execute. [default: "create"]
  -f, --fields[=FIELDS]        To create table fields right away
      --and[=AND]              And junction
      --namespace[=NAMESPACE]  Namespace migration
  -h, --help                   Display this help message
  -q, --quiet                  Do not output any message
  -V, --version                Display this application version
      --ansi                   Force ANSI output
      --no-ansi                Disable ANSI output
  -n, --no-interaction         Do not ask any interactive question
  -v|vv|vvv, --verbose         Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug

Help:
  This command Generate migration template
```

## Unit testing

The package is tested with [PHPUnit](https://phpunit.de/). To run tests:

```php
./vendor/bin/phpunit
```

## Mutation testing

The package tests are checked with [Infection](https://infection.github.io/) mutation framework. To run it:

```php
./vendor/bin/infection
```

## Static analysis

The code is statically analyzed with [Psalm](https://psalm.dev/docs/). To run static analysis:

```php
./vendor/bin/psalm
```
