# Structure

## Project structure

- We follow the well-established Laravel folder structure.
- Custom classes are categorized under the Actions and Support folders.
- These folders always have to be located in the app folder.
- We group all custom classes into subfolders by resource.
- e.g. you have actions that interact with the Product model, you should group them into the Actions/Product folder. [Read more](https://github.com/monicahq/monica/tree/main/app/).

> This helps to organize the codebase in a simple way - it also keeps projects clean, well organized and they will be easier to maintain over time.

## Class structure

When organizing code in the class, it is best to follow this order:

- **Traits**
- **Constants**
- **Static properties**
- **Properties**
- **Static methods**
- **Methods**
- **Abstract methods**

It is also important to order each category by level in the following way:

- **public**
- **protected**
- **private**

```php
use Trait;

const FOO = 1;

public static int $a;

public int $b;
protected int $c;
private int $d;

public static function methodA() {}

public function methodB() {}
protected function methodC() {}
private function methodD() {}

abstract public function methodE() {}
```
