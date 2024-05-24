---
layout: post
title: Příkazy
category: "nodejs"
order: 1
---

## Příkazy v Node.js

Node.js je javascriptový **runtime**. Jedná se o typ softwaru, který nám umožňuje spouštět javascript, jakožto interpretovaný jazyk, na straně serveru == mimo prohlížeč. Node.js je na počítačích v našich učebnách nainstalovaný, v případě problémů se však dá stáhnout [zde](https://nodejs.org/).

Opět budeme pracovat ve vývojovém prostředí vscode. Vytvořte si novou složku a v ní nový soubor s libovolným jménem, standartně se používá `main.js`.

<h5 a><strong><code>main.js</code></strong></h5>

```js
console.log("ahoj");
```

Otevřte si příkazový řádek - `cmd.exe`. Pomocí příkazu `cd` se přesuňte do umístění vašeho `.js` souboru.

![cd](/images/node/cd.png)

Node.js vyžaduje soubor, který obsahuje základní informace o projektu. Jmenuje se `package.json` a vytvoříme ho pomocí npm (node package manager).

```zsh
npm init # Vyzve nás k doplnění jednoltivých informací

npm init -y # Soubor se vytvoří s defaultím nastavením
```

<h5 a><strong><code>package.json</code></strong></h5>

```json
{
  "name": "node",
  "version": "1.0.0",
  "description": "",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

Program spustíme příkazem `node`.

```zsh
node main.js
```

![cd](/images/node/node.png)

Větší programy většinou potřebují knihovny. Pokud stáhnete například z githubu projekt, je nutné před spuštěním doinstalovat potřebné knihovny.

```zsh
npm i
```

Pokud potřebujete ve vašem projektu použít konkrétní knihovnu, musíte znát její jméno.

```zsh
npm i <název knihovny>

npm i socket.io # Příklad
```

> **Úkol 1**
> Najděte na stránce [npm](https://www.npmjs.com/) libovolný balíček a nainstalujte ho.

Při instalaci jakéhokoliv balíčku se nám vytvoří nový soubor - `package-lock.json`. Tento soubor obsahuje informace o všech knihovnách, které projekt používá.

<h5 a><strong><code>package-lock.json</code></strong></h5>

```json
{
  "name": "node",
  "version": "1.0.0",
  "lockfileVersion": 3,
  "requires": true,
  "packages": {
    "": {
      "name": "node",
      "version": "1.0.0",
      "license": "ISC"
    }
  }
}
```

Knihovny se ukládaní to automaticky generované složky `node_modules`. Základní struktura Node.js projektu vypadá tedy takto.

![cd](/images/node/structure.png)

Pokud používáte git, je zapotřebí vytvořit soubor `.gitignore`. Do tohoto souboru můžeme vepsat soubory a složky, které má git ignorovat. Například složka `node_modules` se **nezahrnuje** do commitu.

<h5 a><strong><code>.gitignore</code></strong></h5>

```
node_modules/
```

![cd](/images/node/structure_git.png)

> **Úkol 2**
> Vytvořte v Node.js program, který při spuštění vypíše 100 náhodných čísel od 1 do 458. Program nahrajte na github. Nezapomeňte na správný `.gitignore`.

Pokud máme program, který musí běžet nepřetržitě, můžeme použít k jeho spuštení `nodemon`. Nodemon umí zachytit změnu v souboru a automaticky se při ní restartovat. Změny v kódu se tak projeví okamžite.

```zsh
npm i nodemon -g # Instalce

npx nodemon main.js # Spuštění souboru
```

![cd](/images/node/nodemon.png)
