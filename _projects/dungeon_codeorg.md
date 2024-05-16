---
layout: post
title: "Dungeon"
category: "codeorg"
order: 4
---

# Program "Dungeon"

Hra probíhá v kolech a funguje následujícím způsobem:

1. Hráč se pohybuje v jednoduchém dungeonu se třemi pozicemi
2. Nejprve musí jít na západ natěžit zlato
3. Po každé těžbě se musí vrátit odnést zlato do města (uprostřed) a pak zase může těžit
4. Když má dost zlata, tak může nakoupit meč
5. Na východě jsou Orkové. Pokud na ně hráč zaútočí a má meč, tak vyhrál. Jinak prohraje.

## Logika změny obrazovky

Pro přechod mezi obrazovkami každé přidělíme index a vytvoříme čtyři pole - pro každý směr pohybu jedno. Káždé z těcho polí bude mít počet prvků roven počtu obrazovek.

![Diagram_obrazovek_dungeon](/images/dungeon_diagram.png)

Začínáme na indexu 0 <=> na obrazovce 0. Z této obrazovky se můžeme posunout pouze v pravo. Tímto pohybem se dostaneme na obrazovku 1 <=> index nastavíme na 1. Z obrázku je to zřejmé. Nyní je potřeba zakódovat tuto informaci pomocí polí, abychom s ní pohli dále pracovat.

Z indexu 0 se pohybem dostaneme do indexu 1. Nastavíme tedy nultý prvek pole _right_ na 1. Nulté prvky v ostatních polích nastavíme na -1, protože se nemáme kam posunout.

```js
let index = 0;

const left = [-1];
const right = [1];
const up = [-1];
const down = [-1];
```

Zajímavější situace nastává u obrazovky 1. Z obrázku je patrné, že je možné posunout se do všech čtyřech směrů. Nastavíme tedy každému z polí na indexu 1 obrazovku, na kterou je možné se posunout.

- V levo => 0
- V pravo => 2
- Nahoru => 4
- Dolů => 6

```js
const left = [-1, 0];
const right = [1, 2];
const up = [-1, 4];
const down = [-1, 6];
```

Dále pokračujeme s obrazovkou s indexem 2, pak 3... až 6. Tímto způsobem nenaplníme všechna pole.

```js
const left = [-1, 0, 1, 2, -1, -1, -1];
const right = [1, 2, 3, -1, -1, -1, -1];
const up = [-1, 4, -1, 5, -1, -1, 1];
const down = [-1, 6, -1, -1, 1, 3, -1];
```

Na začátku tedy zobrazíme uživateli pouze šipku doprava. V jeho dalším tahu všechny čtyři šipky. Jestli máme šipku skrýt nebo zobrazit zjistíme velmi jednoduše:

```js
if (left[index] == -1) {
  hideElement("leftButton");
} else {
  showElement("leftButton");
}
if (right[index] == -1) {
  hideElement("rightButton");
} else {
  showElement("rightButton");
}
if (up[index] == -1) {
  hideElement("upButton");
} else {
  showElement("upButton");
}
if (down[index] == -1) {
  hideElement("downButton");
} else {
  showElement("downButton");
}
```

## Výchozí verze

[Dungeon - codeorg](https://studio.code.org/projects/applab/vIsbWwNQW8jfWnvNfDna67jgp1qItTw7JRT4A5yCft8)

## Rozšíření

Zkuste program rozšířit:

- Přidejte zobrazení aktuálního zlata, které má hráč natěženo a také dejte nahoru jméno lokace.
- Přidejte zobrazení seznamu věcí, které má aktuálně u sebe.
- Přidejte do hry počet životů hráče. Pokud prohraje souboj, pak mu život odeberte a dejte do výchozí lokace.
- Po poražení Orků přidejte hráčovi do inventáře "Kouzlo". Přidejte lokaci "hluboký les" s čarodějnicí, kterou jde porazit pouze kouzlem.
- Zkuste se pobavit s chatGPT, aby vám nabídl vhodné rozšíření hry
