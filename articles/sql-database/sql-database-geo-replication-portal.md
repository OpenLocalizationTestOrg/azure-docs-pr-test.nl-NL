---
title: 'Azure-portal: SQL-Database geo-replicatie | Microsoft Docs'
description: "Geo-replicatie configureren voor Azure SQL Database in hello Azure-portal en initiëren failover"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a><span data-ttu-id="ed1eb-103">Actieve geo-replicatie configureren voor Azure SQL Database in hello Azure-portal en initiëren failover</span><span class="sxs-lookup"><span data-stu-id="ed1eb-103">Configure active geo-replication for Azure SQL Database in hello Azure portal and initiate failover</span></span>

<span data-ttu-id="ed1eb-104">Dit artikel ziet u hoe tooconfigure actieve geo-replicatie voor SQL-Database in Hallo [Azure-portal](http://portal.azure.com) en tooinitiate failover.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-104">This article shows you how tooconfigure active geo-replication for SQL Database in hello [Azure portal](http://portal.azure.com) and tooinitiate failover.</span></span>

<span data-ttu-id="ed1eb-105">tooinitiate failover Hello Azure-portal, Zie [initiëren van een geplande of niet-geplande failover voor Azure SQL Database met hello Azure-portal](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ed1eb-105">tooinitiate failover with hello Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with hello Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="ed1eb-106">tooconfigure actieve geo-replicatie met behulp van hello Azure-portal, moet u Hallo resource te volgen:</span><span class="sxs-lookup"><span data-stu-id="ed1eb-106">tooconfigure active geo-replication by using hello Azure portal, you need hello following resource:</span></span>

* <span data-ttu-id="ed1eb-107">Een Azure SQL database: Hallo primaire database die u wilt dat tooreplicate tooa verschillende geografische regio.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-107">An Azure SQL database: hello primary database that you want tooreplicate tooa different geographical region.</span></span>

> [!Note]
<span data-ttu-id="ed1eb-108">Actieve geo-replicatie moet liggen tussen databases in Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-108">Active geo-replication must be between databases in hello same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="ed1eb-109">Toevoegen van een secundaire database</span><span class="sxs-lookup"><span data-stu-id="ed1eb-109">Add a secondary database</span></span>
<span data-ttu-id="ed1eb-110">Hallo volgende stappen een nieuwe secundaire database maken in een associatie geo-replicatie.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-110">hello following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="ed1eb-111">tooadd een secundaire database, moet u de eigenaar van de Hallo-abonnement of mede-eigenaar.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-111">tooadd a secondary database, you must be hello subscription owner or co-owner.</span></span>

<span data-ttu-id="ed1eb-112">Hallo secundaire database heeft dezelfde naam als de primaire database Hallo Hallo en Hallo heeft, standaard hetzelfde serviceniveau.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-112">hello secondary database has hello same name as hello primary database and has, by default, hello same service level.</span></span> <span data-ttu-id="ed1eb-113">Hallo secundaire database is een individuele database of een database in een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-113">hello secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="ed1eb-114">Zie voor meer informatie [Servicelagen](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="ed1eb-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="ed1eb-115">Nadat Hallo secundaire is gemaakt en wordt gemaakt, begint de gegevens van Hallo primaire database toohello nieuwe secundaire database te repliceren.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-115">After hello secondary is created and seeded, data begins replicating from hello primary database toohello new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="ed1eb-116">Als er al Hallo partner-database bestaat (bijvoorbeeld als gevolg van een vorige geo-replicatie relatie beëindigd) mislukt Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-116">If hello partner database already exists (for example, as a result of terminating a previous geo-replication relationship) hello command fails.</span></span>
> 

1. <span data-ttu-id="ed1eb-117">In Hallo [Azure-portal](http://portal.azure.com), toohello database die u tooset voor geo-replicatie wilt bladeren.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-117">In hello [Azure portal](http://portal.azure.com), browse toohello database that you want tooset up for geo-replication.</span></span>
2. <span data-ttu-id="ed1eb-118">Selecteer op de pagina van het Hallo SQL database **geo-replicatie**, en selecteer vervolgens Hallo regio toocreate Hallo secundaire database.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-118">On hello SQL database page, select **geo-replication**, and then select hello region toocreate hello secondary database.</span></span> <span data-ttu-id="ed1eb-119">U kunt een andere regio dan Hallo regio die als host fungeert voor de primaire database Hallo selecteren, maar we raden Hallo [gekoppelde regio](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="ed1eb-119">You can select any region other than hello region hosting hello primary database, but we recommend hello [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Geo-replicatie configureren](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="ed1eb-121">Selecteer of Hallo-server en prijscategorie voor de secundaire database Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-121">Select or configure hello server and pricing tier for hello secondary database.</span></span>
   
    ![Secundaire configureren](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="ed1eb-123">U kunt desgewenst een secundaire database tooan elastische groep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-123">Optionally, you can add a secondary database tooan elastic pool.</span></span> <span data-ttu-id="ed1eb-124">toocreate hello secundaire database in een groep, klikt u op **elastische pool** en selecteer een groep op de doelserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-124">toocreate hello secondary database in a pool, click **elastic pool** and select a pool on hello target server.</span></span> <span data-ttu-id="ed1eb-125">Een groep moet al bestaan op de doelserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-125">A pool must already exist on hello target server.</span></span> <span data-ttu-id="ed1eb-126">Deze werkstroom wordt niet gemaakt voor een groep.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="ed1eb-127">Klik op **maken** tooadd Hallo secundaire.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-127">Click **Create** tooadd hello secondary.</span></span>
6. <span data-ttu-id="ed1eb-128">Hallo secundaire database wordt gemaakt en Hallo seeding proces wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-128">hello secondary database is created and hello seeding process begins.</span></span>
   
    ![Secundaire configureren](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="ed1eb-130">Wanneer Hallo seeding van proces voltooid is, weergegeven Hallo secundaire database de status ervan.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-130">When hello seeding process is complete, hello secondary database displays its status.</span></span>
   
    ![Seeding voltooid](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="ed1eb-132">Initieer een failover</span><span class="sxs-lookup"><span data-stu-id="ed1eb-132">Initiate a failover</span></span>

<span data-ttu-id="ed1eb-133">Hallo secundaire database kan worden uitgeschakeld toobecome Hallo primaire.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-133">hello secondary database can be switched toobecome hello primary.</span></span>  

1. <span data-ttu-id="ed1eb-134">In Hallo [Azure-portal](http://portal.azure.com), primaire database toohello Hallo geo-replicatie samen te bladeren.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-134">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="ed1eb-135">Selecteer op de blade SQL-Database Hallo **alle instellingen** > **geo-replicatie**.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-135">On hello SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="ed1eb-136">In Hallo **SECUNDAIREN** lijst, selecteer Hallo database gewenste toobecome Hallo nieuwe primaire en klik op **Failover**.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-136">In hello **SECONDARIES** list, select hello database you want toobecome hello new primary and click **Failover**.</span></span>
   
    ![failover](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="ed1eb-138">Klik op **Ja** toobegin Hallo failover.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-138">Click **Yes** toobegin hello failover.</span></span>

<span data-ttu-id="ed1eb-139">Hallo opdracht switches onmiddellijk Hallo secundaire database aan Hallo primaire rol.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-139">hello command immediately switches hello secondary database into hello primary role.</span></span> 

<span data-ttu-id="ed1eb-140">Er is een korte periode gedurende welke beide databases niet beschikbaar (in volgorde van de Hallo van 0 too25 seconden zijn) tijdens het Hallo-rollen worden omgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-140">There is a short period during which both databases are unavailable (on hello order of 0 too25 seconds) while hello roles are switched.</span></span> <span data-ttu-id="ed1eb-141">Als de primaire database Hallo meerdere secundaire databases, Hallo opdracht automatisch heeft Hallo configureren andere secundaire replica's tooconnect toohello nieuwe primaire.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-141">If hello primary database has multiple secondary databases, hello command automatically reconfigures hello other secondaries tooconnect toohello new primary.</span></span> <span data-ttu-id="ed1eb-142">Hallo hele bewerking duurt minder dan een minuut toocomplete onder normale omstandigheden.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-142">hello entire operation should take less than a minute toocomplete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="ed1eb-143">Met deze opdracht is ontworpen voor snel herstel van database Hallo bij een stroomstoring.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-143">This command is designed for quick recovery of hello database in case of an outage.</span></span> <span data-ttu-id="ed1eb-144">Dit activeert failover zonder gegevenssynchronisatie (gedwongen failover).</span><span class="sxs-lookup"><span data-stu-id="ed1eb-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="ed1eb-145">Als de primaire Hallo online is en het doorvoeren van transacties wanneer Hallo-opdracht wordt gegeven gegevensverlies optreden.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-145">If hello primary is online and committing transactions when hello command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="ed1eb-146">Secundaire database verwijderen</span><span class="sxs-lookup"><span data-stu-id="ed1eb-146">Remove secondary database</span></span>
<span data-ttu-id="ed1eb-147">Deze bewerking permanent Hallo toohello secundaire replicatiedatabase wordt beëindigd en wijzigingen Hallo rol van Hallo secundaire tooa normale alleen-lezen database.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-147">This operation permanently terminates hello replication toohello secondary database, and changes hello role of hello secondary tooa regular read-write database.</span></span> <span data-ttu-id="ed1eb-148">Als Hallo connectiviteit toohello secundaire database verbroken is, Hallo-opdracht is geslaagd, maar Hallo secundaire biedt niet lezen-schrijven pas nadat de verbinding is hersteld.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-148">If hello connectivity toohello secondary database is broken, hello command succeeds but hello secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="ed1eb-149">In Hallo [Azure-portal](http://portal.azure.com), primaire database toohello Hallo geo-replicatie samen te bladeren.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-149">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="ed1eb-150">Selecteer op de pagina van het Hallo SQL database **geo-replicatie**.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-150">On hello SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="ed1eb-151">In Hallo **SECUNDAIREN** lijst, de gewenste tooremove van Hallo geo-replicatie samenwerking Selecteer Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-151">In hello **SECONDARIES** list, select hello database you want tooremove from hello geo-replication partnership.</span></span>
4. <span data-ttu-id="ed1eb-152">Klik op **Stop replicatie al**.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-152">Click **Stop Replication**.</span></span>
   
    ![Secundaire verwijderen](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="ed1eb-154">Er wordt een bevestigingsvenster geopend.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-154">A confirmation window opens.</span></span> <span data-ttu-id="ed1eb-155">Klik op **Ja** tooremove Hallo-database van Hallo geo-replicatie samenwerking.</span><span class="sxs-lookup"><span data-stu-id="ed1eb-155">Click **Yes** tooremove hello database from hello geo-replication partnership.</span></span> <span data-ttu-id="ed1eb-156">(Deze instellen tooa alleen-lezen database geen deel uit van replicatie.)</span><span class="sxs-lookup"><span data-stu-id="ed1eb-156">(Set it tooa read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed1eb-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ed1eb-157">Next steps</span></span>
* <span data-ttu-id="ed1eb-158">toolearn meer informatie over actieve geo-replicatie, Zie [actieve geo-replicatie](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed1eb-158">toolearn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="ed1eb-159">Zie voor een overzicht van zakelijke continuïteit en scenario's [Business continuity overview](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="ed1eb-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

