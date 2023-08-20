# Database

- [Column Naming](#column-naming)
  - [Names for frequently used columns](#names-for-frequently-used-columns)
  - [Names by column type](#names-by-column-type)
- [Column Sorting](#column-sorting)
- [UUIDs](#uuids)
- [Indexes](#indexes)
- [Migrations](#migrations)
  - [Best practices](#best-practices)
- [Seeders](#seeders)
  - [Naming](#naming)
- [Factories](#factories)
  - [Naming](#naming-1)
  - [Usage Examples](#usage-examples)
  - [Factory methods](#factory-methods)
  - [Custom Methods](#custom-methods)
  - [Factory Callbacks](#factory-callbacks)

---

<a name="column-naming"></a>

## Column Naming

- Primary key should be always `id`
- Foreign keys should be a singular with the suffix `_id` (`user_id`, `product_id`, `category_id`...)
- When choosing a name you should be careful with [reserved words](https://dev.mysql.com/doc/refman/8.0/en/keywords.html)

<a name="names-for-frequently-used-columns"></a>

### Recommended names for frequently used columns:

These names are recommendations on how to name certain columns to unify them across projects. These columns may be called differently, but it is good to keep them unified.

- **order_column** - field for sorting entities (e.g. drag & drop)
- **company_number** - field for CIN / Company Identification Number
- **vat_number** - field for VATIN / VAT ID / VAT Identification Number
- **zip_code** - field for ZIP Code / Postal Code / Post Code

<a name="names-by-column-type"></a>

### Names by column type:

Recommended prefixes/suffixes for naming columns.

- **boolean** - `is_enabled`, `has_reviews`
- **timestamp** - `published_at`, `valid_from`, `scheduled_for`

> **Pro tip:** Some of boolean columns could be converted to timestamps (e.g. from `is_finished` to `finished_at`). There is a benefit that you have in fact two pieces of information in one column.

<a name="column-sorting"></a>

## Column Sorting

This sorting helps for better reading and orientation in the database.

- **id** - should be always first
- **foreign keys**
- **rest of columns** - should be sorted by priorty and grouped by context
- **native timestamps** - `created_at`, `updated_at`

<a name="uuids"></a>

## UUIDs

Secure alternative to ids. They should be used for publicly accessible websites or for some tables with sensitive content (bank accounts, orders, invoices...). [How to use UUIDs?](https://laravel.com/docs/eloquent#uuid-and-ulid-keys)

<a name="indexes"></a>

## Indexes

Indexes are database structures that allow for faster retrieval of data. They work by creating a separate data structure that points to the location of the data in the database. When a query is run, the database can use the index to quickly find the relevant data instead of having to search the entire database.

> **Pro tip:** Just use indexes on any columns that are frequently queried or used in joins and your database performance will be improved.

<a name="migrations"></a>

# Migrations

Migrations are a way to version control your database schema. They allow you to make changes to the database schema in a structured way, and enable you to easily roll back changes if necessary. [Read more](https://laravel.com/docs/migrations)

<a name="best-practices"></a>

## Best practices

- During development, it's fine to modify existing migration files and run `php artisan migrate:fresh` to reset the database
- Once the project is in production, you have to create new migrations for every change, even small ones
- Don't break column sorting - when adding a new column use also `after()` and `before()` methods
- Add short note with `comment()` method if column names are not clear (e.g. professional terms)

> **Pro tip:** As you build your application, you may accumulate more and more migrations over time. This can lead to your `database/migrations` directory becoming bloated with potentially hundreds of migrations. If you would like, you may "squash" your migrations into a single SQL file. [Read more](https://laravel.com/docs/migrations#squashing-migrations)

<a name="seeders"></a>

# Seeders

Seeders are used to populate a database with initial/testing data. They are especially useful in scenarios where you need to populate your database with pre-existing data, such as test data or reference data.

By using a seeder, you can quickly populate your database with the necessary data without having to manually enter it every time. [Read more](https://laravel.com/docs/seeding)

- **Create command:** `php artisan make:seeder UserSeeder`
- **Running all seeders:** `php artisan db:seed`
- **Running specific seeder:** `php artisan db:seed --class=UserSeeder`

> **Pro tip:** Sometimes you need to disable model events inside seeders. You can simply make it with a trait `WithoutModelEvents`. [Read more](https://laravel.com/docs/seeding#muting-model-events)

<a name="naming"></a>

## Naming

Singular with "Seeder" suffix (`UserSeeder`, `ProductSeeder`, `CategorySeeder`...)

<a name="factories"></a>

# Factories

Laravel factories are a convenient way to generate fake data for testing purposes. They allow you to quickly and easily create instances of your models with randomized or custom attributes.

By defining a factory for each of your models, you can easily generate the data you need to test your application's functionality.

They are mostly used in seeders and tests. [Read more](https://laravel.com/docs/eloquent-factories)

**Create command:** `php artisan make:factory UserFactory`

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

<a name="naming-1"></a>

## Naming

Singular model name with "Factory" suffix (`UserFactory`, `ProductFactory`, `CategoryFactory`...)

<a name="usage-examples"></a>

## Usage Examples

Creating a single database record:

```php
User::factory()->create();
```

Creating a single model instance:

```php
User::factory()->make();
```

Creating multiple database records:

```php
User::factory()
    ->count(10)
    ->create();
```

Creating multiple model instances:

```php
User::factory()
    ->count(10)
    ->make();
```

Creating a factory with custom attributes:

```php
User::factory()->create(['email' => 'info@rockero.cz']);
```

<a name="factory-methods"></a>

## Factory methods

### Sequence

You can create models with more data variation. The sequence is looped until the desired number of models is reached. [Read more](https://laravel.com/docs/database-testing#sequences)

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

You can use sequence also with callback:

```php
Category::factory()
    ->count(10)
    ->sequence(fn (Sequence $sequence) => ['order_column' => $sequence->index])
    ->create();
```

### Recycle

Sometimes happens that nested factories have the same relationship as the base factory. For that, you may use the `recycle()` method. It will re-use the relationship instance. [Read more](https://laravel.com/docs/eloquent-factories#recycling-an-existing-model-for-relationships)

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

### Relationships

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

<a name="custom-methods"></a>

## Custom Methods

Instead of creating client with following setup in each test:

```php
Client::factory([
    'platform' => 'github',
    'email' => 'info@rockero.cz'
])->create();
```

you can create a custom method in `ClientFactory`:

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

and then use it like that:

```php
Client::factory()
    ->github()
    ->create();
```

<a name="factory-callbacks"></a>

## Factory Callbacks

Factory callbacks can be used to perform an action after making or creating a model.

These methods are defined inside `configure()` method on factory class.

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
