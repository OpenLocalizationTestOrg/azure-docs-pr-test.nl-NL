---
title: aaaManage rekencapaciteit in Azure SQL Data Warehouse (overzicht) | Microsoft Docs
description: Prestaties scale-out mogelijkheden in Azure SQL Data Warehouse. Uitbreiden door dwu's aan te passen of onderbreken en hervatten van compute resources toosave kosten.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a>De rekencapaciteit in Azure SQL Data Warehouse (overzicht) beheren
> [!div class="op_single_selector"]
> * [Overzicht](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

Hallo-architectuur van SQL Data Warehouse scheidt opslag en berekeningen, zodat elke tooscale onafhankelijk. Als gevolg hiervan mag compute onafhankelijk van de hoeveelheid gegevens Hallo geschaalde toomeet prestatie-eisen. Een natuurlijke gevolg van deze architectuur is dat [facturering] [ billed] voor berekeningen en opslag is gescheiden. 

Dit overzicht beschrijft hoe uitbreiden werkt met SQL Data Warehouse en hoe tooutilize Hallo onderbreken, hervatten en scale-mogelijkheden van SQL Data Warehouse. Raadpleeg Hallo [data warehouse units (dwu's)] [ data warehouse units (DWUs)] pagina toolearn dwu's en prestaties van de relatie. 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a>Hoe compute beheerbewerkingen werken in SQL Data Warehouse
Hallo-architectuur voor SQL Data Warehouse bestaat uit een beheerknooppunt, rekenknooppunten en Hallo opslaglaag verspreid over 60 distributies. 

Tijdens een normale actieve sessie in SQL Data Warehouse het hoofdknooppunt van het systeem beheert Hallo metagegevens en Hallo gedistribueerde queryoptimalisatie bevat. Onder deze node head zijn uw rekenknooppunten en uw storage-laag. Voor een 400 DWU heeft uw systeem één hoofdknooppunt, vier rekenknooppunten en Hallo opslaglaag, die bestaan uit 60 distributies. 

Wanneer u een schaal ondergaan of bewerking onderbreken, Hallo system eerst is funest alle binnenkomende query's en vervolgens teruggedraaid transacties tooensure een consistente status. Voor scale-bewerkingen vindt schalen alleen plaats wanneer deze transactionele terugdraaien is voltooid. Voor het uitvoeren van een scale-up Hallo system bepalingen Hallo extra gewenste aantal rekenknooppunten en begint vervolgens met de Hallo knooppunten toohello opslag berekeningslaag opnieuw te koppelen. Voor een bewerking omlaag schalen hello overbodige knooppunten worden vrijgegeven en Hallo resterende compute nodes toohello kunt u het juiste aantal distributies opnieuw zichzelf koppelen. Voor een bewerking onderbreken compute alle knooppunten worden vrijgegeven en uw systeem ietwat tal van metagegevens operations tooleave uw laatste systeem stabiel is.

| DWU  | \#van rekenknooppunten | \#van distributies per knooppunt |
| ---- | ------------------ | ---------------------------- |
| 100  | 1                  | 60                           |
| 200  | 2                  | 30                           |
| 300  | 3                  | 20                           |
| 400  | 4                  | 15                           |
| 500  | 5                  | 12                           |
| 600  | 6                  | 10                           |
| 1000 | 10                 | 6                            |
| 1200 | 12                 | 5                            |
| 1500 | 15                 | 4                            |
| 2000 | 20                 | 3                            |
| 3000 | 30                 | 2                            |
| 6000 | 60                 | 1                            |

Hallo drie primaire functies voor het beheren van compute zijn:

1. Onderbreken
2. Hervatten
3. Schalen

Elk van deze bewerkingen kan toocomplete van enkele minuten duren. Als u automatisch bent schalen/onderbreken/hervatten klikt, kunt u tooimplement logica tooensure dat bepaalde bewerkingen zijn voltooid voordat u doorgaat met een andere actie. 

Controleren van de status van database Hallo via verschillende eindpunten kunt u toocorrectly implementeren automatisering van dergelijke bewerkingen. Hallo-portal biedt melding na voltooiing van een bewerking en Hallo databases huidige status, maar is niet toegestaan voor de programmatische controle van status. 

>  [!NOTE]
>
>  COMPUTE beheerfunctionaliteit bestaat niet in alle eindpunten.
>
>  

|              | Onderbreken/hervatten | Schalen | Controleer de databasestatus van de |
| ------------ | ------------ | ----- | -------------------- |
| Azure Portal | Ja          | Ja   | **Nee**               |
| PowerShell   | Ja          | Ja   | Ja                  |
| REST API     | Ja          | Ja   | Ja                  |
| T-SQL        | **Nee**       | Ja   | Ja                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Scale compute

Prestaties in SQL Data Warehouse wordt gemeten in [data warehouse units (dwu's)] [ data warehouse units (DWUs)] dit is een abstracte meting van de compute-bronnen zoals CPU, geheugen en i/o-bandbreedte. Een gebruiker die u tooscale hun systeemprestaties wenst kunt doen met behulp van verschillende middelen zoals via het Hallo-portal, T-SQL en REST-API's. 

### <a name="how-do-i-scale-compute"></a>Hoe ik compute schalen?
Rekencapaciteit wordt voor u SQL Data Warehouse beheerd door Hallo DWU-instelling te wijzigen. Prestaties [lineair] [ linearly] als u meer DWU voor bepaalde bewerkingen toevoegt.  We bieden DWU-aanbiedingen die ervoor zorgen dat de prestaties van uw merkbaar wordt veranderen wanneer u uw systeem omhoog of omlaag schalen. 

tooadjust dwu's, kunt u een van deze afzonderlijke methoden kunt gebruiken.

* [Schaal rekenkracht met Azure portal][Scale compute power with Azure portal]
* [Schaal rekenkracht met PowerShell][Scale compute power with PowerShell]
* [De rekencapaciteit schaal met REST-API 's][Scale compute power with REST APIs]
* [Schaal rekenkracht met TSQL][Scale compute power with TSQL]

### <a name="how-many-dwus-should-i-use"></a>Het aantal dwu's moet ik gebruiken?

toounderstand welke de ideale DWU-waarde is, probeer omhoog en omlaag schalen en na het laden van uw gegevens enkele query's uit te voeren. Omdat schalen snel is, kunt u verschillende prestatieniveaus proberen in een uur of minder. 

> [!Note] 
> SQL Data Warehouse is ontworpen tooprocess grote hoeveelheden gegevens. toosee-mogelijkheden voor schaling vooral op grotere Dwu ervan waar u wilt dat toouse een grote gegevensset die nadert of hoger is dan 1 TB.

Aanbevelingen voor het zoeken naar Hallo best DWU voor uw workload:

1. Beginnen met het selecteren van een kleinere DWU-prestatieniveau voor een datawarehouse in ontwikkeling.  Een goed uitgangspunt is DW400 of DW200.
2. De toepassingsprestaties van uw te bewaken, toohello prestaties die u merkt observeren Hallo aantal dwu's geselecteerd vergeleken.
3. Bepalen hoeveel prestatievermogen sneller of langzamer lineaire schaal ervan uitgaande dat moet worden voor u tooreach Hallo optimaal prestatieniveau voor uw vereisten.
4. Vergroten of verkleinen Hallo aantal dwu's in verhouding toohow veel sneller of langzamer dat u wilt dat uw tooperform werkbelasting. 
5. Blijven correcties totdat u een optimaal prestatieniveau voor uw zakelijke vereisten.

> [!NOTE]
>
> Prestaties van query's worden alleen verhoogd met meer garandeert als Hallo werk kan worden gesplitst tussen rekenknooppunten. Als u merkt dat schalen niet van de prestaties van uw wijzigen is, check onze artikelen toocheck of uw gegevens ongelijkmatig verdeeld is of als u een grote hoeveelheid gegevensverplaatsing introduceren afstemmen van de prestaties. 

### <a name="when-should-i-scale-dwus"></a>Wanneer moet ik dwu's schalen?
Dwu's schalen wijzigt Hallo belangrijke scenario's te volgen:

1. Prestaties van systeem voor scans, aggregaties en CTAS instructies Hallo wijzigen lineair
2. Hallo aantal en schrijfprogramma te verhogen bij het laden met PolyBase
3. Maximum aantal gelijktijdige query's en gelijktijdigheid sleuven

Aanbevelingen voor wanneer tooscale dwu's:

1. Voordat u een zware laad- of transformatiebewerking bewerking uitvoert, opschalen dwu's zodat uw gegevens sneller beschikbaar is.
2. Tijdens de kantooruren piek, schalen tooaccommodate grotere aantallen gelijktijdige query's. 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>De rekencapaciteit onderbreken
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

een database toopause gebruik van deze afzonderlijke methoden.

* [Compute onderbreken met de Azure-portal][Pause compute with Azure portal]
* [De rekencapaciteit onderbreken met PowerShell][Pause compute with PowerShell]
* [De rekencapaciteit onderbreken met REST-API 's][Pause compute with REST APIs]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Compute hervatten
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

een database tooresume gebruik van deze afzonderlijke methoden.

* [De berekeningen hervatten met Azure portal][Resume compute with Azure portal]
* [De berekeningen hervatten met PowerShell][Resume compute with PowerShell]
* [De berekeningen hervatten met REST-API 's][Resume compute with REST APIs]

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a>Controleer de databasestatus van de 

een database tooresume gebruik van deze afzonderlijke methoden.

- [Controleer de databasestatus van de met T-SQL][Check database state with T-SQL]
- [Controleer de databasestatus van de met PowerShell][Check database state with PowerShell]
- [Controleer de databasestatus van de met de REST-API 's][Check database state with REST APIs]

## <a name="permissions"></a>Machtigingen

Schalen Hallo-database vereist Hallo machtigingen die zijn beschreven in [ALTER DATABASE][ALTER DATABASE].  Onderbreken en hervatten vereisen Hallo [SQL DB Contributor] [ SQL DB Contributor] machtiging specifiek Microsoft.Sql/servers/databases/action.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Volgende stappen
Raadpleeg toohello artikelen toohelp u enkele aanvullende prestatie-concepten begrijpt te volgen:

* [Werkbelasting en gelijktijdigheid management][Workload and concurrency management]
* [Overzicht van de tabel-ontwerp][Table design overview]
* [Tabeldistributie][Table distribution]
* [Tabel indexeren][Table indexing]
* [Partitioneren van tabel][Table partitioning]
* [Tabelstatistieken][Table statistics]
* [Aanbevolen procedures][Best practices]

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
