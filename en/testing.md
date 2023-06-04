# Testing

For testing, we use a library called [Pest](https://pestphp.com/) because of its

- simplicity
- readability
- better assertations

## Why write tests?

- **Code quality** - writing tests forces you to think about the code
- **Bugs catching** - tests can reveal some bugs before the application is live
- **Time saving** - in the long term, tests should reduce the need for manual testing
- **Increased confidence** - it is easier to make changes and add new features because the risk of breaking functionality is less

## When to write tests?

Each created class containing some logic should also have a test.

## How do we write tests?

We write only _Feature tests_ on most projects. For more complex projects, it is essential to include _Unit tests_ in your development process to ensure the highest quality results.

The content of a single test should contain multiple scenarios so you can cover most of the edges.

The test should contain only assertations that are associated with the tested class so we avoid duplicated assertations.

> Ideal coverage of your tests should be greater than 80%.

## What should be tested?

- Code logic (actions, support classes, jobs…)
- Livewire components
- Routes

## Helpers

Helpers can reduce code duplication and improve test readability. You can use Pest hooks to prepare/clean data before/after each/all test runs. Additionally, you can create custom methods that can be used in multiple tests.

## Pest hooks

- **`beforeEach()`** - Prepare something before each test run…
- **`afterEach()`** - Clear testing data after each test run…
- **`beforeAll()`** - Prepare something once before any of this file's tests run…
- **`afterAll()` -** Clean testing data after all tests run…

## Custom methods

These methods can be written in a single test suite or directly in Pest.php to access them globally.

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

**Example of global helper in Pest.php:**

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

Mocking certain parts of your application can be necessary for some cases, such as events, file uploads, or 3rd party integrations. [More here](https://laravel.com/docs/9.x/mocking).

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
// The class with method you want to mock.
app(Client::class)->acceptOrder($order);

use function Pest\Laravel\mock;

mock(Client::class)
    // You may need to check the passed arguments
    ->withArgs(fn ($givenOrder, $givenState) => $givenOrder->is($order))
    // Or check the returned data
    ->andReturn(true)
    ->shouldReceive('acceptOrder')
    // You also can check how many times the class should be called
    ->once()
    ->twice()
    ->times($int)
    ->never()
```

> **Pro tip:** In case you create a mock for external API integration, you should also ensure that you don’t hit official endpoints with your tests - in Laravel you can prevent these stray requests with* `Http::preventStrayRequests()`*. After calling this method, each request without matching fake throws an exception. [Read more](https://laravel.com/docs/http-client#preventing-stray-requests)

## Fixtures

Fixtures are static files used for testing, and they should be placed inside the "fixtures" directory. They can be used in tests to simulate real data sources or to provide specific test conditions.

**Example of usage**

```php
$payment = base_path('tests/fixtures/payment.xml');

app(ProcessPaymentAction::class)->run($payment, ...);
```

## Naming

To ensure the proper naming of your test cases, it is recommended that you follow the example provided.

**Example of naming**

```php
// Good example - lowercase, descriptive
test('payment can be processed', function () {
	...
});

it('performs sums', function () {
	...
});

// Bad example - uppercase, low descriptive
it('Performs sums', function () {
	...
});
```
