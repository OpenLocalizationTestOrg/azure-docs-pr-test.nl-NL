---
title: Overzicht van Azure Event raster
description: Beschrijving van Azure Event raster en de concepten.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 59a834f32793e349d5639baf3c80dbcba274dfa8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="an-introduction-to-azure-event-grid"></a><span data-ttu-id="718de-103">Een inleiding tot Azure gebeurtenis raster</span><span class="sxs-lookup"><span data-stu-id="718de-103">An introduction to Azure Event Grid</span></span>

<span data-ttu-id="718de-104">Azure Event raster kunt u eenvoudig om toepassingen te bouwen met architectuur op basis van gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="718de-104">Azure Event Grid allows you to easily build applications with event-based architectures.</span></span> <span data-ttu-id="718de-105">U selecteert de Azure resource die u wilt abonneren op en geef de gebeurtenis-handler of WebHook-eindpunt om de gebeurtenis te verzenden.</span><span class="sxs-lookup"><span data-stu-id="718de-105">You select the Azure resource you would like to subscribe to, and give the event handler or WebHook endpoint to send the event to.</span></span> <span data-ttu-id="718de-106">Gebeurtenis raster bevat ingebouwde ondersteuning voor gebeurtenissen die afkomstig zijn van de Azure-services, zoals de storage-blobs en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="718de-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span></span> <span data-ttu-id="718de-107">Gebeurtenis raster heeft ook aangepaste ondersteuning voor de toepassing en gebeurtenissen van derden, met behulp van aangepaste onderwerpen en aangepaste webhooks.</span><span class="sxs-lookup"><span data-stu-id="718de-107">Event Grid also has custom support for application and third-party events, using custom topics and custom webhooks.</span></span> 

<span data-ttu-id="718de-108">U kunt filters gebruiken voor het doorsturen van specifieke gebeurtenissen naar verschillende eindpunten, multicast bij meerdere eindpunten en zorg ervoor dat uw gebeurtenissen op betrouwbare wijze worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="718de-108">You can use filters to route specific events to different endpoints, multicast to multiple endpoints, and make sure your events are reliably delivered.</span></span> <span data-ttu-id="718de-109">Gebeurtenis raster ook met ingebouwde ondersteuning voor aangepaste en derden gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="718de-109">Event Grid also has built in support for custom and third-party events.</span></span>

<span data-ttu-id="718de-110">Voor de preview-versie ondersteunt Event Grid de locaties **westus2** en **westcentralus**.</span><span class="sxs-lookup"><span data-stu-id="718de-110">For the preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span> <span data-ttu-id="718de-111">Andere regio's worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="718de-111">Other regions will be added.</span></span>

<span data-ttu-id="718de-112">Dit artikel bevat een overzicht van Azure Event raster.</span><span class="sxs-lookup"><span data-stu-id="718de-112">This article provides an overview of Azure Event Grid.</span></span> <span data-ttu-id="718de-113">Als u aan de slag met Event raster wilt, Zie [maken en route aangepaste gebeurtenissen met Azure Event raster](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="718de-113">If you want to get started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>

![Gebeurtenis raster functionele model](./media/overview/event-grid-functional-model.png)

<span data-ttu-id="718de-115">Blob Storage is momenteel niet openbaar beschikbaar als een publisher.</span><span class="sxs-lookup"><span data-stu-id="718de-115">Currently, Blob Storage is not publicly available as a publisher.</span></span>

## <a name="concepts"></a><span data-ttu-id="718de-116">Concepten</span><span class="sxs-lookup"><span data-stu-id="718de-116">Concepts</span></span>

<span data-ttu-id="718de-117">Er zijn vijf concepten in Azure gebeurtenis raster waarmee u aan de slag:</span><span class="sxs-lookup"><span data-stu-id="718de-117">There are five concepts in Azure Event Grid that let you get going:</span></span>

* <span data-ttu-id="718de-118">**Gebeurtenissen** -wat is er gebeurd.</span><span class="sxs-lookup"><span data-stu-id="718de-118">**Events** - What happened.</span></span>
* <span data-ttu-id="718de-119">**Gebeurtenisuitgevers bronnen** - waar de gebeurtenis heeft plaatsgevonden.</span><span class="sxs-lookup"><span data-stu-id="718de-119">**Event sources/publishers** - Where the event took place.</span></span>
* <span data-ttu-id="718de-120">**Onderwerpen over** -het eindpunt waar de gebeurtenissen voor het verzenden van uitgevers.</span><span class="sxs-lookup"><span data-stu-id="718de-120">**Topics** - The endpoint where publishers send events.</span></span>
* <span data-ttu-id="718de-121">**Abonnementen voor gebeurtenissen** -eindpunt of de ingebouwde mechanisme route gebeurtenissen, soms aan meerdere handlers.</span><span class="sxs-lookup"><span data-stu-id="718de-121">**Event subscriptions** - The endpoint or built-in mechanism to route events, sometimes to multiple handlers.</span></span> <span data-ttu-id="718de-122">Abonnementen worden ook gebruikt door handlers op intelligente wijze binnenkomende om gebeurtenissen te filteren.</span><span class="sxs-lookup"><span data-stu-id="718de-122">Subscriptions are also used by handlers to intelligently filter incoming events.</span></span>
* <span data-ttu-id="718de-123">**Gebeurtenis-handlers** -de app of de service reageert op de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="718de-123">**Event handlers** - The app or service reacting to the event.</span></span>

<span data-ttu-id="718de-124">Zie voor meer informatie over deze concepten [concepten in Azure gebeurtenis raster](concepts.md).</span><span class="sxs-lookup"><span data-stu-id="718de-124">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span></span>

## <a name="capabilities"></a><span data-ttu-id="718de-125">Functionaliteit</span><span class="sxs-lookup"><span data-stu-id="718de-125">Capabilities</span></span>

<span data-ttu-id="718de-126">Hier volgen enkele van de belangrijkste functies van Azure Event raster:</span><span class="sxs-lookup"><span data-stu-id="718de-126">Here are some of the key features of Azure Event Grid:</span></span>

* <span data-ttu-id="718de-127">**Eenvoud** -punt en klik op om de gebeurtenissen van uw Azure-resource met een gebeurtenis-handler of het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="718de-127">**Simplicity** - Point and click to aim events from your Azure resource to any event handler or endpoint.</span></span>
* <span data-ttu-id="718de-128">**Geavanceerde filters** -Filter op de gebeurtenis type of gebeurtenis publicatiepad om te controleren of gebeurtenis-handlers alleen relevante gebeurtenissen ontvangen.</span><span class="sxs-lookup"><span data-stu-id="718de-128">**Advanced filtering** - Filter on event type or event publish path to ensure event handlers only receive relevant events.</span></span>
* <span data-ttu-id="718de-129">**Fan-out** -abonneren meerdere eindpunten op dezelfde gebeurtenis kopieën van de gebeurtenis verzenden naar plaatsen waar nodig.</span><span class="sxs-lookup"><span data-stu-id="718de-129">**Fan-out** - Subscribe multiple endpoints to the same event to send copies of the event to as many places as needed.</span></span>
* <span data-ttu-id="718de-130">**Betrouwbaarheid** -gebruikmaken van 24 uur opnieuw proberen met exponentieel uitstel om te controleren gebeurtenissen worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="718de-130">**Reliability** - Utilize 24-hour retry with exponential backoff to ensure events are delivered.</span></span>
* <span data-ttu-id="718de-131">**Betalen per gebeurtenis** : betaal alleen voor het bedrag u gebeurtenis raster.</span><span class="sxs-lookup"><span data-stu-id="718de-131">**Pay-per-event** - Pay only for the amount you use Event Grid.</span></span>
* <span data-ttu-id="718de-132">**Hoge doorvoersnelheid** -hoog volume werkbelastingen voor gebeurtenis raster bouwen met ondersteuning voor miljoenen gebeurtenissen per seconde.</span><span class="sxs-lookup"><span data-stu-id="718de-132">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span></span>
* <span data-ttu-id="718de-133">**Ingebouwde gebeurtenissen** - slag snel gebruiksklaar met ingebouwde gebeurtenissen resource gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="718de-133">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span></span>
* <span data-ttu-id="718de-134">**Aangepaste gebeurtenissen** -gebeurtenis raster route, filter en betrouwbaar afleveren aangepaste gebeurtenissen in uw app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="718de-134">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span></span>

## <a name="built-in-publisher-and-handler-integration"></a><span data-ttu-id="718de-135">Ingebouwde publisher en de handler-integratie</span><span class="sxs-lookup"><span data-stu-id="718de-135">Built-in publisher and handler integration</span></span>

<span data-ttu-id="718de-136">Azure biedt gebeurtenisondersteuning voor ingebouwde met meerdere services, waaronder zowel uitgevers en handlers.</span><span class="sxs-lookup"><span data-stu-id="718de-136">Azure offers built-in event support using numerous services, including both publishers and handlers.</span></span>

### <a name="publishers"></a><span data-ttu-id="718de-137">Uitgevers</span><span class="sxs-lookup"><span data-stu-id="718de-137">Publishers</span></span>

<span data-ttu-id="718de-138">De volgende Azure-services hebt op dit moment wordt de uitgever van de ingebouwde ondersteuning voor de gebeurtenis raster:</span><span class="sxs-lookup"><span data-stu-id="718de-138">Currently, the following Azure services have built-in publisher support for event grid:</span></span>

* <span data-ttu-id="718de-139">Resourcegroepen (beheerbewerkingen)</span><span class="sxs-lookup"><span data-stu-id="718de-139">Resource Groups (management operations)</span></span>
* <span data-ttu-id="718de-140">Azure-abonnementen (beheerbewerkingen)</span><span class="sxs-lookup"><span data-stu-id="718de-140">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="718de-141">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="718de-141">Event Hubs</span></span>
* <span data-ttu-id="718de-142">Aangepaste-onderwerpen</span><span class="sxs-lookup"><span data-stu-id="718de-142">Custom Topics</span></span>

<span data-ttu-id="718de-143">Andere Azure-services worden van dit jaar met toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="718de-143">Other Azure services will be added this year.</span></span>

### <a name="handlers"></a><span data-ttu-id="718de-144">Handlers</span><span class="sxs-lookup"><span data-stu-id="718de-144">Handlers</span></span>

<span data-ttu-id="718de-145">De volgende Azure-services hebt op dit moment handler ingebouwde ondersteuning voor gebeurtenis raster:</span><span class="sxs-lookup"><span data-stu-id="718de-145">Currently, the following Azure services have built-in handler support for Event Grid:</span></span> 

* <span data-ttu-id="718de-146">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="718de-146">Azure Functions</span></span>
* <span data-ttu-id="718de-147">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="718de-147">Logic Apps</span></span>
* <span data-ttu-id="718de-148">Azure Automation</span><span class="sxs-lookup"><span data-stu-id="718de-148">Azure Automation</span></span>
* <span data-ttu-id="718de-149">Webhooks.</span><span class="sxs-lookup"><span data-stu-id="718de-149">WebHooks</span></span>

<span data-ttu-id="718de-150">Andere Azure-services worden van dit jaar met toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="718de-150">Other Azure services will be added this year.</span></span>

## <a name="what-can-i-do-with-event-grid"></a><span data-ttu-id="718de-151">Wat kan ik doen met gebeurtenis raster</span><span class="sxs-lookup"><span data-stu-id="718de-151">What can I do with Event Grid?</span></span>

<span data-ttu-id="718de-152">Azure Event raster biedt verschillende mogelijkheden die aanzienlijk zonder server verbeteren, ops automatisering en integratie werk:</span><span class="sxs-lookup"><span data-stu-id="718de-152">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span></span> 

### <a name="serverless-application-architectures"></a><span data-ttu-id="718de-153">Architecturen voor serverloze toepassingen</span><span class="sxs-lookup"><span data-stu-id="718de-153">Serverless application architectures</span></span>

![Toepassing zonder server](./media/overview/serverless_web_app.png)

<span data-ttu-id="718de-155">Event Grid verbindt gegevensbronnen en gebeurtenis-handlers.</span><span class="sxs-lookup"><span data-stu-id="718de-155">Event Grid connects data sources and event handlers.</span></span> <span data-ttu-id="718de-156">Gebruik Event Grid bijvoorbeeld om direct een serverloze functie te triggeren voor het uitvoeren van beeldanalyse zodra er een nieuwe foto wordt toegevoegd aan de container voor blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="718de-156">For example, use Event Grid to instantly trigger a serverless function to run image analysis each time a new photo is added to a blob storage container.</span></span> 

### <a name="ops-automation"></a><span data-ttu-id="718de-157">OPS Automation</span><span class="sxs-lookup"><span data-stu-id="718de-157">Ops Automation</span></span>

![Ops-automatisering](./media/overview/Ops_automation.png)

<span data-ttu-id="718de-159">Met Event Grid kunt u sneller automatiseren en makkelijker beleid afdwingen.</span><span class="sxs-lookup"><span data-stu-id="718de-159">Event Grid allows you to speed automation and simplify policy enforcement.</span></span> <span data-ttu-id="718de-160">Zo kan Event Grid een melding sturen naar Azure Automation wanneer er een virtuele machine is gemaakt of wanneer er een SQL-database in gebruik wordt genomen.</span><span class="sxs-lookup"><span data-stu-id="718de-160">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span></span> <span data-ttu-id="718de-161">Deze gebeurtenissen kunnen worden gebruikt om automatisch te controleren of serviceconfiguraties compatibel zijn, metagegevens aan te bieden aan tools voor bewerkingen, virtuele machines te taggen of werkitems te archiveren.</span><span class="sxs-lookup"><span data-stu-id="718de-161">These events can be used to automatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span></span>

### <a name="application-integration"></a><span data-ttu-id="718de-162">Integratie van toepassingen</span><span class="sxs-lookup"><span data-stu-id="718de-162">Application integration</span></span>

![Integratie van toepassingen](./media/overview/app_integration.png)

<span data-ttu-id="718de-164">Event Grid verbindt uw app met andere services.</span><span class="sxs-lookup"><span data-stu-id="718de-164">Event Grid connects your app with other services.</span></span> <span data-ttu-id="718de-165">Bijvoorbeeld, een eigen onderwerp om uw app gebeurtenisgegevens verzenden naar Event raster en te profiteren van de betrouwbare levering, geavanceerde routering, maken en directe integratie met Azure.</span><span class="sxs-lookup"><span data-stu-id="718de-165">For example, create a custom topic to send your app's event data to Event Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span></span> <span data-ttu-id="718de-166">U kunt Event Grid ook gebruiken met Logic Apps om op elke locatie gegevens te verwerken, zonder dat u hiervoor code hoeft te schrijven.</span><span class="sxs-lookup"><span data-stu-id="718de-166">Alternatively, you can use Event Grid with Logic Apps to process data anywhere, without writing code.</span></span> 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a><span data-ttu-id="718de-167">Hoe wordt gebeurtenis raster van andere integratie van Azure-services?</span><span class="sxs-lookup"><span data-stu-id="718de-167">How is Event Grid different from other Azure integration services?</span></span>

<span data-ttu-id="718de-168">Gebeurtenis raster is een eventing backplane waarmee gebeurtenisafhankelijke, reactieve programmering.</span><span class="sxs-lookup"><span data-stu-id="718de-168">Event Grid is an eventing backplane that enables event-driven, reactive programming.</span></span> <span data-ttu-id="718de-169">Het is nauw geïntegreerd met Azure-services en kan worden geïntegreerd met services van derden.</span><span class="sxs-lookup"><span data-stu-id="718de-169">It is deeply integrated with Azure services and can be integrated with third-party services.</span></span> <span data-ttu-id="718de-170">Het gebeurtenisbericht bevat informatie die u nodig hebt om te reageren op wijzigingen in de services en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="718de-170">The event message contains the information you need to react to changes in services and applications.</span></span> <span data-ttu-id="718de-171">Raster gebeurtenis is niet een gegevens-pijplijn en levert niet het werkelijke object dat is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="718de-171">Event Grid is not a data pipeline, and does not deliver the actual object that was updated.</span></span>

<span data-ttu-id="718de-172">Service Bus is geschikt voor traditionele enterprise-toepassingen waarvoor transacties, rangschikken, detectie van duplicaten en onmiddellijk consistentie.</span><span class="sxs-lookup"><span data-stu-id="718de-172">Service Bus is well suited for traditional enterprise applications that require transactions, ordering, duplicate detection, and instantaneous consistency.</span></span> <span data-ttu-id="718de-173">Gebeurtenis raster is ontworpen voor snelheid, schaal, breedte en lage kosten in een reactieve model.</span><span class="sxs-lookup"><span data-stu-id="718de-173">Event Grid is designed for speed, scale, breadth, and low cost in a reactive model.</span></span> <span data-ttu-id="718de-174">Het is zeer geschikt voor zonder server architectuur.</span><span class="sxs-lookup"><span data-stu-id="718de-174">It is well suited to serverless architecture.</span></span>

<span data-ttu-id="718de-175">Gebeurtenis raster vormt een aanvulling op andere Azure-services zoals Logic Apps en Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="718de-175">Event Grid complements other Azure services like Logic Apps and Event Hubs.</span></span> <span data-ttu-id="718de-176">De logische app om te beginnen met de werkstroom wordt geactiveerd door gebeurtenis raster.</span><span class="sxs-lookup"><span data-stu-id="718de-176">Event Grid triggers the logic app to begin its workflow.</span></span> <span data-ttu-id="718de-177">Event Hubs werkt met gebeurtenis raster doordat u reageren op gebeurtenissen van Event Hubs vastleggen en bouwen van toegangsroutes en transformatie gegevenspijplijnen.</span><span class="sxs-lookup"><span data-stu-id="718de-177">Event Hubs works with Event Grid by enabling you to react to events from Event Hubs Capture, and build data ingress and transformation pipelines.</span></span>

## <a name="how-much-does-event-grid-cost"></a><span data-ttu-id="718de-178">Wat kost gebeurtenis raster?</span><span class="sxs-lookup"><span data-stu-id="718de-178">How much does Event Grid cost?</span></span>

<span data-ttu-id="718de-179">Azure gebeurtenis raster maakt gebruik van een prijsmodel voor betalen per gebeurtenis, zodat u alleen betaalt voor wat u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="718de-179">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span></span>

<span data-ttu-id="718de-180">Gebeurtenis raster kost $0,60 per miljoen operations ($0,30 tijdens de preview) en de eerste 100.000 bewerking per maand zijn gratis.</span><span class="sxs-lookup"><span data-stu-id="718de-180">Event Grid costs $0.60 per million operations ($0.30 during preview) and the first 100,000 operation per month are free.</span></span> <span data-ttu-id="718de-181">Bewerkingen worden gedefinieerd als gebeurtenis inkomend, geavanceerde overeen, levering poging en management aanroepen.</span><span class="sxs-lookup"><span data-stu-id="718de-181">Operations are defined as event ingress, advanced match, delivery attempt, and management calls.</span></span>  <span data-ttu-id="718de-182">Meer informatie vindt u op de [pagina met prijzen](https://azure.microsoft.com/pricing/details/event-grid/).</span><span class="sxs-lookup"><span data-stu-id="718de-182">More details can be found on the [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="718de-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="718de-183">Next steps</span></span>

* <span data-ttu-id="718de-184">[Maken en zich abonneren op aangepaste gebeurtenissen](custom-event-quickstart.md) meteen en uw eigen aangepaste gebeurtenissen verzenden naar een willekeurig eindpunt met behulp van de Azure gebeurtenis raster Quick Start te starten.</span><span class="sxs-lookup"><span data-stu-id="718de-184">[Create and subscribe to custom events](custom-event-quickstart.md) Jump right in and start sending your own custom events to any endpoint using the Azure Event Grid quickstart.</span></span>
* <span data-ttu-id="718de-185">[Met Logic Apps als een gebeurtenis-Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) een zelfstudie over het bouwen van een app met Logic Apps om te reageren op gebeurtenissen door gebeurtenis raster gepusht.</span><span class="sxs-lookup"><span data-stu-id="718de-185">[Using Logic Apps as an Event Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) A tutorial on building an app using Logic Apps to react to events pushed by Event Grid.</span></span>
* [<span data-ttu-id="718de-186">Gebeurtenis raster REST API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="718de-186">Event Grid REST API reference</span></span>](/rest/api/eventgrid)  
  <span data-ttu-id="718de-187">Biedt meer technische informatie over het raster Azure-gebeurtenis en een referentie voor het beheer van abonnementen, doorsturen en filteren.</span><span class="sxs-lookup"><span data-stu-id="718de-187">Provides more technical information about the Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span></span>