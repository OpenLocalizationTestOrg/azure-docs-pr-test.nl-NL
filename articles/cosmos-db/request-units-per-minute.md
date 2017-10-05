---
title: 'Azure CosmosDB: Aanvraageenheden per minuut (RU/m) | Microsoft Docs'
description: Informatie over het om kosten te beperken door het gebruik van aanvraageenheden per minuut.
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
ms.openlocfilehash: 72d60d5656ad664e42a848fc9b372cb09e49b888
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="b98fb-103">Aanvraageenheden per minuut in Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="b98fb-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="b98fb-104">Azure Cosmos DB is ontworpen om u helpen een snelle en voorspelbare prestaties en schaalbaarheid naadloos samen met de groei van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b98fb-104">Azure Cosmos DB is designed to help you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="b98fb-105">U kunt inrichten doorvoer in een Cosmos-DB-container op beide, per seconde en op granulaties per minuut (RU/m).</span><span class="sxs-lookup"><span data-stu-id="b98fb-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="b98fb-106">De ingerichte doorvoer via de granulatie per minuut wordt gebruikt voor het opvangen van onverwachte pieken in de workload terwijl granulatie per seconde wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b98fb-106">The provisioned throughput at per-minute granularity is used to manage unexpected spikes in the workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="b98fb-107">Dit artikel bevat een overzicht van hoe de inrichting van eenheid aanvragen per minuut (RU/m) werkt.</span><span class="sxs-lookup"><span data-stu-id="b98fb-107">This article provides an overview of how the provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="b98fb-108">Het doel rekening met het leveren van RU/m is om een voorspelbare prestaties rond onvoorspelbare behoeften (met name als u wilt uitvoeren analytics boven op uw operationele gegevens) en spiky werkbelastingen te bieden.</span><span class="sxs-lookup"><span data-stu-id="b98fb-108">The goal in mind with provisioning of RU/m is to provide a predictable performance around unpredictable needs (especially if you need to run analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="b98fb-109">We willen hebben onze klanten meer doorvoer die ze inrichten zodat u snel kunt schalen met gemoedsrust gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b98fb-109">We want to have our customers consume more the throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="b98fb-110">Na het lezen van dit artikel kunt u zich de volgende vragen beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="b98fb-110">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="b98fb-111">Hoe werkt een eenheid aanvragen per minuut</span><span class="sxs-lookup"><span data-stu-id="b98fb-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="b98fb-112">Wat is het verschil tussen eenheid aanvragen per minuut en eenheid aanvragen per seconde?</span><span class="sxs-lookup"><span data-stu-id="b98fb-112">What is the difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="b98fb-113">Het inrichten van RU/m?</span><span class="sxs-lookup"><span data-stu-id="b98fb-113">How to provision RU/m?</span></span>
* <span data-ttu-id="b98fb-114">Onder welke scenario onderzoekt ik inrichten eenheid aanvragen per minuut?</span><span class="sxs-lookup"><span data-stu-id="b98fb-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="b98fb-115">Het gebruik van de portal metrische gegevens om mijn kosten en prestaties te optimaliseren?</span><span class="sxs-lookup"><span data-stu-id="b98fb-115">How to use the portal metrics to optimize my cost and performance?</span></span>
* <span data-ttu-id="b98fb-116">Definiëren welk soort aanvraag kan uw budget RU/m gebruiken?</span><span class="sxs-lookup"><span data-stu-id="b98fb-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="b98fb-117">Inrichting aanvraageenheden per minuut (RU/m)</span><span class="sxs-lookup"><span data-stu-id="b98fb-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="b98fb-118">Als u Azure Cosmos DB inrichten in de tweede samenvattingen (RU/s), krijgt u de garantie dat uw aanvraag is uitgevoerd op een lage latentie als de doorvoer niet de capaciteit ingericht binnen die seconde overschreden.</span><span class="sxs-lookup"><span data-stu-id="b98fb-118">When you provision Azure Cosmos DB at the second granularity (RU/s), you get the guarantee that your request succeeds at a low latency if your throughput has not exceeded the capacity provisioned within that second.</span></span> <span data-ttu-id="b98fb-119">Met RU/m, wordt de granulatie is op het moment met de garantie dat uw aanvraag is gelukt binnen die minuut.</span><span class="sxs-lookup"><span data-stu-id="b98fb-119">With RU/m, the granularity is at the minute with the guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="b98fb-120">Vergeleken met het sturen van systemen, zorgen wij ervoor dat de prestaties u voorspelbare en erop kunt u plannen.</span><span class="sxs-lookup"><span data-stu-id="b98fb-120">Compared to bursting systems, we make sure that the performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="b98fb-121">De manier waarop per minuut works inrichting is eenvoudig:</span><span class="sxs-lookup"><span data-stu-id="b98fb-121">The way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="b98fb-122">RU/m wordt in rekening gebracht per uur en naast RU/s.</span><span class="sxs-lookup"><span data-stu-id="b98fb-122">RU/m is billed hourly and in addition to RU/s.</span></span> <span data-ttu-id="b98fb-123">Voor meer informatie gaat u naar Azure Cosmos DB [pagina met prijzen](https://aka.ms/acdbpricing).</span><span class="sxs-lookup"><span data-stu-id="b98fb-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="b98fb-124">RU/m kan worden ingeschakeld op niveau verzameling.</span><span class="sxs-lookup"><span data-stu-id="b98fb-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="b98fb-125">Dat kan worden gedaan via de SDK's (Node.js, Java of .net) of via de portal (ook MongoDB API werkbelastingen bevatten)</span><span class="sxs-lookup"><span data-stu-id="b98fb-125">That can be done through the SDKs (Node.js, Java, or .Net) or through the portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="b98fb-126">Als RU/m is ingeschakeld voor elke 100 RU/s ingericht, krijgt u ook 1000 RU/m ingericht (de verhouding is 10 x)</span><span class="sxs-lookup"><span data-stu-id="b98fb-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (the ratio is 10x)</span></span>
* <span data-ttu-id="b98fb-127">Op een tweede opgegeven, een aanvraag-eenheid verbruikt uw RU/m inrichting alleen als u hebt overschreden uw per tweede inrichting binnen die seconde</span><span class="sxs-lookup"><span data-stu-id="b98fb-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="b98fb-128">Als de periode 60 seconden (UTC) is beëindigd, de per minuut inrichting wordt aangevuld</span><span class="sxs-lookup"><span data-stu-id="b98fb-128">Once the 60-second period (UTC) ends, the per minute provisioning is refilled</span></span>
* <span data-ttu-id="b98fb-129">RU/m kan alleen worden ingeschakeld voor verzamelingen met een maximale inrichting van 5000 RU/s per partitie.</span><span class="sxs-lookup"><span data-stu-id="b98fb-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="b98fb-130">Als u de doorvoerbehoeften van uw schalen en een hoog niveau voor het leveren van per partitie, ontvangt u een waarschuwingsbericht weergegeven</span><span class="sxs-lookup"><span data-stu-id="b98fb-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="b98fb-131">Hieronder wordt een voorbeeld van een concreet, waarin een klant 10kRU/s met 100kRU/m kunt inrichten 73% opslaan in kosten inrichten voor piek (bij 50kRU per seconde) tot en met een periode van 90 seconden op een verzameling die 10.000 is RU/s en 100.000 RU/m ingericht:</span><span class="sxs-lookup"><span data-stu-id="b98fb-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="b98fb-132">1 seconde: het budget RU/m is ingesteld op 100.000</span><span class="sxs-lookup"><span data-stu-id="b98fb-132">1st second: The RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="b98fb-133">tweede 3e: tijdens deze tweede is het verbruik van aanvragen eenheid 11,010 RUs, 1,010 RUs boven het inrichten van RU/s.</span><span class="sxs-lookup"><span data-stu-id="b98fb-133">3rd second: During that second the consumption of Request Unit was 11,010 RUs, 1,010 RUs above the RU/s provisioning.</span></span> <span data-ttu-id="b98fb-134">Daarom worden 1,010 RUs van het budget RU/m afgetrokken.</span><span class="sxs-lookup"><span data-stu-id="b98fb-134">Therefore, 1,010 RUs are deducted from the RU/m budget.</span></span> <span data-ttu-id="b98fb-135">98,990 RUs zijn beschikbaar voor de volgende 57 seconden in het budget RU/m</span><span class="sxs-lookup"><span data-stu-id="b98fb-135">98,990 RUs are available for the next 57 seconds in the RU/m budget</span></span>
* <span data-ttu-id="b98fb-136">29 seconde: tijdens deze tweede, een grote piek is er gebeurd (> 4 x hoger is dan de inrichting per seconde) en het verbruik van aanvragen eenheid 46,920 RUs is.</span><span class="sxs-lookup"><span data-stu-id="b98fb-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and the consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="b98fb-137">36,920 RUs worden afgetrokken van het budget RU/m verwijderd uit 92,323 RUs (28 seconde) naar 55,403 RUs (29 seconde)</span><span class="sxs-lookup"><span data-stu-id="b98fb-137">36,920 RUs are deducted from the RU/m budget that dropped from 92,323 RUs (28th second) to 55,403 RUs (29th second)</span></span>
* <span data-ttu-id="b98fb-138">61st seconde: RU/m budget wordt opnieuw ingesteld op 100.000 RUs.</span><span class="sxs-lookup"><span data-stu-id="b98fb-138">61st second: RU/m budget is set back to 100,000 RUs.</span></span>
 
![Grafiek weer met het verbruik en de inrichting van Azure DB die Cosmos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="b98fb-140">Capaciteit van de aanvraag-eenheid opgeven met RU/m</span><span class="sxs-lookup"><span data-stu-id="b98fb-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="b98fb-141">Bij het maken van een verzameling Azure Cosmos DB u opgeven dat het aantal aanvraageenheden per seconde (ru/s per seconde) die u wilt reserveren voor de verzameling.</span><span class="sxs-lookup"><span data-stu-id="b98fb-141">When creating an Azure Cosmos DB collection, you specify the number of request units per second (RU per second) you want reserved for the collection.</span></span> <span data-ttu-id="b98fb-142">U kunt ook bepalen of u wilt toevoegen RU per minuut.</span><span class="sxs-lookup"><span data-stu-id="b98fb-142">You can also decide if you want to add RU per minute.</span></span> <span data-ttu-id="b98fb-143">Dit kan worden gedaan via de Portal of de SDK.</span><span class="sxs-lookup"><span data-stu-id="b98fb-143">This can be done through the Portal or the SDK.</span></span> 

### <a name="through-the-portal"></a><span data-ttu-id="b98fb-144">Via de Portal</span><span class="sxs-lookup"><span data-stu-id="b98fb-144">Through the Portal</span></span>

<span data-ttu-id="b98fb-145">In- of uitschakelen van RU per minuut hoeven alleen een Klik bij het inrichten van een verzameling.</span><span class="sxs-lookup"><span data-stu-id="b98fb-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Schermopname die laat zien hoe RU/m instelt in de Azure portal](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-the-sdk"></a><span data-ttu-id="b98fb-147">Via de SDK</span><span class="sxs-lookup"><span data-stu-id="b98fb-147">Through the SDK</span></span>
<span data-ttu-id="b98fb-148">Eerst is dit belangrijk te weten RU/m is alleen beschikbaar voor de volgende SDK's:</span><span class="sxs-lookup"><span data-stu-id="b98fb-148">First, this is important to note that RU/m is only available for the following SDKs:</span></span>

* <span data-ttu-id="b98fb-149">.NET 1.14.0</span><span class="sxs-lookup"><span data-stu-id="b98fb-149">.Net 1.14.0</span></span>
* <span data-ttu-id="b98fb-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="b98fb-150">Java 1.11.0</span></span>
* <span data-ttu-id="b98fb-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="b98fb-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="b98fb-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="b98fb-152">Python 2.2.0</span></span>

<span data-ttu-id="b98fb-153">Hier volgt een codefragment voor het maken van een verzameling met 3000 aanvraageenheden per tweede en 30.000 aanvraageenheden per minuut met de .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="b98fb-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using the .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set the throughput to 3,000 request units per second which will give you 30,000 request units per minute as the RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="b98fb-154">Hier volgt een codefragment voor het wijzigen van de doorvoer van een verzameling in 5000 aanvraageenheden per seconde zonder inrichting RU per minuut met de .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="b98fb-154">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second without provisioning RU per minute using the .NET SDK:</span></span>

```csharp
// Get the current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to 5000 request units per second without RU/m enabled (the last parameter to OfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="b98fb-155">Goede aanpassen aan scenario 's</span><span class="sxs-lookup"><span data-stu-id="b98fb-155">Good fit scenarios</span></span>

<span data-ttu-id="b98fb-156">In deze sectie bieden we een overzicht van scenario's die geschikt zijn voor het inschakelen van aanvraageenheden per minuut.</span><span class="sxs-lookup"><span data-stu-id="b98fb-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="b98fb-157">**Omgeving dev/Test:** geschikt.</span><span class="sxs-lookup"><span data-stu-id="b98fb-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="b98fb-158">Tijdens de ontwikkeling, als u uw toepassing met verschillende werkbelastingen, test krijgt RU/m u de flexibiliteit in deze fase.</span><span class="sxs-lookup"><span data-stu-id="b98fb-158">During the development stage, if you are testing your application with different workloads, RU/m can provide the flexibility at this stage.</span></span> <span data-ttu-id="b98fb-159">Terwijl de [emulator](local-emulator.md) is een uitstekend gratis hulpprogramma voor het testen van Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b98fb-159">While the [emulator](local-emulator.md) is a great free tool to test Azure Cosmos DB.</span></span> <span data-ttu-id="b98fb-160">Maar als u starten in een cloudomgeving wilt, hebt u een hoge mate van flexibiliteit met RU/m voor de behoeften van uw ad-hoc-prestaties.</span><span class="sxs-lookup"><span data-stu-id="b98fb-160">However if you want to start in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="b98fb-161">U kwijt meer tijd ontwikkelt, minder zorgen over prestatiebehoeften op het eerste.</span><span class="sxs-lookup"><span data-stu-id="b98fb-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="b98fb-162">We het beste beginnen met de minimale RU/s-inrichting en RU/m inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b98fb-162">We recommend starting with the minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="b98fb-163">**Onvoorspelbare, spiky, minuut granulatie moet:** goed past – besparingen: 25 75%.</span><span class="sxs-lookup"><span data-stu-id="b98fb-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="b98fb-164">Wij hebben grote verbetering van RU/m en de meeste scenario's voor productie zijn in die groep.</span><span class="sxs-lookup"><span data-stu-id="b98fb-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="b98fb-165">Als u een IoT-werkbelasting met piek enkele keren in een minuut hebt als u een query uitvoeren wanneer het systeem massaopslag invoegen op hetzelfde moment laat hebt, moet u extra capaciteit voor handeling spiky behoeften.</span><span class="sxs-lookup"><span data-stu-id="b98fb-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at the same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="b98fb-166">Het is raadzaam om uw resourcebehoeften optimaliseren door het toepassen van onze onderstaande stapsgewijze benadering.</span><span class="sxs-lookup"><span data-stu-id="b98fb-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![Grafiek met aanvraag verbruik in vijf minuten granulatie](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="b98fb-168">*Afbeelding - RU verbruik benchmark*</span><span class="sxs-lookup"><span data-stu-id="b98fb-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="b98fb-169">**Gemoedsrust:** goed past – besparingen: 10-20%.</span><span class="sxs-lookup"><span data-stu-id="b98fb-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="b98fb-170">Soms wilt gemoedsrust hebt en u geen zorgen over potentiële pieken en beperking.</span><span class="sxs-lookup"><span data-stu-id="b98fb-170">Sometimes, you just want to have peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="b98fb-171">Deze functie is de juiste is voor u.</span><span class="sxs-lookup"><span data-stu-id="b98fb-171">This feature is the right one for you.</span></span> <span data-ttu-id="b98fb-172">In dat geval wordt aangeraden RU/m inschakelen en iets lagere uw per tweede inrichten.</span><span class="sxs-lookup"><span data-stu-id="b98fb-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="b98fb-173">In dit geval verschilt van de bovenstaande als u niet wilt optimaliseren agressief uw inrichten.</span><span class="sxs-lookup"><span data-stu-id="b98fb-173">This case is different from the above as you will not try to optimize aggressively your provisioning.</span></span> <span data-ttu-id="b98fb-174">Dit is van een 'Nul beperking' denkt in.</span><span class="sxs-lookup"><span data-stu-id="b98fb-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="b98fb-175">Kritieke bewerkingen met ad-hoc-behoeften: soms het is raadzaam om alleen kritieke bewerkingen toegang RU/m budget zodat het budget niet gebruiken met ad-hoc of minder belangrijke bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="b98fb-175">Critical operations with adhoc needs: We sometimes recommend to only let critical operations access RU/m budget so the budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="b98fb-176">Dat kan eenvoudig worden gedefinieerd in de onderstaande sectie.</span><span class="sxs-lookup"><span data-stu-id="b98fb-176">That can be easily defined in the section below.</span></span>

## <a name="using-the-portal-metrics-to-optimize-cost-and-performance"></a><span data-ttu-id="b98fb-177">Met behulp van de portal metrische gegevens om kosten en prestaties te optimaliseren</span><span class="sxs-lookup"><span data-stu-id="b98fb-177">Using the portal metrics to optimize cost and performance</span></span>

<span data-ttu-id="b98fb-178">**De komende weken wordt er verdere ontwikkeling van de inhoud om de bewaking van RUs minuut verbruik voor het optimaliseren van de doorvoerbehoeften van uw.**</span><span class="sxs-lookup"><span data-stu-id="b98fb-178">**In the coming weeks, we will further develop the content around monitoring RUs minute consumption to optimize your throughput needs.**</span></span>

<span data-ttu-id="b98fb-179">Via de portal metrische gegevens en kunt u zien hoeveel reguliere RU seconden u versus RU verbruikt minuten.</span><span class="sxs-lookup"><span data-stu-id="b98fb-179">Through the portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="b98fb-180">Bewaking van deze metrische gegevens kunt u uw inrichting optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="b98fb-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="b98fb-181">U wordt aangeraden een stapsgewijze benadering voor het gebruik van RU/m in uw voordeel.</span><span class="sxs-lookup"><span data-stu-id="b98fb-181">We recommend a step by step approach on how to use RU/m to your advantage.</span></span> <span data-ttu-id="b98fb-182">Voor elke stap moet u een overzicht van het RU-verbruik voor een volledige cyclus van uw werkbelasting (mogelijk uren, dagen, of zelfs weken) hebben en inzichten te verkrijgen over het gebruik van wat u inrichten.</span><span class="sxs-lookup"><span data-stu-id="b98fb-182">For each step, you should have an overview of the RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on the utilization of what you provision.</span></span>

<span data-ttu-id="b98fb-183">Het principe achter deze benadering is om de doorvoer inrichting zo dicht mogelijk bij een inrichting punt die overeenkomt met de van de onderstaande prestatiecriteria.</span><span class="sxs-lookup"><span data-stu-id="b98fb-183">The principle behind this approach is to make your throughput provisioning as close as possible to a provisioning point that matches your performance criteria below.</span></span> 

![Grafiek met aanvraag verbruik in samenvattingen van 5 minuten](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="b98fb-185">Om de optimale inrichting punt voor uw workload te begrijpen, moet u begrijpen:</span><span class="sxs-lookup"><span data-stu-id="b98fb-185">To understand the optimal provisioning point for your workload, you need to understand:</span></span>

* <span data-ttu-id="b98fb-186">Verbruik patronen: Nee, incidentele of volgehouden pieken?</span><span class="sxs-lookup"><span data-stu-id="b98fb-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="b98fb-187">(2 x gemiddelde) klein, Gemiddeld of grote (> 10 x gemiddelde) pieken?</span><span class="sxs-lookup"><span data-stu-id="b98fb-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="b98fb-188">Percentage van beperkte aanvragen: bent u ervan overtuigd bent als er een stukje beperking?</span><span class="sxs-lookup"><span data-stu-id="b98fb-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="b98fb-189">Zo ja, in welke mate?</span><span class="sxs-lookup"><span data-stu-id="b98fb-189">If so, by how much?</span></span> 

<span data-ttu-id="b98fb-190">Als u wat uw doelstellingen zijn weet, kunt u zich kunt dichter bij de optimale inrichting.</span><span class="sxs-lookup"><span data-stu-id="b98fb-190">Once you have identified what your goals are, you will be able to get closer to the optimal provisioning.</span></span>

<span data-ttu-id="b98fb-191">Om u te helpen, willen we bieden een algemene richtlijn voor het optimaliseren van de inrichting op basis van uw verbruik RU/m.</span><span class="sxs-lookup"><span data-stu-id="b98fb-191">To assist you, we want to provide an overall guidance on how to optimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="b98fb-192">In deze richtlijnen niet van toepassing op alle soort werkbelasting, maar is gebaseerd op de kennis private preview.</span><span class="sxs-lookup"><span data-stu-id="b98fb-192">This guidance doesn’t apply to all kind of workloads but is based on the private preview knowledge.</span></span> <span data-ttu-id="b98fb-193">Dergelijke basislijnen kan worden gewijzigd als er meer informatie:</span><span class="sxs-lookup"><span data-stu-id="b98fb-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="b98fb-194">RU/m % gebruik</span><span class="sxs-lookup"><span data-stu-id="b98fb-194">RU/m % utilization</span></span>|<span data-ttu-id="b98fb-195">Mate van gebruik van RU/m</span><span class="sxs-lookup"><span data-stu-id="b98fb-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="b98fb-196">Aanbevolen acties voor het inrichten</span><span class="sxs-lookup"><span data-stu-id="b98fb-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="b98fb-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="b98fb-197">0-1%</span></span>|<span data-ttu-id="b98fb-198">Onder gebruik</span><span class="sxs-lookup"><span data-stu-id="b98fb-198">Under utilization</span></span>|<span data-ttu-id="b98fb-199">Lagere RU/s meer RU/m gebruiken</span><span class="sxs-lookup"><span data-stu-id="b98fb-199">Lower RU/s to consume more RU/m</span></span>|
|<span data-ttu-id="b98fb-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="b98fb-200">1-10%</span></span>|<span data-ttu-id="b98fb-201">Gebruik in orde</span><span class="sxs-lookup"><span data-stu-id="b98fb-201">Healthy use</span></span>|<span data-ttu-id="b98fb-202">Bewaren van hetzelfde niveau van inrichting</span><span class="sxs-lookup"><span data-stu-id="b98fb-202">Keep the same provisioning level</span></span>|
|<span data-ttu-id="b98fb-203">Meer dan 10%</span><span class="sxs-lookup"><span data-stu-id="b98fb-203">Above 10%</span></span>|<span data-ttu-id="b98fb-204">Overmatig gebruik</span><span class="sxs-lookup"><span data-stu-id="b98fb-204">Over utilization</span></span>|<span data-ttu-id="b98fb-205">RU/s minder op RU/m beroep te verhogen</span><span class="sxs-lookup"><span data-stu-id="b98fb-205">Increase RU/s to rely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-the-rum-budget"></a><span data-ttu-id="b98fb-206">Selecteer welke bewerkingen kunnen het budget RU/m gebruiken</span><span class="sxs-lookup"><span data-stu-id="b98fb-206">Select which operations can consume the RU/m budget</span></span>

<span data-ttu-id="b98fb-207">Op het niveau van de aanvraag, u kunt ook in-of uitschakelen RU/m-budget voor de aanvraag ongeacht bewerkingstype.</span><span class="sxs-lookup"><span data-stu-id="b98fb-207">At request level, you can also enable/disable RU/m budget to serve the request irrespective of operation type.</span></span> <span data-ttu-id="b98fb-208">Als reguliere ingerichte RUs per seconde budget verbruikt en de aanvraag kan niet het budget RU/m gebruiken, is deze aanvraag wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="b98fb-208">If regular provisioned RUs/sec budget is consumed and the request cannot consume the RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="b98fb-209">Standaard wordt elk verzoek afgehandeld door RU/m budget als RU/m doorvoer budget is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="b98fb-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="b98fb-210">Hier volgt een codefragment voor het uitschakelen van RU/m budget met de DocumentDB-API voor CRUD en query-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="b98fb-210">Here is a code snippet for disabling RU/m budget using the DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order to disable any CRUD request for RU/m, set DisableRUPerMinuteUsage to true in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order to disable any query request for RU/m, set DisableRUPerMinuteOnRequest to true in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="b98fb-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b98fb-211">Next steps</span></span>

<span data-ttu-id="b98fb-212">In dit artikel hebt wordt beschreven hoe partitionering werkt in Azure Cosmos DB, hoe u gepartitioneerde verzamelingen kunt maken en hoe u een goede partitiesleutel kunt verzamelen voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b98fb-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="b98fb-213">Schaal en prestaties testen met Azure Cosmos DB uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b98fb-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="b98fb-214">Zie [prestaties en schaal testen met Azure Cosmos DB](performance-testing.md) voor een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b98fb-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="b98fb-215">Aan de slag programmeren met de [SDK's](documentdb-sdk-dotnet.md) of de [REST-API](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="b98fb-215">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="b98fb-216">Meer informatie over [ingerichte doorvoer](request-units.md) in Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="b98fb-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

