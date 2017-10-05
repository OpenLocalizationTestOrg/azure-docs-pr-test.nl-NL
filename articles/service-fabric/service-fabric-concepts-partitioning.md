---
title: Service Fabric-services partitioneren | Microsoft Docs
description: Beschrijft hoe Service Fabric stateful services partitie. Partities kunnen de opslag van gegevens op de lokale computers zodat u gegevens en rekencapaciteit samen kunnen worden geschaald.
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
ms.openlocfilehash: 3c1e80305cb65f41a6981b99f69e8b87f89599ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="a009d-104">Betrouwbare partitie Service Fabric-services</span><span class="sxs-lookup"><span data-stu-id="a009d-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="a009d-105">Dit artikel bevat een inleiding tot de basisconcepten van Azure Service Fabric betrouwbare services partitioneren.</span><span class="sxs-lookup"><span data-stu-id="a009d-105">This article provides an introduction to the basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="a009d-106">De broncode gebruikt in het artikel is ook beschikbaar op [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="a009d-106">The source code used in the article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="a009d-107">Partitionering</span><span class="sxs-lookup"><span data-stu-id="a009d-107">Partitioning</span></span>
<span data-ttu-id="a009d-108">Partitioneren is niet uniek is voor Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a009d-108">Partitioning is not unique to Service Fabric.</span></span> <span data-ttu-id="a009d-109">Het is in feite een patroon core van het bouwen van schaalbare services.</span><span class="sxs-lookup"><span data-stu-id="a009d-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="a009d-110">We kunnen in een ruimere zin nadenken over partitioneren als een concept van het delen van status (gegevens) en compute in kleinere toegankelijk eenheden schaalbaarheid en prestaties te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="a009d-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units to improve scalability and performance.</span></span> <span data-ttu-id="a009d-111">Is een bekende formulier van het partitioneren van [partitioneren van gegevens][wikipartition], ook wel aangeduid als sharding.</span><span class="sxs-lookup"><span data-stu-id="a009d-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="a009d-112">Partitie Service Fabric stateless services</span><span class="sxs-lookup"><span data-stu-id="a009d-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="a009d-113">U kunt een partitie wordt een logische eenheid met een of meer exemplaren van een service bedenken voor stateless services.</span><span class="sxs-lookup"><span data-stu-id="a009d-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="a009d-114">Afbeelding 1 toont een stateless service met vijf exemplaren verdeeld over een cluster met één partitie.</span><span class="sxs-lookup"><span data-stu-id="a009d-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![Staatloze service](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="a009d-116">Er zijn in feite twee soorten stateless Services-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="a009d-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="a009d-117">De eerste is een service die de status extern, bijvoorbeeld zich blijft voordoen in een Azure SQL database (zoals een website die de sessie-informatie en gegevens worden opgeslagen).</span><span class="sxs-lookup"><span data-stu-id="a009d-117">The first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores the session information and data).</span></span> <span data-ttu-id="a009d-118">Het tweede is alleen-berekeningen services (zoals een miniatuur Rekenmachine of afbeelding) die geen permanente status niet beheren.</span><span class="sxs-lookup"><span data-stu-id="a009d-118">The second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="a009d-119">Ofwel in geval een stateless service partitioneren is een zeldzame scenario--schaalbaarheid en beschikbaarheid normaal worden bereikt door meer exemplaren toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="a009d-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="a009d-120">De enige keer dat u wilt meerdere partities voor stateless service-exemplaren is als u nodig hebt om te voldoen aan speciale routering van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="a009d-120">The only time you want to consider multiple partitions for stateless service instances is when you need to meet special routing requests.</span></span>

<span data-ttu-id="a009d-121">Een voorbeeld kunt u een aanvraag waarin gebruikers met de id's in een bepaald bereik moeten alleen worden geleverd door een bepaalde service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="a009d-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="a009d-122">Een ander voorbeeld van wanneer u een stateless service kan partitioneren is wanneer u een echt gepartitioneerde back-end (bijvoorbeeld een shard SQL-database) en u wilt bepalen welk service-exemplaar moet schrijven naar de database shard-- of andere taken voorbereiding binnen de staatloze service waarvoor partitionering dezelfde informatie als wordt gebruikt in de back-end.</span><span class="sxs-lookup"><span data-stu-id="a009d-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want to control which service instance should write to the database shard--or perform other preparation work within the stateless service that requires the same partitioning information as is used in the backend.</span></span> <span data-ttu-id="a009d-123">Dergelijke scenario's kunnen ook op verschillende manieren worden opgelost en niet noodzakelijk partitioneren van de service.</span><span class="sxs-lookup"><span data-stu-id="a009d-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="a009d-124">De rest van dit scenario ligt de nadruk op stateful services.</span><span class="sxs-lookup"><span data-stu-id="a009d-124">The remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="a009d-125">Partitie Service Fabric stateful services</span><span class="sxs-lookup"><span data-stu-id="a009d-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="a009d-126">Service Fabric kunt eenvoudig ontwikkelen van schaalbare stateful services door het aanbieden van een uitstekende manier om de partitie-status (gegevens).</span><span class="sxs-lookup"><span data-stu-id="a009d-126">Service Fabric makes it easy to develop scalable stateful services by offering a first-class way to partition state (data).</span></span> <span data-ttu-id="a009d-127">Conceptueel gezien u over een partitie van een stateful service kunt beschouwen als een schaaleenheid die zeer betrouwbaar via [replica's](service-fabric-availability-services.md) die zijn gedistribueerd en verdeeld zijn over de knooppunten in een cluster.</span><span class="sxs-lookup"><span data-stu-id="a009d-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across the nodes in a cluster.</span></span>

<span data-ttu-id="a009d-128">In de context van de Service Fabric stateful services partitioneren verwijst naar het proces om te bepalen dat een bepaalde service partitie verantwoordelijk voor een deel van de volledige status van de service is.</span><span class="sxs-lookup"><span data-stu-id="a009d-128">Partitioning in the context of Service Fabric stateful services refers to the process of determining that a particular service partition is responsible for a portion of the complete state of the service.</span></span> <span data-ttu-id="a009d-129">(Zoals al eerder vermeld, een partitie is een reeks [replica's](service-fabric-availability-services.md)).</span><span class="sxs-lookup"><span data-stu-id="a009d-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="a009d-130">Een aardige van Service Fabric is dat de partities wordt geplaatst op verschillende knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a009d-130">A great thing about Service Fabric is that it places the partitions on different nodes.</span></span> <span data-ttu-id="a009d-131">Hierdoor kunnen ze toe aan een knooppunt resource limiet.</span><span class="sxs-lookup"><span data-stu-id="a009d-131">This allows them to grow to a node's resource limit.</span></span> <span data-ttu-id="a009d-132">Wanneer de gegevens groeien behoeften, groeien partities en Service Fabric rebalances partities over knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a009d-132">As the data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="a009d-133">Hierdoor worden de blijvende efficiënt gebruik van de hardwarebronnen.</span><span class="sxs-lookup"><span data-stu-id="a009d-133">This ensures the continued efficient use of hardware resources.</span></span>

<span data-ttu-id="a009d-134">Als u een voorbeeld geven, dat u begint met een 5-node cluster en een service die is geconfigureerd met 10 partities en een doel van drie replica's.</span><span class="sxs-lookup"><span data-stu-id="a009d-134">To give you an example, say you start with a 5-node cluster and a service that is configured to have 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="a009d-135">In dit geval Service Fabric zou worden verdeeld en de replica's verdelen over het cluster-- en zou u uiteindelijk eindigen met twee primaire [replica's](service-fabric-availability-services.md) per knooppunt.</span><span class="sxs-lookup"><span data-stu-id="a009d-135">In this case, Service Fabric would balance and distribute the replicas across the cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="a009d-136">Als u nu uitbreiden van het cluster aan 10 knooppunten wilt, de primaire zou opnieuw verdelen Service Fabric [replica's](service-fabric-availability-services.md) op alle knooppunten van 10.</span><span class="sxs-lookup"><span data-stu-id="a009d-136">If you now need to scale out the cluster to 10 nodes, Service Fabric would rebalance the primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="a009d-137">Op dezelfde manier als u terug naar 5 knooppunten geschaald, Service Fabric zou opnieuw verdelen alle replica's op de 5-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a009d-137">Likewise, if you scaled back to 5 nodes, Service Fabric would rebalance all the replicas across the 5 nodes.</span></span>  

<span data-ttu-id="a009d-138">Afbeelding 2 toont de distributie van 10 partities voor en na het schalen van het cluster.</span><span class="sxs-lookup"><span data-stu-id="a009d-138">Figure 2 shows the distribution of 10 partitions before and after scaling the cluster.</span></span>

![Stateful service](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="a009d-140">De scale-out wordt hierdoor bereikt omdat aanvragen van clients worden verdeeld over computers, algehele prestaties van de toepassing is verbeterd en conflicten op toegang tot gegevenssegmenten van wordt verminderd.</span><span class="sxs-lookup"><span data-stu-id="a009d-140">As a result, the scale-out is achieved since requests from clients are distributed across computers, overall performance of the application is improved, and contention on access to chunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="a009d-141">Plan voor het partitioneren</span><span class="sxs-lookup"><span data-stu-id="a009d-141">Plan for partitioning</span></span>
<span data-ttu-id="a009d-142">Voordat u een service implementeert, moet u altijd de partitionering strategie die vereist is voor het uitbreiden van overwegen.</span><span class="sxs-lookup"><span data-stu-id="a009d-142">Before implementing a service, you should always consider the partitioning strategy that is required to scale out.</span></span> <span data-ttu-id="a009d-143">Er zijn verschillende manieren, maar ze allemaal zich richten op wat de toepassing moet bereiken.</span><span class="sxs-lookup"><span data-stu-id="a009d-143">There are different ways, but all of them focus on what the application needs to achieve.</span></span> <span data-ttu-id="a009d-144">De context van dit artikel, laten we eens enkele van de belangrijkste aspecten.</span><span class="sxs-lookup"><span data-stu-id="a009d-144">For the context of this article, let's consider some of the more important aspects.</span></span>

<span data-ttu-id="a009d-145">Er is een goede aanpak om na te denken over de structuur van de status die moet worden gepartitioneerd als de eerste stap.</span><span class="sxs-lookup"><span data-stu-id="a009d-145">A good approach is to think about the structure of the state that needs to be partitioned, as the first step.</span></span>

<span data-ttu-id="a009d-146">U gaat nu een eenvoudig voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="a009d-146">Let's take a simple example.</span></span> <span data-ttu-id="a009d-147">Als u een service voor een countywide poll bouwen, kunt u een partitie voor elke stad kunt maken in de regio.</span><span class="sxs-lookup"><span data-stu-id="a009d-147">If you were to build a service for a countywide poll, you could create a partition for each city in the county.</span></span> <span data-ttu-id="a009d-148">Vervolgens kunt u de stemmen voor elke persoon opslaan in de plaats in de partitie die overeenkomt met die stad.</span><span class="sxs-lookup"><span data-stu-id="a009d-148">Then, you could store the votes for every person in the city in the partition that corresponds to that city.</span></span> <span data-ttu-id="a009d-149">Afbeelding 3 ziet u een set gebruikers en de plaats waar ze zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="a009d-149">Figure 3 illustrates a set of people and the city in which they reside.</span></span>

![Eenvoudige partitie](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="a009d-151">Als de populatie van steden varieert, zou u uiteindelijk met een aantal partities met een grote hoeveelheid gegevens (bijvoorbeeld Haarlem) en andere partities met weinig status (bijvoorbeeld Kirkland).</span><span class="sxs-lookup"><span data-stu-id="a009d-151">As the population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="a009d-152">Wat is de invloed van de partities met ongelijke hoeveelheden status hebben?</span><span class="sxs-lookup"><span data-stu-id="a009d-152">So what is the impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="a009d-153">Als u opnieuw over het voorbeeld denkt, kunt u eenvoudig de partitie die de stemmen voor Seattle bevat krijgt meer verkeer dan de Kirkland een bekijken.</span><span class="sxs-lookup"><span data-stu-id="a009d-153">If you think about the example again, you can easily see that the partition that holds the votes for Seattle will get more traffic than the Kirkland one.</span></span> <span data-ttu-id="a009d-154">Service Fabric maakt standaard ervoor dat er over hetzelfde aantal primaire en secundaire replica's op elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="a009d-154">By default, Service Fabric makes sure that there is about the same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="a009d-155">Zo zou u uiteindelijk met knooppunten die fungeren als replica's die dienen meer verkeer en anderen die minder verkeer dienen houdt.</span><span class="sxs-lookup"><span data-stu-id="a009d-155">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="a009d-156">U wilt bij voorkeur warme en koude plaatsen als volgt in een cluster voorkomen.</span><span class="sxs-lookup"><span data-stu-id="a009d-156">You would preferably want to avoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="a009d-157">Om te voorkomen dat dit, moet u twee dingen doen vanuit het partitionering oogpunt:</span><span class="sxs-lookup"><span data-stu-id="a009d-157">In order to avoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="a009d-158">Probeer voor het partitioneren van de status, zodat deze evenredig verdeeld over alle partities.</span><span class="sxs-lookup"><span data-stu-id="a009d-158">Try to partition the state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="a009d-159">Rapporteren over de belasting van elk van de replica's voor de service.</span><span class="sxs-lookup"><span data-stu-id="a009d-159">Report load from each of the replicas for the service.</span></span> <span data-ttu-id="a009d-160">(Voor meer informatie over het controleren van dit artikel [metrische gegevens en de belasting](service-fabric-cluster-resource-manager-metrics.md)).</span><span class="sxs-lookup"><span data-stu-id="a009d-160">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="a009d-161">Service Fabric biedt de mogelijkheid om te rapporteren over de belasting die door services, zoals de hoeveelheid geheugen of het aantal records worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a009d-161">Service Fabric provides the capability to report load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="a009d-162">Op basis van de metrische gegevens gerapporteerd, detecteert Service Fabric dat een aantal partities fungeren hogere belasting dan andere en het cluster rebalances door te verplaatsen van replica's naar geschikte knooppunten, zodat de algemene geen knooppunt is overbelast.</span><span class="sxs-lookup"><span data-stu-id="a009d-162">Based on the metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances the cluster by moving replicas to more suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="a009d-163">Soms weet u niet kunt hoeveel gegevens worden weergegeven in een bepaalde partitie.</span><span class="sxs-lookup"><span data-stu-id="a009d-163">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="a009d-164">Een algemene aanbeveling wordt beide--eerst door partities die selecteert, de gegevens gelijkmatig over de partities en de tweede, met reporting load.</span><span class="sxs-lookup"><span data-stu-id="a009d-164">So a general recommendation is to do both--first, by adopting a partitioning strategy that spreads the data evenly across the partitions and second, by reporting load.</span></span>  <span data-ttu-id="a009d-165">De eerste methode voorkomt situaties beschreven in het voorbeeld stemmende tijdens de tweede helpt vloeiend maken tijdelijke verschillen in access of load gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="a009d-165">The first method prevents situations described in the voting example, while the second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="a009d-166">Een ander aspect van de planning van de partitie is het juiste aantal partities beginnen te kiezen.</span><span class="sxs-lookup"><span data-stu-id="a009d-166">Another aspect of partition planning is to choose the correct number of partitions to begin with.</span></span>
<span data-ttu-id="a009d-167">Vanuit het perspectief van een Service Fabric is er niets dat verhindert dat u begint met een hoger aantal partities dan verwacht voor uw scenario.</span><span class="sxs-lookup"><span data-stu-id="a009d-167">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="a009d-168">Ervan uitgaande dat het maximum aantal partities is in feite een geldige benadering.</span><span class="sxs-lookup"><span data-stu-id="a009d-168">In fact, assuming the maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="a009d-169">In zeldzame gevallen, zou u uiteindelijk hoeven meer partities dan u oorspronkelijk hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="a009d-169">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="a009d-170">Als u het aantal partities niet nadat het feit wijzigen, zou u moet sommige geavanceerde partitie benaderingen, zoals het maken van een nieuwe service-exemplaar van hetzelfde servicetype toepassen.</span><span class="sxs-lookup"><span data-stu-id="a009d-170">As you cannot change the partition count after the fact, you would need to apply some advanced partition approaches, such as creating a new service instance of the same service type.</span></span> <span data-ttu-id="a009d-171">U moet ook bepaalde client-side '-logica waarmee de aanvragen worden doorgestuurd naar de juiste service-exemplaar, gebaseerd op kennis van clientzijde die u ervoor dat uw clientcode zorgen moet implementeren.</span><span class="sxs-lookup"><span data-stu-id="a009d-171">You would also need to implement some client-side logic that routes the requests to the correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="a009d-172">Andere overweging voor het partitioneren van de planning is de beschikbare computerbronnen.</span><span class="sxs-lookup"><span data-stu-id="a009d-172">Another consideration for partitioning planning is the available computer resources.</span></span> <span data-ttu-id="a009d-173">Als de status moet worden geopend en opgeslagen, wordt u gebonden te volgen:</span><span class="sxs-lookup"><span data-stu-id="a009d-173">As the state needs to be accessed and stored, you are bound to follow:</span></span>

* <span data-ttu-id="a009d-174">Netwerk bandbreedtelimieten</span><span class="sxs-lookup"><span data-stu-id="a009d-174">Network bandwidth limits</span></span>
* <span data-ttu-id="a009d-175">Systeem geheugenlimieten</span><span class="sxs-lookup"><span data-stu-id="a009d-175">System memory limits</span></span>
* <span data-ttu-id="a009d-176">Schijf opslaglimieten</span><span class="sxs-lookup"><span data-stu-id="a009d-176">Disk storage limits</span></span>

<span data-ttu-id="a009d-177">Wat gebeurt zodat er als u in resourcebeperkingen in een actief cluster uitvoert?</span><span class="sxs-lookup"><span data-stu-id="a009d-177">So what happens if you run into resource constraints in a running cluster?</span></span> <span data-ttu-id="a009d-178">Het antwoord is dat u gewoon kunt schalen uit het cluster om de nieuwe vereisten mogelijk te maken.</span><span class="sxs-lookup"><span data-stu-id="a009d-178">The answer is that you can simply scale out the cluster to accommodate the new requirements.</span></span>

<span data-ttu-id="a009d-179">[De handleiding voor capaciteitsplanning](service-fabric-capacity-planning.md) biedt richtlijnen voor het bepalen van het aantal knooppunten uw cluster moet.</span><span class="sxs-lookup"><span data-stu-id="a009d-179">[The capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how to determine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="a009d-180">Aan de slag met partitioneren</span><span class="sxs-lookup"><span data-stu-id="a009d-180">Get started with partitioning</span></span>
<span data-ttu-id="a009d-181">Deze sectie beschrijft hoe u aan de slag met het partitioneren van uw service.</span><span class="sxs-lookup"><span data-stu-id="a009d-181">This section describes how to get started with partitioning your service.</span></span>

<span data-ttu-id="a009d-182">Service Fabric biedt een keuze uit drie partitieschema's:</span><span class="sxs-lookup"><span data-stu-id="a009d-182">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="a009d-183">Varieerden partitioneren (anders UniformInt64Partition genoemd).</span><span class="sxs-lookup"><span data-stu-id="a009d-183">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="a009d-184">Met de naam partitioneren.</span><span class="sxs-lookup"><span data-stu-id="a009d-184">Named partitioning.</span></span> <span data-ttu-id="a009d-185">Toepassingen die gebruikmaken van dit model meestal beschikken over gegevens die kunnen worden bucketed binnen een begrensde set.</span><span class="sxs-lookup"><span data-stu-id="a009d-185">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="a009d-186">Enkele algemene voorbeelden van gegevensvelden gebruikt als benoemde partitiesleutels zou worden regio's, postcode codes, klantengroepen of andere zakelijke grenzen.</span><span class="sxs-lookup"><span data-stu-id="a009d-186">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="a009d-187">Singleton partitioneren.</span><span class="sxs-lookup"><span data-stu-id="a009d-187">Singleton partitioning.</span></span> <span data-ttu-id="a009d-188">Singleton-partities worden meestal gebruikt wanneer de service geen aanvullende routering vereist.</span><span class="sxs-lookup"><span data-stu-id="a009d-188">Singleton partitions are typically used when the service does not require any additional routing.</span></span> <span data-ttu-id="a009d-189">Bijvoorbeeld, stateless services deze partitieschema standaard gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a009d-189">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="a009d-190">Met de naam en partitionering Singleton-schema's zijn speciale soorten varieerde partities.</span><span class="sxs-lookup"><span data-stu-id="a009d-190">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="a009d-191">Standaard de Visual Studio-sjablonen voor Service Fabric gebruik varieerden partitioneren, zoals dit de meest voorkomende en nuttige is.</span><span class="sxs-lookup"><span data-stu-id="a009d-191">By default, the Visual Studio templates for Service Fabric use ranged partitioning, as it is the most common and useful one.</span></span> <span data-ttu-id="a009d-192">De rest van dit artikel is gericht op een ranged partitionering.</span><span class="sxs-lookup"><span data-stu-id="a009d-192">The remainder of this article focuses on the ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="a009d-193">Partitieschema varieerde</span><span class="sxs-lookup"><span data-stu-id="a009d-193">Ranged partitioning scheme</span></span>
<span data-ttu-id="a009d-194">Dit wordt gebruikt om op te geven van een geheel getal-bereik (aangeduid met een lage en hoge sleutel) en een aantal partities (n).</span><span class="sxs-lookup"><span data-stu-id="a009d-194">This is used to specify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="a009d-195">N partities, elke verantwoordelijk is voor een niet-overlappende subbereik van de algehele partitiesleutelbereik wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a009d-195">It creates n partitions, each responsible for a non-overlapping subrange of the overall partition key range.</span></span> <span data-ttu-id="a009d-196">Bijvoorbeeld, een ranged partitieschema met een lage sleutel 0, een hoge sleutel 99 en een telling van 4 maakt vier partities zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a009d-196">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![Bereik partitioneren](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="a009d-198">Een gemeenschappelijke aanpak is het maken van een hash op basis van een unieke sleutel in de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="a009d-198">A common approach is to create a hash based on a unique key within the data set.</span></span> <span data-ttu-id="a009d-199">Enkele algemene voorbeelden van sleutels is een vehicle id-nummer (VIN), een werknemer-ID of een unieke tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="a009d-199">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="a009d-200">Met behulp van deze unieke sleutel, zou u vervolgens een hash-code, modulus de belangrijkste bereik, om te gebruiken als uw sleutel te genereren.</span><span class="sxs-lookup"><span data-stu-id="a009d-200">By using this unique key, you would then generate a hash code, modulus the key range, to use as your key.</span></span> <span data-ttu-id="a009d-201">U kunt de hogere en lagere grenzen van het toegestane bereik van de sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="a009d-201">You can specify the upper and lower bounds of the allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="a009d-202">Selecteer een hash-algoritme</span><span class="sxs-lookup"><span data-stu-id="a009d-202">Select a hash algorithm</span></span>
<span data-ttu-id="a009d-203">Een belangrijk onderdeel van het hash-selecteert hash-algoritme.</span><span class="sxs-lookup"><span data-stu-id="a009d-203">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="a009d-204">Overweging is of het doel is om soortgelijke sleutels in de buurt van elkaar (plaats gevoelige hashing)--groep of als activiteit moet op grote schaal worden gedistribueerd voor alle partities (hash-distributie), waarmee veelvoorkomende is.</span><span class="sxs-lookup"><span data-stu-id="a009d-204">A consideration is whether the goal is to group similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="a009d-205">De kenmerken van een goede distributie hash-algoritme zijn dat het is gemakkelijk om te berekenen, enkele conflicten heeft en wordt de sleutels gelijkmatig gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="a009d-205">The characteristics of a good distribution hashing algorithm are that it is easy to compute, it has few collisions, and it distributes the keys evenly.</span></span> <span data-ttu-id="a009d-206">Een goed voorbeeld van een efficiënte hash-algoritme is de [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash-algoritme.</span><span class="sxs-lookup"><span data-stu-id="a009d-206">A good example of an efficient hash algorithm is the [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="a009d-207">Een goede resource voor algemene hash-code algoritme opties is de [pagina Wikipedia (Engelstalig) op de hash-functies](http://en.wikipedia.org/wiki/Hash_function).</span><span class="sxs-lookup"><span data-stu-id="a009d-207">A good resource for general hash code algorithm choices is the [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="a009d-208">Een stateful service met meerdere partities bouwen</span><span class="sxs-lookup"><span data-stu-id="a009d-208">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="a009d-209">Stel uw eerste betrouwbare stateful service maken met meerdere partities.</span><span class="sxs-lookup"><span data-stu-id="a009d-209">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="a009d-210">In dit voorbeeld maakt u een zeer eenvoudige toepassing waarin u wilt opslaan van alle laatste namen die met dezelfde letter in dezelfde partitie beginnen.</span><span class="sxs-lookup"><span data-stu-id="a009d-210">In this example, you will build a very simple application where you want to store all last names that start with the same letter in the same partition.</span></span>

<span data-ttu-id="a009d-211">Voordat u een code te schrijven, moet u nadenken over de partities en partitiesleutels.</span><span class="sxs-lookup"><span data-stu-id="a009d-211">Before you write any code, you need to think about the partitions and partition keys.</span></span> <span data-ttu-id="a009d-212">U 26 partities (één voor elke letter van het alfabet), maar wat over de lage en hoge sleutels nodig?</span><span class="sxs-lookup"><span data-stu-id="a009d-212">You need 26 partitions (one for each letter in the alphabet), but what about the low and high keys?</span></span>
<span data-ttu-id="a009d-213">Als we letterlijk één partitie per letter hebben willen, kunt we gebruiken 0 als de lage sleutel en 25 als de hoge sleutel elke letter is zijn eigen sleutel.</span><span class="sxs-lookup"><span data-stu-id="a009d-213">As we literally want to have one partition per letter, we can use 0 as the low key and 25 as the high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="a009d-214">Dit is een vereenvoudigde scenario in feite de distributie ongelijke zou zijn.</span><span class="sxs-lookup"><span data-stu-id="a009d-214">This is a simplified scenario, as in reality the distribution would be uneven.</span></span> <span data-ttu-id="a009d-215">Laatste namen die beginnen met de letters "S" of ''M' komen vaker dan degene die beginnen met 'X' of 'Y'.</span><span class="sxs-lookup"><span data-stu-id="a009d-215">Last names starting with the letters "S" or "M" are more common than the ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="a009d-216">Open **Visual Studio** > **bestand** > **nieuwe** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="a009d-216">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="a009d-217">In de **nieuw Project** dialoogvenster Kies de Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a009d-217">In the **New Project** dialog box, choose the Service Fabric application.</span></span>
3. <span data-ttu-id="a009d-218">Het project 'AlphabetPartitions' aanroepen.</span><span class="sxs-lookup"><span data-stu-id="a009d-218">Call the project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="a009d-219">In de **maken van een Service** dialoogvenster Kies **Stateful** service en deze aanroepen 'Alphabet.Processing' zoals weergegeven in de onderstaande afbeelding.</span><span class="sxs-lookup"><span data-stu-id="a009d-219">In the **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in the image below.</span></span>
       <span data-ttu-id="a009d-220">![Dialoogvenster voor nieuwe service in Visual Studio][1]</span><span class="sxs-lookup"><span data-stu-id="a009d-220">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="a009d-221">Stel het aantal partities.</span><span class="sxs-lookup"><span data-stu-id="a009d-221">Set the number of partitions.</span></span> <span data-ttu-id="a009d-222">Open het bestand Applicationmanifest.xml in de map ApplicationPackageRoot van het project AlphabetPartitions en bijwerken van de parameter Processing_PartitionCount 26, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a009d-222">Open the Applicationmanifest.xml file located in the ApplicationPackageRoot folder of the AlphabetPartitions project and update the parameter Processing_PartitionCount to 26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="a009d-223">U moet ook bijwerken van de eigenschappen LowKey en HighKey van het element StatefulService in de ApplicationManifest.xml zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a009d-223">You also need to update the LowKey and HighKey properties of the StatefulService element in the ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="a009d-224">Voor de service toegankelijk is, opent u een eindpunt op een poort door het eindpuntelement van ServiceManifest.xml (te vinden in de map PackageRoot) toe te voegen voor de service Alphabet.Processing zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a009d-224">For the service to be accessible, open up an endpoint on a port by adding the endpoint element of ServiceManifest.xml (located in the PackageRoot folder) for the Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="a009d-225">De service is nu geconfigureerd om te luisteren naar een interne eindpunt met 26 partities.</span><span class="sxs-lookup"><span data-stu-id="a009d-225">Now the service is configured to listen to an internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="a009d-226">Vervolgens moet u voor het onderdrukken van de `CreateServiceReplicaListeners()` methode van de klasse verwerking.</span><span class="sxs-lookup"><span data-stu-id="a009d-226">Next, you need to override the `CreateServiceReplicaListeners()` method of the Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a009d-227">Voor dit voorbeeld nemen we aan dat u van een eenvoudige HttpCommunicationListener gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="a009d-227">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="a009d-228">Zie voor meer informatie over betrouwbare servicecommunicatie [communicatiemodel de betrouwbare Service](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="a009d-228">For more information on reliable service communication, see [The Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="a009d-229">Een aanbevolen patroon voor de URL die een replica luistert op de volgende indeling is: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span><span class="sxs-lookup"><span data-stu-id="a009d-229">A recommended pattern for the URL that a replica listens on is the following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="a009d-230">Zo wilt u de listener communicatie om te luisteren op de juiste eindpunten en met dit patroon configureren.</span><span class="sxs-lookup"><span data-stu-id="a009d-230">So you want to configure your communication listener to listen on the correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="a009d-231">Meerdere replica's van deze service kunnen worden gehost op dezelfde computer, zodat dit adres moet uniek zijn voor de replica.</span><span class="sxs-lookup"><span data-stu-id="a009d-231">Multiple replicas of this service may be hosted on the same computer, so this address needs to be unique to the replica.</span></span> <span data-ttu-id="a009d-232">Daarom partitie-ID + replica-ID in de URL zijn.</span><span class="sxs-lookup"><span data-stu-id="a009d-232">This is why   partition ID + replica ID are in the URL.</span></span> <span data-ttu-id="a009d-233">HttpListener kan luisteren op meerdere adressen op dezelfde poort, zolang het URL-voorvoegsel uniek is.</span><span class="sxs-lookup"><span data-stu-id="a009d-233">HttpListener can listen on multiple addresses on the same port as long as the URL prefix    is unique.</span></span>
   
    <span data-ttu-id="a009d-234">De extra GUID is er voor een geavanceerde aanvraag waarop secundaire replica's ook voor alleen-lezen-aanvragen luisteren.</span><span class="sxs-lookup"><span data-stu-id="a009d-234">The extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="a009d-235">Wanneer dit het geval is, u om ervoor te zorgen dat een nieuw uniek adres tijdens het veranderen van primaire naar secundaire wordt gebruikt voor het afdwingen voor clients opnieuw omzetten van het adres.</span><span class="sxs-lookup"><span data-stu-id="a009d-235">When that's the case, you want to make sure that a new unique address is used when transitioning from primary to secondary to force clients to re-resolve the address.</span></span> <span data-ttu-id="a009d-236">'+' wordt gebruikt als het adres hier zodat de replica luistert op alle beschikbare hosts (IP-, FQDM, ' localhost ', enz.) De volgende code toont een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="a009d-236">'+' is used as the address here so that the replica listens on all available hosts (IP, FQDM, localhost, etc.) The code below shows an example.</span></span>
   
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
   
    <span data-ttu-id="a009d-237">Het is ook opgemerkt dat de gepubliceerde URL enigszins afwijken van de luisterende URL-voorvoegsel is.</span><span class="sxs-lookup"><span data-stu-id="a009d-237">It's also worth noting that the published URL is slightly different from the listening URL prefix.</span></span>
    <span data-ttu-id="a009d-238">De URL van de luisterende aan HttpListener gegeven.</span><span class="sxs-lookup"><span data-stu-id="a009d-238">The listening URL is given to HttpListener.</span></span> <span data-ttu-id="a009d-239">De gepubliceerde URL is de URL die is gepubliceerd op de Service Fabric Naming Service, die wordt gebruikt voor servicedetectie.</span><span class="sxs-lookup"><span data-stu-id="a009d-239">The published URL is the URL that is published to the Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="a009d-240">Clients vragen voor dit adres via die discovery-service.</span><span class="sxs-lookup"><span data-stu-id="a009d-240">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="a009d-241">Het adres dat clients ophalen moet de werkelijke IP of FQDN van het knooppunt om verbinding te kunnen hebben.</span><span class="sxs-lookup"><span data-stu-id="a009d-241">The address that clients get needs to have the actual IP or FQDN of the node in order to connect.</span></span> <span data-ttu-id="a009d-242">Daarom moet u vervangen '+' met het knooppunt IP of FQDN-naam zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="a009d-242">So you need to replace '+' with the node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="a009d-243">De laatste stap is het toevoegen van de logica voor verwerking naar de service, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a009d-243">The last step is to add the processing logic to the service as shown below.</span></span>
   
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
   
    <span data-ttu-id="a009d-244">`ProcessInternalRequest`de waarden van de querytekenreeksparameter gebruikt voor het aanroepen van de partitie en aanroepen leest `AddUserAsync` achternaam toevoegen aan de woordenlijst voor betrouwbare `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="a009d-244">`ProcessInternalRequest` reads the values of the query string parameter used to call the partition and calls `AddUserAsync` to add the lastname to the reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="a009d-245">We gaan een stateless service toevoegen aan het project om te zien hoe u een bepaalde partitie kunt aanroepen.</span><span class="sxs-lookup"><span data-stu-id="a009d-245">Let's add a stateless service to the project to see how you can call a particular partition.</span></span>
    
    <span data-ttu-id="a009d-246">Deze service fungeert als een eenvoudige webinterface die de achternaam als een queryreeksparameter accepteert, bepaalt de partitiesleutel en verzendt het naar de service Alphabet.Processing voor verwerking.</span><span class="sxs-lookup"><span data-stu-id="a009d-246">This service serves as a simple web interface that accepts the lastname as a query string parameter, determines the partition key, and sends it to the Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="a009d-247">In de **maken van een Service** dialoogvenster Kies **Stateless** service en deze aanroepen 'Alphabet.Web' zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a009d-247">In the **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![Schermopname van staatloze service](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="a009d-249">.</span><span class="sxs-lookup"><span data-stu-id="a009d-249">.</span></span>
12. <span data-ttu-id="a009d-250">Werk de eindpuntinformatie in de ServiceManifest.xml van de service Alphabet.WebApi openen van een poort zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a009d-250">Update the endpoint information in the ServiceManifest.xml of the Alphabet.WebApi service to open up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="a009d-251">U moet een verzameling ServiceInstanceListeners retourneren in de Web-klasse.</span><span class="sxs-lookup"><span data-stu-id="a009d-251">You need to return a collection of ServiceInstanceListeners in the class Web.</span></span> <span data-ttu-id="a009d-252">U kunt opnieuw een eenvoudige HttpCommunicationListener implementeren.</span><span class="sxs-lookup"><span data-stu-id="a009d-252">Again, you can choose to implement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is the node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="a009d-253">U moet nu de verwerking van logica implementeren.</span><span class="sxs-lookup"><span data-stu-id="a009d-253">Now you need to implement the processing logic.</span></span> <span data-ttu-id="a009d-254">Het aanroepen van de HttpCommunicationListener `ProcessInputRequest` wanneer een aanvraag binnenkomt.</span><span class="sxs-lookup"><span data-stu-id="a009d-254">The HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="a009d-255">Dus we gaan nu en voeg de volgende code.</span><span class="sxs-lookup"><span data-stu-id="a009d-255">So let's go ahead and add the code below.</span></span>
    
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
                    "Result: {0}. <p>Partition key: '{1}' generated from the first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
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
                output = output + "added to Partition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="a009d-256">We doorlopen die deze stap voor stap.</span><span class="sxs-lookup"><span data-stu-id="a009d-256">Let's walk through it step by step.</span></span> <span data-ttu-id="a009d-257">De code leest de eerste letter van de querytekenreeksparameter `lastname` in een tekenset.</span><span class="sxs-lookup"><span data-stu-id="a009d-257">The code reads the first letter of the query string parameter `lastname` into a char.</span></span> <span data-ttu-id="a009d-258">Vervolgens wordt de partitiesleutel voor deze brief bepaald door af te trekken van de hexadecimale waarde van `A` van de hexadecimale waarde van de eerste letter van de laatste namen.</span><span class="sxs-lookup"><span data-stu-id="a009d-258">Then, it determines the partition key for this letter by subtracting the hexadecimal value of `A` from the hexadecimal value of the last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="a009d-259">Vergeet niet dat voor dit voorbeeld gebruiken we 26 partities met één partitiesleutel per partitie.</span><span class="sxs-lookup"><span data-stu-id="a009d-259">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="a009d-260">Vervolgens verkrijgen van de partitie service `partition` voor deze sleutel met behulp van de `ResolveAsync` methode op de `servicePartitionResolver` object.</span><span class="sxs-lookup"><span data-stu-id="a009d-260">Next, we obtain the service partition `partition` for this key by using the `ResolveAsync` method on the `servicePartitionResolver` object.</span></span> <span data-ttu-id="a009d-261">`servicePartitionResolver`is gedefinieerd als</span><span class="sxs-lookup"><span data-stu-id="a009d-261">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="a009d-262">De `ResolveAsync` methode neemt de URI van de service, de partitiesleutel en een annulering als parameters token.</span><span class="sxs-lookup"><span data-stu-id="a009d-262">The `ResolveAsync` method takes the service URI, the partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="a009d-263">De service-URI voor de verwerkingsservice is `fabric:/AlphabetPartitions/Processing`.</span><span class="sxs-lookup"><span data-stu-id="a009d-263">The service URI for the processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="a009d-264">Vervolgens wordt het eindpunt van de partitie ophalen.</span><span class="sxs-lookup"><span data-stu-id="a009d-264">Next, we get the endpoint of the partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="a009d-265">Ten slotte we de eindpunt-URL plus de querytekenreeks bouwen en de van verwerkingsservice aanroepen.</span><span class="sxs-lookup"><span data-stu-id="a009d-265">Finally, we build the endpoint URL plus the querystring and call the processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="a009d-266">Als de verwerking is voltooid, wordt de uitvoer terug te schrijven.</span><span class="sxs-lookup"><span data-stu-id="a009d-266">Once the processing is done, we write the output back.</span></span>
15. <span data-ttu-id="a009d-267">De laatste stap is het testen van de service.</span><span class="sxs-lookup"><span data-stu-id="a009d-267">The last step is to test the service.</span></span> <span data-ttu-id="a009d-268">Visual Studio maakt gebruik van parameters voor de toepassing voor lokale en cloudimplementatie.</span><span class="sxs-lookup"><span data-stu-id="a009d-268">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="a009d-269">Als u wilt de service met 26 partities lokaal testen, moet u bijwerken de `Local.xml` bestand in de map ApplicationParameters van het project AlphabetPartitions zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a009d-269">To test the service with 26 partitions locally, you need to update the `Local.xml` file in the ApplicationParameters folder of the AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="a009d-270">Wanneer u klaar bent voor implementatie, kunt u de service en alle van de partities in de Service Fabric Explorer controleren.</span><span class="sxs-lookup"><span data-stu-id="a009d-270">Once you finish deployment, you can check the service and all of its partitions in the Service Fabric Explorer.</span></span>
    
    ![Schermafbeelding van de service Fabric Explorer](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="a009d-272">In een browser, kunt u de partitionering logica testen door te voeren `http://localhost:8081/?lastname=somename`.</span><span class="sxs-lookup"><span data-stu-id="a009d-272">In a browser, you can test the partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="a009d-273">U ziet dat elke achternaam op die met dezelfde letter begint worden opgeslagen in dezelfde partitie.</span><span class="sxs-lookup"><span data-stu-id="a009d-273">You will see that each last name that starts with the same letter is being stored in the same partition.</span></span>
    
    ![Schermafbeelding van de browser](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="a009d-275">De volledige broncode van het voorbeeld is beschikbaar op [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="a009d-275">The entire source code of the sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a009d-276">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a009d-276">Next steps</span></span>
<span data-ttu-id="a009d-277">Zie de volgende onderwerpen voor informatie over Service Fabric-concepten:</span><span class="sxs-lookup"><span data-stu-id="a009d-277">For information on Service Fabric concepts, see the following:</span></span>

* [<span data-ttu-id="a009d-278">Beschikbaarheid van Service Fabric-services</span><span class="sxs-lookup"><span data-stu-id="a009d-278">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="a009d-279">Schaalbaarheid van Service Fabric-services</span><span class="sxs-lookup"><span data-stu-id="a009d-279">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="a009d-280">Capaciteitsplanning voor Service Fabric-toepassingen</span><span class="sxs-lookup"><span data-stu-id="a009d-280">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png