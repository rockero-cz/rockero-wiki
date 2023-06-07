# Table of Contents

- [General](#general)
- [Naming Conventions](#naming-conventions)
  - [Class naming](#class-naming)
  - [Code naming](#code-naming)
  - [Database naming](#database-naming)
- [Structure](#structure)
  - [Class structure](#class-structure)
- [Commenting](#commenting)
  - [Attributes](#attributes)
  - [Methods](#methods)
  - [Code](#code)

---

# General

When writing code, it is important to keep in mind some general principles and standards that can help improve its quality and readability.

# Naming Conventions

## Class naming

| Class        | Naming                                                     | Example                                                                              |
| ------------ | ---------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Action       | action name with “Action” suffix                           | `CreateUserAction`, `DeleteProductAction`, `UpdateCategoryAction`                    |
| Command      | command name without suffix                                | `GenerateReport`, `ImportData`, `ExportData`                                         |
| Controller   | singular with “Controller” suffix                          | `UserController`, `ProductController`, `CategoryController`                          |
| Data         | singular with “Data” suffix                                | `UserData`, `ProductData`, `CategoryData`                                            |
| Event        | event name without suffix                                  | `UserCreated`, `OrderCreated`, `OrderShipped`                                        |
| Exception    | singular with “Exception” suffix                           | `ValidationException`, `NotFoundException`, `DuplicateEntryException`                |
| Interface    | adjective/noun without suffix                              | `Loggable`, `Configurable`, `Exportable`                                             |
| Job          | job name without suffix                                    | `SendEmail`, `ProcessPayment`, `GenerateReport`                                      |
| Mail         | mail name without suffix                                   | `WelcomeEmail`, `OrderConfirmationMail`, `NewsletterMail`                            |
| Middleware   | middleware name without suffix                             | `Authentication`, `RateLimit`, `Cors`                                                |
| Model        | singular without suffix                                    | `User`, `Product`, `Category`                                                        |
| Notification | notification name without suffix                           | `InvoicePaid`, `OrderShipped`, `PasswordReset`                                       |
| Observer     | singular model name with “Observer” suffix                 | `UserObserver`, `ProductObserver`, `CategoryObserver`                                |
| Policy       | singular model name with “Policy” suffix                   | `UserPolicy`, `ProductPolicy`, `CategoryPolicy`                                      |
| Provider     | provider name with “Provider” suffix                       | `PaymentProvider`, `StorageProvider`, `EmailProvider`                                |
| Request      | method name with singular model name with “Request” suffix | `StoreUserRequest`, `UpdateProductRequest`, `DestroyCategoryRequest`                 |
| Rule         | rule name without suffix                                   | `ValidPhoneNumber`, `ValidBankAccount`, `Uppercase`                                  |
| Scope        | scope name with “Scope” suffix                             | `ActiveScope`, `NewScope`, `TrendingScope`                                           |
| Support      | support name without suffix                                | `OpeningHours`, `Cart`, `Table`                                                      |
| Trait        | adjective/prefix “with“ without suffix                     | `Sortable`, `Searchable`, `Filterable`, `WithForm`, `WithSorting`, `WithFileUploads` |

## Code naming

| Entity     | Naming                           | Example                                             |
| ---------- | -------------------------------- | --------------------------------------------------- |
| Method     | camelCase                        | `store`, `massDestroy`, `run`                       |
| Property   | snake_case                       | `is_active`, `created_at`                           |
| Route      | lowercase - plural               | `users`, `products`, `categories`                   |
| Route name | snake_case - with 'dot' notation | `users.show`, `products.index`, `categories.create` |

## Database naming

| Entity       | Naming                                              | Example                                |
| ------------ | --------------------------------------------------- | -------------------------------------- |
| Table        | snake_case - plural                                 | `users`, `products`, `categories`      |
| Pivot table  | snake_case - singular model names alphabetically    | `category_product`, `order_user`       |
| Table column | snake_case - without table prefix                   | `title`, `price`, `description`        |
| Primary key  | id                                                  | `id`                                   |
| Foreign key  | snake_case - singular model name with “\_id” suffix | `user_id`, `product_id`, `category_id` |

# Structure

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
