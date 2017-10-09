---
title: aaaSync gegevens (Preview) | Microsoft Docs
description: Dit overzicht introduceert Azure SQL-gegevenssynchronisatie (Preview).
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: douglasl
ms.openlocfilehash: d5b2bbd6a502ba94dba7fb309a6583d2d95cc1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sync-data-across-multiple-cloud-and-on-premises-databases-with-sql-data-sync"></a>Synchronisatie van gegevens over meerdere cloud en on-premises databases met SQL-gegevens synchroniseren

Synchroniseren van de SQL-gegevens is een service die is gebouwd op Azure SQL Database waarmee u synchroniseert Hallo gegevens die u twee richtingen op meerdere SQL-databases en exemplaren van SQL Server selecteren.

Synchroniseren van gegevens is gebaseerd op Hallo concept van een groep voor synchronisatie. Een groep voor synchronisatie is een groep met databases die u toosynchronize wilt.

Een groep voor synchronisatie heeft Hallo volgende eigenschappen:

-   Hallo **synchronisatieschema** wordt beschreven welke gegevens worden gesynchroniseerd.

-   Hallo **Sync richting** kan in twee richtingen of kan stromen slechts in één richting. Dat wil zeggen, Hallo Sync-richting *Hub tooMember* of *lid tooHub*, of beide.

-   Hallo **synchronisatie-Interval** hoe vaak synchronisatie plaatsvindt.

-   Hallo **Conflict resolutie beleid** is een niveau Groepsbeleid, wat kan *Hub wins* of *lid wins*.

Synchroniseren van gegevens gebruikt een hub en spoke-topologie toosynchronize-gegevens. U definieert een Hallo databases in de groep Hallo als Hallo Hub-Database. Hallo overige Hallo databases zijn lid databases. Synchronisatie doet zich alleen tussen Hallo Hub en de afzonderlijke leden.
-   Hallo **Hub Database** moet een Azure SQL Database.
-   Hallo **lid databases** SQL-Databases, de lokale SQL Server-databases of de SQL Server-exemplaren op virtuele machines in Azure.
-   Hallo **synchronisatiedatabase** bevat Hallo metagegevens en de logboekbestanden voor synchronisatie van gegevens. Hallo synchronisatiedatabase toobe een Azure SQL-Database zich in Hallo heeft dezelfde regio bevinden als Hallo Hub-Database. Hallo-synchronisatiedatabase is klant gemaakt en die eigendom zijn van de klant.

> [!NOTE]
> Als u een on-premises-database gebruikt, hebt u te[een lokale agent configureren.](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)

![Gegevens tussen databases synchroniseren](media/sql-database-sync-data/sync-data-overview.png)

## <a name="when-toouse-data-sync"></a>Wanneer toouse gegevens synchroniseren

Synchroniseren van gegevens is handig in gevallen waarin gegevens toobe toodate te houden in verschillende Azure SQL-Databases of SQL Server-databases moet. Hier volgen de belangrijkste gebruiksvoorbeelden Hallo voor synchroniseren van gegevens:

-   **Hybride gegevenssynchronisatie:** met het synchroniseren van gegevens, kun je gegevens worden gesynchroniseerd tussen uw on-premises-databases en de Azure SQL-Databases tooenable hybride toepassingen. Deze mogelijkheid kan beroep toocustomers die overweegt bewegende toohello cloud en wilt tooput enkele van de toepassing in Azure.

-   **Gedistribueerde toepassingen:** In veel gevallen is het nuttig tooseparate verschillende werkbelastingen voor andere databases. Als u een grote productiedatabase hebt, maar u ook een reporting toorun of analytics werkbelasting op deze gegevens moet, is het bijvoorbeeld handig toohave een tweede database voor deze extra belasting. Hierdoor minimaliseert Hallo invloed op de prestaties van de werkbelasting van uw productieomgeving. U kunt synchroniseren van gegevens tookeep deze twee databases gesynchroniseerd.

-   **Globaal gedistribueerde toepassingen:** veel bedrijven verschillende regio's en zelfs meerdere landen omvatten. toominimize netwerklatentie, het beste toohave uw gegevens in een regio te sluiten is tooyou. U kunt databases eenvoudig in regio's wereld Hallo gesynchroniseerd houden met het synchroniseren van gegevens.

Synchroniseren van gegevens wordt niet aanbevolen voor Hallo volgen scenario's:

-   Noodherstel

-   Lezen van schaal

-   ETL (OLTP tooOLAP)

-   Migratie van lokale SQL Server tooAzure SQL-Database

## <a name="how-does-data-sync-work"></a>Hoe werkt synchroniseren van gegevens? 

-   **Bijhouden van gegevenswijzigingen:** synchroniseren van gegevens houdt wijzigingen met behulp van invoegen, bijwerken en verwijderen van triggers. Hallo wijzigingen worden vastgelegd in een tabel aan clientzijde in Hallo-gebruikersdatabase.

-   **Synchroniseren van gegevens:** synchroniseren van gegevens in een Hub en Spoke-model is ontworpen. Hallo Hub wordt gesynchroniseerd met elk lid afzonderlijk. Wijzigingen van Hallo Hub zijn lid van de gedownloade toohello en vervolgens de wijzigingen van Hallo lid geüploade toohello Hub zijn.

-   **Het oplossen van conflicten:** synchroniseren van gegevens biedt twee opties voor conflictoplossing, *Hub wins* of *lid wins*.
    -   Als u selecteert *Hub wins*, Hallo wijzigingen in de hub Hallo altijd wijzigingen in Hallo lid overschreven.
    -   Als u selecteert *lid wins*, wijzigingen in Hallo lid overschrijven wijzigingen in de hub Hallo Hallo. Als er meer dan één lid, afhankelijk van de uiteindelijke waarde Hallo waarvoor de eerste wordt gesynchroniseerd.

## <a name="limitations-and-considerations"></a>Beperkingen en overwegingen

### <a name="performance-impact"></a>Prestatie-invloed
Gegevens synchroniseren gebruikt invoegen, bijwerken en verwijderen van triggers tootrack wijzigingen. Tabellen wordt gemaakt in de gebruikersdatabase Hallo voor het bijhouden. Deze wijziging bijhouden activiteiten heeft dit gevolgen voor de werkbelasting van uw database. De servicelaag beoordelen en indien nodig te upgraden.

### <a name="eventual-consistency"></a>Uiteindelijke consistentie
Omdat synchroniseren van gegevens op basis van een trigger, transactionele consistentie kan niet worden gegarandeerd. Microsoft zorgt ervoor dat alle uiteindelijk wijzigingen en synchroniseren van gegevens veroorzaakt geen gegevens verloren gaan.

### <a name="unsupported-data-types"></a>Niet-ondersteunde gegevenstypen

-   FileStream

-   SQL/CLR UDT

-   XMLSchemaCollection (XML wordt ondersteund)

-   Cursor, Timestamp, Hierarchyid

### <a name="requirements"></a>Vereisten

-   Elke tabel moet een primaire sleutel hebben.

-   Een tabel geen identiteitskolom die geen primaire sleutel Hallo.

-   Hallo-namen van objecten (databases, tabellen en kolommen) kunnen bevatten Hallo afdrukbare tekens punt (.), vierkante linkerhaak ([]), of rechts vierkante haak (]).

### <a name="limitations-on-service-and-database-dimensions"></a>Beperkingen met betrekking tot dimensies service en -database

|                                                                 |                        |                             |
|-----------------------------------------------------------------|------------------------|-----------------------------|
| **Dimensies**                                                      | **Limiet**              | **Tijdelijke oplossing**              |
| Maximum aantal synchronisatiegroepen die elke database kan deel uitmaken.       | 5                      |                             |
| Maximum aantal eindpunten in een enkel sync-groep              | 30                     | Meerdere synchronisatiegroepen maken |
| Maximum aantal lokale eindpunten in een enkel sync-groep. | 5                      | Meerdere synchronisatiegroepen maken |
| Database-, tabel-, schema-en kolomnamen                       | 50 tekens per naam |                             |
| Tabellen in een groep voor synchronisatie                                          | 500                    | Meerdere synchronisatiegroepen maken |
| Kolommen in een tabel in een groep voor synchronisatie                              | 1000                   |                             |
| Grootte van de rij gegevens in een tabel                                        | 24 mb                  |                             |
| Minimale synchronisatie-interval                                           | 5 minuten              |                             |

## <a name="common-questions"></a>Veelgestelde vragen

### <a name="how-frequently-can-data-sync-synchronize-my-data"></a>Hoe vaak kunt synchroniseren van gegevens mijn gegevens Synchroniseer? 
Hallo minimumfrequentie is om de vijf minuten.

### <a name="can-i-use-data-sync-toosync-between-sql-server-on-premises-databases-only"></a>Kan ik toosync synchroniseren van gegevens tussen alleen lokale-databases in SQL Server gebruiken? 
Niet rechtstreeks. U kunt synchroniseren tussen de SQL Server-databases voor lokale indirect echter door het maken van een Hub-database in Azure en vervolgens toe te voegen groep voor synchronisatie met Hallo lokale databases toohello.
   
### <a name="can-i-use-data-sync-tooseed-data-from-my-production-database-tooan-empty-database-and-then-keep-them-synchronized"></a>Kan ik gegevenssynchronisatie tooseed gegevens uit mijn productie database tooan lege database gebruiken, en vervolgens deze gesynchroniseerd houden? 
Ja. Hallo schema handmatig maken in de nieuwe database Hallo door het uitvoeren van scripts uit de oorspronkelijke Hallo. Nadat u Hallo schema maakt, Hallo tabellen tooa toocopy Hallo-gegevens synchroniseren groep toevoegen en het gesynchroniseerd houden.

### <a name="why-do-i-see-tables-that-i-did-not-create"></a>Waarom zie ik tabellen die ik niet hebt gemaakt?  
Synchroniseren van gegevens maakt aan tabellen in de database voor het bijhouden. Deze niet verwijderen of werkt niet meer synchroniseren van gegevens.
   
### <a name="i-got-an-error-message-that-said-cannot-insert-hello-value-null-into-hello-column-column-column-does-not-allow-nulls-what-does-this-mean-and-how-can-i-fix-hello-error"></a>Ik heb een foutbericht weergegeven dat gezegd ' hello waarde NULL kan niet invoegen in kolom Hallo \<kolom\>. Kolom mag geen null-waarden." Wat betekent dit en hoe kan ik Hallo fout oplossen? 
Dit foutbericht geeft aan Hallo van de twee volgende problemen:
1.  Mogelijk zijn er geen tabel zonder een primaire sleutel. een primaire sleutel tooall Hallo tabellen toofix dit probleem toevoegen bent worden gesynchroniseerd.
2.  Mogelijk zijn er een WHERE-component in de instructie CREATE INDEX. Deze voorwaarde verwerkt synchronisatie niet. toofix dit probleem Hallo WHERE-component verwijderen of handmatig aanbrengen Hallo tooall databases. 
 
### <a name="how-does-data-sync-handle-circular-references-that-is-when-hello-same-data-is-synced-in-multiple-sync-groups-and-keeps-changing-as-a-result"></a>Hoe wordt gegevenssynchronisatie kringverwijzingen verwerkt? Dat wil zeggen, wanneer hello dezelfde gegevens in meerdere synchronisatiegroepen is gesynchroniseerd en als gevolg hiervan blijft wijzigen?
Synchroniseren van gegevens kunnen kringverwijzingen niet worden verwerkt. Ervoor tooavoid worden ze. 

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over het synchroniseren van de SQL-gegevens:

-   [Aan de slag met het synchroniseren van de SQL-gegevens](sql-database-get-started-sql-data-sync.md)

-   Voltooien van de PowerShell-voorbeelden laten zien hoe tooconfigure SQL-gegevens synchroniseren:
    -   [Gebruik PowerShell toosync tussen meerdere Azure SQL-databases](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [Gebruik PowerShell toosync tussen een Azure SQL Database en een lokale SQL Server-database.](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [Hallo volledige gegevenssynchronisatie SQL technische documentatie downloaden](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)

-   [Hallo SQL gegevens synchroniseren REST-API-documentatie downloaden](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

Zie voor meer informatie over SQL-Database:

-   [Overzicht van de SQL-Database](sql-database-technical-overview.md)

-   [Database-levenscyclusbeheer](https://msdn.microsoft.com/library/jj907294.aspx)
