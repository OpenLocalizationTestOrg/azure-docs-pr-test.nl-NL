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
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="12216-103">SQL Data Warehouse terugzetten</span><span class="sxs-lookup"><span data-stu-id="12216-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="12216-104">[Overzicht][Overview]</span><span class="sxs-lookup"><span data-stu-id="12216-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="12216-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="12216-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="12216-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="12216-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="12216-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="12216-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="12216-108">SQL Data Warehouse biedt zowel lokale als geografische herstelacties als onderdeel van de datawarehouse disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="12216-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="12216-109">Gebruik datawarehouse-back-ups toorestore uw datawarehouse tooa terugzetten punt in de primaire regio Hallo of gebruik van geografisch redundante back-ups toorestore tooa verschillende geografische regio.</span><span class="sxs-lookup"><span data-stu-id="12216-109">Use data warehouse backups toorestore your data warehouse tooa restore point in hello primary region, or use geo-redundant backups toorestore tooa different geographical region.</span></span> <span data-ttu-id="12216-110">Dit artikel wordt uitgelegd Hallo details van het herstellen van een datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="12216-110">This article explains hello specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="12216-111">Wat is er een datawarehouse te herstellen?</span><span class="sxs-lookup"><span data-stu-id="12216-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="12216-112">Een datawarehouse-herstellen van gegevens is een nieuw datawarehouse is gemaakt van een back-up van een bestaande of verwijderde datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="12216-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="12216-113">Hallo back-up datawarehouse Hallo herstelde datawarehouse opnieuw gemaakt op een bepaald tijdstip.</span><span class="sxs-lookup"><span data-stu-id="12216-113">hello restored data warehouse re-creates hello backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="12216-114">Omdat SQL Data Warehouse een gedistribueerd systeem is, wordt een datawarehouse gegevens terugzetten vanuit veel back-upbestanden die zijn opgeslagen in Azure BLOB's gemaakt.</span><span class="sxs-lookup"><span data-stu-id="12216-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="12216-115">Database terugzetten is een essentieel onderdeel van een zakelijke continuïteit en noodherstel herstelstrategie omdat uw gegevens opnieuw worden gemaakt na het per ongeluk beschadigd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="12216-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="12216-116">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="12216-116">For more information, see:</span></span>

* [<span data-ttu-id="12216-117">Back-ups van SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="12216-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="12216-118">Overzicht van zakelijke continuïteit</span><span class="sxs-lookup"><span data-stu-id="12216-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="12216-119">Datawarehouse-herstelpunten</span><span class="sxs-lookup"><span data-stu-id="12216-119">Data warehouse restore points</span></span>
<span data-ttu-id="12216-120">Als een voordeel van het gebruik van Azure Premium-opslag maakt gebruik van SQL Data Warehouse Azure Storage-Blob momentopnamen toobackup Hallo primaire datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="12216-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots toobackup hello primary data warehouse.</span></span> <span data-ttu-id="12216-121">Elke momentopname is een herstelpunt dat Hallo tijd vertegenwoordigt Hallo momentopname gestart.</span><span class="sxs-lookup"><span data-stu-id="12216-121">Each snapshot has a restore point that represents hello time hello snapshot started.</span></span> <span data-ttu-id="12216-122">toorestore een datawarehouse, kies een herstelpunt en voert u een restore-opdracht.</span><span class="sxs-lookup"><span data-stu-id="12216-122">toorestore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="12216-123">SQL Data Warehouse herstelt altijd Hallo back-tooa nieuw datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="12216-123">SQL Data Warehouse always restores hello backup tooa new data warehouse.</span></span> <span data-ttu-id="12216-124">U kunt Hallo herstelde gegevensmagazijn behouden en huidige hello of een van deze verwijderen.</span><span class="sxs-lookup"><span data-stu-id="12216-124">You can either keep hello restored data warehouse and hello current one, or delete one of them.</span></span> <span data-ttu-id="12216-125">Als u wilt dat tooreplace Hallo huidige datawarehouse met Hallo hersteld datawarehouse, u deze kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="12216-125">If you want tooreplace hello current data warehouse with hello restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="12216-126">Als u een verwijderde of onderbroken datawarehouse toorestore nodig hebt, kunt u [Maak een ondersteuningsticket](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="12216-126">If you need toorestore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="12216-127">Geografisch redundante terugzetten</span><span class="sxs-lookup"><span data-stu-id="12216-127">Geo-redundant restore</span></span>
<span data-ttu-id="12216-128">U kunt uw datawarehouse tooany gegevensgebied Azure SQL Data Warehouse op het niveau van uw gekozen prestatie ondersteunende herstellen.</span><span class="sxs-lookup"><span data-stu-id="12216-128">You can restore your data warehouse tooany region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="12216-129">Houd er rekening mee dat 9000 en 18000 DWU worden niet ondersteund in alle regio's tijdens het Hallo-preview.</span><span class="sxs-lookup"><span data-stu-id="12216-129">Please note that 9000 and 18000 DWU are not supported in all regions during hello preview.</span></span>

> [!NOTE]
> <span data-ttu-id="12216-130">een geografisch redundante tooperform terugzetten die u moet niet buiten deze functie hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="12216-130">tooperform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="12216-131">Tijdlijn herstellen</span><span class="sxs-lookup"><span data-stu-id="12216-131">Restore timeline</span></span>
<span data-ttu-id="12216-132">Afgelopen zeven dagen, kunt u een database tooany beschikbaar herstelpunt binnen Hallo herstellen.</span><span class="sxs-lookup"><span data-stu-id="12216-132">You can restore a database tooany available restore point within hello last seven days.</span></span> <span data-ttu-id="12216-133">Momentopnamen elke vier uur voor tooeight start en zijn beschikbaar voor de zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="12216-133">Snapshots start every four tooeight hours and are available for seven days.</span></span> <span data-ttu-id="12216-134">Wanneer een momentopname ouder dan zeven dagen is, het verloopt en het herstelpunt is niet meer beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="12216-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="12216-135">Kosten herstellen</span><span class="sxs-lookup"><span data-stu-id="12216-135">Restore costs</span></span>
<span data-ttu-id="12216-136">Hallo opslag kosten voor Hallo herstelde datawarehouse wordt gefactureerd snelheid hello Azure Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="12216-136">hello storage charge for hello restored data warehouse is billed at hello Azure Premium Storage rate.</span></span> 

<span data-ttu-id="12216-137">Als u een herstelde datawarehouse onderbreekt, wordt u in rekening gebracht voor opslag snelheid hello Azure Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="12216-137">If you pause a restored data warehouse, you are charged for storage at hello Azure Premium Storage rate.</span></span> <span data-ttu-id="12216-138">Hallo-voordeel van het onderbreken is dat u niet worden in rekening gebracht voor Hallo DWU computerbronnen.</span><span class="sxs-lookup"><span data-stu-id="12216-138">hello advantage of pausing is you are not charged for hello DWU computing resources.</span></span>

<span data-ttu-id="12216-139">Zie voor meer informatie over prijzen van SQL Data Warehouse [prijzen van SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="12216-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="12216-140">Gebruikt voor herstel</span><span class="sxs-lookup"><span data-stu-id="12216-140">Uses for restore</span></span>
<span data-ttu-id="12216-141">Hallo primair gebruik van datawarehouse terugzetten is toorecover gegevens na onbedoeld gegevensverlies of beschadiging.</span><span class="sxs-lookup"><span data-stu-id="12216-141">hello primary use for data warehouse restore is toorecover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="12216-142">U kunt ook gegevens datawarehouse terugzetten tooretain een back-up langer dan zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="12216-142">You can also use data warehouse restore tooretain a backup for longer than seven days.</span></span> <span data-ttu-id="12216-143">Zodra de back-up Hallo is hersteld, moet u Hallo datawarehouse online zijn en kunt onderbreken voor onbepaalde tijd toosave compute-kosten.</span><span class="sxs-lookup"><span data-stu-id="12216-143">Once hello backup is restored, you have hello data warehouse online and can pause it indefinitely toosave compute costs.</span></span> <span data-ttu-id="12216-144">Hallo onderbroken database leidt ertoe dat de opslagkosten snelheid hello Azure Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="12216-144">hello paused database incurs storage charges at hello Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="12216-145">Verwante onderwerpen</span><span class="sxs-lookup"><span data-stu-id="12216-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="12216-146">Scenario's</span><span class="sxs-lookup"><span data-stu-id="12216-146">Scenarios</span></span>
* <span data-ttu-id="12216-147">Zie voor een overzicht zakelijke continuïteit [Business continuity-overzicht](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="12216-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="12216-148">een datawarehouse tooperform herstellen, herstelt u met behulp van:</span><span class="sxs-lookup"><span data-stu-id="12216-148">tooperform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="12216-149">Azure portal, Zie [herstellen van een datawarehouse met behulp van hello Azure-portal](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="12216-149">Azure portal, see [Restore a data warehouse using hello Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="12216-150">PowerShell-cmdlets raadpleegt [herstellen van een datawarehouse met behulp van PowerShell-cmdlets](sql-data-warehouse-restore-database-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="12216-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="12216-151">REST-API's, Zie [herstellen van een datawarehouse Hallo REST-API's gebruiken](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="12216-151">REST APIs, see [Restore a data warehouse using hello REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

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
