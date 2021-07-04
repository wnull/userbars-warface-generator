# Generator game userbars Warface

[![Travis (.org)](https://img.shields.io/travis/wnull/warface-ub?style=flat-square)](//travis-ci.com/wnull/warface-ub)
[![Packagist Downloads](https://img.shields.io/packagist/dm/wnull/warface-ub?color=informational&style=flat-square)](//packagist.org/packages/wnull/warface-ub)
[![Packagist License](https://img.shields.io/packagist/l/wnull/warface-ub?style=flat-square)](//packagist.org/packages/wnull/warface-ub) 
[![Packagist Version](https://img.shields.io/packagist/v/wnull/warface-ub?style=flat-square)](//packagist.org/packages/wnull/warface-ub)

A convenient and simple library for generating Warface game userbars, written in PHP.

![Example userbar](https://user-images.githubusercontent.com/33278849/112180519-afb06000-8c0c-11eb-825b-5cd0b1710fa2.png)

## Prerequisites

To work correctly, you will need `php` version `>=7.4`, as well as the `Imagick` module.

## Installation

You can install it using Composer using the following command:

```sh
$ composer require wnull/warface-ub
```

## Using

Before using it, you should read the description of the available methods and their parameters.

#### Standard use

```php
require __DIR__ . '/vendor/autoload.php';

use warface-ub\Draw;
use Warface\Enums\{Location, Game\Servers};

$ub = new Draw(Location::RU);
$ub->get('Идея', Servers::ALPHA);

$image = $ub->create();
```

#### Localization

You can configure localization by passing an optional parameter (default `RU`), where `X` can be either `EN` or `RU`.

```php
$ub = new Draw(Location::X); 
```

The choice of localization influences on the design of the userbar, as well as the `get()` method, which will be requested to the corresponding API server.

## Methods

Below is a list of all available methods with their description of valid parameters.

* ### get()

    **Required** method that executes a request to the game API and retrieves game statistics.

	```php
	get(string $name, int $server): void
	```

* ### make()

    The method is an alternative to the `get()` method, only without a request to the game API. The idea is to create your own game character data based on an array.

 	```php
	make(array $data): void
	```

	To use it correctly, you must pass at least **3 required parameters** in the associative array, such as: <code>nickname</code>, <code>server</code>, <code>rank_id</code>.

* ### edit()

    The method is used to change the game statistics obtained earlier by the `get()` or `make()` method.

	```php
	edit(array $data): void
	```

* ### add()

    The method is used to add game achievements on userbar.

	```php
	add(array $data, array $dir = []): void
	```

	As the first parameter you need to pass an associative array with the required keys: `mark`, `base`, or `stripe`, whose values are numeric achievement IDs. 

	As the second (optional) parameter, you can pass an associative array with the key dir, the value of which will specify the path to the local with achievement's directory.

* ### create()

    **Required** method that generates the final image (the `Imagick` object).

	```php
	create(string $type = Userbar::USER): \Imagick
	```

	The method accepts a parameter of the type of the userbar. The default value is `user`.

	Valid values: `user`, `join`, or `clan`.

## License

The library is distributed under the [MIT](https://github.com/wnull/warface-ub/blob/master/LICENSE) license.