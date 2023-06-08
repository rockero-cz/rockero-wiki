# Obsah

- [Obecné](#obecné)
- [Jmenné konvence](#jmenné-konvence)
  - [Naming tříd](#naming-tříd)
  - [Naming kódu](#naming-kódu)
  - [Naming databáze](#naming-databáze)
- [Struktura](#struktura)
  - [Struktura třídy](#struktura-třídy)
- [Komentování](#komentování)
  - [Atributy](#atributy)
  - [Metody](#metody)
  - [Kód](#kód)

---

# Obecné

Při psaní kódu je důležité mít na paměti některé obecné zásady a standardy, které mohou pomoci zlepšit jeho kvalitu a čitelnost.

# Jmenné konvence

## Naming tříd

| Třída        | Naming                                            | Příklad                                                                              |
| ------------ | ------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Action       | název akce s příponou "Action"                    | `CreateUserAction`, `DeleteProductAction`, `UpdateCategoryAction`                    |
| Command      | název příkazu bez přípony                         | `GenerateReport`, `ImportData`, `ExportData`                                         |
| Controller   | jednotné číslo s příponou "Controller"            | `UserController`, `ProductController`, `CategoryController`                          |
| Data         | jednotné číslo s příponou "Data"                  | `UserData`, `ProductData`, `CategoryData`                                            |
| Event        | název eventu bez přípony                          | `UserCreated`, `OrderCreated`, `OrderShipped`                                        |
| Exception    | jednotné číslo s příponou "Exception"             | `ValidationException`, `NotFoundException`, `DuplicateEntryException`                |
| Interface    | přídavné jméno/podstatné jméno bez přípony        | `Loggable`, `Configurable`, `Exportable`                                             |
| Job          | název jobu bez přípony                            | `SendEmail`, `ProcessPayment`, `GenerateReport`                                      |
| Mail         | název mailu bez přípony                           | `WelcomeEmail`, `OrderConfirmationMail`, `NewsletterMail`                            |
| Middleware   | název middlewaru bez přípony                      | `Authentication`, `RateLimit`, `Cors`                                                |
| Model        | jednotné číslo bez přípony                        | `User`, `Product`, `Category`                                                        |
| Notification | název notifikace bez přípony                      | `InvoicePaid`, `OrderShipped`, `PasswordReset`                                       |
| Observer     | název modelu s příponou "Observer"                | `UserObserver`, `ProductObserver`, `CategoryObserver`                                |
| Policy       | název modelu s příponou "Policy"                  | `UserPolicy`, `ProductPolicy`, `CategoryPolicy`                                      |
| Provider     | název provideru s příponou "Provider"             | `PaymentProvider`, `StorageProvider`, `EmailProvider`                                |
| Request      | název metody s názvem modelu s příponou "Request" | `StoreUserRequest`, `UpdateProductRequest`, `DestroyCategoryRequest`                 |
| Rule         | název pravidla bez přípony                        | `ValidPhoneNumber`, `ValidBankAccount`, `Uppercase`                                  |
| Scope        | název scopu s příponou "Scope"                    | `ActiveScope`, `NewScope`, `TrendingScope`                                           |
| Support      | název supportu bez přípony                        | `OpeningHours`, `Cart`, `Table`                                                      |
| Trait        | přídavné jméno/předpona "with" bez přípony        | `Sortable`, `Searchable`, `Filterable`, `WithForm`, `WithSorting`, `WithFileUploads` |

## Naming kódu

| Entita     | Naming                        | Příklad                                             |
| ---------- | ----------------------------- | --------------------------------------------------- |
| Method     | camelCase                     | `store`, `massDestroy`, `run`                       |
| Property   | snake_case                    | `is_active`, `created_at`                           |
| Route      | lowercase - množné číslo      | `users`, `products`, `categories`                   |
| Route name | snake_case - s 'dot' notation | `users.show`, `products.index`, `categories.create` |

## Naming databáze

| Entita       | Naming                                      | Příklad                                |
| ------------ | ------------------------------------------- | -------------------------------------- |
| Table        | snake_case - množné číslo                   | `users`, `products`, `categories`      |
| Pivot table  | snake_case - název modelů abecedně          | `category_product`, `order_user`       |
| Table column | snake_case - bez prefixu tabulky            | `title`, `price`, `description`        |
| Primary key  | id                                          | `id`                                   |
| Foreign key  | snake_case - název modelu s příponou "\_id" | `user_id`, `product_id`, `category_id` |

# Struktura

## Struktura třídy

Při organizaci kódu v třídě je nejlepší dodržovat následující pořadí:

- **Traits**
- **Constants**
- **Static properties**
- **Properties**
- **Static methods**
- **Methods**
- **Abstract methods**

Je také důležité každou část řadit následujícím způsobem:

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

# Komentování

## Atributy

- Nativní atributy Laravelu (např. `$fillable`) by měly být bez komentáře.
- Také bez type hintu, protože k proměnné nikdy nebudete přistupovat.

```php
protected $signature = 'command:name';
```

- Vlastní atributy by měly mít type hint a mely by být také popsané komentářem, pokud nemají dostatečně výstižný název.

```php
/**
 * Count represents the number of clicks.
 */
public int $count = 0;

// or

public int $clickCount = 0;
```

## Metody

- Komentujte všechny metody

```php
/**
 * Display a listing of the resource.
 */
public function index()
{
  //
}
```

## Kód

- Komentujte všechnu méně srozumitelnou logiku, např. hodně podmínek
