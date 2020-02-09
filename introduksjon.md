Trafikkdata med R
================
Snorre Hansen
10 februar 2020

  - [Installasjon av R](#installasjon-av-r)
  - [Triks](#triks)
  - [Filformat og prosjekter](#filformat-og-prosjekter)
  - [Les mer](#les-mer)
  - [Trafikkdataanalyser](#trafikkdataanalyser)
  - [Hente data fra
    trafikkdata-APIet](#hente-data-fra-trafikkdata-apiet)
      - [Timetrafikk](#timetrafikk)

## Installasjon av R

Installer siste versjon av R fra [R
Project](https://www.r-project.org/).

Installer så [RStudio](https://www.rstudio.com/).

### Ekstra pakker

Basisversjoen av R inneholder mange muligheter, men noen tilleggspakker
er lurt. Her er de jeg bruker:

  - [tidyverse](https://www.tidyverse.org/): data i tabeller, endre,
    aggregere, plotte m.m.
  - readxl: for å lese inne Excelark
  - lubridate: formatere dato og tid
  - DataExplorer: utforske datasett

Litt senere:

  - jsonlite: formatere json
  - flextable: fine tabeller i “utskrift” (byindeksrapport)
  - ghql: for GraphQL-api (trafikkdata)
  - knitr: lage rapporter
  - leaflet: kart
  - sf: geodata (linjer, ploygoner)

For å installere pakker, bruk installeringsfunksjonen i RStudio. Pakkene
må manuelt oppdateres ved å sjekke etter nye versjoner.

For å ta i bruk pakkene i en R-fil, last de inn øverst i programmet:

    library(tidyverse)

## Triks

### Piping

Piping - hva er det\!? Programkommandoer blir lettere menneskelesbare
ved bruk av piping. Tidyverse bruker %\>% som pipesymbol. Den fungerer
sånn:

    x %>% f() er det samme som f(x)

Mer om dette i [magrittr-pakken](https://magrittr.tidyverse.org/), som
er en del av Tidyverse.

## Filformat og prosjekter

I R kan vi skrive R-kode i ulike filformater:

  - R-skript (ren kodetekst)
  - Markdown (rapport, kan bli html, word, powerpoint o.l.)
  - Notebook (gir html-dokument)

Den mest brukervennlige for vårt formål er kanskje Notebook. Åpne
RStudio og lag en Notebook-fil.

Det er lurt å lage et eget *prosjekt* i RStudio som samler alle filer
tilhørende analysen vi skal gjennomføre. Lagre derfor alle filer som
tilhører prosjektet, inkludert rådatafiler, i den samme mappen.

## Les mer

Nettet flommer over av tips, triks, blogger og dokumentasjon av R. En
fin bok er [R for Data Science](https://r4ds.had.co.nz/) av Grolemund og
Wickham.

# Trafikkdataanalyser

For å lese inn en navngitt CSV-fil, gjør vi slik:

    innlest <- read.csv2("filnavn.csv")

I R har vi da fått et objekt av typen *data.frame* som heter “innlest”.

  - Lese inn data fra utstyrstester (read\_\*)
  - Utforske, finne feil (Exploratory Data Analysis)
    [DataExplorer](https://cran.r-project.org/web/packages/DataExplorer/vignettes/dataexplorer-intro.html)
  - Vaske data (filter)
  - Lage “likt” format fra ulike utstyrstyper (mutate, select)
  - Sette sammen data (dplyr::left\_join)
  - Analyser (summarise, ggplot)

# Hente data fra trafikkdata-APIet

Et kapittel for seg… :)

## Timetrafikk

Fra trafikkdata.no kan vi eksportere CSV-filer eller hente rett fra
API-et.
