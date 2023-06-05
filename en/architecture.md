# Model

**Create command:** `php artisan make:model User`

## Naming

Singular without “Model” suffix (`User`, `Product`, `Category`...)

## Best practices

- Follow the defined structure.
- Methods should be tiny and clean.
- Models should contains only Laravel native things (relations, scopes...) and database-associated code.
  - Huge business logic should be written into `Support` or `Action` classes.
- Use `$fillable` instead of `$guarded` because of greater security.

## Structure

- **Attributes** - `$fillable`, `$casts`…
- **Lifecycle methods** - `boot()`, `booted()`
- **Relationships** - belongs, has, morphs…
- **Accessors & mutators**
- **Everything else**

# Controller

**Create command:** `php artisan make:controller UserController`

## Naming

Singular with “Controller” suffix (`UserController`, `ProductController`, `CategoryController`...)

## Best practices

- Don’t put advanced code logic inside, only use them for data returning or resolving actions.
- When you need an extra method in the resource, you should put it inside the resource controller and register a separate route.

## Types

- **resource** - contains methods for each CRUD operation also with methods that present HTML templates such as `create` and `edit`
- **api** - contains also a method for each CRUD operation, but does not provide HTML templates methods
- **invokable** - controllers for single actions that do not match resources

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

# Action

Actions are classes responsible for only one single task. Code is cleaner and simpler.

**Create command:** `php artisan make:action VerifyUserRequest`

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

## Naming

Action purpose name with “Action” suffix (`VerifyUserAction`, `CreateProductAction`, `ReorderCategoryAction`...)

## Best practices

- Actions should contain only one public method with the name `run()`.
- Helper methods of the single action should be private or protected.
  - Multiple helper methods may be converted to Support classes.

# Support

Support classes are a way to group related functions and logic together in a single class. They allow for easy reuse of code and help to keep application code organized.

They are typically used to provide functionality that is not specific to a single model or controller, but rather is used across multiple parts of an application.

It is simpler alternative than using services.

**Create command:** `php artisan make:class Support/Cart`

```php
class Cart
{
  //
}
```

## Naming

Support purpose name without “Support” suffix (`Cart`, `OpeningHours`, `Table`...)

# Middleware

Middleware is a way to filter and modify incoming HTTP requests in your application, allowing you to perform various tasks such as authentication, authorization, and session management.

You should create middleware in cases when you need to do some specific logic for a specific group of routes.

**Create command:** `php artisan make:middleware HandleLocale`

```php
class HandleLocale
{
  /**
   * Handle an incoming request.
   */
  public function handle(Request $request, Closure $next): Response
  {
    return $next($request);
  }
}
```

## Usage example

```php
Route::prefix('/admin')->name('admin.')->middleware(HandleLocale::class)->group(function () {
  Route::resource('users', UserController::class)->name('users');
  Route::resource('orders', OrderController::class)->name('orders');
});
```
