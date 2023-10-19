---
title: Krav og testbeskrivelser
description: ""
summary: ""
product: eFormidling
sidebar: eformidling_sidebar
---

Formålet med denne siden er å gi en oversikt over krav til integrasjoner mot eFormidling, med tilhørende testbeskrivelser.

Informasjon om nødvendig testoppsett finnes på [Kom i gang med testing](./).

1. TOC
{:toc}

## Felles krav

Disse kravene gjelder uavhengig av hvilke prosess(er) som støttes.

### Støtter visning av siste status for sendt melding (MÅ)

1. Verifiser at bruker som sendte meldingen kan se siste status for denne

### Støtter varsling av avsender for meldinger som får status feilet eller levetid utløpt (MÅ)

1. Fyll inn utilstrekkelige eller feil metadata for melding
2. Send melding til en mottaker som bruker eFormidling
3. Verifiser at meldingen blir markert som feilet
4. Verifiser at bruker som sendte meldingen får beskjed om at melding feilet uten å kreve at bruker selv aktivt sjekker status for meldingen

Verifiser at følgende kategorier feil håndteres:

- synkron feil, for eksempel dersom adresseoppslag feiler, send f.eks. til adresse som ikke finnes
- asynkron feil, for eksempel dersom autentisering feiler mot aktuell meldingstjeneste, legg f.eks. inn feil brukernavn for meldingstjenesten i konfigurasjonen før en sender melding
- levetid utløpt, for eksempel dersom mottaker lar være/ikke klarer å behandle melding, send f.eks. til qa-integrasjonspunkt og vent til levetid utløper

Verifiser at systemet følger med på asynkrone statuser (inkludert feil-statuser) knyttet til en melding helt til den har fått en av følgende statuser: `levert`, `feil` eller `levetid utløpt`. Merk at statusen `lest` vil kunne komme flere dager og uker etter at meldingen er sendt og at en derfor må polle over et udefinert tidsrom dersom denne ønskes.

### Støtter visning av sendte meldinger og status for disse (MÅ)

1. Fyll inn utilstrekkelige eller feil metadata for melding
2. Send melding til en mottaker som bruker eFormidling
3. Verifiser at bruker selv kan vise en liste over forsendelser som har feilet
4. Verifiser at den feilede meldingen er i denne listen

### Bruker grensesnittet eFormidling 2 som beskrevet i dokumentasjonen (MÅ)

1. Verifiser at integrasjonspunktets API (eFormidling 2) brukes
2. Verifiser at integrasjonspunktets gamle API (BEST/EDU) ikke brukes
3. Verifiser at en sender meldinger med en av strategiene som er beskrevet på [Integrasjonspunktets API (eFormidling 2)](../Utvikling/integrasjonspunkt_eformidling2_api)
4. Verifiser at en følger med på status for sendte meldinger med en av strategiene som er beskrevet på [Integrasjonspunktets API (eFormidling 2)](https://docs.digdir.no/docs/eFormidling/Utvikling/integrasjonspunkt_eformidling2_api)
5. Verifiser at en mottar meldinger med en av strategiene som er beskrevet på [Integrasjonspunktets API (eFormidling 2)](../Utvikling/integrasjonspunkt_eformidling2_api)
6. Verifiser at en har lagt til rette for feilsøking ved å oppgi navn og versjon for eget system ved oppretting av melding
7. Verifiser at en ikke bruker ettstegs strategi for sending av små meldinger dersom en skal sende meldinger over 5 MB
8. Verifiser at polling brukes ved mottak av innkommende statuser (webhook-abonnement er bare et supplement)
9. Verifiser at polling brukes ved mottak av innkommende meldinger (webhook-abonnement er bare et supplement)
10. Verifiser at en ikke behandler vellykket bekreftelse på at melding er lagt på kø for sending som at meldingen er sendt eller levert vellykket
11. Verifiser at en ikke behandler vellykket bekreftelse på at melding er sendt som at meldingen er levert vellykket
12. Verifiser at en kan motta så store meldinger som beskrevet i terskelverdiene som er beskrevet under [eFormidlings egenskaper](../Egenskaper/)
13. Verifiser at en kan sende så store meldinger som beskrevet i terskelverdiene som er beskrevet under [eFormidlings egenskaper](../Egenskaper/)
14. Verifiser at det ikke er mulig å sende meldinger som overskrider terskelverdiene som er beskrevet under [eFormidlings egenskaper](../Egenskaper/)

### Dersom på-vegne-av brukes, så er dette oppsettet testet (MÅ)

Se gjerne [på vegne av](../Utvikling/pa_vegne_av).

1. Verifiser at aktuelle tester er gjennomført med på-vegne-av-oppsett

### Dersom kanal brukes, så er dette oppsettet testet (MÅ)

Se gjerne [kanal](../Utvikling/kanal).

1. Verifiser at aktuelle tester er gjennomført med kanal-oppsett

### Produserer og konsumerer meldinger som forventet (MÅ)

1. Verifiser at kommunikasjon fungerer også med andre system enn ens egen
2. Verifiser at spesialtegn fungerer som forventet i titler, filnavn, osv
3. Verifiser at begrensninger som lengder på tekstfelt fungerer som forventet
   - Se begrensninger for [dokumenttypene](../Utvikling/Dokumenttyper/standard_arkivmelding)
   - Se begrensninger for [Integrasjonspunktets API (eFormidling 2)](../Utvikling/integrasjonspunkt_eformidling2_api)
5. Verifiser at sending og mottak fungerer når bare påkrevd informasjon er oppgitt
6. Verifiser at sending og mottak fungerer når all mulig informasjon er oppgitt
7. Verifiser at kommunikasjon fungerer med ønskede filstørrelser
8. Verifiser at kommunikasjon fungerer med ønskede filformat
9. Verifiser at gyldige meldinger produseres både når all informasjon er oppgitt og når bare påkrevd informasjon er oppgitt
10. Verifiser at innkommende meldinger som mangler påkrevd informasjon likevel ikke avvises
11. Verifiser at en ikke sender filer med navn som inneholder tegn som ikke fungerer bra i filnavn, for eksempel kolon

## Krav til eventuell drift av integrasjonspunkt

Disse kravene gjelder eventuell drift av integrasjonspunkt.

### Har tilfredsstillende tilgangskontroll og sikring av grensesnitt, meldinger og hemmeligheter (MÅ)

1. Verifiser at installasjon og konfigurasjon er gjort i henhold til beskrivelser
2. Verifiser at transport er tilstrekkelig sikret, f.eks. med hjelp av transportsikring
3. Verifiser at tilgang til grensesnittet er tilstrekkelig sikret, f.eks. med hjelp av HTTP basic auth
4. Verifiser at hemmeligheter beskyttes tilfredsstillende, f.eks. med hjelp av Hashicorp Vault
5. Verifiser at integrasjonspunktets grensesnitt bare er tilgjengelig for autoriserte brukere og system

### Har rutiner for å holde integrasjonspunktet oppdatert (MÅ)

1. Verifiser at det finnes en rutine for jevnlig oppdatering av integrasjonspunktet

### Har automatiserte rutiner for å holde integrasjonspunktet oppdatert (KAN)

1. Verifiser at automatisk oppdatering er konfigurert
2. Verifiser at oppdateringstidspunkt er gjennomtenkt

## Saksbehandling

Disse kravene gjelder dersom [saksbehandling](../Funksjonalitet/saksbehandling) støttes.

### Støtter sending til mottakere med eFormidling (DPO) (MÅ)

1. Fyll inn ønsket metadata for melding (husk 1.7)
2. Send melding til en mottaker som bruker eFormidling
3. Verifiser at meldingen blir markert som sendt
4. Verifiser at meldingen kommer frem til mottaker
5. Verifiser at innholdet hos mottaker er som forventet (husk 1.7)
6. Verifiser at meldingen blir markert som mottatt og etter hvert levert
7. Marker melding som lest hos mottaker (varierer fra system til system hvordan - f.eks. først ved tilordning av saksnummer)
8. Verifiser at meldingen blir markert som lest

### Støtter sending til mottakere med KS SvarUt/SvarInn (DPF) (MÅ)

1. Fyll inn ønsket metadata for melding (husk 1.7)
2. Send melding til en mottaker som bruker KS SvarUt/SvarInn
3. Verifiser at meldingen blir markert som sendt
4. Verifiser at meldingen kommer frem til mottaker
5. Verifiser at innholdet hos mottaker er som forventet (husk 1.7)
6. Verifiser at meldingen blir markert som mottatt og etter hvert levert
7. Marker melding som lest hos mottaker (varierer fra system til system hvordan - f.eks. først ved tilordning av saksnummer)
8. Verifiser at meldingen blir markert som lest

### Støtter sending til mottakere med Altinn Digital Post (DPV) (MÅ)

1. Fyll inn ønsket metadata for melding (husk 1.7)
2. Send melding til en mottaker som bruker Altinn Digital Post
3. Verifiser at meldingen blir markert som sendt
4. Verifiser at meldingen kommer frem til mottaker
5. Verifiser at innholdet hos mottaker er som forventet (husk 1.7)
6. Verifiser at meldingen blir markert som mottatt og etter hvert levert
7. Marker melding som lest hos mottaker (varierer fra system til system hvordan - f.eks. først ved tilordning av saksnummer)
8. Verifiser at meldingen blir markert som lest

### Støtter mottak fra avsendere med eFormidling (DPO) (MÅ)

1. Fyll inn ønsket metadata for melding i et system som bruker eFormidling (husk 1.7)
2. Send melding til mottaker som bruker eget system (systemet som testes)
3. Verifiser at meldingen blir markert som sendt hos avsender
4. Verifiser at meldingen kommer frem til mottaker
5. Verifiser at innholdet hos mottaker er som forventet (husk 1.7)
6. Verifisert at meldingen blir markert som mottatt og etter hvert levert hos avsender
7. Marker melding som lest hos mottaker
8. Verifiser at meldingen blir markert som lest hos avsender

### Støtter mottak fra avsendere med KS SvarUt/SvarInn (DPF) (MÅ)

1. Fyll inn ønsket metadata for melding i et system som bruker KS SvarUt (husk 1.7)
2. Send melding til mottaker som bruker eget system (systemet som testes)
3. Verifiser at meldingen blir markert som sendt i KS SvarUt
4. Verifiser at meldingen kommer frem til mottaker
5. Verifiser at innholdet hos mottaker er som forventet (husk 1.7)
6. Verifisert at meldingen blir markert som mottatt og etter hvert levert i KS SvarUt
7. Marker melding som lest hos mottaker
8. Verifiser at meldingen blir markert som lest i KS SvarUt

### Støtter å motta svar direkte på sak og journalpost (BØR)

1. Fyll inn ønsket metadata for melding
2. Send melding til en mottaker som bruker eFormidling
3. Verifiser at meldingen kommer frem til mottaker
4. Svar på meldingen fra mottakers system
5. Verifiser at svaret kommer frem, koblet til sak og journalpost som forventet

### Støtter å sende svar direkte til sak og journalpost (BØR)

1. Fyll inn ønsket metadata for melding i et system som bruker eFormidling
2. Send melding til mottaker som bruker eget system (systemet som testes)
3. Verifiser at meldingen kommer frem til mottaker
4. Svar på meldingen fra mottaker
5. Verifiser at svaret kommer frem, koblet til sak og journalpost som forventet

## Taushetsbelagt saksbehandling

Disse kravene gjelder dersom [taushetsbelagt saksbehandling](../Funksjonalitet/taushetsbelagt_saksbehandling) støttes.

Taushetsbelagt saksbehandling følger tilsvarende flyt som saksbehandling, med noen tilleggskrav.

1. [Krav og testbeskrivelser for Saksbehandling](#saksbehandling)
2. Tillegg![image](https://github.com/felleslosninger/docs/assets/785457/6c36eae0-8663-4019-afd3-b2e1801548a7)
skrav for taushetsbelagt saksbehandling
   - Verifiser at det er mulig å markere melding som taushetsbelagt
   - Verifiser at det er mulig å oppgi DPV varslingstekst for taushetsbelagt melding

## Vedtak til innbyggere

Disse kravene gjelder dersom [vedtak til innbyggere](../Funksjonalitet/vedtak_til_innbygger) støttes.

### Støtter sending til mottakere med DPI (MÅ)

1. Fyll inn ønsket metadata for melding (husk 1.7)
2. Verifiser at det er mulig å oppgi varslingstekst
3. Send melding til mottaker som bruker  DPI
4. Verifiser at meldingen blir markert som sendt
5. Verifiser at meldingen kommer frem til DPI
6. Verifiser at innholdet i DPI er som forventet (husk 1.7)
7. Verifiser at meldingen blir markert som mottatt og etter hvert levert

### Støtter sending til mottakere med Altinn Digital Post (DPV) (BØR)

1. Fyll inn ønsket metadata for melding (husk 1.7)
2. Verifiser at det er mulig å oppgi varslingstekst
3. Send melding til mottaker som bruker  DPV
4. Verifiser at meldingen blir markert som sendt
5. Verifiser at meldingen kommer frem til DPV
6. Verifiser at innholdet i DPV er som forventet (husk 1.7)
7. Verifiser at meldingen blir markert som mottatt og etter hvert levert

### Støtter sending til mottakere med postadresse (print) (BØR)

1. Fyll inn ønsket metadata for melding (husk 1.7)
2. Send melding til mottaker som verken bruker DPI eller DPV
3. Verifiser at meldingen blir markert som sendt
4. Verifiser at meldingen kommer frem til print
5. Verifiser at innholdet i print er som forventet (husk 1.7)
6. Verifiser at meldingen blir markert som mottatt og etter hvert levert

### Støtter sending til mottaker med postadresse (print) og ukjent fødselsnummer (BØR)

1. Fyll inn ønsket metadata for melding (husk 1.7)
2. Send melding til annen mottaker som verken bruker DPI eller DPV
3. Verifiser at meldingen blir markert som sendt
4. Verifiser at meldingen kommer frem til print
5. Verifiser at innholdet i print er som forventet (husk 1.7)
6. Verifiser at meldingen blir markert som mottatt og etter hvert levert

### Støtter DPI-utvidelsen "lenke utenfor brev" (KAN)

1. Fyll inn ønsket metadata for melding (husk 1.7)
2. Send melding til annen mottaker som bruker DPI
3. Verifiser at meldingen blir markert som sendt
4. Verifiser at meldingen kommer frem til DPI
5. Verifiser at innholdet i meldingen er som forventet (husk 1.7)![image](https://github.com/felleslosninger/docs/assets/785457/6dc0c936-6f20-45a6-accf-97f044fae70d)
![image](https://github.com/felleslosninger/docs/assets/785457/19ab6db0-49b5-45c4-9c38-78714ed18d56)

6. Verifiser at lenke utenfor brev fungerer som forventet

### Støtter DPI-utvidelsen "bevis" (KAN)

1. Fyll inn ønsket metadata for melding (husk 1.7)
2. Send melding til annen mottaker som bruker DPI
3. Verfiser at meldingen blir markert som sendt
4. Verifiser at meldingen kommer frem til DPI
5. Verifiser at innholdet i meldingen er som forventet (husk 1.7)
6. Verifiser at bevis fungerer som forventet

### Støtter DPI-utvidelsen "arrangement" (KAN)

1. Fyll inn ønsket metadata for melding (husk 1.7)
2. Send melding til annen mottaker som bruker DPI
3. Verfiser at meldingen blir markert som sendt
4. Verifiser at meldingen kommer frem til DPI
5. Verifiser at innholdet i meldingen er som forventet (husk 1.7)
6. Verifiser at arrangement fungerer som forventet

### Støtter konfigurasjon av avsenderidentifikator for DPI (BØR)

1. Verifiser at det er mulig å konfigurere avsenderidentifikator for DPI

## Publisering av møte til eInnsyn

Disse kravene gjelder dersom [publisering av møte til eInnsyn](../Funksjonalitet/mote) støttes.

### Støtter publisering av møte til eInnsyn (MÅ)

1. Fyll inn ønsket metadata for melding (husk 1.7)
2. Send melding til eInnsyn
3. Verifiser at meldingen blir markert som sendt
4. Verifiser at meldingen kommer frem til eInnsyn
5. Verifiser at innholdet i eInnsyn er som forventet (husk 1.7)
6. Verifiser at meldingen blir markert som mottatt og etter hvert levert

## Publisering av journalpost til eInnsyn

Disse kravene gjelder dersom [publisering av journalpost til eInnsyn](../Funksjonalitet/journalpost) støttes.

### Støtter publisering av journalpost til eInnsyn (MÅ)

1. Fyll inn ønsket metadata for melding (husk 1.7)
2. Send melding til eInnsyn
3. Verifiser at meldingen blir markert som sendt
4. Verifiser at meldingen kommer frem til eInnsyn
5. Verifiser at innholdet i eInnsyn er som forventet (husk 1.7)
6. Verifiser at meldingen blir markert som mottatt og etter hvert levert

## Mottak av innsynskrav fra eInnsyn

Disse kravene gjelder dersom [mottak av innsynskrav fra eInnsyn](../Funksjonalitet/innsynskrav) støttes.

### Støtter mottak av innsynskrav fra eInnsyn (MÅ)

1. Send innsynskrav fra eInnsyn
2. Verifiser at innsynskravet kommer frem
3. Verifiser at innholdet i innsynskravet er som forventet (husk 1.7)
