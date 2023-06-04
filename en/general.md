# General

- When writing code, it is important to keep in mind some general principles and standards that can help improve its quality and readability.

# Commenting

## Attributes

- Native attributes from Laravel (e.g. $fillable) should have been without comment.
- Also without a type hint because you will never access the property

```php
protected $signature = 'command:name';
```

- Custom attributes should have a native type hint and should be written with comments when the name is not self-explanatory enough.

```php
/**
 * Count represents the number of clicks.
 */
public int $count = 0;

public int $clickCount = 0;
```

## Methods

- Comment all methods

```php
/**
 * Display a listing of the resource.
 */
public function index()
{
  //
}
```

## Code

- Comment all unclear logic - e.g. many statements
