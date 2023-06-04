# Model

## Naming

- Singular without “Model” suffix (`User`, `Product`, `Category`...)

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

- Singular with “Controller” suffix (`UserController`, `ProductController`, `CategoryController`...)

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

# Database

## Column Naming

- Primary key should be always `id`
- Foreign keys should be a singular with the suffix id (`user_id`, `product_id`, `category_id`...)
- When choosing a name you should be careful with [reserved words](https://dev.mysql.com/doc/refman/8.0/en/keywords.html)

### Names for frequently used columns:

- **order_column** - field for sorting entities (e.g. drag & drop)
- **company_number** - field for CIN / Company Identification Number
- **vat_number** - field for VATIN / VAT ID / VAT Identification Number

### Names by column type:

- **boolean** - `is_enabled`, `has_reviews`
- **timestamp** - `published_at`, `valid_from`, `scheduled_for`

> **Pro tip:** Some of boolean columns could be converted to timestamps (e.g. from is_finished to finished_at)

## Column Sorting

- **id** - should be always first
- **foreign keys**
- **rest of columns** - should be sorted by priorty and groupped by context
- **native timestamps** - `created_at`, `updated_at`

## UUIDs

Secure alternative to ids. They should be used for publicly accessible websites or for some tables with sensitive content (bank accounts, orders, invoices...). [How to use uuids?](https://laravel.com/docs/eloquent#uuid-and-ulid-keys)

## Indexes

Indexes are database structures that allow for faster retrieval of data. They work by creating a separate data structure that points to the location of the data in the database. When a query is run, the database can use the index to quickly find the relevant data instead of having to search the entire database.

> **Pro tip:** Just use indexes on any columns that are frequently queried or used in joins and your database's performance will be improved.

## Migrations

Migrations are a way to version control your database schema. They allow you to make changes to the database schema in a structured way, and enable you to easily roll back changes if necessary. [Read more](https://laravel.com/docs/migrations)

### Rules

- During development, it's fine to modify existing migration files and run `php artisan migrate:fresh` to reset the database
- Once the project is in production, you have to create new migrations for every change, even small ones
- Don't break column sorting - when adding a new column use also `after()` and `before()` methods
- Add short note with `comment()` method if column names are not clear (e.g. professional terms)

> **Pro tip:** As you build your application, you may accumulate more and more migrations over time. This can lead to your `database/migrations` directory becoming bloated with potentially hundreds of migrations. If you would like, you may "squash" your migrations into a single SQL file. [Read more](https://laravel.com/docs/migrations#squashing-migrations)

## Seeders

Seeders are used to populate a database with initial/testing data. They are especially useful in scenarios where you need to populate your database with pre-existing data, such as test data or reference data.

By using a seeder, you can quickly populate your database with the necessary data without having to manually enter it every time.

> **Pro tip:** Sometimes you need to disable model events inside seeders. You can simply make it with a trait `WithoutModelEvents` [Read more](https://laravel.com/docs/seeding#muting-model-events)

### Naming

- Singular with “Seeder” suffix (`UserSeeder`, `ProductSeeder`, `CategorySeeder`...)
