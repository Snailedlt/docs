---
title: Person  
headtitle: Begrepskatalog for Sikker digital post -  
group: Oppslagstjenesten/complexType  

sidebar:
redirect_from: /ot_person
---
| --- | --- |
| Identifikator | <http://begrep.difi.no/Oppslagstjenesten/5.0.0/5.0/Person> |
| Term | {{page.title}} |
| Definisjon | Person slik den er definert i kontakt og reservasjonsregisteret. |
| Datatype | complexType |
| Kilde | DIFI |
| Kommentar | Person er en Innbygger utlevert fra kontakt og reservasjonsregisteret. [status]({{site.baseurl}}/resources/begrep/felles/status) definerer om Person er registrert eller ikke i registreret. |

Merk at Person ikke er unik definert på tvers av Digdirs
felleskomponenter, men at hver av felleskomponentene har en definisjon
av Person i forhold til behovene i den enkelte felleskomponentene.

#### Datamodell

![Visualisering av datamodellen]({{site.baseurl}}/resources/begrep/oppslagstjenesten/uml_diagram_oppslagstjenesten_ekstern.jpg)

#### Attributer

| Term                                                                    | Kardinalitet |
| ----------------------------------------------------------------------- | ------------ |
| [personidentifikator]({{site.baseurl}}/resources/begrep/sikkerDigitalPost/begrep/personidentifikator)                      | 1..1         |
| [reservasjon]({{site.baseurl}}/resources/begrep/sikkerDigitalPost/begrep/reservasjon)                                      | 0..1         |
| [status]({{site.baseurl}}/resources/begrep/felles/status)                                                | 0..1         |
| [varslingsstatus]({{site.baseurl}}/resources/begrep/felles/varslingsstatus)                 | 0..1         |
| [Kontaktinformasjon]({{site.baseurl}}/resources/begrep/oppslagstjenesten/Kontaktinformasjon)             | 0..1         |
| [SikkerDigitalPostAdresse]({{site.baseurl}}/resources/begrep/oppslagstjenesten/SikkerDigitalPostAdresse) | 0..1         |
| [X509Sertifikat]({{site.baseurl}}/resources/begrep/sikkerDigitalPost/begrep/x509Sertifikat)                                | 0..1         |

#### Kodeverk for status

[status]({{site.baseurl}}/resources/begrep/felles/status) kan ha følgende verdi:

| Kodeverdi        | Beskrivelse                      |
| ---------------- | -------------------------------- |
| AKTIV            | Person finnes i registeret       |
| SLETTET          | Person er slettet fra registeret |
| IKKE\_REGISTRERT | Person finnes ikke i registeret  |

Ved AKTIV levers alle felter på Person ut.

Ved SLETTET og IKKE\_REGISTRERT har ikke registeret informasjon om
Kontaktinfo eller PostkasseInfo eller Sertifikat, og vil ikke kunne
levere ut disse elementene selv om det er spesifisert i
informasjonsbehov fra Offentlig virksomhet.

For oppslag av Person(er) er alle statuskoder relevante.  
For oppslag på endringer er kun status AKTIV og SLETTET relevant.

#### varslingsstatus

Ved å angi informasjonsbehov VarslingsStatus vil varslingstatus bli lagt
på Person i responsen. Ved verdi KAN\_IKKE\_VARSLES på varslingstatus
vil elementene Kontaktinformasjon, SikkerDigitalPostAdresse og
X509Sertifikat filtreres bort og dermed ikke være med i responsen.
Dersom varslingsstatus er lik KAN\_VARSLES vil disse elementene være
inkludert i responsen. varslingsstatus elementet vil ikke bli lagt på
Person i responsen om det ikke er etterspurt i requesten ved å legge inn
informasjonsbehov “VarslingsStatus”.

| Request                           | Datofelter i KRR | Utleverte \<InformasjonsBehov\> |                   |                |                    |
| --------------------------------- | ---------------- | ------------------------------- | ----------------- | -------------- | ------------------ |
| Metode                            |                  | Kontaktinfo                     | SikkerDigitalPost | Sertifikat     | VarslingsStatus    |
| HentPerson                        | \< 18 mnd        | utleveres                       | utleveres         | utleveres      | KAN\_VARSLES       |
| HentPerson                        | \> 18 mnd        | utleveres ikke                  | utleveres ikke    | utleveres ikke | KAN\_IKKE\_VARSLES |
| HentPerson (uten varslingsstatus) | vilkårlig        | utleveres                       | utleveres         | utleveres      | utleveres ikke     |
| HentEndringer (lokal kopi)        | vilkårlig        | utleveres                       | utleveres         | utleveres      | utleveres ikke     |

#### Xml eksempler

```
brush: xml; toolbar: false
<ns2:Person>
    <ns2:personidentifikator>010122*****</ns2:personidentifikator>
    <ns2:reservasjon>JA</ns2:reservasjon>
    <ns2:status>AKTIV</ns2:status>
    <ns2:varslingsstatus>KAN_VARSLES</ns2:varslingsstatus>
    <ns2:Kontaktinformasjon>
       <ns2:Mobiltelefonnummer sistOppdatert="2014-02-25T13:08:00.000+01:00" sistVerifisert="2013-10-21T10:09:28.000+02:00">12121212</ns2:Mobiltelefonnummer>
       <ns2:Epostadresse sistOppdatert="2014-02-25T13:08:00.000+01:00" sistVerifisert="2013-10-21T10:09:28.000+02:00">010122*****_test@minid.difi.no</ns2:Epostadresse>
    </ns2:Kontaktinformasjon>
    <ns2:SikkerDigitalPostAdresse>
       <ns2:postkasseadresse>1</ns2:postkasseadresse>
       <ns2:postkasseleverandoerAdresse>012345678</ns2:postkasseleverandoerAdresse>
    </ns2:SikkerDigitalPostAdresse>
    <ns2:X509Sertifikat>MIIC2jCCAkMCAg38MA0GCSqGSIb3DQEBBQUAMIGbMQswCQYDVQQGEwJKUDEOMAwGA1UECBMFVG9reW8xEDAOBgNVBAcTB0NodW8ta3UxETAPBgNVBAoTCEZyYW5rNEREMRgwFgYDVQQLEw9XZWJDZXJ0IFN1cHBvcnQxGDAWBgNVBAMTD0ZyYW5rNEREIFdlYiBDQTEjMCEGCSqGSIb3DQEJARYUc3VwcG9ydEBmcmFuazRkZC5jb20wHhcNMTIwODIyMDUyNzQxWhcNMTcwODIxMDUyNzQxWjBKMQswCQYDVQQGEwJKUDEOMAwGA1UECAwFVG9reW8xETAPBgNVBAoMCEZyYW5rNEREMRgwFgYDVQQDDA93d3cuZXhhbXBsZS5jb20wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC0z9FeMynsC8+udvX+LciZxnh5uRj4C9S6tNeeAlIGCfQYk0zUcNFCoCkTknNQd/YEiawDLNbxBqutbMDZ1aarys1a0lYmUeVLCIqvzBkPJTSQsCopQQ9V8WuT252zzNzs68dVGNdCJd5JNRQykpwexmnjPPv0mvj7i8XgG379TyW6P+WWV5okeUkXJ9eJS2ouDYdR2SM9BoVW+FgxDu6BmXhozW5EfsnajFp7HL8kQClI0QOc79yuKl3492rH6bzFsFn2lfwWy9ic7cP8EpCTeFp1tFaD+vxBhPZkeTQ1HKx6hQ5zeHIB5ySJJZ7af2W8r4eTGYzbdRW24DDHCPhZAgMBAAEwDQYJKoZIhvcNAQEFBQADgYEAQMv+BFvGdMVzkQaQ3/+2noVz/uAKbzpEL8xTcxYyP3lkOeh4FoxiSWqy5pGFALdPONoDuYFpLhjJSZaEwuvjI/TrrGhLV1pRG9frwDFshqD2Vaj4ENBCBh6UpeBop5+285zQ4SI7q4U9oSebUDJiuOx6+tZ9KynmrbJpTSi0+BM=</ns2:X509Sertifikat>
</ns2:Person>
```

Person med utgått kontaktinformasjon:

```
brush: xml; toolbar: false
<ns2:Person>
    <ns2:personidentifikator>010122*****</ns2:personidentifikator>
    <ns2:reservasjon>NEI</ns2:reservasjon>
    <ns2:status>AKTIV</ns2:status>
    <ns2:varslingsstatus>KAN_IKKE_VARSLES</ns2:varslingsstatus>
</ns2:Person>
```
