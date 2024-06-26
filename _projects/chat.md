---
layout: post
title: Chat aplikace (Sockets.io)
category: "nodejs"
order: 2
---

# Základní komunikace

Cílem tohoto úkolu bude se seznámit s knihovnou Sockets.io, která nám umožní vytvořit jednoduché klient-server aplikace.

## Setup

Nejprve si vytvořte fork této [repository](https://github.com/RadimBaca/chat). Klikněte tedy na tlačítko `Fork` na další stránce klikněte na `Create fork`, čímž se vytvoří kopie tohoto repository pod vašim účtem.

Stáhněte lokálně s pomocí `cmd` a otevřete projekt ve VSCode.

```bash
git clone https://github.com/vase_jmeno/chat
cd chat
code .
```

V repository vidíme dva adresáře. Jeden představuje NodeJS server a druhý představuje klienta.

### Server

Začneme zprovozněním serveru. Je nutné se přepnout do adresáře server, nainstalovat `socket.io` a server spustit.

```bash
cd server
npm install socket.io
node main.js
```

Pokud nevidte žádnou chybu, server běží a čeká na připojení klientů. Jedná se o NodeJS program. Vyzkoušejte server po spuštění přerušit s pomocí klávesové zkratky `ctrl+C`. Pokud uděláte nějaké změny v kodu `main.js`, tak je nutné běh serveru takto přerušit a spustit jej znovu, aby se změny projevily.

### Klient

Klient je pouze `index.html`. Takže otevřete `index.html` ve dvou oknech, v jednom něco napište a následně stiskněte tlačítko `SEND`. Pokud vše funguje, tak se napsaná zpráva objevila v obou oknech.

## Jak to funguje

Nyní se podrobněji podíváme na to jak to funguje. Základem řešení jsou zprávy posílané mezi jednotlivými aktéry (klient, server). Schematicky je to znázorněno na následujícím obrázku. Máme server ke kterému se připojili dva klienti. Server má seznam připojených klientů a když obdrží zprávu, tak ji rozešle všem.
![zprávy v socket.io](/images/socket_io1.png)

### Klient

Pro práci se zprávami máme u klienta k dispozici následující funkce:

- `socket.emit('chat_message', msg)` - pošle zprávu `chat_message` s řětězcovou hodnotou `msg`.
- `socket.on('chat_message', function X(msg))` - pokud obdrží zprávu `chat_message` tak spustí funkci `X` a předá ji řetězcový parametr `msg`.

> **Zamyšlení**
> Kde jsme již mohli vidět, že předáváme funkci jako parametr?

### Server

Na straně serveru vypadají funkce velmi podobně jako u klienta:

- `io.emit('chat_message', msg)` - pošle zprávu všem klientům.
- `socket.on('chat_message', function X(msg))` - pokud obdrží zprávu `chat_message` tak spustí funkci `X` a předá ji řetězcový parametr `msg`.

Nicméně přece jenom je to na straně serveru malinko komplikovanější. Můžeme si všimnout, že téměř všechen kód se nachází v handleru `io.on('connection', handler)`:

```JS
io.on('connection', (socket) => {
  // kód handleru
}
```

Můžeme tomu rozumět tak, při vytvoření nového socket spojení (připojení nového klienta) se spustí kód handleru, který následně obsluhuje požadavky klienta. Pokud server provede `io.emit` pak se zpráva rozešle všem klientům, jak to deomnstruje následující obrázek.
![Zaslaní zprávy s pomocí io.emit](/images/socket_io2.png)

> **Úkol 1 - odeslání zprávy jen ostatním klientům**
> Nyní celý program funguje tak, že pokud klient odešle zprávu `'chat_message'`, pak mu zprávu pošle server zpět. Nicméně to je poměrně zbytečné. V Sockets.io [existuje možnost](https://socket.io/docs/v3/broadcasting-events/) rozeslat zprávu všem ostatním kromě klienta, který zprávu inicioval s pomocí `socket.broadcast.emit('chat_message' , msg)`. Přepište tedy celý program, aby se použil `broadcast.emit`.

> **Úkol 2 - vlastní zprávy v chatu podbarvěte**

## JSON

Všimneme si, že při komunikaci si předáváme pouze řetězcové hodnoty. To má za následek skutečnost, že pokud chceme v rámci jedné zprávy předat komplexnější strukturu jako třeba JSON musíme ji nejprve převést na řetězec a pak následně z řetězce zase zpět.

Pro takové převody máme k dispozici následující funkce:

- `JSON.stringify(json_object)` - převede `json_object` na řetězec
- `JSON.parse(string)` - vrací JSON z řetězce

> **Úkol 3 - přidání pořadí zprávy**
> U každého klienta si vytvořte číselnou proměnnou, kterou na začátku nastavíte na nula. Při každém odeslání zprávy ji inkrementujete. Pošlete číslo spolu s textem zprávy jako jeden JSON objekt po stisku tlačítka SEND. Objekt je potřeba převést na řetězec s pomocí `JSON.stringify` a následně zpět.

## Další úkoly

Zkuste nyní dopracovat následující úkoly.

> **Úkol 4 - zadání jména**
> Do `class` `div` elementu s `id="chat"` přidejte hodnotu `hidden`. Tím celou chatovací část skryjete.
> Přidejte druhý `div` s textboxem a tlačítkem OK, kde bude uživatel zadávat svoje jméno. Nastavte `div id="init"`. Po kliknutí se vymění zobrazení `div` (tzn. jeden div zobrazíte a druhý skryjete). Kupříkladu první `div` se zobrazí následujícím příkazem `document.getElementById("chat").classList.remove("hidden")`.  
> Uložené jméno pak přidávejte do JSON objektu, který posíláte serveru po stisku tlačítka SEND a jméno pak zobrazujte před samotnou zprávou.

> **Úkol 5 - přidávání zpráv nahoru**
> Nyní se zprávy přidávají dolů. Upravte kód, aby se zprávy přidávaly nahoru.

[Pokračování - Socket.io room](/project/chat_room)
