# Testování

- [Úvod](#introduction)
- [Proč psát testy?](#why-write-tests)
- [Kdy psát testy?](#when-to-write-tests)
- [Co by mělo být testováno?](#what-should-be-tested)
- [Jak psát testy?](#how-to-write-tests)
- [Helpery](#helpers)
- [Pest hooky](#pest-hooks)
- [Vlastní metody](#custom-methods)
- [Mocking](#mocking)
- [Fixtures](#fixtures)
- [Pojmenování](#naming)

---

<a name="introduction"></a>

## Úvod

Pro automatizované testování používáme framework [Pest](https://pestphp.com/) kvůli jeho mnoha výhodám. `Pest` se soustředí na jednoduchost a psaní testů je s ním opravdu zábava.

Navíc má také lepší asserty, pěknou syntaxi a skvělou dokumentaci.

**Příkaz pro vytvoření:** `php artisan make:test Actions/VerifyUserActionTest`

```php
it('has a welcome page', function() {
  $response = $this->get('/');

  expect($response->status())->toBe(200);
});
```

<a name="why-write-tests"></a>

## Proč psát testy?

- **Kvalita kódu** - psání testů Vás donutí nad kódem přemýšlet
- **Odchytávání bugů** - testy dokážou odhalit některé chyby před tím, než se dostanou na produkci
- **Úspora času** - v dlouhodobém měřítku testy snižují potřeby manuálního testování
- **Větší jistota** - je snazší provádět změny v kódu a přidávat nové funkce, jelikož je malé riziko zničení funkcionality

<a name="when-to-write-tests"></a>

## Kdy psát testy?

Každá vytvořená třída obsahující nějakou logiku by měla mít také test.

<a name="what-should-be-tested"></a>

## Co by mělo být testováno?

- Logika v kódu (akce, support třídy, joby…)
- Livewire komponenty / Controllery
- Routy

<a name="how-to-write-tests"></a>

## Jak psát testy?

Na většině projektů píšeme pouze `Feature` testy. Nicméně u některých složitých projektů je důležité zahrnout také `Unit` testy.

Při psaní testů je důležité zahrnout několik scénářů, aby se pokrylo co nejvíce možných případů. Kromě toho by testy také měly obsahovat pouze asserty, která jsou přímo související s testovanou třídou nebo funkcí. Tím se předejde redundanci a zlepší se celková čitelnost testů.

> **Pro tip:** Udržujte pokrytí testy co nejvyšší, mělo by to být alespoň 70 %.

<a name="helpers"></a>

## Helpery

Helpery mohou snížit duplicitu v kódu a zlepšit čitelnost testů. Pomocí `Pest` hooků můžete připravovat/čistit data před/po každém/všech spuštění testů. Kromě toho můžete vytvářet vlastní metody, které lze použít v několika testech.

<a name="pest-hooks"></a>

## Pest hooky

- **`beforeEach()`** - Připraví něco před každým jednotlivým spuštění testu…
- **`afterEach()`** - Vyčistí testovací data po každém jednotlivém spuštění testu…
- **`beforeAll()`** - Připraví něco před spuštěním všech testů…
- **`afterAll()`** - Vyčistí testovací data po spuštění všech testů…

<a name="custom-methods"></a>

## Vlastní metody

Tyto metody lze napsat v jednom testovacím souboru nebo přímo v souboru `Pest.php`, aby byly globálně přístupné.

**Příklad lokálního helperu v konkrétním testu:**

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

**Příklad globálního helperu v `Pest.php`:**

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

<a name="mocking"></a>

## Mocking

Mockování určitých částí vaší aplikace může být v některých případech nevyhnutelné, například u eventů, nahrávání souborů nebo během integrování třetích stran. [Více informací](https://laravel.com/docs/mocking).

**Ukázka mockování requestu:**

```php
Http::fake([
  'google.com/*' => Http::response('foo@gmail.com', 200)
]);

$response = resolve(FetchGoogleUserEmailAction::class)->run();

expect($response)->toBe('foo@gmail.com');
```

**Ukázka mockování třídy:**

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

> **Pro tip:** V případě, že vytváříte mock pro integraci externího API, měli byste také zajistit, že vaše testy netrefují oficiální endpointy - v Laravelu můžete zabránit těmto přímým requestům pomocí metody `Http::preventStrayRequests()`. Po zavolání této metody vyhodí každý test bez odpovídajícího mocku výjimku. [Více informací](https://laravel.com/docs/http-client#preventing-stray-requests)

<a name="fixtures"></a>

## Fixtures

Fixtures jsou statické soubory používané pro testování a měly by být umístěny v adresáři "fixtures". Mohou být použity v testech k simulaci skutečných zdrojů dat nebo k poskytnutí specifických podmínek pro testování.

**Ukázky použití**

```php
$payment = base_path('tests/fixtures/payment.xml');

app(ProcessPaymentAction::class)->run($payment, ...);
```

<a name="naming"></a>

## Pojmenování

Pro zajištění správného pojmenování vašich testů se doporučuje postupovat podle poskytnutého příkladu.

```php
// Good examples - lowercase, descriptive
test('payment can be processed', function() {
  ...
});

it('has a welcome page', function() {
  ...
});

// Bad example - uppercase, low descriptive
test('PAYMENT', function() {
  ...
});

it('sums', function() {
  ...
});
```
