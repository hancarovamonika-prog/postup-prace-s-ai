# Postup mojej práce

Ako s Claudom vzniká každá nová vec v tomto projekte. Najprv ju popíšem, potom z toho vznikne zadanie, zadanie sa rozseká na malé úlohy a tie sa stavajú a overujú jedna po druhej. Takto vznikli aj úlohy `vyplnit-sablonu-pozadavku` a `navrhnout-stories` v [.ukoly/](.ukoly/).

## Prehľad

1. Popíšem úlohu
2. Claude ma vyspovedá
3. Vznikne zadanie
4. Zadanie sa rozseká na úlohy (rezy)
5. Postaví sa jeden rez
6. Overím ho ja a Claude ho skontroluje
7. Rez sa uzavrie a uloží
8. Zapíše sa slovník a rozhodnutia
9. Odovzdanie, keď sa práca končí

Body 5 až 7 sa opakujú pre každý rez.

## Kroky

1. **Popíšem úlohu.** Po slovensky, vlastnými slovami: čo je dnes zle alebo čo chýba. Napríklad že stories sa dnes do Miro prepisujú ručne.

2. **Vyspovedanie** (`/vyzpovidej`). Claude sa pýta, kým nie je jasné, čo sa má stavať. Rozhodnutia prekladá do dôsledkov, aby som rozhodovala o veci, nie o technike.

3. **Zadanie** (`/zadani`). Z rozhovoru vznikne písané zadanie `.ukoly/<nazov>/zadani.md`: čo je zle, čo s tým urobíme, čo to má vedieť, ako poznáme, že to funguje, a čo tam nepatrí. Ak je to len nápad, čaká ako `.ukoly/napad-<nazov>.md`, kým sa naň nedostane rad.

4. **Rozsekanie** (`/rozsekej`). Zadanie sa rozdelí na malé rezy `01-*.md`, `02-*.md` … Každý sa dá postaviť a ukázať samostatne. Napríklad vyplnenie šablóny má osem rezov: kópia šablóny, kapitola 1, otvorené otázky, osobné údaje, kapitola 2, zvyšok kapitoly 4, kapitola 3, opravy.

5. **Postavenie jedného rezu** (`/postav`). Claude postaví práve jeden rez. Ak je nejasné, ako má niečo vyzerať alebo správať sa, najprv ukáže náhľad (`/prototyp`).

6. **Overenie.** Claude si výsledok otvorí a ukáže ho v chate, nielen tvrdí, že je hotovo (`/zkontroluj`). Potom ho vyskúšam ja na vymyslenom popise a odškrtnem ručné podmienky v rezu. Ak niečo nesedí, vrátime sa k tomu.

7. **Uzavretie rezu.** Rez sa uzavrie, zmena sa uloží do gitu jednou vetou po česky a ide sa na ďalší. Keď sú hotové všetky rezy, hotová zložka sa presunie do `hotovo/`.

8. **Slovník a rozhodnutia** (`/slovnik`). Keď sa ustáli pojem, ide do [KONTEXT.md](KONTEXT.md). Keď padne rozhodnutie, ktoré sa ťažko mení, ide do [rozhodnuti/](rozhodnuti/). Napríklad že osobné údaje sa do dokumentov neprepisujú.

9. **Odovzdanie** (`/predavka`). Keď sa práca začína opakovať, po dvoch neúspešných opravách tej istej veci alebo keď sa uzatvára väčší kus, Claude zabalí, čo je hotové a čo ostáva, aby sa dalo pokračovať v novom rozhovore.

## Ak niečo nejde

- Neviem, čo ďalej: `/kudy`.
- Niečo padá alebo sa správa čudne: `/najdi-chybu`.
- Nerozumiem Claudovmu textu: `/cesky-prosim`.

## Pravidlá celej práce

- Šablónu nikdy neprepisujem, pracuje sa s kópiou.
- Claude nič nevymýšľa. Čo nie je pozorované alebo povedané mnou, je „neoverené“ a ide do otvorených otázok.
- Hotovo sa dokladá výstupom, nie tvrdením.
- Výstupy sú po slovensky, s názvami tlačidiel a polí presne ako v systéme.

Samotné vypĺňanie jedného požiadavku (od popisu po dokument) opisuje skill [pozadavek](.claude/skills/pozadavek/SKILL.md).
