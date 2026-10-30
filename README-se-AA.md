# Toimunud sõidueksamid Eestis

Mootorsõiduki juhtimisõiguse saamiseks tuleb sooritada sõidueksam. Siit leiate Eestis läbiviidud sõidueksamite andmed.

Vaata ka:

- [Transpordiamet - Sõidueksam](https://www.transpordiamet.ee/soidueksam)
- [Transpordiamet - Autokoolide statistika](https://www.transpordiamet.ee/autokoolide-statistika)
- [Riigi Teataja - Juhi eksamineerimine ja juhtimisõiguse andmine](https://www.riigiteataja.ee/akt/128062011018?leiaKehtiv)
  - Lisa 18: Juhiloa tagaküljele kantavad koodid

## Andmestikus olevad failid

- `se_<aasta>.csv` - Sõidueksamite andmed vastava aasta kohta
  - Praeguse aasta failis on andmed kuni jooksva kuu alguseni
- `se_<aasta>.csv töödeldud` - Avaandmete poolt töödeldud versioon failist; API tarbimine võib töötada, aga ei soovita faili ennast alla laadida
- `se_metadata.json` - Veerupõhised metaandmed se csv failide kohta, mis peaks olema ka kättesaadav kui tarbida andmeid läbi API

## Andmete kuju

Sõidueksamite csv failis on igal real üks tehtud eksam:

- `EKSAMI_SOORITAJA` - Eksami sooritanud isik
  - Ühe eksamineeritava ID on sama igas failis selles andmestikus
- `KUUPAEV` - Eksami toimumise aasta ja kuu
- `BYROO` - Eksamiga seotud büroo
- `KATEGOORIA` - Juhiloa kategooria, mida eksamiga taotletakse
- `ERITINGIMUSED` - Eksami (ja juhiloaga) seotud eritingimused/lisaandmed
  - Eritingimuste sisu seletus on eelnevalt mainitud akti lisas 18
- `VIIMANE_AUTOKOOL` - Ajaliselt viimasena alanud nimekirjaga autokool
- `SOIDUOPETAJA_KAASAS` - Kas sõiduõpetaja oli kaasas (J-Jah/E-Ei)
- `EKSAMINEERIJA` - Eksamineerija ID
  - Ühe eksamineerija ID on sama igas failis selles andmestikus
- `SEISUND` - Eksami tulemus
- `KESTUS` - Kestus minutites
- `KATK_POHJUS` - Eksami katkestamise põhjus
- `MITTEARVESTATUD` - Sõidueksam on jagatud üksikuteks elementideks; siin on elemendid, mis ei saanud arvestatud
- `VEAD` - Eksamil esinenud vead

## Andmete Excelisse importimine

Seda faili ei ole soovitatav topelt klõpsuga eestipärases Excelis avada: ta ei oska sellega midagi peale hakata (muu regiooni Excelis võib minna paremini).

Parima tulemuse jaoks:

- Ava Excelis tühi töövihik
- Vali Andmed - Too andmed - Failist - Teksti-/CSV-failist
- Impordi soovitud `se_<aasta>.csv` fail
- Määra õiged parameetrid:
  - Faili päritolu: `65001: Unicode (UTF-8)`
  - Eraldaja: Koma
- Klõpsa "Andmeid transformeerima" (tõenäoliselt ebavajalik, võid ka lihtsalt "Laadi" vajutada)
  - Klõpsa "Kasuta esimest rida päistena" kui "Esiletõstetud päised" ei ole juba etappides
  - Kontrolli üle, et andmetüübid on õiged
    - Andmetüübi muutmiseks klõpsa veeru nimest vasakule jäävat tüübi ikooni
    - Eritingimused peab olema teksti kujul, ülejäänud leiab Excel ilmselt ise üles
    - (Kuupäevade puhul Excel automaatselt märgib kõik ajad esimesele päevale kui selle tüübiks on valitud kuupäev, tegelikult on antud ainult aasta ja kuu)
  - Klõpsa "Sule ja laadi"
- Kui "Päringud ja ühendused" kaardil ei ole näha ühtegi tõrget, siis läks laadimine loodetavasti edukalt

## Avaandmete lehe masintöötlusest

- Avaandmete leht nõuab pealkirja ja kirjeldust nii eesti kui inglise keeles, aga ikkagi automaatselt tõlgib eestikeelse teksti ingliskeelseks ja siis veel on tal jultumust öelda et "Metaandmete tõlkimiseks on kasutatud masintõlget ning nende kvaliteet võib seega olla kohati ebakorrektne"
- Failide järjekord ei ole sama kui üleslaadimise järjekord; ma ei tea miks ta neid sellises järjekorras näitab
- Ära lae alla töödeldud faili
  - Abivalmilt pannakse igale väärtusele jutumärgid ümber, ehk fail läheb suuremaks ja midagi ei muutu paremaks
  - Veerud järjestatakse ümber mingis järjekorras, sest see polnud ju tähtis kuidas need algselt olid, ega ju?
  - Kui laadida csv fail üles läbi veebilehe (mitte API), siis lähevad andmed veel rohkem katki; aga selle detailid jätaksin juba lugeja avastada

# Practical driving tests in Estonia

To obtain the right to drive a motor vehicle, you must pass a driving test. Here you can find details of driving tests taken in Estonia.

See also:

- [Transport Administration - Practical driving test](https://www.transpordiamet.ee/en/practical-driving-test)
- [Transport Administration - Driving school statistics](https://www.transpordiamet.ee/autokoolide-statistika) (only in Estonian)
- [Riigi Teataja - Driver examination and assigning the right to drive](https://www.riigiteataja.ee/akt/128062011018?leiaKehtiv) (probably only in Estonian) (if you find this act in English on their website, please let us know so it can be added here)
  - Annex 18: Codes on the back side of a driving licence

## Files in the dataset

- `se_<year>.csv` - Exam data for a given year
  - Current year data is until start of current month
- `se_<year>.csv processed` - Version of the file that has been processed by the open data website; consuming via API may work, but downloading this file is not advised
- `se_metadata.json` - Column-based metadata about se csv files which should also be available via API

## Data structure

Every row is one finished examination:

- `EKSAMI_SOORITAJA` - Examinee
  - Each examinee has one ID across all files in this dataset
- `KUUPAEV` - Exam year and month
- `BYROO` - Bureau that the exam is related to
- `KATEGOORIA` - Driving licence category that will be obtained
- `ERITINGIMUSED` - Additional information about the exam (and driving licence)
  - Explanations for additional info codes can be found in annex 18 of the previously mentioned act
- `VIIMANE_AUTOKOOL` - Last driving school that the examinee studied in
- `SOIDUOPETAJA_KAASAS` - If the driving teacher was also in the car (J-Yes/E-No)
- `EKSAMINEERIJA` - Examiner
  - Each examiner has one ID across all files in this dataset
- `SEISUND` - Result of exam
- `KESTUS` - Exam duration in minutes
- `KATK_POHJUS` - Reason for aborting exam (if applicable)
- `MITTEARVESTATUD` - An exam is divided into individual elements; this contains unsuccessful exam elements
- `VEAD` - Exam mistakes

## Importing data into Excel

This file is not recommended to be opened in Estonian regional Excel by way of double clicking on it (other flavors that respect comma as a delimiter may fare better).

For best results (keep in mind I do not have English language Excel and some labels may be different):

- Open an empty spreadsheet in Excel
- Click on Data - Get Data - From File - From Text/CSV
- Import the desired `se_<year>.csv` file
- Pick the correct parameters:
  - File Origin: `65001: Unicode (UTF-8)`
  - Delimiter: Comma
- Click "Transform Data" (probably unnecessary, you can also just click "Load")
  - Click "Use First Row as Header" if such a step is not already in applied steps
  - Check that column types are correct (probably not necessary)
    - To change type, click the type icon to the left of the column name, pick a type, and click "Replace current" in the window that opens
    - Eritingimused must be text, the rest should be fine automatically
    - (for dates, Excel will automatically mark every date as happening on the first of the month if date type is picked, even though the actual data only contains year and month)
  - Click "Close & Load"
- If the card on the right does not show any issues, then hopefully the loading was successful

## About Estonian open data machine processing

- The open data page requires a title and description both in Estonian and English, but then proceeds to overwrite the English text with an automatic translation; it then has the gall to say "Metadata is machine translated and may thus be of poor quality"
- The ordering of files is not the same as the order they were uploaded; I have no idea what order this is
- Do not download a processed file
  - Ever-so-helpfully every value gets quotation marks around it, which only serves to inflate the file size and do nothing else
  - Columns are reordered in some god-only-knows order, because it's not like that was an important part of the file that you spent time designing, right?
  - If you upload a csv file through the website (not the API), then the data is even more broken; but the details of that shall be left to the reader to discover
