---
layout: post
title:  "Dungeon"
---
# Program "Dungeon"

1. [Code.org](https://studio.code.org/projects/applab/vIsbWwNQW8jfWnvNfDna67jgp1qItTw7JRT4A5yCft8) verze

Hra probíhá v kolech a funguje následujícím způsobem:
1. Hráč se pohybuje v jednoduchém dungeonu se třemi pozicemi
2. Nejprve musí jít na západ natěžit zlato
3. Po každé těžbě se musí vrátit odnést zlato do města (uprostřed) a pak zase může těžit
4. Když má dost zlata, tak může nakoupit meč
5. Na východě jsou Orkové. Pokud na ně hráč zaútočí a má meč, tak vyhrál. Jinak prohraje.
 
## Rozšíření
Zkuste program rozšířit:
- Přidejte zobrazení aktuálního zlata, které má hráč natěženo a také dejte nahoru jméno lokace.
- Přidejte do hry počet životů hráče. Pokud prohraje souboj, pak mu život odeberte a dejte do výchozí lokace.
- Po poražení Orků přidejte hráčovi do inventáře "Kouzlo". Přidejte lokaci "hluboký les" s čarodějnicí, kterou jde porazit pouze kouzlem.
- Zkuste se pobavit s chatGPT, aby vám nabídl vhodné rozšíření hry

## Repl.it verze
Nejprve se [připojte do Lorem Ipsum týmu](https://replit.com/teams/join/xvtsjzaadrqmanaknpncvlanyelasxgw-lorem-ipsum-team) na Repl.it, kde by jste měli nalézt HTML5 verzi Dungeonu. U této verze zkuste následující úkol:
- S pomocí chatGPT změňte rozložení tlačítek, aby se více podobalo rozložení v code.org. Zkuste si i sami něco nastudovat ke [grid-containeru](https://www.w3schools.com/css/css_grid_container.asp), který by se k tomuto účelu dal využít.
- Vytvořte závěrečnou HTML stránku, která se zobrazí po (ne)výhře.
- Implementujte podobné úkoly jako u Code.org verze.

### Načtení parametru v závěrečné stránce
Pokud vytvoříte závěrečnou HTML stránku, kde budete zobrazovat výsledek souboje, pak jistě budete chtít i předat výsledek souboje. Nejprve tedy v scripts.js přesměrujeme na novou HTML stránku a zároveň přidáme parametr `result`:
```JavaScript
window.location.href = "end.html?result=win";
```
Parametr a jeho hodnotu specifikujeme za otazníkem. Teoreticky může být parametrů více (nicméně zde je jen jeden). Na stránce `end.html` pak parametr načteme v JavaScript kódu následujícím způsobem:
```JavaScript
function getQueryVariable(variable) {
  var query = window.location.search.substring(1);
  var vars = query.split("&");
  for (var i=0;i<vars.length;i++) {
    var pair = vars[i].split("=");
    if (pair[0] == variable) {
      return pair[1];
    }
  } 
}
  
var result = getQueryVariable('result');
```
V proměnné result budeme mít v našem případě hodnotu `win`.

## Code.org studentské verze programu

- [Štěpán](https://studio.code.org/projects/applab/1inL4-_LCA1StixR5R8WeBb6Tb5tF8s6aVeF5IurY_A) 
- [Štěpán JSON verze](https://studio.code.org/projects/applab/WV2sXQu3mQT6pMGhbU2GDcdULpGN4FFTp-3NGe2usCg) 
- [Mikuláš](https://studio.code.org/projects/applab/_3Jqoi4a99BigqIDKwEiDhQRyGZVhUL309LYWasM5_M) 
- [Marek](https://studio.code.org/projects/applab/e5tYkt8TbW2a7KjA3LQpee2vhsxRIhhtTxDYW43LjhQ) 
- [Artem](https://studio.code.org/projects/applab/WzlCkoZl1dB58Zjg3fKFoX1ChARbtxzhFFvJffITgPc) 
