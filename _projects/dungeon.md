---
layout: post
title: "Dungeon"
category: "html"
order: 3
---

# Program "Dungeon"

Nejprve se [připojte do Lorem Ipsum týmu](https://replit.com/teams/join/xvtsjzaadrqmanaknpncvlanyelasxgw-lorem-ipsum-team) na Repl.it, kde by jste měli nalézt HTML5 verzi Dungeonu. U této verze zkuste následující úkol:

- S pomocí chatGPT změňte rozložení tlačítek, aby se více podobalo rozložení v code.org.
- Implementujte ovládání hry tlačítky klávesnice.
- Vytvořte závěrečnou HTML stránku, která se zobrazí po (ne)výhře.
- Zkuste změnit barevné ladění celé stránky. Opět zkuste svoje změny konzultovat s chatGPT.
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

### Ovládání hry tlačítky klávesnice

Pro ovládání hry tlačítky je potřeba přidat událost přímo na HTML dokument, který reprezentuje stránku. To provedeme následujícím způsobem:

```JavaScript
document.addEventListener("keydown", function(event) { // Handle the keydown event here
	if (event.key === "ArrowUp") { // Kód pro reakci na stisk klávesy šipka nahoru
		console.log("Stisknuta klávesa šipka nahoru");
	}
}
```

Zde je seznam několika klíčových kódů pro šipky:

- Šipka nahoru: `ArrowUp`
- Šipka dolů: `ArrowDown`
- Šipka vlevo: `ArrowLeft`
- Šipka vpravo: `ArrowRight`

## Code.org studentské verze programu

- [Štěpán](https://studio.code.org/projects/applab/1inL4-_LCA1StixR5R8WeBb6Tb5tF8s6aVeF5IurY_A)
- [Štěpán JSON verze](https://studio.code.org/projects/applab/WV2sXQu3mQT6pMGhbU2GDcdULpGN4FFTp-3NGe2usCg)
- [Mikuláš](https://studio.code.org/projects/applab/_3Jqoi4a99BigqIDKwEiDhQRyGZVhUL309LYWasM5_M)
- [Marek](https://studio.code.org/projects/applab/e5tYkt8TbW2a7KjA3LQpee2vhsxRIhhtTxDYW43LjhQ)
- [Artem](https://studio.code.org/projects/applab/WzlCkoZl1dB58Zjg3fKFoX1ChARbtxzhFFvJffITgPc)
