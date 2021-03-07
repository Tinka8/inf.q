## Uloha 1

### Zadání

Slovo DNES má po zakódovaný tvar 01000100000000000100111000000000xxxxxxxxxxxxxxxx0101001100000000 (64 bitov). Rozhodnite, ktorý z bežne používaných kódov bol použitý, doplňte bity za x a zhodnoťte (uveďte výhody a nevýhody použitého kódu).

### Postup

- Víme, že výsledný kód má být 64 bitů a jeho formát je:
```
01000100000000000100111000000000xxxxxxxxxxxxxxxx0101001100000000
```
- Víme, že každé písmeno je představené 8 bity, můžeme si tedy rozdělit celý řetězec ze zadání po 8 znacích

```
01000100 00100000 01001110 00100000 xxxxxxxx xxxxxxxx 01010011 00100000
```
- Víme, že v řetězci se nachází určitě 8 znaků (protože 64 bitů / 8 je 8), a víme ze zadání, že jeden znak se opakuje minimálně 3x (00100000).
- Protože ve slově DNES není žádný opakující se znak, budeme předpokládat, že tento opakující se znak je mezera.
- Rozpadneme si slovo na jednotlivé znaky a jejich bity
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
- Víme, ze mezera je ``00100000``, proto mezeru rovnou muzeme doplnit
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
- Hledáme tedy binární reprezentaci UTF znaku E.
- Ze zadání víme, že D je v binárním kódu ``01000100``
- Protože víme, že v UTF jsou znaky zakódované vždy v posloupnosti, kdy třeba B = U+0042, C = U+0043, tak z toho vyplívá, že E bude o 1 větší číslo v desítkové soustavě než D
- Naším úkolem je tedy přepočítat aktuální binární kód D ``01000100`` na hodnotu v desítkové soustavě, přičíst +1 a převést zpět na binární kód
- Převedeme tedy nejdřív binární kód D do desítkové soustavy, abychom zjistili, jaké představuje číslo. Převádění do desítkové soustavy provádíme tak, že každé číslo umocníme podle pozice, na které se nachází (1. pozice = 2 na sedmou)
```
(01000100)₂ = (0 × 2⁷) + (1 × 2⁶) + (0 × 2⁵) + (0 × 2⁴) + (0 × 2³) + (1 × 2²) + (0 × 2¹) + (0 × 2⁰) = (68)₁₀
```
- Víme tedy, že D je v desítkové soustavě 68
- Z toho zjišťujeme, že E je 69
- Naším úkolem je tedy převést 69 na binární kód
- To uděláme tak, že číslo dělíme 2 se zbytkem a zbytky zapisujeme jako jednotlivá čísla binárního kódu odzadu

| Deleni 2 | Vysledek | Zbytek | Poradi Bitu |
|----------|----------|--------|-------------|
| (69)/2   | 34       | 1      | 0           |
| (34)/2   | 17       | 0      | 1           |
| (17)/2   | 8        | 1      | 2           |
| (8)/2    | 4        | 0      | 3           |
| (4)/2    | 2        | 0      | 4           |
| (2)/2    | 1        | 0      | 5           |
| (1)/2    | 0        | 1      | 6           |

- Výsledný binární kód je tedy ``1000101``
- Nyní tedy víme, že
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
- Protože víme, že chceme 64 bitů, a jediný znak E nemá 8 bitů, aplikujeme tzv. byte padding. Což je doplnění čísla zleva nulami (0) tak, aby bylo zarovnané na nějakou délku (v tomto případě 8 bitů)
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

### Řešení

Kód, který byl použitý k zakódování slova ``D N E S `` je binární kód a kompletní binární kód vypadá takto:

```
01000100 00100000 01001110 00100000 01000101 00100000 01010011 00100000
```