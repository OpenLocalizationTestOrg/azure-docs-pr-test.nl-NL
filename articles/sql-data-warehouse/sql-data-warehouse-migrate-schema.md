---
title: aaaMigrate uw schema tooSQL Data Warehouse | Microsoft Docs
description: Tips voor het migreren van uw schema tooAzure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a>Uw schema's tooSQL Data Warehouse migreren
Richtlijnen voor het migreren van uw SQL-schema's tooSQL Data Warehouse. 

## <a name="plan-your-schema-migration"></a>De schema-migratie plannen

Als u van plan een migratie bent, Zie Hallo [tabel overzicht] [ table overview] toobecome bekend zijn met overwegingen bij het ontwerpen van tabel zoals statistieken, distributie, partitioneren en indexeren.  Ook worden enkele [niet-ondersteunde tabelfuncties] [ unsupported table features] en de tijdelijke oplossingen.

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a>Databases van de gebruiker gedefinieerde schema's tooconsolidate gebruiken

De werkbelasting van uw bestaande heeft waarschijnlijk meer dan één database. Een datawarehouse van SQL Server kan bijvoorbeeld een faseringsdatabase, een datawarehouse-database en sommige gegevens datamart-databases. In deze topologie wordt elke database uitgevoerd als een afzonderlijke werkbelasting met afzonderlijke beveiligingsbeleid.

Daarentegen, voert SQL Data Warehouse Hallo gehele datawarehouse-workload binnen één database. Joins zijn niet toegestaan cross-database. SQL Data Warehouse verwacht daarom alle tabellen die worden gebruikt door Hallo datawarehouse toobe opgeslagen in één Hallo-database.

Wordt u aangeraden tooconsolidate van de gebruiker gedefinieerde schema's de werkbelasting van uw bestaande in een database. Zie voor voorbeelden [gebruiker gedefinieerde schema's](sql-data-warehouse-develop-user-defined-schemas.md)

## <a name="use-compatible-data-types"></a>Compatibele gegevenstypen gebruiken
Wijzigen van uw gegevens typen toobe die compatibel is met SQL Data Warehouse. Zie voor een lijst van ondersteunde en niet-ondersteunde gegevenstypen [gegevenstypen][data types]. Dat onderwerp biedt tijdelijke oplossingen voor Hallo niet-ondersteunde typen. Het bevat ook een query tooidentify bestaande typen die niet worden ondersteund in SQL Data Warehouse.

## <a name="minimize-row-size"></a>Rijgrootte minimaliseren
Minimaliseer Hallo rijlengte van de tabellen voor de beste prestaties. Aangezien korter rij lengten toobetter prestaties leiden, Hallo kleinste gegevenstypen gebruiken die werken voor uw gegevens. 

PolyBase heeft voor de breedte van de rij tabel, een limiet van 1 MB.  Als u van plan tooload gegevens in SQL Data Warehouse met PolyBase bent, werk de tabellen toohave maximale rij breedten van minder dan 1 MB. 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a>Hallo distributie optie opgeven
SQL Data Warehouse is een gedistribueerde database-systeem. Elke tabel is gedistribueerd of gerepliceerd via Hallo rekenknooppunten. Er is een tabeloptie waarmee u kunt opgeven hoe toodistribute Hallo gegevens. Hallo zijn opties round-robin wordt gerepliceerd, of hash gedistribueerd. Elk heeft voor- en nadelen. Als u geen optie voor distributie Hallo opgeeft, SQL Data Warehouse round robin Hallo standaard gebruikt.

- Round robin is Hallo standaardwaarde. Dit is de eenvoudigste toouse hello en Hallo gegevens zo snel mogelijk worden geladen, maar joins gegevensverplaatsing waardoor wordt vertraagd queryprestaties is vereist.
- Gerepliceerde winkels een kopie van de tabel Hallo op elk rekenknooppunt. Gerepliceerde tabellen zijn zodat omdat ze geen verplaatsing van gegevens voor samenvoegingen en aggregaties behoeven. Extra opslag vereist, hetgeen daarom het meest geschikt voor kleinere tabellen.
- Hallo rijen verdeelt hash gedistribueerd over alle knooppunten van Hallo via een hash-functie. Gedistribueerd hash-tabellen zijn Hallo hart van SQL Data Warehouse omdat ze ontworpen tooprovide hoge queryprestaties op grote tabellen zijn. Deze optie vereist een planning tooselect Hallo best van de kolommen op welke toodistribute Hallo-gegevens. Echter, als u niet het aanbevolen kolom Hallo Hallo eerst kiest, kunt u eenvoudig opnieuw distribueren Hallo gegevens op een andere kolom. 

Zie toochoose Hallo aanbevolen optie voor distributie voor elke tabel [tabellen gedistribueerd](sql-data-warehouse-tables-distribute.md).


## <a name="next-steps"></a>Volgende stappen
Nadat u uw database schema tooSQL Data Warehouse hebt gemigreerd, gaat u verder tooone Hallo artikelen te volgen:

* [Uw gegevens migreren][Migrate your data]
* [Uw code migreren][Migrate your code]

Zie voor meer informatie over best practices voor SQL Data Warehouse Hallo [aanbevolen procedures] [ best practices] artikel.

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
