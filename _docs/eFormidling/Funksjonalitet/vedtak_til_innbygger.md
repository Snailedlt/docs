---
title: Vedtak til innbygger
description: ""
summary: ""
product: eFormidling
sidebar: eformidling_sidebar
---

eFormidling lar din virksomhet sende vedtak og andre viktige henvendelser til innbygger.

1. TOC
{:toc}

## Introduksjon

Forvaltningsloven definerer et vedtak som _en avgjørelse som treffes under utøving av offentlig myndighet og som
generelt eller konkret er bestemmende for rettigheter eller plikter til private personer (enkeltpersoner eller andre
private rettssubjekter)_. Et vedtak er et resultat av en saksbehandling. Forvaltningsloven stiller krav til
innhold i et vedtak og hvordan et vedtak skal kommuniseres. eForvaltningsforskriften og Digitaliseringsrundskrivet
stiller ytterlige krav til hvordan et vedtak skal kommuniseres digitalt.

Krav til varsling:
> Virksomheten skal bruke kontaktinformasjon fra kontakt- og reservasjonsregisteret ved varsling av innbyggere om og
> utsendelse av enkeltvedtak og andre viktige digitale henvendelser, jf. eForvaltningsforskriften § 8.
>
> [Digitaliseringsrundskrivet](https://www.regjeringen.no/no/dokumenter/digitaliseringsrundskrivet/id2895185/) (ekstern lenke)

> Informasjonssystemet skal registrere tidspunktet for når parten har skaffet seg tilgang til enkeltvedtaket, og data
> som bekrefter at vedkommende har rett til å gjøre seg kjent med vedtaket. Har parten ikke skaffet seg tilgang til
> enkeltvedtaket innen én uke fra det tidspunktet vedtaket ble gjort tilgjengelig, og varsel ble sendt, skal parten
> varsles en gang til i samsvar med tredje ledd.
>
> [eForvaltningsforskriften](https://lovdata.no/forskrift/2004-06-25-988/§8) (ekstern lenke)

Krav til bruk av Digital Post til Innbyggere:
> Virksomheten skal bruke Digital postkasse til innbyggere for utsending av post til innbyggere som har valgt digital
> postkasse, og som ikke har reservert seg. Kravet om bruk av digital postkasse til innbyggere, gjelder alle tjenester
> hvor det sendes brev som har dokumentasjonsverdi for innbygger. Slike brev kan være både vedtak og andre viktige
> henvendelser. Virksomheten skal vurdere hvilke brev som har viktig dokumentasjonsverdi for innbygger.
>
> [Digitaliseringsrundskrivet](https://www.regjeringen.no/no/dokumenter/digitaliseringsrundskrivet/id2895185/) (ekstern lenke)

Mulighet til å bruke Altinn Digital Post for innbyggere uten digital postkasse:
> Virksomheter som ved etablering av Digital postkasse til innbyggere benyttet Altinns meldingsboks for utsending av
> post til innbyggere, skulle fra 1. oktober 2016 bruke Digital postkasse til innbyggere . Har innbyggeren ikke valgt
> postkasse og ikke reservert seg mot digital post, kan post fortsatt sendes til Altinns meldingsboks.
> 
> [Digitaliseringsrundskrivet](https://www.regjeringen.no/no/dokumenter/digitaliseringsrundskrivet/id2895185/) (ekstern lenke)

eFormidlings støtte for å sende vedtak og andre viktige henvendelser til innbygger gjør det enkelt å etterleve gjeldende
regelverk og retningslinjer.

Vedtak til innbygger representeres med følgende prosess:

| **Prosessnavn** | **Prosessidentifikator**                      |
|-----------------|-----------------------------------------------|
| Vedtak          | urn:no:difi:profile:digitalpost:vedtak:ver1.0 |

## Meldingsinnhold

Hvilket innhold som kan sendes avhenger av hvilke dokumenttyper mottakeren støtter for vedtak til innbygger. En
dokumenttype støttes av en eller flere meldingstjenester.

| **Dokumenttype**                                      | **Meldingstjenester**                                                                     |
|-------------------------------------------------------|-------------------------------------------------------------------------------------------|
| [Digital](../Utvikling/Dokumenttyper/digital)         | [Digital Post til Innbyggere](../Utvikling/Meldingstjenester/digital_post_til_innbyggere) |
| [Print](../Utvikling/Dokumenttyper/print)             | [Digital Post til Innbyggere](../Utvikling/Meldingstjenester/digital_post_til_innbyggere) |
| [Digital DPV](../Utvikling/Dokumenttyper/digital_dpv) | [Altinn Digital Post](../Utvikling/Meldingstjenester/altinn_digital_post)                 |

## Adressere meldinger

Meldinger adresseres fra avsenders organisasjonsnummer til mottakers fødselsnummer. For print kan mottakers fødselsnummer utelates dersom dette ikke er kjent eller dersom mottaker ikke har fødselsnummer.

For mottakere som har valgt digital postkasse foretrekkes denne. For mottakere som ikke har valgt postkasse må avsender
selv velge om meldingen kan sendes til Altinn Digital Post eller om den må sendes som fysisk post. Mottakere som er
reservert mot digital post eller som ikke kan varsles på grunn av manglende kontaktinformasjon skal i alle tilfeller
motta fysisk post. Ved sending av fysisk post kan avsender velge å bruke utskriftstjenesten i Digital Post til
Innbyggere eller håndtere disse meldingene med egen utskriftstjeneste.

<div class="mermaid">
graph LR
A{Reservert?}
B{Mulig å varsle?}
C{Har valgt<br>digital postkasse?}
D("a) Utskriftstjenesten i Digital Post til Innbyggere<br>b) Altinn Digital Post")
E(Digital Postkasse)
F(Utskriftstjenesten i Digital Post til Innbyggere)
A -->|Ja| F
A -->|Nei| B
B -->|Ja| C
B -->|Nei| F
C -->|Ja| E
C -->|Nei| D
</div>

Noen innbyggere kan ikke nås med disse meldingstjenestene. Dette gjelder for eksempel utenlandske innbyggere. I slike
tilfeller kan en likevel sende fysisk post til innbyggerene med hjelp av utskriftstjenesten i digital post til innbyggere (DPI).
Les mer om hvordan dette fungerer under:

- [Dokumenttype print](../../Utvikling/Dokumenttyper/print)

## Sende meldinger
Først gjøres et kapabilitetsoppslag for å se hvilke dokumenttyper mottakeren støtter. Dersom mer enn en dokumenttype kan
brukes må virksomhetens fagsystem bestemme hvilken. Virksomhetens fagsystem bygger så en melding med ønsket
dokumenttype. Til slutt sendes meldingen.

<div class="mermaid">
sequenceDiagram
participant A as Virksomhetens<br>fagsystem
participant B as Virksomhetens<br>integrasjonspunkt
participant C as Adressetjeneste
participant D as Digital Post til Innbyggere
participant E as Altinn Digital Post
A->>B: Kapabilitetsoppslag
B->>C: Kapabilitetsoppslag
A->>+B: Alt 1) Utgående melding *digital*
B->>-D: .
A->>+B: Alt 2) Utgående melding *print*
B->>-D: .
A->>+B: Alt 3) Utgående melding *digital_dpv*
B->>-E: .
</div>

Nærmere beskrivelse av de aktuelle meldingstjenestene finnes på:
- [Digital Post til Innbyggere](../Utvikling/Meldingstjenester/digital_post_til_innbyggere)
- [Altinn Digital Post](../Utvikling/Meldingstjenester/altinn_digital_post)

## Varsling

Avsenders system mottar statusmeldinger når en melding blir levert. Avsenders system mottar også statusmeldinger ved
feilsituasjoner og når en melding ikke blir levert innenfor den definerte levetiden. Avsenders system kan varsle
avsenderen om både vellykkede sendinger og avvik.

Ved mottak til Digital Post til Innbyggere kan innbyggeren varsles om mottak av melding. Varsel går til innbyggerens
registrert kontaktinformasjon i kontakt- og reservasjonsregisteret.

Ved mottak til Altinn Digital Post kan innbyggeren varsles om mottak av melding. Varsel går til innbyggerens
registrerte kontaktinformasjon i kontakt- og reservasjonsregisteret.

## Forutsetninger

- Grensesnittet eFormidling 2 må brukes (BEST/EDU støttes ikke)
- Bruk av Digital Post til Innbyggere krever avtale
- Bruk av Altinn Digital Post krever avtale (begrenset tilgjengelighet inntil videre)

## Konfigurasjon

Følgende konfigurasjon er nødvendig for full funksjonalitet:

- [Minimumskonfigurasjon av integrasjonspunktet](../installasjon/installasjon#minimumskonfigurasjon)
- [Konfigurasjon av Digital Post til Innbyggere](../installasjon/installasjon#konfigurere-digital-post-til-innbyggere-dpi)
- [Konfigurasjon av Altinn Digital Post](../installasjon/installasjon#konfigurere-altinn-digital-post-dpv)

Det er også støtte for delvis konfigurasjon. Delvis konfigurasjon medfører at en ikke når alle mottakere. For eksempel
kan en la være å konfigurere Altinn Digital Post dersom en ikke ønsker å nå mottakere som rutes til denne tjenesten.

## Utvikling

- [Eksempel på vedtak til innbygger](../Utvikling/Eksempel/vedtak_til_innbygger)
