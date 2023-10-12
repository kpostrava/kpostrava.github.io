---
layout: post
title:  "Dungeon"
---
# Board game

Nejprve se [připojte do Lorem Ipsum týmu](https://replit.com/teams/join/xvtsjzaadrqmanaknpncvlanyelasxgw-lorem-ipsum-team) na Repl.it, kde by jste měli nalézt HTML5 verzi programu, který se nazývá "BoardGame (1)". 

## Popis programu
Základem celé aplikace je dvourozměrné pole `game_board` (10x10). K jednomu prvku pole přistoupíme s pomocí dvou hranatých závorek. Tzn. například:
```JavaScript
game_board[1][0] = 10
```
uloží na první řádek a nultý sloupec hodnotu 10. Jednotlivé políčka v `game_board` jsou nastavená na hodnotu nula nebo jedna. Hodnota jedna má vyjadřovat, že na dané pozici nachází překážka.

Dále se v programu nachází proměnné `x` a `y`, které uchovávají pozici hráče. Hráč je ovládán šipkami a posun v poli je implementován ve funkci `moveCircle`. 

## Úkoly

U této verze zkuste následující úkoly:
- Ošetřete v metodě `moveCircle` pohyb hráče tak, aby nemohl vstoupit na pole s překážkou (tzn. `game_board` je na dané pozici nastaven na jedna)
- Změňte obrázek překážky z modrého čtverce na nějaký obrázek (např. stěna)
- Změňte obrázek hráče z červeného kruhu na nějaký obrázek (např. auto, osoba zvrchu)
- Přidejte do `game_board` novou hodnotu 2, která bude reprezentovat nějakou odměnu, kterou chceme sebrat. Upravte `createBoard()` funkci, aby se odměny zobrazovaly v HTML.
- Napište do `moveCircle` logiku, která bude kontrolovat, zda-li hráč nevstoupil na pole s odměnou. Pokud vstoupí na pole s odměnou provede následující:
  1. Zvýší skóre hráče.
  2. Odstraní odměnu z `game_board`. Tzn. nastaví dané pole na 0 a v HTML odebere obrázek odměny.

