---
title: aaaLoad gegevens in Azure SQL Data Warehouse | Microsoft Docs
description: Meer informatie over Hallo algemene scenario's om gegevens te laden in SQL Data Warehouse. Deze omvatten het gebruik van PolyBase, Azure blob-opslag, platte bestanden en back-ups van schijf. U kunt ook hulpprogramma's van derden gebruiken.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a>Gegevens laden in Azure SQL Data Warehouse
Een samenvatting van Hallo scenario opties en aanbevelingen voor het laden van gegevens in SQL Data Warehouse.

Hallo lastigste onderdeel van het laden van gegevens is meestal Hallo gegevens voorbereiden voor Hallo laden. Azure vereenvoudigt laden met behulp van Azure blob-opslag als algemene gegevensopslag voor een groot aantal Hallo services en met behulp van Azure Data Factory Hallo tooorchestrate communicatie en gegevens die verkeer tussen Azure-services. Deze processen worden geïntegreerd met PolyBase-technologie die gebruikmaakt van massively parallel verwerken (MPP) tooload gegevens parallel uit Azure blob storage in SQL Data Warehouse. 

Zie voor zelfstudies die voorbeelddatabases worden geladen, [laden voorbeelddatabases][Load sample databases].

## <a name="load-from-azure-blob-storage"></a>Laden van Azure blob-opslag
Hallo snelste manier tooimport gegevens in SQL Data Warehouse zijn toouse PolyBase tooload gegevens uit Azure blob storage. PolyBase gebruikt SQL Data Warehouse van verwerking massively parallel (MPP) ontwerp tooload gegevens parallel uit Azure blob-opslag. toouse PolyBase, kunt u T-SQL-opdrachten of een Azure Data Factory-pijplijn.

### <a name="1-use-polybase-and-t-sql"></a>1. Gebruik PolyBase en T-SQL
Overzicht van het laadproces:

1. Uw gegevens tooAzure blob-opslag- of Azure Data Lake Store verplaatsen en sla het in tekstbestanden.
2. Externe objecten in SQL Data Warehouse toodefine Hallo locatie en indeling van Hallo gegevens configureren
3. Een T-SQL-opdracht tooload Hallo gegevens parallel worden uitgevoerd in een nieuwe databasetabel.

<!-- 5. Schedule and run a loading job. --> 

Zie voor een zelfstudie [laden van gegevens uit Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="2-use-azure-data-factory"></a>2. Azure Data Factory gebruiken
U kunt een Azure Data Factory-pijplijn die gebruikmaakt van PolyBase tooload gegevens uit Azure blob storage in SQL Data Warehouse maken voor een eenvoudigere manier toouse PolyBase. Dit is snel tooconfigure omdat u niet toodefine Hallo T-SQL-objecten hoeft. Als u tooquery Hallo externe gegevens zonder dat u deze importeert, gebruikt u de T-SQL. 

Overzicht van het laadproces:

1. De gegevens tooAzure blob-opslag verplaatsen en sla het in tekstbestanden. Azure Data Factory ondersteunt momenteel geen ADLS-connectiviteit met PolyBase).
2. Een Azure Data Factory pijplijn tooingest Hallo gegevens maken. Hallo PolyBase-optie gebruiken.
4. Plannen en uitvoeren van Hallo pijplijn.

Zie voor een zelfstudie [laden van gegevens uit Azure blob storage tooSQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].

## <a name="load-from-sql-server"></a>Laden van SQL Server
tooload gegevens uit SQL Server-tooSQL Data Warehouse Integration Services (SSIS), kunt u zet platte bestanden of schijven tooMicrosoft worden geleverd. Lees verder toosee een samenvatting van Hallo verschillende processen en koppelingen tootutorials laden.

tooplan volledige gegevens migreren van SQL Server-tooSQL Data Warehouse, Zie Hallo [Migratieoverzicht][Migration overview]. 

### <a name="use-integration-services-ssis"></a>Integratieservices (SSIS) gebruiken
Als u al Integration Services (SSIS) pakketten tooload in SQL Server gebruikt, kunt u uw pakketten toouse SQL Server Hallo bron-en SQL Data Warehouse als bestemming Hallo bijwerken. Dit is snel en eenvoudig toodo en is een goede keuze als u niet toomigrate uw laden probeert toouse gegevens die al in de cloud Hallo verwerken. Hallo afweging is Hallo load zijn lager dan het gebruik van PolyBase omdat deze SSIS geen Hallo load parallel voert.

Overzicht van het laadproces:

1. De Integration Services pakket toopoint toohello SQL Server-exemplaar voor Hallo bron en Hallo SQL Data Warehouse-database voor de bestemming Hallo herzien.
2. Migreer uw schema tooSQL datawarehouse, indien deze nog niet er is.
3. Hallo-toewijzing wijzigen in uw pakketten gebruiken alleen Hallo gegevenstypen die worden ondersteund door SQL Data Warehouse.
4. Plannen en uitvoeren van Hallo-pakket.

Zie voor een zelfstudie [laden van gegevens uit SQL Server-tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].

### <a name="use-azcopy-recommended-for--10-tb-data"></a>AZCopy (aanbevolen voor < 10 TB gegevens) gebruiken
Als de gegevensgrootte van uw < 10 TB is, kunt u Hallo gegevens exporteren uit SQL Server tooflat bestanden kopiëren Hallo bestanden tooAzure blob-opslag en gebruik vervolgens PolyBase tooload Hallo gegevens in SQL Data Warehouse

Overzicht van het laadproces:

1. Hallo bcp opdrachtregelprogramma tooexport gegevens uit SQL Server tooflat-bestanden gebruiken.
2. Hallo AZCopy-opdrachtregelprogramma toocopy gegevens uit platte bestanden tooAzure blob storage gebruiken.
3. Gebruik tooload PolyBase in SQL Data Warehouse.

Zie voor een zelfstudie [laden van gegevens uit Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="use-bcp"></a>Gebruikt bcp
Als u een kleine hoeveelheid gegevens hebt kunt u bcp tooload rechtstreeks in Azure SQL Data Warehouse.

Overzicht van het laadproces:

1. Hallo bcp opdrachtregelprogramma tooexport gegevens uit SQL Server tooflat-bestanden gebruiken.
2. Gebruikt bcp tooload gegevens uit platte bestanden rechtstreeks tooSQL Data Warehouse.

Zie voor een zelfstudie [laden van gegevens uit SQL Server-tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].

### <a name="use-importexport-recommended-for--10-tb-data"></a>Gebruik voor importeren/exporteren (aanbevolen voor > 10 TB gegevens)
Als de gegevensomvang van uw > 10 TB is en u toomove wilt het tooAzure, het is raadzaam dat u ons schijf verzend- [voor importeren/exporteren][Import/Export]. 

Samenvatting van het laadproces

1. Hallo bcp opdrachtregelprogramma tooexport gegevens uit SQL Server tooflat bestanden op naar schijven gebruiken.
2. Hallo schijven tooMicrosoft verzenden.
3. Microsoft laadt hello gegevens in SQL Data Warehouse

## <a name="load-from-hdinsight"></a>Laden van HDInsight
Laden van gegevens uit HDInsight met PolyBase biedt ondersteuning voor SQL Data Warehouse. Hallo-proces is hetzelfde als het laden van gegevens uit Azure Blob Storage - met PolyBase tooconnect tooHDInsight tooload gegevens Hallo. 

### <a name="1-use-polybase-and-t-sql"></a>1. Gebruik PolyBase en T-SQL
Overzicht van het laadproces:

1. Uw tooHDInsight gegevens verplaatsen en op te slaan in tekstbestanden, ORC of parketvloeren-indeling.
2. Externe objecten in SQL Data Warehouse toodefine Hallo locatie en indeling van Hallo gegevens configureren.
3. Een T-SQL-opdracht tooload Hallo gegevens parallel worden uitgevoerd in een nieuwe databasetabel.

Zie voor een zelfstudie [laden van gegevens uit Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

## <a name="recommendations"></a>Aanbevelingen
Veel van onze partners hebben bij het laden van oplossingen. toofind meer, een overzicht van onze [oplossingspartners][solution partners]. 

Als uw gegevens afkomstig is van een niet-relationele bron en u wilt dat deze in SQL Data Warehouse u tooload moet tootransform in rijen en kolommen voordat u het laden. Hallo getransformeerd gegevens hoeft niet toobe opgeslagen in een database, deze kan worden opgeslagen in tekstbestanden.

Statistieken maken voor zojuist geladen gegevens. Azure SQL Data Warehouse bevat nog geen functionaliteit voor het automatisch maken of bijwerken van statistieken.  In de volgorde tooget Hallo optimale prestaties van uw query's is het belangrijk toocreate statistieken voor alle kolommen van alle tabellen na Hallo eerst laden of belangrijke wijzigingen plaatsvinden in Hallo-gegevens.  Zie voor meer informatie [statistieken][Statistics].

## <a name="next-steps"></a>Volgende stappen
Zie voor meer tips voor het ontwikkeling Hallo [overzicht voor ontwikkelaars][development overview].

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
