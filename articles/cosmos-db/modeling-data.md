---
title: aaaModeling documentgegevens voor een NoSQL-database | Microsoft Docs
description: Meer informatie over het modelleren van gegevens voor NoSQL-databases
keywords: modellering van gegevens
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig1
documentationcenter: 
ms.assetid: 69521eb9-590b-403c-9b36-98253a4c88b5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2016
ms.author: arramac
ms.openlocfilehash: 2e388c833f204287896dfa8e6f79c88073731b6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="55aaa-104">Modeling documentgegevens voor NoSQL-databases</span><span class="sxs-lookup"><span data-stu-id="55aaa-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="55aaa-105">Terwijl databases zonder schema, zoals Azure Cosmos DB, kunnen u heel eenvoudig tooembrace wijzigingen tooyour gegevensmodel u moet nog steeds te besteden aan de enige tijd nadenken over uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="55aaa-105">While schema-free databases, like Azure Cosmos DB, make it super easy tooembrace changes tooyour data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="55aaa-106">Hoe gaat gegevens toobe opgeslagen?</span><span class="sxs-lookup"><span data-stu-id="55aaa-106">How is data going toobe stored?</span></span> <span data-ttu-id="55aaa-107">Hoe wordt uw toepassing gaat tooretrieve en query gegevens?</span><span class="sxs-lookup"><span data-stu-id="55aaa-107">How is your application going tooretrieve and query data?</span></span> <span data-ttu-id="55aaa-108">Is uw toepassing dikke lezen of schrijven zwaar?</span><span class="sxs-lookup"><span data-stu-id="55aaa-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="55aaa-109">Na het lezen van dit artikel kunt u zich kunt tooanswer Hallo vragen te volgen:</span><span class="sxs-lookup"><span data-stu-id="55aaa-109">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="55aaa-110">Hoe moet ik denken dat zij een document in een documentdatabase?</span><span class="sxs-lookup"><span data-stu-id="55aaa-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="55aaa-111">Wat is er gegevens modelleren en waarom moet ik het belangrijkst?</span><span class="sxs-lookup"><span data-stu-id="55aaa-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="55aaa-112">Hoe wordt modellering gegevens in een document verschillende tooa relationele database?</span><span class="sxs-lookup"><span data-stu-id="55aaa-112">How is modeling data in a document database different tooa relational database?</span></span>
* <span data-ttu-id="55aaa-113">Hoe ik gegevensrelaties in een niet-relationele database express?</span><span class="sxs-lookup"><span data-stu-id="55aaa-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="55aaa-114">Wanneer insluiten gegevens en wanneer koppelen toodata?</span><span class="sxs-lookup"><span data-stu-id="55aaa-114">When do I embed data and when do I link toodata?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="55aaa-115">Gegevens insluiten</span><span class="sxs-lookup"><span data-stu-id="55aaa-115">Embedding data</span></span>
<span data-ttu-id="55aaa-116">Wanneer u gegevens in een store, document, zoals Azure Cosmos DB modelleren start probeer tootreat uw entiteiten als **zelfstandig documenten** vertegenwoordigd in JSON.</span><span class="sxs-lookup"><span data-stu-id="55aaa-116">When you start modeling data in a document store, such as Azure Cosmos DB, try tootreat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="55aaa-117">Voordat we meteen te veel meer laat het ons Neem een paar stappen terug en bekijk hoe wij iets in een relationele database, een onderwerp dat velen van ons al bekend met bent mogelijk model.</span><span class="sxs-lookup"><span data-stu-id="55aaa-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="55aaa-118">Hallo volgende voorbeeld ziet u hoe een persoon kan worden opgeslagen in een relationele database.</span><span class="sxs-lookup"><span data-stu-id="55aaa-118">hello following example shows how a person might be stored in a relational database.</span></span> 

![Relationele database-model](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="55aaa-120">Als u werkt met relationele databases we hebt geleerd voor jaar toonormalize, normaliseren, normaliseren.</span><span class="sxs-lookup"><span data-stu-id="55aaa-120">When working with relational databases, we've been taught for years toonormalize, normalize, normalize.</span></span>

<span data-ttu-id="55aaa-121">Doorgaans normaliseren van uw gegevens omvat het maken van een entiteit, zoals een persoon, en splitsen in stukken toodiscrete van gegevens.</span><span class="sxs-lookup"><span data-stu-id="55aaa-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in toodiscrete pieces of data.</span></span> <span data-ttu-id="55aaa-122">In bovenstaande Hallo voorbeeld, kan een persoon meerdere details van contactpersonen records, alsmede meerdere adresrecords hebben.</span><span class="sxs-lookup"><span data-stu-id="55aaa-122">In hello example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="55aaa-123">We zelfs nog een stapje verder te gaan en contactgegevens onderverdelen per verdere uitpakken algemene velden, zoals een type.</span><span class="sxs-lookup"><span data-stu-id="55aaa-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="55aaa-124">Hetzelfde adres, heeft elke record hier een type zoals *Start* of *Business*</span><span class="sxs-lookup"><span data-stu-id="55aaa-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="55aaa-125">Hallo premises wegwijs als normalisatie van gegevens te**Vermijd redundante gegevens op te slaan** op elke registreren en in plaats daarvan toodata verwijzen.</span><span class="sxs-lookup"><span data-stu-id="55aaa-125">hello guiding premise when normalizing data is too**avoid storing redundant data** on each record and rather refer toodata.</span></span> <span data-ttu-id="55aaa-126">In dit voorbeeld tooread een persoon, met hun contactgegevens en adressen, moet u toouse JOINS tooeffectively Cumulatieve uitvoeringstijd van uw gegevens op.</span><span class="sxs-lookup"><span data-stu-id="55aaa-126">In this example, tooread a person, with all their contact details and addresses, you need toouse JOINS tooeffectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="55aaa-127">Bijwerken van één persoon met hun contactgegevens en adressen vereist schrijfbewerkingen over veel afzonderlijke tabellen.</span><span class="sxs-lookup"><span data-stu-id="55aaa-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="55aaa-128">Nu gaan we kijken hoe we zou model nemen Hallo dezelfde gegevens als een zelfstandig entiteit in de documentdatabase van een.</span><span class="sxs-lookup"><span data-stu-id="55aaa-128">Now let's take a look at how we would model hello same data as a self-contained entity in a document database.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email: "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

<span data-ttu-id="55aaa-129">Met Hallo benadering bovenstaande we nu hebben **gedenormaliseerd** Hallo persoonsrecord waar we **ingesloten** alle informatie over toothis persoon, zoals hun contactgegevens en -adressen in één tooa Hallo JSON-document.</span><span class="sxs-lookup"><span data-stu-id="55aaa-129">Using hello approach above we have now **denormalized** hello person record where we **embedded** all hello information relating toothis person, such as their contact details and addresses, in tooa single JSON document.</span></span>
<span data-ttu-id="55aaa-130">Bovendien omdat we niet beperkt blijven vast tooa schema we hebben Hallo flexibiliteit toodo dingen alsof u contactgegevens van verschillende vormen volledig.</span><span class="sxs-lookup"><span data-stu-id="55aaa-130">In addition, because we're not confined tooa fixed schema we have hello flexibility toodo things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="55aaa-131">Bij het ophalen van een persoonsrecord voltooid uit Hallo-database is nu één bewerking met betrekking tot één verzameling en voor één document te lezen.</span><span class="sxs-lookup"><span data-stu-id="55aaa-131">Retrieving a complete person record from hello database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="55aaa-132">Bijwerken van een persoonsrecord met hun contactgegevens en -adressen is ook een schrijfbewerking voor één voor één document.</span><span class="sxs-lookup"><span data-stu-id="55aaa-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="55aaa-133">Door gegevens denormalizing, uw toepassing moet mogelijk tooissue minder query's en updates toocomplete algemene bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="55aaa-133">By denormalizing data, your application may need tooissue fewer queries and updates toocomplete common operations.</span></span> 

### <a name="when-tooembed"></a><span data-ttu-id="55aaa-134">Wanneer tooembed</span><span class="sxs-lookup"><span data-stu-id="55aaa-134">When tooembed</span></span>
<span data-ttu-id="55aaa-135">In het algemeen gebruikt ingesloten gegevens modellen wanneer:</span><span class="sxs-lookup"><span data-stu-id="55aaa-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="55aaa-136">Er zijn **bevat** relaties tussen entiteiten.</span><span class="sxs-lookup"><span data-stu-id="55aaa-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="55aaa-137">Er zijn **één aan enkele** relaties tussen entiteiten.</span><span class="sxs-lookup"><span data-stu-id="55aaa-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="55aaa-138">Er zijn ingesloten gegevens die **niet vaak veranderen**.</span><span class="sxs-lookup"><span data-stu-id="55aaa-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="55aaa-139">Er is ingesloten gegevens won't groeien **zonder gebonden**.</span><span class="sxs-lookup"><span data-stu-id="55aaa-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="55aaa-140">Er is ingesloten gegevens **integraal** toodata in een document.</span><span class="sxs-lookup"><span data-stu-id="55aaa-140">There is embedded data that is **integral** toodata in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="55aaa-141">Doorgaans data-modellen beter bieden gedenormaliseerd **lezen** prestaties.</span><span class="sxs-lookup"><span data-stu-id="55aaa-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-tooembed"></a><span data-ttu-id="55aaa-142">Wanneer niet tooembed</span><span class="sxs-lookup"><span data-stu-id="55aaa-142">When not tooembed</span></span>
<span data-ttu-id="55aaa-143">Hallo databasebestandsgrootte in een documentdatabase toodenormalize is alles en sluit alle gegevens in één document tooa, dit kan ertoe leiden toosome situaties die moeten worden vermeden.</span><span class="sxs-lookup"><span data-stu-id="55aaa-143">While hello rule of thumb in a document database is toodenormalize everything and embed all data in tooa single document, this can lead toosome situations that should be avoided.</span></span>

<span data-ttu-id="55aaa-144">Deze JSON-fragment in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="55aaa-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="55aaa-145">Dit is mogelijk wat een post-entiteit met ingesloten opmerkingen eruit zou als we een typische blog of CMS, systeem zijn modelleren.</span><span class="sxs-lookup"><span data-stu-id="55aaa-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="55aaa-146">Hallo probleem met dit voorbeeld is dat Hallo opmerkingen matrix is **unbounded**, wat betekent dat er geen limiet (praktische) toohello aantal opmerkingen eventuele één post kan hebben.</span><span class="sxs-lookup"><span data-stu-id="55aaa-146">hello problem with this example is that hello comments array is **unbounded**, meaning that there is no (practical) limit toohello number of comments any single post can have.</span></span> <span data-ttu-id="55aaa-147">Dit wordt een probleem worden naarmate Hallo grootte van het Hallo-document kan aanzienlijk toenemen.</span><span class="sxs-lookup"><span data-stu-id="55aaa-147">This will become a problem as hello size of hello document could grow significantly.</span></span>

<span data-ttu-id="55aaa-148">Als de grootte Hallo Hallo groeit document Hallo mogelijkheid tootransmit Hallo gegevens via de kabel hello, evenals lezen en bijwerken Hallo-document, op schaal worden beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="55aaa-148">As hello size of hello document grows hello ability tootransmit hello data over hello wire as well as reading and updating hello document, at scale, will be impacted.</span></span>

<span data-ttu-id="55aaa-149">In dit geval zou het beter tooconsider Hallo na model zijn.</span><span class="sxs-lookup"><span data-stu-id="55aaa-149">In this case it would be better tooconsider hello following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from hello field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

<span data-ttu-id="55aaa-150">Dit model heeft Hallo drie meest recente commentaar dat op Hallo van ingesloten zelf, zoals een matrix met een vaste gebonden is dit tijdstip.</span><span class="sxs-lookup"><span data-stu-id="55aaa-150">This model has hello three most recent comments embedded on hello post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="55aaa-151">Hallo andere opmerkingen zijn gegroepeerd in toobatches van 100 opmerkingen en opgeslagen in afzonderlijke documenten.</span><span class="sxs-lookup"><span data-stu-id="55aaa-151">hello other comments are grouped in toobatches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="55aaa-152">Hallo-grootte van Hallo batch is gekozen als 100 omdat de fictieve toepassing kan Hallo 100 gebruikersopmerkingen tooload tegelijk.</span><span class="sxs-lookup"><span data-stu-id="55aaa-152">hello size of hello batch was chosen as 100 because our fictitious application allows hello user tooload 100 comments at a time.</span></span>  

<span data-ttu-id="55aaa-153">Een andere aanvraag ingesloten gegevens waar niet een goed idee is is wanneer Hallo ingesloten gegevens vaak worden gebruikt in de documenten en vaak worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="55aaa-153">Another case where embedding data is not a good idea is when hello embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="55aaa-154">Deze JSON-fragment in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="55aaa-154">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

<span data-ttu-id="55aaa-155">Dit kan leiden tot slot portfolio van een persoon.</span><span class="sxs-lookup"><span data-stu-id="55aaa-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="55aaa-156">We hebt tooembed Hallo voorraad informatie in tooeach portfolio document gekozen.</span><span class="sxs-lookup"><span data-stu-id="55aaa-156">We have chosen tooembed hello stock information in tooeach portfolio document.</span></span> <span data-ttu-id="55aaa-157">Gegevens die regelmatig veranderen insluiten gaat toomean dat u elk document portfolio voortdurend wordt bijgewerkt telkens wanneer een bestand wordt verhandeld in een omgeving waar gerelateerde gegevens vaak wijzigen als een toepassing, handel stock.</span><span class="sxs-lookup"><span data-stu-id="55aaa-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going toomean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="55aaa-158">Stock *zaza* mogen worden verhandeld veel honderden keren in een enkele dag en duizenden gebruikers kunnen hebben *zaza* op hun portfolio.</span><span class="sxs-lookup"><span data-stu-id="55aaa-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="55aaa-159">Met een gegevensmodel zoals hierboven Hallo zou hebben we tooupdate duizenden portfolio documenten vaak dagelijks voorloopspaties tooa system die won't zeer goed worden geschaald.</span><span class="sxs-lookup"><span data-stu-id="55aaa-159">With a data model like hello above we would have tooupdate many thousands of portfolio documents many times every day leading tooa system that won't scale very well.</span></span> 

## <span data-ttu-id="55aaa-160"><a id="Refer"></a>Verwijst naar gegevens</span><span class="sxs-lookup"><span data-stu-id="55aaa-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="55aaa-161">Dus mooi gegevens insluiten werkt voor veel gevallen maar duidelijk is dat er scenario's zijn wanneer uw gegevens denormalizing meer problemen dan het verdient aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="55aaa-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="55aaa-162">Dus wat we doen nu?</span><span class="sxs-lookup"><span data-stu-id="55aaa-162">So what do we do now?</span></span> 

<span data-ttu-id="55aaa-163">Relationele databases zijn niet Hallo enige plaats waar u de relaties tussen entiteiten kunt maken.</span><span class="sxs-lookup"><span data-stu-id="55aaa-163">Relational databases are not hello only place where you can create relationships between entities.</span></span> <span data-ttu-id="55aaa-164">U kunt de informatie in een document dat daadwerkelijk toodata in andere documenten hoort hebben in een documentdatabase.</span><span class="sxs-lookup"><span data-stu-id="55aaa-164">In a document database you can have information in one document that actually relates toodata in other documents.</span></span> <span data-ttu-id="55aaa-165">Nu, ik ben niet pleiten zelfs een minuut dat wij systemen die beter geschikt tooa relationele database in Azure Cosmos-database of een andere documentdatabase maken, maar eenvoudige relaties geen en kunnen zeer nuttig zijn.</span><span class="sxs-lookup"><span data-stu-id="55aaa-165">Now, I am not advocating for even one minute that we build systems that would be better suited tooa relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="55aaa-166">In onderstaande JSON Hallo gekozen we toouse Hallo voorbeeld van een voorraad portfolio van eerder maar dit keer die toohello voorraad item op Hallo portfolio in plaats van het sluiten is.</span><span class="sxs-lookup"><span data-stu-id="55aaa-166">In hello JSON below we chose toouse hello example of a stock portfolio from earlier but this time we refer toohello stock item on hello portfolio instead of embedding it.</span></span> <span data-ttu-id="55aaa-167">Op deze manier is één slot document Hallo wanneer Hallo voorraad item vaak wordt gewijzigd in de gehele Hallo dag Hallo alleen document dat toobe bijgewerkt moet.</span><span class="sxs-lookup"><span data-stu-id="55aaa-167">This way, when hello stock item changes frequently throughout hello day hello only document that needs toobe updated is hello single stock document.</span></span> 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


<span data-ttu-id="55aaa-168">Een onmiddellijke neerwaartse toothis-methode is echter als uw toepassing vereist tooshow informatie over elke voorraad die wordt veroorzaakt is bij het weergeven van een persoon portfolio; in dit geval moet u toomake meerdere reizen toohello tooload Hallo databasegegevens voor elk document voorraad.</span><span class="sxs-lookup"><span data-stu-id="55aaa-168">An immediate downside toothis approach though is if your application is required tooshow information about each stock that is held when displaying a person's portfolio; in this case you would need toomake multiple trips toohello database tooload hello information for each stock document.</span></span> <span data-ttu-id="55aaa-169">We hebben hier een beslissing tooimprove Hallo efficiëntie van schrijfbewerkingen die vaak gedurende de dag van de Hallo gebeuren, maar op zijn beurt inbreuk op Hallo leesbewerkingen die mogelijk minder invloed op prestaties van dit bepaalde systeem Hallo hebben aangebracht.</span><span class="sxs-lookup"><span data-stu-id="55aaa-169">Here we've made a decision tooimprove hello efficiency of write operations, which happen frequently throughout hello day, but in turn compromised on hello read operations that potentially have less impact on hello performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="55aaa-170">Genormaliseerd gegevensmodellen **kunt vereisen meer retouren** toohello-server.</span><span class="sxs-lookup"><span data-stu-id="55aaa-170">Normalized data models **can require more round trips** toohello server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="55aaa-171">Hoe zit het met refererende sleutels?</span><span class="sxs-lookup"><span data-stu-id="55aaa-171">What about foreign keys?</span></span>
<span data-ttu-id="55aaa-172">Omdat er momenteel geen concept van een beperking, refererende sleutel of anderszins, de relaties tussen document die u in documenten hebt zijn effectief 'zwakke koppelingen' en kunnen niet worden gecontroleerd door Hallo-database zelf.</span><span class="sxs-lookup"><span data-stu-id="55aaa-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by hello database itself.</span></span> <span data-ttu-id="55aaa-173">Als u wilt dat tooensure die gegevens die een document verwijst Hallo tooactually bestaat, moet u toodo dit in uw toepassing of door middel van Hallo van server-side '-triggers of opgeslagen procedures op Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="55aaa-173">If you want tooensure that hello data a document is referring tooactually exists, then you need toodo this in your application, or through hello use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-tooreference"></a><span data-ttu-id="55aaa-174">Wanneer tooreference</span><span class="sxs-lookup"><span data-stu-id="55aaa-174">When tooreference</span></span>
<span data-ttu-id="55aaa-175">In het algemeen gebruikt genormaliseerde gegevens modellen wanneer:</span><span class="sxs-lookup"><span data-stu-id="55aaa-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="55aaa-176">Voor **een-op-veel** relaties.</span><span class="sxs-lookup"><span data-stu-id="55aaa-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="55aaa-177">Voor **veel-op-veel** relaties.</span><span class="sxs-lookup"><span data-stu-id="55aaa-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="55aaa-178">Gerelateerde gegevens **regelmatig wordt gewijzigd**.</span><span class="sxs-lookup"><span data-stu-id="55aaa-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="55aaa-179">Gegevens waarnaar wordt verwezen, kan worden **unbounded**.</span><span class="sxs-lookup"><span data-stu-id="55aaa-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="55aaa-180">Doorgaans normaliseren biedt betere **schrijven** prestaties.</span><span class="sxs-lookup"><span data-stu-id="55aaa-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-hello-relationship"></a><span data-ttu-id="55aaa-181">Waar ik Hallo relatie plaatsen?</span><span class="sxs-lookup"><span data-stu-id="55aaa-181">Where do I put hello relationship?</span></span>
<span data-ttu-id="55aaa-182">Hallo groei van Hallo relatie kunt u bepalen in welke document toostore Hallo-verwijzing.</span><span class="sxs-lookup"><span data-stu-id="55aaa-182">hello growth of hello relationship will help determine in which document toostore hello reference.</span></span>

<span data-ttu-id="55aaa-183">Als we Hallo JSON onderstaande modellen uitgevers en rapporten bekijken.</span><span class="sxs-lookup"><span data-stu-id="55aaa-183">If we look at hello JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over hello world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in tooAzure Cosmos DB" }

<span data-ttu-id="55aaa-184">Als Hallo Hallo books per uitgever aantal kleine met beperkte groei, kan bewaren Hallo adresboek naslaginformatie Hallo publisher-document nuttig zijn.</span><span class="sxs-lookup"><span data-stu-id="55aaa-184">If hello number of hello books per publisher is small with limited growth, then storing hello book reference inside hello publisher document may be useful.</span></span> <span data-ttu-id="55aaa-185">Echter als Hallo aantal boeken per uitgever unbounded is, leiden klikt u vervolgens deze gegevensmodel toomutable, groeiende matrices, zoals in de bovenstaande Hallo voorbeeld publisher-document.</span><span class="sxs-lookup"><span data-stu-id="55aaa-185">However, if hello number of books per publisher is unbounded, then this data model would lead toomutable, growing arrays, as in hello example publisher document above.</span></span> 

<span data-ttu-id="55aaa-186">Overschakelen van dingen rond een bits zou resulteren in een model dat nog steeds vertegenwoordigt dezelfde gegevens nu Hallo voorkomt deze grote veranderlijke verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="55aaa-186">Switching things around a bit would result in a model that still represents hello same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over hello world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in tooAzure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="55aaa-187">In Hallo hierboven voorbeeld hebben we verwijderd Hallo unbounded verzameling op Hallo publisher-document.</span><span class="sxs-lookup"><span data-stu-id="55aaa-187">In hello above example, we have dropped hello unbounded collection on hello publisher document.</span></span> <span data-ttu-id="55aaa-188">In plaats daarvan we zojuist hebben een verwijzing toohello uitgever op elk document adresboek.</span><span class="sxs-lookup"><span data-stu-id="55aaa-188">Instead we just have a a reference toohello publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="55aaa-189">Hoe ik veel: veel-relaties model?</span><span class="sxs-lookup"><span data-stu-id="55aaa-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="55aaa-190">In een relationele database *veel:* relaties zijn vaak gemodelleerd met join-tabellen die records uit andere tabellen NET samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="55aaa-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Tabellen samenvoegen](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="55aaa-192">U mogelijk geneigd tooreplicate Hallo met behulp van dezelfde ding documenten en een gegevensmodel dat vergelijkbare toohello volgende lijkt te produceren.</span><span class="sxs-lookup"><span data-stu-id="55aaa-192">You might be tempted tooreplicate hello same thing using documents and produce a data model that looks similar toohello following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over hello world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in tooAzure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="55aaa-193">Dit zou werken.</span><span class="sxs-lookup"><span data-stu-id="55aaa-193">This would work.</span></span> <span data-ttu-id="55aaa-194">Echter, ofwel een auteur met hun books laden of het laden van een rapport met de auteur zou moet altijd ten minste twee extra query's op Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="55aaa-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against hello database.</span></span> <span data-ttu-id="55aaa-195">Een query toohello document en vervolgens een andere query toofetch Hallo werkelijke document wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="55aaa-195">One query toohello joining document and then another query toofetch hello actual document being joined.</span></span> 

<span data-ttu-id="55aaa-196">Als deze tabel join wordt alleen is lijmen samen twee soorten gegevens waarom niet vermeld het dan niet volledig?</span><span class="sxs-lookup"><span data-stu-id="55aaa-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="55aaa-197">Houd rekening met de volgende Hallo.</span><span class="sxs-lookup"><span data-stu-id="55aaa-197">Consider hello following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="55aaa-198">Nu als ik had een auteur, ik onmiddellijk weet welke boeken deze geschreven en als ik een boekdocument geladen had zou ik omgekeerd Hallo-id van Hallo auteur (s) kent.</span><span class="sxs-lookup"><span data-stu-id="55aaa-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know hello ids of hello author(s).</span></span> <span data-ttu-id="55aaa-199">Hiermee slaat u die tussenliggende query op Hallo join-tabel beperken Hallo van server aantal retouren uw toepassing toomake heeft.</span><span class="sxs-lookup"><span data-stu-id="55aaa-199">This saves that intermediary query against hello join table reducing hello number of server round trips your application has toomake.</span></span> 

## <span data-ttu-id="55aaa-200"><a id="WrapUp"></a>Hybride gegevensmodellen</span><span class="sxs-lookup"><span data-stu-id="55aaa-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="55aaa-201">We nu hebt bekeken insluiten (of denormalizing) en gegevens van verwijzende (of normaliseren), hebben elk hun upsides en elk compromissen hebben, zoals we hebben gezien.</span><span class="sxs-lookup"><span data-stu-id="55aaa-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="55aaa-202">Het niet altijd toobe ofwel heeft of, niet Blazende toomix dingen enigszins worden.</span><span class="sxs-lookup"><span data-stu-id="55aaa-202">It doesn't always have toobe either or, don't be scared toomix things up a little.</span></span> 

<span data-ttu-id="55aaa-203">Op basis van de specifieke gebruikspatronen en werkbelastingen die mogelijk zijn er gevallen waarbij de combinatie van ingesloten van uw toepassing en gegevens waarnaar wordt verwezen is wel zinvol en kan lead toosimpler toepassingslogica met minder server retouren tegelijkertijd nog steeds een goede niveau van de prestaties van .</span><span class="sxs-lookup"><span data-stu-id="55aaa-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead toosimpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="55aaa-204">Overweeg het volgende JSON Hallo.</span><span class="sxs-lookup"><span data-stu-id="55aaa-204">Consider hello following JSON.</span></span> 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

<span data-ttu-id="55aaa-205">Hier hebt we Hallo ingesloten model, waarbij gegevens uit andere entiteiten zijn ingesloten in op het hoogste niveau document hello, maar andere gegevens wordt verwezen (voornamelijk) gevolgd.</span><span class="sxs-lookup"><span data-stu-id="55aaa-205">Here we've (mostly) followed hello embedded model, where data from other entities are embedded in hello top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="55aaa-206">Als u Hallo adresboek document bekijkt, ziet u enkele interessante velden wanneer we hello matrix van auteurs bekijkt.</span><span class="sxs-lookup"><span data-stu-id="55aaa-206">If you look at hello book document, we can see a few interesting fields when we look at hello array of authors.</span></span> <span data-ttu-id="55aaa-207">Er is een *id* veld die is hello gebruiken we toorefer back tooan auteur document, standaard Oefening in een genormaliseerde model, maar vervolgens is ook het veld hebben *naam* en *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="55aaa-207">There is an *id* field which is hello field we use toorefer back tooan author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="55aaa-208">Kan we zojuist hebt vastgelopen met *id* en links Hallo toepassing tooget eventuele aanvullende informatie nodig uit Hallo respectieve auteur document met Hallo "link", maar omdat de naam van de auteur van het Hallo onze toepassing worden weergegeven en een miniatuur met elke adresboek weergegeven we kunt opslaan een round trip toohello server per rapport in een lijst door denormalizing **sommige** gegevens van Hallo auteur.</span><span class="sxs-lookup"><span data-stu-id="55aaa-208">We could've just stuck with *id* and left hello application tooget any additional information it needed from hello respective author document using hello "link", but because our application displays hello author's name and a thumbnail picture with every book displayed we can save a round trip toohello server per book in a list by denormalizing **some** data from hello author.</span></span>

<span data-ttu-id="55aaa-209">Controleer of, als de naam van de auteur van het Hallo gewijzigd of dat ze hun photo tooupdate wilden we zou hebben toogo een update elk rapport ze ooit gepubliceerd, maar voor de toepassing, gebaseerd op Hallo veronderstelling dat auteurs niet hun namen vaak veranderen, is dit een acceptabele ontwerp besluit.</span><span class="sxs-lookup"><span data-stu-id="55aaa-209">Sure, if hello author's name changed or they wanted tooupdate their photo we'd have toogo an update every book they ever published but for our application, based on hello assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="55aaa-210">In het Hallo-voorbeeld zijn er **vooraf berekende aggregaties** toosave dure verwerking op een leesbewerking waarden.</span><span class="sxs-lookup"><span data-stu-id="55aaa-210">In hello example there are **pre-calculated aggregates** values toosave expensive processing on a read operation.</span></span> <span data-ttu-id="55aaa-211">In voorbeeld Hallo zijn Hallo-gegevens in Hallo auteur document ingesloten gegevens die tijdens de uitvoering wordt berekend.</span><span class="sxs-lookup"><span data-stu-id="55aaa-211">In hello example, some of hello data embedded in hello author document is data that is calculated at run-time.</span></span> <span data-ttu-id="55aaa-212">Telkens wanneer een nieuw rapport is gepubliceerd, wordt een boekdocument gemaakt **en** hello countOfBooks veld tooa berekende waarde op basis van het aantal documenten adresboek die beschikbaar zijn voor een bepaalde auteur Hallo is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="55aaa-212">Every time a new book is published, a book document is created **and** hello countOfBooks field is set tooa calculated value based on hello number of book documents that exist for a particular author.</span></span> <span data-ttu-id="55aaa-213">Deze optimalisatie zou zijn goede in lezen zware systemen waar we betaalbare toodo berekeningen bij het schrijven in volgorde toooptimize leest.</span><span class="sxs-lookup"><span data-stu-id="55aaa-213">This optimization would be good in read heavy systems where we can afford toodo computations on writes in order toooptimize reads.</span></span>

<span data-ttu-id="55aaa-214">Hallo mogelijkheid toohave een model met vooraf berekende velden mogelijk gemaakt wordt omdat Azure Cosmos DB ondersteunt **transacties met meerdere documenten**.</span><span class="sxs-lookup"><span data-stu-id="55aaa-214">hello ability toohave a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="55aaa-215">Veel NoSQL-opslag kunnen doen transacties meerdere documenten en daarom pleiten ontwerpbeslissingen, zoals 'altijd insluiten alles', vanwege toothis beperking.</span><span class="sxs-lookup"><span data-stu-id="55aaa-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due toothis limitation.</span></span> <span data-ttu-id="55aaa-216">U kunt met Azure Cosmos DB serverzijde triggers of opgeslagen procedures, die books invoegen en auteurs allemaal binnen een ACID-transactie bijwerken gebruiken.</span><span class="sxs-lookup"><span data-stu-id="55aaa-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="55aaa-217">Nu u geen **hebben** tooembed alles in tooone document alleen toobe u ervoor zorgen dat de gegevens consistent blijft.</span><span class="sxs-lookup"><span data-stu-id="55aaa-217">Now you don't **have** tooembed everything in tooone document just toobe sure that your data remains consistent.</span></span>

## <span data-ttu-id="55aaa-218"><a name="NextSteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="55aaa-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="55aaa-219">Hallo grootste takeaways uit dit artikel is toounderstand dat gegevens in een wereld zonder schema modelleren als ooit net zo belangrijk is.</span><span class="sxs-lookup"><span data-stu-id="55aaa-219">hello biggest takeaways from this article is toounderstand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="55aaa-220">Net als er geen eenduidige manier toorepresent een stukje informatie op een scherm is, zijn er geen enkele manier toomodel uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="55aaa-220">Just as there is no single way toorepresent a piece of data on a screen, there is no single way toomodel your data.</span></span> <span data-ttu-id="55aaa-221">U moet toounderstand uw toepassing en hoe deze wordt produceert, gebruiken en Hallo gegevens verwerken.</span><span class="sxs-lookup"><span data-stu-id="55aaa-221">You need toounderstand your application and how it will produce, consume, and process hello data.</span></span> <span data-ttu-id="55aaa-222">Richtlijnen die hier voorgesteld en u kunnen vervolgens door toe te passen aantal Hallo instellen over het maken van een model die zijn gericht op Hallo onmiddellijke behoeften van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="55aaa-222">Then, by applying some of hello guidelines presented here you can set about creating a model that addresses hello immediate needs of your application.</span></span> <span data-ttu-id="55aaa-223">Wanneer uw toepassingen toochange moeten, kunt u gebruikmaken van Hallo flexibiliteit van een database zonder schema tooembrace die wijzigen en het gegevensmodel van uw eenvoudig ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="55aaa-223">When your applications need toochange, you can leverage hello flexibility of a schema-free database tooembrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="55aaa-224">toolearn meer informatie over Azure Cosmos DB toohello-service verwijzen [documentatie](https://azure.microsoft.com/documentation/services/cosmos-db/) pagina.</span><span class="sxs-lookup"><span data-stu-id="55aaa-224">toolearn more about Azure Cosmos DB, refer toohello service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="55aaa-225">toounderstand hoe tooshard van uw gegevens over meerdere partities verwijzen te[partitioneren van gegevens in Azure Cosmos DB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="55aaa-225">toounderstand how tooshard your data across multiple partitions, refer too[Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
