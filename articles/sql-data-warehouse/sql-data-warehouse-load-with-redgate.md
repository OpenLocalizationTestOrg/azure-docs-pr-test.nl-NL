---
title: aaaUse Redgate tooload gegevens tooyour Azure datawarehouse | Microsoft Docs
description: Meer informatie over hoe de toouse Redgate gegevens Platform Studio voor datawarehousescenario's.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a>Gegevens laden met behulp van Data Platform Studio van Redgate
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

Deze zelfstudie leert u hoe toouse [Redgate van gegevens Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DP's) toomove gegevens uit een lokale SQL Server tooAzure SQL Data Warehouse. Gegevens Platform Studio past u het meest geschikte compatibiliteit oplossingen Hallo en optimalisatie, dus het snelst Hallo manier tooget gestart met SQL Data Warehouse.

> [!NOTE]
> [Redgate](http://www.red-gate.com) is al lange tijd een Microsoft-partner en levert verschillende SQL Server-hulpprogramma's. Deze functie in DPS is gratis beschikbaar voor commercieel en niet-commercieel gebruik.
> 
> 

## <a name="before-you-begin"></a>Voordat u begint
### <a name="create-or-identify-resources"></a>Resources maken of identificeren
Voordat u deze zelfstudie begint, moet u toohave:

* **lokale SQL Server-Database**: gegevens die u wilt tooimport tooSQL Data Warehouse toocome van een lokale SQL Server moet Hallo (versie 2008 R2 of hoger). Met DPS kunnen gegevens niet rechtstreeks worden geïmporteerd uit een Azure SQL-database of uit tekstbestanden.
* **Azure Storage-Account**: Data Platform Studio bereidt Hallo-gegevens in Azure Blob Storage voordat deze worden geladen in SQL Data Warehouse. Hallo storage-account moet gebruikmaken van Hallo ' Resource Manager '-implementatiemodel (standaard Hallo) in plaats van 'Klassiek' Hallo-implementatiemodel. Als u geen storage-account hebt, Ontdek hoe tooCreate een opslagaccount. 
* **SQL Data Warehouse**: in deze zelfstudie Hallo gegevens verplaatst van de lokale SQL Server tooSQL datawarehouse, zodat u toohave moet een datawarehouse online. Als u nog geen datawarehouse, Ontdek hoe tooCreate een Azure SQL Data Warehouse.

> [!NOTE]
> De prestaties worden verbeterd als Hallo storage-account en Hallo datawarehouse worden gemaakt in Hallo dezelfde regio.
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a>Stap 1: Registreren in tooData Platform Studio met uw Azure-account
Open uw webbrowser en navigeer toohello [gegevens Platform Studio](https://www.dataplatformstudio.com/) website. Aanmelden met Hallo dezelfde Azure-account die u gebruikte toocreate Hallo storage-account en het datawarehouse. Als uw e-mailadres gekoppeld aan een werk of schoolaccount en een Microsoft-account worden ervoor toochoose Hallo-account dat toegang tooyour bronnen heeft is.

> [!NOTE]
> Als dit de eerste keer met gegevens Platform Studio, wordt u gevraagd toogrant Hallo toepassing machtiging toomanage uw Azure-resources.
> 
> 

## <a name="step-2-start-hello-import-wizard"></a>Stap 2: Start Hallo Wizard importeren
Selecteer in de Hallo DP's hoofdvenster Hallo tooAzure SQL Data Warehouse koppeling toostart Hallo importeren wizard importeren.

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a>Stap 3: Hallo gegevensgateway Platform Studio installeren
tooconnect tooyour lokale SQL Server-database, moet u tooinstall Hallo DP's Gateway. Hallo-gateway is een clientagent waarmee toegang tooyour lokale omgeving haalt gegevens op Hallo en geüpload tooyour storage-account. De gegevens worden niet verwerkt op de servers van Redgate. tooinstall hello Gateway:

1. Klik op Hallo **Gateway maken** koppeling
2. Downloaden en installeren Hallo Gateway met Hallo opgegeven installatieprogramma

![][2]

> [!NOTE]
> Hallo Gateway kan worden geïnstalleerd op een machine met het netwerk toegang toohello bron SQL Server-database. Deze toegang heeft tot Hallo SQL Server-database met behulp van Windows-verificatie met referenties van de huidige gebruiker Hallo Hallo.
> 
> 

Na de installatie configureert Hallo Gateway status wijzigingen tooConnected en kunt u de volgende selecteren.

## <a name="step-4-identify-hello-source-database"></a>Stap 4: De brondatabase Hallo identificeren
In Hallo *servernaam Voer* textbox, voer de naam Hallo van Hallo-server die als host fungeert voor uw database en selecteer **volgende**. Selecteer vervolgens uit de vervolgkeuzelijst hello, tooimport gegevens van gewenste Hallo-database.

![][3]

DP's inspecteert de geselecteerde database Hallo voor tabellen tooimport. Standaard wordt DP's alle Hallo tabellen in Hallo database geïmporteerd. U kunt selecteren of selectie opheffen tabellen door het uitbreiden van alle tabellen koppelen Hallo. Selecteer Hallo volgende knop toomove doorsturen.

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a>Stap 5: Kies een storage account toostage Hallo-gegevens
DP's wordt u gevraagd een locatie toostage Hallo-gegevens. Kies een bestaand opslagaccount in uw abonnement en selecteer **Volgende**.

> [!NOTE]
> DP's maakt een nieuwe blob-container in Hallo gekozen storage-account en een unieke map gebruiken voor elke importeren.
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a>Stap 6: Een datawarehouse selecteren
Vervolgens selecteert u een online [Azure SQL Data Warehouse](http://aka.ms/sqldw) tooimport Hallo gegevens in de database. Wanneer u de database hebt geselecteerd, moet u tooenter Hallo referenties tooconnect toohello database en selecteer **volgende**.

![][5]

> [!NOTE]
> DP's samengevoegd Hallo bron gegevenstabellen met Hallo-datawarehouse. DP's waarschuwt u als Hallo tabelnaam dit vereist is voor de bestaande tabellen toooverwrite in Hallo datawarehouse. U kunt desgewenst verwijderen eventuele bestaande objecten in Hallo datawarehouse door te tikken verwijderen alle bestaande objecten voor de import.
> 
> 

## <a name="step-7-import-hello-data"></a>Stap 7: Hallo gegevens importeren
DP's wordt bevestigd dat u tooimport Hallo gegevens wilt. Klik op Hallo Start knop toobegin Hallo gegevens importeren.

![][6]

DP's wordt weergegeven een visualisatie die Hallo voortgang geeft van het uitpakken en het uploaden van gegevens van Hallo van Hallo lokale SQL Server en Hallo voortgang van Hallo importeren in SQL Data Warehouse.

![][7]

Zodra de Hallo importeren is voltooid, geeft een samenvatting van Hallo gegevens importeren en een rapport wijzigen van Hallo compatibiliteit met oplossingen die zijn uitgevoerd DP's weer.

![][8]

## <a name="next-steps"></a>Volgende stappen
tooexplore uw gegevens in SQL Data Warehouse opstarten weer te geven:

* [Query’s uitvoeren bij Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]
* [Gegevens visualiseren met Power BI][Visualize data with Power BI]

meer informatie over de Redgate gegevens Platform Studio toolearn:

* [Ga naar de startpagina van Hallo DP 's](http://www.dataplatformstudio.com/)
* [Bekijk een demonstratie van DPS op Channel 9](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

Zie voor een overzicht van andere manieren toomigrate en load uw gegevens in SQL Data Warehouse:

* [Uw oplossing tooSQL Data Warehouse migreren][Migrate your solution tooSQL Data Warehouse]
* [Load data into Azure SQL Data Warehouse](sql-data-warehouse-overview-load.md) (Gegevens laden in Azure SQL Data Warehouse)

Zie voor meer tips voor het ontwikkeling Hallo [overzicht van SQL Data Warehouse voor ontwikkelaars](sql-data-warehouse-overview-develop.md).

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
