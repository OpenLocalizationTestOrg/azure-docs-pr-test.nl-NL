---
title: aaaOperating Query Store in Azure SQL Database
description: Meer informatie over hoe toooperate Hallo Query Store in Azure SQL Database
keywords: 
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: 0cccf6bd-1327-44f7-a6f9-8eff0c210463
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: sqldb-performance
ms.workload: data-management
ms.date: 11/08/2016
ms.author: bonova
ms.openlocfilehash: ab741e49685bf6df3bceab219aaf57ea51cdb25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="operating-hello-query-store-in-azure-sql-database"></a>Operationele Hallo Query Store in Azure SQL Database
Query Store in Azure is een volledig beheerde databasefunctie die voortdurend verzamelt en toont gedetailleerde historische informatie over alle query's. U kunt zien over Query Store als vergelijkbare tooan-vliegtuig zwarte gegevens doos die aanzienlijk vereenvoudigt queryprestaties probleemoplossing voor cloud en on-premises-klanten. Dit artikel wordt uitgelegd dat bepaalde aspecten van het besturingssysteem van de Query Store in Azure. Met deze vooraf verzamelde querygegevens kunt u snel te analyseren en oplossen van prestatieproblemen en dus besteden meer tijd aan hun bedrijf. 

Query Store is [wereldwijd beschikbare](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) in Azure SQL Database sinds November 2015 opgehaald. Query Store is Hallo basis voor analyse van prestaties en het afstemmen van functies, zoals [SQL Database Advisor en Prestatiedashboard](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). Op Hallo moment van publicatie van dit artikel, wordt Query Store uitgevoerd in meer dan 200.000 gebruikersdatabases in Azure, verzamelen van informatie voor verschillende maanden, zonder onderbreking van de query gerelateerd.

> [!IMPORTANT]
> Microsoft is bezig Hallo van het Queryarchief voor alle Azure SQL-databases (bestaande en nieuwe) activeren. 
> 
> 

## <a name="optimal-query-store-configuration"></a>Configuratie voor optimale Query Store
Deze sectie beschrijft optimale standaardconfiguratie-instellingen die ontworpen tooensure betrouwbare werking van Hallo Query Store en afhankelijke onderdelen, zoals zijn [SQL Database Advisor en Prestatiedashboard](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). Standaard-configuratie is geoptimaliseerd voor continue gegevensverzameling, is de minimale tijd besteed aan OFF/READ_ONLY statussen.

| Configuratie | Beschrijving | Standaard | Opmerking |
| --- | --- | --- | --- |
| MAX_STORAGE_SIZE_MB |Hallo-limiet voor Hallo gegevensruimte die Query Store kunnen worden uitgevoerd binnen de klantendatabase z |100 |Afgedwongen voor nieuwe databases |
| INTERVAL_LENGTH_MINUTES |Grootte van de periode gedurende welke de verzamelde runtime-statistieken voor queryplannen worden samengevoegd en persistent definieert. Elke actieve queryplan is maximaal één rij voor een bepaalde periode met deze configuratie is gedefinieerd |60 |Afgedwongen voor nieuwe databases |
| STALE_QUERY_THRESHOLD_DAYS |Op basis van tijd opschonen-beleid waarmee wordt bepaald Hallo bewaarperiode van persistente runtime-statistieken en niet-actieve query 's |30 |Afgedwongen voor nieuwe databases en databases met een eerdere standaard (367) |
| SIZE_BASED_CLEANUP_MODE |Hiermee geeft u op of automatische opruimen plaats vindt wanneer de gegevensgrootte van het Queryarchief Hallo limiet nadert |AUTO |Afgedwongen voor alle databases |
| QUERY_CAPTURE_MODE |Hiermee geeft u op of alle query's of alleen een subset van query's worden bijgehouden |AUTO |Afgedwongen voor alle databases |
| FLUSH_INTERVAL_SECONDS |Hiermee geeft u de maximale periode gedurende welke vastgelegde runtime-statistieken worden bewaard in het geheugen voordat toodisk |900 |Afgedwongen voor nieuwe databases |
|  | | | |

> [!IMPORTANT]
> Deze standaardwaarden worden automatisch toegepast in de laatste fase Hallo van activering van de Query Store in alle Azure SQL-databases (Zie belangrijke opmerking voorgaande). Na deze licht up won't op Azure SQL Database, configuratiewaarden die door klanten, tenzij ze negatieve invloed hebben op primaire werkbelasting of betrouwbare operations Hallo Query Store worden gewijzigd.
> 
> 

Als u toostay met uw aangepaste instellingen wilt, gebruikt [ALTER DATABASE met Query Store opties](https://msdn.microsoft.com/library/bb522682.aspx) toorevert configuratie toohello eerdere status. Bekijk [Best Practices Hello Query Store](https://msdn.microsoft.com/library/mt604821.aspx) in volgorde toolearn hoogste optimale configuratieparameters gekozen.

## <a name="next-steps"></a>Volgende stappen
[SQL Database Performance Insight](sql-database-performance.md)

## <a name="additional-resources"></a>Aanvullende bronnen
Voor meer informatie het uitchecken Hallo artikelen te volgen:

* [Een data zwarte doos voor uw database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database) 
* [Bewaking van prestaties door met behulp van Hallo Query Store](https://msdn.microsoft.com/library/dn817826.aspx)
* [Query Store gebruiksscenario 's](https://msdn.microsoft.com/library/mt614796.aspx)
* [Bewaking van prestaties door met behulp van Hallo Query Store](https://msdn.microsoft.com/library/dn817826.aspx) 

