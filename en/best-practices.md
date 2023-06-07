# Best practices

## Accept the standards and principles and follow them.

Code is then easier to maintain and it also improves readiablity and consitency.

If you don't how to write specific code, try to make some research - dig deeper inside the Laravel codebase, list GitHub repositories with many stars, or browse the source code of well-known packages...

```
“Consistency is key“ - Spatie
```

---

## Duplicated code is preferred over the **wrong** abstraction.

If you stumble, fixing a bad abstraction can cost you a lot of time.

Better wait a while and make refactor when you are confident with the abstraction.

---

## Keep test coverage as high as possible.

The ideal coverage is higher than 70%. We specifically strive that our applications have at least 80%.

```php
php artisan test --coverage --min=80
```

---

## Use static analysis to keep code high quality.

We use [PHPStan](https://phpstan.org) and it catches all missing type hints and return types.

```php
./vendor/bin/phpstan
```

---

## Use Artisan CLI for creating classes.

Artisan generates classes from stubs and it causes that you will follow some defined structure.

```php
php artisan make:migration CreateProductsTable
php artisan make:controller ProductController
```

---

## Simplify your business logic with action classes.

They are responsible for only one single task and the code is then cleaner and more understandable for others.

```php
class VerifyUserAction
{
    /**
     * Run the action.
     */
    public function run(): void
    {
        //
    }
}
```

---

## Group classes into subfolders by resources.

The folder structure is more clean and more simplified to maintain.

```php
- Actions/User/VerifyUserAction.php
- Actions/User/BanUserAction.php

- Actions/Order/CreateOrderAction.php
- Actions/Order/ConfirmOrderAction.php
- Actions/Order/CancelOrderAction.php
```

---

## Keep controller methods thin.

Controllers are responsible for one main thing - returning a response. There should not be some significant logic.

```php
/**
 * Store a newly created resource in storage.
 */
public function store(StoreUserRequest $request): JsonResponse
{
    $user = User::query()->create($request->validated());

    return response()->json($user);
}
```

---

## Models should contain only database-related things.

Don't put there your huge business logic, it should be written in `Support` classes instead.

---

## Never update the database directly, always use migrations.

Migrations allow you to share database schema between team members and between environments.

They are also your database version control. There isn't a single reason why someone shouldn't use them.
