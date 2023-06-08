# Table of Contents

- [Testing](#testing)
  - [Why write tests?](#why-write-tests)
  - [When to write tests?](#when-to-write-tests)
  - [What should be tested?](#what-should-be-tested)
  - [How to write tests?](#how-to-write-tests)
  - [Helpers](#helpers)
  - [Pest hooks](#pest-hooks)
  - [Custom methods](#custom-methods)
  - [Mocking](#mocking)
  - [Fixtures](#fixtures)
  - [Naming](#naming)

---

# Testing

For automated testing, we use a framework [Pest](https://pestphp.com/) because of its many benefits. `Pest` focuses on simplicity and writing tests is really enjoyable with it.

Additionally, it also has better assertions, cool syntax, and great documentation.

**Create command:** `php artisan make:test Actions/VerifyUserActionTest`

```php
it('has a welcome page', function() {
  $response = $this->get('/');

  expect($response->status())->toBe(200);
});
```

## Why write tests?

- **Code quality** - writing tests forces you to think about the code
- **Bugs catching** - tests can reveal some bugs before the application is live
- **Time saving** - in the long term, tests should reduce the need for manual testing
- **Increased confidence** - it is easier to make changes and add new features because there is less risk of breaking functionality.

## When to write tests?

Each created class containing some logic should also have a test.

## What should be tested?

- Code logic (actions, support classes, jobs…)
- Livewire components / Controllers
- Routes

## How to write tests?

On most projects, we only write `Feature` tests. However, on some complex ones, it is crucial to include also `Unit` tests.

When writing tests, it is important to include multiple scenarios to cover most of edge cases. Additionally, tests should only contain assertions that are directly related to the tested class or function to avoid redundancy and improve readability.

> **Pro tip:** Keep your coverage as high as possible, it should be at least 70%.

## Helpers

Helpers can reduce code duplication and improve test readability. You can use `Pest` hooks to prepare/clean data before/after each/all test runs. Additionally, you can create custom methods that can be used in multiple tests.

## Pest hooks

- **`beforeEach()`** - Prepare something before each test run…
- **`afterEach()`** - Clear testing data after each test run…
- **`beforeAll()`** - Prepare something once before any of this file's tests run…
- **`afterAll()` -** Clean testing data after all tests run…

## Custom methods

These methods can be written in a single test suite or directly in `Pest.php` to access them globally.

**Example of local helper in a single test suite:**

```php
function asAdmin(): User
{
  $user = User::factory()->create(['admin' => true]);

  return test()->actingAs($user);
}

it('can manage users', function () {
  asAdmin()->get('/users')->assertOk();
})
```

**Example of global helper in `Pest.php`:**

```php
function mockPayments(): object
{
  $client = Mockery::mock(PaymentClient::class);

  return $client;
}

it('may buy a book', function () {
  $client = mockPayments();
})
```

## Mocking

Mocking certain parts of your application can be necessary for some cases, such as events, file uploads, or 3rd party integrations. [More here](https://laravel.com/docs/mocking).

**Example of request mocking:**

```php
Http::fake([
  'google.com/*' => Http::response('foo@gmail.com', 200)
]);

$response = resolve(FetchGoogleUserEmailAction::class)->run();

expect($response)->toBe('foo@gmail.com');
```

**Example of class mocking:**

```php
use function Pest\Laravel\mock;

mock(Client::class)
    // You may need to check the passed arguments
    ->withArgs(fn ($givenOrder) => $givenOrder->is($order))
    // Or check the response
    ->andReturn(true)
    ->shouldReceive('acceptOrder')
    // You also can check how many times the class should be called
    ->never()
    ->once()
    ->twice()
    ->times(3)
```

> **Pro tip:** In case you create a mock for external API integration, you should also ensure that you don't hit official endpoints with your tests - in Laravel you can prevent these stray requests with `Http::preventStrayRequests()`. After calling this method, each request without matching fake throws an exception. [Read more](https://laravel.com/docs/http-client#preventing-stray-requests)

## Fixtures

Fixtures are static files used for testing, and they should be placed inside the "fixtures" directory. They can be used in tests to simulate real data sources or to provide specific test conditions.

**Usage examples**

```php
$payment = base_path('tests/fixtures/payment.xml');

app(ProcessPaymentAction::class)->run($payment, ...);
```

## Naming

To ensure the proper naming of your test cases, it is recommended that you follow the example provided.

```php
// Good examples - lowercase, descriptive
test('payment can be processed', function() {
  ...
});

it('has a welcome page', function() {
  ...
});

// Bad example - uppercase, low descriptive
it('sums', function() {
  ...
});
```
