---
title: "Dokumenttype: Print"
description: ""
summary: ""
product: eFormidling
sidebar: eformidling_sidebar
---

Dokumenttypen `print` består av et standard business document (SBD) og et eller flere dokument.

Dokumenttypen har identifikatoren `urn:no:difi:digitalpost:xsd:fysisk::print`.

1. TOC
{:toc}

## Standard business document

Alle dokumenttyper i eFormidling følger standarden `SBD` for adresseringsinformasjon. `SBD` består av en header (`SBDH`)
og en forretningsmelding som brukes for dokumenttype-spesifikk adresseringsinformasjon.

eFormidlings bruk av standarden `SBD` er beskrevet på [Standard business document](standard_sbd).

Dokumenttypen `print` adresseres fra avsenders organisasjonsnummer til mottakers fødselsnummer. Dersom mottakers
fødselsnummer er ukjent kan dette utelates. I slike tilfeller er det påkrevd å eksplisitt oppgi mottakers postadresse, fordi
eFormidling ellers ikke har nok opplysninger til å gjøre adresseoppslag. En kan dermed bruke `print` til å sende fysisk post
til utenlandske innbyggere og virksomheter.

### Forretningsmeldingen

Forretningsmeldingen `print` er beskrevet under.

> `print.hoveddokument` (påkrevd)
>
> Definerer hvilket vedlagt dokument som er hoveddokumentet.
>
> | Lovlige verdier                 | String        |
> | Standard verdi                  | Ingen         |
> | Konfigurasjon av standard verdi | Ikke støttet  |

> `print.avsenderId` (frivillig)
>
> Brukt for å identifisere en ansvarlig enhet innen for en virksomhet. Ved behov for avsenderidentifikator må dette
> bestilles fra Digdir.
>
> | Lovlige verdier                 | String        |
> | Standard verdi                  | Ingen         |
> | Konfigurasjon av standard verdi | Ikke støttet  |

> `print.utskriftsfarge` (frivillig)
>
> Betegnelse for hva slags print og utskriftstype som skal velges for dette brevet.
>
> | Lovlige verdier                 | `SORT_HVIT` eller `FARGE` |
> | Standard verdi                  | `SORT_HVIT`               |
> | Konfigurasjon av standard verdi | Ikke støttet              |

> `print.posttype` (frivillig)
>
> A-post eller B-post.
>
> | Lovlige verdier                 | `A_PRIORITERT` eller `B_OEKONOMI` |
> | Standard verdi                  | `B_OEKONOMI`                      |
> | Konfigurasjon av standard verdi | Ikke støttet                      |

> `print.retur.returhaandtering` (frivillig)
>
> Definerer hvordan fysisk post som ikke blir levert til mottaker skal håndteres.
>
> | Lovlige verdier                 | `DIREKTE_RETUR` eller `MAKULERING_MED_MELDING` |
> | Standard verdi                  | `DIREKTE_RETUR`                                |
> | Konfigurasjon av standard verdi | Ikke støttet                                   |

> `print.retur.mottaker.navn` (frivillig)
>
> Navn for mottaker av eventuell returpost.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Enhetsregisteret |
> | Konfigurasjon av standard verdi | Ikke støttet                |

> `print.retur.mottaker.adresselinje1` (frivillig)
>
> Adresselinje 1 for mottaker av eventuell returpost.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Enhetsregisteret |
> | Konfigurasjon av standard verdi | Ikke støttet                |

> `print.retur.mottaker.adresselinje2` (frivillig)
>
> Adresselinje 2 for mottaker av eventuell returpost.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Enhetsregisteret |
> | Konfigurasjon av standard verdi | Ikke støttet                |

> `print.retur.mottaker.adresselinje3` (frivillig)
>
> Adresselinje 3 for mottaker av eventuell returpost.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Enhetsregisteret |
> | Konfigurasjon av standard verdi | Ikke støttet                |

> `print.retur.mottaker.adresselinje4` (frivillig)
>
> Adresselinje 4 for mottaker av eventuell returpost.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Enhetsregisteret |
> | Konfigurasjon av standard verdi | Ikke støttet                |

> `print.retur.mottaker.postnummer` (frivillig)
>
> Postnummer for mottaker av eventuell returpost.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Enhetsregisteret |
> | Konfigurasjon av standard verdi | Ikke støttet                |

> `print.retur.mottaker.poststed` (frivillig)
>
> Poststed for mottaker av eventuell returpost.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Enhetsregisteret |
> | Konfigurasjon av standard verdi | Ikke støttet                |

> `print.retur.mottaker.land` (frivillig)
>
> Land for mottaker av eventuell returpost.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Enhetsregisteret |
> | Konfigurasjon av standard verdi | Ikke støttet                |



> `print.mottaker.navn` (frivillig)
>
> Navn for mottaker.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Folkeregisteret  |
> | Konfigurasjon av standard verdi | Ikke støttet                |

> `print.mottaker.adresselinje1` (frivillig)
>
> Adresselinje 1 for mottaker.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Folkeregisteret  |
> | Konfigurasjon av standard verdi | Ikke støttet                |

> `print.mottaker.adresselinje2` (frivillig)
>
> Adresselinje 2 for mottaker.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Folkeregisteret  |
> | Konfigurasjon av standard verdi | Ikke støttet                |

> `print.mottaker.adresselinje3` (frivillig)
>
> Adresselinje 3 for mottaker.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Folkeregisteret  |
> | Konfigurasjon av standard verdi | Ikke støttet                |

> `print.mottaker.adresselinje4` (frivillig)
>
> Adresselinje 4 for mottaker.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Folkeregisteret  |
> | Konfigurasjon av standard verdi | Ikke støttet                |

> `print.mottaker.postnummer` (frivillig)
>
> Postnummer for mottaker.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Folkeregisteret  |
> | Konfigurasjon av standard verdi | Ikke støttet                |

> `print.mottaker.poststed` (frivillig)
>
> Poststed for mottaker.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Folkeregisteret  |
> | Konfigurasjon av standard verdi | Ikke støttet                |

> `print.mottaker.land` (frivillig)
>
> Land for mottaker.
>
> | Lovlige verdier                 | String                      |
> | Standard verdi                  | Hentes fra Folkeregisteret  |
> | Konfigurasjon av standard verdi | Ikke støttet                |


| <nobr>print.mottaker.navn</nobr>                | Nei     | Navn for mottaker.                                                                | String                                         | Hentes fra Folkeregisteret  | Ikke støttet |
| <nobr>print.mottaker.adresselinje1</nobr>       | Nei     | Adresselinje 1 for mottaker.                                                      | String                                         | Hentes fra Folkeregisteret  | Ikke støttet |
| <nobr>print.mottaker.adresselinje2</nobr>       | Nei     | Adresselinje 2 for mottaker.                                                      | String                                         | Hentes fra Folkeregisteret  | Ikke støttet |
| <nobr>print.mottaker.adresselinje3</nobr>       | Nei     | Adresselinje 3 for mottaker.                                                      | String                                         | Hentes fra Folkeregisteret  | Ikke støttet |
| <nobr>print.mottaker.adresselinje4</nobr>       | Nei     | Adresselinje 4 for mottaker.                                                      | String                                         | Hentes fra Folkeregisteret  | Ikke støttet |
| <nobr>print.mottaker.postnummer</nobr>          | Nei     | Postnummer for mottaker.                                                          | String                                         | Hentes fra Folkeregisteret  | Ikke støttet |
| <nobr>print.mottaker.poststed</nobr>            | Nei     | Poststed for mottaker.                                                            | String                                         | Hentes fra Folkeregisteret  | Ikke støttet |
| <nobr>print.mottaker.land</nobr>                | Nei     | Land for mottaker.                                                                | String                                         | Hentes fra Folkeregisteret  | Ikke støttet |
 
## Et eller flere dokument

Hvilke typer dokument som støttes avhenger av mottakeren og er ikke kjent på forhånd. Dette medfører at forsøk på å
sende dokumenter som ikke støttes av mottakeren feiler først ved mottak.

Filformat som støttes er PDF. Nærmere beskrivelse finnes på:

- [Utskrifts- og forsendelsestjenesten](https://samarbeid.digdir.no/digital-postkasse/utskrifts-og-forsendelsestjenesten/644) (ekstern lenke)

## Beriking og transformasjon

Integrasjonspunktet transformerer og beriker meldinger som sendes med Digital Post til Innbyggere.

- [Transformasjon fra print til Digital Post til Innbyggere](../Transformasjoner/print_til_digital_post_til_innbyggere)

## Anbefalinger ved adressering

For å redusere risikoen for at brevpost ikke skal nå mottaker, har Posten kommet med gode anbefalinger på hvordan man skal adressere riktig, både til mottakere i Norge og i utlandet. Det anbefales at alle avsendervirksomheter følger disse. Les mer på [Posten adressering](https://www.posten.no/sende/adressering) (ekstern lenke)

## Neste steg

- [Dokumenttype `print` under Eksempel på vedtak til innbygger](../Eksempel/vedtak_til_innbygger#dersom-dokumenttype-print-st%C3%B8ttes)
