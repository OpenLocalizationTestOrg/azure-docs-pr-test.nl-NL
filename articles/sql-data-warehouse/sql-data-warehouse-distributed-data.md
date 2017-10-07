---
title: aaaHow gegevens werkt in Azure SQL Data Warehouse gedistribueerd | Microsoft Docs
description: Meer informatie over hoe gegevens worden gedistribueerd voor Massively parallelle verwerking (MPP) en Hallo opties voor het distribueren van tabellen in Azure SQL Data Warehouse en Parallel Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: bae494a6-7ac5-4c38-8ca3-ab2696c63a9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 9a712d8d5251e4391ede245105918283aaa4b193
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-data-and-distributed-tables-for-massively-parallel-processing-mpp"></a>Gedistribueerde gegevens en gedistribueerde tabellen voor Massively parallelle verwerking (MPP)
Meer informatie over hoe gebruikersgegevens wordt gedistribueerd in Azure SQL Data Warehouse en Parallel Data Warehouse van Microsoft Massively parallelle verwerking MPP-systemen zijn. Het ontwerpen van uw datawarehouse toouse helpt gedistribueerde gegevens effectief u tooachieve Hallo queryverwerking voordelen van Hallo MPP-architectuur. Enkele database ontwerpbeslissingen die kunnen een aanzienlijke gevolgen hebben voor verbetering van de prestaties van query's.  

> [!NOTE]
> Azure SQL Data Warehouse en Parallel Data Warehouse gebruik Hallo dezelfde Massively Parallel Processing (MPP) ontwerpen, maar ze hebben een paar verschillen vanwege Hallo onderliggende platform. SQL Data Warehouse is een Platform als een Service (PaaS) die wordt uitgevoerd op Azure. Parallel Data Warehouse wordt uitgevoerd op Analytics Platform System (AP) Dit is een lokale apparaat dat wordt uitgevoerd op Windows Server.
> 
> 

## <a name="what-is-distributed-data"></a>Wat is een gedistribueerde gegevens?
In SQL Data Warehouse en Parallel Data Warehouse verwijst gedistribueerde gegevens toouser gegevens die zijn opgeslagen op meerdere locaties via Hallo MPP-systeem. Elk van deze locaties fungeert als een onafhankelijke opslag en verwerkingseenheid dat query's op het gedeelte van Hallo gegevens wordt uitgevoerd. Gedistribueerde gegevens is fundamentele toorunning query's in parallelle tooachieve hoge queryprestaties.

toodistribute gegevens, Hallo datawarehouse wijst elke rij van de locatie van een gebruiker tabel tooone gedistribueerd.  U kunt distribueren tabellen met een hash-distributiemethode of een round robin-methode. Hallo distributiemethode is opgegeven in Hallo CREATE TABLE-instructie. 

## <a name="hash-distributed-tables"></a>Gedistribueerd hash tabellen
Hallo volgende diagram illustreert hoe een volledige (tabel niet gedistribueerd) wordt opgeslagen als een tabel met hash gedistribueerd. Een deterministische functie worden toegewezen voor elke rij toobelong tooone distributie. In de tabeldefinitie hello, wordt een van de kolommen Hallo aangewezen als Hallo distributie kolom. Hallo hash-functie gebruikt Hallo-waarde in Hallo distributie kolom tooassign elke rij tooa distributie.

Er zijn prestatie-overwegingen voor Hallo selectie van een kolom van de distributie, zoals onderscheidbaarheid gegevens Tijdverschil en Hallo typen query's uitvoeren op Hallo-systeem.

![Gedistribueerde tabel](media/sql-data-warehouse-distributed-data/hash-distributed-table.png "gedistribueerde tabel")  

* Elke rij hoort tooone distributie.  
* Een deterministische hash-algoritme worden toegewezen voor elke rij tooone distributie.  
* het aantal rijen per distributiepunt Hallo varieert zoals aangegeven in de verschillende grootten Hallo van tabellen.

## <a name="round-robin-distributed-tables"></a>Round robin gedistribueerde tabellen
Een gedistribueerde tabel round robin distribueert Hallo rijen door toe te wijzen van elke rij tooa distributie in de juiste volgorde. Snelle tooload gegevens in een round robin-tabel is, maar de prestaties van query's mogelijk langzamer.  Lid worden van een tabel round robin meestal vereist reshuffling Hallo rijen tooenable Hallo query tooproduce een accuraat resultaat opleveren, die duurt.

## <a name="distributed-storage-locations-are-called-distributions"></a>Gedistribueerde opslaglocaties worden distributies genoemd
Elke gedistribueerde locatie heet een distributiepunt. Wanneer een query wordt parallel uitgevoerd, voert elke distributie een SQL-query op het gedeelte van Hallo-gegevens. SQL Data Warehouse maakt gebruik van SQL-Database toorun Hallo query. Parallel Data Warehouse maakt gebruik van SQL Server toorun Hallo-query. Dit architectuurontwerp niets wordt gedeeld fundamentele tooachieving scale-out is parallelle berekeningen.

### <a name="can-i-view-hello-distributions"></a>Kan ik Hallo Distributies weergeven?
Elk distributiepunt heeft een distributie-ID en zichtbaar is in systeemweergaven die betrekking tooSQL Data Warehouse en Parallel Data Warehouse hebben. U kunt Hallo distributie ID tootroubleshoot prestaties van query's en andere problemen. Zie voor een lijst van de systeemweergaven Hallo Hallo [MPP systeemweergave](sql-data-warehouse-reference-tsql-statements.md).

## <a name="difference-between-a-distribution-and-a-compute-node"></a>Verschil tussen een distributiepunt en een rekenknooppunt
Een distributiepunt is de basiseenheid Hallo voor gedistribueerde gegevens op te slaan en de verwerking van parallelle query's. Distributies zijn gegroepeerd in rekenknooppunten. Elk rekenknooppunt houdt een of meer verdelingen.  

* Rekenknooppunten Analytics Platform System gebruikt als een centrale onderdeel van Hallo hardware-architectuur en uitbreidbare mogelijkheden. Deze gebruikt altijd acht distributies per rekenknooppunt, zoals wordt weergegeven in het diagram Hallo voor gedistribueerde hash tabellen. Hallo aantal rekenknooppunten, en daarom Hallo aantal distributies, wordt bepaald door het aantal rekenknooppunten die u voor Hallo toestel koopt Hallo. Als u acht rekenknooppunten koopt, krijgt u bijvoorbeeld 64 distributies (8 knooppunten x 8 distributies/rekenknooppunt). 
* SQL Data Warehouse heeft een vast aantal 60 distributies en een flexibele aantal rekenknooppunten. Hallo rekenknooppunten worden geïmplementeerd met Azure-resources berekeningen en opslag. het aantal rekenknooppunten Hallo kunt volgens toohello back-end service werkbelasting en Hallo computercapaciteit (dwu's) u voor het datawarehouse Hallo opgeeft wijzigen. Wanneer het aantal rekenknooppunten hello wordt gewijzigd, wordt het aantal distributies per rekenknooppunt Hallo ook gewijzigd. 

### <a name="can-i-view-hello-compute-nodes"></a>Kan ik Hallo Compute nodes weergeven?
Elk rekenknooppunt heeft een knooppunt-ID en zichtbaar is in systeemweergaven die betrekking tooSQL Data Warehouse en Parallel Data Warehouse hebben.  U ziet het rekenknooppunt Hallo voor Hallo node_id kolom in systeemweergaven waarvan de naam met sys.pdw_nodes begint. Zie voor een lijst van de systeemweergaven Hallo Hallo [MPP systeemweergave](sql-data-warehouse-reference-tsql-statements.md).

## <a name="Replicated"></a>Gerepliceerde tabellen
Een tabel die is gerepliceerd heeft een volledig kopie van Hallo tabel op elk rekenknooppunt worden opgeslagen. Bezig met het repliceren van een tabel, verwijdert Hallo nodig tootransfer gegevens tussen rekenknooppunten voordat een join of aggregatie. Gerepliceerde tabellen zijn alleen mogelijk met kleine tabellen vanwege Hallo extra opslag vereist toostore Hallo volledige tabel op elk rekenknooppunt.  

Hallo toont volgende diagram een gerepliceerde tabel die is opgeslagen op elk rekenknooppunt. Hallo gerepliceerde tabel is volledig gekopieerde tooa distributiedatabase op elk rekenknooppunt voor SQL Data Warehouse. Parallel Data Warehouse, gerepliceerde tabel Hallo opgeslagen over alle schijven die zijn toegewezen toohello rekenknooppunt.  Deze schijf-strategie is geïmplementeerd met behulp van SQL Server-bestandsgroepen.  

![Gerepliceerde tabel](media/sql-data-warehouse-distributed-data/replicated-table.png "gerepliceerde tabel") 

## <a name="next-steps"></a>Volgende stappen
toouse gedistribueerd tabellen effectief, Zie [tabellen in SQL Data Warehouse distribueren](sql-data-warehouse-tables-distribute.md)  

