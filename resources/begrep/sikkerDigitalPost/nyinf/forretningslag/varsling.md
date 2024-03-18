---
title: Varsling
permalink: dpi_varsling.html
sidebar: dpi_timo_sidebar
---

| --- | --- |
| Innbyggerstyrt varsling | Postkasseleverandørene varsler innbygger i henhold til innbyggers egne varslingspreferanser (varslingsinnstillinger i postkassen) |
| Avsenderstyrt varsling | Varslinger en virksomhet bestiller fra postkasseleverandøren. Hos Digipost kommer disse i tillegg til innbyggerstyrt varsling. Hos e-Boks blir innbyggerstyrt varsling overstyrt av avsenderstyrt varsling. OBS! Det er viktig at avsendere unngår bruk av personopplysninger og sensitive opplysninger i [varslingstekst]({{site.baseurl}}/resources/begrep/sikkerDigitalPost/begrep/varslingsTekst), da sms og epost-varsling går ukryptert til mottaker |
| Utsending | Varslinger i digital postkasse til innbyggere sendes kun på dagtid |
| Kanal | Virksomhetene tilknyttet til digital postkassse til innbygger kan bestille varsling på e-post og/eller sms. Hvilken kanal som velges avgjøres både av virksomhetens kanalstrategi og av hvilke opplysninger som finnes i kontakt og reservasjonsregisteret for den enkelte innbygger. Postkasseleverandørene kan ha flere varslingskanaler utover e-post og sms, f.eks. bruk av meldinger direkte til en applikasjon på mobilen |
| Kontaktinformasjon | Avsendere kan varsle innbygger ut fra kontaktinformasjon som innbygger selv har lagt til i [kontakt-og reservasjonsregisteret]({{site.baseurl}}/docs/Kontaktregisteret/). Dette kan være epost til oppgitt [epostaddresse]({{site.baseurl}}/resources/begrep/oppslagstjenesten/Epostadresse) og/eller sms til oppgitt [mobiltelefonnummer]({{site.baseurl}}/resources/begrep/felles/mobiltelefonnummer) |
| Kommentar | Varslinger i digital postkasse til innbyggere sendes kun til Innbygger dersom innbygger ikke har gjort seg kjent med brevet. Det vil si at varslinger bestilt av virksomheter kun blir sendt Innbygger dersom innbygger ikke har vært inn i postkassen og behandlet brevet |

<!--- 
- [Når skal avsendere varsle innbygger om digitale forsendelser?](https://samarbeid.difi.no/felleslosninger/digital-postkasse-til-innbyggere/dokumentasjon/hvordan-skal-jeg-bruke-varsling-i-digital-postkasse) (artikkel i samarbeidsportalen)
 --->
 
- Avsenderstyrt varsling settes på meldingsnivå i schema [Digital](https://docs.digdir.no/schemas/dpi/innbyggerpost_dpi_digital_1_0.schema.json) og er en del av en [forretningsmeldingen](https://docs.digdir.no/dpi_skjema.html#forretningsmelding-schema)

- Beskrivelse av [varslingsinnstillinger (med eksempler)]({{site.baseurl}}/resources/begrep/sikkerDigitalPost/begrep/Varsler)

### Bruk av lenker (URL) i varsler via SMS og/eller e-post

Grunnet økning i svindel via usikre kanaler, som SMS og e-post, anbefaler Digitaliseringsdirektoratet å unngå all bruk av lenker i varsler. Se innlegg om [temaet](https://samarbeid.digdir.no/digital-postkasse/lenke-eller-ikke-det-er-sporsmalet/1525).
