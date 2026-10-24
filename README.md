# Postup mojej práce

*Posledná zmena: 24. 10. 2026*

Ako s AI vzniká každá nová vec v tomto projekte. Najprv ju popíšem, potom z toho vznikne zadanie, zadanie sa rozseká na malé úlohy a tie sa stavajú a overujú jedna po druhej. Takto vznikli aj úlohy `vyplnit-sablonu-pozadavku` a `navrhnout-stories` v [.ukoly/](.ukoly/).

## Prehľad

1. Popíšem úlohu
2. AI ma vyspovedá
3. Vznikne zadanie
4. Zadanie sa rozseká na úlohy (rezy)
5. Postaví sa jeden rez
6. Overím ho ja a AI ho skontroluje
7. Rez sa uzavrie a uloží
8. Zapíše sa znalosť, slovník a rozhodnutia
9. Odovzdanie, keď sa práca končí

Body 5 až 7 sa opakujú pre každý rez.

## Kroky

1. **Popíšem úlohu.** Po slovensky, vlastnými slovami: čo je dnes zle alebo čo chýba. Napríklad že stories sa dnes do Miro prepisujú ručne.

2. **Vyspovedanie** (`/vyzpovidej`). AI sa pýta, kým nie je jasné, čo sa má stavať. Rozhodnutia prekladá do dôsledkov, aby som rozhodovala o veci, nie o technike.

3. **Zadanie** (`/zadani`). Z rozhovoru vznikne písané zadanie `.ukoly/<nazov>/zadani.md`: čo je zle, čo s tým urobíme, čo to má vedieť, ako poznáme, že to funguje, a čo tam nepatrí. Ak je to len nápad, čaká ako `.ukoly/napad-<nazov>.md`, kým sa naň nedostane rad.

4. **Rozsekanie** (`/rozsekej`). Zadanie sa rozdelí na malé rezy `01-*.md`, `02-*.md` … Každý sa dá postaviť a ukázať samostatne. Napríklad vyplnenie šablóny má osem rezov: kópia šablóny, kapitola 1, otvorené otázky, osobné údaje, kapitola 2, zvyšok kapitoly 4, kapitola 3, opravy.

5. **Postavenie jedného rezu** (`/postav`). AI postaví práve jeden rez. Ak je nejasné, ako má niečo vyzerať alebo správať sa, najprv ukáže náhľad (`/prototyp`).

6. **Overenie.** AI si výsledok otvorí a ukáže ho v chate, nielen tvrdí, že je hotovo (`/zkontroluj`). Potom ho vyskúšam ja na vymyslenom popise a odškrtnem ručné podmienky v rezu. Ak niečo nesedí, vrátime sa k tomu.

7. **Uzavretie rezu.** Rez sa uzavrie, zmena sa uloží do gitu jednou vetou po česky a ide sa na ďalší. Keď sú hotové všetky rezy, hotová zložka sa presunie do `hotovo/`.

8. **Znalosť, slovník a rozhodnutia.** Nový poznatok alebo screen o systéme sa zapíše do `znalost/` len na môj pokyn „zapíš do podkladu“, po ukážke zmeny (pred a po) a po mojom potvrdení (`/znalost`). Zápis má stav, dátum a zdroj, a zo screenu sa zapisuje len textový popis. Keď sa ustáli pojem, ide do [KONTEXT.md](KONTEXT.md) (`/slovnik`). Keď padne rozhodnutie, ktoré sa ťažko mení, ide do [rozhodnuti/](rozhodnuti/). Napríklad že osobné údaje sa do dokumentov neprepisujú.

9. **Odovzdanie** (`/predavka`). Keď sa práca začína opakovať, po dvoch neúspešných opravách tej istej veci alebo keď sa uzatvára väčší kus, AI zabalí, čo je hotové a čo ostáva, aby sa dalo pokračovať v novom rozhovore.

## Čo som doteraz urobila

Prešla som tromi úlohami. Každá prešla krokmi 1 až 7 vyššie a je v [.ukoly/](.ukoly/).

| Úloha | Kedy | Čo z nej vzniklo | Stav |
|---|---|---|---|
| **Vyplniť šablónu požiadavku** | 22. až 23. 10. 2026 | Z popisu problému pomocník ukáže prehľad a po potvrdení vytvorí kópiu šablóny. Vyplní kapitoly 1 až 4 (okrem 5 a 6), neoverené veci označí „(neoverené – Q-xx)“ a zapíše do otvorených otázok, osobné údaje do dokumentu nepustí a vie dokument opraviť na pokyn. Rezy: kópia šablóny, kapitola 1, otvorené otázky, osobné údaje, kapitola 2, zvyšok kapitoly 4, kapitola 3, opravy. | hotové, ručne overené, v `.ukoly/hotovo/` |
| **Navrhnúť stories** | 23. 10. 2026 | Story s vlastnými kritériami za každý druh školy a rolu. Text pre Miro po kartách (ID a veta, kritériá v popise), ktorý sa skopíruje ručne. Rezy: kritériá za každú story, text pre Miro, zapojenie do skillu `pozadavek`. | hotové, ručne overené, v `.ukoly/hotovo/` |
| **Znalosť systému** | od 24. 10. 2026 | Pravidlá, ako sa udržuje podklad v `znalost/`: zápis len na pokyn a po potvrdení, so stavom, dátumom a zdrojom. | rozpracované, pozri nižšie |

Popri tom vznikali slovník [KONTEXT.md](KONTEXT.md), rozhodnutia v [rozhodnuti/](rozhodnuti/) a podklad v [znalost/](znalost/), do ktorého som postupne dopĺňala obrazovky a pravidlá systému z testovania a z videonávodov.

## Čo ma čaká

Úloha **Znalosť systému** má päť rezov:

1. Zápis na pokyn s potvrdením: **hotové**, ručná skúška prebehla.
2. Čo sa do podkladu smie: pravidlá sú v skille `znalost`: **hotové**, ručná skúška prebehla (screen s osobnými údajmi a požiadavka „chcem, aby systém robil X“ sa nezapísali, informácia od DITEC dostala stav A).
3. Rozpory a overenie: čo robiť, keď nový screen odporuje staršiemu tvrdeniu, a ako sa tvrdenie z videa zmení na pozorované. **Nezačaté.**
4. Zodpovedané otázky: odpoveď na otvorenú otázku zostane v tabuľke a zapíše sa ako pravidlo. **Nezačaté.**
5. Požiadavok a ponuka zápisu: po dokončení požiadavku pomocník ponúkne zápis nového poznatku do podkladu. **Nezačaté.**

Potom sú v `.ukoly/` dva nápady, ktoré sa ešte neprebrali (každý sa najprv prejde cez `/vyzpovidej`):

- **Archív zadaní:** hotové zadania (vyplnená šablóna a text stories) sa budú ukladať do zložky, aby sa dali dohľadať.
- **Doptávanie a neoverené:** keď pomocníkovi niečo chýba, doptá sa alebo si vypýta screen a čo ostane neoverené, zapíše do otvorených otázok.

Kapitoly 5 a 6 šablóny, číslo požiadavku (`EP-XY`) a meno autora ostávajú mimo pomocníka: dopĺňam ich ja alebo sa vypĺňajú s DITEC.

## Ak niečo nejde

- Neviem, čo ďalej: `/kudy`.
- Niečo padá alebo sa správa čudne: `/najdi-chybu`.
- Nerozumiem textu od AI: `/cesky-prosim`.

## Pravidlá celej práce

- Šablónu nikdy neprepisujem, pracuje sa s kópiou.
- AI nič nevymýšľa. Čo nie je pozorované alebo povedané mnou, je „neoverené“ a ide do otvorených otázok.
- Hotovo sa dokladá výstupom, nie tvrdením.
- Výstupy sú po slovensky, s názvami tlačidiel a polí presne ako v systéme.

Samotné vypĺňanie jedného požiadavku (od popisu po dokument) opisuje skill [pozadavek](.claude/skills/pozadavek/SKILL.md).
