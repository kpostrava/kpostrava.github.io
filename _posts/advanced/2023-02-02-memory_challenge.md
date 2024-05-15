---
layout: post
title:  "Memory challenge"
---
# Program "Memory challenge"

1.  [Code.org](https://studio.code.org/projects/applab/mbu_rC06TSKqfiraKegwSNAtKuePJ-c8Ivh79xyE7-I) verze hry

Hra probíhá v kolech a funguje následujícím způsobem:
1. Hráč si má za pět sekund zapamatovat pět čísel.
2. Pak je má vepsat do textboxu: 
  a. Pokud uhodne, tak další kolo si bude muset zkusit zapamatovat šest čísel za šest sekund.
  b. Pokud neuspěje, tak se mu ukážou čtyři čísla na čtyři sekundy.
3. Hríč vyhraje, pokud si v pěti kolech zapamatuje číslo správně.
6. Hráč prohraje pokud dříve pětkrát číslo napíše špatně.
 
Tzn. hra má maximálně devět kol, protože pak už hráč musí buď prohrát nebo vyhrát.

## Čekání
V programu jsou využity dva triky, které si zaslouží trochu okomentovat. První z nich je čekání. JavaScript neobsahuje přímo funkci `sleep`, takže je nutné si ji naimplementovat. Využili jsme `sleep` funkci ze [StackOverflow](https://stackoverflow.com/a/9748670/2091247):
```javascript
function sleep(delay) {
    var start = new Date().getTime();
    while (new Date().getTime() < start + delay);
}
```
Tuto funkci pak v kódu můžete zavolat třeba takto:
```javascript
console.log("Chtel jsem neco rict, ale nemuzu si vzpomenout ...");
sleep(2000);
console.log("Uz vim! Krouzek programovani je skvely!");
```
Takto bude JavaScript mezi oběma výpisy do konzole chvilku váhat. Přesněji mezi výpisy bude čekat 2 sekundy.

## Generování čísel
V programu potřebujeme generovat náhodné čísla s požadovaným počtem číslic. Požadovaný počet číslic nám udává proměnná `digitNumber`. V podstatě existují dva přístupy k tomuto problému. První iterativní algoritmus generuje v cyklu vždy jednu číslici, kterou přičteme k výslednému číslu a následně násobíme desíti.
```javascript
  number = 0;
  for (var i = 0; i <= digitNumber; i++) {
    number = number * 10;
    number = number + randomNumber(0,9);
  }  
```
Druhý přístup je vypočítat interval, ze kterého se mají čísla vybírat. Kupříkladu pro dvou ciferné čísla budeme náhodně vybírat čísla z intervalu 10 - 99. Obě strany intervalu se dají vypočítat jako 10^1 až 10^2 - 1. V JavaScriptu pak generování čísla bude probíhat takto:
```javascript
number = randomNumber(Math.pow(10,digitNumber), Math.pow(10, digitNumber + 1) - 1);
```
