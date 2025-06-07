# Tartu Programmeerimise Eksam 2025 (progeksam)

# Avutiosa



---

## Olulised juhised enne alustamist:

1.  Enne ülesannete lahendamist **lülita sisse Thonny logimine** (Tools → Options... → Log program usage events).
2.  **Sulge Thonny** ning käivita uuesti.
3.  **Lahenda arvutiosa ülesanded** (kokku 3 tükki).

---

## Ülesanne 1: Toidukuller (40 punkti)

Maarja plaanib hakata kasutama toidukullerit, et tellida toitu koju. Ta soovib teada, kui palju lisaks toidule talle kullerteenus maksma läheb. Ta kirjutas faili `tellimused.txt`, mitu korda ta iga päev toitu tellib (täisarv). Faili ridade arv ei ole teada.

### Näide faili `tellimused.txt` sisust:

```
1
2
3
1
2
```

---

### 1. Funktsioon `arvuta_päevahind`

Koosta funktsioon `arvuta_päevahind`, mille argumentideks on tellimuste arv päevas (täisarv) ja ühe tellimuse kullerteenuse hind eurodes (ujukomaarv). Funktsioon arvutab ja tagastab ühe päeva kullerteenuse hinna (ujukomaarv) ümardatult kaks kohta pärast koma.

**Arvesta:** Kui tellimusi on päevas 3 või rohkem, maksab kullerteenus **6.90 €**, sõltumata tellimuse ühikuhinnast.

#### Funktsiooni kirjeldus:

*   **Argumendid:**
    *   `tellimuste_arv` (int): Tellimuste arv konkreetsel päeval.
    *   `tellimuse_ühikuhind` (float): Ühe tellimuse kullerteenuse hind eurodes.
*   **Tagastab:**
    *   `float`: Ühe päeva kullerteenuse hind, ümardatud kahe kohani pärast koma.

#### Näide funktsiooni `arvuta_päevahind` tööst:

```python
>>> arvuta_päevahind(2, 2.5)
5.0

>>> arvuta_päevahind(3, 2.5)
6.9
```

####  Huviorbiiti sattuvad tegelased:

* **Ujuvpunktitäpsus:** Otsene võrdlemine või akumuleerimine ujukomaarvudega võib viia ootamatute tulemusteni, kuna arvutid salvestavad ujukomaarvu. Nõue `ound()` kahe kümnendkohani leevendab seda probleemi, kuid otseseid võrdlusi (nt ‚kui hind == 5.0‘) tuleks vältida või käsitleda ettevaatlikult.
* **Kõrvaljuhud:** Kuigi reegel `3 või rohkem` on selge, tuleb tagada, et loogika käitleb õigesti `tellimuste_arv` väärtusi, mis on täpselt 3, ja ka äärmuslikke juhtumeid nagu 0 või negatiivsed väärtused (kuigi tavaliselt ei eeldata neid selles kontekstis, arvestab kaitsev programmeerimine neid).
---

### 2. Peaprogramm

Koosta programm, mis täidab järgmisi samme:

1.  **Küsib kasutajalt**, kui palju maksab ühe tellimuse kullerteenus eurodes (ujukomaarv).
2.  **Küsib kasutajalt**, kui palju raha Maarja on planeerinud sel nädalal kullerteenusele kulutada (ujukomaarv).
3.  **Loeb failist `tellimused.txt`** iga päeva tellimuste arvu.
4.  **Arvutab iga päeva kullerteenuse hinna**, kasutades funktsiooni `arvuta_päevahind`.
5.  **Väljastab iga päeva kullerteenuse hinna** koos päeva järjekorranumbriga.
6.  **Arvutab kogu nädala kulleriteenuse hinna**.
7.  **Kui kulutatud summa ületab eelarvet**, väljastab teate: `"Eelarve läks lõhki!"`.

#### Näide programmi tööst (failiga `tellimused.txt`, kasutaja sisend on **paksus kaldkirjas**):

```
Sisesta ühe tellimuse kullerteenuse hind eurodes: **2.5**
Sisesta nädala eelarve eurodes: **15**

1. päeval kulus 2.5 eurot.
2. päeval kulus 5.0 eurot.
3. päeval kulus 6.9 eurot.
4. päeval kulus 2.5 eurot.
5. päeval kulus 5.0 eurot.
Kokku kulus raha 21.9 eurot.
Eelarve läks lõhki!
```

####  Huviorbiiti sattuvad tegelased:

* **Lollikindel faili I/O:**

    * **Lõks:** `FileNotFoundError`. Kui `tellimused.txt` ei ole olemas, siis programm jookseb kokku. Tugev lahendus kasutaks `try-except` plokki, et tabada `FileNotFoundError` ja anda kasutajasõbralik teade.

    * **Lõks:** Ebakorrektne faili sisu. Mis siis, kui rida `tellimused.txt` sisaldab numbri asemel „abc“? `int()` teisendamine tekitab `ValueError`. Selle väärikas käsitlemine (nt rea vahelejätmine või kasutaja teavitamine) parandab töökindlust.

* **Sisendi valideerimine:**

    * **Lõks:** `ValueError` on `float(input())`. Kui kasutaja sisestab mittenumbrilise teksti (nt „2“ asemel „kaks“), siis programmi `float()` teisendamine kukutab programmi. Parim praktika hõlmab `try-except` plokki ja tsüklit, et uuesti küsida kehtivat sisendit.

    * **Lõks:** Negatiivne või nullsisend. Kuigi probleem eeldab positiivseid kulusid ja tellimusi, võiks vanem programmeerija kaaluda, kuidas programm käitub, kui keegi sisestab hinnaks või eelarveks `0` või `-5`.

* **Kogumissumma täpsus:** Kogusumma `21,9` on esitatud ühe kümnendkoha täpsusega. Kuigi `arvuta_päevahind` ümardab kaheni, peaks ka summa säilitama asjakohase täpsuse, mis võib olla ümardatud lõpus, et see vastaks väljundi ootustele.

* **Päeval kuluse täpsus:** Näite väljund eeldab `f„{päev_number}. päeval kulus {kulu:.1f} eurot.“` vormindamiseks. Järjepidevus kümnendkohtade väljundi puhul on võtmetähtsusega.


---

# Ülesanne 2: Eksamitulemused (15 punkti)

Koosta programm õpilaste programmeerimise eksami punktide töötlemiseks. Failis `punktid.txt` on igal real õpilase nimi, tema punktid paberosa ja arvutiosa eest, mis on eraldatud semikoolonitega. Punktid on antud täisarvudena. Õpilaste arv ei ole ette teada.

## Näide faili `punktid.txt` sisust

```
Mari;35;50
Juku;30;30
Kati;38;54
```

---

## 1. Funktsioon `loe_tulemused`

Kirjuta funktsioon `loe_tulemused`, mis võtab argumendiks faili nime (`str`) ja tagastab sõnastiku (`dict`), mille võtmeteks on õpilaste nimed (`str`) ja väärtusteks punktide järjendid (`list` täisarvudest).

### Funktsiooni kirjeldus:

*   **Argumendid:**
    *   `faili_nimi` (str): Faili nimi, kust andmed lugeda.
*   **Tagastab:**
    *   `dict`: Sõnastik, kus võtmed on õpilaste nimed ja väärtused on nende punktide järjendid.

### Näide funktsiooni `loe_tulemused` tööst eelpool toodud tekstifailiga:

```python
>>> loe_tulemused("punktid.txt")
{'Mari': [35, 50], 'Juku': [30, 30], 'Kati': [38, 54]}
```

#### Huviorbiiti sattuvad tegelased:

* **Lollikindel failitöötlemine:**

    * **Lõks:** Ebakorrektsed read. Mis siis, kui `punktid.txt` reas puudub semikoolon (nt `Mari;35`) või on liiga palju (nt `Mari;35;50;extra`)?Meetod `split(';')` ei pruugi anda oodatud arvu osi, mis põhjustab `IndexError`, kui üritatakse pääseda ligi `parts[1]` või `parts[2]`.
    
* **Lõks:** Mitte täisarvulised punktid. Kui punktid on „35a“ asemel „35“, tekitab `int()` teisendamine `ValueError`.
    
  * **Lahendus:** Rakendage `try-except` plokid `ValueError` ja `IndexError` jaoks parsimise ajal, et vahele jätta vigased read või logihoiatused, selle asemel, et programmi crashida.

* **Tühi fail:** Funktsioon peaks korrektselt käitlema tühja `punktid.txt` faili, tagastades tühja sõnastiku.
* **Faili kodeerimine:** Keerulisemate stsenaariumide puhul on faili kodeeringu (nt `utf-8`) arvestamine oluline, et vältida `UnicodeDecodeError`, eriti kui nimed sisaldavad erimärke.


---

## 2. Funktsioon `lisa_osaleja`

Koosta funktsioon `lisa_osaleja` eksamisooritaja punktide lisamiseks või muutmiseks. Funktsioon võtab argumendiks sõnastiku. Funktsioonis küsitakse kasutajalt osaleja nime (sõne), paberosa punkte (täisarv) ja arvutiosa punkte (täisarv).

*   Kui sisestatud nimi on sõnastikus, siis asendatakse selle osaleja punktid uute punktidega ja funktsioon väljastab ekraanile teksti: `"Tulemus muudetud!"`.
*   Kui sellist nime ei ole, siis luuakse sellenimeline osaleja, lisatakse talle punktid ja funktsioon väljastab ekraanile teksti: `"Tulemus lisatud!"`.

Lõpus funktsioon tagastab sõnastiku uue seisu.

### Funktsiooni kirjeldus:

*   **Argumendid:**
    *   `tulemused` (dict): Sõnastik eksamitulemustega.
*   **Tagastab:**
    *   `dict`: Uuendatud sõnastik eksamitulemustega.

### Näited funktsiooni `lisa_osaleja` tööst (eeldades, et `sõnastik` on eelnevalt loetud):

#### Näide 1: Uue osaleja lisamine

```python
>>> sõnastik = loe_tulemused("punktid.txt")
>>> lisa_osaleja(sõnastik)
Nimi: Mart
Paberosa punktid: 15
Arvutiosa punktid: 35
Tulemus lisatud!
{'Mari': [35, 50], 'Juku': [30, 30], 'Kati': [38, 54], 'Mart': [15, 35]}
```

#### Näide 2: Olemasoleva osaleja punktide muutmine

```python
>>> sõnastik = loe_tulemused("punktid.txt") # Värskenda sõnastik algseisule
>>> lisa_osaleja(sõnastik)
Nimi: Mari
Paberosa punktid: 38
Arvutiosa punktid: 50
Tulemus muudetud!
{'Mari': [38, 50], 'Juku': [30, 30], 'Kati': [38, 54]}
```

####  Huviorbiiti sattuvad tegelased:

* **Punktide sisestamise valideerimine:** Sarnaselt eelmisele ülesandele, kui kasutaja sisestab punktide väärtused, mis ei ole täisarvulised, siis `int(input())` põhjustab `ValueError`. Hea tava on `try-except` kasutamine koos tsükliga, et tagada kehtiv täisarvuline sisend.

* **Nimede suurustundlikkus:** „mari“ erineb „Mari“ sõnaraamatu võtmetest. Probleem eeldab nimede suur- ja väiketundlikkust, kuid reaalses rakenduses võib soovida nimede normaliseerimist (nt `nimi.strip().capitalize()`), et vältida sama isiku topeltkandeid erineva suurtähestiku tõttu.

* **Sõnastiku otsene muutmine:** Kuna sõnastikud on muudetavad, saab funktsioon otse muuta argumendina esitatud `tulemused` sõnastikku. Sõnastiku selgesõnaline tagastamine on selguse huvides hea, kuid on oluline mõista, et ka *algne* sõnastikuobjekt väljaspool funktsiooni uuendatakse.
---

## 3. Funktsioon `leia_punktisumma`

Koosta funktsioon `leia_punktisumma`, mis võtab argumentideks sõnastiku ja inimese nime ning tagastab selle inimese punktide summa. Kui sellist nime ei leidu, siis väljastab ekraanile `"Nime ei leitud"`.

### Funktsiooni kirjeldus:

*   **Argumendid:**
    *   `tulemused` (dict): Sõnastik eksamitulemustega.
    *   `nimi` (str): Otsitava õpilase nimi.
*   **Tagastab:**
    *   `int` (punktisumma): Kui nimi leitakse.
    *   `None` (võimalik, kui funktsioon midagi ei tagasta, aga printib teate): Kui nime ei leita. (Märkus: Parim praktika oleks siin `None` tagastada ja printida teade funktsiooni _väliselt_ või tekitada `ValueError`.)

### Näide funktsiooni `leia_punktisumma` tööst (eeldades, et `sõnastik` on eelnevalt loetud):

```python
>>> sõnastik = loe_tulemused("punktid.txt")
>>> leia_punktisumma(sõnastik, "Juku")
60

>>> leia_punktisumma(sõnastik, "Peeter")
Nime ei leitud
```

####  Huviorbiiti sattuvad tegelased:

* **Mitteolemasolevate võtmete käsitlemine (KeyError):**

    * **Lõks:** Otsene ligipääs `tulemused[nimi]`, kui `nimi` ei pruugi olla võti, tekitab `KeyError`, mis kukutab programmi.

    * **Vältimine:** Kasutage `if nimi in tulemused:` enne võtmele juurdepääsu või kasutage `tulemused.get(nimi)`, mis tagastab `None` (või vaikeväärtuse), kui võtit ei leita, võimaldades graatsilist käitlemist. Praegune probleemipüstitus suunab kontrolli `if` suunas.

* **"Parim tava“ Return vs. Print:** Eksamite märkus toob esile olulise disainiotsuse. Funktsioone eelistatakse üldiselt *tagastada* väärtusi, jättes I/O (nagu sõnumite printimine) kutsujale. See muudab funktsioonid paremini taaskasutatavaks ja testitavaks. Kui funktsioon trükib teate ja tagastab vea korral ka `None`, võib see keerulisemaks muuta käitlemise kutsuvas koodis.


## 4. Funktsioon `leia_sisseastujad`

Koosta funktsioon `leia_sisseastujad`, mis võtab argumendiks eelpool kirjeldatud struktuuriga sõnastiku (võtmeteks nimed, väärtusteks punktide järjendid). Funktsioon peab kasutama juba olemasolevat funktsiooni `leia_punktisumma` leidmaks kõik õpilased, kellel on vähemalt **85 punkti**. Leitud õpilaste nimed ja nende *summaarsed* punktid (või keskmised punktid, kui tekstis viidatud "keskmisete punktide arvuga" on õige) väljastatakse ekraanile.

*(Märkus: Tekstis on vastuolu "punktid" ja "keskmisete punktide arvuga". Eeldan, et tuleks väljastada nimi ja **summaarne punktisumma**.)*

### Funktsiooni kirjeldus:

*   **Argumendid:**
    *   `tulemused` (dict): Sõnastik eksamitulemustega (nt. `{'Mari': [35, 50], 'Juku': [30, 30], 'Kati': [38, 54]}`).
*   **Tagastab:**
    *   `None`: Funktsioon väljastab tulemused otse ekraanile.

### Näide funktsiooni `leia_sisseastujad` tööst (eeldades, et sõnastik on eelnevalt laetud ja Mari ning Kati punktisummad on vastavalt 85 ja 92):

```python
>>> sõnastik = {'Mari': [35, 50], 'Juku': [30, 30], 'Kati': [38, 54]}
>>> leia_sisseastujad(sõnastik)
Informaatika erialale pääsevad õppima:
Mari 85
Kati 92
```

#### Huviorbiiti sattuvad tegelased:

* **Korrektne funktsioonide korduvkasutamine:**

    * **Lõks:** Argumentide mitte korrektne üleandmine `leia_punktisummale` või selle tagastusväärtuse valesti tõlgendamine (nt kui `leia_punktisumma` trükkib „Nime ei leitud“ ja tagastab `None`, peab `leia_sisseastujad` seda `None` selgesõnaliselt käitlema).

    * **Lahendus:** Veenduge, et `leia_sisseastujad` käitleb `leia_punktisumma` tagastust `None` graatsiliselt, kui `tulemused` nimi ei lahene kuidagi (nt kui `tulemused` on muudetud teise protsessi poolt või käsitsi).

* **Kahemõttelisuse lahendamine:** Eksami sisemises märkuses "punktid" vs. "keskmisete punktide arvuga" tuuakse esile üks reaalne stsenaarium. Selgitage alati mitmetähenduslikud nõuded. Valik „summaarne punktisumma“, nagu öeldud, on kontekstist lähtudes õige tõlgendus.

* **Itereerimine üle sõnastiku:** Õige iteratsioon üle `tulemused.items()`, et saada nii nimi kui ka punktide nimekiri, seejärel kasutada nime, et kutsuda `leia_punktisumma`.

* **Lävendiloogika:** Tagatakse, et loogika `>= 85` on õigesti rakendatud.

---

## 5. Põhiprogramm (Menüüga rakendus)

Koosta põhiprogramm, kus kasutaja saab valida järgmiste tegevuste vahel. Pärast iga tegevust küsib programm uuesti, mida kasutaja soovib teha, kuni ta valib programmi töö lõpetamise.

### Menüü valikud:

*   **`1` - Vaata tulemusi:**
    *   Kuvab kõigi osalejate tulemused (nimi ja punktid tühikuga eraldatult). (Nt. `Mari 35 50`)

*   **`2` - Lisa tulemus:**
    *   Lisab/muudab eksamipunktid, kasutades **funktsiooni `lisa_osaleja`**.
    *   Küsib kasutajalt nime, paberosa punkte ja arvutiosa punkte.
    *   Kui nimi on sõnastikus olemas, siis asendab punktid.
    *   Kui sellist nime pole, siis lisatakse sõnastikku uus nimi vastavate punktidega.
    *   Programm väljastab ekraanile teate tulemuse muutmise või lisamise kohta.

*   **`3` - Leia õpilase punktid:**
    *   Küsib kasutajalt nime.
    *   Leiab **funktsiooni `leia_punktisumma`** kasutades selle osaleja punktide summa ja väljastab selle ekraanile.

*   **`4` - Leia sisseastujad:**
    *   Leiab kõik informaatika erialale sisseastujad, kasutades **funktsiooni `leia_sisseastujad`**.
    *   Väljastab nende nimed koos *punktisummaga* (nagu eeldati `leia_sisseastujad` puhul) ekraanile.

*   **`5` - Lõpeta programmi töö:**
    *   Salvestab punktitabeli uue seisu **esialgse failiga samal kujul** (nt. `Mari;35;50`) **uude faili `punktid_uus.txt`**.
    *   Väljastab lõpetamise kohta teate: `"Fail salvestatud! Programm lõpetas töö."`

### Näide programmi tööst (kasutaja sisend on **paksus kaldkirjas**):

```
1 - Vaata tulemusi
2 - Lisa tulemus
3 - Leia õpilase punktid
4 - Leia sisseastujad
5 - Lõpeta programmi töö

Sisesta valik: **1**
Mari 35 50
Juku 30 30
Kati 38 54

Sisesta valik: **2**
Nimi: **Mart**
Paberosa punktid: **15**
Arvutiosa punktid: **35**
Tulemus lisatud!

Sisesta valik: **1**
Mari 35 50
Juku 30 30
Kati 38 54
Mart 15 35

Sisesta valik: **3**
Sisesta õpilase nimi: **Juku**
60

Sisesta valik: **4**
Informaatika erialale pääsevad õppima:
Mari 85
Kati 92

Sisesta valik: **5**
Fail salvestatud! Programm lõpetas töö.
```

####  Huviorbiiti sattuvad tegelased:

* **Peamise Tsükli Loogika:**

    * **Lõks:** Lõputu tsükkel, kui väljumistingimus ei ole täidetud või `break` ei ole õigesti kasutatud. Veenduge, et `while` silmus lõpetab ainult siis, kui valitakse `5`.

    * ****Lõks:** Menüü kehtetu sisendiga tegelemine. Kui kasutaja sisestab „x“ või „6“, põhjustab `int(choice)` `ValueError`. Lisa `try-except` plokk `ValueError` jaoks ja küsi kasutajalt uuesti kehtivat valikut.

* **Seisundi haldus:** Sõnastik `tulemused` tuleb initsialiseerida üks kord (nt kutsudes alguses `loe_tulemused(„punktid.txt“)`) ja seejärel pidevalt edastada ja uuendada teistele funktsioonidele kogu programmi täitmise jooksul.

* **Faili salvestamine (valik 5):**

    * **Lõks:** `punktid_uus.txt` kogemata ülekirjutamine. Nõue on salvestada *Uusesse* faili, kuid üldiselt on oluline tagada, et olemasolevad kriitilised andmed ei läheks kaduma (kuigi see ei ole eksami puhul selgesõnaliselt nõutav).

    * **Tulemuse vormindamine:** Tagasi kirjutamisel faili `punktid_uus.txt` tuleb tagada, et iga rida on vormindatud täpselt nii, nagu see on määratud (`Nimi;PaperPoints;ComputerPoints`), kaasa arvatud loetelu teisendamine tagasi stringiks.

    * **Ressursside haldamine:** Veenduge, et väljundfail on pärast kirjutamist korralikult suletud (jällegi, `with open(...)` on kõige ohutum viis).
      
* **Failitoimingute veakäitlus:** Algne kõne `loe_tulemused(„punktid.txt“)` peaks olema pakitud `try-except` plokki, et käsitleda `FileNotFoundError` algset andmete laadimist, alustades ehk tühja sõnastikuga, kui faili ei ole olemas, või andes selge veateate.

* **Kasutajakogemus (UX):** Kuigi seda ei ole otseselt hinnatud, muudavad selged juhised, järjepidevus ja sõbralikud veateated programmi palju kasutatavamaks.
---
</spoiler>
