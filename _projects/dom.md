---
layout: post
title: Ovládací prvky na HTML stránkách
category: "html"
order: 2
---

# Ovládácí prvky na HTML stránce

Dosud jsme používali pro tvorbu grafických aplikací rozhraní applab. Měli jsme tak k dispozici spoustu užitečných funckí pro manipulaci s ovládacími prvky aplikace.

```js
onEvent("id", "click", function () {});

setText("id", "text");

getText("id");

showElement("id");

setProperty("id", "width", 100);
```

Vytváření, rozmístění a stylování prvků jsme prováděli rovněž v grafickém prostředí. Nyní musíme strukturu našeho grafického rozhrání vytvořit pomocí HTML tagů. Základní struktura každé HTML stránky je složena z hlavičky - `<head>` a těla `<body>`. Obsah, který má být zobrazen uživateli se vkládá do tagu `<body>`.

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

💡 Otevřte si v prohlížeči "nástroje pro vývojáře". Zejména konzoli.

### Vybrání prvku

```js
document.getElementById("id"); // Vybrání elementu podle id

document.querySelector(".class"); //.class, #id, element, - Vybrání podle css selectoru
```

### Vložení textu do prvku

```js
document.getElementById("pozdrav").innerText = "čau";

// Ekvivalent k setText("id", "text");
```

### Vytvoření funkce

Pokud chceme sputit určitý kód při zmáčknutí tlačítka, musíme jej "zabalit" do funkce. Máme dva možné zápisy.

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
const nahodne_cislo = Math.floor(Math.random() * 10); // <0, 9>

const nahodne_cislo = Math.floor(Math.random() * 10 + 1); // <1, 10>
```

> **Úkol 1:**
> Předělejte projekt [malá nábosilka](/project/nabosilka) z prostředí codeorg do HTML, CSS, JS.

> **Úkol 2:**
> Předělejte projekt [Non hazard game](/project/non_hazard) z prostředí codeorg do HTML, CSS, JS. Pokud se vám nechce předělávat starý projekt, můžete si vymyslet něco úplně nového!
