# Best practices

- [Přijměte standardy a principy a dodržujte je.](#accept-the-standards-and-principles-and-follow-them)
- [Raději mít duplicitní kód než mít **špatnou** abstrakci.](#duplicated-code-is-preferred-over-the-wrong-abstraction)
- [Držte pokrytí testy co nejvyšší.](#keep-test-coverage-as-high-as-possible)
- [Používejte statickou analýzu k udržení vysoké kvality kódu.](#use-static-analysis-to-keep-code-high-quality)
- [Používejte Artisan CLI k vytváření tříd.](#use-artisan-cli-for-creating-classes)
- [Zjednodušte svou business logiku pomocí akcí.](#simplify-your-business-logic-with-action-classes)
- [Seskupujte třídy do podsložek podle typu.](#group-classes-into-subfolders-by-resources)
- [Držte metody controllerů krátké.](#keep-controller-methods-thin)
- [Modely by měly obsahovat pouze věci související s databází.](#models-should-contain-only-database-related-things)
- [Nikdy neupravujte databázi natvrdo, vždy používejte migrace.](#never-update-the-database-directly-always-use-migrations)

---

<a name="accept-the-standards-and-principles-and-follow-them"></a>

## Přijměte standardy a principy a dodržujte je.

Kód se pak snadněji udržuje a také se zlepšuje jeho čitelnost a konzistence.

Pokud nevíte, jak napsat specifickou část kódu, tak zkuste trochu hledat - ponořte se hlouběji do codebase Laravelu, procházejte repozitáře s hodně hvězdičkami na GitHubu, a nebo prozkoumejte zdrojový kód znamých balíčků.

```
"Konzistence je klíč" - Spatie
```

---

<a name="duplicated-code-is-preferred-over-the-wrong-abstraction"></a>

## Raději mít duplicitní kód, než **špatnou** abstrakci.

Pokud narazíte, oprava špatné abstrakce Vás může stát hodně času, protože může být použita na mnoha místech a mohou se na ni vázat další věci, které bude potřeba přepsat.

Je lepší počkat až budete mít jistotu ohledně abstrakce a pak se pustit do refaktorování.

---

<a name="keep-test-coverage-as-high-as-possible"></a>

## Držte pokrytí testy co nejvyšší.

Ideální pokrytí je vyšší než 70%. My konkrétně se snažíme, aby naše aplikace byly pokryty alespoň z 80%.

```php
php artisan test --coverage --min=80
```

---

<a name="use-static-analysis-to-keep-code-high-quality"></a>

## Používejte statickou analýzu k udržení vysoké kvality kódu.

My používáme [PHPStan](https://phpstan.org), který za nás odhaluje chybějící typy a návratové hodnoty.

```php
./vendor/bin/phpstan
```

---

<a name="use-artisan-cli-for-creating-classes"></a>

## Používejte Artisan CLI k vytváření tříd.

Artisan generuje třídy ze šablon a tím Vás nutí dodržovat danou strukturu.

```php
php artisan make:migration CreateProductsTable
php artisan make:controller ProductController
```

---

<a name="simplify-your-business-logic-with-action-classes"></a>

## Zjednodušte svou business logiku pomocí akcí.

Tyto třídy jsou zodpovědné pouze za jednu jedinou úlohu, což vede k čistšímu a srozumitelnějšímu kódu pro ostatní.

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

---

<a name="group-classes-into-subfolders-by-resources"></a>

## Seskupujte třídy do podsložek podle typu.

Struktura složek je čistší a snadnější na udržování.

```php
- Actions/User/VerifyUserAction.php
- Actions/User/BanUserAction.php

- Actions/Order/CreateOrderAction.php
- Actions/Order/ConfirmOrderAction.php
- Actions/Order/CancelOrderAction.php
```

---

<a name="keep-controller-methods-thin"></a>

## Držte metody controllerů krátké.

Controllery jsou zodpovědné za jednu hlavní věc - vrácení odpovědi. Neměly by obsahovat žádnou významnou logiku.

```php
/**
 * Store a newly created resource in storage.
 */
public function store(StoreUserRequest $request): JsonResponse
{
    $user = User::query()->create($request->validated());

    return response()->json($user);
}
```

---

<a name="models-should-contain-only-database-related-things"></a>

## Modely by měly obsahovat pouze věci související s databází.

Nepište do nich rozsáhlou business logiku, ta by měla být raději napsána v třídách `Support` nebo `Action`.

---

<a name="never-update-the-database-directly-always-use-migrations"></a>

## Nikdy neupravujte databázi natvrdo, vždy používejte migrace.

Migrace Vám umožňují sdílet schéma databáze mezi členy týmu a mezi prostředími.

Jsou také vaším verzováním databáze. Pokud upravíte databázi natvrdo, tak to může vytvořit mnoho problémů, které se budou zpětně špatně hledat. Neexistuje žádný důvod, proč by je někdo neměl používat.
