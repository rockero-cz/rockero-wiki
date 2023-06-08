# Obsah

- [Naming sloupců](#naming-sloupců)
  - [Názvy pro často používané sloupce](#názvy-pro-často-používané-sloupce)
  - [Názvy podle datového typu sloupce](#názvy-podle-datového-typu-sloupce)
- [Řazení sloupců](#řazení-sloupců)
- [UUIDs](#uuids)
- [Indexy](#indexy)
- [Migrace](#migrace)
  - [Best practices](#best-practices)
- [Seedery](#seedery)
  - [Naming](#naming)
- [Factories](#factories)
  - [Naming](#naming-1)
  - [Ukázky použití](#ukázky-použití)
  - [Factory metody](#factory-metody)
  - [Vlastní metody](#vlastní-metody)
  - [Factory Callbacks](#factory-callbacks)

---

## Naming sloupců

- Primární klíč by měl vždy být `id`
- Cizí klíče by měly být zapsány v jednotném čísle a s příponou `_id` (`user_id`, `product_id`, `category_id`...)
- Když volíte jméno, buďte opatrní s [rezervovanými slovy](https://dev.mysql.com/doc/refman/8.0/en/keywords.html)

### Názvy pro často používané sloupce:

- **order_column** - název pro řazení entit (např. drag & drop)
- **company_number** - název pro IČO / Identifikační Číslo Organizace
- **vat_number** - název pro DIČ / Daňové Identifikační Číslo

### Názvy podle datového typu sloupce:

- **boolean** - `is_enabled`, `has_reviews`
- **timestamp** - `published_at`, `valid_from`, `scheduled_for`

> **Pro tip:** SoNěkteré boolean sloupce by mohly být převedeny na timestamp (např. z `is_finished` na `finished_at`). Výhodou je, že máte ve skutečnosti dvě informace v jednom sloupci.

## Řazení sloupců

- **id** - vždy by mělo být první
- **cizí klíče**
- **ostatní slopce** - měly by být seřazené podle priorit a seskupiné podle kontextu
- **nativní timestampy** - `created_at`, `updated_at`

## UUIDs

Bezpečná alternativa k ID. Měla by být používána pro veřejně přístupné webové stránky nebo pro některé tabulky s citlivým obsahem (bankovní účty, objednávky, faktury...). [Jak používat UUIDs?](https://laravel.com/docs/eloquent#uuid-and-ulid-keys)

## Indexy

Indexy jsou struktury databáze, které umožňují rychlejší získávání dat. Fungují tak, že vytvářejí samostatnou datovou strukturu, která ukazuje na umístění dat v databázi. Při spuštění dotazu může databáze použít index k rychlému nalezení relevantních dat místo prohledávání celé databáze.

> **Pro tip:** Použijte indexy na sloupce, které jsou často dotazovány nebo používány v joinech a výkon vaší databáze se zlepší.

# Migrace

Migrace jsou způsob verzování schématu vaší databáze. Umožňují vám provádět změny v schématu Vaší databáze přehledným způsobem a umožňují Vám také snadný způsob jak vrátit změny zpět, když je to nutné. [Více informací](https://laravel.com/docs/migrations)

## Best practices

- Během vývoje je v pořádku upravovat existující migrace a spouštět příkaz `php artisan migrate:fresh` pro resetování databáze.
- Jakmile je projekt v produkčním prostředí, musíte vytvořit novou migraci pro každou změnu, i malou.
- Nerozbijte řazení sloupců - při přidávání nového sloupce použijte metody k řazení `after()` nebo `before()`.
- Přidejte krátkou poznámku pomocí metody `comment()`, pokud název sloupce není výstižný (např. odborné výrazy).

> **Pro tip:** Při vývoji se postupem času může hromadit stále více a více migrací. To může vést k nadměrnému počtu souborů v adresáři `database/migrations`, kde mohou být stovky migrací. Pokud chcete, můžete své migrace "squashnout" do jednoho SQL souboru. [Více informací](https://laravel.com/docs/migrations#squashing-migrations)

# Seedery

Seedery slouží k naplnění databáze počátečními/testovacími daty. Jsou zvláště užitečné v situacích, kdy potřebujete naplnit databázi předem existujícími daty, jako jsou testovací nebo referenční data.

Použitím seedru můžete rychle naplnit databázi potřebnými daty, aniž byste je museli pokaždé zadávat ručně. [Více informací](https://laravel.com/docs/seeding)

- **Příkaz pro vytvoření:** `php artisan make:seeder UserFactory`
- **Spuštění všech seederů:** `php artisan db:seed`
- **Spuštění konkrétního seederu:** `php artisan db:seed --class=UserSeeder`

> **Pro tip:** Někdy je třeba v seederech vypnout eventy modelu. To lze jednoduše provést pomocí traitu `WithoutModelEvents`. [Více informací](https://laravel.com/docs/seeding#muting-model-events)

## Naming

Jednotné číslo s příponou "Seeder" (`UserSeeder`, `ProductSeeder`, `CategorySeeder`...)

# Factories

Factories v Laravelu jsou pohodlný způsob jak generovat falešná data pro účely testování. Umožňují vám rychle a snadno vytvářet instance vašich modelů s náhodnými nebo vlastními atributy.

Definováním factory pro každý z vašich modelů můžete snadno generovat data, která potřebujete pro testování funkcionality vaší aplikace.

Jsou převážně používány v seederech a testech. [Více informací](https://laravel.com/docs/eloquent-factories)

**Příkaz pro vytvoření:** `php artisan make:factory UserFactory`

```php
class ProductFactory extends Factory
{
    public function definition(): array
    {
        return [
            'name' => fake()->name(),
            'category_id' => Category::factory(),
            ...
        ];
    }
}
```

## Naming

Název modelu s příponou "Factory" (`UserFactory`, `ProductFactory`, `CategoryFactory`...)

## Ukázky použití

Vytvoření jednoho záznamu v databázi:

```php
User::factory()->create();
```

Vytvoření jedné instance modelu:

```php
User::factory()->make();
```

Vytvoření více záznamů v databázi:

```php
User::factory()
    ->count(10)
    ->create();
```

Vytvoření více instancí modelu:

```php
User::factory()
    ->count(10)
    ->make();
```

Vytvoření factory s vlastní hodnotou:

```php
User::factory()->create(['email' => 'info@rockero.cz']);
```

## Factory metody

### Sequence

Můžete vytvářet modely s větší variabilitou dat. Sekvence je opakována, dokud není dosaženo požadovaného počtu modelů. [Více informací](https://laravel.com/docs/database-testing#sequences)

```php
// Creates 5 orders with state new and 5 orders with state pending:
Order::factory()
    ->count(10)
    ->sequence(
        ['state' => 'new'],
        ['state' => 'pending']
    )
    ->create();
```

Můžete používat sequence také s callbackem:

```php
Category::factory()
    ->count(10)
    ->sequence(fn (Sequence $sequence) => ['order_column' => $sequence->index])
    ->create();
```

### Recycle

Někdy se stane, že vnořené factories mají stejný vztah jako základní factory. V takovém případě můžete použít metodu `recycle()`. Tato metoda opětovně použije instanci vztahu. [Více informací](https://laravel.com/docs/eloquent-factories#recycling-an-existing-model-for-relationships)

```php
$tenant = Tenant::factory()->create();

// Bad example:
Product::factory()->create(['tenant_id' => $tenant]);
ProductCategory::factory()->create(['tenant_id' => $tenant]);

// Good example:
Product::factory()
	->recycle($tenant)
	->has(ProductCategory::factory())
	->create();
```

### Vztahy

```php
// Creates user with 3 posts:
User::factory()
    ->has(Post::factory()->count(3))
    ->create();

// Or using magic methods:
User::factory()
    ->hasPosts(3)
    ->create();

// Creates post that belongs to the user:
Post::factory()
    ->count(3)
    ->for(User::factory(['name' => 'Rockero']))
    ->create();

// Or using magic methods:
Post::factory()
    ->count(3)
    ->forUser(['name' => 'Rockero'])
    ->create();

// Creates user with 3 roles and custom pivot value:
User::factory()
    ->hasAttached(
        Role::factory()->count(3),
        ['active' => true]
    )
    ->create();

// Or using magic methods:
User::factory()
    ->hasRoles(1, ['name' => 'Editor'])
    ->create();
```

## Vlastní metody

Místo vytváření klienta s následujícími hodnotami v každém testu:

```php
Client::factory([
    'platform' => 'github',
    'email' => 'info@rockero.cz'
])->create();
```

lze vytvořit vlastní metoda v `ClientFactory`:

```php
public function github(array $attributes = []): self
{
    return $this->state([
        'platform' => 'github',
        'email' => $attributes['email'] ?? fake()->email()
        'access_token' => $attributes['token'] ?? Str::random()
    ]);
}
```

a pak ji můžete používat následovně:

```php
Client::factory()
    ->github()
    ->create();
```

## Factory Callbacks

Factory callbacks můžou být použité k provedení akce po vytvoření nebo uložení modelu.

Tyto metody jsou definovány uvnitř metody `configure()` v třídě factory.

```php
public function configure(): static
{
    return $this->afterMaking(function (User $user) {
        // ...
    })->afterCreating(function (User $user) {
        // ...
    });
}
```
