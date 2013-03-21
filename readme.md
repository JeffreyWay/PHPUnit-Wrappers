# Assert and Should

> [Prefer a video introduction](https://dl.dropbox.com/u/774859/GitHub-Repos/PHPUnit-Wrappers.mp4)?

This project provides two wrappers (you can add more) around PHPUnit's assertion library. For example, rather than typing:

```php
$this->assertEquals(4, 2 + 2);
```

You can instead do:

```php
Assert::equals(4, 2 + 2);

# or
Should::equal(4, 2 + 2);
```

To allow for more readability, when using Should, you may prepend `be` or `have`, like so:

```php
Should::beTrue(true);
Should::haveCount(2, ['a', 'b']);
```

## Aliases

Additionally, you can register your own aliases.

```php
Should::getInstance()->registerAliases([
	'beCakesAndPies' => 'assertTrue'
]);

# or

Assert::getInstance()->registerAliases([
	'eq' => 'assertEquals'
]);
```

Now, you can use `Should::beCakesAndPies` and `Assert::eq` in your tests, and they will map to `assertTrue` and `assertEquals`, respectively.

## Installation

Install these helpers through Composer. To your `composer.json` file, add:

```js
{
	"require-dev": {
		"way/phpunit-wrappers": "dev-master"
	}
}
```

Next, as always, run a `composer install` or `composer update` for development.

```bash
composer install --dev
```

That command will pull in those clases under the `Way\Tests` namespace.

Next, within your test file, use your desired assertion wrapper (or both).

```php
<?php

use Way\Tests\Should;

class DemoTest extends PHPUnit_Framework_TestCase {
	public function testItWorks()
	{
		Should::beTrue(true);
	}
}
```

If you wish, you can optionally alias Should to something shorter, such as `S`.

```php
use Way\Tests\Should as S;
```

This would allow for `S::beTrue()`. It's an option, but I prefer to stick with the more readable `Should`.


And that's it! Here's a few examples:

```php
<?php

use Way\Tests\Should;
use Way\Tests\Assert;

class DemoTest extends PHPUnit_Framework_TestCase {
	public function testItWorks()
	{
		Should::beTrue(true);
		Assert::true(true);

		Should::equal(4, 2 + 2);
		Assert::equals(4, 2 + 2);

		Should::beGreaterThan(20, 21);
		Assert::greaterThan(20, 21);

		Should::contain('Joe', ['John', 'Joe']);
		Should::have('Joe', ['John', 'Joe']);
		Assert::has('Joe', ['John', 'Joe']);
		Assert::has('Joe', 'Joey');

		Should::haveCount(2, ['1', '2']);
		Assert::count(2, ['1', '2']);
	}
}
```

> Don't forget to include Composer's autoloader into your project somewhere: `require_once 'vendor/autoload.php'`. Alternatively, you can specify a bootstrap option when running PHPUnit: `phpunit --bootstrap vendor/autoload.php --colors SomeTest.php`

Remember: these are simple wrappers around PHPUnit's assertions. Refer to the sidebar [here](http://www.phpunit.de/manual/current/en/index.html) for a full list.