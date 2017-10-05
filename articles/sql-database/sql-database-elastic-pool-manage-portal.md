---
title: 'Azure-portal: maken en beheren van een elastische pool SQL Database | Microsoft Docs'
description: Informatie over het gebruik van de Azure portal en de ingebouwde intelligentie SQL-Database om te beheren, controleren en het juiste formaat een schaalbare elastische pool te optimaliseren van databaseprestaties en kosten beheren.
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
ms.openlocfilehash: 4ffd1db31f42967dc7f07aa979898dddbb333641
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-the-azure-portal"></a><span data-ttu-id="a0c13-103">Maken en beheren van een elastische groep met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="a0c13-103">Create and manage an elastic pool with the Azure portal</span></span>
<span data-ttu-id="a0c13-104">In dit onderwerp wordt beschreven hoe u maken en beheren van schaalbare [elastische pools](sql-database-elastic-pool.md) met de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a0c13-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with the Azure portal.</span></span> <span data-ttu-id="a0c13-105">U kunt ook maken en beheren van een Azure elastische groep met [PowerShell](sql-database-elastic-pool-manage-powershell.md), de REST-API of [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="a0c13-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="a0c13-106">U kunt ook maken en databases verplaatsen naar en van elastische pools met [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="a0c13-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="a0c13-107">Elastische pool maken</span><span class="sxs-lookup"><span data-stu-id="a0c13-107">Create an elastic pool</span></span> 

<span data-ttu-id="a0c13-108">Er zijn twee manieren kunt u een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="a0c13-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="a0c13-109">U kunt dit zelf doen, als u weet welke instellingen u voor uw groep wilt gebruiken, of u kunt gebruikmaken van wat de service u aanraadt.</span><span class="sxs-lookup"><span data-stu-id="a0c13-109">You can do it from scratch if you know the pool setup you want, or start with a recommendation from the service.</span></span> <span data-ttu-id="a0c13-110">SQL-Database beschikt over ingebouwde intelligentie die raadt aan om een elastische groep is ingesteld als het kostenefficiënte op basis van de gebruikstelemetrie van uw databases.</span><span class="sxs-lookup"><span data-stu-id="a0c13-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on the past usage telemetry for your databases.</span></span>

<span data-ttu-id="a0c13-111">U kunt meerdere groepen maken op een server, maar u kunt geen databases van verschillende servers toevoegen aan dezelfde pool.</span><span class="sxs-lookup"><span data-stu-id="a0c13-111">You can create multiple pools on a server, but you can't add databases from different servers into the same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="a0c13-112">Elastische pools zijn algemeen beschikbaar in alle Azure-regio's, behalve in West-India, waar deze zich momenteel in de previewfase bevinden.</span><span class="sxs-lookup"><span data-stu-id="a0c13-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="a0c13-113">Algemene beschikbaarheid van elastische pools in deze regio zal zo snel mogelijk plaatsvinden.</span><span class="sxs-lookup"><span data-stu-id="a0c13-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="a0c13-114">Stap 1: Een elastische pool maken</span><span class="sxs-lookup"><span data-stu-id="a0c13-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="a0c13-115">Een elastische pool te maken van een bestaand **server** blade in de portal is de eenvoudigste manier om te verplaatsen van bestaande databases in een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="a0c13-115">Creating an elastic pool from an existing **server** blade in the portal is the easiest way to move existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="a0c13-116">U kunt ook een elastische pool maken door te zoeken naar **elastische SQL-groep** in de **Marketplace** of klikken op **+ toevoegen** in de **SQL elastische pools** blade bladeren.</span><span class="sxs-lookup"><span data-stu-id="a0c13-116">You can also create an elastic pool by searching **SQL elastic pool** in the **Marketplace** or clicking **+Add** in the **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="a0c13-117">U bent een nieuwe of bestaande server via deze werkstroom van toepassingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="a0c13-117">You are able to specify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="a0c13-118">In de [Azure-portal](http://portal.azure.com/), klikt u op **meer services**  **>**  **SQL-servers**, en klik vervolgens op de server waarop de databases die u wilt toevoegen aan een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="a0c13-118">In the [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click the server that contains the databases you want to add to an elastic pool.</span></span>
2. <span data-ttu-id="a0c13-119">Klik op **Nieuwe groep**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-119">Click **New pool**.</span></span>

    ![Voeg de groep toe aan een server](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="a0c13-121">**-OF-**</span><span class="sxs-lookup"><span data-stu-id="a0c13-121">**-OR-**</span></span>

    <span data-ttu-id="a0c13-122">Mogelijk ziet u een bericht weergegeven dat er aanbevolen elastische pools voor de server.</span><span class="sxs-lookup"><span data-stu-id="a0c13-122">You may see a message saying there are recommended elastic pools for the server.</span></span> <span data-ttu-id="a0c13-123">Klik op het bericht om de groepen die worden aanbevolen op basis van de telemetrie van het databasegebruik te bekijken. Klik vervolgens op de categorie voor meer informatie en om de groep aan te passen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-123">Click the message to see the recommended pools based on historical database usage telemetry, and then click the tier to see more details and customize the pool.</span></span> <span data-ttu-id="a0c13-124">Zie [Aanbevelingen voor groepen begrijpen](#understand-elastic-pool-recommendations) verderop in dit onderwerp om te ontdekken hoe de aanbeveling tot stand is gekomen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how the recommendation is made.</span></span>

    ![aanbevolen groep](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="a0c13-126">De **elastische pool** blade wordt weergegeven waarin u de instellingen voor uw groep opgeven.</span><span class="sxs-lookup"><span data-stu-id="a0c13-126">The **elastic pool** blade appears, which is where you specify the settings for your pool.</span></span> <span data-ttu-id="a0c13-127">Als u hebt geklikt **nieuwe pool** in de vorige stap, de prijscategorie is **standaard** standaard en geen databases geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="a0c13-127">If you clicked **New pool** in the previous step, the pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="a0c13-128">U kunt een lege pool maken of een set bestaande databases van deze server opgeven die moeten worden verplaatst naar de pool.</span><span class="sxs-lookup"><span data-stu-id="a0c13-128">You can create an empty pool, or specify a set of existing databases from that server to move into the pool.</span></span> <span data-ttu-id="a0c13-129">Als u een aanbevolen pool maakt, zijn de aanbevolen prijscategorie, de prestatie-instellingen en de lijst met databases vooraf ingevuld, maar u ze nog steeds wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-129">If you are creating a recommended pool, the recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Elastische groep configureren](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="a0c13-131">Kies een naam voor de elastische groep, of behoud de standaardnaam.</span><span class="sxs-lookup"><span data-stu-id="a0c13-131">Specify a name for the elastic pool, or leave it as the default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="a0c13-132">Stap 2: kies een prijscategorie</span><span class="sxs-lookup"><span data-stu-id="a0c13-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="a0c13-133">De prijscategorie van de pool bepaalt welke functies beschikbaar zijn voor de elastics in de groep en het maximale aantal edtu's (eDTU MAX) en opslag (GB) beschikbaar zijn voor elke database.</span><span class="sxs-lookup"><span data-stu-id="a0c13-133">The pool's pricing tier determines the features available to the elastics in the pool, and the maximum number of eDTUs (eDTU MAX), and storage (GBs) available to each database.</span></span> <span data-ttu-id="a0c13-134">Zie voor meer informatie de Servicecategorieën.</span><span class="sxs-lookup"><span data-stu-id="a0c13-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="a0c13-135">Klik op **Prijscategorie** om de prijscategorie van de pool te wijzigen. Klik op de gewenste prijscategorie en vervolgens op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-135">To change the pricing tier for the pool, click **Pricing tier**, click the pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0c13-136">Nadat u de prijscategorie gekozen heeft en uw wijzigingen heeft opgeslagen door in de laatste stap op **OK** te klikken, kunt u de prijscategorie van de groep niet meer wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-136">After you choose the pricing tier and commit your changes by clicking **OK** in the last step, you won't be able to change the pricing tier of the pool.</span></span> <span data-ttu-id="a0c13-137">De prijscategorie voor een bestaande elastische pool niet wijzigen, een elastische pool maken in de gewenste prijscategorie en migreert de databases naar deze nieuwe pool.</span><span class="sxs-lookup"><span data-stu-id="a0c13-137">To change the pricing tier for an existing elastic pool, create an elastic pool in the desired pricing tier and migrate the databases to this new pool.</span></span>
>

![Een prijscategorie selecteren](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-the-pool"></a><span data-ttu-id="a0c13-139">Stap 3: configureer de groep</span><span class="sxs-lookup"><span data-stu-id="a0c13-139">Step 3: Configure the pool</span></span>

<span data-ttu-id="a0c13-140">Zodra de prijscategorie is ingesteld, klikt u op pool configureren Hier voegt u databases, set groepen met edtu's en opslag (GB adresgroep) en waar u de min en max edtu's voor de elastics instellen in de groep.</span><span class="sxs-lookup"><span data-stu-id="a0c13-140">After setting the pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set the min and max eDTUs for the elastics in the pool.</span></span>

1. <span data-ttu-id="a0c13-141">Klik op **Groep configureren**</span><span class="sxs-lookup"><span data-stu-id="a0c13-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="a0c13-142">Selecteer de databases die u aan de groep wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-142">Select the databases you want to add to the pool.</span></span> <span data-ttu-id="a0c13-143">Deze stap is optioneel bij het maken van de groep.</span><span class="sxs-lookup"><span data-stu-id="a0c13-143">This step is optional while creating the pool.</span></span> <span data-ttu-id="a0c13-144">Databases kunnen ook worden toegevoegd wanneer de groep is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a0c13-144">Databases can be added after the pool has been created.</span></span>
    <span data-ttu-id="a0c13-145">Om databases toe te voegen klikt u op **Database toevoegen** en vervolgens op de databases die u wilt toevoegen. Klik als laatste op de knop **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-145">To add databases, click **Add database**, click the databases that you want to add, and then click the **Select** button.</span></span>

    ![Databases toevoegen](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="a0c13-147">Als de gebruikstelemetrie van de databases waar u mee werkt genoeg is, worden de grafiek **Geschat eDTU- en GB-gebruik** en het staafdiagram **Werkelijk eDTU-gebruik** bijgewerkt zodat u betere beslissingen kunt nemen met betrekking tot de configuratie.</span><span class="sxs-lookup"><span data-stu-id="a0c13-147">If the databases you're working with have enough historical usage telemetry, the **Estimated eDTU and GB usage** graph and the **Actual eDTU usage** bar chart update to help you make configuration decisions.</span></span> <span data-ttu-id="a0c13-148">De service kan ook een bericht weergeven met een aanbeveling zodat u de groep het juiste formaat kunt geven.</span><span class="sxs-lookup"><span data-stu-id="a0c13-148">Also, the service may give you a recommendation message to help you right-size the pool.</span></span> <span data-ttu-id="a0c13-149">Zie [Dynamische aanbevelingen](#understand-elastic-pool-recommendations).</span><span class="sxs-lookup"><span data-stu-id="a0c13-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="a0c13-150">Gebruik de bedieningselementen op de pagina **Groep configureren** om de instellingen te verkennen en uw groep te configureren.</span><span class="sxs-lookup"><span data-stu-id="a0c13-150">Use the controls on the **Configure pool** page to explore settings and configure your pool.</span></span> <span data-ttu-id="a0c13-151">Zie [limieten elastische pools](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) voor meer informatie over de limieten van elke servicecategorie en Zie [prijs- en Prestatieoverwegingen voor elastische pools](sql-database-elastic-pool.md) voor gedetailleerde richtlijnen voor het juiste formaat een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="a0c13-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="a0c13-152">Zie voor meer informatie over de groepsinstellingen [eigenschappen van de elastische groep](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="a0c13-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Elastische groep configureren](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="a0c13-154">Klik op **Selectere** in de blade **Groep configureren** nadat u de instellingen heeft gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="a0c13-154">Click **Select** in the **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="a0c13-155">Klik op **OK** om de groep te maken.</span><span class="sxs-lookup"><span data-stu-id="a0c13-155">Click **OK** to create the pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="a0c13-156">Aanbevelingen voor elastische Pools begrijpen</span><span class="sxs-lookup"><span data-stu-id="a0c13-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="a0c13-157">De SQL Database-service beoordeelt de gebruiksgeschiedenis en beveelt een of meerdere groepen aan wanneer deze kosteneffectiever zijn dan het gebruik van individuele databases.</span><span class="sxs-lookup"><span data-stu-id="a0c13-157">The SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="a0c13-158">Elke aanbeveling wordt geconfigureerd met een unieke subset van de databases van de server die het meest geschikt zijn voor de groep.</span><span class="sxs-lookup"><span data-stu-id="a0c13-158">Each recommendation is configured with a unique subset of the server's databases that best fit the pool.</span></span>

![aanbevolen groep](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="a0c13-160">De aanbevelingen voor de groep bestaan uit:</span><span class="sxs-lookup"><span data-stu-id="a0c13-160">The pool recommendation comprises:</span></span>

- <span data-ttu-id="a0c13-161">Een prijscategorie voor de pool (Basic, Standard, Premium of RS Premium)</span><span class="sxs-lookup"><span data-stu-id="a0c13-161">A pricing tier for the pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="a0c13-162">De juiste **eDTU’s voor de groep** (ook wel Max eDTU's per groep)</span><span class="sxs-lookup"><span data-stu-id="a0c13-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="a0c13-163">De **eDTU MAX** en **eDTU Min** per database</span><span class="sxs-lookup"><span data-stu-id="a0c13-163">The **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="a0c13-164">De lijst met aanbevolen databases voor de groep</span><span class="sxs-lookup"><span data-stu-id="a0c13-164">The list of recommended databases for the pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0c13-165">De service houdt rekening met de laatste 30 dagen telemetrie bij het aanbevelen van groepen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-165">The service takes the last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="a0c13-166">Voor een database te worden beschouwd als kandidaat voor een elastische pool, moet er ten minste 7 dagen bestaan.</span><span class="sxs-lookup"><span data-stu-id="a0c13-166">For a database to be considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="a0c13-167">Databases die zich al in een elastische pool bevinden, worden niet aanbevolen voor een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="a0c13-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="a0c13-168">De service beoordeelt wat de resource nodig heeft en hoe kosteneffectief het is om de individuele databases in elke servicecategorie te verplaatsen naar groepen van dezelfde categorie.</span><span class="sxs-lookup"><span data-stu-id="a0c13-168">The service evaluates resource needs and cost effectiveness of moving the single databases in each service tier into pools of the same tier.</span></span> <span data-ttu-id="a0c13-169">Alle Standard databases op een server worden bijvoorbeeld beoordeeld op hoe ze in een Standard elastische groep passen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="a0c13-170">Dit betekent dat de service geen aanbevelingen doet voor het verplaatsen van databases naar een andere categorie, zoals het verplaatsen van een Standard database naar een Premium groep.</span><span class="sxs-lookup"><span data-stu-id="a0c13-170">This means the service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="a0c13-171">Nadat databases zijn toegevoegd aan de groep, worden aanbevelingen dynamisch gegenereerd op basis van het gebruik van de databases die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="a0c13-171">After adding databases to the pool, recommendations are dynamically generated based on the historical usage of the databases you have selected.</span></span> <span data-ttu-id="a0c13-172">Deze aanbevelingen worden weergegeven in de eDTU- en GB-gebruiksgrafiek en in een banner aan de bovenkant van de **pool configureren** blade.</span><span class="sxs-lookup"><span data-stu-id="a0c13-172">These recommendations are shown in the eDTU and GB usage chart and in a recommendation banner at the top of the **Configure pool** blade.</span></span> <span data-ttu-id="a0c13-173">Deze aanbevelingen zijn bedoeld om u te helpen bij het maken van een elastische pool die geoptimaliseerd is voor uw specifieke databases.</span><span class="sxs-lookup"><span data-stu-id="a0c13-173">These recommendations are intended to assist you in creating an elastic pool optimized for your specific databases.</span></span>

![dynamische aanbevelingen](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="a0c13-175">Beheren en controleren van een elastische pool</span><span class="sxs-lookup"><span data-stu-id="a0c13-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="a0c13-176">U kunt de Azure portal gebruiken om te controleren en beheren van een elastische groep en de databases in de pool.</span><span class="sxs-lookup"><span data-stu-id="a0c13-176">You can use the Azure portal to monitor and manage an elastic pool and the databases in the pool.</span></span> <span data-ttu-id="a0c13-177">U kunt het gebruik van een elastische groep en de databases binnen die groep bewaken vanuit de portal.</span><span class="sxs-lookup"><span data-stu-id="a0c13-177">From the portal, you can monitor the utilization of an elastic pool and the databases within that pool.</span></span> <span data-ttu-id="a0c13-178">U kunt ook een aantal wijzigingen aanbrengen in uw elastische groep en alle wijzigingen tegelijk verzenden.</span><span class="sxs-lookup"><span data-stu-id="a0c13-178">You can also make a set of changes to your elastic pool and submit all changes at the same time.</span></span> <span data-ttu-id="a0c13-179">Deze wijzigingen omvatten toevoegen of verwijderen van databases, elastische pool-instellingen wijzigen of database-instellingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="a0c13-180">De volgende afbeelding toont een voorbeeld van de elastische groep.</span><span class="sxs-lookup"><span data-stu-id="a0c13-180">The following graphic shows an example elastic pool.</span></span> <span data-ttu-id="a0c13-181">De weergave bevat:</span><span class="sxs-lookup"><span data-stu-id="a0c13-181">The view includes:</span></span>

*  <span data-ttu-id="a0c13-182">De grafieken voor het brongebruik van de elastische groep en de databases die zijn opgenomen in de groep.</span><span class="sxs-lookup"><span data-stu-id="a0c13-182">Charts for monitoring resource usage of both the elastic pool and the databases contained in the pool.</span></span>
*  <span data-ttu-id="a0c13-183">De **configureren** knop wijzigingen aanbrengen in de elastische groep van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-183">The **Configure** pool button to make changes to the elastic pool.</span></span>
*  <span data-ttu-id="a0c13-184">De **database maken** knop waarmee een database wordt gemaakt en toegevoegd aan de huidige elastische groep.</span><span class="sxs-lookup"><span data-stu-id="a0c13-184">The **Create database** button that creates a database and adds it to the current elastic pool.</span></span>
*  <span data-ttu-id="a0c13-185">Groot aantal databases beheren elastische taken die u helpen door te voeren van Transact-SQL-scripts op alle databases in een lijst.</span><span class="sxs-lookup"><span data-stu-id="a0c13-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Toepassingen weergeven][2]

<span data-ttu-id="a0c13-187">U kunt gaan naar een bepaalde groep om te zien van de bronnen beter worden benut.</span><span class="sxs-lookup"><span data-stu-id="a0c13-187">You can go to a particular pool to see its resource utilization.</span></span> <span data-ttu-id="a0c13-188">Standaard worden de toepassingen is geconfigureerd voor het weergeven van opslag en het eDTU-gebruik voor het afgelopen uur.</span><span class="sxs-lookup"><span data-stu-id="a0c13-188">By default, the pool is configured to show storage and eDTU usage for the last hour.</span></span> <span data-ttu-id="a0c13-189">De grafiek kan worden geconfigureerd voor andere metrische gegevens weergeven over verschillende tijdvensters.</span><span class="sxs-lookup"><span data-stu-id="a0c13-189">The chart can be configured to show different metrics over various time windows.</span></span>

1. <span data-ttu-id="a0c13-190">Selecteer een elastische pool met werkt.</span><span class="sxs-lookup"><span data-stu-id="a0c13-190">Select an elastic pool to work with.</span></span>
2. <span data-ttu-id="a0c13-191">Onder **elastische Pool bewaking** is een grafiek met het label **Resourcegebruik**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="a0c13-192">Klik op de grafiek.</span><span class="sxs-lookup"><span data-stu-id="a0c13-192">Click the chart.</span></span>

    ![Bewaking van de elastische groep][3]

    <span data-ttu-id="a0c13-194">De **metriek** blade wordt geopend, waarin een gedetailleerde weergave van de opgegeven metrische gegevens via de opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="a0c13-194">The **Metric** blade opens, showing a detailed view of the specified metrics over the specified time window.</span></span>   

    ![Blade met metrische gegevens][9]

### <a name="to-customize-the-chart-display"></a><span data-ttu-id="a0c13-196">De grafiekweergave aanpassen</span><span class="sxs-lookup"><span data-stu-id="a0c13-196">To customize the chart display</span></span>

<span data-ttu-id="a0c13-197">U kunt de metrische blade om weer te geven van andere metrische gegevens zoals CPU-percentage, gegevens-IO-percentage en log-IO-percentage gebruikt en de grafiek bewerken.</span><span class="sxs-lookup"><span data-stu-id="a0c13-197">You can edit the chart and the metric blade to display other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="a0c13-198">Klik op de blade metrische **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-198">On the metric blade, click **Edit**.</span></span>

    ![Klik op bewerken][6]

2. <span data-ttu-id="a0c13-200">In de **grafiek bewerken** blade, selecteert u een tijdsbereik (voorbij vandaag de dag, uur of afgelopen week), of klik op **aangepaste** datumbereik selecteren in de afgelopen twee weken.</span><span class="sxs-lookup"><span data-stu-id="a0c13-200">In the **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** to select any date range in the last two weeks.</span></span> <span data-ttu-id="a0c13-201">Selecteer het grafiektype (staaf- of regel) en selecteer vervolgens de bronnen om te controleren.</span><span class="sxs-lookup"><span data-stu-id="a0c13-201">Select the chart type (bar or line), then select the resources to monitor.</span></span>

   > [!Note]
   > <span data-ttu-id="a0c13-202">Metrische gegevens met de dezelfde eenheid kunnen worden weergegeven in de grafiek op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="a0c13-202">Only metrics with the same unit of measure can be displayed in the chart at the same time.</span></span> <span data-ttu-id="a0c13-203">Bijvoorbeeld, als u 'eDTU percentage' selecteert kunt vervolgens u alleen selecteren andere metrische gegevens met percentage als de maateenheid.</span><span class="sxs-lookup"><span data-stu-id="a0c13-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as the unit of measure.</span></span>
   >

    ![Klik op bewerken](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="a0c13-205">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="a0c13-206">Beheren en controleren van de databases in een elastische pool</span><span class="sxs-lookup"><span data-stu-id="a0c13-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="a0c13-207">Afzonderlijke databases kunnen ook worden gecontroleerd voor potentiële problemen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="a0c13-208">Onder **elastische Database bewaken**, er is een diagram waarin metrische gegevens voor vijf databases.</span><span class="sxs-lookup"><span data-stu-id="a0c13-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="a0c13-209">Standaard het diagram toont de bovenste 5 databases in de groep door gemiddeld eDTU-gebruik in het afgelopen uur.</span><span class="sxs-lookup"><span data-stu-id="a0c13-209">By default, the chart displays the top 5 databases in the pool by average eDTU usage in the past hour.</span></span> <span data-ttu-id="a0c13-210">Klik op de grafiek.</span><span class="sxs-lookup"><span data-stu-id="a0c13-210">Click the chart.</span></span>

    ![Bewaking van de elastische groep][4]

2. <span data-ttu-id="a0c13-212">De **Database Resourcegebruik** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a0c13-212">The **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="a0c13-213">Dit biedt een gedetailleerde weergave van het Databasegebruik in de groep.</span><span class="sxs-lookup"><span data-stu-id="a0c13-213">This provides a detailed view of the database usage in the pool.</span></span> <span data-ttu-id="a0c13-214">Het raster in het onderste gedeelte van de blade kunt u geen databases selecteren in de groep om het gebruik ervan in de grafiek (maximaal 5 databases) weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a0c13-214">Using the grid in the lower part of the blade, you can select any databases in the pool to display its usage in the chart (up to 5 databases).</span></span> <span data-ttu-id="a0c13-215">U kunt ook de metrische gegevens en het tijdstip venster wordt weergegeven in de grafiek door te klikken op **grafiek bewerken**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-215">You can also customize the metrics and time window displayed in the chart by clicking **Edit chart**.</span></span>

    ![Gebruik van de databaseblade resource][8]

### <a name="to-customize-the-view"></a><span data-ttu-id="a0c13-217">De weergave aanpassen</span><span class="sxs-lookup"><span data-stu-id="a0c13-217">To customize the view</span></span>

1. <span data-ttu-id="a0c13-218">In de **Resourcegebruik van de Database** blade, klikt u op **grafiek bewerken**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-218">In the **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Klik op de grafiek bewerken](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="a0c13-220">In de **bewerken** blade grafiek, selecteert u een tijdsbereik (voorbij uur of afgelopen 24 uur) of klik op **aangepaste** selecteren van een andere dag in de afgelopen twee weken om weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a0c13-220">In the **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** to select a different day in the past 2 weeks to display.</span></span>

    ![Klik op aangepast](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="a0c13-222">Klik op de **vergelijken databases door** dropdown selecteren van een andere waarde voor gebruik bij het vergelijken van databases.</span><span class="sxs-lookup"><span data-stu-id="a0c13-222">Click the **Compare databases by** dropdown to select a different metric to use when comparing databases.</span></span>

    ![De grafiek bewerken](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="to-select-databases-to-monitor"></a><span data-ttu-id="a0c13-224">Databases bewaken selecteren</span><span class="sxs-lookup"><span data-stu-id="a0c13-224">To select databases to monitor</span></span>

<span data-ttu-id="a0c13-225">In de databaselijst in de **Database Resourcegebruik** blade kunt u bepaalde databases vinden door te zoeken door de pagina's in de lijst of typ in de naam van een database.</span><span class="sxs-lookup"><span data-stu-id="a0c13-225">In the database list in the **Database Resource Utilization** blade, you can find particular databases by looking through the pages in the list or by typing in the name of a database.</span></span> <span data-ttu-id="a0c13-226">Gebruik de selectievakjes om de database te selecteren.</span><span class="sxs-lookup"><span data-stu-id="a0c13-226">Use the checkbox to select the database.</span></span>

![Zoeken naar databases bewaken][7]


## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="a0c13-228">Een waarschuwing toevoegen aan een resource voor de elastische groep</span><span class="sxs-lookup"><span data-stu-id="a0c13-228">Add an alert to an elastic pool resource</span></span>

<span data-ttu-id="a0c13-229">U kunt regels toevoegen aan een elastische groep die e-mail verzenden naar personen of waarschuwing tekenreeksen met URL-eindpunten wanneer de elastische groep treffers een drempelwaarde voor overbenutting die u hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a0c13-229">You can add rules to an elastic pool that send email to people or alert strings to URL endpoints when the elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="a0c13-230">**Een waarschuwing toevoegen aan een resource:**</span><span class="sxs-lookup"><span data-stu-id="a0c13-230">**To add an alert to any resource:**</span></span>

1. <span data-ttu-id="a0c13-231">Klik op de **Resourcegebruik** grafiek te openen de **metriek** blade klikt u op **waarschuwing toevoegen**, en geef vervolgens de informatie in de **een waarschuwingsregeltoevoegen** blade (**Resource** wordt automatisch ingesteld tot worden de toepassingen waarmee u werkt).</span><span class="sxs-lookup"><span data-stu-id="a0c13-231">Click the **Resource utilization** chart to open the **Metric** blade, click **Add alert**, and then fill out the information in the **Add an alert rule** blade (**Resource** is automatically set up to be the pool you're working with).</span></span>
2. <span data-ttu-id="a0c13-232">Typ een **naam** en **beschrijving** die de waarschuwing u en de ontvangers identificeert.</span><span class="sxs-lookup"><span data-stu-id="a0c13-232">Type a **Name** and **Description** that identifies the alert to you and the recipients.</span></span>
3. <span data-ttu-id="a0c13-233">Kies een **metriek** die u wilt een waarschuwing in de lijst.</span><span class="sxs-lookup"><span data-stu-id="a0c13-233">Choose a **Metric** that you want to alert from the list.</span></span>

    <span data-ttu-id="a0c13-234">De grafiek wordt dynamisch Resourcegebruik voor deze metriek bij het kiezen van een drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="a0c13-234">The chart dynamically shows resource utilization for that metric to help you choose a threshold.</span></span>

4. <span data-ttu-id="a0c13-235">Kies een **voorwaarde** (groter dan maximaal, enzovoort) en een **drempelwaarde**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="a0c13-236">Kies een **periode** tijdsperiode waarin de meetwaarde regel moet worden voldaan voordat de waarschuwing triggers.</span><span class="sxs-lookup"><span data-stu-id="a0c13-236">Choose a **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span>
6. <span data-ttu-id="a0c13-237">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-237">Click **OK**.</span></span>

<span data-ttu-id="a0c13-238">Zie voor meer informatie [waarschuwingen van de SQL-Database maken in Azure portal](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a0c13-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="a0c13-239">Een database verplaatsen naar een elastische pool</span><span class="sxs-lookup"><span data-stu-id="a0c13-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="a0c13-240">U kunt toevoegen of verwijderen van databases uit een bestaande groep.</span><span class="sxs-lookup"><span data-stu-id="a0c13-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="a0c13-241">De databases kunnen zich in andere toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-241">The databases can be in other pools.</span></span> <span data-ttu-id="a0c13-242">U kunt echter alleen databases die zich op dezelfde logische server toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-242">However, you can only add databases that are on the same logical server.</span></span>

1. <span data-ttu-id="a0c13-243">In de blade voor de groep, onder **elastische databases** klikt u op **pool configureren**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-243">In the blade for the pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Klik op pool configureren][1]

2. <span data-ttu-id="a0c13-245">In de **pool configureren** blade, klikt u op **toevoegen aan groep**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-245">In the **Configure pool** blade, click **Add to pool**.</span></span>

    ![Klik op toevoegen aan groep](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="a0c13-247">In de **databases toevoegen** blade, selecteer de database of databases toevoegen aan de groep.</span><span class="sxs-lookup"><span data-stu-id="a0c13-247">In the **Add databases** blade, select the database or databases to add to the pool.</span></span> <span data-ttu-id="a0c13-248">Klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-248">Then click **Select**.</span></span>

    ![Selecteer de databases toevoegen](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="a0c13-250">De **pool configureren** blade bevat nu de database die u hebt geselecteerd om te worden toegevoegd, klikt u met de status ingesteld op **in behandeling**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-250">The **Configure pool** blade now lists the database you selected to be added, with its status set to **Pending**.</span></span>

    ![In behandeling pool-toevoegingen](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="a0c13-252">In de **blade van de pool configureren**, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-252">In the **Configure pool blade**, click **Save**.</span></span>

    ![Op Opslaan klikken](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="a0c13-254">Een database verplaatst buiten een elastische pool</span><span class="sxs-lookup"><span data-stu-id="a0c13-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="a0c13-255">In de **pool configureren** blade, selecteer de database of databases verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-255">In the **Configure pool** blade, select the database or databases to remove.</span></span>

    ![databases weergeven](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="a0c13-257">Klik op **verwijderen uit groep**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-257">Click **Remove from pool**.</span></span>

    ![databases weergeven](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="a0c13-259">De **pool configureren** blade bevat nu de database die u hebt geselecteerd om te worden verwijderd met de status ingesteld op **in behandeling**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-259">The **Configure pool** blade now lists the database you selected to be removed with its status set to **Pending**.</span></span>

    ![voorbeeld database toevoegen en verwijderen](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="a0c13-261">In de **blade van de pool configureren**, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a0c13-261">In the **Configure pool blade**, click **Save**.</span></span>

    ![Op Opslaan klikken](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="a0c13-263">Instellingen van de prestaties van een elastische groep wijzigen</span><span class="sxs-lookup"><span data-stu-id="a0c13-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="a0c13-264">Als u het Resourcegebruik van een elastische pool bewaken, ontdekt u dat bepaalde aanpassingen nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="a0c13-264">As you monitor the resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="a0c13-265">De groep moet mogelijk een wijziging in de limieten van de prestaties of de opslag.</span><span class="sxs-lookup"><span data-stu-id="a0c13-265">Maybe the pool needs a change in the performance or storage limits.</span></span> <span data-ttu-id="a0c13-266">Mogelijk wilt u de database-instellingen in de groep wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-266">Possibly you want to change the database settings in the pool.</span></span> <span data-ttu-id="a0c13-267">U kunt de installatie van de groep wijzigen op elk gewenst moment om op te halen van de beste balans van prestaties en kosten.</span><span class="sxs-lookup"><span data-stu-id="a0c13-267">You can change the setup of the pool at any time to get the best balance of performance and cost.</span></span> <span data-ttu-id="a0c13-268">Zie [wanneer moet een elastische pool worden gebruikt?](sql-database-elastic-pool.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a0c13-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="a0c13-269">De limieten voor edtu's of opslag per groep en edtu's per database wijzigen:</span><span class="sxs-lookup"><span data-stu-id="a0c13-269">To change the eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="a0c13-270">Open de **pool configureren** blade.</span><span class="sxs-lookup"><span data-stu-id="a0c13-270">Open the **Configure pool** blade.</span></span>

    <span data-ttu-id="a0c13-271">Onder **elastische groepsinstellingen**, gebruik de schuifregelaar voor de Groepsinstellingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a0c13-271">Under **elastic pool settings**, use either slider to change the pool settings.</span></span>

    ![Resourcegebruik van de elastische groep](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="a0c13-273">Wanneer de instelling wordt gewijzigd, worden de weergave de geschatte maandelijkse kosten van de wijziging.</span><span class="sxs-lookup"><span data-stu-id="a0c13-273">When the setting changes, the display shows the estimated monthly cost of the change.</span></span>

    ![Bijwerken van een elastische pool en nieuwe maandelijkse kosten](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="a0c13-275">Latentie van bewerkingen van de elastische groep</span><span class="sxs-lookup"><span data-stu-id="a0c13-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="a0c13-276">Doorgaans wijzigen van de edtu min's per database of max edtu's per database is voltooid in de 5 minuten of minder.</span><span class="sxs-lookup"><span data-stu-id="a0c13-276">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="a0c13-277">Het wijzigen van de edtu's per groep, is afhankelijk van de totale hoeveelheid ruimte die wordt gebruikt door alle databases in de groep.</span><span class="sxs-lookup"><span data-stu-id="a0c13-277">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="a0c13-278">Wijzigingen duren gemiddeld 90 minuten of minder per 100 GB.</span><span class="sxs-lookup"><span data-stu-id="a0c13-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="a0c13-279">Bijvoorbeeld, als de totale ruimte gebruikt door alle databases in de pool is 200 GB, dan is de verwachte latentie voor het wijzigen van de groeps-eDTU per pool drie uur of minder.</span><span class="sxs-lookup"><span data-stu-id="a0c13-279">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0c13-280">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a0c13-280">Next steps</span></span>

- <span data-ttu-id="a0c13-281">Om te begrijpen wat een elastische groep is, Zie [elastische pool in SQL-Database](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="a0c13-281">To understand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="a0c13-282">Zie voor instructies over het gebruik van elastische pools [prijs- en Prestatieoverwegingen voor elastische pools](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="a0c13-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="a0c13-283">Zie voor het gebruik van elastische taken Transact-SQL-scripts uitvoeren op een willekeurig aantal databases in de pool, [elastische taken overzicht](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0c13-283">To use elastic jobs to run Transact-SQL scripts against any number of databases in the pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="a0c13-284">Om te vragen via een willekeurig aantal databases in de groep, Zie [elastische query overzicht](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0c13-284">To query across any number of databases in the pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="a0c13-285">Zie voor transacties een willekeurig aantal databases in de pool [elastische transacties](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0c13-285">For transactions any number of databases in the pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


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
