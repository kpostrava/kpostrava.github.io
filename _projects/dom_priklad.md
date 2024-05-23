---
layout: post
title: Jednoduchá aplikace
category: "html"
order: 3
---

### Jednoduchá aplikace

Pojďeme využít nově nabyté vědomosti k vytvoření jednoduché aplikace. Vytvoříme webovou stránku se dvěma číselnými vstupy, tlačítkem a textem. Uživatel zadá rozsah hodnot a my mu vygenerujeme náhodné číslo v tomto rozsahu.

Jako první věc si musíme otevřít vývojé prostředí - vscode. Vytovříme si nový soubor - `index.html`. Poté si vytvoříme sturkturu stránky. Ve vývojovém prostředí vscode nám stačí napsat "!" a stisknout klávesu enter.

<h5 a><strong><code>index.html</code></strong></h5>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body></body>
</html>
```

Pokud chceme přidat statické stránce logiku, potřebujeme javascript. Pro přehlednost si vytvoříme nový soubor - `script.js`. Musíme také přidat `<script>` tag do našeho `index.html`, tím tyto dva soubory propojíme.

<h5 a><strong><code>index.html</code></strong></h5>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <!-- Grafické rozhraní programu půjde zde -->
  </body>
</html>
<script src="script.js"></script>
```

<h5 a><strong><code>script.js</code></strong></h5>

```js
// Logika programu půjde zde
```

Máme vytvořenou základní strukturu. Nyní můžeme vytvořit grafické rozhraní. Začneme uživatelskými vstupy - `<input>`.

```html
<input id="minimum" value="0" />

<input id="maximum" value="100" />
```

Dále potřebujeme tlačítko, kterým bude uživatel generovat nové náhodné číslo.

```html
<button onclick="generuj()">GENERUJ!</button>
```

Pro zobrazení náhodného čísla uživateli si vytvoříme prvek `<span>`. Výchozí hodnotu nastavíme na libovolný text.

```html
<span id="zobrazeni_cisla">---------Vítejte---------</span>
```

Přidáme všechny tyto prvky na naši stránku.

<h5 a><strong><code>index.html</code></strong></h5>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <span id="zobrazeni_cisla">---------Vítejte---------</span>

    <input id="minimum" value="0" />
    <input id="maximum" value="100" />

    <button onclick="generuj()">GENERUJ!</button>
  </body>
</html>
<script src="script.js"></script>
```

Naše stránka by měla vypadat takto.
![screenshot](/images/dom/ui.png)

Pojďme vytvořit v javascriptu funkci pro generování čísel.

<h5 a><strong><code>script.js</code></strong></h5>

```js
const generuj = () => {};
```

Potřebuje zjistit rozsah ve kterém máme generovat čísla. Získáme hodnoty od uživatele z jednotlivých textových polí. Tyto hodnoty musíme převést na čísla.

```js
let min = Number(document.getElementById("minimum").value);
let max = Number(document.getElementById("maximum").value);
```

Nyní máme potřebné informace k vygenerování náhodného čísla.

```js
let nahodne_cislo = Math.floor(Math.random() * (max - min + 1)) + min;
```

Nyní už jsem stačí toto číslo vypsat na obrazovku.

```js
document.getElementById("zobrazeni_cisla").innerText = nahodne_cislo;
```

Když to dáme dohromady, získáme celou funkci.

<h5 a><strong><code>script.js</code></strong></h5>

```js
const generuj = () => {
  let min = Number(document.getElementById("minimum").value);
  let max = Number(document.getElementById("maximum").value);

  let nahodne_cislo = Math.floor(Math.random() * (max - min + 1)) + min;

  document.getElementById("zobrazeni_cisla").innerText = nahodne_cislo;
};
```

> **Úkol 1:**
> Přidejte další `<span>` a vypište vylosované číslo do všech najednou.

> **Úkol 2:**
> Pro každý `<span>` generujte jiné náhodné číslo. Mějte minimálne tři.

Když máme hotovou funkcionalitu, můžeme se pustit do vzhledu. Ke stylování nám slouží CSS - kaskádové styly. Vytvoříme si pro ně nový soubor `style.css`.

<h5 a><strong><code>style.css</code></strong></h5>

```css
/* tady upravujeme vzhled */
```

Opět musíme soubor spojit s našim `index.html`. U CSS toto provádíme v hlavičce stránky.

<h5 a><strong><code>index.html</code></strong></h5>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>

    <!-- Připojení css -->
    <link rel="stylesheet" type="text/css" href="style.css" />
  </head>
  <body>
    <span id="zobrazeni_cisla">---------Vítejte---------</span>

    <input id="minimum" value="0" />
    <input id="maximum" value="100" />

    <button onclick="generuj()">GENERUJ!</button>
  </body>
</html>
<script src="script.js"></script>
```

CSS nabízí obrovské množství různých nastavení, ukážeme si jen pár příkladů. Nastavení, která vám pochybí najdete snadno na internetu.

<h5 a><strong><code>style.css</code></strong></h5>

```css
body {
  background: gray;
  text-align: center;
}

button {
  background: orange;
  color: slate;
  width: 200px;
  height: 80px;
  border: 10px solid green;
  border-radius: 10px;
}

input {
  height: 80px;
}

span {
  color: red;
  font-size: 2rem;
}
```

Po přidání CSS naše stránka vypadá takto.
![screenshot](/images/dom/css.png)

> **Úkol 3:**
> S pomocí internetu změňte vzhled stránky, aby se vám líbila.

Nyní si ověřte své znalosti HTML, CSS a JS předěláním straších projektů z applabu.

> **Úkol 4:**
> Předělejte projekt [malá nábosilka](/project/nabosilka) z prostředí codeorg do HTML, CSS, JS.

> **Úkol 5:**
> Předělejte projekt [Non hazard game](/project/non_hazard) z prostředí codeorg do HTML, CSS, JS. Pokud se vám nechce předělávat starý projekt, můžete si vymyslet něco úplně nového!
