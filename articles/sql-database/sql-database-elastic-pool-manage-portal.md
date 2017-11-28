---
title: 'Azure-portal: maken en beheren van een elastische pool SQL Database | Microsoft Docs'
description: Ontdek hoe toouse hello Azure-portal en SQL-Database ingebouwde intelligentie toomanage, bewaken en de prestaties van een schaalbare elastische pool toooptimize-database het juiste formaat en kosten beheren.
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a><span data-ttu-id="1e7b1-103">Maken en beheren van een elastische groep met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="1e7b1-103">Create and manage an elastic pool with hello Azure portal</span></span>
<span data-ttu-id="1e7b1-104">Dit onderwerp leest u hoe toocreate en beheren van schaalbare [elastische pools](sql-database-elastic-pool.md) Hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with hello Azure portal.</span></span> <span data-ttu-id="1e7b1-105">U kunt ook maken en beheren van een Azure elastische groep met [PowerShell](sql-database-elastic-pool-manage-powershell.md), Hallo REST-API of [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="1e7b1-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="1e7b1-106">U kunt ook maken en databases verplaatsen naar en van elastische pools met [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="1e7b1-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="1e7b1-107">Elastische pool maken</span><span class="sxs-lookup"><span data-stu-id="1e7b1-107">Create an elastic pool</span></span> 

<span data-ttu-id="1e7b1-108">Er zijn twee manieren kunt u een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="1e7b1-109">U kunt dit doen vanaf het begin als u Hallo groep instellingen u wilt weet, of met een aanbeveling van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-109">You can do it from scratch if you know hello pool setup you want, or start with a recommendation from hello service.</span></span> <span data-ttu-id="1e7b1-110">SQL-Database beschikt over ingebouwde intelligentie die raadt aan om een elastische groep is ingesteld als het kostenefficiënte op basis van Hallo voorbij gebruik telemetrie van uw databases.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on hello past usage telemetry for your databases.</span></span>

<span data-ttu-id="1e7b1-111">U kunt meerdere groepen maken op een server, maar u kunt geen databases van verschillende servers toevoegen in Hallo dezelfde groep.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-111">You can create multiple pools on a server, but you can't add databases from different servers into hello same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="1e7b1-112">Elastische pools zijn algemeen beschikbaar in alle Azure-regio's, behalve in West-India, waar deze zich momenteel in de previewfase bevinden.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="1e7b1-113">Algemene beschikbaarheid van elastische pools in deze regio zal zo snel mogelijk plaatsvinden.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="1e7b1-114">Stap 1: Een elastische pool maken</span><span class="sxs-lookup"><span data-stu-id="1e7b1-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="1e7b1-115">Een elastische pool te maken van een bestaand **server** blade in de portal Hallo Hallo gemakkelijkste manier toomove bestaande databases in een elastische groep is.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-115">Creating an elastic pool from an existing **server** blade in hello portal is hello easiest way toomove existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="1e7b1-116">U kunt ook een elastische pool maken door te zoeken naar **elastische SQL-groep** in Hallo **Marketplace** of klikken op **+ toevoegen** in Hallo **SQL elastische pools**blade bladeren.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-116">You can also create an elastic pool by searching **SQL elastic pool** in hello **Marketplace** or clicking **+Add** in hello **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="1e7b1-117">U zijn kunt toospecify een nieuwe of bestaande server via deze werkstroom van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-117">You are able toospecify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="1e7b1-118">In Hallo [Azure-portal](http://portal.azure.com/), klikt u op **meer services**  **>**  **SQL-servers**, en klik vervolgens op Hallo-server die Hallo bevat databases die u wilt dat tooadd tooan elastische pool.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-118">In hello [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click hello server that contains hello databases you want tooadd tooan elastic pool.</span></span>
2. <span data-ttu-id="1e7b1-119">Klik op **Nieuwe groep**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-119">Click **New pool**.</span></span>

    ![Groep tooa server toevoegen](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="1e7b1-121">**-OF-**</span><span class="sxs-lookup"><span data-stu-id="1e7b1-121">**-OR-**</span></span>

    <span data-ttu-id="1e7b1-122">Mogelijk ziet u een bericht weergegeven dat er aanbevolen elastische pools voor Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-122">You may see a message saying there are recommended elastic pools for hello server.</span></span> <span data-ttu-id="1e7b1-123">Hallo-bericht toosee Hallo aanbevolen pools voor op basis van historische database gebruik telemetrie, klikt u op en klikt u op Hallo laag toosee voor meer informatie en Hallo groep aanpassen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-123">Click hello message toosee hello recommended pools based on historical database usage telemetry, and then click hello tier toosee more details and customize hello pool.</span></span> <span data-ttu-id="1e7b1-124">Zie [aanbevelingen voor Pools begrijpen](#understand-elastic-pool-recommendations) verderop in dit onderwerp voor hoe Hallo aanbeveling wordt gesteld.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how hello recommendation is made.</span></span>

    ![aanbevolen groep](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="1e7b1-126">Hallo **elastische pool** blade wordt weergegeven waarin u Hallo-instellingen opgeven voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-126">hello **elastic pool** blade appears, which is where you specify hello settings for your pool.</span></span> <span data-ttu-id="1e7b1-127">Als u hebt geklikt **nieuwe pool** in de vorige stap Hallo Hallo prijscategorie is **standaard** standaard en geen databases geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-127">If you clicked **New pool** in hello previous step, hello pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="1e7b1-128">U kunt een lege groep maken of een set van bestaande databases van die server toomove in Hallo van toepassingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-128">You can create an empty pool, or specify a set of existing databases from that server toomove into hello pool.</span></span> <span data-ttu-id="1e7b1-129">Als u een aanbevolen pool maakt, Hallo aanbevolen prijscategorie, prestatie-instellingen en lijst met databases vooraf worden ingevuld, maar u kunt ze nog steeds wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-129">If you are creating a recommended pool, hello recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Elastische groep configureren](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="1e7b1-131">Geef een naam voor de elastische groep Hallo of laat het veld als Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-131">Specify a name for hello elastic pool, or leave it as hello default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="1e7b1-132">Stap 2: kies een prijscategorie</span><span class="sxs-lookup"><span data-stu-id="1e7b1-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="1e7b1-133">Hallo bepaalt prijscategorie van pool Hallo functies beschikbaar toohello elastics in Hallo pool en Hallo maximumaantal edtu's (eDTU MAX) en opslag (GB) beschikbare tooeach database.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-133">hello pool's pricing tier determines hello features available toohello elastics in hello pool, and hello maximum number of eDTUs (eDTU MAX), and storage (GBs) available tooeach database.</span></span> <span data-ttu-id="1e7b1-134">Zie voor meer informatie de Servicecategorieën.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="1e7b1-135">toochange hello prijscategorie voor Hallo-groep, klikt u op **prijscategorie**, klikt u op de prijscategorie die u wilt en klik vervolgens op Hallo **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-135">toochange hello pricing tier for hello pool, click **Pricing tier**, click hello pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1e7b1-136">Nadat u Hallo prijscategorie kiezen en uw wijzigingen door te klikken op **OK** in de laatste stap hello, niet meer kunnen toochange Hallo prijscategorie van Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-136">After you choose hello pricing tier and commit your changes by clicking **OK** in hello last step, you won't be able toochange hello pricing tier of hello pool.</span></span> <span data-ttu-id="1e7b1-137">toochange Hallo prijscategorie voor een bestaande elastische pool, een elastische pool maken in de gewenste prijscategorie Hallo en Hallo databases toothis nieuwe toepassingen te migreren.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-137">toochange hello pricing tier for an existing elastic pool, create an elastic pool in hello desired pricing tier and migrate hello databases toothis new pool.</span></span>
>

![Een prijscategorie selecteren](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a><span data-ttu-id="1e7b1-139">Stap 3: Hallo pool configureren</span><span class="sxs-lookup"><span data-stu-id="1e7b1-139">Step 3: Configure hello pool</span></span>

<span data-ttu-id="1e7b1-140">Klik na het instellen van Hallo prijscategorie pool configureren Hier voegt u databases, set groepen met edtu's en opslag (GB adresgroep) en waar u Hallo min en max Edtu voor Hallo elastics instellen in de groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-140">After setting hello pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set hello min and max eDTUs for hello elastics in hello pool.</span></span>

1. <span data-ttu-id="1e7b1-141">Klik op **Groep configureren**</span><span class="sxs-lookup"><span data-stu-id="1e7b1-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="1e7b1-142">Hallo-databases u tooadd toohello toepassingen wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-142">Select hello databases you want tooadd toohello pool.</span></span> <span data-ttu-id="1e7b1-143">Deze stap is optioneel bij het maken van Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-143">This step is optional while creating hello pool.</span></span> <span data-ttu-id="1e7b1-144">Databases kunnen worden toegevoegd nadat Hallo-groep is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-144">Databases can be added after hello pool has been created.</span></span>
    <span data-ttu-id="1e7b1-145">tooadd databases, klik met de **database toevoegen**, klikt u op Hallo databases wilt tooadd en klik vervolgens op Hallo **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-145">tooadd databases, click **Add database**, click hello databases that you want tooadd, and then click hello **Select** button.</span></span>

    ![Databases toevoegen](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="1e7b1-147">Hallo-databases waarmee u samenwerkt hebt voldoende gebruikstelemetrie, Hallo **geschat eDTU- en GB-gebruik** grafiek en Hallo **werkelijk eDTU-gebruik** staafdiagram update toohelp maken van configuratie beslissingen te nemen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-147">If hello databases you're working with have enough historical usage telemetry, hello **Estimated eDTU and GB usage** graph and hello **Actual eDTU usage** bar chart update toohelp you make configuration decisions.</span></span> <span data-ttu-id="1e7b1-148">Bovendien Hallo-service kan bieden u een aanbeveling bericht toohelp u het juiste formaat Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-148">Also, hello service may give you a recommendation message toohelp you right-size hello pool.</span></span> <span data-ttu-id="1e7b1-149">Zie [Dynamische aanbevelingen](#understand-elastic-pool-recommendations).</span><span class="sxs-lookup"><span data-stu-id="1e7b1-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="1e7b1-150">Hallo-opties op Hallo gebruiken **pool configureren** pagina tooexplore instellingen en uw pool te configureren.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-150">Use hello controls on hello **Configure pool** page tooexplore settings and configure your pool.</span></span> <span data-ttu-id="1e7b1-151">Zie [limieten elastische pools](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) voor meer informatie over de limieten van elke servicecategorie en Zie [prijs- en Prestatieoverwegingen voor elastische pools](sql-database-elastic-pool.md) voor gedetailleerde richtlijnen voor het juiste formaat een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="1e7b1-152">Zie voor meer informatie over de groepsinstellingen [eigenschappen van de elastische groep](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="1e7b1-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Elastische groep configureren](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="1e7b1-154">Klik op **Selecteer** in Hallo **Pool configureren** blade na het wijzigen van instellingen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-154">Click **Select** in hello **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="1e7b1-155">Klik op **OK** toocreate Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-155">Click **OK** toocreate hello pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="1e7b1-156">Aanbevelingen voor elastische Pools begrijpen</span><span class="sxs-lookup"><span data-stu-id="1e7b1-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="1e7b1-157">Hallo SQL Database-service beoordeelt de gebruiksgeschiedenis en beveelt een of meer groepen wanneer deze kosteneffectiever zijn dan het gebruik van individuele databases.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-157">hello SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="1e7b1-158">Elke aanbeveling wordt geconfigureerd met een unieke subset van Hallo-server-databases die het meest Hallo van toepassingen geschikt.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-158">Each recommendation is configured with a unique subset of hello server's databases that best fit hello pool.</span></span>

![aanbevolen groep](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="1e7b1-160">Hallo groep aanbeveling omvat:</span><span class="sxs-lookup"><span data-stu-id="1e7b1-160">hello pool recommendation comprises:</span></span>

- <span data-ttu-id="1e7b1-161">Een prijscategorie voor Hallo pool (Basic, Standard, Premium of RS Premium)</span><span class="sxs-lookup"><span data-stu-id="1e7b1-161">A pricing tier for hello pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="1e7b1-162">De juiste **eDTU’s voor de groep** (ook wel Max eDTU's per groep)</span><span class="sxs-lookup"><span data-stu-id="1e7b1-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="1e7b1-163">Hallo **eDTU MAX** en **eDTU Min** per database</span><span class="sxs-lookup"><span data-stu-id="1e7b1-163">hello **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="1e7b1-164">Hallo-lijst met aanbevolen databases voor Hallo van toepassingen</span><span class="sxs-lookup"><span data-stu-id="1e7b1-164">hello list of recommended databases for hello pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1e7b1-165">Hallo service wordt rekening gehouden Hallo afgelopen 30 dagen telemetrie bij het aanbevelen van pools.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-165">hello service takes hello last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="1e7b1-166">Voor een database toobe beschouwd als kandidaat voor een elastische pool, moet er ten minste 7 dagen bestaan.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-166">For a database toobe considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="1e7b1-167">Databases die zich al in een elastische pool bevinden, worden niet aanbevolen voor een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="1e7b1-168">Hallo service beoordeelt resourcebehoeften en kosteneffectiviteit zwevend Hallo één databases in elke servicelaag naar pools van Hallo dezelfde laag.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-168">hello service evaluates resource needs and cost effectiveness of moving hello single databases in each service tier into pools of hello same tier.</span></span> <span data-ttu-id="1e7b1-169">Alle Standard databases op een server worden bijvoorbeeld beoordeeld op hoe ze in een Standard elastische groep passen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="1e7b1-170">Dit betekent dat het Hallo-service maakt geen cross-aanbevelingen zoals het verplaatsen van een Standard database naar een Premium pool.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-170">This means hello service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="1e7b1-171">Na het toevoegen van databases toohello groep worden aanbevelingen dynamisch gegenereerd op basis van historisch gebruik Hallo Hallo-databases die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-171">After adding databases toohello pool, recommendations are dynamically generated based on hello historical usage of hello databases you have selected.</span></span> <span data-ttu-id="1e7b1-172">Deze aanbevelingen worden weergegeven in Hallo eDTU- en GB-gebruiksgrafiek en in een banner boven Hallo Hallo **pool configureren** blade.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-172">These recommendations are shown in hello eDTU and GB usage chart and in a recommendation banner at hello top of hello **Configure pool** blade.</span></span> <span data-ttu-id="1e7b1-173">Deze aanbevelingen zijn bedoeld tooassist u bij het maken van een elastische pool geoptimaliseerd voor uw specifieke databases.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-173">These recommendations are intended tooassist you in creating an elastic pool optimized for your specific databases.</span></span>

![dynamische aanbevelingen](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="1e7b1-175">Beheren en controleren van een elastische pool</span><span class="sxs-lookup"><span data-stu-id="1e7b1-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="1e7b1-176">U kunt hello Azure portal toomonitor gebruiken en een elastische pool en het Hallo-databases in de groep Hallo beheren.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-176">You can use hello Azure portal toomonitor and manage an elastic pool and hello databases in hello pool.</span></span> <span data-ttu-id="1e7b1-177">Vanuit de portal Hallo kunt u gebruik van een elastische pool en het Hallo-databases binnen die groep Hallo bewaken.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-177">From hello portal, you can monitor hello utilization of an elastic pool and hello databases within that pool.</span></span> <span data-ttu-id="1e7b1-178">U kunt ook een aantal wijzigingen tooyour elastische pool en dienen alle wijzigingen op Hallo dezelfde tijd.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-178">You can also make a set of changes tooyour elastic pool and submit all changes at hello same time.</span></span> <span data-ttu-id="1e7b1-179">Deze wijzigingen omvatten toevoegen of verwijderen van databases, elastische pool-instellingen wijzigen of database-instellingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="1e7b1-180">Hallo volgende afbeelding toont een voorbeeld van de elastische groep.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-180">hello following graphic shows an example elastic pool.</span></span> <span data-ttu-id="1e7b1-181">Hallo-weergave bevat:</span><span class="sxs-lookup"><span data-stu-id="1e7b1-181">hello view includes:</span></span>

*  <span data-ttu-id="1e7b1-182">De grafieken voor het brongebruik van Hallo elastische pool en Hallo-databases die zijn opgenomen in de groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-182">Charts for monitoring resource usage of both hello elastic pool and hello databases contained in hello pool.</span></span>
*  <span data-ttu-id="1e7b1-183">Hallo **configureren** groep knop toomake toohello elastische pool wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-183">hello **Configure** pool button toomake changes toohello elastic pool.</span></span>
*  <span data-ttu-id="1e7b1-184">Hallo **database maken** knop waarmee een database wordt gemaakt en de huidige elastische pool toohello toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-184">hello **Create database** button that creates a database and adds it toohello current elastic pool.</span></span>
*  <span data-ttu-id="1e7b1-185">Groot aantal databases beheren elastische taken die u helpen door te voeren van Transact-SQL-scripts op alle databases in een lijst.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Toepassingen weergeven][2]

<span data-ttu-id="1e7b1-187">Het Resourcegebruik, kunt u tooa bepaalde toepassingen toosee gaan.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-187">You can go tooa particular pool toosee its resource utilization.</span></span> <span data-ttu-id="1e7b1-188">Hallo-groep is standaard geconfigureerde tooshow opslag en het eDTU-gebruik voor Hallo afgelopen uur.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-188">By default, hello pool is configured tooshow storage and eDTU usage for hello last hour.</span></span> <span data-ttu-id="1e7b1-189">Hallo-grafiek kunt geconfigureerde tooshow andere metrische gegevens worden via verschillende tijdvensters.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-189">hello chart can be configured tooshow different metrics over various time windows.</span></span>

1. <span data-ttu-id="1e7b1-190">Selecteer een elastische pool toowork met.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-190">Select an elastic pool toowork with.</span></span>
2. <span data-ttu-id="1e7b1-191">Onder **elastische Pool bewaking** is een grafiek met het label **Resourcegebruik**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="1e7b1-192">Klik op Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-192">Click hello chart.</span></span>

    ![Bewaking van de elastische groep][3]

    <span data-ttu-id="1e7b1-194">Hallo **metriek** blade wordt geopend, waarin een gedetailleerde weergave van Hallo metrische gegevens opgegeven via de opgegeven tijdvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-194">hello **Metric** blade opens, showing a detailed view of hello specified metrics over hello specified time window.</span></span>   

    ![Blade met metrische gegevens][9]

### <a name="toocustomize-hello-chart-display"></a><span data-ttu-id="1e7b1-196">grafiekweergave van toocustomize Hallo</span><span class="sxs-lookup"><span data-stu-id="1e7b1-196">toocustomize hello chart display</span></span>

<span data-ttu-id="1e7b1-197">U kunt Hallo grafiek en Hallo metrische blade toodisplay bewerken andere metrische gegevens zoals CPU-percentage, gegevens-IO-percentage en log-IO-percentage gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-197">You can edit hello chart and hello metric blade toodisplay other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="1e7b1-198">Klik op Hallo metrische blade **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-198">On hello metric blade, click **Edit**.</span></span>

    ![Klik op bewerken][6]

2. <span data-ttu-id="1e7b1-200">In Hallo **grafiek bewerken** blade, selecteert u een tijdsbereik (voorbij vandaag de dag, uur of afgelopen week), of klik op **aangepaste** tooselect een datumbereik in Hallo afgelopen twee weken.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-200">In hello **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** tooselect any date range in hello last two weeks.</span></span> <span data-ttu-id="1e7b1-201">Hallo grafiektype (staaf- of regel) selecteren en selecteer vervolgens Hallo resources toomonitor.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-201">Select hello chart type (bar or line), then select hello resources toomonitor.</span></span>

   > [!Note]
   > <span data-ttu-id="1e7b1-202">Alleen metrische gegevens met dezelfde eenheid kan worden weergegeven in Hallo Hallo grafiek op Hallo dezelfde tijd.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-202">Only metrics with hello same unit of measure can be displayed in hello chart at hello same time.</span></span> <span data-ttu-id="1e7b1-203">Bijvoorbeeld, als u 'eDTU percentage' selecteert kunt vervolgens u alleen selecteren andere metrische gegevens met percentage als eenheid Hallo.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as hello unit of measure.</span></span>
   >

    ![Klik op bewerken](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="1e7b1-205">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="1e7b1-206">Beheren en controleren van de databases in een elastische pool</span><span class="sxs-lookup"><span data-stu-id="1e7b1-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="1e7b1-207">Afzonderlijke databases kunnen ook worden gecontroleerd voor potentiële problemen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="1e7b1-208">Onder **elastische Database bewaken**, er is een diagram waarin metrische gegevens voor vijf databases.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="1e7b1-209">Standaard Hallo diagram toont Hallo bovenste 5 databases in de groep Hallo door gemiddeld eDTU-gebruik in Hallo afgelopen uur.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-209">By default, hello chart displays hello top 5 databases in hello pool by average eDTU usage in hello past hour.</span></span> <span data-ttu-id="1e7b1-210">Klik op Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-210">Click hello chart.</span></span>

    ![Bewaking van de elastische groep][4]

2. <span data-ttu-id="1e7b1-212">Hallo **Database Resourcegebruik** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-212">hello **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="1e7b1-213">Dit biedt een gedetailleerde weergave van het Databasegebruik Hallo in Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-213">This provides a detailed view of hello database usage in hello pool.</span></span> <span data-ttu-id="1e7b1-214">Hallo raster Hallo onder in de blade Hallo gebruikt, kunt u geen databases in Hallo groep toodisplay het gebruik ervan in de grafiek hello (omhoog too5 databases).</span><span class="sxs-lookup"><span data-stu-id="1e7b1-214">Using hello grid in hello lower part of hello blade, you can select any databases in hello pool toodisplay its usage in hello chart (up too5 databases).</span></span> <span data-ttu-id="1e7b1-215">U kunt ook aanpassen Hallo metrische gegevens en het tijdstip venster wordt weergegeven in de grafiek Hallo door te klikken op **grafiek bewerken**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-215">You can also customize hello metrics and time window displayed in hello chart by clicking **Edit chart**.</span></span>

    ![Gebruik van de databaseblade resource][8]

### <a name="toocustomize-hello-view"></a><span data-ttu-id="1e7b1-217">toocustomize hello weergeven</span><span class="sxs-lookup"><span data-stu-id="1e7b1-217">toocustomize hello view</span></span>

1. <span data-ttu-id="1e7b1-218">In Hallo **Resourcegebruik van de Database** blade, klikt u op **grafiek bewerken**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-218">In hello **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Klik op de grafiek bewerken](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="1e7b1-220">In Hallo **bewerken** blade grafiek, selecteert u een tijdsbereik (voorbij uur of afgelopen 24 uur) of klik op **aangepaste** tooselect een andere dag in Hallo voorbij toodisplay 2 weken.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-220">In hello **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** tooselect a different day in hello past 2 weeks toodisplay.</span></span>

    ![Klik op aangepast](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="1e7b1-222">Klik op Hallo **vergelijken databases door** dropdown tooselect verschillende metrische toouse bij het vergelijken van databases.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-222">Click hello **Compare databases by** dropdown tooselect a different metric toouse when comparing databases.</span></span>

    ![Hallo grafiek bewerken](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a><span data-ttu-id="1e7b1-224">tooselect databases toomonitor</span><span class="sxs-lookup"><span data-stu-id="1e7b1-224">tooselect databases toomonitor</span></span>

<span data-ttu-id="1e7b1-225">In de lijst met de Hallo database in Hallo **Database Resourcegebruik** blade kunt u bepaalde databases vinden door te zoeken door Hallo pagina's in de lijst Hallo of door in het Hallo-naam van een database te typen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-225">In hello database list in hello **Database Resource Utilization** blade, you can find particular databases by looking through hello pages in hello list or by typing in hello name of a database.</span></span> <span data-ttu-id="1e7b1-226">Hallo selectievakje tooselect Hallo database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-226">Use hello checkbox tooselect hello database.</span></span>

![Zoeken naar databases toomonitor][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="1e7b1-228">Een elastische pool waarschuwing tooan resource toevoegen</span><span class="sxs-lookup"><span data-stu-id="1e7b1-228">Add an alert tooan elastic pool resource</span></span>

<span data-ttu-id="1e7b1-229">Regels tooan elastische groep die e-mail verzenden toopeople of waarschuwing tekenreeksen tooURL eindpunten wanneer Hallo elastische pool treffers een drempelwaarde voor overbenutting die u hebt ingesteld, kunt u toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-229">You can add rules tooan elastic pool that send email toopeople or alert strings tooURL endpoints when hello elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="1e7b1-230">**een waarschuwing tooany resource tooadd:**</span><span class="sxs-lookup"><span data-stu-id="1e7b1-230">**tooadd an alert tooany resource:**</span></span>

1. <span data-ttu-id="1e7b1-231">Klik op Hallo **Resourcegebruik** grafiek tooopen Hallo **metriek** blade klikt u op **waarschuwing toevoegen**, en vult u de informatie in Hallo Hallo **een waarschuwing toevoegen regel** blade (**Resource** automatisch ingesteld toobe Hallo toepassingen waarmee u werkt).</span><span class="sxs-lookup"><span data-stu-id="1e7b1-231">Click hello **Resource utilization** chart tooopen hello **Metric** blade, click **Add alert**, and then fill out hello information in hello **Add an alert rule** blade (**Resource** is automatically set up toobe hello pool you're working with).</span></span>
2. <span data-ttu-id="1e7b1-232">Typ een **naam** en **beschrijving** die Hallo waarschuwing tooyou en Hallo ontvangers identificeert.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-232">Type a **Name** and **Description** that identifies hello alert tooyou and hello recipients.</span></span>
3. <span data-ttu-id="1e7b1-233">Kies een **metriek** dat u wilt dat tooalert uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-233">Choose a **Metric** that you want tooalert from hello list.</span></span>

    <span data-ttu-id="1e7b1-234">Hallo diagram toont dynamisch Resourcegebruik voor die metrische toohelp die u kiest een drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-234">hello chart dynamically shows resource utilization for that metric toohelp you choose a threshold.</span></span>

4. <span data-ttu-id="1e7b1-235">Kies een **voorwaarde** (groter dan maximaal, enzovoort) en een **drempelwaarde**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="1e7b1-236">Kies een **periode** hoelang Hallo metriek regel moet worden voldaan voordat de waarschuwing Hallo-triggers.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-236">Choose a **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span>
6. <span data-ttu-id="1e7b1-237">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-237">Click **OK**.</span></span>

<span data-ttu-id="1e7b1-238">Zie voor meer informatie [waarschuwingen van de SQL-Database maken in Azure portal](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1e7b1-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="1e7b1-239">Een database verplaatsen naar een elastische pool</span><span class="sxs-lookup"><span data-stu-id="1e7b1-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="1e7b1-240">U kunt toevoegen of verwijderen van databases uit een bestaande groep.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="1e7b1-241">Hallo-databases kunnen zich in andere toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-241">hello databases can be in other pools.</span></span> <span data-ttu-id="1e7b1-242">U kunt echter alleen toevoegen databases die zijn op Hallo dezelfde logische server.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-242">However, you can only add databases that are on hello same logical server.</span></span>

1. <span data-ttu-id="1e7b1-243">Hallo-blade voor Hallo-toepassingen onder **elastische databases** klikt u op **pool configureren**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-243">In hello blade for hello pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Klik op pool configureren][1]

2. <span data-ttu-id="1e7b1-245">In Hallo **pool configureren** blade, klikt u op **toopool toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-245">In hello **Configure pool** blade, click **Add toopool**.</span></span>

    ![Klik op toevoegen toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="1e7b1-247">In Hallo **databases toevoegen** blade, selecteer Hallo database of databases tooadd toohello van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-247">In hello **Add databases** blade, select hello database or databases tooadd toohello pool.</span></span> <span data-ttu-id="1e7b1-248">Klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-248">Then click **Select**.</span></span>

    ![Selecteer de databases tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="1e7b1-250">Hallo **pool configureren** blade nu een lijst met toobe toegevoegd met de status ervan instellen te geselecteerde database Hallo**in behandeling**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-250">hello **Configure pool** blade now lists hello database you selected toobe added, with its status set too**Pending**.</span></span>

    ![In behandeling pool-toevoegingen](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="1e7b1-252">In Hallo **blade van de pool configureren**, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-252">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Op Opslaan klikken](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="1e7b1-254">Een database verplaatst buiten een elastische pool</span><span class="sxs-lookup"><span data-stu-id="1e7b1-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="1e7b1-255">In Hallo **pool configureren** blade, selecteer Hallo database of databases tooremove.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-255">In hello **Configure pool** blade, select hello database or databases tooremove.</span></span>

    ![databases weergeven](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="1e7b1-257">Klik op **verwijderen uit groep**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-257">Click **Remove from pool**.</span></span>

    ![databases weergeven](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="1e7b1-259">Hallo **pool configureren** blade nu een lijst met toobe verwijderd met de status ervan instellen te geselecteerde database Hallo**in behandeling**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-259">hello **Configure pool** blade now lists hello database you selected toobe removed with its status set too**Pending**.</span></span>

    ![voorbeeld database toevoegen en verwijderen](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="1e7b1-261">In Hallo **blade van de pool configureren**, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-261">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Op Opslaan klikken](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="1e7b1-263">Instellingen van de prestaties van een elastische groep wijzigen</span><span class="sxs-lookup"><span data-stu-id="1e7b1-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="1e7b1-264">Tijdens het controleren van Resourcegebruik Hallo van een pool voor elastische ontdekt u dat bepaalde aanpassingen nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-264">As you monitor hello resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="1e7b1-265">Hallo-groep moet mogelijk een wijziging in Hallo prestaties of de opslag limieten.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-265">Maybe hello pool needs a change in hello performance or storage limits.</span></span> <span data-ttu-id="1e7b1-266">Mogelijk wilt u toochange Hallo database-instellingen in Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-266">Possibly you want toochange hello database settings in hello pool.</span></span> <span data-ttu-id="1e7b1-267">U kunt setup Hallo van Hallo van toepassingen die op elk moment tooget Hallo beste balans van prestaties en kosten wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-267">You can change hello setup of hello pool at any time tooget hello best balance of performance and cost.</span></span> <span data-ttu-id="1e7b1-268">Zie [wanneer moet een elastische pool worden gebruikt?](sql-database-elastic-pool.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="1e7b1-269">toochange hello edtu's of opslag limieten per groep van toepassingen en edtu's per database:</span><span class="sxs-lookup"><span data-stu-id="1e7b1-269">toochange hello eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="1e7b1-270">Open Hallo **pool configureren** blade.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-270">Open hello **Configure pool** blade.</span></span>

    <span data-ttu-id="1e7b1-271">Onder **elastische groepsinstellingen**, ofwel groepsinstellingen schuifregelaar toochange hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-271">Under **elastic pool settings**, use either slider toochange hello pool settings.</span></span>

    ![Resourcegebruik van de elastische groep](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="1e7b1-273">Wanneer Hallo-instelling wordt gewijzigd, ziet u Hallo weergave Hallo Geschatte maandelijkse kosten van Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-273">When hello setting changes, hello display shows hello estimated monthly cost of hello change.</span></span>

    ![Bijwerken van een elastische pool en nieuwe maandelijkse kosten](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="1e7b1-275">Latentie van bewerkingen van de elastische groep</span><span class="sxs-lookup"><span data-stu-id="1e7b1-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="1e7b1-276">Hallo min edtu's per database of max edtu's per database doorgaans wijzigen is voltooid in de 5 minuten of minder.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-276">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="1e7b1-277">Hallo edtu's per groep wijzigen hangt af van de totale hoeveelheid ruimte die wordt gebruikt door alle databases in de groep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-277">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="1e7b1-278">Wijzigingen duren gemiddeld 90 minuten of minder per 100 GB.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="1e7b1-279">Bijvoorbeeld, als de totale ruimte hello worden gebruikt door alle databases in de groep Hallo is 200 GB en vervolgens Hallo verwachte latentie voor het wijzigen van Hallo groeps-eDTU per pool is drie uur of minder.</span><span class="sxs-lookup"><span data-stu-id="1e7b1-279">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e7b1-280">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1e7b1-280">Next steps</span></span>

- <span data-ttu-id="1e7b1-281">welke een elastische groep is, Zie toounderstand [elastische pool in SQL-Database](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="1e7b1-281">toounderstand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="1e7b1-282">Zie voor instructies over het gebruik van elastische pools [prijs- en Prestatieoverwegingen voor elastische pools](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="1e7b1-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="1e7b1-283">toouse elastische taken toorun Transact-SQL-scripts uitvoeren op een willekeurig aantal databases in de groep hello, Zie [elastische taken overzicht](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1e7b1-283">toouse elastic jobs toorun Transact-SQL scripts against any number of databases in hello pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="1e7b1-284">tooquery via een willekeurig aantal databases in de groep hello, Zie [elastische query overzicht](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1e7b1-284">tooquery across any number of databases in hello pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="1e7b1-285">Zie voor transacties een willekeurig aantal databases in de groep hello, [elastische transacties](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1e7b1-285">For transactions any number of databases in hello pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
