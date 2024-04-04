---
layout: post
title: Classes
tags:
  - git
---
# NodeJS
Dnes budeme pracovat s NodeJS. Tzn. vytvořte si lokální soubor `tank.js` do kterého si budete dávat kód. Program pak jednoduše spustíte přes příkazovou řádku:
```bash
node tank.js
```
Pokud chcete, vytvořte si na Github prázdnou repository a soubor si případně umístěte.

# Tank třída
V následující úloze se seznámíne s pojmem třída. Třída je užitečná pro organizaci kódu a jeho následné pochopení. 
```JavaScript
const colors = ["red", "green", "blue", "yellow"];

const min_x = 0
const max_x = 10
const min_y = 0
const max_y = 10

const start_positions = [
    { x: min_x, y: min_y, dir: 2 },
    { x: max_x, y: min_y, dir: 2 },
    { x: min_x, y: max_y, dir: 0 },
    { x: max_x, y: max_y, dir: 0 },
];

class Tank {
    constructor(index, player_name) {
        this.x = start_positions[index].x;
        this.y = start_positions[index].y;
        this.dir = start_positions[index].dir;
        this.color = colors[index];
        this.player_name = player_name;
        this.index = index;
    }
    
    print() {
        console.log("Tank name: " + this.player_name)
        console.log("Position: (" + this.x + ", " + this.y + ")");
    }
};
```
V tomto kódu jsme definovali třídu `Tank`, která má:
- Konstruktor 
- Metodu `print`

Jak konstruktor tak metodu si za chvilku vysvětlíme. Nejprve, ale začneme objektem.

## Objekt
Třída sama o sobě nic nedělá. Můžeme o ní uvažovat jako o datovém typu (jako třeba číslo nebo řetězec). Do datového typu nic neuložíme. Abychom mohli s třídou pracovat, musíme vytvořit **objekt**:
```JavaScript
tank1 = new Tank(0, "Radim");
```
Takto jsme vytvořili objekt typu `Tank`, který se jmenuje `tank1`. `tank1` má několik atributů:
- `x` 
- `y`
- `dir` - natočení tanku. 0 je nahoru, 1 doprava. 2 dolů a 3 doleva
- `color`
- `player_name`
- `index`

Slovo `this`, které vidíme v konstruktoru znamená něco jako "tento aktuální objekt". Tzn. že když napíšeme `this.player_name = player_name;`, tak u objektu (v našem případě `tank1`) nastavíme hodnotu atributu na hodnotu parametru `player_name`. 

> **Úkol 1 - Přidání atributů do třídy**
> Přidejte do třídy dva atributy: `lives`, `ammo`. Oba atributy budou na začátku nastaveny na hodnotu 3.

## Konstruktor
Jako první se u objektu vždy volá konstruktor. Jde o kód, který se provede automaticky. V našem kódu má konstruktor dva parametry `index` a `player_name`. Při vytváření objektu je tedy nutné tyto parametry předat, což jsme udělali (dali jsme tam hodnoty `0` a `"Radim"`).

> **Úkol 2 - Přidání parametrů konstruktoru**
> Přidejte do konstruktoru třídy atribut: `lives`. Nastavte daným parametrem atribut `lives` u objektu.
 
> **Úkol 3 - Nový objekt**
> Vytvořte druhý objekt `tank2`, kde konstruktor bude mít parametry `1`, `"Petr"` a `3`. 

## Metoda objektu
pokud chceme s objektem pracovat typicky se k tomu využívají metody jako je `print`.  Metodu zavoláte pomocí následujícího kódu:
```JavaScript
tank1.print();
```

> **Úkol 4 - Rozšíření výpisu**
> Rozšiřte metodu `print`, aby vypsala i další atributy jako je otočení (atribut `dir`), barva, životy atd. 

> **Úkol 5 - Nová metoda**
> Napište metodu `move`, která posune tank o jedno pole (podle toho kam je otočený). Metoda bude kontrolovat, jestli se tank nedostal mimo vyhrazené pole, které je definováno proměnnými `min_x`, `max_x`, `min_y`, `max_y`. 