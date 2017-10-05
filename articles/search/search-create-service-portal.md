---
title: Maak een Azure Search-service in de portal | Microsoft Docs
description: Inrichten van een Azure Search-service in de portal.
services: search
manager: jhubbard
author: HeidiSteen
documentationcenter: 
ms.assetid: c8c88922-69aa-4099-b817-60f7b54e62df
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 58f4eab190e40e16ed261c165ffdfc8155eeb434
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-search-service-in-the-portal"></a><span data-ttu-id="8a413-103">Maak een Azure Search-service in de portal</span><span class="sxs-lookup"><span data-stu-id="8a413-103">Create an Azure Search service in the portal</span></span>

<span data-ttu-id="8a413-104">In dit artikel wordt uitgelegd hoe maken of een Azure Search-service in de portal inrichten.</span><span class="sxs-lookup"><span data-stu-id="8a413-104">This article explains how to create or provision an Azure Search service in the portal.</span></span> <span data-ttu-id="8a413-105">Zie voor instructies PowerShell [Azure Search beheren met PowerShell](search-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8a413-105">For PowerShell instructions, see [Manage Azure Search with PowerShell](search-manage-powershell.md).</span></span>

## <a name="subscribe-free-or-paid"></a><span data-ttu-id="8a413-106">Abonneren (gratis of betaalde)</span><span class="sxs-lookup"><span data-stu-id="8a413-106">Subscribe (free or paid)</span></span>

<span data-ttu-id="8a413-107">[Een gratis Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) en gratis tegoed gebruiken om uit te proberen betaalde Azure-services.</span><span class="sxs-lookup"><span data-stu-id="8a413-107">[Open a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) and use free credits to try out paid Azure services.</span></span> <span data-ttu-id="8a413-108">Nadat het tegoed is gebruikt, wordt het account houden en blijven gratis Azure-services, zoals Websites gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8a413-108">After credits are used up, keep the account and continue to use free Azure services, such as Websites.</span></span> <span data-ttu-id="8a413-109">Uw creditcard is nooit in rekening gebracht tenzij u expliciet de instellingen wijzigen en vragen kunnen worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="8a413-109">Your credit card is never charged unless you explicitly change your settings and ask to be charged.</span></span>

<span data-ttu-id="8a413-110">U kunt ook [voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="8a413-110">Alternatively, [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="8a413-111">Een MSDN-abonnement ontvangt u elke maand tegoeden die kunt u voor betaalde Azure-services.</span><span class="sxs-lookup"><span data-stu-id="8a413-111">An MSDN subscription gives you credits every month you can use for paid Azure services.</span></span> 

## <a name="find-azure-search"></a><span data-ttu-id="8a413-112">Zoeken naar Azure Search</span><span class="sxs-lookup"><span data-stu-id="8a413-112">Find Azure Search</span></span>
1. <span data-ttu-id="8a413-113">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8a413-113">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8a413-114">Klik op het plusteken ('+') in de linkerbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="8a413-114">Click the plus sign ("+") in the top left corner.</span></span>
3. <span data-ttu-id="8a413-115">Selecteer **Web en mobiel** > **Azure Search**.</span><span class="sxs-lookup"><span data-stu-id="8a413-115">Select **Web + Mobile** > **Azure Search**.</span></span>

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-the-service-and-url-endpoint"></a><span data-ttu-id="8a413-116">Naam van de service en de URL-eindpunt</span><span class="sxs-lookup"><span data-stu-id="8a413-116">Name the service and URL endpoint</span></span>

<span data-ttu-id="8a413-117">Naam van een service maakt deel uit van het URL-eindpunt op basis waarvan de API-aanroepen zijn uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="8a413-117">A service name is part of the URL endpoint against which API calls are issued.</span></span> <span data-ttu-id="8a413-118">Typ de servicenaam van uw in de **URL** veld.</span><span class="sxs-lookup"><span data-stu-id="8a413-118">Type your service name in the **URL** field.</span></span> 

<span data-ttu-id="8a413-119">Vereisten voor service-naam:</span><span class="sxs-lookup"><span data-stu-id="8a413-119">Service name requirements:</span></span>
   * <span data-ttu-id="8a413-120">2 en 60 tekens lang zijn</span><span class="sxs-lookup"><span data-stu-id="8a413-120">2 and 60 characters in length</span></span>
   * <span data-ttu-id="8a413-121">kleine letters, getallen of streepjes ('-')</span><span class="sxs-lookup"><span data-stu-id="8a413-121">lowercase letters, digits, or dashes ("-")</span></span>
   * <span data-ttu-id="8a413-122">Er is geen streepje ('-') als de eerste 2 tekens of laatste teken</span><span class="sxs-lookup"><span data-stu-id="8a413-122">no dash ("-") as the first 2 characters or last single character</span></span>
   * <span data-ttu-id="8a413-123">Er zijn geen twee opeenvolgende streepjes ('--')</span><span class="sxs-lookup"><span data-stu-id="8a413-123">no consecutive dashes ("--")</span></span>

## <a name="select-a-subscription"></a><span data-ttu-id="8a413-124">Een abonnement selecteren</span><span class="sxs-lookup"><span data-stu-id="8a413-124">Select a subscription</span></span>
<span data-ttu-id="8a413-125">Als u meer dan één abonnement hebt, kiest u dat ook gegevens of file storage-services heeft.</span><span class="sxs-lookup"><span data-stu-id="8a413-125">If you have more than one subscription, choose one that also has data or file storage services.</span></span> <span data-ttu-id="8a413-126">Azure Search kunt automatische detectie Azure Table- en Blob-opslag, SQL-Database en Azure Cosmos DB voor indexeren *indexeerfuncties*, maar alleen voor services in hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="8a413-126">Azure Search can auto-detect Azure Table and Blob storage, SQL Database, and Azure Cosmos DB for indexing via *indexers*, but only for services in the same subscription.</span></span>

## <a name="select-a-resource-group"></a><span data-ttu-id="8a413-127">Een resourcegroep selecteren</span><span class="sxs-lookup"><span data-stu-id="8a413-127">Select a resource group</span></span>
<span data-ttu-id="8a413-128">Een resourcegroep is een verzameling Azure-services en bronnen die samen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8a413-128">A resource group is a collection of Azure services and resources used together.</span></span> <span data-ttu-id="8a413-129">Bijvoorbeeld, als u van Azure Search gebruikmaakt index van een SQL-database, moeten klikt u vervolgens beide services deel uitmaken van dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8a413-129">For example, if you are using Azure Search to index a SQL database, then both services should be part of the same resource group.</span></span>

> [!TIP]
> <span data-ttu-id="8a413-130">Verwijderen van een resourcegroep, verwijdert tevens de services in het.</span><span class="sxs-lookup"><span data-stu-id="8a413-130">Deleting a resource group also deletes the services within it.</span></span> <span data-ttu-id="8a413-131">Prototype projecten met gebruik van meerdere services, gemakkelijker als ze allemaal in dezelfde resourcegroep opschoning nadat het project voltooid is.</span><span class="sxs-lookup"><span data-stu-id="8a413-131">For prototype projects utilizing multiple services, putting all of them in the same resource group makes cleanup easier after the project is over.</span></span> 

## <a name="select-a-hosting-location"></a><span data-ttu-id="8a413-132">Selecteer een hosting-locatie</span><span class="sxs-lookup"><span data-stu-id="8a413-132">Select a hosting location</span></span> 
<span data-ttu-id="8a413-133">Als een Azure-service kan de Azure Search in datacenters over de hele wereld worden gehost.</span><span class="sxs-lookup"><span data-stu-id="8a413-133">As an Azure service, Azure Search can be hosted in datacenters around the world.</span></span> <span data-ttu-id="8a413-134">Houd er rekening mee dat [prijzen kunnen verschillen](https://azure.microsoft.com/pricing/details/search/) per Geografie.</span><span class="sxs-lookup"><span data-stu-id="8a413-134">Note that [prices can differ](https://azure.microsoft.com/pricing/details/search/) by geography.</span></span>

## <a name="select-a-pricing-tier-sku"></a><span data-ttu-id="8a413-135">Selecteer een prijscategorie (SKU)</span><span class="sxs-lookup"><span data-stu-id="8a413-135">Select a pricing tier (SKU)</span></span>
<span data-ttu-id="8a413-136">[Azure Search momenteel wordt aangeboden in meerdere Prijscategorieën](https://azure.microsoft.com/pricing/details/search/): gratis, basis of standaard.</span><span class="sxs-lookup"><span data-stu-id="8a413-136">[Azure Search is currently offered in multiple pricing tiers](https://azure.microsoft.com/pricing/details/search/): Free, Basic, or Standard.</span></span> <span data-ttu-id="8a413-137">Elke laag heeft zijn eigen [capaciteit en limieten](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="8a413-137">Each tier has its own [capacity and limits](search-limits-quotas-capacity.md).</span></span> <span data-ttu-id="8a413-138">Zie [Kies een prijscategorie laag of SKU](search-sku-tier.md) voor hulp.</span><span class="sxs-lookup"><span data-stu-id="8a413-138">See [Choose a pricing tier or SKU](search-sku-tier.md) for guidance.</span></span>

<span data-ttu-id="8a413-139">In dit overzicht hebben we de prijscategorie Standard gekozen voor onze service.</span><span class="sxs-lookup"><span data-stu-id="8a413-139">In this walkthrough, we have chosen the Standard tier for our service.</span></span>

## <a name="create-your-service"></a><span data-ttu-id="8a413-140">Uw service maken</span><span class="sxs-lookup"><span data-stu-id="8a413-140">Create your service</span></span>

<span data-ttu-id="8a413-141">Vergeet niet om uw service aan het dashboard voor gemakkelijke toegang vast wanneer u zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="8a413-141">Remember to pin your service to the dashboard for easy access whenever you sign in.</span></span>

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a><span data-ttu-id="8a413-142">Schalen van uw service</span><span class="sxs-lookup"><span data-stu-id="8a413-142">Scale your service</span></span>
<span data-ttu-id="8a413-143">Het kan even duren om een service (15 minuten of langer, afhankelijk van de laag) te maken.</span><span class="sxs-lookup"><span data-stu-id="8a413-143">It can take a few minutes to create a service (15 minutes or more depending on the tier).</span></span> <span data-ttu-id="8a413-144">Nadat de service is geconfigureerd, kunt u schalen om te voldoen aan uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="8a413-144">After your service is provisioned, you can scale it to meet your needs.</span></span> <span data-ttu-id="8a413-145">Omdat u de prijscategorie Standard voor uw Azure Search-service hebt gekozen, kunt u uw service schalen in twee dimensies: replica's en partities.</span><span class="sxs-lookup"><span data-stu-id="8a413-145">Because you chose the Standard tier for your Azure Search service, you can scale your service in two dimensions: replicas and partitions.</span></span> <span data-ttu-id="8a413-146">Had u de basisstaffel gekozen, kunt u alleen toevoegen replica's.</span><span class="sxs-lookup"><span data-stu-id="8a413-146">Had you chosen the Basic tier, you can only add replicas.</span></span> <span data-ttu-id="8a413-147">Als u de gratis service hebt ingericht, is scale niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="8a413-147">If you provisioned the free service, scale is not available.</span></span>

<span data-ttu-id="8a413-148">***Partities*** zodat uw service voor het opslaan en doorzoeken meer documenten.</span><span class="sxs-lookup"><span data-stu-id="8a413-148">***Partitions*** allow your service to store and search through more documents.</span></span>

<span data-ttu-id="8a413-149">***Replica's*** zodat uw service voor het afhandelen van een hogere belasting van de zoekquery's.</span><span class="sxs-lookup"><span data-stu-id="8a413-149">***Replicas*** allow your service to handle a higher load of search queries.</span></span>

> [!Important]
> <span data-ttu-id="8a413-150">Een service moet hebben [2 replica's voor alleen-lezen-SLA en 3 replica's voor lezen/schrijven SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span><span class="sxs-lookup"><span data-stu-id="8a413-150">A service must have [2 replicas for read-only SLA and 3 replicas for read/write SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

1. <span data-ttu-id="8a413-151">Ga naar de blade van het zoeken in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8a413-151">Go to your search service blade in the Azure portal.</span></span>
2. <span data-ttu-id="8a413-152">Selecteer in het deelvenster navigatie aan de linkerkant **instellingen** > **Scale**.</span><span class="sxs-lookup"><span data-stu-id="8a413-152">In the left-navigation pane, select **Settings** > **Scale**.</span></span>
3. <span data-ttu-id="8a413-153">Gebruik de slidebar replica's of partities toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="8a413-153">Use the slidebar to add Replicas or Partitions.</span></span>

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> <span data-ttu-id="8a413-154">Elke laag zijn verschillende [limieten](search-limits-quotas-capacity.md) op het totale aantal Search-eenheden die zijn toegestaan in een enkele service (replica's * partities totaal aantal Search-eenheden =).</span><span class="sxs-lookup"><span data-stu-id="8a413-154">Each tier has different [limits](search-limits-quotas-capacity.md) on the total number of Search Units allowed in a single service (Replicas * Partitions = Total Search Units).</span></span>

## <a name="when-to-add-a-second-service"></a><span data-ttu-id="8a413-155">Wanneer een tweede service toevoegen</span><span class="sxs-lookup"><span data-stu-id="8a413-155">When to add a second service</span></span>

<span data-ttu-id="8a413-156">Een grote meerderheid van klanten gebruik slechts één service ingericht op een laag met de [rechtermuisknop saldo van resources](search-sku-tier.md).</span><span class="sxs-lookup"><span data-stu-id="8a413-156">A large majority of customers use just one service provisioned at a tier that provides the [right balance of resources](search-sku-tier.md).</span></span> <span data-ttu-id="8a413-157">Een service kan meerdere indexen hosten onderworpen aan de [maximaal limieten van de laag die u selecteert](search-capacity-planning.md), met elke geïsoleerd van een andere index.</span><span class="sxs-lookup"><span data-stu-id="8a413-157">One service can host multiple indexes, subject to the [maximum limits of the tier you select](search-capacity-planning.md), with each index isolated from another.</span></span> <span data-ttu-id="8a413-158">In Azure Search kunnen alleen aanvragen worden omgeleid naar een index, minimaliseert de kans op per ongeluk of opzettelijk gegevens ophalen uit andere indexen in dezelfde service.</span><span class="sxs-lookup"><span data-stu-id="8a413-158">In Azure Search, requests can only be directed to one index, minimizing the chance of accidental or intentional data retrieval from other indexes in the same service.</span></span>

<span data-ttu-id="8a413-159">Hoewel de meeste klanten slechts één service gebruikt, is het mogelijk dat service redundantie nodig als de volgende operationele vereisten gelden:</span><span class="sxs-lookup"><span data-stu-id="8a413-159">Although most customers use just one service, service redundancy might be necessary if operational requirements include the following:</span></span>

+ <span data-ttu-id="8a413-160">Herstel na noodgevallen (onderbreking datacentrum).</span><span class="sxs-lookup"><span data-stu-id="8a413-160">Disaster recovery (data center outage).</span></span> <span data-ttu-id="8a413-161">Azure Search biedt geen chatberichten failover in geval van een storing.</span><span class="sxs-lookup"><span data-stu-id="8a413-161">Azure Search does not provide instant failover in the event of an outage.</span></span> <span data-ttu-id="8a413-162">Zie voor aanbevelingen en richtlijnen [Service-beheer](search-manage.md).</span><span class="sxs-lookup"><span data-stu-id="8a413-162">For recommendations and guidance, see [Service administration](search-manage.md).</span></span>
+ <span data-ttu-id="8a413-163">Uw onderzoek van multi-tenancymodus modellering heeft vastgesteld dat extra services het ontwerp van de optimale is.</span><span class="sxs-lookup"><span data-stu-id="8a413-163">Your investigation of multi-tenancy modeling has determined that additional services is the optimal design.</span></span> <span data-ttu-id="8a413-164">Zie voor meer informatie [ontwerp voor multi-tenancy](search-modeling-multitenant-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="8a413-164">For more information, see [Design for multi-tenancy](search-modeling-multitenant-saas-applications.md).</span></span>
+ <span data-ttu-id="8a413-165">Voor globaal geïmplementeerde toepassingen mogelijk een exemplaar van Azure Search in meerdere regio's te minimaliseren latentie van de internationale verkeer van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="8a413-165">For globally deployed applications, you might require an instance of Azure Search in multiple regions to minimize latency of your application’s international traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="8a413-166">In Azure Search kan niet u werkbelastingen voor indexering en opvragen; scheiden Zo maakt u meerdere services voor gescheiden werkbelastingen nooit.</span><span class="sxs-lookup"><span data-stu-id="8a413-166">In Azure Search, you cannot segregate indexing and querying workloads; thus, you would never create multiple services for segregated workloads.</span></span> <span data-ttu-id="8a413-167">Een index is altijd een query uitgevoerd op de service waarin het is gemaakt (u kunt geen een index in een service maken of kopiëren naar een andere).</span><span class="sxs-lookup"><span data-stu-id="8a413-167">An index is always queried on the service in which it was created (you cannot create an index in one service and copy it to another).</span></span>
>

<span data-ttu-id="8a413-168">Een tweede service is niet vereist voor hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="8a413-168">A second service is not required for high availability.</span></span> <span data-ttu-id="8a413-169">Hoge beschikbaarheid voor query's wordt bereikt wanneer u 2 of meer replica's in dezelfde service.</span><span class="sxs-lookup"><span data-stu-id="8a413-169">High availability for queries is achieved when you use 2 or more replicas in the same service.</span></span> <span data-ttu-id="8a413-170">Replica-updates zijn sequentiële, ten minste één operationeel is wanneer een service-update is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8a413-170">Replica updates are sequential, which means at least one is operational when a service update is rolled out.</span></span> <span data-ttu-id="8a413-171">Zie voor meer informatie over bedrijfstijd [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span><span class="sxs-lookup"><span data-stu-id="8a413-171">For more information about uptime, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a413-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a413-172">Next steps</span></span>
<span data-ttu-id="8a413-173">Na het inrichten van een Azure Search-service, bent u klaar om [een index definiëren](search-what-is-an-index.md) zodat u kunt uploaden en uw gegevens te zoeken.</span><span class="sxs-lookup"><span data-stu-id="8a413-173">After provisioning an Azure Search service, you are ready to [define an index](search-what-is-an-index.md) so you can upload and search your data.</span></span>

<span data-ttu-id="8a413-174">Voor toegang tot de service via code of script, en geef de URL (*servicenaam*. search.windows.net) en een sleutel.</span><span class="sxs-lookup"><span data-stu-id="8a413-174">To access the service from code or script, provide the URL (*service-name*.search.windows.net) and a key.</span></span> <span data-ttu-id="8a413-175">Beheersleutels bieden volledige toegang. querysleutels verlenen alleen-lezen toegang.</span><span class="sxs-lookup"><span data-stu-id="8a413-175">Admin keys grant full access; query keys grant read-only access.</span></span> <span data-ttu-id="8a413-176">Zie [het gebruik van Azure Search in .NET](search-howto-dotnet-sdk.md) aan de slag.</span><span class="sxs-lookup"><span data-stu-id="8a413-176">See [How to use Azure Search in .NET](search-howto-dotnet-sdk.md) to get started.</span></span>

<span data-ttu-id="8a413-177">Zie [bouwen en query uitvoeren op uw eerste index](search-get-started-portal.md) voor een snelle zelfstudie op basis van de portal.</span><span class="sxs-lookup"><span data-stu-id="8a413-177">See [Build and query your first index](search-get-started-portal.md) for a quick portal-based tutorial.</span></span>

