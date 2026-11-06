# Postup mojej práce

*Posledná aktualizácia: 6. 11. 2026, 21:20*

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

Prešla som šiestimi úlohami a siedma sa dokončuje. Každá prešla krokmi 1 až 7 vyššie a je v [.ukoly/](.ukoly/).

| Úloha | Kedy | Čo z nej vzniklo | Stav |
|---|---|---|---|
| **Vyplniť šablónu požiadavku** | 22. až 23. 10. 2026 | Z popisu problému pomocník ukáže prehľad a po potvrdení vytvorí kópiu šablóny. Vyplní kapitoly 1 až 4 (okrem 5 a 6), neoverené veci označí „(neoverené – Q-xx)“ a zapíše do otvorených otázok, osobné údaje do dokumentu nepustí a vie dokument opraviť na pokyn. Rezy: kópia šablóny, kapitola 1, otvorené otázky, osobné údaje, kapitola 2, zvyšok kapitoly 4, kapitola 3, opravy. | hotové, ručne overené, v `.ukoly/hotovo/` |
| **Navrhnúť stories** | 23. 10. 2026 | Story s vlastnými kritériami za každý druh školy a rolu. Text pre Miro po kartách (ID a veta, kritériá v popise), ktorý sa skopíruje ručne. Rezy: kritériá za každú story, text pre Miro, zapojenie do skillu `pozadavek`. | hotové, ručne overené, v `.ukoly/hotovo/` |
| **Znalosť systému** | 24. 10. 2026 | Pravidlá, ako sa udržuje podklad v `znalost/`: zápis len na pokyn a po potvrdení, so stavom, dátumom a zdrojom. Rezy: zápis na pokyn, čo sa smie zapísať, rozpory a overenie, zodpovedané otázky, ponuka zápisu po dokončení požiadavku. | hotové, ručne overené, v `.ukoly/hotovo/` |
| **Doptávanie a neoverené** | od 25. 10. 2026 | Pomocník sa pred prehľadom doptá na druh školy, používateľa a obrazovku, najviac tromi otázkami v kole. Ak podklad drží obrazovku len v stave N, K alebo A, vypýta si screen alebo textový popis, bez neho ide obrazovka ako neoverená. Veta o súčasnom fungovaní systému má „(neoverené – Q-xx)“, veta o požadovanej zmene značku nemá. Rezy: doptanie pred prehľadom, vyžiadanie screenu, rozlíšenie viet. | hotové, ručne overené, v `.ukoly/hotovo/` |
| **Archív zadaní** | 27. až 30. 10. 2026 | Každý požiadavok má v `pozadavky/` dokument, vedľa neho súbor stories a riadok v prehľade požiadaviek `pozadavky/PREHLAD.md` so stavom a počtom stories a otvorených otázok. Číslo požiadavky zapíše pomocník, až keď ho dám, a súbory sa potom premenujú (rozhodnutie 0005). Rezy: prehľad existujúcich dokumentov, nový riadok pri založení kópie, súbor stories, stav a číslo. | hotové, v `.ukoly/hotovo/` |
| **Testy stories a otázok** | 30. 10. 2026 | Automatické testy strážia, že stories, kritériá a tabuľka otvorených otázok 4.3 sa do dokumentu zapisujú správne a nerozbijú sa pri uložení. Rezy: spoločné pomôcky, zápis stories, text pre Miro a súbor stories, otvorené otázky. | hotové, v `.ukoly/hotovo/` |
| **Zdieľanie s kolegami** | od 3. 11. 2026 | Pomocník sa presúva do práce ako spoločný agent v Microsoft 365 Copilote (rozhodnutie 0007). Vznikol balík na stiahnutie: pokyny pre agenta, podklad vo Worde, tabuľka požiadaviek v Exceli, postup vo Worde a šablóna. Rezy 01 až 05 sú postavené a overené výpočtom. | ručné overenie a skúška prvého dňa čakajú na firemný počítač |

Popri tom vznikali slovník [KONTEXT.md](KONTEXT.md), rozhodnutia v [rozhodnuti/](rozhodnuti/) a podklad v [znalost/](znalost/), do ktorého som postupne dopĺňala obrazovky a pravidlá systému z testovania a z videonávodov.

### Testovanie systému s AI

Od 4. 11. 2026 testujem s AI systém ePrihlášky v testovacom prostredí, od 6. 11. podľa akceptačných testov (UAT) pre dodávateľa. Postup:

- AI pracuje vo vstavanom prehliadači. Prihlasujem sa vždy ja, AI heslá nezadáva. Na prepnutie role (zákonný zástupca, riaditeľ) alebo školy sa treba odhlásiť a prihlásiť znova.
- AI smie použiť existujúce testovacie dáta a vytvoriť nové, len keď to dovolím, a vždy s vymyslenými údajmi. Druhú osobu s rodným číslom si nevymýšľa.
- Výsledky, vady, návrh e-mailu pre dodávateľa a priebežný stav sa ukladajú do samostatného súkromného repozitára. E-mail posielam ja.
- Do súborov ani obrázkov sa nezapisujú mená, adresy, rodné čísla, čísla prihlášok ani heslá.
- Overené poznatky idú do podkladu v [znalost/](znalost/) len cez `/znalost`, po ukážke a mojom potvrdení. Po zápise sa znova vygeneruje podklad vo Worde a balík.
- Poučenie z testovania: AI nesmie vyberať neaktívne (sivé) prvky nástrojom, ktorý ich obíde. Inak vznikne chyba, ktorú bežný používateľ nikdy neuvidí.

## Čo ma čaká

- **Skúška prvého dňa vo firme** (rez 06 zdieľania): nastavím spoločného agenta, overím ho na skutočnom požiadavku a prvý kolega podľa postupu sám vyplní kópiu šablóny. Až potom dostanú agenta ostatní kolegovia.
- **Ručné overenia rezov 01 až 05** na firemnom počítači: podklad vo Worde, tabuľka v Exceli, postup a stiahnutie balíka.
- **Dokončenie UAT, fáza 1**, a po potvrdení dodávateľa fázy 2 a 3.

## Čo potrebujú kolegovia

Od 4. 11. 2026 platí rozhodnutie 0007: kolegovia budú pracovať so spoločným agentom v Microsoft 365 Copilote, nie so skriptmi. Pôvodná cesta cez VS Code a Python padla, lebo kolegovia majú len M365 Copilot. Treba mať:

1. **Microsoft 365 Copilot** a spoločného agenta, ktorého nastavím a zdieľam ja. **Neoverené:** či licencia dovoľuje agenta vytvoriť a zdieľať.
2. **Spoločný priečinok v Teams alebo SharePointe** so šablónou, tabuľkou požiadaviek a hotovými dokumentmi. Podklad v ňom mením len ja. **Neoverené:** či smie podklad ležať vo firemnom M365.
3. **Word** na vyplnenie kópie šablóny a **prístup do Miro**, kam sa karty z textu kopírujú ručne.

### Ako to bude fungovať v práci

1. Stiahnem z GitHubu balík `balik.zip` (pokyny pre agenta, podklad vo Worde, postup, tabuľka požiadaviek, šablóna) a nahrám ho do spoločného priečinka a do agenta.
2. Kolega opíše agentovi problém alebo chýbajúcu funkciu. Agent ukáže prehľad a po potvrdení napíše text kapitol 1 až 4, stories a kontrolný zoznam.
3. Kolega text ručne prenesie do kópie šablóny vo Worde, skontroluje ho podľa kontrolného zoznamu a pridá riadok do tabuľky požiadaviek.
4. Prvé dva až tri dokumenty každého kolegu skontrolujem ja, lebo bez skriptov chýbajú automatické kontroly.

Podrobný postup pre kolegov je v balíku (`postup.docx`).

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
