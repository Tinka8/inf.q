## Úloha 1

### Zadanie

Slovo DNES má zakódovaný tvar 01000100000000000100111000000000xxxxxxxxxxxxxxxx0101001100000000 (64 bitov). 
Rozhodnite, ktorý z bežne používaných kódov bol použitý, doplňte bity za x a zhodnoťte (uveďte výhody a nevýhody použitého kódu).

### Postup

- Vieme, že výsledný kód má mať 64 bitov a jeho formát je:
```
01000100000000000100111000000000xxxxxxxxxxxxxxxx0101001100000000
```
- Vieme, že každé písmeno predstavuje 8 bitov (UTF-8), rozdelíme si celý reťazec zo zadania po 8 znakoch

```
01000100 00100000 01001110 00100000 xxxxxxxx xxxxxxxx 01010011 00100000
```
- Vieme, že v reťazci sa nachádza určite 8 znakov (pretože 64 / 8 je 8 bitov) a zo zadania vieme, že jeden znak sa opakuje minimálne 3x (00100000).
- Pretože v slove DNES nie je žiadny opakujúci sa znak, budeme predpokladať, že tento opakujúci sa znak je medzera.
- Rozdelíme si slovo na jednotlivé znaky a ich bity:
```
D - 01000100
  - 00100000
N - 01001110
  - 00100000
E - xxxxxxxx
  - xxxxxxxx
S - 01010011
  - 00100000
```
- Vieme, že medzera je ``00100000``, preto medzeru rovno doplníme:
```
D - 01000100
  - 00100000
N - 01001110
  - 00100000
E - xxxxxxxx
  - 00100000
S - 01010011
  - 00100000
```
- Hľadáme binárnu reprezentáciu UTF-8 znaku E.
- Zo zadania vieme, že D je v binárnom kóde ``01000100``
- Pretože vieme, že v UTF-8 sú znaky zakódované vždy v postupnosti, kde napríklad: B = U+0042, C = U+0043, tak z toho vyplýva, že E bude o 1 väčšie číslo v desiatkovej sústave ako D
- Našou úlohou je prepočítať aktuálny binárny kód písmena D ``01000100`` na hodnotu v desiatkovej sústave, pričítať +1 a previesť späť na binárny kód
- Prevedieme najprv binárny kód písmena D do desiatkovej sústavy, aby sme zistili, aké predstavuje číslo. 
  Prevod do desiatkovej sústavy spravíme tak, že každé číslo umocníme podľa pozície, na ktorej sa nachádza (1. pozícia = 2 na siedmu)
```
(01000100)₂ = (0 × 2⁷) + (1 × 2⁶) + (0 × 2⁵) + (0 × 2⁴) + (0 × 2³) + (1 × 2²) + (0 × 2¹) + (0 × 2⁰) = (68)₁₀
```
- Vieme, že písmeno D je v desiatkovej sústave 68
- Z toho sme zistili, že E je 69
- Našou úlohou je previesť 69 na binárny kód
- To urobíme tak, že číslo delíme 2 so zvyškom a zvyšky zapisujeme ako jednotlivé čísla binárneho kódu odzadu

| Delenie 2 | Výsledok | Zvyšok | Poradie Bitov |
|-----------|----------|--------|---------------|
| (69)/2    | 34       | 1      | 0             |
| (34)/2    | 17       | 0      | 1             |
| (17)/2    | 8        | 1      | 2             |
| (8)/2     | 4        | 0      | 3             |
| (4)/2     | 2        | 0      | 4             |
| (2)/2     | 1        | 0      | 5             |
| (1)/2     | 0        | 1      | 6             |

- Výsledný binárny kód je: ``1000101``
- Vieme teda, že:
```
D - 01000100
  - 00100000
N - 01001110
  - 00100000
E - 1000101
  - 00100000
S - 01010011
  - 00100000
```
- Pretože chceme 64 bitov a jediný znak E nemá 8 bitov, aplikujeme tzv. byte padding, čo je doplnenie čísla zľava nulami (0) tak, aby    bolo zarovnané na určitú dĺžku (v tomto prípade 8 bitov)
```
D - 01000100
  - 00100000
N - 01001110
  - 00100000
E - 01000101
  - 00100000
S - 01010011
  - 00100000
```

### Riešenie

Kód, ktorý bol použitý k zakódovaniu slova ``D N E S`` je binárny kód, jeho kompletné znenie vyzerá takto:

```
01000100 00100000 01001110 00100000 01000101 00100000 01010011 00100000
```