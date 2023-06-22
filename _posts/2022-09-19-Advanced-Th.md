---
layout: post
title:  "Pokročilí čtvrtek"
category: "bar"
--- 

## Úvod

### Zakladni informace

Lektor: Radim Bača

Classroom code (section): DGQYYY

Místnost: EB405

Čas: 14:30

### Popis kroužku

Tento kroužek je koncipován jako navazující na kroužek pro začátečníky. Předpokládá se, že účastníci chápou a umějí používat základní stavební bloky programovacích jazyků jako:

- Opakované provedení (cyklus)
- Podmíněné provedení (if-else)
- Funkce
- Proměnná (typu integer a string)

V prvním půl roce znalost těchto konceptů ještě dále prohloubíme a zejména uplatníme při tvorbě aplikací s jednoduchými ovládacími prvky (textbox, tlačítko, dropdown). V druhé polovině roku, pak začneme pracovat s polem, což nám umožní ještě více rozšířit paletu aplikací.

## Práce s ovládacímí prvky

Každý ovládací prvek má své unikátní jméno. Na následujícím obrázku vidíme aplikaci se třemi ovládacími prvky:

![kids](images/applab_basic.png)

1. TextBox - jak vidíme na obrázku jméno textboxu je `text_input1`. Jméno se objeví, když v AppLabu najedeme na ovládací prvek myší.
2. Tlačítko - jeho jméno je `button_ok`.
3. Label - popiska s textem "text", kde jméno ovládacího prvku je `label_text`.

### getText - načtení hodnoty

Jak tedy načteme textovou hodnotu ovládacího prvku do proměnné? Pro načtení textové hodnoty textboxu `text_input1` do proměnné `moje_promenna` napíšeme:
```javascript
var moje_promenna = getText("text_input1");
```

### setText - nastavení hodnoty

Podobně potřebujeme občas hodnoty ovládacích prvků nastavovat. Nyní máme v proměnné `moje_promenna` hodnotu načtenou z textboxu. Nyní hodnotu nastavíme do popisky `label_text`:
```javascript
setText("label_text", moje_promenna);
```

### onEvent - reakce na událost

V mnoha situacích potřebujeme ještě reagovat na události. Nejobvykleji se jedná o vstupy od uživatele jako je kliknutí na tlačítko, nebo zadání hodnoty. Reakce na stisknutí tlačítka `button_ok`, kde zkopírujeme hodnotu zadanou v text boxu do popisky  `label_text` bude vypadat následovně:
```javascript
onEvent("screen1", "click", function( ) {
	var moje_promenna = getText("text_input1");
	setText("label_text", moje_promenna);
});
```

## Rozličné zajímavé úkoly

- [Úniková hra](https://studio.code.org/projects/applab/E80ueH72KM8WSqk1bvPrdwk1IPv1J36EEW_Xhum__Mo "Unikova hra")
- [Úniková hra (autor Matěj Chamrád)](https://studio.code.org/projects/applab/JLlNAmd3VcM0ItZXYBR-TCnfL_wLoTK52etVfogTHfQ "Unikova hra (autor Matěj Chamrád)")
- [Malá nábosilka](https://studio.code.org/projects/applab/-hRWjKGg9Q8nzRiqLY1XzC_WWRawVgYgtxjtjDDbiR4 "Malá nábosilka")
- [Memory challenge]({% post_url advanced/2022-12-08-memory_challenge %})
- [Dungeon]({% post_url advanced/2023-2-2-dungeon %})
- [JSON](https://bit.ly/3eTLeYH)

## Dungeon hra vytvořená studenty kroužku
V rámci kroužku studenti vytvořili svou varinatu hry Dungeon. Pokud máte zájem vyzkoušejte jednotlivé varianty této hry a následně [zde vložte své hodnocení jednotlivých verzí](https://forms.gle/9opLdAvNL8XhRCX67):

- [Štěpán](https://dungeon-blbeceknakoni.lorem-ipsum-team.repl.co/)
- [Michael](https://dungeon-misa2012.lorem-ipsum-team.repl.co/)
- [Marek](https://dungeon-marekhornik.lorem-ipsum-team.repl.co/)
- [Oli](https://dungeon-kanystrbenzinu.lorem-ipsum-team.repl.co/)
- [Artek](https://dungeon-artek0027.lorem-ipsum-team.repl.co/)