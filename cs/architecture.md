# Architektura

- [Model](#model)
  - [Pojmenování](#naming)
  - [Best practices](#best-practices)
  - [Struktura](#structure)
- [Controller](#controller)
  - [Pojmenování](#naming-1)
  - [Typy](#types)
  - [Best practices](#best-practices-1)
  - [Namespacing](#namespacing)
- [Request](#request)
  - [Pojmenování](#naming-2)
- [Konfigurace](#configuration)
  - [Best practices](#best-practices-2)
- [Action](#action)
  - [Pojmenování](#naming-3)
  - [Best practices](#best-practices-3)
- [Support](#support)
  - [Pojmenování](#naming-4)
- [Routing](#routing)
  - [Typy tras](#route-types)
  - [Best practices](#best-practices-4)
- [Middleware](#middleware)
  - [Ukázky použití](#usage-example)
- [Observer](#observer)
  - [Pojmenování](#naming-5)
  - [Ukázky použití](#usage-example-1)
- [Event](#event)
  - [Vyvolání eventů](#dispatching-events)
  - [Listeners](#listeners)
- [Command](#command)
  - [Plánování příkazů](#scheduling-commands)

---

<a name="model"></a>

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

<a name="naming"></a>

## Pojmenování

Jednotné číslo bez přípony "Model" (`User`, `Product`, `Category`...)

<a name="best-practices"></a>

## Best practices

1. Dodržujte danou strukturu:

- Atributy - `$fillable`, `$casts`…
- Lifecycle metody - `boot()`, `booted()`
- Vztahy - belongs, has, morphs…
- Accessors & mutators
- Ostatní metody

2. Modely by měly obsahovat pouze prvky specifické pro Laravel (vztahy, scopes…) a kód související s databází.

- Vaše business logika by měla být zapsána do tříd `Support` nebo `Action`.

3. Použvíejte [mass assignment](https://laravel.com/docs/eloquent#mass-assignment) všude, kde je to možné.

- Kód pro vytváření/upravování modelu je kratší a také čistší.

4. Používejte raději `$fillable` místo `$guarded`.

- Obecně je to bezpečnější princip => snižuje riziko problémů s daty.
- Větší kontrola nad atributy.
- Snadná možnost najít názvy databázových sloupců pouhým otevřením modelu.

<a name="controller"></a>

# Controller

Controllery zpracovávají požadavky a odpovědi. Ve skutečnosti jsou prostředníky mezi databází, zobrazením a obchodní logikou. [Více informací](https://laravel.com/docs/controllers)

**Příkaz pro vytvoření:** `php artisan make:controller UserController`

```php
class UserController extends Controller
{
  //
}
```

<a name="naming-1"></a>

## Pojmenování

Jednotné číslo s příponou "Controller" (`UserController`, `ProductController`, `CategoryController`...)

<a name="types"></a>

## Typy

- **resource** - obsahuje metody pro každou `CRUD` operaci a také metody, které představují HTML šablony, jako jsou `create` a `edit`
- **api** - obsahuje také metodu pro každou `CRUD` operaci, ale neobsahuje metody pro HTML šablony
- **invokable** - controllery pro jednotlivé akce, které neodpovídají zdrojům

<a name="best-practices-1"></a>

## Best practices

1. Udržujte metody controllerů co nejkratší.

- Metody controllerů by neměly obsahovat rozsáhlou business logiku.
- Jsou primárně zodpovědné jen za jednu věc - vrácení odpovědi.

2. Používejte [resource controllery](https://laravel.com/docs/controllers#resource-controllers) pro `CRUD` operace.

- Resource controllery definují metody `CRUD` s dodržením jmenných konvencí.

<a name="namespacing"></a>

## Namespacing

Pokud máte více typů controllerů (pro `API`, pro Admin...), měli byste je seskupit podle následující struktury:

```php
Admin/UserController.php
Api/Admin/UserController.php
Api/UserController.php
UserController.php
```

<a name="request"></a>

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

<a name="naming-2"></a>

## Pojmenování

Název metody s názvem modelu v jednotném čísle a příponou "Request" (`StoreUserRequest`, `StoreProductRequest`, `UpdateCategoryRequest`...)

<a name="configuration"></a>

# Konfigurace

Konfigurace jsou vždy uloženy v adresáři `config`.

> **Varování:** Metodu `env()` byste nikdy neměli volat přímo v aplikaci. Měli byste ji používat pouze v konfiguračních souborech a přistupovat k ní pomocí metody `config()`.

<a name="best-practices-2"></a>

## Best practices

1. Přistupujte k hodnotám z konfigurace pouze pomocí metody `config()`.
2. Ukládejte vlastní nastavení aplikace do samostatného konfiguračního souboru.

- např. `project.php`

3. Klíče API třetích stran by měly být uloženy v souboru `services.php`.

<a name="action"></a>

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

<a name="naming-3"></a>

## Pojmenování

Název akce s příponou "Action" (`VerifyUserAction`, `CreateProductAction`, `ReorderCategoryAction`...)

<a name="best-practices-3"></a>

## Best practices

1. Každá akce by měla obsahovat pouze jednu public metodu.

- Použijte výstižný název funkce, jako například `run()` nebo `execute()`.

2. Jiné pomocné metody akce by měly být private nebo protected.

- Více pomocných metod může být převedeno do tříd `Support`.

<a name="support"></a>

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

<a name="naming-4"></a>

## Pojmenování

Název supportu bez přípony "Support" (`Cart`, `OpeningHours`, `Table`...)

<a name="routing"></a>

# Routing

<a name="route-types"></a>

## Typy routů

- **web** - Routy, které zpracovávají webové HTTP požadavky a odpovědi…
- **api** - Routy, které zpracovávají API požadavky a odpovědi…
- **channels** - Routy, které zpracovávají vysílání v reálném čase do kanálů pomocí websockets…
- **console** - Routy pro vlastní příkazy, které lze spustit pomocí Artisan CLI...

<a name="best-practices-4"></a>

## Best practices

1. URL by měly být v množném čísle.
2. Každá route by měla mít jméno.
3. Routy by měly být seskupeny podle entit.

```php
Route::middleware('auth')->group(function () {
  Route::name('users.')->group(function () {
    Route::get('/', UserIndex::class)->name('index');
    Route::get('/{user}', UserShow::class)->name('show');
  });
});
```

<a name="middleware"></a>

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

<a name="usage-example"></a>

## Ukázky použití

```php
Route::prefix('/admin')->name('admin.')->middleware(HandleLocale::class)->group(function () {
  Route::resource('users', UserController::class)->name('users');
  Route::resource('orders', OrderController::class)->name('orders');
});
```

<a name="observer"></a>

# Observer

Observery se používají k naslouchání určitým událostem, které nastaly u modelů, jako například `created`, `updated` nebo `deleted` a další...

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

<a name="naming-5"></a>

## Pojmenování

Jméno modelu v jednotném čísle s příponou "Observer" (`UserObserver`, `ProductObserver`, `CategoryObserver`...)

<a name="usage-example-1"></a>

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

<a name="event"></a>

# Event

Eventy jsou cesta, jak spouštět a zpracovávat akce, které se vyskytují během provozu vaší aplikace. Používají se v kombinaci s listenery.

Když je event vyvolán, Laravel upozorní všechny zaregistrované listenery k eventu, aby měly možnost provést veškeré akce. [Více informací](https://laravel.com/docs/events)

> Většinou používáme akce místo eventů, protože jsou jednodušší a srozumitelnější. Nicméně stále používáme eventy pro některé notifikace nebo v kombinaci s [websockety](https://laravel.com/docs/broadcasting).

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

<a name="dispatching-events"></a>

## Vyvolání eventů

```php
OrderCreated::dispatch();

// or

event(new OrderCreated());
```

<a name="listeners"></a>

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

<a name="command"></a>

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

<a name="scheduling-commands"></a>

## Plánování příkazů

Můžete snadno spouštět příkazy v určitých intervalech nebo časech pomocí [Scheduleru](https://laravel.com/docs/scheduling).

```php
// app/Console/Kernel.php
protected function schedule(Schedule $schedule)
{
    $schedule->command('telescope:prune')->daily();
}
```
