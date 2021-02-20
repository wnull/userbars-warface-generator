# Generator game userbars Warface

[![Travis (.org)](https://img.shields.io/travis/wnull/wfub?style=flat-square)](https://travis-ci.com/wnull/wfub) [![Packagist Downloads](https://img.shields.io/packagist/dm/wnull/wfub?color=informational&style=flat-square)](//packagist.org/packages/wnull/wfub) [![Packagist License](https://img.shields.io/packagist/l/wnull/wfub?style=flat-square)](//packagist.org/packages/wnull/wfub) ![Packagist Version](https://img.shields.io/packagist/v/wnull/wfub?style=flat-square)

A convenient and simple library for generating Warface game userbars, written in PHP.

## Dependencies

To work correctly, you will need `php` version `>=7.4`, as well as the `Imagick` module.

## Installation

You can install it using Composer using the following command:

```sh
composer require wnull/wfub
```

## Using

Before using it, you should read the description of the available methods and their parameters.

#### Common use

```php
require __DIR__ . '/vendor/autoload.php';

use WFub\Draw;
use Warface\Enums\{Location, Game\Servers};

$ub = new Draw(Location::RU);
$ub->get('Сласть', Servers::ALPHA);

$image = $ub->create();
```

#### Localization

By default, the russian localization is set.

```php
$ub = new Draw(Location::RU);
$ub->get('Сласть', Servers::ALPHA);
```

The choice of localization depends on the design of the userbar, as well as the `get()` method, which will be requested to the corresponding API server.

```php
$ub = new Draw(Location::EN);
$ub->get('thebavoz', Servers::EU);
```

## Methods and description

Below is a list of all available methods with their description of valid parameters.

* ### get()
	```php
	get(string $name, int $server): void
	```
	**Required** method that executes a request to the game API and retrieves game statistics.

	Example:
	```php
	$ub->get('Сласть', Servers::ALPHA);
	```
  
* ### make()
 	```php
	make(array $data): void
	```
	The method is an alternative to the `get()` method, only without a request to the game API. The idea is to create your own game character data based on an array.
	
	<details>
		<summary>Additional information</summary>
		<p>	</p>
		<p>To use it correctly, you must pass at least 3 required parameters in the associative array, such as: <code>nickname</code>, <code>server</code>, <code>rank_id</code>.</p>
	</details>

	Example:
	```php
	$ub->make([
	    'nickname' => 'Никнейм',
	    'server' => Servers::BRAVO,
	    'rank_id' => 69,
	    'clan_name' => 'Название_Клана'
	]);
	```

* ### edit()
	```php
	edit(array $data): void
	```
  The method is used to change the game statistics obtained earlier by the `get()` or `make()` method.

	Example:
	```php
	$ub->edit([
	    'pve_wins' => 1000,
	    'favoritPVE' => Classes::ENGINEER
	]);
	```

* ### add()
	```php
	add(array $data, array $dir = []): void
	```
	The method is used to add game achievements on userbar.

	<details>
		<summary>Additional information</summary>
		<p>	</p>
		<p>As the first parameter you need to pass an associative array with the required keys: <code>mark</code>, <code>base</code>, or <code>stripe</code>, whose values are numeric achievement IDs.</p>
		<p>As the second (optional) parameter, you can pass an associative array with the key <code>dir</code>, the value of which will specify the path to the local achievements directory.</p>
	</details>

	Example:
	```php
	$ub->add([
	    'mark' => 417,
	    'stripe' => 8018
	]);
	```
	Example with a local directory:
	```php
	$ub->add(
	    ['mark' => 95, 'badge' => 425],
	    ['dir' => 'C:/Users/wnull/Desktop/dir_with_achievements/']
	);
	```

* ### create()
	```php
	create(string $type = Userbar::USER): \Imagick
	```
	**Required** method that generates the final image (the `Imagick` object).

	<details>
		<summary>Additional information</summary>
		<p>	</p>
		<p>The method accepts a parameter <i>of the type</i> of the userbar. The default value is <code>user</code>. Valid values: <code>user</code>, <code>join</code>, or <code>clean</code>.</p>
	</details>
	
	Example:
	```php
	$image = $ub->create();
	```

## Result

After execution, a similar result is obtained:

<p align="center">
	<img src="https://user-images.githubusercontent.com/33278849/108274140-8a4fb280-7185-11eb-9bd9-f3becce70b70.png" alt="Result generate image (userbar)">
</p>

## License

The library is distributed under the [MIT](https://github.com/wnull/wfub/blob/master/LICENSE) license.