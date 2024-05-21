---
layout: post
title: Ovládací prvky na HTML stránkách
category: "html"
order: 2
---

# Ovládácí prvky na HTML stránce

Dosud jsme používali pro tvorbu grafických aplikací rozhraní App lab. Měli jsme tak k dispozici spoustu užitečných funckí pro manipulaci s ovládacími prvky aplikace.

```js
onEvent("id", "click", function () {});

setText("id", "text");

getText("id");

showElement("id");

setProperty("id", "width", 100);
```

Vytváření, rozmístění a stylování prvků jsme prováděli rovněž v grafickém prostředí. Nyní musíme strukturu našeho grafického rozhrání vytvořit pomocí HTML tagů. Základní struktura každé HTML stránky je složena z hlavičky - `<head>` a těla `<body>`. Obsah, který má být zobrazen uživateli, se vkládá do tagu `<body>`.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Skvělá aplikace</title>
  </head>
  <body>
    <!-- TEĎ tě zajímá jen tento prostor -->
  </body>
</html>
```

Pro zobrazení textu můžeme použít dvou základních prvků:

- `<span>` - Vhodný pro krátké textu
- `<p>` - "paragraph" - Celý odstavec

Text pak jednoduše stačí napsat mezi otevírací tag `<p>` a zavírací tag `</p>`.

```html
<body>
  <p id="muj_dlouhy_text_1">mooooooooooooc dlouhý text</p>

  <span id="pozdrav">ahoj</span>
</body>
```

Tlačítko vytvoříme pomocí tagu `<button>`. Přidáme mu atribut `onclick` a nastavíme jej na funkci, která se má zavolat při jeho stisknutí.

```html
<button onclick="start()">START</button>
```

Hodnotu od uživatele můžeme získat pomocí tagu `<input>`. `<input />` má teto zrácený zápis - není třeba otevíracího a zavíraího tagu.

```html
<input id="uzivatelsky_vstup" value="vychozi hodnota" />
```

Když teď přecházíme na technologie HTML, CSS, JS. Bohužel zde již nemáme k dispozici předpřipravené funkce pro práci s grafickým rozhraním. Musíme si je naimplementovat sami. Interakci s prvky HTML stránky označujeme jako DOM (document object model) manipulaci.

Javascript píšeme do tagu `<script>`.

```html
<script>
  console.log("Ahoj z JS!"); // Vypíše text do konzole
</script>
```

> 💡 Otevřte si v prohlížeči "nástroje pro vývojáře". Zejména konzoli.

### Vybrání prvku

```js
document.getElementById("id"); // Vybrání elementu podle id

document.querySelector(".class"); //.class, #id, element, - Vybrání podle CSS selectoru
```

### Vložení textu do prvku

```js
document.getElementById("pozdrav").innerText = "čau";

// Ekvivalent k setText("id", "text") z prostředí App lab
```

### Vytvoření funkce

Pokud chceme sputit určitý kód při zmáčknutí tlačítka, musíme jej "zabalit" do funkce. Máme dva možné zápisy. Pro naše účely, je druhý způsob vhodnější.

```js
function start() {
  console.log("start");
}

const start = () => {
  console.log("start");
};
```

### Získání vstupu od uživatele

```js
const value = document.getElementById("uzivatelsky_vstup").value;
console.log(value);
```

### Změna vlastností prvku

```js
const element = document.getElementById("id_prvku"); // vybereme prvek

element.classList.add("nazev_tridy"); // přidání třídy prvku
element.classList.remove("nazev_tridy"); // přidání třídy prvku
element.classList.toggle("nazev_tridy"); // pokud prvek třídu má - odebere se, pokud nemá - přidá se

element.style.backgroundColor = "red"; // Změna barvy pozadí
element.style.left = "200px"; // Vzdálenost od levého okraje
element.style.right = "10px"; // Vzdálenost od pravého okraje
element.style.bottom = "10px"; // Vzdálenost od spodního okraje
element.style.top = "10px"; // Vzdálenost od horního okraje
```

### Náhodné číslo

```js
const prvni_nahodne_cislo = Math.floor(Math.random() * 10); // <0, 9>

const druhe_nahodne_cislo = Math.floor(Math.random() * 10 + 1); // <1, 10>
```

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
