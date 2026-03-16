JWT Client Library for PHP 
============================
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-v2.0%20adopted-ff69b4.svg)](CODE_OF_CONDUCT.md)
[![Build Status](https://github.com/vonage/vonage-php-jwt/workflows/build/badge.svg)](https://github.com/Vonage/vonage-php-jwt/actions?query=workflow%3Abuild)
[![Latest Stable Version](https://poser.pugx.org/vonage/jwt/v/stable)](https://packagist.org/packages/vonage/jwt)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![codecov](https://codecov.io/gh/Vonage/vonage-php-jwt/graph/badge.svg?token=6WIMGZSOUL)](https://codecov.io/gh/Vonage/vonage-php-jwt)

<img src="vonage_logo.png" alt="Vonage logo" />

*This library requires a minimum PHP version of 8.1*

This is the PHP library for generating JWTs to use Vonage's API. To use this, you'll need a Vonage account. 
Sign up [for free at vonage.com/dashboard][signup].

 * [Installation](#installation)
 * [Usage](#usage)
 * [Examples](#examples)
 * [Contributing](#contributing) 

Installation
------------

To use the client library you'll need to have [created a Vonage account][signup].

To install the PHP client library to your project, we recommend using [Composer](https://getcomposer.org/).

```bash
composer require vonage/jwt
```

> You don't need to clone this repository to use this library in your own projects. Use Composer to install it from Packagist.

If you're new to Composer, here are some resources that you may find useful:

* [Composer's Getting Started page](https://getcomposer.org/doc/00-intro.md) from Composer project's documentation.
* [A Beginner's Guide to Composer](https://scotch.io/tutorials/a-beginners-guide-to-composer) from the good people at ScotchBox.

Usage
-----

If you're using Composer, make sure the autoloader is included in your project's bootstrap file:

```php
require_once "vendor/autoload.php";
```

Create a Token Generator with the Application ID and Private Key of the Vonage Application you want to access:

```php
$generator = new Vonage\JWT\TokenGenerator('d70425f2-1599-4e4c-81c4-cffc66e49a12', file_get_contents('/path/to/private.key'));
```

You can then retrieve a generated JWT token by calling the `generate()` method on the Token Generator:

```php
$token = $generator->generate();
```

This will return a string token that can be used for Bearer Authentication to Vonage APIs that require JWTs.

Examples
--------

### Generating a token with a specific Time To Live

By default, Vonage JWT tokens are generated with an Time To Live, or TTL, of 15 minutes after generation. In cases where the token lifetime 
should be different, you can override this setting by calling the `setTTL()` method on the Token Generator and passing the length of seconds
that the token should be valid for

```php
$generator->setTTL(30 * 60); // Set expiration to 30 minutes after token creation
```

### Setting ACLs

Vonage JWTs will default to full access to all of the paths for an application, but this may not be desirable for cases where clients
may need restricted access. You can specify the paths that a JWT token is valid for by using the `setPaths()` or `addPath()` methods
to set the path information in bulk, or add individual paths in a more fluent interface.

```php
// Set paths in bulk
$generator->setPaths([
    '/*/users/**',
    '/*/conversations/**'
]);

// Set paths individually
$generator->addPath('/*/users/**');
$generator->addPath('/*/conversations/**');
```

For more information on assigning ACL information, please see [How to generate JWTs
 on the Vonage Developer Platform](https://developer.nexmo.com/conversation/guides/jwt-acl)

Contributing
------------

This library is actively developed and we love to hear from you! Please feel free to [create an issue][issues] or [open a pull request][pulls] with your questions, comments, suggestions and feedback.

[signup]: https://dashboard.nexmo.com/sign-up?utm_source=DEV_REL&utm_medium=github&utm_campaign=php-client-library
[license]: LICENSE.txt
[issues]: https://github.com/Vonage/vonage-php-jwt/issues
[pulls]: https://github.com/Vonage/vonage-php-jwt/pulls
