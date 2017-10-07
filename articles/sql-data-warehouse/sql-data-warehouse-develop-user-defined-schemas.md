---
title: aaaUser gedefinieerde schema's in SQL Data Warehouse | Microsoft Docs
description: Tips voor het gebruik van Transact-SQL-schema's in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a>Gebruiker gedefinieerde schema's in SQL Data Warehouse
Traditionele datawarehouses vaak gebruik afzonderlijke databases toocreate toepassingsgrenzen op basis van de werkbelasting, domein of beveiliging. Een traditionele SQL Server datawarehouse kan bijvoorbeeld een faseringsdatabase, een datawarehouse-database en sommige gegevens datamart-databases. In deze topologie wordt elke database uitgevoerd als een werkbelasting en de beveiligingsgrens in Hallo-architectuur.

Daarentegen, voert SQL Data Warehouse Hallo gehele datawarehouse-workload binnen één database. Joins zijn niet toegestaan cross-database. SQL Data Warehouse verwacht daarom alle tabellen die worden gebruikt door Hallo datawarehouse toobe opgeslagen in één Hallo-database.

> [!NOTE]
> SQL Data Warehouse biedt geen ondersteuning voor meerdere databasequery's van elk type. Daarom moet datawarehouse-implementaties die gebruikmaken van dit patroon toobe herzien.
> 
> 

## <a name="recommendations"></a>Aanbevelingen
Dit zijn aanbevelingen voor de consolidatie van werkbelastingen, beveiliging, domein en functionele grenzen met behulp van de gebruiker gedefinieerde schema

1. Gebruik een SQL Data Warehouse-database toorun uw hele datawarehouse-workload
2. Consolideren van uw bestaande datawarehouse omgeving toouse een SQL Data Warehouse-database
3. Hefboomwerking **gebruiker gedefinieerde schema's** tooprovide Hallo grens eerder geïmplementeerd met behulp van databases.

Als de gebruiker gedefinieerde schema's zijn niet eerder is gebruikt, hebt u een schone lei. Hallo oude databasenaam als basis Hallo gewoon gebruiken voor de gebruiker gedefinieerde schema's in SQL Data Warehouse-database Hallo.

Als de schema's al zijn gebruikt hebt u een aantal opties:

1. Hallo verouderde schemanamen verwijderen en opnieuw beginnen
2. Hallo verouderde schemanamen door vooraf in behandeling Hallo oude naam toohello tabel schemanaam behouden
3. Hallo verouderde schemanamen behouden door het implementeren van weergaven via Hallo-tabel in een extra schema toore-structuur van oude Hallo schema maken.

> [!NOTE]
> Op de eerste inspectie lijkt optie 3 Hallo meest interessante optie. Hallo duivelse is echter in detail Hallo. Weergaven zijn alleen-lezen in SQL Data Warehouse. Wijzigingen van gegevens of de tabel moet toobe Hallo basistabel uitgevoerd. Optie 3 introduceert bovendien een laag van weergaven in uw systeem. U kunt de toogive deze extra voorzichtig als u weergaven in uw architectuur al.
> 
> 

### <a name="examples"></a>Voorbeelden:
Implementeren van de gebruiker gedefinieerde schema's op basis van de databasenamen van de

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

Behouden verouderde schema benoemd door de vooraf in behandeling toohello tabelnaam. Schema's gebruiken voor Hallo werkbelasting grens.

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

Verouderde schemanamen met weergaven behouden

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> Eventuele wijzigingen in de strategie voor schema moet een overzicht van het beveiligingsmodel Hallo voor Hallo-database. In veel gevallen mogelijk kunnen toosimplify Hallo beveiligingsmodel door machtigingen op het schemaniveau hello te wijzen. Als u meer gedetailleerde machtigingen zijn vereist, kunt u databaserollen gebruiken.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
