# Postup: automatické vyplnenie šablóny cez Copilot Studio a Power Automate (cesta B)

*Návrh z 19. 11. 2026. Ešte nič z toho nebeží, všetko sa overí v práci.*

Cieľ: kolega opíše požiadavku agentovi a dostane späť odkaz na hotový dokument vo Worde. Text sa do šablóny už nekopíruje ručne po poliach.

Ako to funguje:

1. Kolega napíše agentovi popis požiadavky.
2. Agent ukáže prehľad a počká na potvrdenie (ako dnes).
3. Agent zavolá flow v Power Automate a pošle mu text všetkých polí.
4. Flow vezme šablónu zo SharePointu, vyplní jej polia a uloží kópiu `EP-XY_<kratky-nazov>.docx` do spoločného priečinka.
5. Agent vráti kolegovi odkaz na dokument a kontrolný zoznam.

Názvy ponúk Microsoftu sú tu podľa dokumentácie, nie zo skutočnej obrazovky.

## Čo akcia vie a čo nie

Flow používa akciu **Populate a Microsoft Word template** z konektora **Word Online (Business)**. Zdroj: [Microsoft Learn, Word Online (Business)](https://learn.microsoft.com/en-us/connectors/wordonlinebusiness/), overené 19. 11. 2026.

| Typ poľa | Akcia | Šablóna |
| --- | --- | --- |
| Textové pole (plain text) | vyplní | 101 polí, všetky majú názov (napr. `BUSINESS_PROBLEM`) |
| Zaškrtávacie pole | **nevyplní** | 67 polí (druh školy, typ požiadavky, používatelia, frekvencia, dopady) |
| Pole s formátovaným textom (rich text) | **nevyplní** | 65; v šablóne len obaľujú zaškrtávacie polia |
| Rozbaľovací zoznam | vyplní, ak má názov | 6, bez názvu (Priorita, Stav); tie aj tak nevypĺňame |
| Opakovaná sekcia (pridávanie riadkov) | vyplní | šablóna žiadnu nemá |

Ďalšie obmedzenia z dokumentácie, ktoré sa nás týkajú:

- **Prémiový konektor:** v Power Automate aj v Copilot Studiu.
- **MFA:** ak firma používa podmienený prístup s viacfaktorovým overením (MFA), akcia sa nedá použiť. Toto musí IT potvrdiť ako prvé, inak cesta B padá.
- **Zamknuté polia:** polia vo vygenerovanom dokumente môžu byť v lokálnom Worde zamknuté a sivé. Ak sa to stane, DITEC by nemohol dopĺňať kapitoly 5 a 6. Overí sa to pri skúške.
- **Veľkosť:** šablóna musí mať najviac 10 MB (naša má asi 0,7 MB) a dokument sa musí vytvoriť do 2 minút.

Čo z toho vyplýva:

- **Text kapitol 1 až 4** vyplní flow.
- **Zaškrtávacie polia** zaškrtne kolega ručne podľa zoznamu od agenta. To je asi 5 až 10 kliknutí a šablóna sa nemení.
- **Pevný počet riadkov:** šablóna má 3 riadky stories (`US_SUM_*_1` až `_3`), 6 akceptačných kritérií (`US_AC_1` až `_6`) a 3 otvorené otázky (`Q_*_1` až `_3`). Čo je navyše, agent vypíše a kolega pridá riadok ručne.
- **Plná automatizácia** by vyžadovala zmenu šablóny: zaškrtávacie polia nahradiť rozbaľovacím zoznamom ☐/☒ a tabuľky opakovanou sekciou. Na to treba súhlas toho, kto šablónu spracúva (neoverené, kto to je), a overenie, že sa upravený dokument dá spracovať. Kým to nie je potvrdené, platí pravidlo „šablónu nikto nemení“.

## Čo musí potvrdiť IT a zamestnávateľ

Pred stavbou si nechaj potvrdiť:

1. **MFA:** podmienený prístup s viacfaktorovým overením nezablokuje akciu Populate a Microsoft Word template.
2. **Copilot Studio:** firma má licenciu alebo kapacitu na Copilot Studio a analytička smie v prostredí Power Platform vytvoriť agenta a tok agenta (agent flow). Toky agenta sa platia z kapacity Copilot Studia, nie licenciou Power Automate pre každého ([Microsoft Learn, FAQ k tokom](https://learn.microsoft.com/en-us/microsoft-copilot-studio/flows-faqs)).
3. **DLP politika:** politika ochrany údajov v Power Platform dovoľuje konektory Word Online (Business) a SharePoint.
4. **Zdieľanie:** agenta smieš publikovať do Microsoft 365 Copilota a Teams a zdieľať ho s piatimi kolegami.
5. **Podklad a dokumenty:** smú ležať vo firemnom SharePointe (to platí aj pre cestu bez flow).

Kolegovia potrebujú len prístup k agentovi, prístup do spoločného priečinka a lokálny Word. Python, VS Code ani Power Automate nepotrebujú.

## Nastavenie (analytička, raz)

### 1. SharePoint

1. Na SharePoint stránke tímu vytvor priečinok `Šablóna` a nahraj doň šablónu `_EP-XY_Specifikacia DoF_Nazov poziadavky_VZOR.docx` z balíka. Šablónu neupravuj.
2. Priečinok `Dokumenty` je spoločný priečinok, kam flow ukladá hotové dokumenty a kde je tabuľka požiadaviek.
3. Kolegom daj do `Dokumenty` čítanie a zápis, do `Šablóna` len čítanie.

### 2. Tok agenta (agent flow) v Copilot Studiu

1. V Copilot Studiu otvor **Flows → New agent flow**. Trigger je **When an agent calls the flow**.
2. Pridaj vstupy (oba typu Text):
   - `nazovSuboru`, napríklad `EP-XY_zmena-poradia-skol`,
   - `polia`, čo je JSON s textom polí (formát je nižšie).
3. Pridaj akciu **Parse JSON**. Obsah je vstup `polia`, schému vygeneruj tlačidlom **Use sample payload** z príkladu nižšie.
4. Pridaj akciu **Populate a Microsoft Word template**. Location je SharePoint stránka, Document Library je knižnica s priečinkom `Šablóna` a File je šablóna. Objaví sa zoznam polí podľa ich názvov.
5. Do každého poľa z tabuľky „Polia, ktoré flow vypĺňa“ vlož rovnomennú hodnotu z Parse JSON. Polia, ktoré tam nie sú, nechaj prázdne.
6. Pridaj akciu **SharePoint → Create file**: priečinok `Dokumenty`, názov súboru `nazovSuboru` + `.docx`, obsah je výstup z predchádzajúceho kroku. Ak súbor s rovnakým názvom už existuje, flow ho nesmie prepísať. Pred Create file preto pridaj **Get file metadata using path** a podmienku, ktorá v tom prípade vráti chybu.
7. Pridaj **Respond to the agent** s výstupom `odkaz`, čo je odkaz na vytvorený súbor.
8. Ulož a pomenuj tok, napríklad „Vyplniť šablónu požiadavky“.

### 3. Agent v Copilot Studiu

1. **Create → New agent**. Name je „Pomocník ePrihlášok“.
2. **Instructions:** vlož celý obsah `pokyny-pre-agenta.txt` a pod neho dodatok z časti „Dodatok do pokynov agenta“. Neoverené: či má pole Instructions v Copilot Studiu rovnaký limit 8 000 znakov. Pokyny majú asi 6 900 znakov a dodatok asi 1 000, takže to treba pri vkladaní skontrolovať.
3. **Knowledge:** pridaj podklad (štyri `.docx` a `eP20.pdf`) zo SharePointu.
4. **Tools → Add a tool → Flow:** pridaj tok „Vyplniť šablónu požiadavky“. Do popisu nástroja napíš: „Zavolaj až po tom, čo používateľ potvrdil prehľad. Vytvorí dokument požiadavky zo šablóny.“
5. Pri vstupe autora použi premennú `System.User.DisplayName` (meno prihláseného). Autor sa potom berie zo systému, nie z textu. Neoverené: či je meno dostupné aj po publikovaní do Microsoft 365 Copilota. Ak nie, pole `Autor / gestor` ostane prázdne.
6. **Publish** a v **Channels** zapni Microsoft 365 Copilot a Teams. Zdieľaj s piatimi kolegami ako s konkrétnymi ľuďmi.

### Dodatok do pokynov agenta

```
## Vytvorenie dokumentu
Po potvrdení prehľadu zavolaj nástroj „Vyplniť šablónu požiadavky“:
- nazovSuboru: názov súboru z prehľadu bez .docx.
- polia: JSON s kľúčmi podľa zoznamu polí. Hodnota je presne text, ktorý by si inak vypísal do daného poľa. Kľúč, ktorý nemáš čím vyplniť, vynechaj. Nikdy nevypĺňaj polia kapitol 5 a 6, Priorita, Stav, Biznisový termín, Release ani Odkazy.
Stories daj do US_*_1 až _3 v poradí MŠ, ZŠ, SŠ a kritériá do US_AC_1 až _6. Otvorené otázky daj do Q_*_1 až _3.
Po zavolaní vypíš:
1. odkaz na dokument,
2. „Zaškrtni ručne:“ a presne tie možnosti z Druh školy, Typ požiadavky, Dotknutí používatelia, Koho sa problém týka a ako často nastáva a Požiadavka sa týka, ktoré platia,
3. „Pridaj ručne:“ stories, kritériá a otázky nad počet riadkov šablóny, s presným textom,
4. kontrolný zoznam.
Ak nástroj vráti chybu, napíš ju a vypíš text polí ako doteraz, aby ho kolega preniesol ručne.
```

## Polia, ktoré flow vypĺňa

Názvy polí sú v šablóne (karta **Vývojár → Vlastnosti**). Flow vypĺňa len tieto:

| Kapitola | Polia |
| --- | --- |
| Titulná strana | `COVER_TITLE` |
| 1. Základné údaje | `BASIC_ID_TITLE`, `BASIC_AUTHOR`, `BASIC_AREA` |
| 2. Biznis | `BUSINESS_PROBLEM`, `BUSINESS_GOAL`, `BUSINESS_USERS_IMPACT`, `PROCESS_STEP_1` až `PROCESS_STEP_5`, `BUSINESS_GUARDRAILS` |
| 3. Stories | `US_SUM_ID_n`, `US_SUM_TITLE_n`, `US_SUM_PERSONA_n`, `US_AS_n`, `US_WANT_n`, `US_VALUE_n` (n = 1 až 3), `US_AC_1` až `US_AC_6` |
| 4. Ostatné | `DEPENDENCIES`, `Q_ID_n`, `Q_TEXT_n`, `Q_OWNER_n`, `Q_DATE_n` (n = 1 až 3), `ATTACHMENTS` |

Flow nevypĺňa `COVER_ID` (číslo EP-XY dáva analytička), `COVER_VERSION`, `COVER_OWNER`, `COVER_ANALYST`, `BASIC_DATE`, `BASIC_RELEASE`, `BASIC_LINKS`, `PERSONA_OTHER`, `DITEC_*`, `FINAL_*` ani `HIST_*`.

Neoverené: či akcia v nevyplnených poliach nechá pôvodný text (napr. „[DOPLNÍ DITEC]“), alebo ho zmaže. Ak ho zmaže, do týchto polí vlož vo flow pôvodný text šablóny ako pevnú hodnotu.

Príklad vstupu `polia` (na vygenerovanie schémy):

```json
{
  "COVER_TITLE": "Zmena poradia škôl",
  "BASIC_ID_TITLE": "EP-XY-Zmena poradia škôl",
  "BASIC_AUTHOR": "",
  "BASIC_AREA": "Prihláška – výber škôl",
  "BUSINESS_PROBLEM": "…",
  "BUSINESS_GOAL": "…",
  "BUSINESS_USERS_IMPACT": "…",
  "PROCESS_STEP_1": "…",
  "BUSINESS_GUARDRAILS": "…",
  "US_SUM_ID_1": "EP-XY-ZŠ-US-01",
  "US_SUM_TITLE_1": "…",
  "US_SUM_PERSONA_1": "Zákonný zástupca",
  "US_AS_1": "zákonný zástupca",
  "US_WANT_1": "…",
  "US_VALUE_1": "…",
  "US_AC_1": "…",
  "DEPENDENCIES": "…",
  "Q_ID_1": "Q-01",
  "Q_TEXT_1": "…",
  "Q_OWNER_1": "",
  "Q_DATE_1": "",
  "ATTACHMENTS": "…"
}
```

Pri generovaní schémy doplň do príkladu všetky polia z tabuľky. Žiadne nesmie byť povinné, lebo agent nevyplnené kľúče vynecháva.

## Pre kolegov

1. Pozri do `tabulka-poziadaviek.xlsx`, či rovnakú vec už niekto nezadal.
2. Otvor agenta „Pomocník ePrihlášok“ v Microsoft 365 Copilote alebo v Teams a opíš požiadavku. Nepíš mená, e-maily, telefóny ani rodné čísla.
3. Skontroluj prehľad a potvrď ho („áno“) alebo ho oprav.
4. Agent vytvorí dokument a pošle odkaz. Otvor dokument v **lokálnom Worde**, nie vo Worde pre web.
5. Zaškrtni možnosti zo zoznamu „Zaškrtni ručne“, nič navyše.
6. Ak agent vypísal „Pridaj ručne“, pridaj riadok do tabuľky 3.1 alebo 4.3 a vlož text ako **Ponechať iba text**.
7. Skontroluj dokument podľa kontrolného zoznamu a ulož ho.
8. Pridaj riadok do `tabulka-poziadaviek.xlsx`.

Ak agent napíše, že dokument nevytvoril, prenes text ručne podľa `postup.docx`, časť 5.

## Skúška pred zdieľaním s kolegami

Skúšaj na požiadavke, ku ktorej už je hotový dokument (napríklad EP-06), aby si mala s čím porovnať.

1. Agent vytvorí dokument a vráti odkaz, zoznam „Zaškrtni ručne“ a kontrolný zoznam.
2. V lokálnom Worde ide zaškrtnúť a odškrtnúť každé zaškrtávacie pole v 1.1, 1.2 a 4.1.
3. Polia kapitol 5 a 6 sa dajú upravovať (nie sú zamknuté ani sivé) a majú pôvodný text šablóny.
4. Na karte **Vývojár** v **Režime návrhu** sú všetky polia ako v šablóne a žiadne nechýba.
5. Text sa zhoduje s odpoveďou agenta a s hotovým dokumentom EP-06 (rovnaké polia vyplnené).
6. Pole `Autor / gestor` obsahuje meno prihláseného, alebo je prázdne. Nikdy nie je cudzie meno.
7. Druhé spustenie s rovnakým názvom súboru existujúci dokument neprepíše.
8. Kolega, ktorý agenta nepoužíval, podľa časti „Pre kolegov“ sám vytvorí dokument.

Ak bod 2 alebo 3 neprejde (polia sú zamknuté), cesta B v tejto podobe nefunguje a ostáva ručný prenos. Ak prejde všetko, cesta B nahradí ručný prenos z rozhodnutia 0007. Zapíše sa to ako nové rozhodnutie.

## Neoverené

- MFA, licencia a kapacita Copilot Studia, DLP politika a zdieľanie (potvrdí IT).
- Zamknuté polia vo vygenerovanom dokumente a to, či zostane pôvodný text v nevyplnených poliach.
- Limit pokynov v Copilot Studiu a premenná `System.User.DisplayName` po publikovaní do Microsoft 365 Copilota.
- Presné názvy ponúk v Copilot Studiu a Power Automate vo firemnom prostredí.
