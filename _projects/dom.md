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

Jako první si musíme otevřít vývojé prostředí - vscode. Vytovříme si nový soubor - `index.html`. Poté si vytvoříme sturkturu stránky. Ve vývojovém prostředí vscode nám stačí napsat "!" a stisknout klávesu enter.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Skvělá aplikace</title>
  </head>
  <body>
    <!-- Grafické rozhraní aplikace -->
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

Vytvořený soubor si uložte. HTML soubory můžeme otevírat přimo v prohlížeči. Naše stránka by měla vypadat nějak takto.

![ukazka_stranky](/images/dom/first_page.png)

Tlačítko vytvoříme pomocí tagu `<button>`. Přidáme mu atribut `onclick` a nastavíme jej na funkci, která se má zavolat při jeho stisknutí.

```html
<button onclick="start()">START</button>
```

Hodnotu od uživatele můžeme získat pomocí tagu `<input>`. `<input />` má teto zrácený zápis - není třeba otevíracího a zavíraího tagu.

```html
<input id="uzivatelsky_vstup" value="vychozi hodnota" />
```

Když teď přecházíme na technologie HTML, CSS, JS. Bohužel zde již nemáme k dispozici předpřipravené funkce pro práci s grafickým rozhraním. Musíme si je naimplementovat sami. Interakci s prvky HTML stránky označujeme jako DOM (document object model) manipulaci.

Javascript píšeme do tagu `<script>` a můžeme jej vložit na úplný konec dokumentu.

```html
<script>
  console.log("Ahoj z JS!"); // Vypíše text do konzole
</script>
```

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Skvělá aplikace</title>
  </head>
  <body>
    <!-- Grafické rozhraní aplikace -->
  </body>
</html>

<script>
  console.log("Ahoj z JS!"); // Vypíše text do konzole
</script>
```

Nepostradatelný nástroj každého vývojáře je **konzole**. Tu webovou najdete v nástrojích pro vývojáře. Otevřete je zkratkou `ctrl` + `shift` + `j`. Například konzole ve firefoxu vypadá takto.

![konzole](/images/dom/konzole.png)

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

> **Úkol 1:**
> Přepište text `<span>` s id "pozdrav" na libovolný text pomocí konzole.
> ![zmena_textu](/images/dom/zmena_textu.png)

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

> **Úkol 2a:**
> Vytvořte a zavolejte z konzole funkci `start()`.

> **Úkol 2b:**
> Zavolejte funkci přes tlačítko s atributen `onclick`.

### Získání vstupu od uživatele

```js
const value = document.getElementById("uzivatelsky_vstup").value;
console.log(value);
```

> **Úkol 3:**
> Zadejte libovolný text do `<input>` s id "uzivatelsky_vstup" a vypište jej do konzole.

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

> **Úkol 4:**
> Upravte vzhled libovolných prvků na stránce pomocí konzole.

### Náhodné číslo

```js
const prvni_nahodne_cislo = Math.floor(Math.random() * 10); // <0, 9>

const druhe_nahodne_cislo = Math.floor(Math.random() * 10 + 1); // <1, 10>
```

> **Úkol 5:**
> Vypište do konzole náhodné čislo od 4 do 80.
