# Model

**Create command:** `php artisan make:model User`

## Naming

Singular without “Model” suffix (`User`, `Product`, `Category`...)

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

**Create command:** `php artisan make:controller UserController`

## Naming

Singular with “Controller” suffix (`UserController`, `ProductController`, `CategoryController`...)

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

# Request

Requests are objects that encapsulate the input data from an HTTP request.

They provide a convenient way to validate and process user input before using it in your application.

**Create command:** `php artisan make:request StoreUserRequest`

```php
class StoreUserRequest extends FormRequest
{
    /**
     * Determine if the user is authorized to make this request.
     */
    public function authorize()
    {
        return true;
    }

    /**
     * Get the validation rules that apply to the request.
     */
    public function rules()
    {
        return ['name' => 'required'];
    }
}
```

## Naming

Method name with singular model name and with “Request” suffix (`StoreUserRequest`, `StoreProductRequest`, `UpdateCategoryRequest`...)
