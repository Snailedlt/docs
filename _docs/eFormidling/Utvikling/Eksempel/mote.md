---
title: Eksempel på møte til eInnsyn
description: ""
summary: ""
product: eFormidling
sidebar: eformidling_sidebar
---

Denne siden viser et eksempel på møte til eInnsyn.

1. TOC
{:toc}

## Sende meldinger

### Opprett standard business document (SBD) for meldingen

```
curl -XPOST http://localhost:9093/api/messages/out \
-H 'Content-Type: application/json' -d \
'{
    "standardBusinessDocumentHeader": {
        "headerVersion": "1.0",
        "receiver": [{
                "identifier": {
                    "value": "0192:991825827",
                    "authority": "iso6523-actorid-upis"
                }
            }
        ],
        "documentIdentification": {
            "standard": "urn:no:difi:einnsyn:xsd::publisering",
            "typeVersion": "1.0",
            "type": "publisering"
        },
        "businessScope": {
            "scope": [{
                    "type": "ConversationId",
                    "identifier": "urn:no:difi:profile:einnsyn:journalpost:ver1.0"
                }
            ]
        }
    },
    "publisering": {
        "orgnr": "986252932",
    }
}'
```

### Legg ved filen mote.json

```
curl -XPUT http://localhost:9093/api/messages/out/93f530e3-0d4f-4273-94cd-e0d64019ea83 \
-H 'Content-Type: application/json' \
-H 'Content-Disposition: attachment; name=Mote; filename=mote.json' -d \
'{
    "@context": {
        "@base": "http://data.einnsyn.no/noark5/",
        "arkiv": "http://www.arkivverket.no/standarder/noark5/arkivstruktur/",
        "xsd": "http://www.w3.org/2001/XMLSchema#"
    },
    "@graph": [{
            "@id": "../møtemappe-uuid",
            "@type": "arkiv:Moetemappe",
            "arkiv:systemID": "møtemappe-uuid",
            "arkiv:moetedato": {
                "@type": "xsd:dateTime",
                "@value": "2021-09-25T18:00:00.000+02:00"
            },
            "arkiv:moetenummer": "999",
            "arkiv:moetested": "Teams, Møterom 066 Leikanger",
            "arkiv:offentligTittel": "Møte i Quizutvalget",
            "arkiv:offentligTittel_LIST": {
                "@list": ["Møte", "Quiz"]
            },
            "arkiv:offentligTittel_SENSITIV": "Møte Quiz - Sensitiv",
            "arkiv:tittel": "Møte Quiz",
            "arkiv:utvalg": "Quizutvalget",
            "arkiv:videolink": ["https://oslo.kommunetv.no/archive/269", "https://oslo.kommunetv.no/archive/268"]
        }, {
            "@id": "../møteredokregistrering-innkalling-uuid",
            "@type": "arkiv:Møtedokumentregistrering",
            "arkiv:systemID": "møteredokregistrering-innkalling-uuid",
            "arkiv:administrativEnhet": "BridgeUtvalget",
            "arkiv:parent": {
                "@id": "../møtemappe-uuid"
            },
            "arkiv:møtedokumentregistreringstype": {
                "@id": "arkiv:innkalling"
            },
            "arkiv:tittel_SENSITIV": "Møtedokumenter",
            "arkiv:offentligTittel": "Møtedokumenter",
            "arkiv:offentligTittel_LIST": {
                "@list": ["Møtedokumenter"]
            },
            "arkiv:offentligTittel_SENSITIV": "Møtedokumenter Tittel sensitiv",
            "arkiv:dokumentbeskrivelse": {
                "@id": "dokumentbeskrivelse-innkalling-uuid"
            }
        }, {
            "@id": "dokumentbeskrivelse-innkalling-uuid",
            "@type": "arkiv:Dokumentbeskrivelse",
            "arkiv:systemID": "dokumentbeskrivelse-innkalling-uuid",
            "arkiv:beskrivelse": "Innkallelse",
            "arkiv:dokumentnummer": {
                "@type": "xsd:integer",
                "@value": "177093"
            },
            "arkiv:dokumenttype": "Innkallelse",
            "arkiv:tilknyttetAv": "N/A",
            "arkiv:tilknyttetDato": {
                "@type": "xsd:dateTime",
                "@value": "2018-04-25T00:00:00.000+02:00"
            },
            "arkiv:tilknyttetRegistreringSom": {
                "@id": "arkiv:hoveddokument"
            },
            "arkiv:tittel": "Møteinnkallelse Quizutvalg møte",
            "arkiv:tittel_LIST": {
                "@list": ["Møteinnkallelse", "Quizutvalg", "møte"]
            },
            "arkiv:tittel_SENSITIV": "Møteinnkallelse Quizutvalg møte sensitiv",
            "arkiv:dokumentobjekt": {
                "@id": "dokumentobjekt-innkalling-uuid"
            }
        }, {
            "@id": "dokumentobjekt-innkalling-uuid",
            "@type": "arkiv:Dokumentobjekt",
            "arkiv:format": "pdf",
            "arkiv:opprettetDato": {
                "@type": "xsd:dateTime",
                "@value": "2018-04-26T12:15:12.000+02:00"
            },
            "arkiv:referanseDokumentfil": "https://www.arkivverket.no/forvaltning-og-utvikling/noark-standarden/noark-5/noark5-standarden/_/attachment/download/f52e37da-31ed-4bf0-9fbf-69f0357aa25c:025a30b602a65d74377b9e0c22a0f2fb8eab84df/Noark5v4%20vedl1%20Metadatakatalog.pdf",
            "arkiv:variantformat": {
                "@id": "arkiv:arkivformat"
            },
            "arkiv:versjonsnummer": {
                "@type": "xsd:integer",
                "@value": "1"
            }
        }
    ]
}'
```

### Send meldingen fra integrasjonspunktet

```
curl -XPOST http://localhost:9093/api/messages/out/93f530e3-0d4f-4273-94cd-e0d64019ea83
```

### Følg med på status for meldingen

```
curl http://localhost:9093/api/statuses/93f530e3-0d4f-4273-94cd-e0d64019ea83
```

### Motta og slett kvittering

```
curl http://localhost:9093/api/messages/in/peek?process=urn:no:difi:profile:einnsyn:response:ver1.0
curl -XDELETE 'http://localhost:9093/api/messages/in/9e1ad87d-256d-46f6-ae5f-5dfabb0246af
```

## Neste steg

- Funksjonell beskrivelse av [Møte til eInnsyn](../../Funksjonalitet/mote)
- Dokumenttypen [Publisering](../Dokumenttyper/publisering)
- Grensesnittet [eFormidling 2](../integrasjonspunkt_eformidling2_api)
- Flere [Eksempler](./)
