# Domácí úkol 1 - program na výpočet zobrazení


## Základní funkce programu
Program umí vypočítat 4 válcová tečná zobrazení, a to Marinovo,
Lambertovo, Braunovo a Mercatorovo. Dle zadaných vstupů vypočte vzdálenosti 
rovnoběžek a poledníků ve vodorovné, respektive svislé ose tak, jak 
bychom je vykreslovali na papír. 

### Vstupy
Nejdříve je nutné zadat požadované zobrazení. Program se po spuštění zeptá
uživatele na zobrazení, přesněji na jeho počíteční písmeno. Pro jednotlivá 
zobrazení jsou definována tato písmena:

- `L` - Lambertovo zobrazení
- `A` - Marinovo zobrazení 
- `B` - Braunovo zobrazení 
- `M` - Mercatorovo zobrazení 

Dále se program uživatele zaptá na poloměr Země. Poloměr Země je volitelný,
uživatel tedy může zadat libovolný poloměr. Pokud ale nechce zadávat poloměr, 
může využít defaultně nastaveného poloměru, který se rovná 6371,11 km a který
uživatel zvolí, pokud za poloměr zadá 0. Poloměr definován jako desetinné číslo.

Posledním vstupem je měřítko. U měřítka je požadován pouze vstup m z tvaru 1:m, 
to znamená, že např. při požadovaném měřítku 1 : 50000000 je nutné zadat pouze 
číslo 500000000. Měřítko je nutné zadávat vždy pouze celočíselně. 

### Výpočet zobrazení

Zobrazení jsou počítána dle daných vzorců. Pro přehlednější a efektivnější 
výpočet zobrazení je definováno několik vlastních funkcí. K výpočtu zobrazení 
byly použity funkce z knihovny math, konkrétně radians, sin, tan a log.

Výpočt poledníků je shodný pro všechna zobrazení, proto je pro něj definována
pouze jedna funkce. Ve funkci je použit  for cyklus, který zajišťuje opakování
výpočtu pro poledníky po 10 stupních. Nastaven je od -180 do 190 stupňů (protože
range nepočítá s koncovou hodnotou včetně). Výsledky jsou vypisovány s přesností 
na milimetry, zaokrouhlení výsledku na 1 desetinné místo zajišťuje funkce round. 
Funkce na výpočet poledníků vrací výslednou hodnotu v centimetrech zaokrouhlenou 
na 1 desetinné místo. Pokud je výsledná hodnota větší než 100 cm, respektive menší 
než -100 cm, vypíše program místo hodnoty "-". 

Výpočet rovnoběžek se liší dle požadovaného zobrazení, proto jsou zde definovány
celkem 4 funkce. Všechny ale fungují na stejném proncipu jako výpočet poledníků. 
Opět je zde zase for cyklus, který bere z intervalu od -90 do 100 stupňů hodnoty
po deseti. Pouze u výpočtu Mercatorova zobrazení je interval omezen na -80 až 80
stupňů, neboť v 90 stupních se blíží tyto hodnoty do nekonečna. Výsledky jsou taktéž
uvedeny s přesností na milimetry. Pro hodnoty větší než 100 cm a menší než -100 cm 
program opět vypisuje "-". 

### Výstupy

Výstupem základního běhu programu je výpis následujících údajů, například: 

- Zadané zobrazení: B
- Zadaný poloměr Země je: 6371,11 km
- Zadané měřítko je: 1:10000000
- Rovnoběžky: [-63.7, -53.5, -44.6, -36.8, -29.7, -23.2, -17.1, -11.2, -5.6, 0.0, 5.6, 
11.2, 17.1, 23.2, 29.7, 36.8, 44.6, 53.5, 63.7]
- Poledníky: ['-', '-', '-', '-', '-', '-', '-', '-', '-', '-', -89.0, -77.8, -66.7, -55.6, 
-44.5, -33.4, -22.2, -11.1, 0.0, 11.1, 22.2, 33.4, 44.5, 55.6, 66.7, 77.8, 89.0, '-', '-', 
'-', '-', '-', '-', '-', '-', '-', '-']

### Řešení nesprávných vstupů

#### Zobrazení:
Pokud uživatel zadá nesprávné písmeno zbrazení, program uvede chybovou hlášku: 
"Zadej správné počáteční písmeno zobrazení!" a skončí. Program se ukončí také v případě, 
že uživatel zadá písmeno x. 

#### Poloměr:
Chybovou hlášku vydá program v případě, že uživatel zadá jako měřítko číslo menší než 0, 
v tomto případě také program skončí. 

#### Měřítko:
Program vydá chybovou hlášku a ukončí se, pokud uživatel zadá za měřítko číslo menší 
nebo rovno nule. 


## Nadstavbové funkce programu

### Výpočet souřadnic zadaných bodů
Po úspěšném proběhnutí základního běhu programu se program uživatele zeptá na souřadnice 
(zeměpisnou šířku a zeměpisnou délku) libovolného bodu. Ty jsou pak dle na začátku zvoleného 
zobrazení, poloměru a měřítka přepočteny. 

Opakované dotazování uživatele na vstup je zajištěno pomocí nekonečného while cyklu, 
ve kterém jsou podmínkami ošetřeny nekorektní vstupy od uživatele. Pokud uživatel zadá 
zeměpisnou délku nebo šířku v nesprávných stupních, vydá hlášku a ptá se znovu na vstup. 
Taktéž při výpočtu Mercatorova zobrazení nepovoluje vstup větší nebo roven 90°, respektive - 90°. 
Pokud uživatel zadá jako vstup bod o souřadnicích [0,0], program skončí. 
