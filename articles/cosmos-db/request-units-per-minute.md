---
title: 'Azure CosmosDB: Aanvraageenheden per minuut (RU/m) | Microsoft Docs'
description: Meer informatie over hoe tooreduce kosten door het gebruik van aanvraageenheden per minuut.
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="ec566-103">Aanvraageenheden per minuut in Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="ec566-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="ec566-104">Azure Cosmos DB is ontworpen toohelp u een snelle en voorspelbare prestaties en schaalbaarheid naadloos samen met de groei van uw toepassing bereiken.</span><span class="sxs-lookup"><span data-stu-id="ec566-104">Azure Cosmos DB is designed toohelp you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="ec566-105">U kunt inrichten doorvoer in een Cosmos-DB-container op beide, per seconde en op granulaties per minuut (RU/m).</span><span class="sxs-lookup"><span data-stu-id="ec566-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="ec566-106">Hallo ingerichte doorvoer per minuut samenvattingen is gebruikte toomanage onverwachte pieken in Hallo werkbelasting optreedt samenvattingen per seconde.</span><span class="sxs-lookup"><span data-stu-id="ec566-106">hello provisioned throughput at per-minute granularity is used toomanage unexpected spikes in hello workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="ec566-107">Dit artikel bevat een overzicht van de werking Hallo inrichting van eenheid aanvragen per minuut (RU/m).</span><span class="sxs-lookup"><span data-stu-id="ec566-107">This article provides an overview of how hello provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="ec566-108">Hallo doel rekening met het leveren van RU/m is tooprovide een voorspelbare prestaties rond onvoorspelbare behoeften (met name als u toorun analyses nodig boven op uw operationele gegevens) en spiky werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="ec566-108">hello goal in mind with provisioning of RU/m is tooprovide a predictable performance around unpredictable needs (especially if you need toorun analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="ec566-109">We willen toohave die onze klanten meer Hallo doorvoer die ze inrichten zodat u snel kunt schalen met gemoedsrust gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ec566-109">We want toohave our customers consume more hello throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="ec566-110">Na het lezen van dit artikel kunt u zich kunt tooanswer Hallo vragen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ec566-110">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="ec566-111">Hoe werkt een eenheid aanvragen per minuut</span><span class="sxs-lookup"><span data-stu-id="ec566-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="ec566-112">Wat is Hallo verschil tussen eenheid aanvragen per minuut en eenheid aanvragen per seconde?</span><span class="sxs-lookup"><span data-stu-id="ec566-112">What is hello difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="ec566-113">Hoe tooprovision RU/m?</span><span class="sxs-lookup"><span data-stu-id="ec566-113">How tooprovision RU/m?</span></span>
* <span data-ttu-id="ec566-114">Onder welke scenario onderzoekt ik inrichten eenheid aanvragen per minuut?</span><span class="sxs-lookup"><span data-stu-id="ec566-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="ec566-115">Hoe Hallo toouse portal metrische gegevens toooptimize mijn kosten en prestaties?</span><span class="sxs-lookup"><span data-stu-id="ec566-115">How toouse hello portal metrics toooptimize my cost and performance?</span></span>
* <span data-ttu-id="ec566-116">Definiëren welk soort aanvraag kan uw budget RU/m gebruiken?</span><span class="sxs-lookup"><span data-stu-id="ec566-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="ec566-117">Inrichting aanvraageenheden per minuut (RU/m)</span><span class="sxs-lookup"><span data-stu-id="ec566-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="ec566-118">Als u Azure Cosmos DB inricht Hallo tweede samenvattingen (RU/s), krijgt u Hallo garanderen dat uw aanvraag is uitgevoerd op een lage latentie als de doorvoer niet Hallo capaciteit ingericht binnen die seconde overschreden.</span><span class="sxs-lookup"><span data-stu-id="ec566-118">When you provision Azure Cosmos DB at hello second granularity (RU/s), you get hello guarantee that your request succeeds at a low latency if your throughput has not exceeded hello capacity provisioned within that second.</span></span> <span data-ttu-id="ec566-119">Met RU/m is het Hallo granulatie op Hallo minuut met Hallo garanderen dat uw aanvraag is gelukt binnen die minuut.</span><span class="sxs-lookup"><span data-stu-id="ec566-119">With RU/m, hello granularity is at hello minute with hello guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="ec566-120">Vergeleken toobursting systemen, zorgen wij ervoor dat Hallo prestaties u voorspelbare en erop kunt u plannen.</span><span class="sxs-lookup"><span data-stu-id="ec566-120">Compared toobursting systems, we make sure that hello performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="ec566-121">Hallo manier per minuut works inrichting is eenvoudig:</span><span class="sxs-lookup"><span data-stu-id="ec566-121">hello way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="ec566-122">RU/m wordt in rekening gebracht per uur en toevoeging tooRU/s.</span><span class="sxs-lookup"><span data-stu-id="ec566-122">RU/m is billed hourly and in addition tooRU/s.</span></span> <span data-ttu-id="ec566-123">Voor meer informatie gaat u naar Azure Cosmos DB [pagina met prijzen](https://aka.ms/acdbpricing).</span><span class="sxs-lookup"><span data-stu-id="ec566-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="ec566-124">RU/m kan worden ingeschakeld op niveau verzameling.</span><span class="sxs-lookup"><span data-stu-id="ec566-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="ec566-125">Dat kan worden gedaan via Hallo SDK's (Node.js, Java of .net) of via de portal hello (ook MongoDB API werkbelastingen bevatten)</span><span class="sxs-lookup"><span data-stu-id="ec566-125">That can be done through hello SDKs (Node.js, Java, or .Net) or through hello portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="ec566-126">Als RU/m is ingeschakeld voor elke 100 RU/s ingericht, krijgt u ook 1000 RU/m ingericht (Hallo verhouding is 10 x)</span><span class="sxs-lookup"><span data-stu-id="ec566-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (hello ratio is 10x)</span></span>
* <span data-ttu-id="ec566-127">Op een tweede opgegeven, een aanvraag-eenheid verbruikt uw RU/m inrichting alleen als u hebt overschreden uw per tweede inrichting binnen die seconde</span><span class="sxs-lookup"><span data-stu-id="ec566-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="ec566-128">Eenmaal Hallo 60 seconden tijd (UTC) ends, Hallo per minuut inrichting is gevuld.</span><span class="sxs-lookup"><span data-stu-id="ec566-128">Once hello 60-second period (UTC) ends, hello per minute provisioning is refilled</span></span>
* <span data-ttu-id="ec566-129">RU/m kan alleen worden ingeschakeld voor verzamelingen met een maximale inrichting van 5000 RU/s per partitie.</span><span class="sxs-lookup"><span data-stu-id="ec566-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="ec566-130">Als u de doorvoerbehoeften van uw schalen en een hoog niveau voor het leveren van per partitie, ontvangt u een waarschuwingsbericht weergegeven</span><span class="sxs-lookup"><span data-stu-id="ec566-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="ec566-131">Hieronder wordt een voorbeeld van een concreet, waarin een klant 10kRU/s met 100kRU/m kunt inrichten 73% opslaan in kosten inrichten voor piek (bij 50kRU per seconde) tot en met een periode van 90 seconden op een verzameling die 10.000 is RU/s en 100.000 RU/m ingericht:</span><span class="sxs-lookup"><span data-stu-id="ec566-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="ec566-132">tweede 1e: Hallo RU/m budget is ingesteld op 100.000</span><span class="sxs-lookup"><span data-stu-id="ec566-132">1st second: hello RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="ec566-133">tweede 3e: tijdens deze tweede Hallo verbruik van aanvragen eenheid 11,010 RUs, 1,010 RUs hierboven Hallo RU/s inrichting is.</span><span class="sxs-lookup"><span data-stu-id="ec566-133">3rd second: During that second hello consumption of Request Unit was 11,010 RUs, 1,010 RUs above hello RU/s provisioning.</span></span> <span data-ttu-id="ec566-134">Daarom worden 1,010 RUs van Hallo RU/m budget afgetrokken.</span><span class="sxs-lookup"><span data-stu-id="ec566-134">Therefore, 1,010 RUs are deducted from hello RU/m budget.</span></span> <span data-ttu-id="ec566-135">98,990 RUs zijn beschikbaar voor Hallo volgende 57 seconden in Hallo RU/m budget</span><span class="sxs-lookup"><span data-stu-id="ec566-135">98,990 RUs are available for hello next 57 seconds in hello RU/m budget</span></span>
* <span data-ttu-id="ec566-136">29 seconde: tijdens deze tweede, een grote piek is er gebeurd (> 4 x hoger is dan de inrichting per seconde) en Hallo verbruik van aanvragen eenheid 46,920 RUs is.</span><span class="sxs-lookup"><span data-stu-id="ec566-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and hello consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="ec566-137">36,920 RUs worden afgetrokken van Hallo RU/m budget verwijderd uit 92,323 RUs (28 seconde) too55, 403 RUs (29 seconde)</span><span class="sxs-lookup"><span data-stu-id="ec566-137">36,920 RUs are deducted from hello RU/m budget that dropped from 92,323 RUs (28th second) too55,403 RUs (29th second)</span></span>
* <span data-ttu-id="ec566-138">61st seconde: RU/m budget terug too100, 000 RUs is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ec566-138">61st second: RU/m budget is set back too100,000 RUs.</span></span>
 
![Grafiek weergeven Hallo verbruik en het inrichten van Azure DB die Cosmos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="ec566-140">Capaciteit van de aanvraag-eenheid opgeven met RU/m</span><span class="sxs-lookup"><span data-stu-id="ec566-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="ec566-141">Bij het maken van een verzameling Azure Cosmos DB u Hallo-nummer opgeven aantal aanvraageenheden per seconde (ru/s per seconde) u wilt dat gereserveerd voor Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="ec566-141">When creating an Azure Cosmos DB collection, you specify hello number of request units per second (RU per second) you want reserved for hello collection.</span></span> <span data-ttu-id="ec566-142">U kunt ook aangeven of u wilt dat tooadd RU per minuut.</span><span class="sxs-lookup"><span data-stu-id="ec566-142">You can also decide if you want tooadd RU per minute.</span></span> <span data-ttu-id="ec566-143">Dit kan worden gedaan via Hallo Portal of Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="ec566-143">This can be done through hello Portal or hello SDK.</span></span> 

### <a name="through-hello-portal"></a><span data-ttu-id="ec566-144">Via Hallo Portal</span><span class="sxs-lookup"><span data-stu-id="ec566-144">Through hello Portal</span></span>

<span data-ttu-id="ec566-145">In- of uitschakelen van RU per minuut hoeven alleen een Klik bij het inrichten van een verzameling.</span><span class="sxs-lookup"><span data-stu-id="ec566-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Schermopname die laat zien hoe tooset RU/m in hello Azure-portal](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a><span data-ttu-id="ec566-147">Via Hallo SDK</span><span class="sxs-lookup"><span data-stu-id="ec566-147">Through hello SDK</span></span>
<span data-ttu-id="ec566-148">Dit is eerst belangrijk toonote RU/m is alleen beschikbaar voor Hallo SDK's te volgen:</span><span class="sxs-lookup"><span data-stu-id="ec566-148">First, this is important toonote that RU/m is only available for hello following SDKs:</span></span>

* <span data-ttu-id="ec566-149">.NET 1.14.0</span><span class="sxs-lookup"><span data-stu-id="ec566-149">.Net 1.14.0</span></span>
* <span data-ttu-id="ec566-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="ec566-150">Java 1.11.0</span></span>
* <span data-ttu-id="ec566-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="ec566-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="ec566-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="ec566-152">Python 2.2.0</span></span>

<span data-ttu-id="ec566-153">Hier volgt een codefragment voor het maken van een verzameling met 3000 aanvraageenheden per tweede en 30.000 aanvraageenheden per minuut Hallo .NET SDK gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ec566-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using hello .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="ec566-154">Hier volgt een codefragment voor het wijzigen van Hallo doorvoer van een verzameling too5, 000 aanvraageenheden per seconde zonder RU inrichting per minuut gebruik Hallo .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="ec566-154">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second without provisioning RU per minute using hello .NET SDK:</span></span>

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="ec566-155">Goede aanpassen aan scenario 's</span><span class="sxs-lookup"><span data-stu-id="ec566-155">Good fit scenarios</span></span>

<span data-ttu-id="ec566-156">In deze sectie bieden we een overzicht van scenario's die geschikt zijn voor het inschakelen van aanvraageenheden per minuut.</span><span class="sxs-lookup"><span data-stu-id="ec566-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="ec566-157">**Omgeving dev/Test:** geschikt.</span><span class="sxs-lookup"><span data-stu-id="ec566-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="ec566-158">Tijdens het Hallo-ontwikkeling, als u uw toepassing met verschillende werkbelastingen, test kunt RU/m bieden Hallo flexibiliteit in deze fase.</span><span class="sxs-lookup"><span data-stu-id="ec566-158">During hello development stage, if you are testing your application with different workloads, RU/m can provide hello flexibility at this stage.</span></span> <span data-ttu-id="ec566-159">Tijdens het Hallo [emulator](local-emulator.md) is een uitstekend gratis hulpprogramma tootest Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ec566-159">While hello [emulator](local-emulator.md) is a great free tool tootest Azure Cosmos DB.</span></span> <span data-ttu-id="ec566-160">Maar als u toostart in een cloudomgeving wilt, hebt u een hoge mate van flexibiliteit met RU/m voor de behoeften van uw ad-hoc-prestaties.</span><span class="sxs-lookup"><span data-stu-id="ec566-160">However if you want toostart in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="ec566-161">U kwijt meer tijd ontwikkelt, minder zorgen over prestatiebehoeften op het eerste.</span><span class="sxs-lookup"><span data-stu-id="ec566-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="ec566-162">We het beste beginnen met het inrichten Hallo minimale RU/s en RU/m inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ec566-162">We recommend starting with hello minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="ec566-163">**Onvoorspelbare, spiky, minuut granulatie moet:** goed past – besparingen: 25 75%.</span><span class="sxs-lookup"><span data-stu-id="ec566-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="ec566-164">Wij hebben grote verbetering van RU/m en de meeste scenario's voor productie zijn in die groep.</span><span class="sxs-lookup"><span data-stu-id="ec566-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="ec566-165">Als u een IoT-werkbelasting met piek enkele keren in een minuut hebt, hebt u query's wanneer het systeem laat massaal invoegen op Hallo dezelfde tijd, moet u extra capaciteit voor handeling spiky.</span><span class="sxs-lookup"><span data-stu-id="ec566-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at hello same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="ec566-166">Het is raadzaam om uw resourcebehoeften optimaliseren door het toepassen van onze onderstaande stapsgewijze benadering.</span><span class="sxs-lookup"><span data-stu-id="ec566-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![Grafiek met aanvraag verbruik in vijf minuten granulatie](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="ec566-168">*Afbeelding - RU verbruik benchmark*</span><span class="sxs-lookup"><span data-stu-id="ec566-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="ec566-169">**Gemoedsrust:** goed past – besparingen: 10-20%.</span><span class="sxs-lookup"><span data-stu-id="ec566-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="ec566-170">Soms wilt toohave gemoedsrust en u geen zorgen over potentiële pieken en beperking.</span><span class="sxs-lookup"><span data-stu-id="ec566-170">Sometimes, you just want toohave peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="ec566-171">Deze functie is Hallo rechts een voor u.</span><span class="sxs-lookup"><span data-stu-id="ec566-171">This feature is hello right one for you.</span></span> <span data-ttu-id="ec566-172">In dat geval wordt aangeraden RU/m inschakelen en iets lagere uw per tweede inrichten.</span><span class="sxs-lookup"><span data-stu-id="ec566-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="ec566-173">In dit geval wijkt af van Hallo hierboven als u wordt niet geprobeerd toooptimize agressief uw inrichten.</span><span class="sxs-lookup"><span data-stu-id="ec566-173">This case is different from hello above as you will not try toooptimize aggressively your provisioning.</span></span> <span data-ttu-id="ec566-174">Dit is van een 'Nul beperking' denkt in.</span><span class="sxs-lookup"><span data-stu-id="ec566-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="ec566-175">Kritieke bewerkingen met ad-hoc-behoeften: soms aangeraden tooonly kunnen kritieke bewerkingen toegang RU/m budget Hallo budget niet ophalen door de ad-hoc of minder belangrijke bewerkingen verbruiken.</span><span class="sxs-lookup"><span data-stu-id="ec566-175">Critical operations with adhoc needs: We sometimes recommend tooonly let critical operations access RU/m budget so hello budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="ec566-176">Dat kan eenvoudig worden gedefinieerd in Hallo onderstaande sectie.</span><span class="sxs-lookup"><span data-stu-id="ec566-176">That can be easily defined in hello section below.</span></span>

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a><span data-ttu-id="ec566-177">Met behulp van Hallo portal metrische gegevens toooptimize kosten en prestaties</span><span class="sxs-lookup"><span data-stu-id="ec566-177">Using hello portal metrics toooptimize cost and performance</span></span>

<span data-ttu-id="ec566-178">**De komende weken hello ontwikkelen we verder Hallo inhoud rond de bewaking van RUs minuut verbruik toooptimize die uw doorvoer moet.**</span><span class="sxs-lookup"><span data-stu-id="ec566-178">**In hello coming weeks, we will further develop hello content around monitoring RUs minute consumption toooptimize your throughput needs.**</span></span>

<span data-ttu-id="ec566-179">Via de portal metrics hello, kunt u zien hoeveel reguliere RU seconden u versus RU verbruikt minuten.</span><span class="sxs-lookup"><span data-stu-id="ec566-179">Through hello portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="ec566-180">Bewaking van deze metrische gegevens kunt u uw inrichting optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="ec566-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="ec566-181">Een stapsgewijze benadering voor het wordt aangeraden toouse RU/m tooyour profiteren.</span><span class="sxs-lookup"><span data-stu-id="ec566-181">We recommend a step by step approach on how toouse RU/m tooyour advantage.</span></span> <span data-ttu-id="ec566-182">Voor elke stap moet u een overzicht van Hallo RU verbruik voor een volledige cyclus van uw werkbelasting (mogelijk uren, dagen, of zelfs weken) hebben en inzichten verkrijgen op Hallo-gebruik van wat u inrichten.</span><span class="sxs-lookup"><span data-stu-id="ec566-182">For each step, you should have an overview of hello RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on hello utilization of what you provision.</span></span>

<span data-ttu-id="ec566-183">Hallo principe achter deze benadering is toomake uw doorvoer inrichten als sluiten als mogelijke tooa punt die overeenkomt met de van de onderstaande prestatiecriteria wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="ec566-183">hello principle behind this approach is toomake your throughput provisioning as close as possible tooa provisioning point that matches your performance criteria below.</span></span> 

![Grafiek met aanvraag verbruik in samenvattingen van 5 minuten](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="ec566-185">toounderstand hello optimale inrichting punt voor uw workload, moet u toounderstand:</span><span class="sxs-lookup"><span data-stu-id="ec566-185">toounderstand hello optimal provisioning point for your workload, you need toounderstand:</span></span>

* <span data-ttu-id="ec566-186">Verbruik patronen: Nee, incidentele of volgehouden pieken?</span><span class="sxs-lookup"><span data-stu-id="ec566-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="ec566-187">(2 x gemiddelde) klein, Gemiddeld of grote (> 10 x gemiddelde) pieken?</span><span class="sxs-lookup"><span data-stu-id="ec566-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="ec566-188">Percentage van beperkte aanvragen: bent u ervan overtuigd bent als er een stukje beperking?</span><span class="sxs-lookup"><span data-stu-id="ec566-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="ec566-189">Zo ja, in welke mate?</span><span class="sxs-lookup"><span data-stu-id="ec566-189">If so, by how much?</span></span> 

<span data-ttu-id="ec566-190">Als u wat uw doelstellingen zijn weet, kunt u zich kunt tooget dichter toohello optimale inrichten.</span><span class="sxs-lookup"><span data-stu-id="ec566-190">Once you have identified what your goals are, you will be able tooget closer toohello optimal provisioning.</span></span>

<span data-ttu-id="ec566-191">tooassist, willen we tooprovide een algemene richtlijnen voor hoe toooptimize op uw inrichting basis van uw verbruik RU/m.</span><span class="sxs-lookup"><span data-stu-id="ec566-191">tooassist you, we want tooprovide an overall guidance on how toooptimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="ec566-192">In deze richtlijnen tooall soort werkbelasting is niet van toepassing, maar is gebaseerd op kennis van Hallo private preview.</span><span class="sxs-lookup"><span data-stu-id="ec566-192">This guidance doesn’t apply tooall kind of workloads but is based on hello private preview knowledge.</span></span> <span data-ttu-id="ec566-193">Dergelijke basislijnen kan worden gewijzigd als er meer informatie:</span><span class="sxs-lookup"><span data-stu-id="ec566-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="ec566-194">RU/m % gebruik</span><span class="sxs-lookup"><span data-stu-id="ec566-194">RU/m % utilization</span></span>|<span data-ttu-id="ec566-195">Mate van gebruik van RU/m</span><span class="sxs-lookup"><span data-stu-id="ec566-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="ec566-196">Aanbevolen acties voor het inrichten</span><span class="sxs-lookup"><span data-stu-id="ec566-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="ec566-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="ec566-197">0-1%</span></span>|<span data-ttu-id="ec566-198">Onder gebruik</span><span class="sxs-lookup"><span data-stu-id="ec566-198">Under utilization</span></span>|<span data-ttu-id="ec566-199">Lagere RU/s tooconsume meer RU/m</span><span class="sxs-lookup"><span data-stu-id="ec566-199">Lower RU/s tooconsume more RU/m</span></span>|
|<span data-ttu-id="ec566-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="ec566-200">1-10%</span></span>|<span data-ttu-id="ec566-201">Gebruik in orde</span><span class="sxs-lookup"><span data-stu-id="ec566-201">Healthy use</span></span>|<span data-ttu-id="ec566-202">Hello Houd dezelfde inrichting niveau</span><span class="sxs-lookup"><span data-stu-id="ec566-202">Keep hello same provisioning level</span></span>|
|<span data-ttu-id="ec566-203">Meer dan 10%</span><span class="sxs-lookup"><span data-stu-id="ec566-203">Above 10%</span></span>|<span data-ttu-id="ec566-204">Overmatig gebruik</span><span class="sxs-lookup"><span data-stu-id="ec566-204">Over utilization</span></span>|<span data-ttu-id="ec566-205">RU/s toorely minder op RU/m verhogen</span><span class="sxs-lookup"><span data-stu-id="ec566-205">Increase RU/s toorely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a><span data-ttu-id="ec566-206">Selecteer welke bewerkingen kunnen Hallo RU/m budget gebruiken</span><span class="sxs-lookup"><span data-stu-id="ec566-206">Select which operations can consume hello RU/m budget</span></span>

<span data-ttu-id="ec566-207">Op het niveau van de aanvraag, u kunt ook in-of uitschakelen RU/m budget tooserve Hallo aanvraag ongeacht bewerkingstype.</span><span class="sxs-lookup"><span data-stu-id="ec566-207">At request level, you can also enable/disable RU/m budget tooserve hello request irrespective of operation type.</span></span> <span data-ttu-id="ec566-208">Als reguliere ingerichte RUs per seconde budget verbruikt en Hallo-aanvraag kan niet Hallo RU/m budget verbruikt, worden deze aanvraag wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="ec566-208">If regular provisioned RUs/sec budget is consumed and hello request cannot consume hello RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="ec566-209">Standaard wordt elk verzoek afgehandeld door RU/m budget als RU/m doorvoer budget is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="ec566-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="ec566-210">Hier volgt een codefragment voor het uitschakelen van RU/m budget Hallo DocumentDB API gebruiken CRUD en query-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="ec566-210">Here is a code snippet for disabling RU/m budget using hello DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="ec566-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ec566-211">Next steps</span></span>

<span data-ttu-id="ec566-212">In dit artikel hebt wordt beschreven hoe partitionering werkt in Azure Cosmos DB, hoe u gepartitioneerde verzamelingen kunt maken en hoe u een goede partitiesleutel kunt verzamelen voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ec566-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="ec566-213">Schaal en prestaties testen met Azure Cosmos DB uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ec566-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="ec566-214">Zie [prestaties en schaal testen met Azure Cosmos DB](performance-testing.md) voor een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ec566-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="ec566-215">Aan de slag met Hallo coderen [SDK's](documentdb-sdk-dotnet.md) of Hallo [REST-API](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="ec566-215">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="ec566-216">Meer informatie over [ingerichte doorvoer](request-units.md) in Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="ec566-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

