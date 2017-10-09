---
title: een Azure Search-service in de portal Hallo aaaCreate | Microsoft Docs
description: Een Azure Search-service in de portal Hallo inrichten.
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
ms.openlocfilehash: f1c7197a1467e32bd4b360b165c9059e6bb0e496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-service-in-hello-portal"></a><span data-ttu-id="9af52-103">Maken van een Azure Search-service in Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="9af52-103">Create an Azure Search service in hello portal</span></span>

<span data-ttu-id="9af52-104">Dit artikel wordt uitgelegd hoe toocreate of het inrichten een Azure Search-service in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="9af52-104">This article explains how toocreate or provision an Azure Search service in hello portal.</span></span> <span data-ttu-id="9af52-105">Zie voor instructies PowerShell [Azure Search beheren met PowerShell](search-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9af52-105">For PowerShell instructions, see [Manage Azure Search with PowerShell](search-manage-powershell.md).</span></span>

## <a name="subscribe-free-or-paid"></a><span data-ttu-id="9af52-106">Abonneren (gratis of betaalde)</span><span class="sxs-lookup"><span data-stu-id="9af52-106">Subscribe (free or paid)</span></span>

<span data-ttu-id="9af52-107">[Een gratis Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) en gebruik gratis tegoed tootry uit betaalde Azure-services.</span><span class="sxs-lookup"><span data-stu-id="9af52-107">[Open a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) and use free credits tootry out paid Azure services.</span></span> <span data-ttu-id="9af52-108">Nadat het tegoed is gebruikt, Hallo account houden en toouse gratis Azure-services, zoals Websites worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="9af52-108">After credits are used up, keep hello account and continue toouse free Azure services, such as Websites.</span></span> <span data-ttu-id="9af52-109">Uw creditcard is nooit in rekening gebracht tenzij u expliciet de instellingen wijzigen en vraag toobe in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="9af52-109">Your credit card is never charged unless you explicitly change your settings and ask toobe charged.</span></span>

<span data-ttu-id="9af52-110">U kunt ook [voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="9af52-110">Alternatively, [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="9af52-111">Een MSDN-abonnement ontvangt u elke maand tegoeden die kunt u voor betaalde Azure-services.</span><span class="sxs-lookup"><span data-stu-id="9af52-111">An MSDN subscription gives you credits every month you can use for paid Azure services.</span></span> 

## <a name="find-azure-search"></a><span data-ttu-id="9af52-112">Zoeken naar Azure Search</span><span class="sxs-lookup"><span data-stu-id="9af52-112">Find Azure Search</span></span>
1. <span data-ttu-id="9af52-113">Meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9af52-113">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9af52-114">Klik op Hallo plus -teken ('+') in de linkerbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="9af52-114">Click hello plus sign ("+") in hello top left corner.</span></span>
3. <span data-ttu-id="9af52-115">Selecteer **Web en mobiel** > **Azure Search**.</span><span class="sxs-lookup"><span data-stu-id="9af52-115">Select **Web + Mobile** > **Azure Search**.</span></span>

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-hello-service-and-url-endpoint"></a><span data-ttu-id="9af52-116">Naam Hallo-service en de URL-eindpunt</span><span class="sxs-lookup"><span data-stu-id="9af52-116">Name hello service and URL endpoint</span></span>

<span data-ttu-id="9af52-117">Naam van een service maakt deel uit van Hallo URL-eindpunt op basis waarvan de API-aanroepen zijn uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="9af52-117">A service name is part of hello URL endpoint against which API calls are issued.</span></span> <span data-ttu-id="9af52-118">Typ de servicenaam van uw in Hallo **URL** veld.</span><span class="sxs-lookup"><span data-stu-id="9af52-118">Type your service name in hello **URL** field.</span></span> 

<span data-ttu-id="9af52-119">Vereisten voor service-naam:</span><span class="sxs-lookup"><span data-stu-id="9af52-119">Service name requirements:</span></span>
   * <span data-ttu-id="9af52-120">2 en 60 tekens lang zijn</span><span class="sxs-lookup"><span data-stu-id="9af52-120">2 and 60 characters in length</span></span>
   * <span data-ttu-id="9af52-121">kleine letters, getallen of streepjes ('-')</span><span class="sxs-lookup"><span data-stu-id="9af52-121">lowercase letters, digits, or dashes ("-")</span></span>
   * <span data-ttu-id="9af52-122">Er is geen streepje ('-') als Hallo eerst 2 tekens of laatste teken</span><span class="sxs-lookup"><span data-stu-id="9af52-122">no dash ("-") as hello first 2 characters or last single character</span></span>
   * <span data-ttu-id="9af52-123">Er zijn geen twee opeenvolgende streepjes ('--')</span><span class="sxs-lookup"><span data-stu-id="9af52-123">no consecutive dashes ("--")</span></span>

## <a name="select-a-subscription"></a><span data-ttu-id="9af52-124">Een abonnement selecteren</span><span class="sxs-lookup"><span data-stu-id="9af52-124">Select a subscription</span></span>
<span data-ttu-id="9af52-125">Als u meer dan één abonnement hebt, kiest u dat ook gegevens of file storage-services heeft.</span><span class="sxs-lookup"><span data-stu-id="9af52-125">If you have more than one subscription, choose one that also has data or file storage services.</span></span> <span data-ttu-id="9af52-126">Azure Search kunt automatische detectie Azure Table- en Blob-opslag, SQL-Database en Azure Cosmos DB voor indexeren *indexeerfuncties*, maar alleen voor services in Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="9af52-126">Azure Search can auto-detect Azure Table and Blob storage, SQL Database, and Azure Cosmos DB for indexing via *indexers*, but only for services in hello same subscription.</span></span>

## <a name="select-a-resource-group"></a><span data-ttu-id="9af52-127">Een resourcegroep selecteren</span><span class="sxs-lookup"><span data-stu-id="9af52-127">Select a resource group</span></span>
<span data-ttu-id="9af52-128">Een resourcegroep is een verzameling Azure-services en bronnen die samen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9af52-128">A resource group is a collection of Azure services and resources used together.</span></span> <span data-ttu-id="9af52-129">Bijvoorbeeld, als u van Azure Search tooindex een SQL-database gebruikmaakt, klikt u vervolgens beide services moeten deel uitmaken van Hallo dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="9af52-129">For example, if you are using Azure Search tooindex a SQL database, then both services should be part of hello same resource group.</span></span>

> [!TIP]
> <span data-ttu-id="9af52-130">Verwijderen van een resourcegroep verwijderd Hallo services binnen deze ook.</span><span class="sxs-lookup"><span data-stu-id="9af52-130">Deleting a resource group also deletes hello services within it.</span></span> <span data-ttu-id="9af52-131">Voor prototype projecten met behulp van meerdere services, zodat ze allemaal Hallo gemakkelijker dezelfde resourcegroep opschoning nadat het Hallo-project is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9af52-131">For prototype projects utilizing multiple services, putting all of them in hello same resource group makes cleanup easier after hello project is over.</span></span> 

## <a name="select-a-hosting-location"></a><span data-ttu-id="9af52-132">Selecteer een hosting-locatie</span><span class="sxs-lookup"><span data-stu-id="9af52-132">Select a hosting location</span></span> 
<span data-ttu-id="9af52-133">Als een Azure-service kan de Azure Search in datacenters Hallo wereld worden gehost.</span><span class="sxs-lookup"><span data-stu-id="9af52-133">As an Azure service, Azure Search can be hosted in datacenters around hello world.</span></span> <span data-ttu-id="9af52-134">Houd er rekening mee dat [prijzen kunnen verschillen](https://azure.microsoft.com/pricing/details/search/) per Geografie.</span><span class="sxs-lookup"><span data-stu-id="9af52-134">Note that [prices can differ](https://azure.microsoft.com/pricing/details/search/) by geography.</span></span>

## <a name="select-a-pricing-tier-sku"></a><span data-ttu-id="9af52-135">Selecteer een prijscategorie (SKU)</span><span class="sxs-lookup"><span data-stu-id="9af52-135">Select a pricing tier (SKU)</span></span>
<span data-ttu-id="9af52-136">[Azure Search momenteel wordt aangeboden in meerdere Prijscategorieën](https://azure.microsoft.com/pricing/details/search/): gratis, basis of standaard.</span><span class="sxs-lookup"><span data-stu-id="9af52-136">[Azure Search is currently offered in multiple pricing tiers](https://azure.microsoft.com/pricing/details/search/): Free, Basic, or Standard.</span></span> <span data-ttu-id="9af52-137">Elke laag heeft zijn eigen [capaciteit en limieten](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="9af52-137">Each tier has its own [capacity and limits](search-limits-quotas-capacity.md).</span></span> <span data-ttu-id="9af52-138">Zie [Kies een prijscategorie laag of SKU](search-sku-tier.md) voor hulp.</span><span class="sxs-lookup"><span data-stu-id="9af52-138">See [Choose a pricing tier or SKU](search-sku-tier.md) for guidance.</span></span>

<span data-ttu-id="9af52-139">In dit overzicht hebben we Hallo standaardcategorie gekozen voor onze service.</span><span class="sxs-lookup"><span data-stu-id="9af52-139">In this walkthrough, we have chosen hello Standard tier for our service.</span></span>

## <a name="create-your-service"></a><span data-ttu-id="9af52-140">Uw service maken</span><span class="sxs-lookup"><span data-stu-id="9af52-140">Create your service</span></span>

<span data-ttu-id="9af52-141">Houd er rekening mee toopin uw dashboard service toohello voor eenvoudige toegang wanneer u zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="9af52-141">Remember toopin your service toohello dashboard for easy access whenever you sign in.</span></span>

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a><span data-ttu-id="9af52-142">Schalen van uw service</span><span class="sxs-lookup"><span data-stu-id="9af52-142">Scale your service</span></span>
<span data-ttu-id="9af52-143">Het kan enkele minuten toocreate een service (15 minuten of langer, afhankelijk van het Hallo-laag) duren.</span><span class="sxs-lookup"><span data-stu-id="9af52-143">It can take a few minutes toocreate a service (15 minutes or more depending on hello tier).</span></span> <span data-ttu-id="9af52-144">Nadat de service is geconfigureerd, kunt u de schaal het toomeet uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="9af52-144">After your service is provisioned, you can scale it toomeet your needs.</span></span> <span data-ttu-id="9af52-145">Omdat u de standaardcategorie Hallo voor uw Azure Search-service kiest, kunt u uw service schalen in twee dimensies: replica's en partities.</span><span class="sxs-lookup"><span data-stu-id="9af52-145">Because you chose hello Standard tier for your Azure Search service, you can scale your service in two dimensions: replicas and partitions.</span></span> <span data-ttu-id="9af52-146">Had u Hallo basisstaffel gekozen, kunt u alleen toevoegen replica's.</span><span class="sxs-lookup"><span data-stu-id="9af52-146">Had you chosen hello Basic tier, you can only add replicas.</span></span> <span data-ttu-id="9af52-147">Als u de gratis service Hallo ingericht, is scale niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="9af52-147">If you provisioned hello free service, scale is not available.</span></span>

<span data-ttu-id="9af52-148">***Partities*** toestaan uw service toostore en zoek via meer documenten.</span><span class="sxs-lookup"><span data-stu-id="9af52-148">***Partitions*** allow your service toostore and search through more documents.</span></span>

<span data-ttu-id="9af52-149">***Replica's*** een hogere belasting van zoekopdrachten voor uw service toohandle toestaan.</span><span class="sxs-lookup"><span data-stu-id="9af52-149">***Replicas*** allow your service toohandle a higher load of search queries.</span></span>

> [!Important]
> <span data-ttu-id="9af52-150">Een service moet hebben [2 replica's voor alleen-lezen-SLA en 3 replica's voor lezen/schrijven SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span><span class="sxs-lookup"><span data-stu-id="9af52-150">A service must have [2 replicas for read-only SLA and 3 replicas for read/write SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

1. <span data-ttu-id="9af52-151">Ga tooyour search-service-blade in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9af52-151">Go tooyour search service blade in hello Azure portal.</span></span>
2. <span data-ttu-id="9af52-152">Selecteer in het deelvenster navigatie aan de linkerkant Hallo **instellingen** > **Scale**.</span><span class="sxs-lookup"><span data-stu-id="9af52-152">In hello left-navigation pane, select **Settings** > **Scale**.</span></span>
3. <span data-ttu-id="9af52-153">Hallo slidebar tooadd replica's of partities gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9af52-153">Use hello slidebar tooadd Replicas or Partitions.</span></span>

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> <span data-ttu-id="9af52-154">Elke laag zijn verschillende [limieten](search-limits-quotas-capacity.md) van totaal aantal Search-eenheden die zijn toegestaan in een enkele service hello (replica's * partities totaal aantal Search-eenheden =).</span><span class="sxs-lookup"><span data-stu-id="9af52-154">Each tier has different [limits](search-limits-quotas-capacity.md) on hello total number of Search Units allowed in a single service (Replicas * Partitions = Total Search Units).</span></span>

## <a name="when-tooadd-a-second-service"></a><span data-ttu-id="9af52-155">Wanneer een tweede service tooadd</span><span class="sxs-lookup"><span data-stu-id="9af52-155">When tooadd a second service</span></span>

<span data-ttu-id="9af52-156">Een grote meerderheid van klanten gebruik slechts één service ingericht op een laag die Hallo biedt [rechtermuisknop saldo van resources](search-sku-tier.md).</span><span class="sxs-lookup"><span data-stu-id="9af52-156">A large majority of customers use just one service provisioned at a tier that provides hello [right balance of resources](search-sku-tier.md).</span></span> <span data-ttu-id="9af52-157">Een service kunt hosten meerdere indexen, onderwerp toohello [Hallo laag die u selecteert deze limieten](search-capacity-planning.md), met elke geïsoleerd van een andere index.</span><span class="sxs-lookup"><span data-stu-id="9af52-157">One service can host multiple indexes, subject toohello [maximum limits of hello tier you select](search-capacity-planning.md), with each index isolated from another.</span></span> <span data-ttu-id="9af52-158">In Azure Search aanvragen kunnen slechts worden gerichte tooone index, minimaliseert de kans op Hallo van per ongeluk of opzettelijk gegevens ophalen van andere in Hallo dezelfde indexen service.</span><span class="sxs-lookup"><span data-stu-id="9af52-158">In Azure Search, requests can only be directed tooone index, minimizing hello chance of accidental or intentional data retrieval from other indexes in hello same service.</span></span>

<span data-ttu-id="9af52-159">Hoewel de meeste klanten slechts één service gebruikt, is het mogelijk dat service redundantie nodig als operationele vereisten Hallo volgende opnemen:</span><span class="sxs-lookup"><span data-stu-id="9af52-159">Although most customers use just one service, service redundancy might be necessary if operational requirements include hello following:</span></span>

+ <span data-ttu-id="9af52-160">Herstel na noodgevallen (onderbreking datacentrum).</span><span class="sxs-lookup"><span data-stu-id="9af52-160">Disaster recovery (data center outage).</span></span> <span data-ttu-id="9af52-161">Azure Search biedt geen chatberichten failover in Hallo-gebeurtenis van een storing.</span><span class="sxs-lookup"><span data-stu-id="9af52-161">Azure Search does not provide instant failover in hello event of an outage.</span></span> <span data-ttu-id="9af52-162">Zie voor aanbevelingen en richtlijnen [Service-beheer](search-manage.md).</span><span class="sxs-lookup"><span data-stu-id="9af52-162">For recommendations and guidance, see [Service administration](search-manage.md).</span></span>
+ <span data-ttu-id="9af52-163">Uw onderzoek van multi-tenancymodus modellering heeft vastgesteld dat extra services Hallo optimaal ontwerp.</span><span class="sxs-lookup"><span data-stu-id="9af52-163">Your investigation of multi-tenancy modeling has determined that additional services is hello optimal design.</span></span> <span data-ttu-id="9af52-164">Zie voor meer informatie [ontwerp voor multi-tenancy](search-modeling-multitenant-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="9af52-164">For more information, see [Design for multi-tenancy](search-modeling-multitenant-saas-applications.md).</span></span>
+ <span data-ttu-id="9af52-165">Voor globaal geïmplementeerde toepassingen mogelijk u een exemplaar van Azure Search in meerdere regio's toominimize latentie van de internationale verkeer van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="9af52-165">For globally deployed applications, you might require an instance of Azure Search in multiple regions toominimize latency of your application’s international traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="9af52-166">In Azure Search kan niet u werkbelastingen voor indexering en opvragen; scheiden Zo maakt u meerdere services voor gescheiden werkbelastingen nooit.</span><span class="sxs-lookup"><span data-stu-id="9af52-166">In Azure Search, you cannot segregate indexing and querying workloads; thus, you would never create multiple services for segregated workloads.</span></span> <span data-ttu-id="9af52-167">Een index is altijd opgevraagd op Hallo service waarin het is gemaakt (u kunt geen een index in een service maken of kopiëren tooanother).</span><span class="sxs-lookup"><span data-stu-id="9af52-167">An index is always queried on hello service in which it was created (you cannot create an index in one service and copy it tooanother).</span></span>
>

<span data-ttu-id="9af52-168">Een tweede service is niet vereist voor hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="9af52-168">A second service is not required for high availability.</span></span> <span data-ttu-id="9af52-169">Hoge beschikbaarheid voor query's wordt bereikt wanneer u 2 of meer replica's in dezelfde service Hallo.</span><span class="sxs-lookup"><span data-stu-id="9af52-169">High availability for queries is achieved when you use 2 or more replicas in hello same service.</span></span> <span data-ttu-id="9af52-170">Replica-updates zijn sequentiële, ten minste één operationeel is wanneer een service-update is geïmplementeerd. Zie voor meer informatie over bedrijfstijd [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span><span class="sxs-lookup"><span data-stu-id="9af52-170">Replica updates are sequential, which means at least one is operational when a service update is rolled out. For more information about uptime, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9af52-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9af52-171">Next steps</span></span>
<span data-ttu-id="9af52-172">Na het inrichten van een Azure Search-service, bent u klaar te[een index definiëren](search-what-is-an-index.md) zodat u kunt uploaden en uw gegevens te zoeken.</span><span class="sxs-lookup"><span data-stu-id="9af52-172">After provisioning an Azure Search service, you are ready too[define an index](search-what-is-an-index.md) so you can upload and search your data.</span></span>

<span data-ttu-id="9af52-173">Hallo-service van code of het script tooaccess Hallo-URL opgeven (*servicenaam*. search.windows.net) en een sleutel.</span><span class="sxs-lookup"><span data-stu-id="9af52-173">tooaccess hello service from code or script, provide hello URL (*service-name*.search.windows.net) and a key.</span></span> <span data-ttu-id="9af52-174">Beheersleutels bieden volledige toegang. querysleutels verlenen alleen-lezen toegang.</span><span class="sxs-lookup"><span data-stu-id="9af52-174">Admin keys grant full access; query keys grant read-only access.</span></span> <span data-ttu-id="9af52-175">Zie [hoe toouse Azure zoeken in .NET](search-howto-dotnet-sdk.md) tooget gestart.</span><span class="sxs-lookup"><span data-stu-id="9af52-175">See [How toouse Azure Search in .NET](search-howto-dotnet-sdk.md) tooget started.</span></span>

<span data-ttu-id="9af52-176">Zie [bouwen en query uitvoeren op uw eerste index](search-get-started-portal.md) voor een snelle zelfstudie op basis van de portal.</span><span class="sxs-lookup"><span data-stu-id="9af52-176">See [Build and query your first index](search-get-started-portal.md) for a quick portal-based tutorial.</span></span>

