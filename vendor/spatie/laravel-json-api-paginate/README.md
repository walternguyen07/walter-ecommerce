# A paginator that plays nice with the JSON API spec

[![Latest Version on Packagist](https://img.shields.io/packagist/v/spatie/laravel-json-api-paginate.svg?style=flat-square)](https://packagist.org/packages/spatie/laravel-json-api-paginate)
![GitHub Workflow Status](https://img.shields.io/github/workflow/status/spatie/laravel-json-api-paginate/run-tests?label=tests)
[![Quality Score](https://img.shields.io/scrutinizer/g/spatie/laravel-json-api-paginate.svg?style=flat-square)](https://scrutinizer-ci.com/g/spatie/laravel-json-api-paginate)
[![StyleCI](https://styleci.io/repos/94352951/shield?branch=master)](https://styleci.io/repos/94352951)
[![Total Downloads](https://img.shields.io/packagist/dt/spatie/laravel-json-api-paginate.svg?style=flat-square)](https://packagist.org/packages/spatie/laravel-json-api-paginate)

In a vanilla Laravel application [the query builder paginators will listen to `page` request parameter](https://laravel.com/docs/5.4/pagination#paginating-query-builder-results). This works great, but it does not comply with [the json:api spec](http://jsonapi.org/). That spec [expects](http://jsonapi.org/examples/#pagination) the query builder paginator to listen to the `page[number]` and `page[size]` request parameters. 

This package adds a `jsonPaginate` method to the Eloquent query builder that listens to those parameters and adds [the pagination links the spec requires](http://jsonapi.org/format/#fetching-pagination).

## Support us

We invest a lot of resources into creating [best in class open source packages](https://spatie.be/open-source). You can support us by [buying one of our paid products](https://spatie.be/open-source/support-us). 

We highly appreciate you sending us a postcard from your hometown, mentioning which of our package(s) you are using. You'll find our address on [our contact page](https://spatie.be/about-us). We publish all received postcards on [our virtual postcard wall](https://spatie.be/open-source/postcards).

## Installation

You can install the package via composer:

```bash
composer require spatie/laravel-json-api-paginate
```

In Laravel 5.5 and above the service provider will automatically get registered. In older versions of the framework just add the service provider in `config/app.php` file:

```php
'providers' => [
    ...
    Spatie\JsonApiPaginate\JsonApiPaginateServiceProvider::class,
];
```

Optionally you can publish the config file with:

```bash
php artisan vendor:publish --provider="Spatie\JsonApiPaginate\JsonApiPaginateServiceProvider" --tag="config"
```

This is the content of the file that will be published in `config/json-api-paginate.php`

```php
<?php

return [

    /*
     * The maximum number of results that will be returned
     * when using the JSON API paginator.
     */
    'max_results' => 30,

    /*
     * The default number of results that will be returned
     * when using the JSON API paginator.
     */
    'default_size' => 30,

    /*
     * The key of the page[x] query string parameter for page number.
     */
    'number_parameter' => 'number',

    /*
     * The key of the page[x] query string parameter for page size.
     */
    'size_parameter' => 'size',

    /*
     * The name of the macro that is added to the Eloquent query builder.
     */
    'method_name' => 'jsonPaginate',

    /*
     * Here you can override the base url to be used in the link items.
     */
    'base_url' => null,

    /*
     * The name of the query parameter used for pagination
     */
    'pagination_parameter' => 'page',
];
```

## Usage

To paginate the results according to the json API spec, simply call the `jsonPaginate` method.

```php
YourModel::jsonPaginate();
```

Of course you may still use all the builder methods you know and love:

```php
YourModel::where('my_field', 'myValue')->jsonPaginate();
```

By default the maximum page size is set to 30. You can change this number in the `config` file or just pass the value to  `jsonPaginate`.

```php
$maxResults = 60;

YourModel::jsonPaginate($maxResults);
```

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Testing

```bash
composer test
```

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Security

If you discover any security related issues, please email freek@spatie.be instead of using the issue tracker.

## Credits

- [Freek Van der Herten](https://github.com/freekmurze)
- [All Contributors](../../contributors)

The base code of this page was published on [this Laracasts forum thread](https://laracasts.com/discuss/channels/laravel/pagination-using-json-api-strategy?page=1#reply-346619) by [Joram van den Boezem](https://twitter.com/@hongaar)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
