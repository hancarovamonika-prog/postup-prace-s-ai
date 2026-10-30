# Postup mojej práce

*Posledná aktualizácia: 25. 10. 2026, 18:20*

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

Prešla som štyrmi úlohami. Každá prešla krokmi 1 až 7 vyššie a je v [.ukoly/](.ukoly/).

| Úloha | Kedy | Čo z nej vzniklo | Stav |
|---|---|---|---|
| **Vyplniť šablónu požiadavku** | 22. až 23. 10. 2026 | Z popisu problému pomocník ukáže prehľad a po potvrdení vytvorí kópiu šablóny. Vyplní kapitoly 1 až 4 (okrem 5 a 6), neoverené veci označí „(neoverené – Q-xx)“ a zapíše do otvorených otázok, osobné údaje do dokumentu nepustí a vie dokument opraviť na pokyn. Rezy: kópia šablóny, kapitola 1, otvorené otázky, osobné údaje, kapitola 2, zvyšok kapitoly 4, kapitola 3, opravy. | hotové, ručne overené, v `.ukoly/hotovo/` |
| **Navrhnúť stories** | 23. 10. 2026 | Story s vlastnými kritériami za každý druh školy a rolu. Text pre Miro po kartách (ID a veta, kritériá v popise), ktorý sa skopíruje ručne. Rezy: kritériá za každú story, text pre Miro, zapojenie do skillu `pozadavek`. | hotové, ručne overené, v `.ukoly/hotovo/` |
| **Znalosť systému** | 24. 10. 2026 | Pravidlá, ako sa udržuje podklad v `znalost/`: zápis len na pokyn a po potvrdení, so stavom, dátumom a zdrojom. Rezy: zápis na pokyn, čo sa smie zapísať, rozpory a overenie, zodpovedané otázky, ponuka zápisu po dokončení požiadavku. | hotové, ručne overené, v `.ukoly/hotovo/` |
| **Doptávanie a neoverené** | od 25. 10. 2026 | Pomocník sa pred prehľadom doptá na druh školy, používateľa a obrazovku, najviac tromi otázkami v kole. Ak podklad drží obrazovku len v stave N, K alebo A, vypýta si screen alebo textový popis, bez neho ide obrazovka ako neoverená. Veta o súčasnom fungovaní systému má „(neoverené – Q-xx)“, veta o požadovanej zmene značku nemá. Rezy: doptanie pred prehľadom, vyžiadanie screenu, rozlíšenie viet. | hotové, ručne overené, v `.ukoly/hotovo/` |

Popri tom vznikali slovník [KONTEXT.md](KONTEXT.md), rozhodnutia v [rozhodnuti/](rozhodnuti/) a podklad v [znalost/](znalost/), do ktorého som postupne dopĺňala obrazovky a pravidlá systému z testovania a z videonávodov.

## Čo ma čaká

Všetky štyri úlohy sú hotové. V `.ukoly/` ostávajú dva nápady, každý sa najprv prejde cez `/vyzpovidej`:

- **Archív zadaní:** hotové zadania (vyplnená šablóna a text stories) sa budú ukladať do zložky, aby sa dali dohľadať.
- **Zdieľanie s kolegami:** kolegovia (päť ľudí, denne, približne tri mesiace) chcú dostať hotový vyplnený dokument ako ja, majú Visual Studio Code. V Microsoft 365 Copilote sa projekt preniesť nedá, lebo stojí na skriptoch, preto ide cesta cez VS Code. Čo musia mať pripravené, je v časti nižšie. Ešte sa vyspovedáva: kde bude zdieľaný priečinok a kto smie meniť podklad.

## Čo potrebujú kolegovia

Hotový dokument vznikne len vtedy, keď si AI môže na počítači kolegu spustiť skripty skillu `pozadavek`. Preto treba mať:

1. **Visual Studio Code.** Majú.
2. **Python 3** nainštalovaný na pracovnom počítači. Skripty používajú len štandardnú knižnicu, nič ďalšie sa neinštaluje. **Treba potvrdiť s IT, či to smú.**
3. **Agenta v VS Code, ktorý vie spúšťať príkazy** (napríklad GitHub Copilot s licenciou). Číta skills z `.agents/skills/`. **Treba potvrdiť s IT, či a akú licenciu majú.**
4. **Prístup k zdieľanému priečinku projektu** (podklad `znalost/`, šablóna `sablona/`, skills). Kde bude, sa ešte rozhoduje. Podklad sú popisy obrazoviek zo štátneho systému, preto treba potvrdiť, či smie ležať mimo môjho počítača.
5. **Word** na otvorenie a dokončenie hotového dokumentu a **prístup do Miro**, kam sa karty z textu kopírujú ručne.

Kým IT body 2 a 3 nepotvrdí, kolegovia môžu dostávať len hotový výstup, ktorý vyplním ja, alebo si v M365 Copilote nechať navrhnúť text kapitol a stories, ktorý do šablóny prepíšu ručne.

Kapitoly 5 a 6 šablóny a meno autora ostávajú mimo pomocníka: dopĺňam ich ja alebo sa vypĺňajú s DITEC. Číslo požiadavky dám pomocníkovi ja (v chate alebo cez „zosúlaď prehľad“) a on ho zapíše do dokumentu, stories, názvu súboru aj prehľadu.

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
