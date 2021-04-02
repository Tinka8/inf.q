## Úloha 2

### Zadanie

Kód 0100110101000001010101000101010101010010 (40 bitov) obsahuje prvé písmená zo slova MATURANT. 
O aký kód ide, zdôvodnite a dopíšte chýbajúce bity.

### Postup

- Vieme, že vstupný kód má 40 bitov a obsahuje začiatok slova MATURANT.
- Vieme, že každé písmeno je v UTF-8 reprezentované 8 bitmi
- Takže vieme, že 40 bitov predstavuje 5 písmen (40 / 8 = 5)
- Najprv si rozdelíme vstupný kód po 8 bitoch
```
01001101 01000001 01010100 01010101 01010010
```
- Tento kód reprezentuje znaky MATUR a chýbajú nám znaky ANT:
```
M - 01001101
A - 01000001
T - 01010100
U - 01010101
R - 01010010
A -
N -
T -
```
- Pretože znaky "A" a "T" už poznáme zo zadania, doplníme ich:
```
M - 01001101
A - 01000001
T - 01010100
U - 01010101
R - 01010010
A - 01000001
N -
T - 01010100
```
- Zostáva nám určiť binárnu reprezentáciu UTF-8 znaku "N"
- Zo zadania vieme, že M je v binárnom kóde ``01001101``
- Pretože vieme, že v UTF-8 sú znaky zakódované vždy v postupnosti, kde napríklad: B = U+0042, C = U+0043, tak z toho vyplýva, že N bude o 1 väčšie číslo v desiatkovej sústave ako M
- Našou úlohou je prepočítať aktuálny binárny kód M ``01001101`` na hodnotu v desiatkovej sústave, pripočítať +1 a previesť späť na binárny kód
- Prevedieme najskôr binárny kód M do desiatkovej sústavy, aby sme zistili, aké predstavuje číslo. Prevod do desiatkovej sústavy spravíme tak, že každé číslo umocníme podľa pozície, na ktorej sa nachádza (1. pozícia = 2 na siedmu)
```
(01001101)₂ = (0 × 2⁷) + (1 × 2⁶) + (0 × 2⁵) + (0 × 2⁴) + (1 × 2³) + (1 × 2²) + (0 × 2¹) + (1 × 2⁰) = (77)₁₀
```
- Vieme teda, že M je v desiatkovej sústave 77
- Z toho zistíme, že N je 78
- Našou úlohou je previesť 78 na binárny kód
- To urobíme tak, že číslo delíme 2 so zvyškom a zvyšky zapisujeme ako jednotlivé čísla binárneho kódu odzadu

| Delenie 2 | Výsledok | Zvyšok | Poradie Bitov |
|-----------|----------|--------|---------------|
| (78)/2    | 39       | 0      | 0             |
| (39)/2    | 19       | 1      | 1             |
| (19)/2    | 9        | 1      | 2             |
| (9)/2     | 4        | 1      | 3             |
| (4)/2     | 2        | 0      | 4             |
| (2)/2     | 1        | 0      | 5             |
| (1)/2     | 0        | 1      | 6             |

- Výsledný binárny kód je: ``1001110``
```
M - 01001101
A - 01000001
T - 01010100
U - 01010101
R - 01010010
A - 01000001
N - 1001110
T - 01010100
```
- Pretože všetky znaky majú 8 bitov, aplikujeme tzv. byte padding, čo je doplnenie čísla zľava nulami (0) tak, aby bylo zarovnané na určitú dĺžku (v tomto prípade 8 bitov)
```
M - 01001101
A - 01000001
T - 01010100
U - 01010101
R - 01010010
A - 01000001
N - 01001110
T - 01010100
```

### Riešenie

Kód, ktorý byl použitý k zakódovaniu slova ``MATURANT`` je binárny kód a kompletný binárny kód vyzerá nasledovne:

```
01001101 01000001 01010100 01010101 01010010 01000001 01001110 01010100
```