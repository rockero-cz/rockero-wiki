# Model

## Naming

- Singular without “Model” suffix

## Rules

- Follow the defined structure.
- Models should keep only
  - native things from Laravel - relationships, scopes, etc.
  - things associated with the database.
- Methods should be tiny and clean.
  - Huge business logic should be written into Support/Action classes.
- Use `$fillable` instead of `$guarded`
  - it is more secured

## Structure

- **Attributes** - `$fillable`, `$casts`…
- **Lifecycle methods**
  - `boot()`, `booted()`
- **Relationships**
  - belongs, has, morphs…
- **Accessors & mutators**
- **Everything else**

# Controller

## Naming

- Singular with “Controller” suffix

## Types

- **resource** - contains methods for each CRUD operation also with methods that present HTML templates such as `create` and `edit`
- **api** - contains also a method for each CRUD operation, but does not provide HTML templates methods
- **invokable** - controllers for single actions that do not match resources

## Best practices

- Don’t put advanced code logic inside, only use them for data returning or resolving actions
- When you need an extra method in the resource, you should put it inside the resource controller and register a separate route.

## Namespacing

- When you have multiple types of controllers (one for API, one for Admins), you should group them by the following structure:

```php
/Admin
  - Admin controllers
/API
	/Admin
		- Administration controllers for API
  - Controllers for API

- UserController.php
```
