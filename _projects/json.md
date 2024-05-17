---
layout: post
title: "JSON"
category: "html"
order: 3
---

## JSON

JSON je způsob uchovávání, přesouvání a zpravání dat. Jeho struktura je velmi jednoduchá.

```json
{
  "klic": "hodnota"
}
```

Můžeme si takto například uložit ceny v elektru. Jako klíč použijeme název zařízení a do hodnot uložíme pole cen. První cena je při okamžitém odběru a druhá při nákupu na splátky.

```json
{
  "pocitac": [11999, 10099],
  "notebook": [12999, 11099],
  "mobil": [13999, 12099],
  "tablet": [14999, 13099]
}
```

Pokud nyní chceme s těmito daty pracovat, musíme je "deserializovat". Z obyčejného textu - JSONu si vytvoříme javascriptový objekt.

```js
let ceny_objekt = JSON.parse(`{
  "pocitac": [11999, 10099],
  "notebook": [12999, 11099],
  "mobil": [13999, 12099],
  "tablet": [14999, 13099]
}`);
```

Nyní můžeme na základě klíče získat hodnotu. Cheme například zjistit kolik stojí notebook a tablet. Můžeme použít dvě různe syntaxe.

```js
// dot notation - tečková notace
const cena_notebook = ceny_objekt.notebook; // [11999, 10099]

// bracket notation - závorková notace
const cena_tablet = ceny_objekt["tablet"]; // [14999, 13099]
```

Můžeme rovněž jednoduše upravit data objektu. Mějme například slevu na mobilní telefony při nákupu na splátky. Upravíme tedy prvek v poli na indexu 1.

```js
ceny_objekt.mobil[1] = 9999;
```

Toto řešení funguje, ale není příliš přehledné. JSON nám s tím ale pomůže! Přepišme původní strukturu JSON tak, aby byla přehlednější.

```json
{
  "pocitac": { "okamzite": 11999, "splatky": 10099 },
  "notebook": { "okamzite": 12999, "splatky": 11099 },
  "mobil": { "okamzite": 13999, "splatky": 12099 },
  "tablet": { "okamzite": 14999, "splatky": 13099 }
}
```

Nyní můžeme cenu u mobilu upravit tímto způsobem.

```js
ceny_objekt.mobil.splatky = 9999;
```

Můžeme také tuto strukturu zcela změnit. Objekty můžeme přidávat do pole. Uděláme si tedy seznam zařízení, kde každé bude reprezentováno jako JSON.

```json
[
  {
    "nazev": "pocitac",
    "cena": {
      "okamzite": 11999,
      "splatky": 10099
    }
  },
  {
    "nazev": "notebook",
    "cena": {
      "okamzite": 12999,
      "splatky": 11099
    }
  },
  {
    "nazev": "mobil",
    "cena": {
      "okamzite": 13999,
      "splatky": 12099
    }
  },
  {
    "nazev": "tablet",
    "cena": {
      "okamzite": 14999,
      "splatky": 13099
    }
  }
]
```

Tento přístup může být výhodnější pokud checem změnit určitou vlastnost u všech prvnků najedou. Můžeme například veškere zboží zlevnit o 100 Kč.

```js
for (let i = 0; i < pole.length; i++) {
  pole[i].cena.okamzite -= 100;
  pole[i].cena.splatky -= 100;
}
```

> **Úkol 1 - Vytvořte rozsáhlejší strukturu**
> Zkuste přidat další záznamy. Přidejte atributy - barva, značka zařízení. Přidejte ke korunám (CZK) možnost platby v EUR a USD. Přeorganizujte sturkuturu, aby byla smysluplná a k datům se v aplikaci snadno přistupovalo.

Upravenou cenu následně můžeme poslat například zpět do databáze. K tomu je nutné javascriptový objekt znovu převést na prostý text - Serializovat.

```js
const aktualizovany_json = JSON.stringify(ceny_mobil);
```

Pokud bychom chtěli vypsat všechny ceny najedou, můžeme k tomu použít jednu z následujících metod.

```js
// Získáme všechny klíče a poté je projdeme
Object.keys(ceny_objekt).forEach((klic) => {
  console.log(klic, ceny_object[klic]); // zde je nutné pužít bracket notation
});

// Projdeme jednotlivé klíče pomocí cyklu for
for (let klic in ceny_objekt) {
  console.log(klic, ceny_object[klic]); // zde je nutné pužít bracket notation
}

// Můžeme také získat JEN hodnoty a postupně je vypsat bez klíčů
Object.values(ceny_objekt).forEach((hodnota) => {
  console.log(hodnota);
});
```

> **Úkol 2 - Vytvořte aplikaci**
> Vytvořete jednoduchou webovou aplikaci, ve které bude možné změnit data v JSON pomocí textového vstupu. Po každné aktualizace vypište do konzole / na stránku celý JSON.
