# Nástroje pro efektivní vývoj

### Vývojová prostředí (IDE)

- [Php Storm](#php-storm)
- [VS Code](#vs-code)
- [Sublime Text](#sublime-text)

### Debug / Testování

- [Spatie Ray](#spatie-ray)
- [Tinkerwell](#tinkerwell)
- [Postman](#postman)
- [Insomnia](#insomnia)

### Database

- [Table Plus](#table-plus)
- [DBngin](#dbngin)

### Emaily

- [MailTrap](#mailtrap)
- [Helo](#helo)

### Lokální vývoj

- [HerdLaravel](#herdlaravel)

### Deployment

- [Forge](#forge)
- [Envoyer](#envoyer)

### Git

- [GitHub Desktop](#github-desktop)

### Produktivita

- [Raycast](#raycast)
- [Tuple](#tuple)
- [Slack](#slack)
- [Discord](#discord)
- [Iterm](#iterm)
- [Fig](#fig)

### Ostatní

- [Laravel Shift](#laravel-shift)

---

# Vývojová prostředí (IDE)

<a name="php-storm"></a>

## PhpStorm

OS: (MacOS, Linux, Windows)

Profesionální IDE na vývoj aplikací v php. Nejvíce se hodí na střední a větší projekty.

**Odkaz ke stažení:** [https://www.jetbrains.com/phpstorm/download](https://www.jetbrains.com/phpstorm/download)

**Výhody:**

- Hodně integrovaných funkcí na refactoring kódu
- Vše potřebné pro vývoj robustních php projektů v jedné instalaci
- Rozšiřující pluginy pro snadnější našeptávání pro Laravel
- Velká základna pluginů

**Nevýhody:**

- Pomalejší načítání projektů
- Placená licence

<a name="vs-code"></a>

## Visual Studio Code

OS: (MacOS, Linux, Windows)

Rychlý editor na efektivní práci na menších a středních projektech, ale i velké zvládne s přehledem.

**Odkaz ke stažení:** [https://code.visualstudio.com/download](https://code.visualstudio.com/download)

**Výhody:**

- Velká základna komunitních pluginů na celé spektrum jazyků
- Rychlé načítání projektů a práce s nimi
- Zdarma

**Nevýhody:**

- Nutné do instalovat pluginy pro vývoj v PHP a Laravelu
- Náročnější refactoring oproti PHPStorm

<a name="sublime-text"></a>

## Sublime Text

OS: (MacOS, Linux, Windows)

Výborný nástroj na práci s velkými soubory jako jsou dumpy z databáze, XML nebo json soubory.

**Odkaz ke stažení:** [https://www.sublimetext.com/download](https://www.sublimetext.com/download)

**Výhody:**

- Zvládá otevírání a práci s velkými soubory

**Nevýhody:**

- Podpora pluginů není udržována jako ve VS Code nebo PhpStorm
- Občasné chyby pluginů
- Placená licence

# Debug / Testování

<a name="spatie-ray"></a>

## Ray (by Spatie)

OS: (MacOS, Linux, Windows)

Nástroj pro debug php bez zásahu do flow aplikace.
Už žádné echo, dd(), dump() (Pouze sranda pořád jsou případy kdy je efektivnější napsat dd).
Ray Vám dá možnost analyzovat aplikaci efektivně s možností rozdělení debugovaných částí kódu do jednotlivých záložek dle barev.

**Odkaz ke stažení:** [https://spatie.be/products/ray](https://spatie.be/products/ray)

- Efektivní debug aplikace
- Snadná organizace dumpů dle barev
- Přehledný rozpis zápisů na jednom místě
- Hodně variant výstupů debubovaného kódu
- Při velkém množství zápisů je aplikace pomalejší
- Placená licence

<a name="tinkerwell"></a>

## Tinkerwell

OS: (MacOS, Linux, Windows)

Nástroj pro snadné testování kódu přímo na projektu s možností připojení přes ssh na remote server a spouštění scriptů na něm.

**Odkaz ke stažení:** [https://tinkerwell.app](https://tinkerwell.app)

- Efektivní testování logiky kódu na daném projektu
- Spouštění kódu v projektu bez použití browseru
- Možnost ukládání scriptů do snippets
- Pouštění scriptů přes ssh přímo na serverech. Například pro update dat v databázi
- Placená licence

<a name="postman"></a>

## Postman

OS: (MacOS, Linux, Windows)

Výkonný nástroj pro testování a vývoj API. Poskytuje uživatelské rozhraní, které umožňuje vytvářet, odesílat a testovat HTTP požadavky na různá API.

**Odkaz ke stažení:** [https://www.postman.com/downloads](https://www.postman.com/downloads)

<a name="insomnia"></a>

## Insomnia

OS: (MacOS, Linux, Windows)

Nástroj pro testování a vývoj API, podobně jako Postman. Insomnia je oblíbená u vývojářů hlavně kvůli jednoduššímu uživatelskému rozhraní a celkové přehlednosti.

**Odkaz ke stažení:** [https://insomnia.rest/pricing](https://insomnia.rest/pricing)

# Databáze

<a name="table-plus"></a>

## Table Plus

OS: (MacOS, Linux, Windows)

Úžasný nástroj pro správu nejrůznějších databází jak na lokálním environmentu tak na serverech

**Odkaz ke stažení:** [https://tableplus.com](https://tableplus.com)

- Správa databází na jednom místě
- SSH připojení na servery
- Přehledné UI
- Spouštění raw queries přímo na lokálním projektu nebo na serveru
- Debug queries
- Free licence dovolí otevřít pouze 3 záložky

<a name="dbngin"></a>

## DBngin

OS: (MacOS)

Rychlá instalace a management lokálních databází jako je PostgreSQL, MySQL, Redis.

**Odkaz ke stažení:** [https://dbngin.com](https://dbngin.com)

# Emaily

<a name="mailtrap"></a>

## Mailtrap

Cloudová služba pro testování emailů jak na lokálním environmentu tak na serveru.

**Odkaz:** [https://mailtrap.io](https://mailtrap.io)

<a name="helo"></a>

## Helo

OS: (MacOS, Linux, Windows)

Nástroj pro testování emailů na lokálním environmentu.

**Odkaz ke stažení:** [https://usehelo.com](https://usehelo.com)

# Lokální vývoj

<a name="herdlaravel"></a>

## Laravel Herd

OS: (MacOS)

Alternativa pro valet ve formě aplikace.
Rychlejší práce serveru a čas testů.

**Odkaz ke stažení:** [https://herd.laravel.com](https://herd.laravel.com)

# Deployment

<a name="forge"></a>

## Laravel Forge

Cloudová služba pro správu projektů, serverů, queues a databází na nich.

**Odkaz ke stažení:** [https://forge.laravel.com](https://forge.laravel.com)

- Snadný deployment applikace
- Propojení s gitem
- Správa serverů

<a name="envoyer"></a>

### Envoyer

Služba pro snadný deployment aplikace se zero downtime.

**Odkaz ke stažení:** [https://envoyer.io](https://envoyer.io)

- Rychlý deployment bez výpadku chodu aplikace
- Možnost nastavení deployment flow a automatického spouštění scriptů při deploymentu
- Automatizované spouštění migrací pří deploymentu aplikace
- Automatizovaný restart queues
- Placená licence

# Git

<a name="github-desktop"></a>

## GitHub Desktop

OS: (MacOS, Linux, Windows)

Snadný a rychlý management gitu s propojením na github.

**Odkaz ke stažení:** [https://desktop.github.com](https://desktop.github.com)

- Přehledné UI pro správu gitu a jednotlivých commitů
- Integrace s githubem pro rychlou práci a snadnou udržitelnost vývoje
- Zdarma

# Produktivita

<a name="raycast"></a>

## Raycast

OS: (MacOS)

Pro uživatele MacOS jasná volba jak si zefektivnit práci a být produktivnější.
"Spotlight na steroidech"

**Odkaz ke stažení:** [https://www.raycast.com](https://www.raycast.com)

- Efektivní práce s MacOS
- Rychlé a snadné spouštění aplikací
- Komunitní pluginy pro velkou část aplikací potřebných k vývoji laravelu
- Snadné otevírání projektů ve VS code

<a name="tuple"></a>

## Tuple

OS: (MacOS, Linux)

Programování ve dvouch nebo přímá asistence od dev leadera tou nejsnadnější cestou.

**Odkaz ke stažení:** [https://tuple.app](https://tuple.app)

- Komunikace v teamu s možností zásahu kohokoliv do sdílené obrazovky
- Pair programming
- Efektivní nástroj pro spolupráci remote
- Propojení s kýmkoliv kdo má aplikaci nainstalovanou a pošle Vám invite
- Placená licence

<a name="slack"></a>

## Slack

OS: (MacOS, Linux, Windows)

Komunikační nástroj pro rychlou komunikaci v teamu a možností vytváření kanálů, společností.

**Odkaz ke stažení:** [https://slack.com](https://slack.com)

- Pěkné a přehledné UI
- Placená licence

<a name="discord"></a>

## Discord

OS: (MacOS, Linux, Windows)

Alternativa slacku. S velkým množstvím komunitních kanálů.

**Odkaz ke stažení:** [https://discord.com](https://discord.com)

- Komunitní kanály například FilamentPHP, Laravel
- Možnost používat pouze v prohlížeči
- Zdarma

<a name="iterm"></a>

## iTerm

OS: (MacOS)

Rozšířený terminál.

**Odkaz ke stažení:** [https://iterm2.com](https://iterm2.com)

- Možnost více panelů
- Přepínání na fullscreen
- Upravitelnost barev fontů...
- Nastavení klávesových zkratek
- Vyhledávání v konzoli
- Komunitní pluginy

<a name="fig"></a>

## Fig

OS: (MacOS, Linux)

Rozšíření pro Váš terminál se skvělým našeptávání.

**Odkaz ke stažení:** [https://fig.io](https://fig.io)

- Rychlejší a snadnější práce s terminálem
- Našeptávání komandů popřípadě složek, souborů
- Zdarma

# Ostatní

<a name="laravel-shift"></a>

## Laravel Shift

Potřebujete snadno upgradovat svůj laravel projekt na novější verzi tak laravel shift je ta správná cesta. V porovnání s cenou Vašeho času shift překonvertuje Váš projekt na nejnovější verzi za výhodnou cenu a ne jen to. Služba má spoustu utilit například pro přechod z phpunit na pest nebo z bootstrap na tailwind a mnoho dalšího.

**Odkaz ke stažení:** [https://laravelshift.com](https://laravelshift.com)

- Automatizované upgrady laravelu na nejnovější verze
- Automatizované přepisování scriptů z phpunit do pestu
