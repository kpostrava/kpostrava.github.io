---
layout: post
title: TNKI
category: "nodejs"
order: 4
---

![Logo](/images/logo.png)

![Screenshot](/images/screen.png)

TNKI je real-time multiplayerová hra založená na websocketech. Avšak, protože zábava je v programování, a ne ve hraní hry, dostanete pouze repozitář se základní funkcionalitou a bude na vás hru dokončit. Po dokončení úkolů si hru můžete upravit k vlastnímu obrazu.

Repozitář: [https://github.com/kpostrava/tnki](https://github.com/kpostrava/tnki)

> 💡 Pro snadnější oriantaci v kódu si do vscode nainstaluje rozšíření “better comments”: [https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments](https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments)

## Spuštění serveru

Je zapotřebí z githubu stáhnout výchozí bod k programu. Domluvte se v týmu, kdo vytvoří společný fork a všichni si jej naklonujte. Pomocí `npm` následně nainstalujte potřebné balíčky. Server spusťte pomocí `nodemon`, tato služba umožňuje automatický restart serveru při změně souboru.

```bash
git clone <URL_forknutého_repozitáře>

cd <Cesta_k_uloženému_repozitáři>/server

npm i

npm i nodemon -g

npx nodemon main.js
```

## Popis kódu

**Datová struktura asociativní pole (hashmap)**

```js
const map_id_room = new Map();
```

<aside>
> 💡 Map() = asociativní pole

</aside>

V asociativním poli `map_id_room` používáme id tanku jako klíč a název místnosti jako hodnotu. Při každém připojení tanku do roomky zároveň do tohoto asociativního pole přidáme nový záznam.

Tímto máme zajištěno, že kdykoliv v programu můžeme okamžitě zjistit v jaké místosti se tank nachází. Naopak při odpojení tanku je důležité, abyste tank z tohoto pole smazali!

```js
const map_id_room = new Map(["id1", "místnost1"], ["id2", "místnost2"]);

map_id_room.set("id3", "místnost3"); //přidání záznamu s klíčem "id3"

console.log(map_id_room.get("id2")); //načtení záznamu podle klíče - vypíše "místnost2"

map_id_room.delete("id1"); //smazání záznamu s klíčem "id1"
```

Příklad zapsání a získání dat z asociativního pole.

```js
const map_key_value = new Map([
  ["ArrowUp", { x: 0, y: -1 }],
  ["ArrowLeft", { x: -1, y: 0 }],
  ["ArrowDown", { x: 0, y: 1 }],
  ["ArrowRight", { x: 1, y: 0 }],
]);
```

Dalším příkladem asociativního pole je `map_key_value`. Umožňuje nám najít podle názvu klávesy koeficienty pro pohyb po jednotlivých osách.

**Server:**

Třídy:

`Room` - Jeden server může hostovat více her součásně, každá hra má svou instanci třídy `Room`.\_

Každá instance má svůj unikátní identifikátor - `room_name`, který se následně používá v asociativních polích pro její identifikaci.

Konstruktor potřebuje:

`session_id` - ID uživatele, který vytvořil místnost, pochází ze socketio

`tank` - Instance třídy tank, který vytvořil místnost

`max_players` - Maximální počet hráču, zadán tvůrcem místnosti, defaultně 2-4

`room_name` - Název místnosti, zadán tvůrcem místnosti, **musí být unikátní**

`game_map` - Herní mapa, může být konstanta, nebo výstup z funkce `shuffle_map()` pro randomizaci mapy

Třída Room obsahuje vlastní asociativní pole `tanks`. Toto pole slouží k rychlému přiřazení `session_id` ke konkrétní instance třídy Tank.

Maximální počet hráčů a jméno místnosti zadává uživatel do formuláře na domovské stránce.

```js
class Room {
  started = false;
  tanks = new Map();

  constructor(session_id, tank, max_players, room_name, game_map) {
    this.admin = session_id;
    this.max_players = max_players;
    this.room_name = room_name;
    this.game_map = game_map;

    this.tanks.set(session_id, tank);
    map_id_room.set(session_id, room_name);
  }

  join(session_id, tank) {
    this.tanks.set(session_id, tank);
    map_id_room.set(session_id, this.room_name);
  }

  tanks_length() {
    return this.tanks.size;
  }
}
```

`Tank` - Každý hráč má svou instanci. Všechny tanky musí patřit nějaké instanci třídy Room.

Konstruktor potřebuje:

`index` - Pořadí tanku, získáme voláním `tanks.length()` na instanci třídy `Room`, do které daný tank patří

`player_name` - Jméno hráče, zadává uživatel do formuláře na domovské stránce

`session_id` - ID uživatele, pochází ze socketio

Každá instance třídy `Tank` obsahuje informace o aktuální poloze tanku a jeho barvu.

```js
class Tank {
  constructor(index, player_name, session_id) {
    this.x = start_positions[index].x;
    this.y = start_positions[index].y;
    this.color = colors[index];
    this.player_name = player_name;
    this.index = index;
    this.session_id = session_id;
  }

  validate_move(coords) {}

  move(key, shift) {}

  shoot() {}
}
```

**websockety**

Veškerá komunikace klient - server je zprostředokována pomocí websocket.

Například při kliknutí na talčítko `create room` na domovské stránce. Se emitne event.

```js
socket.emit("create_room", {
  room_name: room_name,
  max_players: max_players,
  player_name: player_name,
});
```

Server na něj umí reagovat:

```js
io.on("connection", (socket) => {
    socket.on("create_room", (msg) => {
	    console.log(msg);
    });

    socket.on("join_room", (msg) => {
    })
```

Stejným způsobem to funguje i opačným směrem.

**Klient**

**Změna obrazovek**

Pro snadné přepínání mezi obrazovkami - `home`, `lobby`, `game`, máme implementovanou jednoduchou funkci. Obrazovku, kterou cheme zobrazit zadáme jako argument při volání funkce `set_screen()`. Funkce nastaví viditelnost obrazovky v argumentu a skryje všechny ostatní.

```js
const screens = ["home", "lobby", "game"];

const set_screen = (visible_screen) => {
  screens // Všechny obrazovky
    .filter((hidden_screen) => hidden_screen != visible_screen) // Vybereme jen ty, jejichž jméno se nerovná jménu v argumentu funkce
    .forEach((hidden_screen) => {
      document.getElementById(hidden_screen).classList.add("hidden"); // Přidáme jim třídu "hidden" - skryjeme je
    });
  document.getElementById(visible_screen).classList.remove("hidden"); // Zobrazíme obrazovku z argumentu
};
```

<h5 a><code>(Můžeme také jednoduše skrýt všechny prvky a následně zobrazit jen prvek z argumentu)</code></h5>

Jako argument posíláme název obrazovky.

```js
set_screen("lobby");
```

Můžeme takto jednoduše přepínat obrazovky. Pokud chcete přidat vlastí obrazovku, stačí jen přidat její id do pole `screens` a vytvořit k ní příslušný prvek v grafickém rozhrání pomocí html.

**Uživatelské vstupy**

V základu aplikace používá šipky pro pohyb, shift pro rotaci a mezerník pro střelbu. Pokud je některá z těchto kláves stisknuta, informujeme o tom server. Zároveň voláme metodu `preventDefault()`, která zabrání například nechtěnému posunu obrazovky v důsledku stisknutí šipky dolů.

```js
const move_keys = ["ArrowUp", "ArrowLeft", "ArrowDown", "ArrowRight"];

document.onkeydown = (e) => {
  if (move_keys.includes(e.code)) {
    e.preventDefault();
    socket.emit("update_move", { key: e.code, shift: e.shiftKey });
    return;
  }

  //? Líbí se ti střelba při klávese "space"? Pokud ne, můžeš ji libovolně měnit!
  if (e.code == "Space") {
    e.preventDefault();
    socket.emit("update_shoot");
  }
};
```

**Indikátory**

Slouží k ukazování hráčů ve hře, jejich životů a nábojů. Při změně stavu nábojů, či životů je nutná jejich ruční aktualizace. Pomůže nám k tomu funkce `set_indicator()`.

```js
const set_indicator = (index, value, type) => {
  const indicator = document.querySelector(`#indicator_${index} .${type}`); // Načteme indikátor podle indexu tanku a jeho typu (životy, náboje, vlastní...)

  indicator.innerHTML = ""; // Vymažeme obsah indikátoru

  // Několikrát přidáme ikonu v závislosti na "value"
  for (let i = 0; i < value; i++) {
    indicator.innerHTML += `<img src="assets/${type}.png" class="w-8 h-8" />`; // Přidáme ikonu (srdce, náboj, vlastní...)
  }
};
```

Aktualizaci pak můžeme udělat velmi snadno.

```js
set_indicator(tank.index, 3, "ammo");
set_indicator(tank.index, 3, "health");
```

> 💡 Index identifikátoru je shodný s indexem tanku o kterém informuje

## Úkoly

> 💡 Veškerá logika je řešena na straně serveru. Klient pouze vykresluje získaná data z eventu a emituje event při uživatelském vstupu.

**Server:**

- Změnit mapu (\* generovat novou / upravenou pro každou hru)
- Implementovat kolize -
  - S okraji mapy (\* dynamicky v závislosti na velikosti mapy)
  - S barikádami
- Přidat třídě `Tank` potřebné atributy - životy, náboje, **směr** (\* vlastní atributy pro dalši herní mechaniky)
- Ověření dostatku nábojů při střelbě
- Trajektorie střely ve směru tanku
- Detekce zásahu tanku střelou
- Ubrání života při zásahu
- Ubrání náboje při střelbě
- Doplňování munice všech hráčů v pravidelných intervalech
- Stisknutím šipky společně s klávesou `shift` rotovat tank
- Logika odpojování hráčů
- Oznámení výhry / prohry
- Validace vstupů pro udáje nutné k vytvoření / připojení do místosti

**Klient**

- Vlastní textury
- Měnit texturu / rotaci textury na základně atributu směru ⇒ tank se natáčí ve směru pohybu
- Textura výbuchu při zasažení hráče
- Tlačítko pro odpojení z místnosti v čekacím lobby
- Reakce na odpojení hráče ze hry (smrt, problém s připojením) - Skrýt jeho indetifikátor a odstranit ze seznamu hráčů
- Naimplementovat event handler, který aktualizuje stav nábojů na indetifikátorech
- Funkce pro reset stavu hry pro jejím skončení
- Oznámení výhru / prohry například na eventu `win` / `lost`

**Bonusové**

- Úkoly uvedeny výše, označené symbolem \*
- Změňte ovládání ze šipek a mezerníku například na wsad a enter
- Vymyslete vlastní typ nábojů, například: splash demage, procházení barikádami, odrážení, více směrné
- Generujte na mapě náhodně bonusové životy / náboje
- Nastavení velikosti hracího pole adminem při vytváření roomky
- **Vymysli něco nového!**
