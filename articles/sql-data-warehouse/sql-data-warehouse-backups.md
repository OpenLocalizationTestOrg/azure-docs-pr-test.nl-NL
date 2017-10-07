---
title: back-ups SQL Data Warehouse aaaAzure - momentopnamen, geografisch redundante | Microsoft Docs
description: Meer informatie over SQL Data Warehouse ingebouwde databaseback-ups die u in staat toorestore stellen een herstelpunt voor Azure SQL Data Warehouse tooa of een andere geografische regio.
services: sql-data-warehouse
documentationcenter: 
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: b5aff094-05b2-4578-acf3-ec456656febd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 34659480485246f54a1490e185fc1b903fb2520d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-backups"></a>Back-ups van SQL Data Warehouse
SQL Data Warehouse biedt zowel lokale als geografische back-ups als onderdeel van de back-mogelijkheden van datawarehouse. Het gaat hierbij om Azure Storage-Blob momentopnamen en geografisch redundante opslag. Gebruik datawarehouse-back-ups toorestore uw datawarehouse tooa terugzetten punt in de primaire regio Hallo of verschillende geografische regio tooa herstellen. Dit artikel wordt uitgelegd Hallo details van back-ups in SQL Data Warehouse.

## <a name="what-is-a-data-warehouse-backup"></a>Wat is er een back-up van gegevens datawarehouse?
Een back-up van gegevens datawarehouse is Hallo gegevens waarmee u toorestore een datawarehouse tooa specifiek tijdstip kunt.  Omdat SQL Data Warehouse een gedistribueerd systeem is, wordt een back-up van gegevens datawarehouse bestaat uit veel bestanden die zijn opgeslagen in Azure blobs. 

Databaseback-ups zijn een essentieel onderdeel van een zakelijke continuïteit en noodherstel herstelstrategie omdat ze uw gegevens tegen per ongeluk beschadigd of verwijderd beschermen. Zie voor meer informatie [Business continuity overview](../sql-database/sql-database-business-continuity.md).

## <a name="data-redundancy"></a>Gegevensredundantie
SQL Data Warehouse beschermt u uw gegevens door het opslaan van gegevens in lokaal redundante (LRS) Azure Premium-opslag. Deze functie Azure Storage slaat meerdere synchrone kopieën van Hallo gegevens in Hallo lokale gegevens center tooguarantee transparante gegevensbeveiliging, als er gelokaliseerde fouten. Gegevensredundantie zorgt ervoor dat uw gegevens kunt blijven bewaard als infrastructuur problemen zoals schijffouten. Gegevensredundantie zorgt bedrijfscontinuïteit met een fouttolerant en infrastructuur maximaal beschikbaar.

meer informatie over toolearn:

* Azure Premium-opslag, Zie [inleiding tooAzure Premium-opslag](../storage/common/storage-premium-storage.md).
* Lokaal redundante opslag Zie [Azure Storage-replicatie](../storage/common/storage-redundancy.md#locally-redundant-storage).

## <a name="azure-storage-blob-snapshots"></a>Azure Blob-opslag-momentopnamen
Als een voordeel van het gebruik van Azure Premium-opslag SQL Data Warehouse maakt gebruik van Azure Storage-Blob momentopnamen toobackup Hallo-datawarehouse lokaal. U kunt een herstelpunt voor datawarehouse tooa momentopname terugzetten. Momentopnamen van een minimum van elke acht uur start en zijn beschikbaar voor de zeven dagen.  

meer informatie over toolearn:

* Azure blob-momentopnamen, Zie [momentopname maken van een blob](../storage/blobs/storage-blob-snapshots.md).

## <a name="geo-redundant-backups"></a>Geografisch redundante back-ups
Elke 24 uur slaat SQL Data Warehouse Hallo volledige datawarehouse in Standard-opslag. Hallo volledige datawarehouse wordt gemaakt toomatch tijd van laatste momentopname Hallo Hallo. Hallo standaardopslag hoort account van de tooa geografisch redundante opslag met leestoegang (RA-GRS). Hello Azure Storage RA-GRS functie repliceert Hallo back-upbestanden tooa [gekoppeld Datacenter](../best-practices-availability-paired-regions.md). Deze geo-replicatie, zorgt u ervoor dat kunt u datawarehouse herstellen als u geen toegang momentopnamen Hallo in uw primaire regio tot. 

Deze functie is standaard ingeschakeld. Als u niet wilt toouse geografisch redundante back-ups, u kunt [opt-out] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn). 

> [!NOTE]
> In Azure storage Hallo term *replicatie* toocopying bestanden vanaf één locatie tooanother verwijst. De SQL *databasereplicatie* tookeeping toomultiple secundaire databases gesynchroniseerd met een primaire database verwijst. 
> 
> 

> [!NOTE]
> U kunnen zich niet geografisch redundante back-ups met DWU 9000 en DWU 18000 afmelden. 
>
> 

meer informatie over toolearn:

* Geografisch redundante opslag Zie [Azure Storage-replicatie](../storage/common/storage-redundancy.md).
* RA-GRS-opslag, Zie [geografisch redundante opslag met leestoegang](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage).

## <a name="data-warehouse-backup-schedule-and-retention-period"></a>Back-upschema en de bewaarperiode van datawarehouse
SQL Data Warehouse maakt momentopnamen op uw online datawarehouses elke vier uur tooeight en houdt elke momentopname voor de zeven dagen. Afgelopen zeven dagen, kunt u uw tooone onlinedatabase Hallo herstelpunten in Hallo herstellen. 

toosee wanneer de laatste momentopname Hallo gestart, wordt deze query uitvoeren op uw online SQL Data Warehouse. 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

Als u een momentopname tooretain langer dan zeven dagen moet, kunt u een terugzetbewerking punt tooa nieuw datawarehouse herstellen. Na het Hallo terugzetten is voltooid, wordt in SQL Data Warehouse start maken van momentopnamen op Hallo nieuw datawarehouse. Als u geen wijzigingen toohello nieuw datawarehouse maakt, blijft leeg Hallo momentopnamen, en daarom Hallo momentopname kosten is minimaal. U kan Hallo database tookeep SQL Data Warehouse ook onderbreken van het maken van momentopnamen.

### <a name="what-happens-toomy-backup-retention-while-my-data-warehouse-is-paused"></a>Wat gebeurt er back-up bewaren toomy terwijl Mijn datawarehouse is onderbroken?
SQL Data Warehouse geen momentopnamen maken en momentopnamen niet verloopt terwijl een datawarehouse is onderbroken. Hallo momentopname leeftijd wordt niet gewijzigd tijdens het Hallo-datawarehouse is onderbroken. Momentopname bewaarperiode is gebaseerd op Hallo aantal dagen op Hallo-datawarehouse niet kalenderdagen online is.

Als een momentopname oktober 1 om 16: 00 gestart en Hallo-datawarehouse om 16: 00 oktober 3 is onderbroken, is de momentopname Hallo twee dagen oud. Wanneer het Hallo-datawarehouse server weer online is Hallo momentopname twee dagen oud. Hallo datawarehouse online wordt gezet oktober 5 om 16: 00, Hallo momentopname is twee dagen oud als blijft gedurende vijf dagen.

Hallo datawarehouse weer online wordt gezet, SQL Data Warehouse wordt hervat nieuwe momentopnamen die als momentopnamen verloopt wanneer ze meer dan zeven dagen aan gegevens hebben.

### <a name="how-long-is-hello-retention-period-for-a-dropped-data-warehouse"></a>Hoe lang is Hallo bewaarperiode voor een verwijderde datawarehouse?
Wanneer een datawarehouse is verwijderd, worden Hallo datawarehouse en Hallo momentopnamen voor zeven dagen opgeslagen en vervolgens wordt verwijderd. U kunt Hallo datawarehouse tooany Hallo opgeslagen herstelpunten herstellen.

> [!IMPORTANT]
> Als u een logische SQL server-exemplaar verwijdert, worden alle databases die deel uitmaken van toohello exemplaar worden ook verwijderd en kunnen niet worden hersteld. U kunt een verwijderde server niet herstellen.
> 
> 

## <a name="data-warehouse-backup-costs"></a>Datawarehouse-back-kosten
totale kosten voor de primaire datawarehouse en de zeven dagen van Azure Blob-momentopnamen Hallo is afgerond toohello dichtstbijzijnde TB. Als uw datawarehouse 1,5 TB is en Hallo momentopnamen 100 GB gebruiken, kunt u wordt bijvoorbeeld voor gefactureerd voor 2 TB aan gegevens volgens de tarieven voor Azure Premium-opslag. 

> [!NOTE]
> Elke momentopname in eerste instantie leeg is en neemt toe naarmate het aanbrengen van wijzigingen toohello primaire datawarehouse. Alle momentopnamen toeneemt in omvang als Hallo gegevens datawarehouse worden gewijzigd. Hallo-kosten voor opslag voor momentopnamen groeien daarom volgens toohello wijzigingsratio.
> 
> 

Als u geografisch redundante opslag gebruikt, ontvangt u een afzonderlijke opslag kosten. Hallo geografisch redundante opslag wordt gefactureerd snelheid Hallo standard-geografisch redundante opslag met leestoegang (RA-GRS).

Zie voor meer informatie over prijzen van SQL Data Warehouse [prijzen van SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="using-database-backups"></a>Met behulp van de databaseback-ups
Hallo primair gebruik van SQL datawarehouse-back-ups is toorestore Hallo datawarehouse tooone Hallo herstelpunten binnen de bewaarperiode Hallo.  

* Zie voor een SQL datawarehouse toorestore [herstellen van een SQL datawarehouse](sql-data-warehouse-restore-database-overview.md).

## <a name="related-topics"></a>Verwante onderwerpen
### <a name="scenarios"></a>Scenario's
* Zie voor een overzicht zakelijke continuïteit [Business continuity-overzicht](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

* een datawarehouse toorestore Zie [herstellen van een SQL datawarehouse](sql-data-warehouse-restore-database-overview.md)

<!-- ### Tutorials -->

