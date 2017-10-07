---
title: een Azure datawarehouse - lokale en geografisch redundante aaaRestore | Microsoft Docs
description: Overzicht van opties voor Hallo database terugzetten voor het herstellen van een database in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a>SQL Data Warehouse terugzetten
> [!div class="op_single_selector"]
> * [Overzicht][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

SQL Data Warehouse biedt zowel lokale als geografische herstelacties als onderdeel van de datawarehouse disaster recovery. Gebruik datawarehouse-back-ups toorestore uw datawarehouse tooa terugzetten punt in de primaire regio Hallo of gebruik van geografisch redundante back-ups toorestore tooa verschillende geografische regio. Dit artikel wordt uitgelegd Hallo details van het herstellen van een datawarehouse.

## <a name="what-is-a-data-warehouse-restore"></a>Wat is er een datawarehouse te herstellen?
Een datawarehouse-herstellen van gegevens is een nieuw datawarehouse is gemaakt van een back-up van een bestaande of verwijderde datawarehouse. Hallo back-up datawarehouse Hallo herstelde datawarehouse opnieuw gemaakt op een bepaald tijdstip. Omdat SQL Data Warehouse een gedistribueerd systeem is, wordt een datawarehouse gegevens terugzetten vanuit veel back-upbestanden die zijn opgeslagen in Azure BLOB's gemaakt. 

Database terugzetten is een essentieel onderdeel van een zakelijke continuïteit en noodherstel herstelstrategie omdat uw gegevens opnieuw worden gemaakt na het per ongeluk beschadigd of verwijderd.

Zie voor meer informatie:

* [Back-ups van SQL Data Warehouse](sql-data-warehouse-backups.md)
* [Overzicht van zakelijke continuïteit](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a>Datawarehouse-herstelpunten
Als een voordeel van het gebruik van Azure Premium-opslag maakt gebruik van SQL Data Warehouse Azure Storage-Blob momentopnamen toobackup Hallo primaire datawarehouse. Elke momentopname is een herstelpunt dat Hallo tijd vertegenwoordigt Hallo momentopname gestart. toorestore een datawarehouse, kies een herstelpunt en voert u een restore-opdracht.  

SQL Data Warehouse herstelt altijd Hallo back-tooa nieuw datawarehouse. U kunt Hallo herstelde gegevensmagazijn behouden en huidige hello of een van deze verwijderen. Als u wilt dat tooreplace Hallo huidige datawarehouse met Hallo hersteld datawarehouse, u deze kunt wijzigen.

Als u een verwijderde of onderbroken datawarehouse toorestore nodig hebt, kunt u [Maak een ondersteuningsticket](sql-data-warehouse-get-started-create-support-ticket.md). 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a>Geografisch redundante terugzetten
U kunt uw datawarehouse tooany gegevensgebied Azure SQL Data Warehouse op het niveau van uw gekozen prestatie ondersteunende herstellen. Houd er rekening mee dat 9000 en 18000 DWU worden niet ondersteund in alle regio's tijdens het Hallo-preview.

> [!NOTE]
> een geografisch redundante tooperform terugzetten die u moet niet buiten deze functie hebt gekozen.
> 
> 

## <a name="restore-timeline"></a>Tijdlijn herstellen
Afgelopen zeven dagen, kunt u een database tooany beschikbaar herstelpunt binnen Hallo herstellen. Momentopnamen elke vier uur voor tooeight start en zijn beschikbaar voor de zeven dagen. Wanneer een momentopname ouder dan zeven dagen is, het verloopt en het herstelpunt is niet meer beschikbaar.

## <a name="restore-costs"></a>Kosten herstellen
Hallo opslag kosten voor Hallo herstelde datawarehouse wordt gefactureerd snelheid hello Azure Premium-opslag. 

Als u een herstelde datawarehouse onderbreekt, wordt u in rekening gebracht voor opslag snelheid hello Azure Premium-opslag. Hallo-voordeel van het onderbreken is dat u niet worden in rekening gebracht voor Hallo DWU computerbronnen.

Zie voor meer informatie over prijzen van SQL Data Warehouse [prijzen van SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="uses-for-restore"></a>Gebruikt voor herstel
Hallo primair gebruik van datawarehouse terugzetten is toorecover gegevens na onbedoeld gegevensverlies of beschadiging.

U kunt ook gegevens datawarehouse terugzetten tooretain een back-up langer dan zeven dagen. Zodra de back-up Hallo is hersteld, moet u Hallo datawarehouse online zijn en kunt onderbreken voor onbepaalde tijd toosave compute-kosten. Hallo onderbroken database leidt ertoe dat de opslagkosten snelheid hello Azure Premium-opslag. 

## <a name="related-topics"></a>Verwante onderwerpen
### <a name="scenarios"></a>Scenario's
* Zie voor een overzicht zakelijke continuïteit [Business continuity-overzicht](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

een datawarehouse tooperform herstellen, herstelt u met behulp van:

* Azure portal, Zie [herstellen van een datawarehouse met behulp van hello Azure-portal](sql-data-warehouse-restore-database-portal.md)
* PowerShell-cmdlets raadpleegt [herstellen van een datawarehouse met behulp van PowerShell-cmdlets](sql-data-warehouse-restore-database-powershell.md)
* REST-API's, Zie [herstellen van een datawarehouse Hallo REST-API's gebruiken](sql-data-warehouse-restore-database-rest-api.md)

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
