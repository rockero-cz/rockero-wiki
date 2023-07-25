# Nástroje pro efektivní vývoj

### IDE / Editory
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
- [Valet](#valet)
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

## IDE / Editory

<a name="php-storm"></a>

### Php Storm

Profesionální IDE na vývoj aplikací v php. Nejvíce se hodí na střední a větší projekty.

Výhody:
- Hodně integrovaných funkcí na refactoring kódu.
- Vše potřebné pro vývoj robustních php projektů v jedné instalaci.
- Rozšiřující pluginy pro snadnější našeptávání pro Laravel.
- Velká základna pluginů.

Nevýhody:
- Pomalejší načítání projektů.
- Placená licence (Úhel pohledu).

https://www.jetbrains.com/phpstorm/


<a name="vs-code"></a>

### VS Code

Rychlý editor na efektivní práci na menších a středních projektech, ale i velké zvládne s přehledem.

Výhody:
- Velká základna komunitních pluginů na celé spektrum jazyků.
- Rychlé načítání projektů a práce s nimi.
- Zdarma.

Nevýhody:
- Nutné do instalovat pluginy pro vývoj v php a laravelu.
- Náročnější refactoring oproti PHP Strom.

https://code.visualstudio.com/


<a name="sublime-text"></a>

### Sublime Text

Výborný nástroj na práci s velkými soubory jako jsou dumpy z databáze, XML nebo json soubory.

Výhody:
- Zvládá otevírání a práci s velkými soubory.

Nevýhody:
- Podpora pluginů není udržována jako ve VS Code nebo PHP storm.
- Občasné chyby pluginů.
- Placená licence (Úhel pohledu).

https://www.sublimetext.com/


## Debug / Testování


<a name="spatie-ray"></a>

### Spatie Ray

Nástroj pro debug php bez zásahu do flow aplikace.
Už žádné echo, dd(), dump() (Pouze sranda pořád jsou případy kdy je efektivnější napsat dd).
Ray Vám dá možnost analyzovat aplikaci efektivně s možností rozdělení debugovaných částí kódu do jednotlivých záložek dle barev.

Výhody:
- Efektivní debug aplikace.
- Snadná organizace dumpů dle barev.
- Přehledný rozpis zápisů na jednom místě.
- Hodně variant výstupů debubovaného kódu.

Nevýhody:
- Při velkém množství zápisů je aplikace pomalejší.
- Placená licence (Úhel pohledu).

https://spatie.be/products/ray


<a name="tinkerwell"></a>

### Tinkerwell

Nástroj pro snadné testování kódu přímo na projektu s možností připojení přes ssh na remote server a spouštění scriptů na něm.

Výhody:
- Efektivní testování logiky kódu na daném projektu.
- Spouštění kódu v projektu bez použití browseru.
- Možnost ukládání scriptů do snippets.
- Pouštění scriptů přes ssh přímo na serverech. Například pro update dat v databázi.

Nevýhody:
- Placená licence (Úhel pohledu).

https://tinkerwell.app/

<a name="postman"></a>

### Postman

Nástroj pro testování api.

https://www.postman.com/


<a name="insomnia"></a>

### Insomnia

Nástroj na design, debug a testování API.

https://insomnia.rest/


## Databáze


<a name="table-plus"></a>

### Table Plus

Úžasný nástroj pro správu nejrůznějších databází jak na lokálním environmentu tak na serverech.

Výhody:
- Správa databází na jednom místě.
- SSH připojení na servery.
- Přehledné UI.
- Spouštění raw queries přímo na lokálním projektu nebo na serveru.
- Debug queries.

Nevýhody:
- Free licence dovolí otevřít pouze 3 záložky.

https://tableplus.com/

<a name="dbngin"></a>

### DBngin

Rychlá instalace a management lokálních databází jako je PostgreSQL, MySQL, Redis.

https://dbngin.com/


## Emaily

<a name="mailtrap"></a>

### MailTrap

Cloudová služba pro testování emailů jak na lokálním environmentu tak na serveru.

https://mailtrap.io/

<a name="helo"></a>

### Helo

Nástroj pro testování emailů na lokálním environmentu.

https://usehelo.com/

## Lokální vývoj

<a name="valet"></a>

### Valet

Snadný způsob jak spravovat projekty a lokální server.
Díky valetu můžete snadno spouštět nové projekty a okamžitě na nich pracovat bez nutnosti nastavování lokálního prostředí.
Lze snadno měnit PHP verzi pro jednotlivé projekty přes isolate.

https://laravel.com/docs/valet

<a name="herdlaravel"></a>

### HerdLaravel

Alternativa pro valet ve formě aplikace.
Rychlejší práce serveru a čas testů.

https://herd.laravel.com/


## Deployment

<a name="forge"></a>

### Forge

Cloudová služba pro správu projektů, serverů, queues a databází na nich.

Výhody:
- Snadný deployment applikace.
- Propojení s gitem.
- Správa serverů.

https://forge.laravel.com/

<a name="envoyer"></a>

### Envoyer

Služba pro snadný deployment aplikace se zero downtime.

Výhody:
- Rychlý deployment bez výpadku chodu aplikace.
- Možnost nastavení deployment flow a automatického spouštění scriptů při deploymentu.
- Automatizované spouštění migrací pří deploymentu aplikace.
- Automatizovaný restart queues.

Nevýhody:
- Placená licence (Úhel pohledu).

https://envoyer.io/


## Git

<a name="github-desktop"></a>

### GitHub Desktop

Snadný a rychlý management gitu s propojením na github.

Výhody:
- Přehledné UI pro správu gitu a jednotlivých commitů.
- Integrace s githubem pro rychlou práci a snadnou udržitelnost vývoje.
- Zdarma.

https://desktop.github.com/


## Produktivita

<a name="raycast"></a>

### Raycast

Pro uživatele MAC OS jasná volba jak si zefektivnit práci a být produktivnější.
"Spotlight na steroidech"

Výhody:
- Efektivní práce s MAC OS.
- Rychlé a snadné spouštění aplikací.
- Komunitní pluginy pro velkou část aplikací potřebných k vývoji laravelu.
- Snadné otevírání projektů ve VS code.

Nevýhody:
- Placená licence (Úhel pohledu).

https://www.raycast.com/


<a name="tuple"></a>

### Tuple

Programování ve dvouch nebo přímá asistence od dev leadera tou nejsnadnější cestou.

Výhody:
- Komunikace v teamu s možností zásahu kohokoliv do sdílené obrazovky.
- Pair programming.
- Efektivní nástroj pro spolupráci remote.
- Propojení s kýmkoliv kdo má aplikaci nainstalovanou a pošle Vám invite.

Nevýhody:
- Pouze pro Mac.
- Placená licence (Úhel pohledu).

https://tuple.app/


<a name="slack"></a>

### Slack

Komunikační nástroj pro rychlou komunikaci v teamu a možností vytváření kanálů, společností.

Výhody:
- Pěkné a přehledné UI.

Nevýhody:
- Placená licence (Úhel pohledu).

https://slack.com/


<a name="discord"></a>

### Discord

Alternativa slacku. S velkým množstvím komunitních kanálů.

Výhody:
- Zdarma.
- Komunitní kanály například FilamentPHP, Laravel.
- Možnost používat pouze v prohlížeči.

https://discord.com/


<a name="iterm"></a>

### Iterm

Rozšířený terminál pro MAC OS.

Výhody:
- Možnost více panelů.
- Přepínání na fullscreen.
- Upravitelnost barev fontů...
- Nastavení klávesových zkratek.
- Vyhledávání v konzoli.
- Komunitní pluginy.

https://iterm2.com/


<a name="fig"></a>

### Fig

Rozšíření pro Váš terminál se skvělým našeptávání.

Výhody:
- Rychlejší a snadnější práce s terminálem.
- Našeptávání komandů popřípadě složek, souborů.
- Zdarma.

https://fig.io/


## Ostatní

<a name="laravel-shift"></a>

### Laravel Shift

Potřebujete snadno upgradovat svůj laravel projekt na novější verzi tak laravel shift je ta správná cesta. V porovnání s cenou Vašeho času shift překonvertuje Váš projekt na nejnovější verzi za výhodnou cenu a ne jen to. Služba má spoustu utilit například pro přechod z phpunit na pest nebo z bootstrap na tailwind a mnoho dalšího.

Výhody:
- Automatizované upgrady laravelu na nejnovější verze.
- Automatizované přepisování scriptů z phpunit do pestu.

Nevýhody:
- Placená licence (Úhel pohledu).

https://laravelshift.com/
