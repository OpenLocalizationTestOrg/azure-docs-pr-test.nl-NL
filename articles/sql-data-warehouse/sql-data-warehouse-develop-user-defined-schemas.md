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
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="7dd6a-103">Gebruiker gedefinieerde schema's in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7dd6a-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="7dd6a-104">Traditionele datawarehouses vaak gebruik afzonderlijke databases toocreate toepassingsgrenzen op basis van de werkbelasting, domein of beveiliging.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-104">Traditional data warehouses often use separate databases toocreate application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="7dd6a-105">Een traditionele SQL Server datawarehouse kan bijvoorbeeld een faseringsdatabase, een datawarehouse-database en sommige gegevens datamart-databases.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="7dd6a-106">In deze topologie wordt elke database uitgevoerd als een werkbelasting en de beveiligingsgrens in Hallo-architectuur.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-106">In this topology each database operates as a workload and security boundary in hello architecture.</span></span>

<span data-ttu-id="7dd6a-107">Daarentegen, voert SQL Data Warehouse Hallo gehele datawarehouse-workload binnen één database.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-107">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="7dd6a-108">Joins zijn niet toegestaan cross-database.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="7dd6a-109">SQL Data Warehouse verwacht daarom alle tabellen die worden gebruikt door Hallo datawarehouse toobe opgeslagen in één Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-109">Therefore SQL Data Warehouse expects all tables used by hello warehouse toobe stored within hello one database.</span></span>

> [!NOTE]
> <span data-ttu-id="7dd6a-110">SQL Data Warehouse biedt geen ondersteuning voor meerdere databasequery's van elk type.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="7dd6a-111">Daarom moet datawarehouse-implementaties die gebruikmaken van dit patroon toobe herzien.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-111">Consequently, data warehouse implementations that leverage this pattern will need toobe revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="7dd6a-112">Aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="7dd6a-112">Recommendations</span></span>
<span data-ttu-id="7dd6a-113">Dit zijn aanbevelingen voor de consolidatie van werkbelastingen, beveiliging, domein en functionele grenzen met behulp van de gebruiker gedefinieerde schema</span><span class="sxs-lookup"><span data-stu-id="7dd6a-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="7dd6a-114">Gebruik een SQL Data Warehouse-database toorun uw hele datawarehouse-workload</span><span class="sxs-lookup"><span data-stu-id="7dd6a-114">Use one SQL Data Warehouse database toorun your entire data warehouse workload</span></span>
2. <span data-ttu-id="7dd6a-115">Consolideren van uw bestaande datawarehouse omgeving toouse een SQL Data Warehouse-database</span><span class="sxs-lookup"><span data-stu-id="7dd6a-115">Consolidate your existing data warehouse environment toouse one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="7dd6a-116">Hefboomwerking **gebruiker gedefinieerde schema's** tooprovide Hallo grens eerder geïmplementeerd met behulp van databases.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-116">Leverage **user-defined schemas** tooprovide hello boundary previously implemented using databases.</span></span>

<span data-ttu-id="7dd6a-117">Als de gebruiker gedefinieerde schema's zijn niet eerder is gebruikt, hebt u een schone lei.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="7dd6a-118">Hallo oude databasenaam als basis Hallo gewoon gebruiken voor de gebruiker gedefinieerde schema's in SQL Data Warehouse-database Hallo.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-118">Simply use hello old database name as hello basis for your user-defined schemas in hello SQL Data Warehouse database.</span></span>

<span data-ttu-id="7dd6a-119">Als de schema's al zijn gebruikt hebt u een aantal opties:</span><span class="sxs-lookup"><span data-stu-id="7dd6a-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="7dd6a-120">Hallo verouderde schemanamen verwijderen en opnieuw beginnen</span><span class="sxs-lookup"><span data-stu-id="7dd6a-120">Remove hello legacy schema names and start fresh</span></span>
2. <span data-ttu-id="7dd6a-121">Hallo verouderde schemanamen door vooraf in behandeling Hallo oude naam toohello tabel schemanaam behouden</span><span class="sxs-lookup"><span data-stu-id="7dd6a-121">Retain hello legacy schema names by pre-pending hello legacy schema name toohello table name</span></span>
3. <span data-ttu-id="7dd6a-122">Hallo verouderde schemanamen behouden door het implementeren van weergaven via Hallo-tabel in een extra schema toore-structuur van oude Hallo schema maken.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-122">Retain hello legacy schema names by implementing views over hello table in an extra schema toore-create hello old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="7dd6a-123">Op de eerste inspectie lijkt optie 3 Hallo meest interessante optie.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-123">On first inspection option 3 may seem like hello most appealing option.</span></span> <span data-ttu-id="7dd6a-124">Hallo duivelse is echter in detail Hallo.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-124">However, hello devil is in hello detail.</span></span> <span data-ttu-id="7dd6a-125">Weergaven zijn alleen-lezen in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="7dd6a-126">Wijzigingen van gegevens of de tabel moet toobe Hallo basistabel uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-126">Any data or table modification would need toobe performed against hello base table.</span></span> <span data-ttu-id="7dd6a-127">Optie 3 introduceert bovendien een laag van weergaven in uw systeem.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="7dd6a-128">U kunt de toogive deze extra voorzichtig als u weergaven in uw architectuur al.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-128">You might want toogive this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="7dd6a-129">Voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="7dd6a-129">Examples:</span></span>
<span data-ttu-id="7dd6a-130">Implementeren van de gebruiker gedefinieerde schema's op basis van de databasenamen van de</span><span class="sxs-lookup"><span data-stu-id="7dd6a-130">Implement user-defined schemas based on database names</span></span>

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

<span data-ttu-id="7dd6a-131">Behouden verouderde schema benoemd door de vooraf in behandeling toohello tabelnaam.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-131">Retain legacy schema names by pre-pending them toohello table name.</span></span> <span data-ttu-id="7dd6a-132">Schema's gebruiken voor Hallo werkbelasting grens.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-132">Use schemas for hello workload boundary.</span></span>

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

<span data-ttu-id="7dd6a-133">Verouderde schemanamen met weergaven behouden</span><span class="sxs-lookup"><span data-stu-id="7dd6a-133">Retain legacy schema names using views</span></span>

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
> <span data-ttu-id="7dd6a-134">Eventuele wijzigingen in de strategie voor schema moet een overzicht van het beveiligingsmodel Hallo voor Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-134">Any change in schema strategy needs a review of hello security model for hello database.</span></span> <span data-ttu-id="7dd6a-135">In veel gevallen mogelijk kunnen toosimplify Hallo beveiligingsmodel door machtigingen op het schemaniveau hello te wijzen.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-135">In many cases you might be able toosimplify hello security model by assigning permissions at hello schema level.</span></span> <span data-ttu-id="7dd6a-136">Als u meer gedetailleerde machtigingen zijn vereist, kunt u databaserollen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7dd6a-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7dd6a-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7dd6a-137">Next steps</span></span>
<span data-ttu-id="7dd6a-138">Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].</span><span class="sxs-lookup"><span data-stu-id="7dd6a-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
