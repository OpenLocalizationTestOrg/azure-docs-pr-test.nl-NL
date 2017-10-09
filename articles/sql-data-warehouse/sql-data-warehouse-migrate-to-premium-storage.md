---
title: aaaMigrate uw bestaande Azure-opslag toopremium datawarehouse | Microsoft Docs
description: Instructies voor het migreren van een bestaande datawarehouse toopremium gegevensopslag
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
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a><span data-ttu-id="ac2c4-103">Uw datawarehouse toopremium opslag migreren</span><span class="sxs-lookup"><span data-stu-id="ac2c4-103">Migrate your data warehouse toopremium storage</span></span>
<span data-ttu-id="ac2c4-104">Azure SQL Data Warehouse onlangs geïntroduceerd [premium-opslag voor groter prestaties, voorspelbaarheid][premium storage for greater performance predictability].</span><span class="sxs-lookup"><span data-stu-id="ac2c4-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="ac2c4-105">Bestaande gegevens worden in datawarehouses die momenteel in de standard-opslag kunnen worden gemigreerd toopremium opslag.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-105">Existing data warehouses currently on standard storage can now be migrated toopremium storage.</span></span> <span data-ttu-id="ac2c4-106">U kunt profiteren van de automatische migratie van of als u liever toocontrol wanneer toomigrate (waarbij uitval), kunt u doen Hallo migratie zelf.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-106">You can take advantage of automatic migration, or if you prefer toocontrol when toomigrate (which does involve some downtime), you can do hello migration yourself.</span></span>

<span data-ttu-id="ac2c4-107">Als u meer dan een datawarehouse hebt, gebruikt u Hallo [schema voor automatische migratie] [ automatic migration schedule] toodetermine wanneer deze ook worden gemigreerd.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-107">If you have more than one data warehouse, use hello [automatic migration schedule][automatic migration schedule] toodetermine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="ac2c4-108">Opslagtype bepalen</span><span class="sxs-lookup"><span data-stu-id="ac2c4-108">Determine storage type</span></span>
<span data-ttu-id="ac2c4-109">Als u een datawarehouse voordat Hallo datums na hebt gemaakt, gebruikt u momenteel standard-opslag.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-109">If you created a data warehouse before hello following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="ac2c4-110">**Regio**</span><span class="sxs-lookup"><span data-stu-id="ac2c4-110">**Region**</span></span> | <span data-ttu-id="ac2c4-111">**Datawarehouse gemaakt voor deze datum**</span><span class="sxs-lookup"><span data-stu-id="ac2c4-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="ac2c4-112">Australië - oost</span><span class="sxs-lookup"><span data-stu-id="ac2c4-112">Australia East</span></span> |<span data-ttu-id="ac2c4-113">Premium-opslag is nog niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="ac2c4-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="ac2c4-114">China - oost</span><span class="sxs-lookup"><span data-stu-id="ac2c4-114">China East</span></span> |<span data-ttu-id="ac2c4-115">1 november 2016</span><span class="sxs-lookup"><span data-stu-id="ac2c4-115">November 1, 2016</span></span> |
| <span data-ttu-id="ac2c4-116">China - noord</span><span class="sxs-lookup"><span data-stu-id="ac2c4-116">China North</span></span> |<span data-ttu-id="ac2c4-117">1 november 2016</span><span class="sxs-lookup"><span data-stu-id="ac2c4-117">November 1, 2016</span></span> |
| <span data-ttu-id="ac2c4-118">Duitsland - centraal</span><span class="sxs-lookup"><span data-stu-id="ac2c4-118">Germany Central</span></span> |<span data-ttu-id="ac2c4-119">1 november 2016</span><span class="sxs-lookup"><span data-stu-id="ac2c4-119">November 1, 2016</span></span> |
| <span data-ttu-id="ac2c4-120">Duitsland - noordoost</span><span class="sxs-lookup"><span data-stu-id="ac2c4-120">Germany Northeast</span></span> |<span data-ttu-id="ac2c4-121">1 november 2016</span><span class="sxs-lookup"><span data-stu-id="ac2c4-121">November 1, 2016</span></span> |
| <span data-ttu-id="ac2c4-122">India - west</span><span class="sxs-lookup"><span data-stu-id="ac2c4-122">India West</span></span> |<span data-ttu-id="ac2c4-123">Premium-opslag is nog niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="ac2c4-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="ac2c4-124">Japan - west</span><span class="sxs-lookup"><span data-stu-id="ac2c4-124">Japan West</span></span> |<span data-ttu-id="ac2c4-125">Premium-opslag is nog niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="ac2c4-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="ac2c4-126">Noord-centraal VS</span><span class="sxs-lookup"><span data-stu-id="ac2c4-126">North Central US</span></span> |<span data-ttu-id="ac2c4-127">10 november 2016</span><span class="sxs-lookup"><span data-stu-id="ac2c4-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="ac2c4-128">Details van de automatische migratie</span><span class="sxs-lookup"><span data-stu-id="ac2c4-128">Automatic migration details</span></span>
<span data-ttu-id="ac2c4-129">Standaard gaan we uw database voor u tussen 18:00 uur en 6:00 uur in uw regio lokale tijd tijdens Hallo [schema voor automatische migratie][automatic migration schedule].</span><span class="sxs-lookup"><span data-stu-id="ac2c4-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during hello [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="ac2c4-130">Uw bestaande datawarehouse kan niet worden gebruikt tijdens de migratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-130">Your existing data warehouse will be unusable during hello migration.</span></span> <span data-ttu-id="ac2c4-131">Hallo migratie duurt ongeveer één uur per terabyte van opslag per datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-131">hello migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="ac2c4-132">U wordt niet in rekening gebracht tijdens een gedeelte van de automatische Hallo-migratie.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-132">You will not be charged during any portion of hello automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="ac2c4-133">Wanneer Hallo migratie voltooid is, wordt uw datawarehouse zich weer online is en kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-133">When hello migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="ac2c4-134">Microsoft neemt Hallo stappen toocomplete Hallo migratie (deze hoeven niet alle betrokkenheid van uw kant) te volgen.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-134">Microsoft is taking hello following steps toocomplete hello migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="ac2c4-135">Stel in dit voorbeeld of uw bestaande datawarehouse op een standard-opslag is momenteel met de naam 'MyDW'.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="ac2c4-136">Microsoft wijzigt de naam 'MyDW' te 'MyDW_DO_NOT_USE_ [tijdstempel]'.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-136">Microsoft renames “MyDW” too“MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="ac2c4-137">Microsoft pauzeert 'MyDW_DO_NOT_USE_ [tijdstempel]'.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="ac2c4-138">Gedurende deze tijd is een back-up gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-138">During this time, a backup is taken.</span></span> <span data-ttu-id="ac2c4-139">Mogelijk ziet u meerdere onderbroken en hervat als er problemen ondervindt tijdens dit proces.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="ac2c4-140">Microsoft maakt een nieuw datawarehouse met de naam 'MyDW' op premium-opslag vanuit Hallo back-up gemaakt in stap 2.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from hello backup taken in step 2.</span></span> <span data-ttu-id="ac2c4-141">'MyDW' worden niet weergegeven tot nadat Hallo herstellen voltooid is.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-141">“MyDW” will not appear until after hello restore is complete.</span></span>
4. <span data-ttu-id="ac2c4-142">Nadat het Hallo herstellen is voltooid 'MyDW' toohello dezelfde gegevens datawarehouse-eenheden en -status geretourneerd (onderbroken of actieve) die deze was voordat Hallo-migratie.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-142">After hello restore is complete, “MyDW” returns toohello same data warehouse units and state (paused or active) that it was before hello migration.</span></span>
5. <span data-ttu-id="ac2c4-143">Nadat Hallo migratie voltooid is, verwijdert Microsoft 'MyDW_DO_NOT_USE_ [tijdstempel]'.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-143">After hello migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="ac2c4-144">Hallo uitvoeren volgende instellingen niet via als onderdeel van Hallo migratie:</span><span class="sxs-lookup"><span data-stu-id="ac2c4-144">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="ac2c4-145">Controle op databaseniveau Hallo moet toobe weer wordt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-145">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="ac2c4-146">Firewallregels op databaseniveau Hallo moeten toobe opnieuw toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-146">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="ac2c4-147">Firewallregels op serverniveau Hallo worden niet getroffen.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-147">Firewall rules at hello server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="ac2c4-148">Planning voor automatische migratie</span><span class="sxs-lookup"><span data-stu-id="ac2c4-148">Automatic migration schedule</span></span>
<span data-ttu-id="ac2c4-149">Automatische migraties optreden tussen 18:00 uur en 6:00 uur (lokale tijd per regio) tijdens het Hallo onderbreking schema te volgen.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during hello following outage schedule.</span></span>

| <span data-ttu-id="ac2c4-150">**Regio**</span><span class="sxs-lookup"><span data-stu-id="ac2c4-150">**Region**</span></span> | <span data-ttu-id="ac2c4-151">**Geschatte begindatum**</span><span class="sxs-lookup"><span data-stu-id="ac2c4-151">**Estimated start date**</span></span> | <span data-ttu-id="ac2c4-152">**Geschatte einddatum**</span><span class="sxs-lookup"><span data-stu-id="ac2c4-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ac2c4-153">Australië - oost</span><span class="sxs-lookup"><span data-stu-id="ac2c4-153">Australia East</span></span> |<span data-ttu-id="ac2c4-154">Nog niet worden vastgesteld</span><span class="sxs-lookup"><span data-stu-id="ac2c4-154">Not determined yet</span></span> |<span data-ttu-id="ac2c4-155">Nog niet worden vastgesteld</span><span class="sxs-lookup"><span data-stu-id="ac2c4-155">Not determined yet</span></span> |
| <span data-ttu-id="ac2c4-156">China - oost</span><span class="sxs-lookup"><span data-stu-id="ac2c4-156">China East</span></span> |<span data-ttu-id="ac2c4-157">9 januari 2017</span><span class="sxs-lookup"><span data-stu-id="ac2c4-157">January 9, 2017</span></span> |<span data-ttu-id="ac2c4-158">13 januari 2017</span><span class="sxs-lookup"><span data-stu-id="ac2c4-158">January 13, 2017</span></span> |
| <span data-ttu-id="ac2c4-159">China - noord</span><span class="sxs-lookup"><span data-stu-id="ac2c4-159">China North</span></span> |<span data-ttu-id="ac2c4-160">9 januari 2017</span><span class="sxs-lookup"><span data-stu-id="ac2c4-160">January 9, 2017</span></span> |<span data-ttu-id="ac2c4-161">13 januari 2017</span><span class="sxs-lookup"><span data-stu-id="ac2c4-161">January 13, 2017</span></span> |
| <span data-ttu-id="ac2c4-162">Duitsland - centraal</span><span class="sxs-lookup"><span data-stu-id="ac2c4-162">Germany Central</span></span> |<span data-ttu-id="ac2c4-163">9 januari 2017</span><span class="sxs-lookup"><span data-stu-id="ac2c4-163">January 9, 2017</span></span> |<span data-ttu-id="ac2c4-164">13 januari 2017</span><span class="sxs-lookup"><span data-stu-id="ac2c4-164">January 13, 2017</span></span> |
| <span data-ttu-id="ac2c4-165">Duitsland - noordoost</span><span class="sxs-lookup"><span data-stu-id="ac2c4-165">Germany Northeast</span></span> |<span data-ttu-id="ac2c4-166">9 januari 2017</span><span class="sxs-lookup"><span data-stu-id="ac2c4-166">January 9, 2017</span></span> |<span data-ttu-id="ac2c4-167">13 januari 2017</span><span class="sxs-lookup"><span data-stu-id="ac2c4-167">January 13, 2017</span></span> |
| <span data-ttu-id="ac2c4-168">India - west</span><span class="sxs-lookup"><span data-stu-id="ac2c4-168">India West</span></span> |<span data-ttu-id="ac2c4-169">Nog niet worden vastgesteld</span><span class="sxs-lookup"><span data-stu-id="ac2c4-169">Not determined yet</span></span> |<span data-ttu-id="ac2c4-170">Nog niet worden vastgesteld</span><span class="sxs-lookup"><span data-stu-id="ac2c4-170">Not determined yet</span></span> |
| <span data-ttu-id="ac2c4-171">Japan - west</span><span class="sxs-lookup"><span data-stu-id="ac2c4-171">Japan West</span></span> |<span data-ttu-id="ac2c4-172">Nog niet worden vastgesteld</span><span class="sxs-lookup"><span data-stu-id="ac2c4-172">Not determined yet</span></span> |<span data-ttu-id="ac2c4-173">Nog niet worden vastgesteld</span><span class="sxs-lookup"><span data-stu-id="ac2c4-173">Not determined yet</span></span> |
| <span data-ttu-id="ac2c4-174">Noord-centraal VS</span><span class="sxs-lookup"><span data-stu-id="ac2c4-174">North Central US</span></span> |<span data-ttu-id="ac2c4-175">9 januari 2017</span><span class="sxs-lookup"><span data-stu-id="ac2c4-175">January 9, 2017</span></span> |<span data-ttu-id="ac2c4-176">13 januari 2017</span><span class="sxs-lookup"><span data-stu-id="ac2c4-176">January 13, 2017</span></span> |

## <a name="self-migration-toopremium-storage"></a><span data-ttu-id="ac2c4-177">Zelfstandige migratie toopremium opslag</span><span class="sxs-lookup"><span data-stu-id="ac2c4-177">Self-migration toopremium storage</span></span>
<span data-ttu-id="ac2c4-178">Als u toocontrol wilt wanneer uw uitvaltijd wordt uitgevoerd, kunt u Hallo stappen toomigrate een bestaand datawarehouse op standaardopslag toopremium opslag te volgen.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-178">If you want toocontrol when your downtime will occur, you can use hello following steps toomigrate an existing data warehouse on standard storage toopremium storage.</span></span> <span data-ttu-id="ac2c4-179">Als u deze optie kiest, moet u Hallo zelf migratie voltooien voordat Hallo automatische migratie in deze regio begint.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-179">If you choose this option, you must complete hello self-migration before hello automatic migration begins in that region.</span></span> <span data-ttu-id="ac2c4-180">Dit zorgt ervoor dat u het risico van Hallo automatische migratie een conflict veroorzaken vermijden (Raadpleeg toohello [schema voor automatische migratie][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="ac2c4-180">This ensures that you avoid any risk of hello automatic migration causing a conflict (refer toohello [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="ac2c4-181">Zelfstandige migratie-instructies</span><span class="sxs-lookup"><span data-stu-id="ac2c4-181">Self-migration instructions</span></span>
<span data-ttu-id="ac2c4-182">toomigrate uw gegevens datawarehouse zelf, gebruikt u Hallo back-up en herstellen van functies.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-182">toomigrate your data warehouse yourself, use hello backup and restore features.</span></span> <span data-ttu-id="ac2c4-183">Hallo terugzetten gedeelte van de migratie Hallo is verwachte tootake ongeveer één uur per terabyte van opslag per datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-183">hello restore portion of hello migration is expected tootake around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="ac2c4-184">Als u wilt dat tookeep Hallo dezelfde naam nadat de migratie is voltooid, voert u de Hallo [stappen toorename tijdens de migratie][steps toorename during migration].</span><span class="sxs-lookup"><span data-stu-id="ac2c4-184">If you want tookeep hello same name after migration is complete, follow hello [steps toorename during migration][steps toorename during migration].</span></span>

1. <span data-ttu-id="ac2c4-185">[Onderbreken] [ Pause] uw datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="ac2c4-186">Dit vindt een automatische back-up.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="ac2c4-187">[Herstellen] [ Restore] van uw meest recente momentopname.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="ac2c4-188">Verwijder het bestaande datawarehouse op een standard-opslag.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="ac2c4-189">**Als u niet in deze stap toodo, wordt in rekening gebracht voor beide datawarehouses.**</span><span class="sxs-lookup"><span data-stu-id="ac2c4-189">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="ac2c4-190">Hallo uitvoeren volgende instellingen niet via als onderdeel van Hallo migratie:</span><span class="sxs-lookup"><span data-stu-id="ac2c4-190">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="ac2c4-191">Controle op databaseniveau Hallo moet toobe weer wordt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-191">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="ac2c4-192">Firewallregels op databaseniveau Hallo moeten toobe opnieuw toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-192">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="ac2c4-193">Firewallregels op serverniveau Hallo worden niet getroffen.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-193">Firewall rules at hello server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="ac2c4-194">Wijzig de naam van datawarehouse tijdens de migratie (optioneel)</span><span class="sxs-lookup"><span data-stu-id="ac2c4-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="ac2c4-195">Twee databases op dezelfde logische server kan geen Hallo Hallo dezelfde naam.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-195">Two databases on hello same logical server cannot have hello same name.</span></span> <span data-ttu-id="ac2c4-196">SQL Data Warehouse ondersteunt nu Hallo mogelijkheid toorename een datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-196">SQL Data Warehouse now supports hello ability toorename a data warehouse.</span></span>

<span data-ttu-id="ac2c4-197">Stel in dit voorbeeld of uw bestaande datawarehouse op een standard-opslag is momenteel met de naam 'MyDW'.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="ac2c4-198">Wijzig de naam 'MyDW' met behulp van Hallo na de opdracht ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-198">Rename "MyDW" by using hello following ALTER DATABASE command.</span></span> <span data-ttu-id="ac2c4-199">(In dit voorbeeld we je Wijzig de naam 'MyDW_BeforeMigration'.)  Deze opdracht alle bestaande transacties wordt gestopt en moet worden uitgevoerd in Hallo hoofddatabase toosucceed.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in hello master database toosucceed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="ac2c4-200">[Onderbreken] [ Pause] 'MyDW_BeforeMigration'.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="ac2c4-201">Dit vindt een automatische back-up.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="ac2c4-202">[Herstellen] [ Restore] van uw meest recente momentopname van een nieuwe database met naam Hallo deze toobe (bijvoorbeeld ' MyDW') gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-202">[Restore][Restore] from your most recent snapshot a new database with hello name it used toobe (for example, "MyDW").</span></span>
4. <span data-ttu-id="ac2c4-203">Verwijderen van 'MyDW_BeforeMigration'.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="ac2c4-204">**Als u niet in deze stap toodo, wordt in rekening gebracht voor beide datawarehouses.**</span><span class="sxs-lookup"><span data-stu-id="ac2c4-204">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="ac2c4-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ac2c4-205">Next steps</span></span>
<span data-ttu-id="ac2c4-206">Hello toopremium opslag wijzigen, moet u ook een toenemend aantal blob-databasebestanden in Hallo onderliggende architectuur van uw datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-206">With hello change toopremium storage, you also have an increased number of database blob files in hello underlying architecture of your data warehouse.</span></span> <span data-ttu-id="ac2c4-207">toomaximize hello prestatievoordelen van deze wijziging opnieuw maken van uw geclusterde columnstore-indexen met behulp van Hallo script volgen.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-207">toomaximize hello performance benefits of this change, rebuild your clustered columnstore indexes by using hello following script.</span></span> <span data-ttu-id="ac2c4-208">Hallo script werkt door af te dwingen enkele van uw bestaande gegevens toohello extra blobs.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-208">hello script works by forcing some of your existing data toohello additional blobs.</span></span> <span data-ttu-id="ac2c4-209">Als u geen actie onderneemt, distribueren Hallo gegevens natuurlijk gedurende een bepaalde periode, als u meer gegevens in de tabellen laden.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-209">If you take no action, hello data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="ac2c4-210">**Vereisten:**</span><span class="sxs-lookup"><span data-stu-id="ac2c4-210">**Prerequisites:**</span></span>

- <span data-ttu-id="ac2c4-211">Hallo-datawarehouse moet worden uitgevoerd met 1000 datawarehouse eenheden of hoger (Zie [scale rekenkracht][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="ac2c4-211">hello data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="ac2c4-212">Hallo gebruiker uitvoeren van script Hallo zou in Hallo [mediumrc rol] [ mediumrc role] of hoger.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-212">hello user executing hello script should be in hello [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="ac2c4-213">een gebruikersrol toothis tooadd Hallo volgende uitvoeren:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="ac2c4-213">tooadd a user toothis role, execute hello following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
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
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
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

<span data-ttu-id="ac2c4-214">Als u problemen ondervindt met uw datawarehouse [Maak een ondersteuningsticket] [ create a support ticket] en verwijzen naar 'migratie toopremium opslag' als Hallo mogelijke oorzaak.</span><span class="sxs-lookup"><span data-stu-id="ac2c4-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration toopremium storage” as hello possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
