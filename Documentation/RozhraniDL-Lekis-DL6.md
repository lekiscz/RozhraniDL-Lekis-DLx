# Rozhraní dodacího listu a převodky Lekis DL6

## Název

Soubor má jméno ve tvaru "XXXXXXXX.DL6", kde XXXXXXXX je označení souboru s dodacím listem nebo převodkou dodavatelem (označení je libovolné a nemusí se shodovat s číslem dodacího listu, pokud je to možné z hlediska délky a jednoznačnosti, je to vhodné). Počet znaků je 1-8 a je vyžadováno, aby byl název byl pro daného dodavatele jedinečný.

## Obsah

V jednom souboru je uložen vždy pouze jeden dodací list nebo převodka.

Formát neobsahuje žádné rozlišení, zda jde o dodací list nebo převodku.

Jedná se o textový formát s pevnou délkou polí. První řádek představuje hlavičku dodacího listu, další řádky představují položky dodacího listu.

### Hlavička souboru (1. věta, tedy 1. řádek)

| Název                             | Pozice    | Typ   | Délka* | Zar.  | Poznámky |
|-----------------------------------|-----------|-------|--------|-------|----------|
| IČ dodavatele                     | 1-20      | C     | 20     | L     | IČ dodavatele (distributora) |
| Označení DL                       | 21-40     | C     | 20     | L     | označení (číslo) dodacího listu |
| IČ odběratele                     | 41-60     | C     | 20     | L     | IČ odběratele (lékárny) |
| Číslo objednávky                  | 61-72     | N     | 12,0   | R     | označení (číslo) objednávky, na základě které vznikl tento DL<br />(nepovinný údaj) |
| Kódová stránka                    | 73-77     | N     | 5      | R     | kódová stránka pro položku "Název" |
| Počet položek                     | 78-85     | N     | 8      | R     | počet položek dodacího listu<br />(kontrolní údaj) |
| Součet bez DPH                    | 86-95     | N     | 10,2   | R     | součet všech cen bez DPH - hradí lékárna |
| Součet s DPH                      | 96-105    | N     | 10,2   | R     | součet všech cen s DPH - hradí lékárna |
| Součet bez DPH (1. snížená sazba) | 106-115   | N     | 10,2   | R     | součet celkových cen bez DPH pro zboží v první snížené sazbě DPH (př. v 15% k 1.1.2015) |
| Součet s DPH (1. snížená sazba)   | 116-125   | N     | 10,2   | R     | součet celkových cen s DPH pro zboží v první snížené sazbě DPH (př. v 15% k 1.1.2015) |
| Součet bez DPH (2. snížená sazba) | 126-135   | N     | 10,2   | R     | součet celkových cen bez DPH pro zboží v druhé snížené sazbě DPH (př.v 10% k 1.1.2015) |
| Součet s DPH (2. snížená sazba)   | 136-145   | N     | 10,2   | R     | součet celkových cen s DPH pro zboží v druhé snížené sazbě DPH (př. v 10% k 1.1.2015) |
| Součet bez DPH (základní sazba)   | 146-155   | N     | 10,2   | R     | součet celkových cen bez DPH pro zboží v základní sazbě DPH (př. v 21% k 1.1.2015) |
| Součet s DPH (základní sazba)     | 156-165   | N     | 10,2   | R     | součet celkových cen s DPH pro zboží v základní sazbě DPH (př. v 21% k 1.1.2015) |
| ID skladu                         | 166-175   | C     | 10     | L     | rozlišení skladu pro shodné IČ dodavatele<br />(nepovinný údaj) |

### Položky dodacího listu (počínaje druhou větou)

Každý řádek představuje jednu položku dodacího listu. Mezi jednotlivými řádky nesmí být prázdný řádek. Všechny ceny uvedené u položek jsou jednotkové.

| Název                 | Pozice    | Typ   | Délka*    | Zar.  | Poznámky |
|-----------------------|-----------|-------|-----------|-------|----------|
| Kód                   | 1-7       | C     | 7         | R     | kód přípravku používaný v číselnících VZP či KLK (kód VZP či kód SÚKLu)<br />u skupiny 4 nebo 8 se neuvádí (vyplňuje se mezerami) |
| Název                 | 8-67      | C     | 60        | L     | název položky / přípravku |
| Skupina               | 68-68     | N     | 1,0       | R     | `1` registrované LP<br /> `2` IVLP<br /> `3` PZT<br /> `4` ostatní<br /> `8` ostatní osvobozené při prodeji konečnému spotřebiteli v lékárně od DPH |
| DPH                   | 69-73     | N     | 5,2       | R     | sazba DPH distributora |
| Výrobní cena          | 74-82     | N     | 9,2       | R     | cena původce<br />pouze u regulovaných přípravků |
| Nákupní cena s DPH    | 83-91     | N     | 9,2       | R     | jednotková nákupní cena lékárny, tj. prodejní cena distributora včetně DPH |
| Prodejní cena s DPH   | 92-100    | N     | 9,2       | R     | jednotková doporučená prodejní cena lékárny včetně DPH |
| Množství              | 101-108   | N     | 8,2       | R     | dodané množství |
| Šarže                 | 109-128   | C     | 20        | L     | šarže zboží<br />(nepovinný údaj) |
| Exspirace             | 129-138   | C     | 10        | L     | exspirační (záruční) doba<br />formát DD.MM.RRRR<br />(nepovinný údaj) |
| Čárový kód            | 139-158   | C     | 20        | L     | čárový kód zboží<br />u skupiny 4 nebo 8 slouží jako identifikační údaj<br />(nepovinný údaj) |
| Kód dodavatele        | 159-178   | C     | 20        | L     | kód zboží používaný dodavatelem<br />u skupiny 4 nebo 8 slouží jako identifikační údaj, má přednost před položkou "Čárový kód" |
| Druh kódu dodavatele  | 179-179   | N     | 1,0       | R     | `3` PDK kód<br /> `0` interní (skladový) kód dodavatele |
| Nákupní cena bez DPH  | 180-188   | N     | 9,2       | R     | jednotková nákupní cena lékárny, tj. prodejní cena distributora bez DPH |
| Certifikát            | 189-208   | C     | 20        | L     | cetrifikát (atest)<br />pouze pro suroviny |

### Kódové stránky

| Označení kódové stránky | Název kódové stránky |
|-------------------------|----------------------|
| 437                     | U.S. MS-DOS |
| 852                     | Eastern European MS-DOS |
| 895                     | Kamenický (Czech) MS-DOS |
| 1250                    | Windows-1250 |

### Poznámky

\* V údaji Délka znamená první číslice celkový počet míst (i s desetinnou tečkou) a druhá počet míst za desetinnou tečkou.
