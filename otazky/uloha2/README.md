## Uloha 2

### Zadání

Kód 0100110101000001010101000101010101010010 (40 bitov) obsahuje prvé písmená zo slova MATURANT. O aký kód ide, zdôvodnite a dopíšte chýbajúce bity.

### Postup

- Víme, že vstupní kód má 40 bitů a obsahuje začátek slova MATURANT.
- Víme, že každé písmeno je v UTF-8 reprezentováno 8 bity
- Víme tedy, že 40 bitů představuje 5 písmen (40 / 8 = 5)
- Rozdělíme si nejprve vstupní kód po 8 bitech
```
01001101 01000001 01010100 01010101 01010010
```
- Tento kód tedy reprezentuje znaky MATUR a schází nám znaky ANT:
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
- Protože znaky "A" a "T" nám jsou již známé ze zadání, můžeme je rovnou doplnit
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
- Zbývá nám tedy určit binární reprezentaci UTF-8 znaku "N"
- Ze zadání víme, že M je v binárním kódu ``01001101``
- Protože víme, že v UTF-8 jsou znaky zakódované vždy v posloupnosti, kdy třeba B = U+0042, C = U+0043, tak z toho vyplívá, že E bude o 1 větší číslo v desítkové soustavě než D
- Naším úkolem je tedy přepočítat aktuální binární kód M ``01001101`` na hodnotu v desítkové soustavě, přičíst +1 a převést zpět na binární kód
- Převedeme tedy nejdřív binární kód M do desítkové soustavy, abychom zjistili, jaké představuje číslo. Převádění do desítkové soustavy provádíme tak, že každé číslo umocníme podle pozice, na které se nachází (1. pozice = 2 na sedmou)
```
(01001101)₂ = (0 × 2⁷) + (1 × 2⁶) + (0 × 2⁵) + (0 × 2⁴) + (1 × 2³) + (1 × 2²) + (0 × 2¹) + (1 × 2⁰) = (77)₁₀
```
- Víme tedy, že M je v desítkové soustavě 77
- Z toho zjišťujeme, že N je 78
- Naším úkolem je tedy převést 78 na binární kód
- To uděláme tak, že číslo dělíme 2 se zbytkem a zbytky zapisujeme jako jednotlivá čísla binárního kódu odzadu

| Deleni 2 | Vysledek | Zbytek | Poradi Bitu |
|----------|----------|--------|-------------|
| (78)/2   | 39       | 0      | 0           |
| (39)/2   | 19       | 1      | 1           |
| (19)/2   | 9        | 1      | 2           |
| (9)/2    | 4        | 1      | 3           |
| (4)/2    | 2        | 0      | 4           |
| (2)/2    | 1        | 0      | 5           |
| (1)/2    | 0        | 1      | 6           |

- Výsledný binární kód je tedy ``1001110``
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
- Protože všechny znaky mají 8 bitů, aplikujeme tzv. byte padding. Což je doplnění čísla zleva nulami (0) tak, aby bylo zarovnané na nějakou délku (v tomto případě 8 bitů)
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

### Řešení

Kód, který byl použitý k zakódování slova ``MATURANT`` je binární kód a kompletní binární kód vypadá takto:

```
01001101 01000001 01010100 01010101 01010010 01000001 01001110 01010100
```