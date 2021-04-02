## Úloha 3

### Zadanie

V schéme je zakódovaný obrázok. Vyhodnoťte použitý kód, diskutujte o možnom vzhľade obrázka,
jeho farbách, veľkosti. 
Schéma:

```
10000011
01111101
01010101
01111101
01000101
01111101
10000011
```

### Postup

- Vieme, že zadaný binárny kód je obrázok
- Vieme, že zadaný binárny kód je relatívne krátky, preto zrejme obsahuje 1-bitový obrázok
- 1-bitový obrázok je obrázok, ktorý má dve možné farby (0 = biela, 1 = čierna). Analogicky k tomu, napríklad 2-bitový obrázok by mal 4 možné farby (00, 01, 10, 11), 3-bitový by mal 8 farieb atd.
- Každé číslo v bitovej reprezentácii obrázka prevedieme na čierny alebo biely pixel, podľa toho, či je na jeho pozícii 1 alebo 0

### Riešenie 

![binary image](./uloha3.png "Binarni obrazek")

### Pro diskuzi o velikosti a barvách

Pokud by zadaný kód reprezentoval třeba dvoubitový obrázek (což by mohl, to by všechno záleželo na metadatech obrázku, kde tato informace má být uložena). 