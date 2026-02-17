## Yoradio: Walda's Edition

[<i>English version bellow]</i>]

Yoradio je projekt přehrávače internetových rádií a je založen na ESP32 + ADC převodník, displej, tlačítka, rotační enkodéry apod. V rámci svého baslení jsem se včak rozhodl udělat drobné vylepšení a úpravy (stejně jako mnoho dalších lidí).

Originální projekt najdete zde: https://github.com/e2002/yoradio

Moje verze vychází z originálních zdrojových kódů z poloviny roku 2025. V nich jsem provedl následující úpravy:

* Přidal jsem funkci autocommit
* Upravil jsem vzhled displeje, resp. obrazovek

#### Autocommit

Autor umožňuje ovládání přehrávače prostřednictvím tlačítek, rotačních enkodérů nebo dotykového displeje. Kombinace těchto ovládacích prvků je variabilní, přičemž nejefektivnější se jeví použití jediného enkodéru, konkrétně ENC2. Pohybem enkodéru doleva nebo doprava se přepíná mezi režimem přehrávače (zobrazení času, názvu stanice a dalších informací) a režimem playlistu (seznam stanic nahraných do ESP prostřednictvím webového rozhraní).

V režimu playlistu lze vybrat požadovanou stanici a spuštění probíhá stiskem enkodéru. Tento způsob ovládání však vykazuje jednu nevýhodu: při stisku enkodéru dochází často k nechtěnému pohybu enkodéru, což může vést ke spuštění jiné stanice, než byla zamýšlena.

Funkce autocommit řeší tuto situaci tím, že pokud v režimu playlistu enkodér přestane být otáčen, považuje se aktuální volba stanice za potvrzenou. Po uplynutí dvou sekund je tato stanice automaticky spuštěna, bez nutnosti dalšího stisku enkodéru.

Technicky jde o drobné úpravy ve třech souborech: <i>myoptions.h</i>, <i>timekeeper.cpp</i> a <i>display.cpp</i>. Co se měnilo je zde: __walda_mod__/autocommit_mod.png


#### Vzhled displeje

Pro svůj přehrávač jsem si vybral OLED displej s řadičem SSD1322. Jedná se o monochromatický (ano, umí i stupně šedi) displej s rozlišením 256x64, černým pozadním a bílými pixely. Původní vzhled byl s velkými hodinami, inverovaným zobrazením názvu stanice, posuvníkem hlasitosti apod. Nebylo to vyloženě škaredé, ale jak se říká, 100 lidí, 100 chutí.

Cílem byl konzervativní vzhled se základními údaji a bez zbytečných grafických kravinek - kromě toho čtverece s bitrate a typem kodeku.

<img src="__walda_mod__/SSD1322_mod.jpg">

Upozornění: Pokud použijete jiný displej než je tento, tak neručím za správné zobrazení. Některé sekce ve zdrojovém kódu jsou autorem velmi zobecněny a pokud bych chtěl zachovat plnou kompatibilitu s ostatními displeji, musel bych tyto úpravy napsat zcela jinak, složitěji a pak vše řádně otestovat. A tolik času se mi do toho vkládat nechtělo.



