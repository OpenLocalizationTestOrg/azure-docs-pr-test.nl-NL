---
title: Service Fabric-services aaaPartitioning | Microsoft Docs
description: Hierin wordt beschreven hoe toopartition Service Fabric stateful services. Partities kunnen de opslag van gegevens op de lokale machines Hallo zodat gegevens en rekencapaciteit samen kunnen worden geschaald.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="e0161-104">Betrouwbare partitie Service Fabric-services</span><span class="sxs-lookup"><span data-stu-id="e0161-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="e0161-105">Dit artikel bevat een inleiding toohello basisconcepten van Azure Service Fabric betrouwbare services partitioneren.</span><span class="sxs-lookup"><span data-stu-id="e0161-105">This article provides an introduction toohello basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="e0161-106">Hallo broncode gebruikt in Hallo artikel is ook beschikbaar op [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="e0161-106">hello source code used in hello article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="e0161-107">Partitionering</span><span class="sxs-lookup"><span data-stu-id="e0161-107">Partitioning</span></span>
<span data-ttu-id="e0161-108">Partitioneren is niet uniek tooService Fabric.</span><span class="sxs-lookup"><span data-stu-id="e0161-108">Partitioning is not unique tooService Fabric.</span></span> <span data-ttu-id="e0161-109">Het is in feite een patroon core van het bouwen van schaalbare services.</span><span class="sxs-lookup"><span data-stu-id="e0161-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="e0161-110">We kunnen in een ruimere zin nadenken over partitioneren als een concept van het delen van status (gegevens) en compute in kleinere eenheden toegankelijk tooimprove schaalbaarheid en prestaties.</span><span class="sxs-lookup"><span data-stu-id="e0161-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units tooimprove scalability and performance.</span></span> <span data-ttu-id="e0161-111">Is een bekende formulier van het partitioneren van [partitioneren van gegevens][wikipartition], ook wel aangeduid als sharding.</span><span class="sxs-lookup"><span data-stu-id="e0161-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="e0161-112">Partitie Service Fabric stateless services</span><span class="sxs-lookup"><span data-stu-id="e0161-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="e0161-113">U kunt een partitie wordt een logische eenheid met een of meer exemplaren van een service bedenken voor stateless services.</span><span class="sxs-lookup"><span data-stu-id="e0161-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="e0161-114">Afbeelding 1 toont een stateless service met vijf exemplaren verdeeld over een cluster met één partitie.</span><span class="sxs-lookup"><span data-stu-id="e0161-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![Staatloze service](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="e0161-116">Er zijn in feite twee soorten stateless Services-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="e0161-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="e0161-117">Hallo eerst is een een service die de status extern, bijvoorbeeld zich blijft voordoen in een Azure SQL database (zoals een website die Hallo sessie-informatie en gegevens worden opgeslagen).</span><span class="sxs-lookup"><span data-stu-id="e0161-117">hello first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores hello session information and data).</span></span> <span data-ttu-id="e0161-118">Hallo is tweede alleen-berekeningen services (zoals een miniatuur Rekenmachine of afbeelding) die geen permanente status niet beheren.</span><span class="sxs-lookup"><span data-stu-id="e0161-118">hello second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="e0161-119">Ofwel in geval een stateless service partitioneren is een zeldzame scenario--schaalbaarheid en beschikbaarheid normaal worden bereikt door meer exemplaren toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="e0161-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="e0161-120">Hallo enige keer dat u wilt dat meerdere partities voor stateless service-exemplaren is wanneer u toomeet speciale routering tooconsider aanvragen.</span><span class="sxs-lookup"><span data-stu-id="e0161-120">hello only time you want tooconsider multiple partitions for stateless service instances is when you need toomeet special routing requests.</span></span>

<span data-ttu-id="e0161-121">Een voorbeeld kunt u een aanvraag waarin gebruikers met de id's in een bepaald bereik moeten alleen worden geleverd door een bepaalde service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="e0161-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="e0161-122">Een ander voorbeeld van wanneer u een stateless service kan partitioneren is wanneer u een echt gepartitioneerde back-end (bijvoorbeeld een shard SQL-database) en u wilt dat toocontrol welk service-exemplaar moet schrijven toohello database shard-- of andere taken voorbereiding binnen Hallo staatloze service waarvoor Hallo dezelfde partitiegegevens, zoals wordt gebruikt in Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="e0161-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want toocontrol which service instance should write toohello database shard--or perform other preparation work within hello stateless service that requires hello same partitioning information as is used in hello backend.</span></span> <span data-ttu-id="e0161-123">Dergelijke scenario's kunnen ook op verschillende manieren worden opgelost en niet noodzakelijk partitioneren van de service.</span><span class="sxs-lookup"><span data-stu-id="e0161-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="e0161-124">Hallo rest van dit scenario ligt de nadruk op stateful services.</span><span class="sxs-lookup"><span data-stu-id="e0161-124">hello remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="e0161-125">Partitie Service Fabric stateful services</span><span class="sxs-lookup"><span data-stu-id="e0161-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="e0161-126">Service Fabric maakt het eenvoudig toodevelop schaalbare stateful services door het aanbieden van een uitstekende manier toopartition status (gegevens).</span><span class="sxs-lookup"><span data-stu-id="e0161-126">Service Fabric makes it easy toodevelop scalable stateful services by offering a first-class way toopartition state (data).</span></span> <span data-ttu-id="e0161-127">Conceptueel gezien u over een partitie van een stateful service kunt beschouwen als een schaaleenheid die zeer betrouwbaar via [replica's](service-fabric-availability-services.md) die zijn gedistribueerd en verdeeld zijn over Hallo knooppunten in een cluster.</span><span class="sxs-lookup"><span data-stu-id="e0161-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across hello nodes in a cluster.</span></span>

<span data-ttu-id="e0161-128">In de context van Service Fabric stateful services Hallo partitioneren verwijst toohello proces om te bepalen dat een bepaalde service partitie verantwoordelijk voor een deel van de volledige status Hallo van Hallo-service is.</span><span class="sxs-lookup"><span data-stu-id="e0161-128">Partitioning in hello context of Service Fabric stateful services refers toohello process of determining that a particular service partition is responsible for a portion of hello complete state of hello service.</span></span> <span data-ttu-id="e0161-129">(Zoals al eerder vermeld, een partitie is een reeks [replica's](service-fabric-availability-services.md)).</span><span class="sxs-lookup"><span data-stu-id="e0161-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="e0161-130">Een aardige van Service Fabric is Hallo partities geplaatst op verschillende knooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0161-130">A great thing about Service Fabric is that it places hello partitions on different nodes.</span></span> <span data-ttu-id="e0161-131">Hierdoor kunnen ze toogrow tooa knooppunt resource limiet.</span><span class="sxs-lookup"><span data-stu-id="e0161-131">This allows them toogrow tooa node's resource limit.</span></span> <span data-ttu-id="e0161-132">Wanneer gegevens Hallo groeien behoeften, groeien partities en Service Fabric rebalances partities over knooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0161-132">As hello data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="e0161-133">Dit zorgt ervoor Hallo voortgezet hardwarebronnen efficiënt worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e0161-133">This ensures hello continued efficient use of hardware resources.</span></span>

<span data-ttu-id="e0161-134">toogive u bijvoorbeeld dat u begint met een 5-node cluster en een service die is geconfigureerd toohave 10 partities en een doel van drie replica's.</span><span class="sxs-lookup"><span data-stu-id="e0161-134">toogive you an example, say you start with a 5-node cluster and a service that is configured toohave 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="e0161-135">In dit geval Service Fabric zou worden verdeeld en Hallo replica's verdelen over Hallo-cluster en zou u uiteindelijk eindigen met twee primaire [replica's](service-fabric-availability-services.md) per knooppunt.</span><span class="sxs-lookup"><span data-stu-id="e0161-135">In this case, Service Fabric would balance and distribute hello replicas across hello cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="e0161-136">Als u nu tooscale uit Hallo too10 clusterknooppunten moet, Service Fabric zou opnieuw verdelen Hallo primaire [replica's](service-fabric-availability-services.md) op alle knooppunten van 10.</span><span class="sxs-lookup"><span data-stu-id="e0161-136">If you now need tooscale out hello cluster too10 nodes, Service Fabric would rebalance hello primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="e0161-137">Op dezelfde manier als u back too5 knooppunten uitgebreide, Service Fabric zou opnieuw verdelen alle Hallo-replica's op Hallo 5-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="e0161-137">Likewise, if you scaled back too5 nodes, Service Fabric would rebalance all hello replicas across hello 5 nodes.</span></span>  

<span data-ttu-id="e0161-138">Afbeelding 2 toont de distributie van de Hallo van 10 partities voor en na het Hallo-cluster schalen.</span><span class="sxs-lookup"><span data-stu-id="e0161-138">Figure 2 shows hello distribution of 10 partitions before and after scaling hello cluster.</span></span>

![Stateful service](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="e0161-140">Hallo scale-out wordt hierdoor bereikt omdat aanvragen van clients worden verdeeld over computers, algehele prestaties van de toepassing hello is verbeterd en conflicten op toegang toochunks van gegevens wordt verminderd.</span><span class="sxs-lookup"><span data-stu-id="e0161-140">As a result, hello scale-out is achieved since requests from clients are distributed across computers, overall performance of hello application is improved, and contention on access toochunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="e0161-141">Plan voor het partitioneren</span><span class="sxs-lookup"><span data-stu-id="e0161-141">Plan for partitioning</span></span>
<span data-ttu-id="e0161-142">Voordat u een service implementeert, moet u altijd Hallo-strategie is vereist tooscale uit partitioneren overwegen. Er zijn verschillende manieren, maar ze allemaal ligt de nadruk op welke toepassing hello tooachieve moet.</span><span class="sxs-lookup"><span data-stu-id="e0161-142">Before implementing a service, you should always consider hello partitioning strategy that is required tooscale out. There are different ways, but all of them focus on what hello application needs tooachieve.</span></span> <span data-ttu-id="e0161-143">Hallo-context van dit artikel, laten we eens enkele Hallo meer belangrijke aspecten.</span><span class="sxs-lookup"><span data-stu-id="e0161-143">For hello context of this article, let's consider some of hello more important aspects.</span></span>

<span data-ttu-id="e0161-144">Een goede benadering is toothink over Hallo-structuur van Hallo status die is gepartitioneerd, als de eerste stap Hallo toobe nodig.</span><span class="sxs-lookup"><span data-stu-id="e0161-144">A good approach is toothink about hello structure of hello state that needs toobe partitioned, as hello first step.</span></span>

<span data-ttu-id="e0161-145">U gaat nu een eenvoudig voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e0161-145">Let's take a simple example.</span></span> <span data-ttu-id="e0161-146">Als u een service voor een countywide poll toobuild was, kunt u een partitie voor elke stad in Hallo regio kunt maken.</span><span class="sxs-lookup"><span data-stu-id="e0161-146">If you were toobuild a service for a countywide poll, you could create a partition for each city in hello county.</span></span> <span data-ttu-id="e0161-147">Vervolgens kunt u Hallo stemmen voor elke persoon opslaan in plaats van Hallo in Hallo partitie die overeenkomt met toothat plaats.</span><span class="sxs-lookup"><span data-stu-id="e0161-147">Then, you could store hello votes for every person in hello city in hello partition that corresponds toothat city.</span></span> <span data-ttu-id="e0161-148">Afbeelding 3 ziet u een set van mensen en Hallo plaats waar ze zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="e0161-148">Figure 3 illustrates a set of people and hello city in which they reside.</span></span>

![Eenvoudige partitie](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="e0161-150">Als Hallo populatie steden varieert, zou u uiteindelijk met een aantal partities met een grote hoeveelheid gegevens (bijvoorbeeld Haarlem) en andere partities met weinig status (bijvoorbeeld Kirkland).</span><span class="sxs-lookup"><span data-stu-id="e0161-150">As hello population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="e0161-151">Wat is Hallo impact van partities met ongelijke hoeveelheden status hebben?</span><span class="sxs-lookup"><span data-stu-id="e0161-151">So what is hello impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="e0161-152">Als u opnieuw over Hallo voorbeeld denkt, kunt u eenvoudig hello partitie waarin Hallo stemmen voor Seattle krijgt meer verkeer dan Hallo Kirkland een bekijken.</span><span class="sxs-lookup"><span data-stu-id="e0161-152">If you think about hello example again, you can easily see that hello partition that holds hello votes for Seattle will get more traffic than hello Kirkland one.</span></span> <span data-ttu-id="e0161-153">Service Fabric maakt standaard ervoor dat er over Hallo hetzelfde aantal primaire en secundaire replica's op elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="e0161-153">By default, Service Fabric makes sure that there is about hello same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="e0161-154">Zo zou u uiteindelijk met knooppunten die fungeren als replica's die dienen meer verkeer en anderen die minder verkeer dienen houdt.</span><span class="sxs-lookup"><span data-stu-id="e0161-154">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="e0161-155">U zou bij voorkeur wilt tooavoid warme en koude plaatsen zoals deze in een cluster.</span><span class="sxs-lookup"><span data-stu-id="e0161-155">You would preferably want tooavoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="e0161-156">In volgorde tooavoid dit, moet u twee dingen doen vanuit het partitionering oogpunt:</span><span class="sxs-lookup"><span data-stu-id="e0161-156">In order tooavoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="e0161-157">Probeer toopartition Hallo status, zodat deze evenredig verdeeld over alle partities.</span><span class="sxs-lookup"><span data-stu-id="e0161-157">Try toopartition hello state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="e0161-158">Rapporteren over de belasting van elk van de replica's Hallo voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="e0161-158">Report load from each of hello replicas for hello service.</span></span> <span data-ttu-id="e0161-159">(Voor meer informatie over het controleren van dit artikel [metrische gegevens en de belasting](service-fabric-cluster-resource-manager-metrics.md)).</span><span class="sxs-lookup"><span data-stu-id="e0161-159">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="e0161-160">Service Fabric bevat Hallo mogelijkheid tooreport load verbruikt door services, zoals de hoeveelheid geheugen of het aantal records.</span><span class="sxs-lookup"><span data-stu-id="e0161-160">Service Fabric provides hello capability tooreport load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="e0161-161">Op basis van Hallo metrische gegevens die zijn gerapporteerd, detecteert Service Fabric dat een aantal partities hogere belasting dan andere fungeren en rebalances Hallo cluster door bewegende replica's toomore geschikte knooppunten, zodat de algemene geen knooppunt is overbelast.</span><span class="sxs-lookup"><span data-stu-id="e0161-161">Based on hello metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances hello cluster by moving replicas toomore suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="e0161-162">Soms weet u niet kunt hoeveel gegevens worden weergegeven in een bepaalde partitie.</span><span class="sxs-lookup"><span data-stu-id="e0161-162">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="e0161-163">Zodat een algemene aanbeveling toodo beide--eerst selecteert door partities die, Hallo gegevens gelijkmatig over Hallo partities en de tweede pagina, met reporting laden.</span><span class="sxs-lookup"><span data-stu-id="e0161-163">So a general recommendation is toodo both--first, by adopting a partitioning strategy that spreads hello data evenly across hello partitions and second, by reporting load.</span></span>  <span data-ttu-id="e0161-164">de eerste methode Hallo voorkomt situaties beschreven in Hallo bijvoorbeeld stemmen terwijl Hallo tweede vloeiend maken tijdelijke verschillen in access of load gedurende een bepaalde periode helpt.</span><span class="sxs-lookup"><span data-stu-id="e0161-164">hello first method prevents situations described in hello voting example, while hello second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="e0161-165">Een ander aspect van de planning van de partitie is toochoose Hallo juiste aantal partities toobegin met.</span><span class="sxs-lookup"><span data-stu-id="e0161-165">Another aspect of partition planning is toochoose hello correct number of partitions toobegin with.</span></span>
<span data-ttu-id="e0161-166">Vanuit het perspectief van een Service Fabric is er niets dat verhindert dat u begint met een hoger aantal partities dan verwacht voor uw scenario.</span><span class="sxs-lookup"><span data-stu-id="e0161-166">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="e0161-167">Ervan uitgaande dat Hallo kunt u het maximum aantal partities is in feite een geldige benadering.</span><span class="sxs-lookup"><span data-stu-id="e0161-167">In fact, assuming hello maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="e0161-168">In zeldzame gevallen, zou u uiteindelijk hoeven meer partities dan u oorspronkelijk hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="e0161-168">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="e0161-169">Zoals u kunt Hallo partitie aantal niet wijzigen nadat Hallo feit, moet u tooapply sommige geavanceerde partitie benaderingen, zoals het maken van een nieuwe service-exemplaar Hallo dezelfde servicetype.</span><span class="sxs-lookup"><span data-stu-id="e0161-169">As you cannot change hello partition count after hello fact, you would need tooapply some advanced partition approaches, such as creating a new service instance of hello same service type.</span></span> <span data-ttu-id="e0161-170">U moet tevens tooimplement bepaalde clientzijde logica die Hallo routeert toohello juiste service-exemplaar aanvragen, gebaseerd op kennis van clientzijde die u ervoor dat uw clientcode zorgen moet.</span><span class="sxs-lookup"><span data-stu-id="e0161-170">You would also need tooimplement some client-side logic that routes hello requests toohello correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="e0161-171">Andere overweging voor het partitioneren van de planning is Hallo beschikbare computerbronnen.</span><span class="sxs-lookup"><span data-stu-id="e0161-171">Another consideration for partitioning planning is hello available computer resources.</span></span> <span data-ttu-id="e0161-172">Als het Hallo-status moet toobe toegankelijk is en opgeslagen, zijn gebonden toofollow:</span><span class="sxs-lookup"><span data-stu-id="e0161-172">As hello state needs toobe accessed and stored, you are bound toofollow:</span></span>

* <span data-ttu-id="e0161-173">Netwerk bandbreedtelimieten</span><span class="sxs-lookup"><span data-stu-id="e0161-173">Network bandwidth limits</span></span>
* <span data-ttu-id="e0161-174">Systeem geheugenlimieten</span><span class="sxs-lookup"><span data-stu-id="e0161-174">System memory limits</span></span>
* <span data-ttu-id="e0161-175">Schijf opslaglimieten</span><span class="sxs-lookup"><span data-stu-id="e0161-175">Disk storage limits</span></span>

<span data-ttu-id="e0161-176">Wat gebeurt zodat er als u in resourcebeperkingen in een actief cluster uitvoert? Hallo-antwoord is dat u kunt gewoon worden uitgebreid Hallo cluster tooaccommodate Hallo nieuwe vereisten.</span><span class="sxs-lookup"><span data-stu-id="e0161-176">So what happens if you run into resource constraints in a running cluster? hello answer is that you can simply scale out hello cluster tooaccommodate hello new requirements.</span></span>

<span data-ttu-id="e0161-177">[handleiding voor capaciteitsplanning Hallo](service-fabric-capacity-planning.md) biedt richtlijnen voor het toodetermine hoeveel knooppunten uw cluster moet.</span><span class="sxs-lookup"><span data-stu-id="e0161-177">[hello capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how toodetermine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="e0161-178">Aan de slag met partitioneren</span><span class="sxs-lookup"><span data-stu-id="e0161-178">Get started with partitioning</span></span>
<span data-ttu-id="e0161-179">Deze sectie beschrijft hoe tooget gestart met het partitioneren van uw service.</span><span class="sxs-lookup"><span data-stu-id="e0161-179">This section describes how tooget started with partitioning your service.</span></span>

<span data-ttu-id="e0161-180">Service Fabric biedt een keuze uit drie partitieschema's:</span><span class="sxs-lookup"><span data-stu-id="e0161-180">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="e0161-181">Varieerden partitioneren (anders UniformInt64Partition genoemd).</span><span class="sxs-lookup"><span data-stu-id="e0161-181">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="e0161-182">Met de naam partitioneren.</span><span class="sxs-lookup"><span data-stu-id="e0161-182">Named partitioning.</span></span> <span data-ttu-id="e0161-183">Toepassingen die gebruikmaken van dit model meestal beschikken over gegevens die kunnen worden bucketed binnen een begrensde set.</span><span class="sxs-lookup"><span data-stu-id="e0161-183">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="e0161-184">Enkele algemene voorbeelden van gegevensvelden gebruikt als benoemde partitiesleutels zou worden regio's, postcode codes, klantengroepen of andere zakelijke grenzen.</span><span class="sxs-lookup"><span data-stu-id="e0161-184">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="e0161-185">Singleton partitioneren.</span><span class="sxs-lookup"><span data-stu-id="e0161-185">Singleton partitioning.</span></span> <span data-ttu-id="e0161-186">Singleton-partities worden meestal gebruikt wanneer het Hallo-service vereist geen aanvullende routering.</span><span class="sxs-lookup"><span data-stu-id="e0161-186">Singleton partitions are typically used when hello service does not require any additional routing.</span></span> <span data-ttu-id="e0161-187">Bijvoorbeeld, stateless services deze partitieschema standaard gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e0161-187">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="e0161-188">Met de naam en partitionering Singleton-schema's zijn speciale soorten varieerde partities.</span><span class="sxs-lookup"><span data-stu-id="e0161-188">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="e0161-189">Standaard varieerden Hallo Visual Studio-sjablonen voor Service Fabric gebruik partitioneren, omdat deze Hallo veelgebruikte en handige één.</span><span class="sxs-lookup"><span data-stu-id="e0161-189">By default, hello Visual Studio templates for Service Fabric use ranged partitioning, as it is hello most common and useful one.</span></span> <span data-ttu-id="e0161-190">Hallo rest van dit artikel is gericht op Hallo varieerde partitieschema.</span><span class="sxs-lookup"><span data-stu-id="e0161-190">hello remainder of this article focuses on hello ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="e0161-191">Partitieschema varieerde</span><span class="sxs-lookup"><span data-stu-id="e0161-191">Ranged partitioning scheme</span></span>
<span data-ttu-id="e0161-192">Dit is een geheel getal van gebruikte toospecify bereik (aangeduid met een lage en hoge sleutel) en een aantal partities (n).</span><span class="sxs-lookup"><span data-stu-id="e0161-192">This is used toospecify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="e0161-193">Het maken van n partities, elke verantwoordelijk is voor een niet-overlappende subbereik Hallo algemene partitie sleutel bereik.</span><span class="sxs-lookup"><span data-stu-id="e0161-193">It creates n partitions, each responsible for a non-overlapping subrange of hello overall partition key range.</span></span> <span data-ttu-id="e0161-194">Bijvoorbeeld, een ranged partitieschema met een lage sleutel 0, een hoge sleutel 99 en een telling van 4 maakt vier partities zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e0161-194">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![Bereik partitioneren](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="e0161-196">Een veelgebruikte oplossing is toocreate een hash op basis van een unieke sleutel in Hallo-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="e0161-196">A common approach is toocreate a hash based on a unique key within hello data set.</span></span> <span data-ttu-id="e0161-197">Enkele algemene voorbeelden van sleutels is een vehicle id-nummer (VIN), een werknemer-ID of een unieke tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="e0161-197">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="e0161-198">Met behulp van deze unieke sleutel, zou u vervolgens een hash-code, modulus Hallo sleutel bereik, toouse als uw sleutel gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="e0161-198">By using this unique key, you would then generate a hash code, modulus hello key range, toouse as your key.</span></span> <span data-ttu-id="e0161-199">U kunt Hallo bovenste en de ondergrenzen Hallo het toegestane bereik sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="e0161-199">You can specify hello upper and lower bounds of hello allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="e0161-200">Selecteer een hash-algoritme</span><span class="sxs-lookup"><span data-stu-id="e0161-200">Select a hash algorithm</span></span>
<span data-ttu-id="e0161-201">Een belangrijk onderdeel van het hash-selecteert hash-algoritme.</span><span class="sxs-lookup"><span data-stu-id="e0161-201">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="e0161-202">Overweging is of Hallo doel toogroup vergelijkbare sleutels in de buurt van elkaar (plaats gevoelige hashing)--is of als activiteit moet op grote schaal worden gedistribueerd voor alle partities (hash-distributie), waarmee veelvoorkomende is.</span><span class="sxs-lookup"><span data-stu-id="e0161-202">A consideration is whether hello goal is toogroup similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="e0161-203">Hallo kenmerken van een goede distributie hash-algoritme zijn dat het eenvoudig toocompute is, enkele conflicten heeft en het Hallo-sleutels gelijkmatig worden verdeeld.</span><span class="sxs-lookup"><span data-stu-id="e0161-203">hello characteristics of a good distribution hashing algorithm are that it is easy toocompute, it has few collisions, and it distributes hello keys evenly.</span></span> <span data-ttu-id="e0161-204">Een goed voorbeeld van een efficiënte hash-algoritme is Hallo [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash-algoritme.</span><span class="sxs-lookup"><span data-stu-id="e0161-204">A good example of an efficient hash algorithm is hello [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="e0161-205">Een goede resource voor algemene hash-code algoritme die is Hallo [pagina Wikipedia (Engelstalig) op de hash-functies](http://en.wikipedia.org/wiki/Hash_function).</span><span class="sxs-lookup"><span data-stu-id="e0161-205">A good resource for general hash code algorithm choices is hello [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="e0161-206">Een stateful service met meerdere partities bouwen</span><span class="sxs-lookup"><span data-stu-id="e0161-206">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="e0161-207">Stel uw eerste betrouwbare stateful service maken met meerdere partities.</span><span class="sxs-lookup"><span data-stu-id="e0161-207">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="e0161-208">In dit voorbeeld maakt u een zeer eenvoudige toepassing waar u toostore alle laatste namen die beginnen met dezelfde stationsletter in Hallo Hallo dezelfde partitie.</span><span class="sxs-lookup"><span data-stu-id="e0161-208">In this example, you will build a very simple application where you want toostore all last names that start with hello same letter in hello same partition.</span></span>

<span data-ttu-id="e0161-209">Voordat u een code te schrijven, moet u toothink over Hallo partities en partitiesleutels.</span><span class="sxs-lookup"><span data-stu-id="e0161-209">Before you write any code, you need toothink about hello partitions and partition keys.</span></span> <span data-ttu-id="e0161-210">Moet u 26 partities (één voor elke letter in Hallo alfabet), maar wat over lage en hoge sleutels Hallo?</span><span class="sxs-lookup"><span data-stu-id="e0161-210">You need 26 partitions (one for each letter in hello alphabet), but what about hello low and high keys?</span></span>
<span data-ttu-id="e0161-211">Als we letterlijk toohave één partitie per letter willen, kunt we gebruiken 0 als de lage sleutelwaarde Hallo en 25 als Hallo hoge sleutel, omdat elke letter een eigen sleutel.</span><span class="sxs-lookup"><span data-stu-id="e0161-211">As we literally want toohave one partition per letter, we can use 0 as hello low key and 25 as hello high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="e0161-212">Dit is een vereenvoudigde scenario in werkelijkheid Hallo distributie ongelijke zou zijn.</span><span class="sxs-lookup"><span data-stu-id="e0161-212">This is a simplified scenario, as in reality hello distribution would be uneven.</span></span> <span data-ttu-id="e0161-213">Laatste namen die beginnen met Hallo letters "S" of ''M' komen vaker dan Hallo die beginnen met 'X' of 'Y'.</span><span class="sxs-lookup"><span data-stu-id="e0161-213">Last names starting with hello letters "S" or "M" are more common than hello ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="e0161-214">Open **Visual Studio** > **bestand** > **nieuwe** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="e0161-214">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="e0161-215">In Hallo **nieuw Project** dialoogvenster Kies Hallo Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e0161-215">In hello **New Project** dialog box, choose hello Service Fabric application.</span></span>
3. <span data-ttu-id="e0161-216">Hallo project 'AlphabetPartitions' aanroepen.</span><span class="sxs-lookup"><span data-stu-id="e0161-216">Call hello project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="e0161-217">In Hallo **maken van een Service** dialoogvenster Kies **Stateful** service en deze aanroepen 'Alphabet.Processing' zoals wordt weergegeven in onderstaande Hallo-afbeelding.</span><span class="sxs-lookup"><span data-stu-id="e0161-217">In hello **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in hello image below.</span></span>
       <span data-ttu-id="e0161-218">![Dialoogvenster voor nieuwe service in Visual Studio][1]</span><span class="sxs-lookup"><span data-stu-id="e0161-218">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="e0161-219">Het aantal partities Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="e0161-219">Set hello number of partitions.</span></span> <span data-ttu-id="e0161-220">Open Hallo Applicationmanifest.xml bestand zich in Hallo ApplicationPackageRoot map van Hallo AlphabetPartitions project en update Hallo parameter Processing_PartitionCount too26 zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e0161-220">Open hello Applicationmanifest.xml file located in hello ApplicationPackageRoot folder of hello AlphabetPartitions project and update hello parameter Processing_PartitionCount too26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="e0161-221">U moet ook tooupdate hello LowKey en HighKey eigenschappen van Hallo StatefulService element in Hallo ApplicationManifest.xml zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e0161-221">You also need tooupdate hello LowKey and HighKey properties of hello StatefulService element in hello ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="e0161-222">Voor Hallo service toobe toegankelijk is, opent u een eindpunt op een poort door toe te voegen Hallo eindpuntelement van ServiceManifest.xml (te vinden in Hallo PackageRoot map) voor Hallo Alphabet.Processing service zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e0161-222">For hello service toobe accessible, open up an endpoint on a port by adding hello endpoint element of ServiceManifest.xml (located in hello PackageRoot folder) for hello Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="e0161-223">Hallo-service is nu geconfigureerd toolisten tooan interne eindpunt met 26 partities.</span><span class="sxs-lookup"><span data-stu-id="e0161-223">Now hello service is configured toolisten tooan internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="e0161-224">Vervolgens moet u toooverride hello `CreateServiceReplicaListeners()` methode van Hallo verwerking klasse.</span><span class="sxs-lookup"><span data-stu-id="e0161-224">Next, you need toooverride hello `CreateServiceReplicaListeners()` method of hello Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e0161-225">Voor dit voorbeeld nemen we aan dat u van een eenvoudige HttpCommunicationListener gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="e0161-225">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="e0161-226">Zie voor meer informatie over betrouwbare servicecommunicatie [Hallo-communicatie van betrouwbare servicemodel](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="e0161-226">For more information on reliable service communication, see [hello Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="e0161-227">Een aanbevolen patroon voor Hallo-URL die een replica luistert op Hallo na indeling is: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span><span class="sxs-lookup"><span data-stu-id="e0161-227">A recommended pattern for hello URL that a replica listens on is hello following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="e0161-228">Zodat u tooconfigure uw communicatie-listener toolisten op de juiste eindpunten Hallo en met dit patroon.</span><span class="sxs-lookup"><span data-stu-id="e0161-228">So you want tooconfigure your communication listener toolisten on hello correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="e0161-229">Meerdere replica's van deze service kunnen worden gehost op Hallo dezelfde computer, zodat dit adres toobe unieke toohello replica moet.</span><span class="sxs-lookup"><span data-stu-id="e0161-229">Multiple replicas of this service may be hosted on hello same computer, so this address needs toobe unique toohello replica.</span></span> <span data-ttu-id="e0161-230">Daarom partitie-ID + replica-ID in Hallo-URL zijn.</span><span class="sxs-lookup"><span data-stu-id="e0161-230">This is why   partition ID + replica ID are in hello URL.</span></span> <span data-ttu-id="e0161-231">HttpListener kan luisteren op meerdere adressen op Hallo die dezelfde poort als Hallo URL-voorvoegsel uniek is.</span><span class="sxs-lookup"><span data-stu-id="e0161-231">HttpListener can listen on multiple addresses on hello same port as long as hello URL prefix    is unique.</span></span>
   
    <span data-ttu-id="e0161-232">Hallo die extra GUID is er voor een geavanceerde aanvraag waarop secundaire replica's ook voor alleen-lezen-aanvragen luisteren.</span><span class="sxs-lookup"><span data-stu-id="e0161-232">hello extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="e0161-233">Wanneer dit Hallo geval is, wilt u ervoor dat er een nieuw uniek adres wordt gebruikt tijdens het veranderen van primaire toosecondary tooforce clients toore oplossen Hallo adres toomake.</span><span class="sxs-lookup"><span data-stu-id="e0161-233">When that's hello case, you want toomake sure that a new unique address is used when transitioning from primary toosecondary tooforce clients toore-resolve hello address.</span></span> <span data-ttu-id="e0161-234">'+' wordt gebruikt als Hallo adres hier zodat hello replica op alle beschikbare hosts (IP-, FQDM, ' localhost ', enz.) Hallo code hieronder luistert ziet u een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e0161-234">'+' is used as hello address here so that hello replica listens on all available hosts (IP, FQDM, localhost, etc.) hello code below shows an example.</span></span>
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    <span data-ttu-id="e0161-235">Het verdient aanbeveling ook weten dat Hallo gepubliceerde URL verschilt enigszins van Hallo luisterende URL-voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="e0161-235">It's also worth noting that hello published URL is slightly different from hello listening URL prefix.</span></span>
    <span data-ttu-id="e0161-236">Hallo luisterende URL tooHttpListener krijgt.</span><span class="sxs-lookup"><span data-stu-id="e0161-236">hello listening URL is given tooHttpListener.</span></span> <span data-ttu-id="e0161-237">Hallo die gepubliceerde URL is Hallo-URL die is gepubliceerd toohello Service Fabric Naming Service, die wordt gebruikt voor servicedetectie.</span><span class="sxs-lookup"><span data-stu-id="e0161-237">hello published URL is hello URL that is published toohello Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="e0161-238">Clients vragen voor dit adres via die discovery-service.</span><span class="sxs-lookup"><span data-stu-id="e0161-238">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="e0161-239">Hallo-adres dat clients behoeften toohave Hallo werkelijke IP of FQDN van Hallo-knooppunt in de volgorde tooconnect ophalen.</span><span class="sxs-lookup"><span data-stu-id="e0161-239">hello address that clients get needs toohave hello actual IP or FQDN of hello node in order tooconnect.</span></span> <span data-ttu-id="e0161-240">Daarom tooreplace '+' met Hallo van het knooppunt IP of FQDN-naam zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="e0161-240">So you need tooreplace '+' with hello node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="e0161-241">de laatste stap Hallo is tooadd Hallo verwerken logica toohello service zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e0161-241">hello last step is tooadd hello processing logic toohello service as shown below.</span></span>
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    <span data-ttu-id="e0161-242">`ProcessInternalRequest`leesbewerkingen Hallo waarden van Hallo query tekenreeks parameter gebruikt toocall Hallo partitie en aanroepen `AddUserAsync` tooadd Hallo lastname toohello betrouwbare woordenlijst `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="e0161-242">`ProcessInternalRequest` reads hello values of hello query string parameter used toocall hello partition and calls `AddUserAsync` tooadd hello lastname toohello reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="e0161-243">We voegen een stateless service toohello project toosee hoe u een bepaalde partitie kunt aanroepen.</span><span class="sxs-lookup"><span data-stu-id="e0161-243">Let's add a stateless service toohello project toosee how you can call a particular partition.</span></span>
    
    <span data-ttu-id="e0161-244">Deze service fungeert als een eenvoudige webinterface die Hallo lastname als een queryreeksparameter accepteert, bepaalt de partitiesleutel Hallo en verzendt het toohello Alphabet.Processing service voor de verwerking.</span><span class="sxs-lookup"><span data-stu-id="e0161-244">This service serves as a simple web interface that accepts hello lastname as a query string parameter, determines hello partition key, and sends it toohello Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="e0161-245">In Hallo **maken van een Service** dialoogvenster Kies **Stateless** service en deze aanroepen 'Alphabet.Web' zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e0161-245">In hello **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![Schermopname van staatloze service](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="e0161-247">.</span><span class="sxs-lookup"><span data-stu-id="e0161-247">.</span></span>
12. <span data-ttu-id="e0161-248">Hallo eindpuntinformatie in Hallo ServiceManifest.xml van Hallo Alphabet.WebApi service tooopen van een poort zoals hieronder wordt weergegeven bijwerken.</span><span class="sxs-lookup"><span data-stu-id="e0161-248">Update hello endpoint information in hello ServiceManifest.xml of hello Alphabet.WebApi service tooopen up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="e0161-249">U moet een verzameling van ServiceInstanceListeners in Hallo klasse Web tooreturn.</span><span class="sxs-lookup"><span data-stu-id="e0161-249">You need tooreturn a collection of ServiceInstanceListeners in hello class Web.</span></span> <span data-ttu-id="e0161-250">Nogmaals, kunt u tooimplement een eenvoudige HttpCommunicationListener.</span><span class="sxs-lookup"><span data-stu-id="e0161-250">Again, you can choose tooimplement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="e0161-251">Nu moet u tooimplement Hallo verwerking logica.</span><span class="sxs-lookup"><span data-stu-id="e0161-251">Now you need tooimplement hello processing logic.</span></span> <span data-ttu-id="e0161-252">Hallo HttpCommunicationListener aanroepen `ProcessInputRequest` wanneer een aanvraag binnenkomt.</span><span class="sxs-lookup"><span data-stu-id="e0161-252">hello HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="e0161-253">Dus we gaan nu en voeg Hallo code hieronder.</span><span class="sxs-lookup"><span data-stu-id="e0161-253">So let's go ahead and add hello code below.</span></span>
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="e0161-254">We doorlopen die deze stap voor stap.</span><span class="sxs-lookup"><span data-stu-id="e0161-254">Let's walk through it step by step.</span></span> <span data-ttu-id="e0161-255">Hallo code leest de eerste letter Hallo van Hallo querytekenreeksparameter `lastname` in een tekenset.</span><span class="sxs-lookup"><span data-stu-id="e0161-255">hello code reads hello first letter of hello query string parameter `lastname` into a char.</span></span> <span data-ttu-id="e0161-256">Vervolgens, bepaalt de partitiesleutel Hallo voor deze brief door af te trekken Hallo hexadecimale waarde van `A` van Hallo hexadecimale waarde van de eerste letter Hallo laatste namen.</span><span class="sxs-lookup"><span data-stu-id="e0161-256">Then, it determines hello partition key for this letter by subtracting hello hexadecimal value of `A` from hello hexadecimal value of hello last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="e0161-257">Vergeet niet dat voor dit voorbeeld gebruiken we 26 partities met één partitiesleutel per partitie.</span><span class="sxs-lookup"><span data-stu-id="e0161-257">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="e0161-258">Vervolgens verkrijgen van Hallo service partitie `partition` voor deze sleutel met behulp van Hallo `ResolveAsync` methode op Hallo `servicePartitionResolver` object.</span><span class="sxs-lookup"><span data-stu-id="e0161-258">Next, we obtain hello service partition `partition` for this key by using hello `ResolveAsync` method on hello `servicePartitionResolver` object.</span></span> <span data-ttu-id="e0161-259">`servicePartitionResolver`is gedefinieerd als</span><span class="sxs-lookup"><span data-stu-id="e0161-259">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="e0161-260">Hallo `ResolveAsync` methode vergt Hallo service URI, Hallo partitiesleutel en een token annulering als parameters.</span><span class="sxs-lookup"><span data-stu-id="e0161-260">hello `ResolveAsync` method takes hello service URI, hello partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="e0161-261">Hallo service-URI voor Hallo verwerking van de service is `fabric:/AlphabetPartitions/Processing`.</span><span class="sxs-lookup"><span data-stu-id="e0161-261">hello service URI for hello processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="e0161-262">Vervolgens krijgen we Hallo endpoint van Hallo-partitie.</span><span class="sxs-lookup"><span data-stu-id="e0161-262">Next, we get hello endpoint of hello partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="e0161-263">Ten slotte we Hallo eindpunt-URL plus Hallo querystring bouwen en Hallo verwerking van de service aanroepen.</span><span class="sxs-lookup"><span data-stu-id="e0161-263">Finally, we build hello endpoint URL plus hello querystring and call hello processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="e0161-264">Zodra het Hallo verwerken is voltooid, terugschrijven we Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e0161-264">Once hello processing is done, we write hello output back.</span></span>
15. <span data-ttu-id="e0161-265">de laatste stap Hallo is tootest Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="e0161-265">hello last step is tootest hello service.</span></span> <span data-ttu-id="e0161-266">Visual Studio maakt gebruik van parameters voor de toepassing voor lokale en cloudimplementatie.</span><span class="sxs-lookup"><span data-stu-id="e0161-266">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="e0161-267">met lokaal 26 partities tootest Hallo-service, moet u tooupdate hello `Local.xml` bestand in Hallo ApplicationParameters map van Hallo AlphabetPartitions project, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e0161-267">tootest hello service with 26 partitions locally, you need tooupdate hello `Local.xml` file in hello ApplicationParameters folder of hello AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="e0161-268">Wanneer u klaar bent voor implementatie, kunt u Hallo-service en alle van de partities in Service Fabric Explorer Hallo controleren.</span><span class="sxs-lookup"><span data-stu-id="e0161-268">Once you finish deployment, you can check hello service and all of its partitions in hello Service Fabric Explorer.</span></span>
    
    ![Schermafbeelding van de service Fabric Explorer](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="e0161-270">In een browser, kunt u testen Hallo logica partitioneren door te voeren `http://localhost:8081/?lastname=somename`.</span><span class="sxs-lookup"><span data-stu-id="e0161-270">In a browser, you can test hello partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="e0161-271">U ziet dat elke achternaam op die begint met dezelfde letter worden opgeslagen in Hallo Hallo dezelfde partitie.</span><span class="sxs-lookup"><span data-stu-id="e0161-271">You will see that each last name that starts with hello same letter is being stored in hello same partition.</span></span>
    
    ![Schermafbeelding van de browser](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="e0161-273">Hallo volledige broncode van Hallo voorbeeld is beschikbaar op [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="e0161-273">hello entire source code of hello sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0161-274">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0161-274">Next steps</span></span>
<span data-ttu-id="e0161-275">Zie voor informatie over Service Fabric-concepten Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="e0161-275">For information on Service Fabric concepts, see hello following:</span></span>

* [<span data-ttu-id="e0161-276">Beschikbaarheid van Service Fabric-services</span><span class="sxs-lookup"><span data-stu-id="e0161-276">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="e0161-277">Schaalbaarheid van Service Fabric-services</span><span class="sxs-lookup"><span data-stu-id="e0161-277">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="e0161-278">Capaciteitsplanning voor Service Fabric-toepassingen</span><span class="sxs-lookup"><span data-stu-id="e0161-278">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png