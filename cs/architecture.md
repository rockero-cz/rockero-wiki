# Obsah

- [Model](#model)
  - [Naming](#naming)
  - [Best practices](#best-praktiky)
  - [Struktura](#struktura)
- [Controller](#controller)
  - [Naming](#naming-1)
  - [Typy](#typy)
  - [Best practices](#best-praktiky-1)
  - [Namespacing](#namespacing)
- [Request](#request)
  - [Naming](#naming-2)
- [Konfigurace](#konfigurace)
  - [Best practices](#best-praktiky-2)
- [Action](#action)
  - [Naming](#naming-3)
  - [Best practices](#best-praktiky-3)
- [Support](#support)
  - [Naming](#naming-4)
- [Routing](#routing)
  - [Typy tras](#typy-tras)
  - [Best practices](#best-praktiky-4)
- [Middleware](#middleware)
  - [Ukázky použití](#ukázky-použití)
- [Observer](#observer)
  - [Naming](#naming-5)
  - [Ukázky použití](#ukázky-použití-1)
- [Event](#event)
  - [Vyvolání eventů](#vyvolání-eventů)
  - [Listeners](#listeners)
- [Command](#command)
  - [Plánování příkazů](#plánování-příkazů)

---

# Model

Modely jsou třídy, které reprezentují tabulky v databázi. Umožňují Vám interakci s odpovídajícími daty pomocí objektově orientované syntaxe.

Jinými slovy, modely poskytují snadný způsob pro dotazování, vkládání, aktualizaci a mazání dat v databázové tabulce. [Více informací](https://laravel.com/docs/eloquent)

**Příkaz pro vytvoření:** `php artisan make:model Product`

```php
class Product extends Model
{
    use HasFactory;
}
```

## Naming

Jednotné číslo bez přípony "Model" (`User`, `Product`, `Category`...)

## Best practices

- Dodržujte definovanou strukturu.
- Modely by měly obsahovat pouze nativní věci z Laravelu (vztahy, scopes...) a kód související s databází.
- Rozsáhlá business logika by měla být rozepsaná do tříd `Support` nebo `Action`.
- Používejte [mass assignment](https://laravel.com/docs/eloquent#mass-assignment) všude, kde je to možné.
- Preferujte `$fillable` před `$guarded`, kvůli vyšší bezpečnosti.

## Struktura

- **Atributy** - `$fillable`, `$casts`…
- **Lifecycle metody** - `boot()`, `booted()`
- **Vztahy** - belongs, has, morphs…
- **Accessory & mutatory**
- **Ostatní metody**

# Controller

Controllery zpracovávají požadavky a odpovědi. Ve skutečnosti jsou prostředníky mezi databází, zobrazením a obchodní logikou. [Více informací](https://laravel.com/docs/controllers)

**Příkaz pro vytvoření:** `php artisan make:controller UserController`

```php
class UserController extends Controller
{
  //
}
```

## Naming

Jednotné číslo s příponou "Controller" (`UserController`, `ProductController`, `CategoryController`...)

## Typy

- **resource** - obsahuje metody pro každou `CRUD` operaci a také metody, které představují HTML šablony, jako jsou `create` a `edit`
- **api** - obsahuje také metodu pro každou `CRUD` operaci, ale neobsahuje metody pro HTML šablony
- **invokable** - controllery pro jednotlivé akce, které neodpovídají zdrojům

## Best practices

- Udržujte metody controllerů krátké.
- Neměly by obsahovat rozsáhlou business logiku.
- Jsou hlavně zodpovědné za jednu věc - vrácení odpovědi.
- Pro `CRUD` operace byste měli používat [resource controllery](https://laravel.com/docs/controllers#resource-controllers)

## Namespacing

Pokud máte více typů controllerů (pro `API`, pro Admin...), měli byste je seskupit podle následující struktury:

```php
Admin/UserController.php
Api/Admin/UserController.php
Api/UserController.php
UserController.php
```

# Request

Requesty jsou objekty, které zahrnují vstupní data z HTTP požadavku.

Poskytují pohodlný způsob, jak validovat a zpracovávat uživatelský vstup před jeho použitím v aplikaci. [Více informací](https://laravel.com/docs/validation#form-request-validation)

**Příkaz pro vytvoření:** `php artisan make:request StoreUserRequest`

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

Název metody s názvem modelu v jednotném čísle a příponou "Request" (`StoreUserRequest`, `StoreProductRequest`, `UpdateCategoryRequest`...)

# Konfigurace

Konfigurace jsou vždy uloženy v adresáři `config`.

> **Pro tip:** Metodu `env()` byste nikdy neměli volat přímo v aplikaci. Měli byste ji používat pouze v konfiguračních souborech a přistupovat k ní pomocí metody `config()`.

## Best practices

- Vlastní nastavení aplikace by mělo být uloženo v `project.php`.
- API klíče třetích stran by měly být uloženy v `services.php`.

# Action

Akce jsou třídy zodpovědné za pouze jednu úlohu. Kód je tak čistší a jednodušší.

**Příkaz pro vytvoření:** `php artisan make:action VerifyUserAction`

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

> **Tip:** Tento příkaz není součástí frameworku Laravel, nainstalujte si balíček `rockero-cz/laravel-starter-kit`.

## Naming

Název akce s příponou "Action" (`VerifyUserAction`, `CreateProductAction`, `ReorderCategoryAction`...)

## Best practices

- Akce by měly obsahovat pouze jednu public metodu s názvem `run()`.
- Pomocné metody jedné akce by měly být private nebo protected.
  - Více pomocných metod může zapsáno do třídy `Support`.

# Support

Třídy `Support` jsou způsob, jak seskupit související funkce a logiku do jedné třídy. Umožňují snadné znovupoužití kódu a pomáhají udržovat kód aplikace organizovaný.

Obvykle se používají k poskytování funkcionality, která se neváže na jediný model nebo controller, ale spíše se používá v několika částech aplikace.

Je to jednodušší alternativa než použití services.

**Příkaz pro vytvoření:** `php artisan make:class Support/Cart`

```php
class Cart
{
  //
}
```

> **Tip:** Tento příkaz není součástí frameworku Laravel, nainstalujte si balíček `rockero-cz/laravel-starter-kit`.

## Naming

Název supportu bez přípony "Support" (`Cart`, `OpeningHours`, `Table`...)

# Routing

## Typy routů

- **web** - Routy, které zpracovávají webové HTTP požadavky a odpovědi…
- **api** - Routy, které zpracovávají API požadavky a odpovědi…
- **channels** - Routy, které zpracovávají vysílání v reálném čase do kanálů pomocí websockets…
- **console** - Routy pro vlastní příkazy, které lze spustit pomocí Artisan CLI...

## Best practices

- URL by měly být v množném čísle.
- Každý route by měl mít jméno.
- Routy by měly být seskupeny podle entit.

```php
Route::middleware('auth')->group(function () {
  Route::name('users.')->group(function () {
    Route::get('/', UserIndex::class)->name('index');
    Route::get('/{user}', UserShow::class)->name('show');
  });
});
```

# Middleware

Middleware je způsob filtrování a úpravy příchozích HTTP požadavků v aplikaci, což umožňuje provádět různé úkoly, jako je ověřování, autorizace a správa sessionů.

Middleware byste měli vytvářet v případech, kdy potřebujete provést určitou logiku pro konkrétní skupinu routů. [Více informací](https://laravel.com/docs/middleware)

**Příkaz pro vytvoření:** `php artisan make:middleware HandleLocale`

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

## Ukázky použití

```php
Route::prefix('/admin')->name('admin.')->middleware(HandleLocale::class)->group(function () {
  Route::resource('users', UserController::class)->name('users');
  Route::resource('orders', OrderController::class)->name('orders');
});
```

# Observer

Observery se používají k naslouchání určitým událostem, které nastaly modely, jako například `created`, `updated` nebo `deleted` a další...

Použitím observerů můžete udržet vaše modely zaměřené na jejich hlavní odpovědnosti a zabránit zanesení další logiky. [Více informací](https://laravel.com/docs/eloquent#observers)

> **Varování:** Dotazy hromadného updatu v Eloquentu nevyvolávají event a observer tím pádem není spuštěn. Je to kvůli tomu, že modely nejsou při hromadném updatu skutečně načteny, jelikož je v pozadí proveden pouze SQL dotaz.

**Příkaz pro vytvoření:** `php artisan make:observer UserObserver --model=User`

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

Jméno modelu v jednotném čísle s příponou "Observer" (`UserObserver`, `ProductObserver`, `CategoryObserver`...)

## Ukázky použití

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

Eventy jsou cesta, jak spouštět a zpracovávat akce, které se vyskytují během provozu vaší aplikace. Používají se v kombinaci s listenery.

Když je event vyvolán, Laravel upozorní všechny zaregistrované listenery k eventu, aby měly možnost provést veškeré akce. [Více informací](https://laravel.com/docs/events)

> Většinou používáme akce místo eventů, protože jsou jednodušší a srozumitelnější. Nicméně stále používáme eventy pro některé notifikace nebo v kombinaci s akcemi či [websockety](https://laravel.com/docs/broadcasting).

**Příkaz pro vytvoření:** `php artisan make:event OrderCreated`

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

## Vyvolání eventů

```php
OrderCreated::dispatch();

// or

event(new OrderCreated());
```

## Listeners

**Příkaz pro vytvoření:** `php artisan make:listener SendOrderCreatedNotification --event=OrderCreated`

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

Příkazy jsou mocným nástrojem pro automatizaci některých úloh v aplikaci. Laravel také poskytuje sadu vestavěných příkazů, které můžete použít ihned po instalaci.

Pomocí příkazů můžete snadno provádět opakující se akce, jako je spouštění testů nebo provádění databázových migrací a to s minimálním úsilím. [Více informací](https://laravel.com/docs/artisan#writing-commands)

**Příkaz pro vytvoření:** `php artisan make:command FetchUsers`

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

## Plánování příkazů

Můžete snadno spouštět příkazy v určitých intervalech nebo časech pomocí [Scheduleru](https://laravel.com/docs/scheduling).

```php
// app/Console/Kernel.php
protected function schedule(Schedule $schedule)
{
    $schedule->command('telescope:prune')->daily();
}
```
