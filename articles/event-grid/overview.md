---
title: overzicht van de gebeurtenis raster aaaAzure
description: Beschrijving van Azure Event raster en de concepten.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a><span data-ttu-id="f5d50-103">Een inleiding tooAzure gebeurtenis raster</span><span class="sxs-lookup"><span data-stu-id="f5d50-103">An introduction tooAzure Event Grid</span></span>

<span data-ttu-id="f5d50-104">Azure Event raster kunt u tooeasily build toepassingen met architectuur op basis van gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="f5d50-104">Azure Event Grid allows you tooeasily build applications with event-based architectures.</span></span> <span data-ttu-id="f5d50-105">U selecteren hello Azure resource die u wilt toosubscribe aan, en geven Hallo gebeurtenis-handler of WebHook eindpunt toosend Hallo gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="f5d50-105">You select hello Azure resource you would like toosubscribe to, and give hello event handler or WebHook endpoint toosend hello event to.</span></span> <span data-ttu-id="f5d50-106">Gebeurtenis raster bevat ingebouwde ondersteuning voor gebeurtenissen die afkomstig zijn van de Azure-services, zoals de storage-blobs en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="f5d50-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span></span> <span data-ttu-id="f5d50-107">Gebeurtenis raster heeft ook aangepaste ondersteuning voor de toepassing en gebeurtenissen van derden, met behulp van aangepaste onderwerpen en aangepaste webhooks.</span><span class="sxs-lookup"><span data-stu-id="f5d50-107">Event Grid also has custom support for application and third-party events, using custom topics and custom webhooks.</span></span> 

<span data-ttu-id="f5d50-108">U kunt filters tooroute specifieke gebeurtenissen toodifferent eindpunten, multicast toomultiple eindpunten, gebruiken en zorg ervoor dat uw gebeurtenissen op betrouwbare wijze worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="f5d50-108">You can use filters tooroute specific events toodifferent endpoints, multicast toomultiple endpoints, and make sure your events are reliably delivered.</span></span> <span data-ttu-id="f5d50-109">Gebeurtenis raster ook met ingebouwde ondersteuning voor aangepaste en derden gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="f5d50-109">Event Grid also has built in support for custom and third-party events.</span></span>

<span data-ttu-id="f5d50-110">Voor de preview-versie Hallo gebeurtenis raster ondersteunt **westus2** en **westcentralus** locaties.</span><span class="sxs-lookup"><span data-stu-id="f5d50-110">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span> <span data-ttu-id="f5d50-111">Andere regio's worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f5d50-111">Other regions will be added.</span></span>

<span data-ttu-id="f5d50-112">Dit artikel bevat een overzicht van Azure Event raster.</span><span class="sxs-lookup"><span data-stu-id="f5d50-112">This article provides an overview of Azure Event Grid.</span></span> <span data-ttu-id="f5d50-113">Als u tooget met raster gebeurtenis wordt gestart wilt, Zie [maken en route aangepaste gebeurtenissen met Azure Event raster](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="f5d50-113">If you want tooget started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>

![Gebeurtenis raster functionele model](./media/overview/event-grid-functional-model.png)

<span data-ttu-id="f5d50-115">Blob Storage is momenteel niet openbaar beschikbaar als een publisher.</span><span class="sxs-lookup"><span data-stu-id="f5d50-115">Currently, Blob Storage is not publicly available as a publisher.</span></span>

## <a name="concepts"></a><span data-ttu-id="f5d50-116">Concepten</span><span class="sxs-lookup"><span data-stu-id="f5d50-116">Concepts</span></span>

<span data-ttu-id="f5d50-117">Er zijn vijf concepten in Azure gebeurtenis raster waarmee u aan de slag:</span><span class="sxs-lookup"><span data-stu-id="f5d50-117">There are five concepts in Azure Event Grid that let you get going:</span></span>

* <span data-ttu-id="f5d50-118">**Gebeurtenissen** -wat is er gebeurd.</span><span class="sxs-lookup"><span data-stu-id="f5d50-118">**Events** - What happened.</span></span>
* <span data-ttu-id="f5d50-119">**Gebeurtenisuitgevers bronnen** - Hallo gebeurtenis heeft plaatsgevonden.</span><span class="sxs-lookup"><span data-stu-id="f5d50-119">**Event sources/publishers** - Where hello event took place.</span></span>
* <span data-ttu-id="f5d50-120">**Onderwerpen over** -Hallo eindpunt waar de gebeurtenissen voor het verzenden van uitgevers.</span><span class="sxs-lookup"><span data-stu-id="f5d50-120">**Topics** - hello endpoint where publishers send events.</span></span>
* <span data-ttu-id="f5d50-121">**Abonnementen voor gebeurtenissen** -Hallo eindpunt of de ingebouwde mechanisme tooroute gebeurtenissen, soms toomultiple handlers.</span><span class="sxs-lookup"><span data-stu-id="f5d50-121">**Event subscriptions** - hello endpoint or built-in mechanism tooroute events, sometimes toomultiple handlers.</span></span> <span data-ttu-id="f5d50-122">Abonnementen worden ook gebruikt door handlers toointelligently binnenkomende Filtergebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="f5d50-122">Subscriptions are also used by handlers toointelligently filter incoming events.</span></span>
* <span data-ttu-id="f5d50-123">**Gebeurtenis-handlers** - app Hallo of kruisreagerende toohello-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="f5d50-123">**Event handlers** - hello app or service reacting toohello event.</span></span>

<span data-ttu-id="f5d50-124">Zie voor meer informatie over deze concepten [concepten in Azure gebeurtenis raster](concepts.md).</span><span class="sxs-lookup"><span data-stu-id="f5d50-124">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span></span>

## <a name="capabilities"></a><span data-ttu-id="f5d50-125">Functionaliteit</span><span class="sxs-lookup"><span data-stu-id="f5d50-125">Capabilities</span></span>

<span data-ttu-id="f5d50-126">Hier volgen enkele van de belangrijkste functies van Azure Event raster Hallo:</span><span class="sxs-lookup"><span data-stu-id="f5d50-126">Here are some of hello key features of Azure Event Grid:</span></span>

* <span data-ttu-id="f5d50-127">**Eenvoud** -punt en klik op tooaim-gebeurtenissen van uw Azure-resource tooany gebeurtenis-handler of het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="f5d50-127">**Simplicity** - Point and click tooaim events from your Azure resource tooany event handler or endpoint.</span></span>
* <span data-ttu-id="f5d50-128">**Geavanceerde filters** -Filter op de gebeurtenis type of een gebeurtenis publiceren pad tooensure gebeurtenis-handlers alleen relevante gebeurtenissen ontvangen.</span><span class="sxs-lookup"><span data-stu-id="f5d50-128">**Advanced filtering** - Filter on event type or event publish path tooensure event handlers only receive relevant events.</span></span>
* <span data-ttu-id="f5d50-129">**Fan-out** -meerdere eindpunten toohello abonneren dezelfde gebeurtenis toosend kopieën van Hallo gebeurtenis tooas veel plaatsen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="f5d50-129">**Fan-out** - Subscribe multiple endpoints toohello same event toosend copies of hello event tooas many places as needed.</span></span>
* <span data-ttu-id="f5d50-130">**Betrouwbaarheid** -gebruikmaken van 24 uur opnieuw proberen met exponentieel uitstel tooensure gebeurtenissen worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="f5d50-130">**Reliability** - Utilize 24-hour retry with exponential backoff tooensure events are delivered.</span></span>
* <span data-ttu-id="f5d50-131">**Betalen per gebeurtenis** : betaal alleen voor Hallo bedrag u gebeurtenis raster.</span><span class="sxs-lookup"><span data-stu-id="f5d50-131">**Pay-per-event** - Pay only for hello amount you use Event Grid.</span></span>
* <span data-ttu-id="f5d50-132">**Hoge doorvoersnelheid** -hoog volume werkbelastingen voor gebeurtenis raster bouwen met ondersteuning voor miljoenen gebeurtenissen per seconde.</span><span class="sxs-lookup"><span data-stu-id="f5d50-132">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span></span>
* <span data-ttu-id="f5d50-133">**Ingebouwde gebeurtenissen** - slag snel gebruiksklaar met ingebouwde gebeurtenissen resource gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="f5d50-133">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span></span>
* <span data-ttu-id="f5d50-134">**Aangepaste gebeurtenissen** -gebeurtenis raster route, filter en betrouwbaar afleveren aangepaste gebeurtenissen in uw app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f5d50-134">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span></span>

## <a name="built-in-publisher-and-handler-integration"></a><span data-ttu-id="f5d50-135">Ingebouwde publisher en de handler-integratie</span><span class="sxs-lookup"><span data-stu-id="f5d50-135">Built-in publisher and handler integration</span></span>

<span data-ttu-id="f5d50-136">Azure biedt gebeurtenisondersteuning voor ingebouwde met meerdere services, waaronder zowel uitgevers en handlers.</span><span class="sxs-lookup"><span data-stu-id="f5d50-136">Azure offers built-in event support using numerous services, including both publishers and handlers.</span></span>

### <a name="publishers"></a><span data-ttu-id="f5d50-137">Uitgevers</span><span class="sxs-lookup"><span data-stu-id="f5d50-137">Publishers</span></span>

<span data-ttu-id="f5d50-138">Op dit moment hebben hello volgende Azure-services een ingebouwde publisher ondersteuning voor gebeurtenis raster:</span><span class="sxs-lookup"><span data-stu-id="f5d50-138">Currently, hello following Azure services have built-in publisher support for event grid:</span></span>

* <span data-ttu-id="f5d50-139">Resourcegroepen (beheerbewerkingen)</span><span class="sxs-lookup"><span data-stu-id="f5d50-139">Resource Groups (management operations)</span></span>
* <span data-ttu-id="f5d50-140">Azure-abonnementen (beheerbewerkingen)</span><span class="sxs-lookup"><span data-stu-id="f5d50-140">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="f5d50-141">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f5d50-141">Event Hubs</span></span>
* <span data-ttu-id="f5d50-142">Aangepaste-onderwerpen</span><span class="sxs-lookup"><span data-stu-id="f5d50-142">Custom Topics</span></span>

<span data-ttu-id="f5d50-143">Andere Azure-services worden van dit jaar met toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f5d50-143">Other Azure services will be added this year.</span></span>

### <a name="handlers"></a><span data-ttu-id="f5d50-144">Handlers</span><span class="sxs-lookup"><span data-stu-id="f5d50-144">Handlers</span></span>

<span data-ttu-id="f5d50-145">Op dit moment hebben hello volgende Azure-services een ingebouwde handler ondersteuning voor gebeurtenis raster:</span><span class="sxs-lookup"><span data-stu-id="f5d50-145">Currently, hello following Azure services have built-in handler support for Event Grid:</span></span> 

* <span data-ttu-id="f5d50-146">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f5d50-146">Azure Functions</span></span>
* <span data-ttu-id="f5d50-147">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="f5d50-147">Logic Apps</span></span>
* <span data-ttu-id="f5d50-148">Azure Automation</span><span class="sxs-lookup"><span data-stu-id="f5d50-148">Azure Automation</span></span>
* <span data-ttu-id="f5d50-149">Webhooks.</span><span class="sxs-lookup"><span data-stu-id="f5d50-149">WebHooks</span></span>

<span data-ttu-id="f5d50-150">Andere Azure-services worden van dit jaar met toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f5d50-150">Other Azure services will be added this year.</span></span>

## <a name="what-can-i-do-with-event-grid"></a><span data-ttu-id="f5d50-151">Wat kan ik doen met gebeurtenis raster</span><span class="sxs-lookup"><span data-stu-id="f5d50-151">What can I do with Event Grid?</span></span>

<span data-ttu-id="f5d50-152">Azure Event raster biedt verschillende mogelijkheden die aanzienlijk zonder server verbeteren, ops automatisering en integratie werk:</span><span class="sxs-lookup"><span data-stu-id="f5d50-152">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span></span> 

### <a name="serverless-application-architectures"></a><span data-ttu-id="f5d50-153">Architecturen voor serverloze toepassingen</span><span class="sxs-lookup"><span data-stu-id="f5d50-153">Serverless application architectures</span></span>

![Toepassing zonder server](./media/overview/serverless_web_app.png)

<span data-ttu-id="f5d50-155">Event Grid verbindt gegevensbronnen en gebeurtenis-handlers.</span><span class="sxs-lookup"><span data-stu-id="f5d50-155">Event Grid connects data sources and event handlers.</span></span> <span data-ttu-id="f5d50-156">Bijvoorbeeld, gebeurtenis raster tooinstantly trigger-een zonder server functie toorun installatiekopie analyse telkens wanneer een nieuwe foto is toegevoegd tooa blob storage-container gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f5d50-156">For example, use Event Grid tooinstantly trigger a serverless function toorun image analysis each time a new photo is added tooa blob storage container.</span></span> 

### <a name="ops-automation"></a><span data-ttu-id="f5d50-157">OPS Automation</span><span class="sxs-lookup"><span data-stu-id="f5d50-157">Ops Automation</span></span>

![Ops-automatisering](./media/overview/Ops_automation.png)

<span data-ttu-id="f5d50-159">Gebeurtenis raster kunt u toospeed automation en afdwingen van beleid vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="f5d50-159">Event Grid allows you toospeed automation and simplify policy enforcement.</span></span> <span data-ttu-id="f5d50-160">Zo kan Event Grid een melding sturen naar Azure Automation wanneer er een virtuele machine is gemaakt of wanneer er een SQL-database in gebruik wordt genomen.</span><span class="sxs-lookup"><span data-stu-id="f5d50-160">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span></span> <span data-ttu-id="f5d50-161">Deze gebeurtenissen kunnen worden gebruikt tooautomatically Controleer of-configuraties zijn compatibel zijn, metagegevens in de operations-hulpprogramma's, tag virtuele machines of werkitems bestand geplaatst.</span><span class="sxs-lookup"><span data-stu-id="f5d50-161">These events can be used tooautomatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span></span>

### <a name="application-integration"></a><span data-ttu-id="f5d50-162">Integratie van toepassingen</span><span class="sxs-lookup"><span data-stu-id="f5d50-162">Application integration</span></span>

![Integratie van toepassingen](./media/overview/app_integration.png)

<span data-ttu-id="f5d50-164">Event Grid verbindt uw app met andere services.</span><span class="sxs-lookup"><span data-stu-id="f5d50-164">Event Grid connects your app with other services.</span></span> <span data-ttu-id="f5d50-165">Bijvoorbeeld een aangepaste onderwerp toosend van uw app gebeurtenis gegevens tooEvent raster en maken en te profiteren van de geavanceerde routering, betrouwbare aflevering directe integratie met Azure.</span><span class="sxs-lookup"><span data-stu-id="f5d50-165">For example, create a custom topic toosend your app's event data tooEvent Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span></span> <span data-ttu-id="f5d50-166">U kunt ook gebeurtenis raster met Logic Apps tooprocess gegevens overal en gebruiken zonder code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="f5d50-166">Alternatively, you can use Event Grid with Logic Apps tooprocess data anywhere, without writing code.</span></span> 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a><span data-ttu-id="f5d50-167">Hoe wordt gebeurtenis raster van andere integratie van Azure-services?</span><span class="sxs-lookup"><span data-stu-id="f5d50-167">How is Event Grid different from other Azure integration services?</span></span>

<span data-ttu-id="f5d50-168">Gebeurtenis raster is een eventing backplane waarmee gebeurtenisafhankelijke, reactieve programmering.</span><span class="sxs-lookup"><span data-stu-id="f5d50-168">Event Grid is an eventing backplane that enables event-driven, reactive programming.</span></span> <span data-ttu-id="f5d50-169">Het is nauw geïntegreerd met Azure-services en kan worden geïntegreerd met services van derden.</span><span class="sxs-lookup"><span data-stu-id="f5d50-169">It is deeply integrated with Azure services and can be integrated with third-party services.</span></span> <span data-ttu-id="f5d50-170">Hallo-gebeurtenisbericht bevat Hallo-informatie die u nodig hebt tooreact toochanges in services en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="f5d50-170">hello event message contains hello information you need tooreact toochanges in services and applications.</span></span> <span data-ttu-id="f5d50-171">Raster gebeurtenis is niet een gegevens-pijplijn en bezorgt geen daadwerkelijke Hallo-object dat is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f5d50-171">Event Grid is not a data pipeline, and does not deliver hello actual object that was updated.</span></span>

<span data-ttu-id="f5d50-172">Service Bus is geschikt voor traditionele enterprise-toepassingen waarvoor transacties, rangschikken, detectie van duplicaten en onmiddellijk consistentie.</span><span class="sxs-lookup"><span data-stu-id="f5d50-172">Service Bus is well suited for traditional enterprise applications that require transactions, ordering, duplicate detection, and instantaneous consistency.</span></span> <span data-ttu-id="f5d50-173">Gebeurtenis raster is ontworpen voor snelheid, schaal, breedte en lage kosten in een reactieve model.</span><span class="sxs-lookup"><span data-stu-id="f5d50-173">Event Grid is designed for speed, scale, breadth, and low cost in a reactive model.</span></span> <span data-ttu-id="f5d50-174">Het is uitermate geschikt tooserverless architectuur.</span><span class="sxs-lookup"><span data-stu-id="f5d50-174">It is well suited tooserverless architecture.</span></span>

<span data-ttu-id="f5d50-175">Gebeurtenis raster vormt een aanvulling op andere Azure-services zoals Logic Apps en Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="f5d50-175">Event Grid complements other Azure services like Logic Apps and Event Hubs.</span></span> <span data-ttu-id="f5d50-176">Raster gebeurtenistriggers Hallo logic app toobegin de workflow.</span><span class="sxs-lookup"><span data-stu-id="f5d50-176">Event Grid triggers hello logic app toobegin its workflow.</span></span> <span data-ttu-id="f5d50-177">Event Hubs werkt met gebeurtenis raster doordat u tooreact tooevents van Event Hubs vastleggen en build inkomende en transformatie gegevenspijplijnen.</span><span class="sxs-lookup"><span data-stu-id="f5d50-177">Event Hubs works with Event Grid by enabling you tooreact tooevents from Event Hubs Capture, and build data ingress and transformation pipelines.</span></span>

## <a name="how-much-does-event-grid-cost"></a><span data-ttu-id="f5d50-178">Wat kost gebeurtenis raster?</span><span class="sxs-lookup"><span data-stu-id="f5d50-178">How much does Event Grid cost?</span></span>

<span data-ttu-id="f5d50-179">Azure gebeurtenis raster maakt gebruik van een prijsmodel voor betalen per gebeurtenis, zodat u alleen betaalt voor wat u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f5d50-179">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span></span>

<span data-ttu-id="f5d50-180">Gebeurtenis raster kost $0,60 per miljoen operations ($0,30 tijdens de preview) en Hallo eerst 100.000 bewerking per maand zijn gratis.</span><span class="sxs-lookup"><span data-stu-id="f5d50-180">Event Grid costs $0.60 per million operations ($0.30 during preview) and hello first 100,000 operation per month are free.</span></span> <span data-ttu-id="f5d50-181">Bewerkingen worden gedefinieerd als gebeurtenis inkomend, geavanceerde overeen, levering poging en management aanroepen.</span><span class="sxs-lookup"><span data-stu-id="f5d50-181">Operations are defined as event ingress, advanced match, delivery attempt, and management calls.</span></span>  <span data-ttu-id="f5d50-182">Meer informatie vindt u op Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/event-grid/).</span><span class="sxs-lookup"><span data-stu-id="f5d50-182">More details can be found on hello [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5d50-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f5d50-183">Next steps</span></span>

* <span data-ttu-id="f5d50-184">[Maken en zich abonneren toocustom gebeurtenissen](custom-event-quickstart.md) meteen en beginnen met het verzenden van uw eigen aangepaste gebeurtenissen tooany eindpunt met behulp van hello Azure gebeurtenis raster Quick Start.</span><span class="sxs-lookup"><span data-stu-id="f5d50-184">[Create and subscribe toocustom events](custom-event-quickstart.md) Jump right in and start sending your own custom events tooany endpoint using hello Azure Event Grid quickstart.</span></span>
* <span data-ttu-id="f5d50-185">[Met Logic Apps als een gebeurtenis-Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) een zelfstudie over het bouwen van een app met Logic Apps tooreact tooevents gepusht door gebeurtenis raster.</span><span class="sxs-lookup"><span data-stu-id="f5d50-185">[Using Logic Apps as an Event Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) A tutorial on building an app using Logic Apps tooreact tooevents pushed by Event Grid.</span></span>
* [<span data-ttu-id="f5d50-186">Gebeurtenis raster REST API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="f5d50-186">Event Grid REST API reference</span></span>](/rest/api/eventgrid)  
  <span data-ttu-id="f5d50-187">Biedt meer technische informatie over hello Azure gebeurtenis raster en een verwijzing voor het beheer van abonnementen, doorsturen en filteren.</span><span class="sxs-lookup"><span data-stu-id="f5d50-187">Provides more technical information about hello Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span></span>
