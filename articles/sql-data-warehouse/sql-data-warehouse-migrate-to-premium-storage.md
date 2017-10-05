---
title: Uw bestaande Azure datawarehouse migreren naar premium-opslag | Microsoft Docs
description: Instructies voor het migreren van een bestaand datawarehouse naar premium-opslag
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 860e50b532b4b0a21d3be54f087730070b0e56bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-data-warehouse-to-premium-storage"></a><span data-ttu-id="97678-103">Uw datawarehouse migreren naar premium-opslag</span><span class="sxs-lookup"><span data-stu-id="97678-103">Migrate your data warehouse to premium storage</span></span>
<span data-ttu-id="97678-104">Azure SQL Data Warehouse onlangs geïntroduceerd [premium-opslag voor groter prestaties, voorspelbaarheid][premium storage for greater performance predictability].</span><span class="sxs-lookup"><span data-stu-id="97678-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="97678-105">Bestaande datawarehouses momenteel op standaardopslag kunnen nu worden gemigreerd naar de premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="97678-105">Existing data warehouses currently on standard storage can now be migrated to premium storage.</span></span> <span data-ttu-id="97678-106">U kunt profiteren van de automatische migratie van of als u liever om te beheren wanneer voor het migreren van (dit heeft betrekking op enige downtime), kunt u de migratie zelf doen.</span><span class="sxs-lookup"><span data-stu-id="97678-106">You can take advantage of automatic migration, or if you prefer to control when to migrate (which does involve some downtime), you can do the migration yourself.</span></span>

<span data-ttu-id="97678-107">Als u meer dan een datawarehouse hebt, gebruikt u de [schema voor automatische migratie] [ automatic migration schedule] om te bepalen wanneer dit wordt ook worden gemigreerd.</span><span class="sxs-lookup"><span data-stu-id="97678-107">If you have more than one data warehouse, use the [automatic migration schedule][automatic migration schedule] to determine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="97678-108">Opslagtype bepalen</span><span class="sxs-lookup"><span data-stu-id="97678-108">Determine storage type</span></span>
<span data-ttu-id="97678-109">Als u een datawarehouse hebt gemaakt voordat de volgende datums, u standaardopslag momenteel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97678-109">If you created a data warehouse before the following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="97678-110">**Regio**</span><span class="sxs-lookup"><span data-stu-id="97678-110">**Region**</span></span> | <span data-ttu-id="97678-111">**Datawarehouse gemaakt voor deze datum**</span><span class="sxs-lookup"><span data-stu-id="97678-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="97678-112">Australië - oost</span><span class="sxs-lookup"><span data-stu-id="97678-112">Australia East</span></span> |<span data-ttu-id="97678-113">Premium-opslag is nog niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="97678-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="97678-114">China - oost</span><span class="sxs-lookup"><span data-stu-id="97678-114">China East</span></span> |<span data-ttu-id="97678-115">1 november 2016</span><span class="sxs-lookup"><span data-stu-id="97678-115">November 1, 2016</span></span> |
| <span data-ttu-id="97678-116">China - noord</span><span class="sxs-lookup"><span data-stu-id="97678-116">China North</span></span> |<span data-ttu-id="97678-117">1 november 2016</span><span class="sxs-lookup"><span data-stu-id="97678-117">November 1, 2016</span></span> |
| <span data-ttu-id="97678-118">Duitsland - centraal</span><span class="sxs-lookup"><span data-stu-id="97678-118">Germany Central</span></span> |<span data-ttu-id="97678-119">1 november 2016</span><span class="sxs-lookup"><span data-stu-id="97678-119">November 1, 2016</span></span> |
| <span data-ttu-id="97678-120">Duitsland - noordoost</span><span class="sxs-lookup"><span data-stu-id="97678-120">Germany Northeast</span></span> |<span data-ttu-id="97678-121">1 november 2016</span><span class="sxs-lookup"><span data-stu-id="97678-121">November 1, 2016</span></span> |
| <span data-ttu-id="97678-122">India - west</span><span class="sxs-lookup"><span data-stu-id="97678-122">India West</span></span> |<span data-ttu-id="97678-123">Premium-opslag is nog niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="97678-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="97678-124">Japan - west</span><span class="sxs-lookup"><span data-stu-id="97678-124">Japan West</span></span> |<span data-ttu-id="97678-125">Premium-opslag is nog niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="97678-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="97678-126">Noord-centraal VS</span><span class="sxs-lookup"><span data-stu-id="97678-126">North Central US</span></span> |<span data-ttu-id="97678-127">10 november 2016</span><span class="sxs-lookup"><span data-stu-id="97678-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="97678-128">Details van de automatische migratie</span><span class="sxs-lookup"><span data-stu-id="97678-128">Automatic migration details</span></span>
<span data-ttu-id="97678-129">Standaard gaan we uw database voor u tussen 18:00 uur en 6:00 uur in uw regio lokale tijd tijdens de [schema voor automatische migratie][automatic migration schedule].</span><span class="sxs-lookup"><span data-stu-id="97678-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during the [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="97678-130">Uw bestaande datawarehouse kan niet worden gebruikt tijdens de migratie.</span><span class="sxs-lookup"><span data-stu-id="97678-130">Your existing data warehouse will be unusable during the migration.</span></span> <span data-ttu-id="97678-131">De migratie duurt ongeveer één uur per terabyte van opslag per datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="97678-131">The migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="97678-132">U wordt niet in rekening gebracht tijdens een gedeelte van de automatische migratie.</span><span class="sxs-lookup"><span data-stu-id="97678-132">You will not be charged during any portion of the automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="97678-133">Wanneer de migratie voltooid is, wordt uw datawarehouse worden weer online is en kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97678-133">When the migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="97678-134">Microsoft neemt de volgende stappen uit om de migratie (deze hoeven niet alle betrokkenheid van uw kant) te voltooien.</span><span class="sxs-lookup"><span data-stu-id="97678-134">Microsoft is taking the following steps to complete the migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="97678-135">Stel in dit voorbeeld of uw bestaande datawarehouse op een standard-opslag is momenteel met de naam 'MyDW'.</span><span class="sxs-lookup"><span data-stu-id="97678-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="97678-136">Microsoft wijzigt de naam 'MyDW' naar 'MyDW_DO_NOT_USE_ [tijdstempel]'.</span><span class="sxs-lookup"><span data-stu-id="97678-136">Microsoft renames “MyDW” to “MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="97678-137">Microsoft pauzeert 'MyDW_DO_NOT_USE_ [tijdstempel]'.</span><span class="sxs-lookup"><span data-stu-id="97678-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="97678-138">Gedurende deze tijd is een back-up gemaakt.</span><span class="sxs-lookup"><span data-stu-id="97678-138">During this time, a backup is taken.</span></span> <span data-ttu-id="97678-139">Mogelijk ziet u meerdere onderbroken en hervat als er problemen ondervindt tijdens dit proces.</span><span class="sxs-lookup"><span data-stu-id="97678-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="97678-140">Microsoft maakt een nieuw datawarehouse met de naam 'MyDW' op premium-opslag van de back-up gemaakt in stap 2.</span><span class="sxs-lookup"><span data-stu-id="97678-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from the backup taken in step 2.</span></span> <span data-ttu-id="97678-141">'MyDW' worden niet weergegeven tot na het herstellen voltooid is.</span><span class="sxs-lookup"><span data-stu-id="97678-141">“MyDW” will not appear until after the restore is complete.</span></span>
4. <span data-ttu-id="97678-142">Nadat het herstel voltooid is 'MyDW' retourneert met dezelfde magazijn eenheden en status (onderbroken of actieve) is dat deze vóór de migratie.</span><span class="sxs-lookup"><span data-stu-id="97678-142">After the restore is complete, “MyDW” returns to the same data warehouse units and state (paused or active) that it was before the migration.</span></span>
5. <span data-ttu-id="97678-143">Nadat de migratie voltooid is, verwijdert Microsoft 'MyDW_DO_NOT_USE_ [tijdstempel]'.</span><span class="sxs-lookup"><span data-stu-id="97678-143">After the migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="97678-144">De volgende instellingen uitvoeren als onderdeel van de migratie niet via:</span><span class="sxs-lookup"><span data-stu-id="97678-144">The following settings do not carry over as part of the migration:</span></span>
>
> * <span data-ttu-id="97678-145">Controle op het databaseniveau van de moet opnieuw worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="97678-145">Auditing at the database level needs to be re-enabled.</span></span>
> * <span data-ttu-id="97678-146">Firewall-regels op het databaseniveau van de moeten opnieuw worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="97678-146">Firewall rules at the database level need to be re-added.</span></span> <span data-ttu-id="97678-147">Firewallregels op serverniveau worden niet getroffen.</span><span class="sxs-lookup"><span data-stu-id="97678-147">Firewall rules at the server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="97678-148">Planning voor automatische migratie</span><span class="sxs-lookup"><span data-stu-id="97678-148">Automatic migration schedule</span></span>
<span data-ttu-id="97678-149">Automatische migraties optreden tussen 18:00 uur en 6:00 uur (lokale tijd per regio) tijdens het volgende schema van de storing.</span><span class="sxs-lookup"><span data-stu-id="97678-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during the following outage schedule.</span></span>

| <span data-ttu-id="97678-150">**Regio**</span><span class="sxs-lookup"><span data-stu-id="97678-150">**Region**</span></span> | <span data-ttu-id="97678-151">**Geschatte begindatum**</span><span class="sxs-lookup"><span data-stu-id="97678-151">**Estimated start date**</span></span> | <span data-ttu-id="97678-152">**Geschatte einddatum**</span><span class="sxs-lookup"><span data-stu-id="97678-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="97678-153">Australië - oost</span><span class="sxs-lookup"><span data-stu-id="97678-153">Australia East</span></span> |<span data-ttu-id="97678-154">Nog niet worden vastgesteld</span><span class="sxs-lookup"><span data-stu-id="97678-154">Not determined yet</span></span> |<span data-ttu-id="97678-155">Nog niet worden vastgesteld</span><span class="sxs-lookup"><span data-stu-id="97678-155">Not determined yet</span></span> |
| <span data-ttu-id="97678-156">China - oost</span><span class="sxs-lookup"><span data-stu-id="97678-156">China East</span></span> |<span data-ttu-id="97678-157">9 januari 2017</span><span class="sxs-lookup"><span data-stu-id="97678-157">January 9, 2017</span></span> |<span data-ttu-id="97678-158">13 januari 2017</span><span class="sxs-lookup"><span data-stu-id="97678-158">January 13, 2017</span></span> |
| <span data-ttu-id="97678-159">China - noord</span><span class="sxs-lookup"><span data-stu-id="97678-159">China North</span></span> |<span data-ttu-id="97678-160">9 januari 2017</span><span class="sxs-lookup"><span data-stu-id="97678-160">January 9, 2017</span></span> |<span data-ttu-id="97678-161">13 januari 2017</span><span class="sxs-lookup"><span data-stu-id="97678-161">January 13, 2017</span></span> |
| <span data-ttu-id="97678-162">Duitsland - centraal</span><span class="sxs-lookup"><span data-stu-id="97678-162">Germany Central</span></span> |<span data-ttu-id="97678-163">9 januari 2017</span><span class="sxs-lookup"><span data-stu-id="97678-163">January 9, 2017</span></span> |<span data-ttu-id="97678-164">13 januari 2017</span><span class="sxs-lookup"><span data-stu-id="97678-164">January 13, 2017</span></span> |
| <span data-ttu-id="97678-165">Duitsland - noordoost</span><span class="sxs-lookup"><span data-stu-id="97678-165">Germany Northeast</span></span> |<span data-ttu-id="97678-166">9 januari 2017</span><span class="sxs-lookup"><span data-stu-id="97678-166">January 9, 2017</span></span> |<span data-ttu-id="97678-167">13 januari 2017</span><span class="sxs-lookup"><span data-stu-id="97678-167">January 13, 2017</span></span> |
| <span data-ttu-id="97678-168">India - west</span><span class="sxs-lookup"><span data-stu-id="97678-168">India West</span></span> |<span data-ttu-id="97678-169">Nog niet worden vastgesteld</span><span class="sxs-lookup"><span data-stu-id="97678-169">Not determined yet</span></span> |<span data-ttu-id="97678-170">Nog niet worden vastgesteld</span><span class="sxs-lookup"><span data-stu-id="97678-170">Not determined yet</span></span> |
| <span data-ttu-id="97678-171">Japan - west</span><span class="sxs-lookup"><span data-stu-id="97678-171">Japan West</span></span> |<span data-ttu-id="97678-172">Nog niet worden vastgesteld</span><span class="sxs-lookup"><span data-stu-id="97678-172">Not determined yet</span></span> |<span data-ttu-id="97678-173">Nog niet worden vastgesteld</span><span class="sxs-lookup"><span data-stu-id="97678-173">Not determined yet</span></span> |
| <span data-ttu-id="97678-174">Noord-centraal VS</span><span class="sxs-lookup"><span data-stu-id="97678-174">North Central US</span></span> |<span data-ttu-id="97678-175">9 januari 2017</span><span class="sxs-lookup"><span data-stu-id="97678-175">January 9, 2017</span></span> |<span data-ttu-id="97678-176">13 januari 2017</span><span class="sxs-lookup"><span data-stu-id="97678-176">January 13, 2017</span></span> |

## <a name="self-migration-to-premium-storage"></a><span data-ttu-id="97678-177">Zelfstandige migratie naar de premium-opslag</span><span class="sxs-lookup"><span data-stu-id="97678-177">Self-migration to premium storage</span></span>
<span data-ttu-id="97678-178">Als u bepalen wilt wanneer uw uitvaltijd wordt uitgevoerd, kunt u de volgende stappen uit om te migreren van een bestaand datawarehouse op een standard-opslag naar de premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="97678-178">If you want to control when your downtime will occur, you can use the following steps to migrate an existing data warehouse on standard storage to premium storage.</span></span> <span data-ttu-id="97678-179">Als u deze optie kiest, moet u de zelfstandige migratie voltooien voordat de automatische migratie in deze regio begint.</span><span class="sxs-lookup"><span data-stu-id="97678-179">If you choose this option, you must complete the self-migration before the automatic migration begins in that region.</span></span> <span data-ttu-id="97678-180">Dit zorgt ervoor dat u het risico van de automatische migratie een conflict veroorzaken vermijden (Raadpleeg de [schema voor automatische migratie][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="97678-180">This ensures that you avoid any risk of the automatic migration causing a conflict (refer to the [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="97678-181">Zelfstandige migratie-instructies</span><span class="sxs-lookup"><span data-stu-id="97678-181">Self-migration instructions</span></span>
<span data-ttu-id="97678-182">Migreren van uw datawarehouse, gebruikt u de back-up en herstellen van functies.</span><span class="sxs-lookup"><span data-stu-id="97678-182">To migrate your data warehouse yourself, use the backup and restore features.</span></span> <span data-ttu-id="97678-183">Het gedeelte voor herstel van de migratie is ongeveer één uur per terabyte van opslag verwacht per datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="97678-183">The restore portion of the migration is expected to take around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="97678-184">Als u wilt behouden dezelfde naam na de migratie is voltooid, voert u de [stappen om te wijzigen tijdens de migratie][steps to rename during migration].</span><span class="sxs-lookup"><span data-stu-id="97678-184">If you want to keep the same name after migration is complete, follow the [steps to rename during migration][steps to rename during migration].</span></span>

1. <span data-ttu-id="97678-185">[Onderbreken] [ Pause] uw datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="97678-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="97678-186">Dit vindt een automatische back-up.</span><span class="sxs-lookup"><span data-stu-id="97678-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="97678-187">[Herstellen] [ Restore] van uw meest recente momentopname.</span><span class="sxs-lookup"><span data-stu-id="97678-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="97678-188">Verwijder het bestaande datawarehouse op een standard-opslag.</span><span class="sxs-lookup"><span data-stu-id="97678-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="97678-189">**Als u niet in deze stap doet, wordt in rekening gebracht voor beide datawarehouses.**</span><span class="sxs-lookup"><span data-stu-id="97678-189">**If you fail to do this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="97678-190">De volgende instellingen uitvoeren als onderdeel van de migratie niet via:</span><span class="sxs-lookup"><span data-stu-id="97678-190">The following settings do not carry over as part of the migration:</span></span>
>
> * <span data-ttu-id="97678-191">Controle op het databaseniveau van de moet opnieuw worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="97678-191">Auditing at the database level needs to be re-enabled.</span></span>
> * <span data-ttu-id="97678-192">Firewall-regels op het databaseniveau van de moeten opnieuw worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="97678-192">Firewall rules at the database level need to be re-added.</span></span> <span data-ttu-id="97678-193">Firewallregels op serverniveau worden niet getroffen.</span><span class="sxs-lookup"><span data-stu-id="97678-193">Firewall rules at the server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="97678-194">Wijzig de naam van datawarehouse tijdens de migratie (optioneel)</span><span class="sxs-lookup"><span data-stu-id="97678-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="97678-195">Twee databases op dezelfde logische server kunnen niet dezelfde naam hebben.</span><span class="sxs-lookup"><span data-stu-id="97678-195">Two databases on the same logical server cannot have the same name.</span></span> <span data-ttu-id="97678-196">SQL Data Warehouse ondersteunt nu de mogelijkheid om te wijzigen van een datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="97678-196">SQL Data Warehouse now supports the ability to rename a data warehouse.</span></span>

<span data-ttu-id="97678-197">Stel in dit voorbeeld of uw bestaande datawarehouse op een standard-opslag is momenteel met de naam 'MyDW'.</span><span class="sxs-lookup"><span data-stu-id="97678-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="97678-198">Wijzig de naam 'MyDW' met behulp van de volgende opdracht ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="97678-198">Rename "MyDW" by using the following ALTER DATABASE command.</span></span> <span data-ttu-id="97678-199">(In dit voorbeeld we je Wijzig de naam 'MyDW_BeforeMigration'.)  Deze opdracht alle bestaande transacties wordt gestopt en moet worden uitgevoerd in de database master kan slagen.</span><span class="sxs-lookup"><span data-stu-id="97678-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in the master database to succeed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="97678-200">[Onderbreken] [ Pause] 'MyDW_BeforeMigration'.</span><span class="sxs-lookup"><span data-stu-id="97678-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="97678-201">Dit vindt een automatische back-up.</span><span class="sxs-lookup"><span data-stu-id="97678-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="97678-202">[Herstellen] [ Restore] van de meest recente momentopname maken van een nieuwe database met de naam die wordt gebruikt om te worden (bijvoorbeeld 'MyDW').</span><span class="sxs-lookup"><span data-stu-id="97678-202">[Restore][Restore] from your most recent snapshot a new database with the name it used to be (for example, "MyDW").</span></span>
4. <span data-ttu-id="97678-203">Verwijderen van 'MyDW_BeforeMigration'.</span><span class="sxs-lookup"><span data-stu-id="97678-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="97678-204">**Als u niet in deze stap doet, wordt in rekening gebracht voor beide datawarehouses.**</span><span class="sxs-lookup"><span data-stu-id="97678-204">**If you fail to do this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="97678-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="97678-205">Next steps</span></span>
<span data-ttu-id="97678-206">Met het wijzigen naar premium-opslag hebt u ook een toenemend aantal blob-databasebestanden in de onderliggende architectuur van uw datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="97678-206">With the change to premium storage, you also have an increased number of database blob files in the underlying architecture of your data warehouse.</span></span> <span data-ttu-id="97678-207">Om de prestatievoordelen maximaliseren van deze wijziging, kunt u uw geclusterde columnstore-indexen met behulp van het volgende script opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="97678-207">To maximize the performance benefits of this change, rebuild your clustered columnstore indexes by using the following script.</span></span> <span data-ttu-id="97678-208">Het script werkt door af te dwingen een deel van uw bestaande gegevens voor de aanvullende blobs.</span><span class="sxs-lookup"><span data-stu-id="97678-208">The script works by forcing some of your existing data to the additional blobs.</span></span> <span data-ttu-id="97678-209">Als u geen actie onderneemt, wordt de gegevens natuurlijk na verloop van tijd distribueren, als u meer gegevens in de tabellen laden.</span><span class="sxs-lookup"><span data-stu-id="97678-209">If you take no action, the data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="97678-210">**Vereisten:**</span><span class="sxs-lookup"><span data-stu-id="97678-210">**Prerequisites:**</span></span>

- <span data-ttu-id="97678-211">Het datawarehouse moet worden uitgevoerd met 1000 datawarehouse eenheden of hoger (Zie [scale rekenkracht][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="97678-211">The data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="97678-212">De gebruiker uitvoeren van het script moet in de [mediumrc rol] [ mediumrc role] of hoger.</span><span class="sxs-lookup"><span data-stu-id="97678-212">The user executing the script should be in the [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="97678-213">Een gebruiker toevoegen aan deze rol, uitvoeren van het volgende:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="97678-213">To add a user to this role, execute the following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table to control index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, the below can be re-run to restart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

<span data-ttu-id="97678-214">Als u problemen ondervindt met uw datawarehouse [Maak een ondersteuningsticket] [ create a support ticket] en verwijzing 'migratie naar de premium-opslag' als de mogelijke oorzaak.</span><span class="sxs-lookup"><span data-stu-id="97678-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration to premium storage” as the possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration to Premium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps to rename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
