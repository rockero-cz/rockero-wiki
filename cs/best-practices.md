# Obsah

- [Přijměte standardy a principy a dodržujte je.](#přijměte-standardy-a-principy-a-dodržujte-je)
- [Raději mít duplicitní kód než mít **špatnou** abstrakci.](#raději-mít-duplicitní-kód-než-mít-špatnou-abstrakci)
- [Držte pokrytí testy co nejvyšší.](#držte-pokrytí-testy-co-nejvyšší)
- [Používejte statickou analýzu k udržení vysoké kvality kódu.](#používejte-statickou-analýzu-k-udržení-vysoké-kvality-kódu)
- [Používejte Artisan CLI k vytváření tříd.](#používejte-artisan-cli-k-vytváření-tříd)
- [Zjednodušte svou business logiku pomocí akcí.](#zjednodušte-svou-business-logiku-pomocí-akcí)
- [Seskupujte třídy do podsložek podle typu.](#seskupujte-třídy-do-podsložek-podle-typu)
- [Držte metody controllerů krátké.](#držte-metody-controllerů-krátké)
- [Modely by měly obsahovat pouze věci související s databází.](#modely-by-měly-obsahovat-pouze-věci-související-s-databází)
- [Nikdy neupravujte databázi natvrdo, vždy používejte migrace.](#nikdy-neupravujte-databázi-natvrdo-vždy-používejte-migrace)

---

## Přijměte standardy a principy a dodržujte je.

Kód se pak snadněji udržuje a také se zlepšuje jeho čitelnost a konzistence.

Pokud nevíte, jak napsat specifickou část kódu, tak zkuste trochu hledat - ponořte se hlouběji do codebase Laravelu, procházejte repozitáře s hodně hvězdičkami na GitHubu, a nebo prozkoumejte zdrojový kód znamých balíčků.

```
"Konzistence je klíč" - Spatie
```

---

## Raději mít duplicitní kód, než **špatnou** abstrakci.

Pokud narazíte, oprava špatné abstrakce Vás může stát hodně času.

Je lepší počkat až budete mít jistotu ohledně abstrakce a pak se pustit do refaktorování.

---

## Držte pokrytí testy co nejvyšší.

Ideální pokrytí je vyšší než 70%. My konkrétně se snažíme, aby naše aplikace byly pokryty alespoň z 80%.

```php
php artisan test --coverage --min=80
```

---

## Používejte statickou analýzu k udržení vysoké kvality kódu.

My používáme [PHPStan](https://phpstan.org), který za nás odhaluje chybějící typy a návratové hodnoty.

```php
./vendor/bin/phpstan
```

---

## Používejte Artisan CLI k vytváření tříd.

Artisan generuje třídy ze šablon a tím Vás nutí dodržovat danou strukturu.

```php
php artisan make:migration CreateProductsTable
php artisan make:controller ProductController
```

---

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

## Modely by měly obsahovat pouze věci související s databází.

Nepište do nich rozsáhlou business logiku, ta by měla být raději napsána v třídách `Support` nebo `Action`.

---

## Nikdy neupravujte databázi natvrdo, vždy používejte migrace.

Migrace Vám umožňují sdílet schéma databáze mezi členy týmu a mezi prostředími.

Jsou také vaším verzováním databáze. Neexistuje žádný důvod, proč by je někdo neměl používat.
