# Assert and Should

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

First, import the `helpers` directory from this repo into your project, where you store your tests. Next, within your test file, require your desired assertion wrapper (or both).

```php
<?php

require 'tests/helpers/Should.php';

use Tests\Should;

class DemoTest extends PHPUnit_Framework_TestCase {

}
```

If you wish, you can optionally alias Should to something shorter, such as `S`.

```php
use Tests\Should as S;
```

This would allow for `S::beTrue()`. It's an option, but I prefer to stick with the more readable `Should`.


And that's it! Here's a few examples:

```php
<?php

require 'tests/helpers/Should.php';
require 'tests/helpers/Assert.php';

use Tests\Should;
use Tests\Assert;

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

Remember: these are simple wrappers around PHPUnit's assertions. Refer to the sidebar [here](http://www.phpunit.de/manual/current/en/index.html) for a full list.



