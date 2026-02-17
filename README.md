## Yoradio: Walda's Edition

[<i>English version bellow]</i>]

Projekt YoRadio představuje přehrávač internetových rádií založený na platformě ESP32. Hardwarová konfigurace typicky zahrnuje externí DA převodník, displej, tlačítka a rotační enkodéry.

V rámci vlastní implementace byly provedeny dílčí úpravy a rozšíření funkčnosti oproti původní verzi projektu.

Původní projekt je dostupný v repozitáři GitHub: https://github.com/e2002/yoradio

Upravená verze vychází ze zdrojových kódů publikovaných přibližně v polovině roku 2025. Oproti této verzi byly realizovány následující změny:

* implementace funkce autocommit
* úprava grafického rozhraní a vzhledu zobrazovaných obrazovek.

#### Autocommit

Autor umožňuje ovládání přehrávače prostřednictvím tlačítek, rotačních enkodérů nebo dotykového displeje. Kombinace těchto ovládacích prvků je variabilní, přičemž nejefektivnější se jeví použití jediného enkodéru, konkrétně ENC2. Pohybem enkodéru doleva nebo doprava se přepíná mezi režimem přehrávače (zobrazení času, názvu stanice a dalších informací) a režimem playlistu (seznam stanic nahraných do ESP prostřednictvím webového rozhraní).

V režimu playlistu lze vybrat požadovanou stanici a spuštění probíhá stiskem enkodéru. Tento způsob ovládání však vykazuje jednu nevýhodu: při stisku enkodéru dochází často k nechtěnému pohybu enkodéru, což může vést ke spuštění jiné stanice, než byla zamýšlena.

Funkce autocommit řeší tuto situaci tím, že pokud v režimu playlistu enkodér přestane být otáčen, považuje se aktuální volba stanice za potvrzenou. Po uplynutí dvou sekund je tato stanice automaticky spuštěna, bez nutnosti dalšího stisku enkodéru.

Technicky jde o drobné úpravy ve třech souborech: <i>myoptions.h</i>, <i>timekeeper.cpp</i> a <i>display.cpp</i>. Co se měnilo je <a href="__walda_mod__/autocommit_mod.png">ZDE</a>. 

[![Watch the video](https://img.youtube.com/vi/5O8sYkVi7VU/maxresdefault.jpg)](https://youtu.be/5O8sYkVi7VU)


#### Vzhled displeje

Pro realizaci přehrávače byl zvolen OLED displej s řadičem SSD1322. Jedná se o monochromatický displej s podporou stupňů šedi, s rozlišením 256 × 64 pixelů, černým pozadím a světlými (bílými) obrazovými body.

Původní grafické rozhraní obsahovalo výrazné digitální hodiny, inverzní zobrazení názvu stanice, grafický indikátor hlasitosti a další prvky. Přestože bylo funkční, výsledné provedení nevyhovovalo požadovanému stylu zobrazení.

Cílem úpravy bylo vytvořit konzervativně pojaté uživatelské rozhraní se zobrazením pouze základních informací a bez nadbytečných grafických prvků. Výjimku tvoří čtverec zobrazující datový tok (bitrate) a použitý kodek, který se mi velmi libí.

Upozornění: Použití jiného typu displeje může vést k nesprávnému zobrazení. Některé části zdrojového kódu jsou navrženy obecně, nicméně úpravy byly provedeny specificky s ohledem na parametry použitého displeje. Zachování plné kompatibility s jinými zobrazovacími moduly by vyžadovalo odlišnou implementaci, vyšší míru abstrakce a následné důkladné testování, což nebylo předmětem této úpravy.



