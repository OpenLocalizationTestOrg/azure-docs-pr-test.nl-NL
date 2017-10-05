---
title: Modeling documentgegevens voor een NoSQL-database | Microsoft Docs
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
ms.openlocfilehash: 16c387fe574243544cf54cf283c7713ddcaa1942
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="6d746-104">Modeling documentgegevens voor NoSQL-databases</span><span class="sxs-lookup"><span data-stu-id="6d746-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="6d746-105">Terwijl databases zonder schema, zoals Azure Cosmos DB, u kunnen heel eenvoudig om af te spelen op wijzigingen in het gegevensmodel u moet nog steeds hoeven te besteden aan bepaalde tijd na te denken over uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="6d746-105">While schema-free databases, like Azure Cosmos DB, make it super easy to embrace changes to your data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="6d746-106">Hoe er gegevens worden opgeslagen?</span><span class="sxs-lookup"><span data-stu-id="6d746-106">How is data going to be stored?</span></span> <span data-ttu-id="6d746-107">Hoe uw toepassing gaat op te halen en het opvragen van gegevens?</span><span class="sxs-lookup"><span data-stu-id="6d746-107">How is your application going to retrieve and query data?</span></span> <span data-ttu-id="6d746-108">Is uw toepassing dikke lezen of schrijven zwaar?</span><span class="sxs-lookup"><span data-stu-id="6d746-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="6d746-109">Na het lezen van dit artikel kunt u zich de volgende vragen beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="6d746-109">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="6d746-110">Hoe moet ik denken dat zij een document in een documentdatabase?</span><span class="sxs-lookup"><span data-stu-id="6d746-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="6d746-111">Wat is er gegevens modelleren en waarom moet ik het belangrijkst?</span><span class="sxs-lookup"><span data-stu-id="6d746-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="6d746-112">Hoe wordt modellering gegevens in een documentdatabase in een relationele database?</span><span class="sxs-lookup"><span data-stu-id="6d746-112">How is modeling data in a document database different to a relational database?</span></span>
* <span data-ttu-id="6d746-113">Hoe ik gegevensrelaties in een niet-relationele database express?</span><span class="sxs-lookup"><span data-stu-id="6d746-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="6d746-114">Wanneer insluiten gegevens en wanneer kan ik gegevens koppelen?</span><span class="sxs-lookup"><span data-stu-id="6d746-114">When do I embed data and when do I link to data?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="6d746-115">Gegevens insluiten</span><span class="sxs-lookup"><span data-stu-id="6d746-115">Embedding data</span></span>
<span data-ttu-id="6d746-116">Wanneer u gegevens in een store, document, zoals Azure Cosmos DB modelleren start probeer uw entiteiten behandelen als **zelfstandig documenten** vertegenwoordigd in JSON.</span><span class="sxs-lookup"><span data-stu-id="6d746-116">When you start modeling data in a document store, such as Azure Cosmos DB, try to treat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="6d746-117">Voordat we meteen te veel meer laat het ons Neem een paar stappen terug en bekijk hoe wij iets in een relationele database, een onderwerp dat velen van ons al bekend met bent mogelijk model.</span><span class="sxs-lookup"><span data-stu-id="6d746-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="6d746-118">Het volgende voorbeeld ziet hoe een persoon kan worden opgeslagen in een relationele database.</span><span class="sxs-lookup"><span data-stu-id="6d746-118">The following example shows how a person might be stored in a relational database.</span></span> 

![Relationele database-model](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="6d746-120">Als u werkt met relationele databases, hebben we geleerd jaar normaliseren, normaliseren, normaliseren.</span><span class="sxs-lookup"><span data-stu-id="6d746-120">When working with relational databases, we've been taught for years to normalize, normalize, normalize.</span></span>

<span data-ttu-id="6d746-121">Doorgaans normaliseren van uw gegevens omvat het maken van een entiteit, zoals een persoon, en deze te splitsen op discrete gegevens.</span><span class="sxs-lookup"><span data-stu-id="6d746-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in to discrete pieces of data.</span></span> <span data-ttu-id="6d746-122">In het bovenstaande voorbeeld hebben van een persoon meerdere details van contactpersonen records, alsmede meerdere adresrecords.</span><span class="sxs-lookup"><span data-stu-id="6d746-122">In the example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="6d746-123">We zelfs nog een stapje verder te gaan en contactgegevens onderverdelen per verdere uitpakken algemene velden, zoals een type.</span><span class="sxs-lookup"><span data-stu-id="6d746-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="6d746-124">Hetzelfde adres, heeft elke record hier een type zoals *Start* of *Business*</span><span class="sxs-lookup"><span data-stu-id="6d746-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="6d746-125">Lokale wanneer de normalisatie van gegevens wordt de wegwijs **voorkomen gegevensopslag voor redundante** op elke registreren en in plaats van te verwijzen naar gegevens.</span><span class="sxs-lookup"><span data-stu-id="6d746-125">The guiding premise when normalizing data is to **avoid storing redundant data** on each record and rather refer to data.</span></span> <span data-ttu-id="6d746-126">In dit voorbeeld om te lezen van een persoon, met hun contactgegevens en adressen, moet u JOINS te gebruiken voor het cumuleren van uw gegevens effectief tijdens de uitvoering.</span><span class="sxs-lookup"><span data-stu-id="6d746-126">In this example, to read a person, with all their contact details and addresses, you need to use JOINS to effectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="6d746-127">Bijwerken van één persoon met hun contactgegevens en adressen vereist schrijfbewerkingen over veel afzonderlijke tabellen.</span><span class="sxs-lookup"><span data-stu-id="6d746-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="6d746-128">Nu eens kijken hoe we dezelfde gegevens als een zelfstandig entiteit in de documentdatabase van een zou model.</span><span class="sxs-lookup"><span data-stu-id="6d746-128">Now let's take a look at how we would model the same data as a self-contained entity in a document database.</span></span>

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

<span data-ttu-id="6d746-129">Met de bovenstaande benadering, we nu hebben **gedenormaliseerd** degene vastleggen waar we **ingesloten** alle informatie met betrekking tot deze persoon, zoals hun contactgegevens en -adressen naar een enkele JSON document.</span><span class="sxs-lookup"><span data-stu-id="6d746-129">Using the approach above we have now **denormalized** the person record where we **embedded** all the information relating to this person, such as their contact details and addresses, in to a single JSON document.</span></span>
<span data-ttu-id="6d746-130">Aangezien we niet beperkt naar een vast schema blijven hebben we bovendien de flexibiliteit voor handelingen zoals de contactgegevens van verschillende vormen volledig hebben.</span><span class="sxs-lookup"><span data-stu-id="6d746-130">In addition, because we're not confined to a fixed schema we have the flexibility to do things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="6d746-131">Een persoonsrecord voltooid ophalen uit de database is nu één bewerking met betrekking tot één verzameling en voor één document te lezen.</span><span class="sxs-lookup"><span data-stu-id="6d746-131">Retrieving a complete person record from the database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="6d746-132">Bijwerken van een persoonsrecord met hun contactgegevens en -adressen is ook een schrijfbewerking voor één voor één document.</span><span class="sxs-lookup"><span data-stu-id="6d746-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="6d746-133">Door denormalizing gegevens, moet uw toepassing mogelijk minder query's en updates algemene bewerkingen worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="6d746-133">By denormalizing data, your application may need to issue fewer queries and updates to complete common operations.</span></span> 

### <a name="when-to-embed"></a><span data-ttu-id="6d746-134">Wanneer voor het insluiten van</span><span class="sxs-lookup"><span data-stu-id="6d746-134">When to embed</span></span>
<span data-ttu-id="6d746-135">In het algemeen gebruikt ingesloten gegevens modellen wanneer:</span><span class="sxs-lookup"><span data-stu-id="6d746-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="6d746-136">Er zijn **bevat** relaties tussen entiteiten.</span><span class="sxs-lookup"><span data-stu-id="6d746-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="6d746-137">Er zijn **één aan enkele** relaties tussen entiteiten.</span><span class="sxs-lookup"><span data-stu-id="6d746-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="6d746-138">Er zijn ingesloten gegevens die **niet vaak veranderen**.</span><span class="sxs-lookup"><span data-stu-id="6d746-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="6d746-139">Er is ingesloten gegevens won't groeien **zonder gebonden**.</span><span class="sxs-lookup"><span data-stu-id="6d746-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="6d746-140">Er is ingesloten gegevens **integraal** tot gegevens in een document.</span><span class="sxs-lookup"><span data-stu-id="6d746-140">There is embedded data that is **integral** to data in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="6d746-141">Doorgaans data-modellen beter bieden gedenormaliseerd **lezen** prestaties.</span><span class="sxs-lookup"><span data-stu-id="6d746-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-to-embed"></a><span data-ttu-id="6d746-142">Wanneer u niet in te sluiten</span><span class="sxs-lookup"><span data-stu-id="6d746-142">When not to embed</span></span>
<span data-ttu-id="6d746-143">De databasebestandsgrootte in een documentdatabase is denormalize alles en alle gegevens in één document insluiten, kan dit leiden tot een aantal situaties die moeten worden vermeden.</span><span class="sxs-lookup"><span data-stu-id="6d746-143">While the rule of thumb in a document database is to denormalize everything and embed all data in to a single document, this can lead to some situations that should be avoided.</span></span>

<span data-ttu-id="6d746-144">Deze JSON-fragment in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="6d746-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="6d746-145">Dit is mogelijk wat een post-entiteit met ingesloten opmerkingen eruit zou als we een typische blog of CMS, systeem zijn modelleren.</span><span class="sxs-lookup"><span data-stu-id="6d746-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="6d746-146">Het probleem met dit voorbeeld is dat de matrix opmerkingen **unbounded**, wat betekent dat er geen limiet (praktische) aan het aantal opmerkingen eventuele één post kan hebben.</span><span class="sxs-lookup"><span data-stu-id="6d746-146">The problem with this example is that the comments array is **unbounded**, meaning that there is no (practical) limit to the number of comments any single post can have.</span></span> <span data-ttu-id="6d746-147">Hiermee worden een probleem omdat de grootte van het document kan aanzienlijk toenemen.</span><span class="sxs-lookup"><span data-stu-id="6d746-147">This will become a problem as the size of the document could grow significantly.</span></span>

<span data-ttu-id="6d746-148">Wanneer de grootte van het document de mogelijkheid om te verzenden van de gegevens over de kabel, evenals met het lezen en bijwerken van het document, op schaal, groeit zullen worden beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="6d746-148">As the size of the document grows the ability to transmit the data over the wire as well as reading and updating the document, at scale, will be impacted.</span></span>

<span data-ttu-id="6d746-149">In dit geval zou het beter rekening houden met het volgende model zijn.</span><span class="sxs-lookup"><span data-stu-id="6d746-149">In this case it would be better to consider the following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from the field"},
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

<span data-ttu-id="6d746-150">Dit model heeft de meest recente drie opmerkingen die zijn ingesloten in het bericht, hetgeen een matrix met een vaste ditmaal gebonden.</span><span class="sxs-lookup"><span data-stu-id="6d746-150">This model has the three most recent comments embedded on the post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="6d746-151">De andere opmerkingen zijn gegroepeerd in naar batches van 100 opmerkingen en opgeslagen in afzonderlijke documenten.</span><span class="sxs-lookup"><span data-stu-id="6d746-151">The other comments are grouped in to batches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="6d746-152">De grootte van de batch is gekozen als 100 omdat onze fictieve toepassing kan de gebruiker het laden van 100 opmerkingen tegelijk.</span><span class="sxs-lookup"><span data-stu-id="6d746-152">The size of the batch was chosen as 100 because our fictitious application allows the user to load 100 comments at a time.</span></span>  

<span data-ttu-id="6d746-153">Een andere aanvraag ingesloten gegevens waar niet een goed idee is is wanneer de ingesloten gegevens vaak op documenten gebruikt wordt en vaak worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="6d746-153">Another case where embedding data is not a good idea is when the embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="6d746-154">Deze JSON-fragment in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="6d746-154">Take this JSON snippet.</span></span>

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

<span data-ttu-id="6d746-155">Dit kan leiden tot slot portfolio van een persoon.</span><span class="sxs-lookup"><span data-stu-id="6d746-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="6d746-156">We hebben ervoor gekozen voor het insluiten van de vooraf gedefinieerde informatie in voor elk document portfolio.</span><span class="sxs-lookup"><span data-stu-id="6d746-156">We have chosen to embed the stock information in to each portfolio document.</span></span> <span data-ttu-id="6d746-157">In een omgeving waar gerelateerde gegevens vaak wordt gewijzigd, gaat zoals een stock handel van toepassing, het insluiten van gegevens die regelmatig veranderen betekenen dat u elk document portfolio voortdurend wordt bijgewerkt telkens wanneer een bestand wordt verhandeld.</span><span class="sxs-lookup"><span data-stu-id="6d746-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going to mean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="6d746-158">Stock *zaza* mogen worden verhandeld veel honderden keren in een enkele dag en duizenden gebruikers kunnen hebben *zaza* op hun portfolio.</span><span class="sxs-lookup"><span data-stu-id="6d746-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="6d746-159">Met een gegevensmodel als de bovenstaande we moet bijwerken duizenden portfolio documenten vaak elke dag leidt tot een systeem dat won't schalen uitstekend.</span><span class="sxs-lookup"><span data-stu-id="6d746-159">With a data model like the above we would have to update many thousands of portfolio documents many times every day leading to a system that won't scale very well.</span></span> 

## <span data-ttu-id="6d746-160"><a id="Refer"></a>Verwijst naar gegevens</span><span class="sxs-lookup"><span data-stu-id="6d746-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="6d746-161">Dus mooi gegevens insluiten werkt voor veel gevallen maar duidelijk is dat er scenario's zijn wanneer uw gegevens denormalizing meer problemen dan het verdient aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="6d746-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="6d746-162">Dus wat we doen nu?</span><span class="sxs-lookup"><span data-stu-id="6d746-162">So what do we do now?</span></span> 

<span data-ttu-id="6d746-163">Relationele databases zijn niet de enige plaats waar u de relaties tussen entiteiten kunt maken.</span><span class="sxs-lookup"><span data-stu-id="6d746-163">Relational databases are not the only place where you can create relationships between entities.</span></span> <span data-ttu-id="6d746-164">U kunt de informatie in een document dat daadwerkelijk is gekoppeld aan gegevens in andere documenten hebben in een documentdatabase.</span><span class="sxs-lookup"><span data-stu-id="6d746-164">In a document database you can have information in one document that actually relates to data in other documents.</span></span> <span data-ttu-id="6d746-165">Nu, ik ben niet pleiten zelfs een minuut dat wij systemen die worden beter voor een relationele database in Azure Cosmos DB of een andere documentdatabase geschikt zouden maken, maar eenvoudige relaties geen en kunnen zeer nuttig zijn.</span><span class="sxs-lookup"><span data-stu-id="6d746-165">Now, I am not advocating for even one minute that we build systems that would be better suited to a relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="6d746-166">In de JSON we kiest voor het gebruik van het voorbeeld van een voorraad portfolio van eerder, maar deze tijd is de voorraad item in de portfolio in plaats van te sluiten.</span><span class="sxs-lookup"><span data-stu-id="6d746-166">In the JSON below we chose to use the example of a stock portfolio from earlier but this time we refer to the stock item on the portfolio instead of embedding it.</span></span> <span data-ttu-id="6d746-167">Wanneer het slot item vaak wijzigen gedurende de dag het enige document dat moet worden bijgewerkt, is enkele voorraad document.</span><span class="sxs-lookup"><span data-stu-id="6d746-167">This way, when the stock item changes frequently throughout the day the only document that needs to be updated is the single stock document.</span></span> 

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


<span data-ttu-id="6d746-168">Een onmiddellijke nadeel voor deze benadering is echter als uw toepassing vereist om aan te tonen informatie over elke voorraad die wordt veroorzaakt is bij het weergeven van een persoon portfolio; in dit geval moet u meerdere reizen aanbrengen in de database laden van de gegevens voor elk document voorraad.</span><span class="sxs-lookup"><span data-stu-id="6d746-168">An immediate downside to this approach though is if your application is required to show information about each stock that is held when displaying a person's portfolio; in this case you would need to make multiple trips to the database to load the information for each stock document.</span></span> <span data-ttu-id="6d746-169">Hier hebt wordt een beslissing voor het verbeteren van de efficiëntie van schrijfbewerkingen die vaak gedurende de dag gebeuren, maar op zijn beurt inbreuk op de leesbewerkingen die mogelijk minder invloed op de prestaties van dit bepaalde systeem hebben genomen.</span><span class="sxs-lookup"><span data-stu-id="6d746-169">Here we've made a decision to improve the efficiency of write operations, which happen frequently throughout the day, but in turn compromised on the read operations that potentially have less impact on the performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="6d746-170">Genormaliseerd gegevensmodellen **kunt vereisen meer retouren** naar de server.</span><span class="sxs-lookup"><span data-stu-id="6d746-170">Normalized data models **can require more round trips** to the server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="6d746-171">Hoe zit het met refererende sleutels?</span><span class="sxs-lookup"><span data-stu-id="6d746-171">What about foreign keys?</span></span>
<span data-ttu-id="6d746-172">Omdat er momenteel geen concept van een beperking, refererende sleutel of anderszins, de relaties tussen document die u in documenten hebt zijn effectief 'zwakke koppelingen' en kunnen niet worden gecontroleerd door de database zelf.</span><span class="sxs-lookup"><span data-stu-id="6d746-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by the database itself.</span></span> <span data-ttu-id="6d746-173">Als u zorgen dat de gegevens die een document verwijst wilt naar het daadwerkelijk bestaat, moet u dit doen in uw toepassing of door het gebruik van serverzijde triggers of opgeslagen procedures op Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6d746-173">If you want to ensure that the data a document is referring to actually exists, then you need to do this in your application, or through the use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-to-reference"></a><span data-ttu-id="6d746-174">Wanneer u om te verwijzen naar</span><span class="sxs-lookup"><span data-stu-id="6d746-174">When to reference</span></span>
<span data-ttu-id="6d746-175">In het algemeen gebruikt genormaliseerde gegevens modellen wanneer:</span><span class="sxs-lookup"><span data-stu-id="6d746-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="6d746-176">Voor **een-op-veel** relaties.</span><span class="sxs-lookup"><span data-stu-id="6d746-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="6d746-177">Voor **veel-op-veel** relaties.</span><span class="sxs-lookup"><span data-stu-id="6d746-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="6d746-178">Gerelateerde gegevens **regelmatig wordt gewijzigd**.</span><span class="sxs-lookup"><span data-stu-id="6d746-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="6d746-179">Gegevens waarnaar wordt verwezen, kan worden **unbounded**.</span><span class="sxs-lookup"><span data-stu-id="6d746-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="6d746-180">Doorgaans normaliseren biedt betere **schrijven** prestaties.</span><span class="sxs-lookup"><span data-stu-id="6d746-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-the-relationship"></a><span data-ttu-id="6d746-181">Waar ik de relatie plaatsen?</span><span class="sxs-lookup"><span data-stu-id="6d746-181">Where do I put the relationship?</span></span>
<span data-ttu-id="6d746-182">De groei van de relatie kunt u bepalen in welke document voor het opslaan van de referentie.</span><span class="sxs-lookup"><span data-stu-id="6d746-182">The growth of the relationship will help determine in which document to store the reference.</span></span>

<span data-ttu-id="6d746-183">Als we de onderstaande JSON modellen uitgevers en rapporten bekijken.</span><span class="sxs-lookup"><span data-stu-id="6d746-183">If we look at the JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over the world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in to Azure Cosmos DB" }

<span data-ttu-id="6d746-184">Als het nummer van de boeken per uitgever met beperkte groei klein is, kan klikt u vervolgens de adresboek naslaginformatie voor de publisher-document opslaan nuttig zijn.</span><span class="sxs-lookup"><span data-stu-id="6d746-184">If the number of the books per publisher is small with limited growth, then storing the book reference inside the publisher document may be useful.</span></span> <span data-ttu-id="6d746-185">Echter als het aantal boeken per uitgever unbounded is, zou klikt u vervolgens deze gegevensmodel leiden tot veranderlijke, groeiende matrices, zoals in het bovenstaande voorbeeld publisher document.</span><span class="sxs-lookup"><span data-stu-id="6d746-185">However, if the number of books per publisher is unbounded, then this data model would lead to mutable, growing arrays, as in the example publisher document above.</span></span> 

<span data-ttu-id="6d746-186">Overschakelen van dingen rond een bits zou leiden tot een model die nog steeds vertegenwoordigt dezelfde gegevens, maar deze grote veranderlijke verzamelingen nu voorkomt.</span><span class="sxs-lookup"><span data-stu-id="6d746-186">Switching things around a bit would result in a model that still represents the same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over the world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in to Azure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="6d746-187">In het bovenstaande voorbeeld hebben we de unbounded verzameling verwijderd op de publisher-document.</span><span class="sxs-lookup"><span data-stu-id="6d746-187">In the above example, we have dropped the unbounded collection on the publisher document.</span></span> <span data-ttu-id="6d746-188">In plaats daarvan we zojuist hebben een verwijzing naar de uitgever op elk document adresboek.</span><span class="sxs-lookup"><span data-stu-id="6d746-188">Instead we just have a a reference to the publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="6d746-189">Hoe ik veel: veel-relaties model?</span><span class="sxs-lookup"><span data-stu-id="6d746-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="6d746-190">In een relationele database *veel:* relaties zijn vaak gemodelleerd met join-tabellen die records uit andere tabellen NET samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="6d746-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Tabellen samenvoegen](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="6d746-192">U kunt mogelijk geneigd te repliceren van hetzelfde met behulp van documenten en produceren van een gegevensmodel dat op het volgende lijkt.</span><span class="sxs-lookup"><span data-stu-id="6d746-192">You might be tempted to replicate the same thing using documents and produce a data model that looks similar to the following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over the world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in to Azure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="6d746-193">Dit zou werken.</span><span class="sxs-lookup"><span data-stu-id="6d746-193">This would work.</span></span> <span data-ttu-id="6d746-194">Echter, ofwel een auteur met hun books laden of het laden van een rapport met de auteur zou moet altijd ten minste twee extra query's op de database.</span><span class="sxs-lookup"><span data-stu-id="6d746-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against the database.</span></span> <span data-ttu-id="6d746-195">Een query voor het gekoppelde document en vervolgens een andere query voor het ophalen van het document wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6d746-195">One query to the joining document and then another query to fetch the actual document being joined.</span></span> 

<span data-ttu-id="6d746-196">Als deze tabel join wordt alleen is lijmen samen twee soorten gegevens waarom niet vermeld het dan niet volledig?</span><span class="sxs-lookup"><span data-stu-id="6d746-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="6d746-197">Overweeg het volgende.</span><span class="sxs-lookup"><span data-stu-id="6d746-197">Consider the following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in to Azure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="6d746-198">Nu als ik had een auteur, ik onmiddellijk weet welke boeken deze geschreven en als u daarentegen als ik een boekdocument geladen had ik weet de id's van de auteur (s).</span><span class="sxs-lookup"><span data-stu-id="6d746-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know the ids of the author(s).</span></span> <span data-ttu-id="6d746-199">Dit bespaart die tussenliggende-query op het verminderen van join tabel het nummer van server-retouren uw toepassing heeft om te nemen.</span><span class="sxs-lookup"><span data-stu-id="6d746-199">This saves that intermediary query against the join table reducing the number of server round trips your application has to make.</span></span> 

## <span data-ttu-id="6d746-200"><a id="WrapUp"></a>Hybride gegevensmodellen</span><span class="sxs-lookup"><span data-stu-id="6d746-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="6d746-201">We nu hebt bekeken insluiten (of denormalizing) en gegevens van verwijzende (of normaliseren), hebben elk hun upsides en elk compromissen hebben, zoals we hebben gezien.</span><span class="sxs-lookup"><span data-stu-id="6d746-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="6d746-202">Heeft geen altijd te zijn of niet worden Blazende naar dingen enigszins van elkaar.</span><span class="sxs-lookup"><span data-stu-id="6d746-202">It doesn't always have to be either or, don't be scared to mix things up a little.</span></span> 

<span data-ttu-id="6d746-203">Op basis van de specifieke gebruikspatronen en werkbelastingen die mogelijk zijn er gevallen waarbij de combinatie van ingesloten van uw toepassing en gegevens waarnaar wordt verwezen is wel zinvol en kan leiden tot eenvoudiger toepassingslogica met minder server retouren tegelijkertijd nog steeds een goede niveau van de prestaties.</span><span class="sxs-lookup"><span data-stu-id="6d746-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead to simpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="6d746-204">Houd rekening met de volgende JSON.</span><span class="sxs-lookup"><span data-stu-id="6d746-204">Consider the following JSON.</span></span> 

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

<span data-ttu-id="6d746-205">Hier hebt we het ingesloten model, waarbij gegevens uit andere entiteiten zijn ingesloten in het document op het hoogste niveau, maar andere gegevens wordt verwezen (voornamelijk) gevolgd.</span><span class="sxs-lookup"><span data-stu-id="6d746-205">Here we've (mostly) followed the embedded model, where data from other entities are embedded in the top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="6d746-206">Als u het document adresboek bekijkt, ziet u enkele interessante velden bij de matrix van auteurs.</span><span class="sxs-lookup"><span data-stu-id="6d746-206">If you look at the book document, we can see a few interesting fields when we look at the array of authors.</span></span> <span data-ttu-id="6d746-207">Er is een *id* veld dit is het veld we gebruiken terug te verwijzen naar een auteur-document standaardprocedure in een genormaliseerde model, maar vervolgens we hebben ook *naam* en *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="6d746-207">There is an *id* field which is the field we use to refer back to an author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="6d746-208">Kan we zojuist hebt vastgelopen met *id* en links van de toepassing eventuele aanvullende informatie nodig ophalen uit het respectieve auteur-document met behulp van de 'koppeling', maar omdat onze toepassing de naam van de auteur en een miniatuur geeft met elke adresboek weergegeven kunnen we een round trip opslaan op de server per rapport in een lijst door denormalizing **sommige** gegevens van de auteur.</span><span class="sxs-lookup"><span data-stu-id="6d746-208">We could've just stuck with *id* and left the application to get any additional information it needed from the respective author document using the "link", but because our application displays the author's name and a thumbnail picture with every book displayed we can save a round trip to the server per book in a list by denormalizing **some** data from the author.</span></span>

<span data-ttu-id="6d746-209">Ervoor dat, als de naam van de auteur gewijzigd of dat ze hun photo die zou moeten we een update gaat bijwerken wilden elk rapport ze ooit gepubliceerd maar voor onze toepassing, op basis van de veronderstelling dat auteurs niet hun namen vaak veranderen, is dit een acceptabele ontwerpbeslissing.</span><span class="sxs-lookup"><span data-stu-id="6d746-209">Sure, if the author's name changed or they wanted to update their photo we'd have to go an update every book they ever published but for our application, based on the assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="6d746-210">In het voorbeeld zijn er **vooraf berekende aggregaties** waarden op te slaan dure verwerking op een leesbewerking.</span><span class="sxs-lookup"><span data-stu-id="6d746-210">In the example there are **pre-calculated aggregates** values to save expensive processing on a read operation.</span></span> <span data-ttu-id="6d746-211">In het voorbeeld is enkele van de gegevens die zijn ingesloten in het document de auteur van gegevens die tijdens de uitvoering wordt berekend.</span><span class="sxs-lookup"><span data-stu-id="6d746-211">In the example, some of the data embedded in the author document is data that is calculated at run-time.</span></span> <span data-ttu-id="6d746-212">Telkens wanneer een nieuw rapport is gepubliceerd, wordt een boekdocument gemaakt **en** countOfBooks veld is ingesteld voor een berekende waarde op basis van het aantal documenten adresboek die beschikbaar zijn voor een bepaalde auteur.</span><span class="sxs-lookup"><span data-stu-id="6d746-212">Every time a new book is published, a book document is created **and** the countOfBooks field is set to a calculated value based on the number of book documents that exist for a particular author.</span></span> <span data-ttu-id="6d746-213">Deze optimalisatie zou zijn goede in lezen zware systemen waar we doen van berekeningen bij het schrijven om te optimaliseren leesbewerkingen toestaan.</span><span class="sxs-lookup"><span data-stu-id="6d746-213">This optimization would be good in read heavy systems where we can afford to do computations on writes in order to optimize reads.</span></span>

<span data-ttu-id="6d746-214">De mogelijkheid om een model met vooraf berekende velden wordt mogelijk gemaakt omdat Azure Cosmos DB ondersteunt **transacties met meerdere documenten**.</span><span class="sxs-lookup"><span data-stu-id="6d746-214">The ability to have a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="6d746-215">Veel NoSQL-opslag kunnen doen transacties meerdere documenten en daarom pleiten ontwerpbeslissingen, zoals 'altijd insluiten alles', vanwege deze beperking.</span><span class="sxs-lookup"><span data-stu-id="6d746-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due to this limitation.</span></span> <span data-ttu-id="6d746-216">U kunt met Azure Cosmos DB serverzijde triggers of opgeslagen procedures, die books invoegen en auteurs allemaal binnen een ACID-transactie bijwerken gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6d746-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="6d746-217">Nu u geen **hebben** voor het insluiten van alles in één document net om ervoor te zorgen dat de gegevens consistent blijft.</span><span class="sxs-lookup"><span data-stu-id="6d746-217">Now you don't **have** to embed everything in to one document just to be sure that your data remains consistent.</span></span>

## <span data-ttu-id="6d746-218"><a name="NextSteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d746-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="6d746-219">De grootste takeaways uit dit artikel is om te begrijpen dat modelleren in een wereld schemavrije gegevens even belangrijk is als ooit.</span><span class="sxs-lookup"><span data-stu-id="6d746-219">The biggest takeaways from this article is to understand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="6d746-220">Net als er geen enkele manier een stukje informatie op een scherm vertegenwoordigt is, is er geen eenduidige manier om uw gegevens te modelleren.</span><span class="sxs-lookup"><span data-stu-id="6d746-220">Just as there is no single way to represent a piece of data on a screen, there is no single way to model your data.</span></span> <span data-ttu-id="6d746-221">U moet uw toepassing en hoe deze wordt produceert, gebruiken en de gegevens verwerken.</span><span class="sxs-lookup"><span data-stu-id="6d746-221">You need to understand your application and how it will produce, consume, and process the data.</span></span> <span data-ttu-id="6d746-222">Vervolgens kunt u door het toepassen van enkele van de richtlijnen die hier wordt gepresenteerd ook instellen over het maken van een model die zijn gericht op de onmiddellijke behoeften van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="6d746-222">Then, by applying some of the guidelines presented here you can set about creating a model that addresses the immediate needs of your application.</span></span> <span data-ttu-id="6d746-223">Als uw toepassingen wijzigen wilt, kunt u gebruikmaken van de flexibiliteit van een schema gratis database over te gaan die wijzigen en het gegevensmodel van uw eenvoudig ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="6d746-223">When your applications need to change, you can leverage the flexibility of a schema-free database to embrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="6d746-224">Raadpleeg voor meer informatie over Azure Cosmos DB, van de service [documentatie](https://azure.microsoft.com/documentation/services/cosmos-db/) pagina.</span><span class="sxs-lookup"><span data-stu-id="6d746-224">To learn more about Azure Cosmos DB, refer to the service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="6d746-225">Om te begrijpen hoe naar shard van uw gegevens over meerdere partities verwijzen naar [partitioneren van gegevens in Azure Cosmos DB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="6d746-225">To understand how to shard your data across multiple partitions, refer to [Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
