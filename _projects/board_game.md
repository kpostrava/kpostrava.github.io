---
layout: post
title: "Board game"
category: "html"
order: 4
---

# Board game

Nejprve si forkněte z [githubu](https://github.com/kpostrava/board_game) repozitář s výchozím bodem k tomuto projektu.

## Popis programu

Základem celé aplikace je dvourozměrné pole `game_board` (10x10). K jednomu prvku pole přistoupíme s pomocí dvou hranatých závorek. Tzn. například:

```JavaScript
game_board[1][0] = 10
```

uloží na první řádek a nultý sloupec hodnotu 10. Jednotlivé políčka v `game_board` jsou nastavená na hodnotu nula nebo jedna. Hodnota jedna má vyjadřovat, že se na dané pozici nachází překážka.

Dále se v programu nachází proměnné `x` a `y`, které uchovávají pozici hráče. Hráč je ovládán šipkami a posun v poli je implementován ve funkci `moveCircle`.

## Vytvoření herní mapy

Potřebujeme projít každý prvkek v dvourrozměrném poli, které reprezentuje herní mapu. Jelikož známe velikost tohoto pole, můžeme použít cyklus `for`.

```js
for (let index = 0; index < game_board.length; index++) {
  // něco udělej
}
```

Jak můžete vidět, udáváme cyklu `for` při jeho vytváření tři údaje.

- `let index = 0` - vytvoříme si novou proměnnou, do které ukládáme průběžný stav cyklu.
- `index < game_board.length` - podmínka za jaké má cyklus pokračovat
- `index++` - na konci každého cyklu zvýší hodnotu `index` o jedna (index = index + 1)

Ukažme si to na příkladu, chceme 10x vypsat "ahoj".

```js
for (let index = 0; index < 10; index++) {
  console.log("ahoj");
}
```

Nyní zkusíme tento cyklus použít k vypsání prvků v poli. Nejdříve si vypíšeme pouze jednotlivé řádky.

```js
for (let radek = 0; radek < game_board.length; radek++) {
  console.log(game_board[radek]);
}
```

Cheme ale vypsat každý prvek zvlášť. Použijeme tedy druhý `for` pro vypsání prvků z každého řádku.

```js
for (let radek = 0; radek < game_board.length; radek++) {
  for (let sloupec = 0; sloupec < game_board.length; sloupec++) {
    console.log(game_board[radek][sloupec]);
  }
}
```

Herní mapu reprezentujeme, jako HTML tabulku. Stejně jako naše 2d pole je tabulka složena z řádků a sloupců. Konkrétní prvek v poli nazýváme "buňka".

```js
const radek = document.createElement("tr");
const bunka = document.createElement("td"); // skládáním za sebe tvoříme sloupce
```

HTML elementům můžeme přidávat vlastnosti. Třídu můžeme přidat pomocí metody `classList.add()`.

```js
square.classList.add("square");
```

Vytvoření elementu však nestačí pro jeho zobrazení. Na stránku ho přidáme pomocí metody `appendChild()`;

```js
bunka.appendChild(square);
```

Herní mapa je čtvercová => počet řádků je roven počtu sloupců. S těmito znalostmi jsme nyní schopni vytvořit herní mapu.

```js
for (let radek = 0; radek < game_board.length; radek++) {
  const radek_tabulky = document.createElement("tr"); // Vytvoříme nový řádek tabulky

  for (let sloupec = 0; sloupec < game_board.length; sloupec++) {
    const bunka_tabulky = document.createElement("td"); // Vytvoříme novou buňku tabulky

    radek_tabulky.appendChild(cell); // Přidáme novou buňku do řádku tabulky

    if (game_board[i][j] == 1) {
      // Pokud se na této pozici nachází překážka

      const square = document.createElement("div"); // Vytvoříme element div, který slouží jako zábrana

      square.classList.add("square"); // Přidáme divu třídu pro pozdější nastavení jeho vlastností

      cell.appendChild(square); // Přidáme div do buňky tabulky
    }
  }
  board.appendChild(row); // přidáme celý řádek do tabulky
}
```

## Úkoly

U této verze zkuste následující úkoly:

- Ošetřete v metodě `moveCircle` pohyb hráče tak, aby nemohl vstoupit na pole s překážkou (tzn. `game_board` je na dané pozici nastaven na jedna)
- Změňte obrázek překážky z modrého čtverce na nějaký obrázek (např. stěna)
- Změňte obrázek hráče z červeného kruhu na nějaký obrázek (např. auto, osoba zvrchu)
- Přidejte do `game_board` novou hodnotu 2, která bude reprezentovat nějakou odměnu, kterou chceme sebrat. Upravte `createBoard()` funkci, aby se odměny zobrazovaly v HTML.
- Napište do `moveCircle` logiku, která bude kontrolovat, zda-li hráč nevstoupil na pole s odměnou. Pokud vstoupí na pole s odměnou provede následující:
  1. Zvýší skóre hráče.
  2. Odstraní odměnu z `game_board`. Tzn. nastaví dané pole na 0 a v HTML odebere obrázek odměny.

# NPC

Nyní zkusíme do našeho programu přidat NPC (non-playable character), který bude hráče pronásledovat. K tomu potřebujeme několik změn v našem programu:

1. Proměnné, které budou udávat pozici NPC v programu.
2. Funkci, která se bude spouštět v pravidelných intervalech a která bude posunovat pozici NPC.
3. Funkci, která bude schopna v našem `game_board` nalézt nejkratší cestu od hráče k NPC.

## Spouštění v pravidelných intervalech

Vytvořte si funkci `posunNPC`, kde bude docházet k posunu NPC a také se bude kontrolovat, zda-li NPC není na stejném poli s hráčem. Tato funkce se bude v JavaScriptu volat spomocí funkce `setInterval`. Takže to bude vypadat nějak takto:

```JavaScript
function posunNPC() {
  // dopiště vlastní logiku
  console.log("Function executed every second.");
}
setInterval(myFunction, 1000); // spouštěno každou sekundu
```

## Hledání nejkratší cesty

Pro hledání nejkratší cesty využijeme algoritmus breath first search (BFS). Názorné vysvětlení algoritmu je možné vidět třeba [zde](https://www.youtube.com/watch?v=T_m27bhVQQQ&t=131s). V lorem ipsum týmu na Repl.it je nyní program, který hledá nejkratší cestu v bludišti. Toto hledání realizuje funkce `shortestPathSearch`. Zkusme se podrobně podívat na jednotlivé parametry funkce:

- `game_board` - dvourozměrné pole, tak jak jej máme v předchozím programu.
- `xp`, `yp` - souřadnice hráče
- `x_npc`, `y_npc` - souřadnice NPC

<script src="https://gist.github.com/RadimBaca/aee7196ba05f3d214862f99d8e10950b.js"></script>

## Import do souboru

Pro zpřehlednění programu můžeme hledání nejkratší cesty (funkci shortestPathSearch) přenést do samostatného souboru a v index.js ji naimportovat. Příklad toho jak se to v JavaScriptu dělá můžete vidět v následující [otázce na StackOverflow](https://stackoverflow.com/questions/56336729/how-can-i-import-functions-from-an-other-javascript-file) popřípadě si můžete přečíst delší vysvětlení exportu a importu v JavaScriptu [zde](https://javascript.info/import-export).

# Projects

- [Oli](https://a9832060-26c8-4de7-ae72-72d48ee97a2a-00-2trpl9iqhy9de.kirk.repl.co/)
- [Marek](https://67bddb21-684e-459a-bc84-700143735516-00-2z1jsm83dcxin.picard.replit.dev/)
- [Vinca](https://b749510d-4acf-447b-ad59-4263eeec8acf-00-yzju7i5noigg.spock.replit.dev/)
- [Štěpán](https://d52cf779-cb95-4456-855b-d14e5fb2909e-00-22du8e5dvf147.spock.replit.dev/)
- [Dominik](https://7bf0ad76-008d-44a5-9f2e-45f1186bb280-00-1n6rw7vbrqagr.spock.replit.dev/)

[Formulář pro hodnocení](https://docs.google.com/forms/d/e/1FAIpQLSfsBAm0frYEt1yUAt_QfjHXDDR4fXaRNIVSg_iLYyodVk58Yg/viewform?usp=sf_link) výsledné aplikace.
