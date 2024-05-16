---
layout: post
title: Git intro
category: "html"
order: 1
---

# Git - Úvod

Git nám především umožní jednoduše sdílet soubory (tzn. náš zdrojový kód) s dalšími lidmi. Nicméně funkcí, kterém nám git nabízí je mnohem více. Uložením na git server vytvoříme zálohu našeho projektu na internetu, budeme se moci vracet k předchozím verzím, řešit konflikty v kódu a také budeme moci vytvářet tzv. větve. K práci s gitem budeme z počátku používat command line příkazy, které si dnes vyzkoušíme.

# Github

Jednomu projektu se na gitu říká **repository**. Repository můžete mít lokální v adresáři, nebo někde na server třeba na [github.com](https://github.com/). Začneme tedy tím, že na `github.com`:

1. vytvoříte účet (např. `hacker_ostravski`),
2. přihlásíte se do něj
3. a vytvoříte si nové repository se jménem `KeyDown`:

- Klikneme na `New`
- Vyplníme repository name na `KeyDown`
- Klikneme na `Create repository`

![Vytváření nového repository v github.com](images/git_new.png)

Po vytvoření se nám v `github.com` otevře stránka https://github.com/hacker_ostravski/KeyDown našeho nově vytvořeného repository. Prozatím je repository prázdné a stránka by tedy měla vypadat podobně jako to vidíme na obrázku.
![Nové repository v github.com](images/git_repository.png)

Naše repository je tedy umístěno na serveru `github.com` a my budeme chtít vytvořit jeho kopií v na lokálním počítači. K tomu využijeme příkazovou řádku.

## Přidávání změn

Otevřete příkazovou řádku (v nabídce Start napište `cmd`) a přesuňte se do adresáře `c:\users\kp\git`. Následně proveďte stažení repository do lokálního adresáře. Adresář se bude jmenovat stejně jako repository.

```bash
cd c:\users\kp\git
git clone https://github.com/hacker_ostravski/KeyDown
cd KeyDown
```

Nyní se nacházíme v naší lokální kopií repository `KeyDown`. Nyní se pustíme do vytvoření nového souboru, jeho umístění do lokálního repository a jeho následné zkopírování na `github.com`.

```bash
echo # Moje nove repository > readme.md
git add readme.md
git commit -m "Muj prvni commit"
git push
```

**Tuto posloupnost `git` příkazů si zapamatujte. Budete ji používat vemi často.** Na následujícím obrázku jsou tyto příkazy vyjádřeny schématicky.
![Základní příkazy](images/git_basic.png)

Po provedení příkazů se přepněte do prohlížeče a znovu si zobrazte svoje repository na `github.com`. Nyní už by mělo obsahovat jeden soubor `readme.md`, který jsme tam přidali. Také se na stránce objevil popis, který odpovídá textu v `readme.md`. Git servery vždy automaticky zobrazují obsah `readme.md` na stránce repository.

> **Úkol 1:**
> Ve svém počítači proveďte změnu `readme.md` (cokoli do něj dopište) a následně tuto změnu propagujte do repository. Použijte stejnou posloupnost git příkazů (tzn. `add`, `commit`, `push`).

Příkaz `git add` jsme využili k přidávání změn v jednom souboru. Nicméně tento příkaz dokáže přidat i změny z více soborů najednou, takže jej nemusíme spouštět pro každý soubor zvlášť. Místo jména souboru dáme hvězdičku, která představuje libovolný řetězec.

> **Úkol 2:**
> Přidejte do repository soubory `index.html`, `script.js`, a `style.css` z board game, kterou jste vytvořili v repl.it. Následně tyto změny propagujte do lokální repository a pošlete na Github. Použijte stejnou posloupnost git příkazů (tzn. `add`, `commit`, `push`).

Pokud chceme vložit do staging area změny, které jsme provedli v souborech, které už v repository jsou, pak můžeme využít příkaz `git add -u`.

> **Úkol 3:**
> Přidejte do lokálního adresáře soubor `poznamky.txt`, kde si zapíšete dnešní datum. Přidejte do souboru `readme.md` popis projektu. Tzn. že se jedná o jednoduchou HTML hru, která se ovládá klávesami. Propagujte změny na Github tak, aby tam soubor `poznamky.txt` nebyl, ale změny provedené v `readme.md` ano.

## Přidání spolupracovníka (collaborators)

Pro přidání spolupracovníka přejdeme opět na stránku https://github.com/hacker_ostravski/KeyDow. Vybereme nahoře záložku `settings` a pak vlevo `collaborators`. Otevře se nám okno, kde můžeme přidat uživatele jak vidíme na obrázku. Přidejte uživatele se kterým jste domluveni (on vás také přidá).
![collaborators](images/git_colaborator.png)

Nyní máme přístup k repository druhého uživatele. Řekněme, že jde o uživatele `polrajch`. Nyní chcete přistoupit k jeho repository a přidat mu do souboru `readme.md` nějaké změny. Opět repository stáhneme do lokálního adresesáře provedeme změny a ty následně potvrdíme posloupností příkazů `add`, `commit`, `push`.

```bash
git clone http:\\gitbub.com\polrajch\KeyDown polrajch_keydown
cd polrajch_keydown
# provedeme změnu v souboru readme.md
git add -u
git commit -m "Readme.md upraveno"
git push
```

**Nyní počkejte až ve vašem repository provede uživatel také změny a dá je na github.**

V tuto chvíli jsou ve vašem Github repository změny provedené druhým uživatelem. Aby jste mohli dále pracovat na aktuální verzi u sebe na počítači, tak je potřeba změny stáhnout. To se provede příkazem `git pull`.

> **Úkol 4:**
> Zkuste se zamyslet, v jakých chvílích by jste měli příkaz `git pull` spouštět. Existují nějaké typické chvíle, kdy by jste jej měli provést?

## Konflikty

Konflikt je situace, kdy vy i druhý uživatel provede změny ve stejném souboru.

Zkusíte si tedy vyvolat konflikt v lokálním repository sami tak, že si repository stáhneme podruhé do jiného adresáře. Otevřete si druhé command line okno a proveďte následující.

```
git clone http:\\gitbub.com\hacker_ostravski\KeyDown KeyDown2
cd keydown2
```

Máme tedy repository lokálně dvakrát. Jednou v adresáři `KeyDown` a podruhé v adresáři `KeyDown2`.

### Automaticky řešené konflikty

Zkusíme nyní v repository vyvolat konflikt. Zkusíme začít konfliktem, který by měl git vyřešit sám, bez nutnosti zásahu uživatele.

Provedeme postupně změny ve `script.js` souborech. V prvním adresáři zapíšete komentář na začátek souboru a v tomto adresáři provedete `add`, `commit`, `push`.

```bash
# provedeme změnu v souboru script.js (dáme komentář na začátek script.js)
git add -u
git commit -m "script.js Komentar pridan na zacatek"
git push
```

V druhém adresáři provedeme změnu ve `script.js` tak, že přidáme komentář na konec. V druhém adresáři nyní provedem příkazy `add`, `commit`

```bash
git add -u
git commit -m "script.js Komentar pridan na konec"
```

Pokud se nyní pokusíme provést příkaz `push`, tak se příkaz neprovede, protože na git je nyní verze, která je o jeden commit dále něž je tato lokální verze. Tzn. musíme v druhém adresáři před provedením `git push` provést nejprve `git pull`.

```bash
git pull
```

Obě změny jsou ve stejném souboru (tzn. jsou konfliktní). Nicméně git si s nimi poradí, protože změny jsou v jiných částech souboru a obě verze spojí do nové verze, kde jsou oba komentáře.
![automaticky vyřešený konflikt](images/git_automatic_merge.png)

Nyní změnu pošlete na Github respository s pomocí `push`.

```bash
git push
```

### Konflikty řešené uživatelem

Druhá situace, kterou vyzkoušíme, je komplikovanější. Může se nám stát, že vznikne konflikt ve stejném řádku souboru a git si s tím nebude vědět rady. Nejprve tedy v obou adresářích provedeme `git pull`.

```bash
git pull
```

Nyní v obou adresářích změníme text v úvodním komentáři. V prvním adresáři dáte `add`, `commit`, `push`. V druhém adresáři dáte následující příkazy.

```bash
git add -u
git commit -m "script.js upraven komentar prvniho radku"
git pull
```

Příkaz `git pull` povede na konflikt, který je nutné vyřešit ručně. Když dáme příkaz `git status` uvdíme, že soubor je v konfliktním stavu. Při otevření souboru v libovolném textovém editoru vidíme poněkud nepřehledný obsah, který neodpovídá ani jedné verzi souboru. Pro efektivní vyřešení konfliktu využijeme Visual Studio Code.

```bash
code .
```

Ve VSCode bychom u souboru s git konfliktem měli vidět barevně vyznačené konfliktní řádky a vpravo dole tlačítko "Resolve in merge editor", které nám umožní konflikty efektivně vyřešit s pomocí tzv. 3-way merge monitor.
![VSCode](images/vscode.png)

3-way merge monitor nám umožní akceptovat buď je jednu z vybraných změn, nebo akteptovat obě. Možné je také to, že vytvoříme verzi úplně novou vzniklou spojením předchozích dvou. V editoru máme tři okna. Dvě horní jsou pro lokální verzi a pro vzdálenou verzi. Dolní okno je výsledek spojení.
![mergeeditor](images/mergeeditor.png)

Nad každým konfliktem můžeme v obou hodních oknech vidět tlačítka `Accept Incomming`, `Accept Combination`, nebo `Accept Current`. Pokud na některé klikneme, pak to odpovídajícím způsobem upraví kód v dolním okně. Vyzkoušejte. Jakmile budete mít všechny konflikty vyřešeny, tak klikněte na tlačítko `Complete Merge`.

Nyní je konflikt vyřešen a git nám dovolí provést `push`.

```bash
git push
```
