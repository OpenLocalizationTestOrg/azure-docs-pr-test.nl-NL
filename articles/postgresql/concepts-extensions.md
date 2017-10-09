---
title: aaaUsing PostgreSQL uitbreidingen in een Azure-Database voor PostgreSQL | Microsoft Docs
description: Hierin wordt beschreven Hallo mogelijkheid tooextend Hallo functionaliteit van de extensies in de Azure-Database gebruiken voor PostgreSQL-database.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/29/2017
ms.openlocfilehash: af2462d7a923b934bc0329153be7079ba86e8856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a>PostgreSQL-uitbreidingen in Azure PostgreSQL-Database
PostgreSQL biedt Hallo mogelijkheid tooextend Hallo functionaliteit van de database met de extensies. Uitbreidingen kunnen voor meerdere verwante SQL objecten toobe samen gebundeld in één pakket toestaan en worden geladen of verwijderd uit de database met één opdracht. Extensies na het laden in hello database kunnen werken net als functies die zijn ingebouwd in. Zie voor meer informatie over PostgreSQL extensies [verpakking verwante objecten in een uitbreiding](https://www.postgresql.org/docs/9.6/static/extend-extensions.html).

## <a name="how-toouse-postgresql-extensions"></a>Hoe toouse PostgreSQL extensies?
PostgreSQL-uitbreidingen moeten toobe geïnstalleerd voor uw database voordat u ze kunt gebruiken. tooinstall een bepaalde extensie, voer de [EXTENSIE maken](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) opdracht van psql hulpprogramma tooload Hallo verpakte objecten in uw database.

Azure PostgreSQL-Database ondersteunt een subset van de belangrijkste uitbreidingen, zoals hier vermeld. Afgezien van Hallo die zijn vermeld, worden andere extensies niet ondersteund. U kunt uw eigen uitbreiding met Azure-Database maken voor PostgreSQL-service.

## <a name="extensions-supported-by-azure-database-for-postgresql"></a>Uitbreidingen voor PostgreSQL wordt ondersteund door Azure Database
Hallo volgende tabellen lijst Hallo standaard PostgreSQL-uitbreidingen die momenteel worden ondersteund door Azure-Database voor PostgreSQL. U kunt deze informatie ook ophalen door het uitvoeren van query's pg\_beschikbare\_extensies. 

### <a name="data-types-extensions"></a>Gegevens typen uitbreidingen

> [!div class="mx-tableFixed"]
| **De extensie** | **Beschrijving** |
|---|---|
| [citext](https://www.postgresql.org/docs/9.6/static/citext.html) | Bevat een niet-hoofdlettergevoelige tekentype tekenreeks |
| [hstore](https://www.postgresql.org/docs/9.6/static/hstore.html) | Gegevenstype biedt voor het opslaan van sets van sleutel-waardeparen |

### <a name="functions-extensions"></a>Uitbreidingen van functies

> [!div class="mx-tableFixed"]
| **De extensie** | **Beschrijving** |
|---|---|
| [fuzzystrmatch](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | Biedt verschillende functies toodetermine overeenkomsten en de afstand tussen tekenreeksen. |
| [intarray](https://www.postgresql.org/docs/9.6/static/intarray.html) | Biedt de functies en operators voor het manipuleren van null gratis matrices van gehele getallen. |
| [pgcrypto](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | Voorziet in cryptografische functies |
| [PG\_partman](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | Gepartitioneerde tabellen wordt beheerd door de time- of -ID |
| [PG\_trgm](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | Functies en operatoren biedt voor het bepalen van Hallo overeenkomsten van alfanumerieke tekst op basis van overeenkomst trigram |
| [UUID ossp](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | Universeel unieke id's (UUID's) genereren |

### <a name="full-text-search-extensions"></a>Uitbreidingen voor volledige tekst zoeken

> [!div class="mx-tableFixed"]
| **De extensie** | **Beschrijving** |
|---|---|
| [unaccent](https://www.postgresql.org/docs/9.6/static/unaccent.html) | Een woordenlijst van de tekst zoeken waarmee accenten (diakritische tekens) uit lexemes worden verwijderd. |

### <a name="index-types-extensions"></a>Index typen uitbreidingen

> [!div class="mx-tableFixed"]
| **De extensie** | **Beschrijving** |
|---|---|
| [bTree\_gin](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | Voorbeeld GIN operator klassen die B-tree zoals gedrag voor bepaalde gegevenstypen implementeren biedt. |
| [bTree\_basisvertalingen](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | Biedt basisvertalingen index operator klassen die B-tree implementeren. |

### <a name="language-extensions"></a>Taal-extensies

> [!div class="mx-tableFixed"]
| **De extensie** | **Beschrijving** |
|---|---|
| [plpgsql](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | PL/pgSQL geladen procedurele taal |

### <a name="miscellaneous-extensions"></a>Diverse uitbreidingen

> [!div class="mx-tableFixed"]
| **De extensie** | **Beschrijving** |
|---|---|
| [PG\_buffercache](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | Biedt een manier voor het onderzoeken van wat er gebeurt in Hallo gedeelde buffercache in realtime. |
| [PG\_prewarm](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | Biedt een manier tooload relatie gegevens in cache van Hallo buffer. |
| [PG\_stat\_instructies](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | Biedt een manier voor het bijhouden van Uitvoeringsstatistieken van alle SQL-instructies uitgevoerd door een server. |
| [postgres\_fdw](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | Afwijkend gegevens wrapper gebruikt tooaccess opgeslagen gegevens in externe PostgreSQL-servers |

### <a name="postgis"></a>PostGIS

> [!div class="mx-tableFixed"]
| **De extensie** | **Beschrijving** |
|---|---|
| [PostGIS](http://www.postgis.net/), postgis\_topologie, postgis\_tiger\_geocoder, postgis\_sfcgal | Ruimtelijke en geografische objecten voor PostgreSQL. |
| adres\_standardizer, adres\_standardizer\_gegevens\_ons | Gebruikte tooparse een adres in de elementen. Toosupport geocodering adres normalisatie stap gebruikt. |
| [pgrouting](http://pgrouting.org/) | Hallo PostGIS breidt / PostgreSQL georuimtelijke tooprovide georuimtelijke routeringsfunctionaliteit database. |

## <a name="next-steps"></a>Volgende stappen
Zie een uitbreiding die u wilt dat toouse niet? Laat ons weten. Stemmen voor bestaande aanvragen of maak nieuwe feedback en wensen in onze [forum met feedback van klanten](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).
