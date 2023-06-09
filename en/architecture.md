# Table of Contents

- [Model](#model)
  - [Naming](#naming)
  - [Best practices](#best-practices)
  - [Structure](#structure)
- [Controller](#controller)
  - [Naming](#naming-1)
  - [Types](#types)
  - [Best practices](#best-practices-1)
  - [Namespacing](#namespacing)
- [Request](#request)
  - [Naming](#naming-2)
- [Configuration](#configuration)
  - [Best practices](#best-practices-2)
- [Action](#action)
  - [Naming](#naming-3)
  - [Best practices](#best-practices-3)
- [Support](#support)
  - [Naming](#naming-4)
- [Routing](#routing)
  - [Route Types](#route-types)
  - [Best practices](#best-practices-4)
- [Middleware](#middleware)
  - [Usage example](#usage-example)
- [Observer](#observer)
  - [Naming](#naming-5)
  - [Usage example](#usage-example-1)
- [Event](#event)
  - [Dispatching events](#dispatching-events)
  - [Listeners](#listeners)
- [Command](#command)
  - [Scheduling commands](#scheduling-commands)

---

# Model

Models are classes that represent database tables. They allow you to interact with the corresponding data using object-oriented syntax.

In other words, models provide an easy way to query, insert, update, and delete data in a database table. [Read more](https://laravel.com/docs/eloquent)

**Create command:** `php artisan make:model Product`

```php
class Product extends Model
{
    use HasFactory;
}
```

## Naming

Singular without "Model" suffix (`User`, `Product`, `Category`...)

## Best practices

- Follow the defined structure.
- Models should contains only Laravel native things (relations, scopes...) and database-related code.
  - Huge business logic should be written into `Support` or `Action` classes.
- Use [mass assignment](https://laravel.com/docs/eloquent#mass-assignment) where possible.
- Prefer `$fillable` over `$guarded` because of higher security.

## Structure

- **Attributes** - `$fillable`, `$casts`…
- **Lifecycle methods** - `boot()`, `booted()`
- **Relationships** - belongs, has, morphs…
- **Accessors & mutators**
- **Other methods**

# Controller

Controllers handle requests and responses. In fact, they are intermediaries between the database, views, and business logic. [Read more](https://laravel.com/docs/controllers)

**Create command:** `php artisan make:controller UserController`

```php
class UserController extends Controller
{
  //
}
```

## Naming

Singular with "Controller" suffix (`UserController`, `ProductController`, `CategoryController`...)

## Types

- **resource** - contains methods for each `CRUD` operation also with methods that present HTML templates such as `create` and `edit`
- **api** - contains also a method for each `CRUD` operation, but does not provide HTML templates methods
- **invokable** - controllers for single actions that do not match resources

## Best practices

- Keep controller methods thin.
  - They should not contain huge business logic.
  - They are mainly responsible for one thing - returning a response.
- For `CRUD` operations you should use [resource controllers](https://laravel.com/docs/controllers#resource-controllers)

## Namespacing

When you have multiple types of controllers (for `API`, for Admin...), you should group them by the following structure:

```php
Admin/UserController.php
Api/Admin/UserController.php
Api/UserController.php
UserController.php
```

# Request

Requests are objects that encapsulate the input data from an HTTP request.

They provide a convenient way to validate and process user input before using it in your application. [Read more](https://laravel.com/docs/validation#form-request-validation)

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
        return [
          //
        ];
    }
}
```

## Naming

Method name with singular model name and with "Request" suffix (`StoreUserRequest`, `StoreProductRequest`, `UpdateCategoryRequest`...)

# Configuration

Configurations are always stored in the `config` directory.

> **Warning:** You should never access the `env()` method directly in application. You should use it only in configuration files and access it by `config()` method.

## Best practices

- Custom application settings should be stored in `project.php`.
- API keys of 3rd party services should be stored in `services.php`.

# Action

Actions are classes responsible for only one single task. Code is cleaner and simpler.

**Create command:** `php artisan make:action VerifyUserAction`

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

> **Tip:** This command is not part of Laravel framework, install our package `rockero-cz/laravel-starter-kit` to get a bit of magics.

## Naming

Action purpose name with "Action" suffix (`VerifyUserAction`, `CreateProductAction`, `ReorderCategoryAction`...)

## Best practices

- Actions should contain only one public method with the name `run()`.
- Helper methods of the single action should be private or protected.
  - Multiple helper methods may be converted to `Support` classes.

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

> **Tip:** This command is not part of Laravel framework, install our package `rockero-cz/laravel-starter-kit` to get a bit of magics.

## Naming

Support purpose name without "Support" suffix (`Cart`, `OpeningHours`, `Table`...)

# Routing

## Route Types

- **web** - Routes that handle web-based HTTP requests and responses…
- **api** - Routes that handle API requests and responses…
- **channels** - Routes that handle real-time broadcasting to channels using websockets…
- **console** - Routes for custom commands that can be executed via Artisan CLI…

## Best practices

- URLs should be in plural.
- Each route should have name.
- Routes should be groupped by entities.

```php
Route::middleware('auth')->group(function () {
  Route::name('users.')->group(function () {
    Route::get('/', UserIndex::class)->name('index');
    Route::get('/{user}', UserShow::class)->name('show');
  });
});
```

# Middleware

Middleware is a way to filter and modify incoming HTTP requests in your application, allowing you to perform various tasks such as authentication, authorization, and session management.

You should create middleware in cases when you need to do some specific logic for a specific group of routes. [Read more](https://laravel.com/docs/middleware)

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

# Observer

Observers are used to listen for specific events that occurred by models, such as `created`, `updated`, or `deleted` and more...

By using observers, you can keep your model classes focused on their primary responsibilities and avoid cluttering them with additional logic. [Read more](https://laravel.com/docs/eloquent#observers)

> **Warning:** Eloquent mass update queries do not perform the event and the observer is not triggered. It is caused because models are not actually loaded when doing a mass update but only SQL query is.

**Create command:** `php artisan make:observer UserObserver --model=User`

```php
class UserObserver
{
  /**
   * Handle the User "created" event.
   */
  public function created(User $user): void
  {
    //
  }
}
```

## Naming

Singular model name with "Observer" suffix (`UserObserver`, `ProductObserver`, `CategoryObserver`...)

## Usage example

```php
// Recalculate invoice when the invoice item is saved.
public function saved(InvoiceItem $invoiceItem): void
{
  $invoiceItem->invoice()->recalculate();
}

// Set default state when the order is created.
public function creating(Order $order): void
{
  $order->state = OrderState::NEW;
}

// Delete relations before the model is deleted.
public function deleting(Order $order): void
{
  $order->products()->delete();
}
```

# Event

Events are a way to trigger and handle actions that occur during the execution of your application. They are used in combination with listeners.

When an event is dispatched, Laravel will notify all registered listeners for that event, giving them a chance to perform any necessary actions. [Read more](https://laravel.com/docs/events)

> We primarily use actions instead of events because they are more simple and understandable. However, we use still events for some notifications or in combination with [websockets](https://laravel.com/docs/broadcasting).

**Create command:** `php artisan make:event OrderCreated`

```php
class OrderCreated
{
    use Dispatchable, InteractsWithSockets, SerializesModels;

    /**
     * Create a new event instance.
     */
    public function __construct()
    {
        //
    }

    /**
     * Get the channels the event should broadcast on.
     */
    public function broadcastOn(): Channel|array
    {
        return new PrivateChannel('channel-name');
    }
}
```

## Dispatching events

```php
OrderCreated::dispatch();

// or

event(new OrderCreated());
```

## Listeners

**Create command:** `php artisan make:listener SendOrderCreatedNotification --event=OrderCreated`

```php
class SendOrderCreatedNotification
{
    /**
     * Create the event listener.
     */
    public function __construct()
    {
        //
    }

    /**
     * Handle the event.
     */
    public function handle(OrderCreated $event): void
    {
        //
    }
}
```

# Command

Commands are a powerful tool for automating some tasks in your application. Laravel also provides a set of built-in commands that you can use out of the box.

With commands, you can easily perform repetitive actions like running tests or executing database migrations, with minimal effort. [Read more](https://laravel.com/docs/artisan#writing-commands)

**Create command:** `php artisan make:command FetchUsers`

```php
class FetchUsers extends Command
{
    protected $signature = 'command:name';
    protected $description = 'Command description';

    /**
     * Execute the console command.
     */
    public function handle(): int
    {
        return Command::SUCCESS;
    }
}
```

## Scheduling commands

You can easily run commands at specified intervals or times using [Scheduler](https://laravel.com/docs/scheduling).

```php
// app/Console/Kernel.php
protected function schedule(Schedule $schedule)
{
    $schedule->command('telescope:prune')->daily();
}
```
