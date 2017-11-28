---
title: aaaMulti hoofddatabase architecturen met Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe toodesign toepassingsarchitecturen met lokale leest en schrijft over meerdere geografische regio's met Azure Cosmos DB.
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 706ced74-ea67-45dd-a7de-666c3c893687
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3269c8405afe16f75db69b42e576fe76e00a8e16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="43d6c-103">Meerdere master gerepliceerd globaal database architecturen met Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="43d6c-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="43d6c-104">Azure Cosmos DB ondersteunt klare [globale replicatie](distribute-data-globally.md), waarmee u toodistribute gegevensgebieden toomultiple met lage latentie toegang overal in Hallo werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="43d6c-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you toodistribute data toomultiple regions with low latency access anywhere in hello workload.</span></span> <span data-ttu-id="43d6c-105">Dit model wordt meestal gebruikt voor publisher/consumer werkbelastingen wanneer er een schrijver in één geografische regio en globaal gedistribueerde lezers in andere regio (lezen).</span><span class="sxs-lookup"><span data-stu-id="43d6c-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="43d6c-106">U kunt ook Azure Cosmos DB globale replicatie ondersteuning toobuild toepassingen waarin schrijvers en lezers worden globaal gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="43d6c-106">You can also use Azure Cosmos DB's global replication support toobuild applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="43d6c-107">Dit document bevat een patroon waarmee lokale schrijf- en lokale leestoegang voor gedistribueerde schrijvers met behulp van Azure DB die Cosmos bereiken.</span><span class="sxs-lookup"><span data-stu-id="43d6c-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="43d6c-108"><a id="ExampleScenario"></a>Publicatie - een voorbeeldscenario</span><span class="sxs-lookup"><span data-stu-id="43d6c-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="43d6c-109">Bekijk een werkelijk scenario toodescribe hoe u globaal gedistribueerde meerdere-region/meerdere-pre-master lezen schrijven patronen kunt gebruiken met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="43d6c-109">Let's look at a real world scenario toodescribe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="43d6c-110">U kunt een content publishing platform gebouwd op Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="43d6c-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="43d6c-111">Hier volgen enkele vereisten waaraan dit platform voor consumenten en uitgevers voor een goede gebruikerservaring moet voldoen.</span><span class="sxs-lookup"><span data-stu-id="43d6c-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="43d6c-112">Zowel auteurs en abonnees verdeeld over Hallo wereld</span><span class="sxs-lookup"><span data-stu-id="43d6c-112">Both authors and subscribers are spread over hello world</span></span> 
* <span data-ttu-id="43d6c-113">Auteurs moeten (schrijven) artikelen tootheir lokale (dichtst) regio publiceren</span><span class="sxs-lookup"><span data-stu-id="43d6c-113">Authors must publish (write) articles tootheir local (closest) region</span></span>
* <span data-ttu-id="43d6c-114">Auteurs hebben lezers/abonnees van hun artikelen die zijn verdeeld over de hele wereld Hallo.</span><span class="sxs-lookup"><span data-stu-id="43d6c-114">Authors have readers/subscribers of their articles who are distributed across hello globe.</span></span> 
* <span data-ttu-id="43d6c-115">Abonnees moeten een melding krijgen wanneer nieuwe artikelen worden gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="43d6c-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="43d6c-116">Abonnees moet kunnen tooread artikelen van hun lokale regio.</span><span class="sxs-lookup"><span data-stu-id="43d6c-116">Subscribers must be able tooread articles from their local region.</span></span> <span data-ttu-id="43d6c-117">Ze moeten ook worden kunnen tooadd beoordelingen toothese artikelen.</span><span class="sxs-lookup"><span data-stu-id="43d6c-117">They should also be able tooadd reviews toothese articles.</span></span> 
* <span data-ttu-id="43d6c-118">Iedereen inclusief Hallo auteur Hallo artikelen moet kunnen weergeven, dat alle gekoppelde tooarticles beoordelingen van een lokale regio Hallo.</span><span class="sxs-lookup"><span data-stu-id="43d6c-118">Anyone including hello author of hello articles should be able view all hello reviews attached tooarticles from a local region.</span></span> 

<span data-ttu-id="43d6c-119">Ervan uitgaande dat miljoenen consumenten en uitgevers miljarden artikelen, snel hebben we tooconfront Hallo problemen van de schaal samen met plaats van toegang te garanderen.</span><span class="sxs-lookup"><span data-stu-id="43d6c-119">Assuming millions of consumers and publishers with billions of articles, soon we have tooconfront hello problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="43d6c-120">Net als bij de meeste schaalbaarheidsproblemen, ligt Hallo oplossing in de strategie voor een goede partitionering.</span><span class="sxs-lookup"><span data-stu-id="43d6c-120">As with most scalability problems, hello solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="43d6c-121">Vervolgens laten we kijken hoe toomodel artikelen, controleren en meldingen als documenten, Azure DB die Cosmos-accounts configureren en implementeren van een gegevenstoegangslaag.</span><span class="sxs-lookup"><span data-stu-id="43d6c-121">Next, let's look at how toomodel articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="43d6c-122">Als u meer informatie over partitioneren en partitiesleutels toolearn, Zie [partitionerings- en schalen in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="43d6c-122">If you would like toolearn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="43d6c-123"><a id="ModelingNotifications"></a>Modellering meldingen</span><span class="sxs-lookup"><span data-stu-id="43d6c-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="43d6c-124">Meldingen zijn gegevens feeds tooa specifieke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="43d6c-124">Notifications are data feeds specific tooa user.</span></span> <span data-ttu-id="43d6c-125">Hallo toegangspatronen voor meldingen documenten zijn daarom altijd in de context Hallo van één gebruiker.</span><span class="sxs-lookup"><span data-stu-id="43d6c-125">Therefore, hello access patterns for notifications documents are always in hello context of single user.</span></span> <span data-ttu-id="43d6c-126">U zou bijvoorbeeld 'posten een tooa meldingsgebruiker' of 'alle meldingen voor een bepaalde gebruiker ophalen'.</span><span class="sxs-lookup"><span data-stu-id="43d6c-126">For example, you would "post a notification tooa user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="43d6c-127">Beste keuze van de partitiesleutel voor dit type zou worden dus Hallo `UserId`.</span><span class="sxs-lookup"><span data-stu-id="43d6c-127">So, hello optimal choice of partitioning key for this type would be `UserId`.</span></span>

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // hello user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // hello partition Key for hello resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of hello notification. 
        public string ArticleId { get; set; } 
    }

## <span data-ttu-id="43d6c-128"><a id="ModelingSubscriptions"></a>Modellering abonnementen</span><span class="sxs-lookup"><span data-stu-id="43d6c-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="43d6c-129">Abonnementen kunnen worden gemaakt voor de verschillende criteria zoals een specifieke categorie artikelen interessegebied of een bepaalde uitgever.</span><span class="sxs-lookup"><span data-stu-id="43d6c-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="43d6c-130">Daarom Hallo `SubscriptionFilter` een goede keuze voor de partitiesleutel is.</span><span class="sxs-lookup"><span data-stu-id="43d6c-130">Hence hello `SubscriptionFilter` is a good choice for partition key.</span></span>

    class Subscriptions 
    { 
        // Unique ID for Subscription 
        public string Id { get; set; }

        // Subscription source. Could be Author | Category etc. 
        public string SubscriptionFilter { get; set; }

        // subscribing User. 
        public string UserId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.SubscriptionFilter; 
            } 
        } 
    }

## <span data-ttu-id="43d6c-131"><a id="ModelingArticles"></a>Vormgeven aan artikelen</span><span class="sxs-lookup"><span data-stu-id="43d6c-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="43d6c-132">Zodra een artikel wordt geïdentificeerd door meldingen, de volgende query's doorgaans zijn gebaseerd op Hallo `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="43d6c-132">Once an article is identified through notifications, subsequent queries are typically based on hello `Article.Id`.</span></span> <span data-ttu-id="43d6c-133">Kiezen `Article.Id` als partitie biedt Hallo sleutel dus Hallo best distributiepunten voor het opslaan van de artikelen in een verzameling Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="43d6c-133">Choosing `Article.Id` as partition hello key thus provides hello best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

    class Article 
    { 
        // Unique ID for Article 
        public string Id { get; set; }
        
        public string PartitionKey 
        { 
            get 
            { 
                return this.Id; 
            } 
        }
        
        // Author of hello article
        public string Author { get; set; }

        // Category/genre of hello article
        public string Category { get; set; }

        // Tags associated with hello article
        public string[] Tags { get; set; }

        // Title of hello article
        public string Title { get; set; }
        
        //... 
    }

## <span data-ttu-id="43d6c-134"><a id="ModelingReviews"></a>Modellering beoordelingen</span><span class="sxs-lookup"><span data-stu-id="43d6c-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="43d6c-135">Beoordelingen zijn voornamelijk zoals artikelen, geschreven en gelezen in Hallo context van het artikel.</span><span class="sxs-lookup"><span data-stu-id="43d6c-135">Like articles, reviews are mostly written and read in hello context of article.</span></span> <span data-ttu-id="43d6c-136">Kiezen `ArticleId` een partitie sleutel biedt aanbevolen distributie en efficiënte toegang van revisies die zijn gekoppeld aan het artikel.</span><span class="sxs-lookup"><span data-stu-id="43d6c-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of hello review 
        public string ArticleId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.ArticleId; 
            } 
        }
        
        //Reviewer Id 
        public string UserId { get; set; }
        public string ReviewText { get; set; }
        
        public int Rating { get; set; } }
    }

## <span data-ttu-id="43d6c-137"><a id="DataAccessMethods"></a>Methoden voor gegevenstoegang laag</span><span class="sxs-lookup"><span data-stu-id="43d6c-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="43d6c-138">Nu we kijken naar de belangrijkste gegevens Hallo toegangsmethoden moeten we tooimplement.</span><span class="sxs-lookup"><span data-stu-id="43d6c-138">Now let's look at hello main data access methods we need tooimplement.</span></span> <span data-ttu-id="43d6c-139">Hier volgt de lijst Hallo van methoden die Hallo `ContentPublishDatabase` moet:</span><span class="sxs-lookup"><span data-stu-id="43d6c-139">Here's hello list of methods that hello `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="43d6c-140"><a id="Architecture"></a>Configuratie van Azure DB Cosmos-account</span><span class="sxs-lookup"><span data-stu-id="43d6c-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="43d6c-141">lokale tooguarantee leest en schrijft, we gegevens niet alleen op partitiesleutel moet partitioneren, maar ook op basis van de geografische toegangspatroon Hallo in regio's.</span><span class="sxs-lookup"><span data-stu-id="43d6c-141">tooguarantee local reads and writes, we must partition data not just on partition key, but also based on hello geographical access pattern into regions.</span></span> <span data-ttu-id="43d6c-142">Hallo model afhankelijk is van een account Azure Cosmos DB database geo-replicatie voor elke regio.</span><span class="sxs-lookup"><span data-stu-id="43d6c-142">hello model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="43d6c-143">Bijvoorbeeld, met twee gebieden is hier een instelling voor schrijfacties voor meerdere landen/regio:</span><span class="sxs-lookup"><span data-stu-id="43d6c-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="43d6c-144">Accountnaam</span><span class="sxs-lookup"><span data-stu-id="43d6c-144">Account Name</span></span> | <span data-ttu-id="43d6c-145">Regio schrijven</span><span class="sxs-lookup"><span data-stu-id="43d6c-145">Write Region</span></span> | <span data-ttu-id="43d6c-146">Lees de regio</span><span class="sxs-lookup"><span data-stu-id="43d6c-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="43d6c-147">Hallo volgende diagram ziet u hoe lees- en schrijfbewerkingen worden uitgevoerd in een typische toepassing met deze instellingen:</span><span class="sxs-lookup"><span data-stu-id="43d6c-147">hello following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Azure meerdere masters Cosmos-DB-architectuur](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="43d6c-149">Hier volgt een codefragment met hoe tooinitialize clients in een DAL uitgevoerd in de Hallo Hallo `West US` regio.</span><span class="sxs-lookup"><span data-stu-id="43d6c-149">Here is a code snippet showing how tooinitialize hello clients in a DAL running in hello `West US` region.</span></span>
    
    ConnectionPolicy writeClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    writeClientPolicy.PreferredLocations.Add(LocationNames.WestUS);
    writeClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

    DocumentClient writeClient = new DocumentClient(
        new Uri("https://contentpubdatabase-usa.documents.azure.com"), 
        writeRegionAuthKey,
        writeClientPolicy);

    ConnectionPolicy readClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    readClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);
    readClientPolicy.PreferredLocations.Add(LocationNames.WestUS);

    DocumentClient readClient = new DocumentClient(
        new Uri("https://contentpubdatabase-europe.documents.azure.com"),
        readRegionAuthKey,
        readClientPolicy);

<span data-ttu-id="43d6c-150">Met de Hallo voorafgaand aan installatie, kan Hallo gegevenstoegangslaag doorsturen alle schrijfbewerkingen toohello lokale account op basis van waarop deze wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="43d6c-150">With hello preceding setup, hello data access layer can forward all writes toohello local account based on where it is deployed.</span></span> <span data-ttu-id="43d6c-151">Leesbewerkingen worden uitgevoerd door bij het lezen van beide accounts tooget Hallo globale weergave van gegevens.</span><span class="sxs-lookup"><span data-stu-id="43d6c-151">Reads are performed by reading from both accounts tooget hello global view of data.</span></span> <span data-ttu-id="43d6c-152">Deze methode kan worden uitgebreid tooas veel regio's waar nodig.</span><span class="sxs-lookup"><span data-stu-id="43d6c-152">This approach can be extended tooas many regions as required.</span></span> <span data-ttu-id="43d6c-153">Dit is bijvoorbeeld een installatie met drie geografische regio's:</span><span class="sxs-lookup"><span data-stu-id="43d6c-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="43d6c-154">Accountnaam</span><span class="sxs-lookup"><span data-stu-id="43d6c-154">Account Name</span></span> | <span data-ttu-id="43d6c-155">Regio schrijven</span><span class="sxs-lookup"><span data-stu-id="43d6c-155">Write Region</span></span> | <span data-ttu-id="43d6c-156">Regio 1 lezen</span><span class="sxs-lookup"><span data-stu-id="43d6c-156">Read Region 1</span></span> | <span data-ttu-id="43d6c-157">Regio 2 lezen</span><span class="sxs-lookup"><span data-stu-id="43d6c-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="43d6c-158"><a id="DataAccessImplementation"></a>Data access-laag implementatie</span><span class="sxs-lookup"><span data-stu-id="43d6c-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="43d6c-159">Nu we bekijken Hallo-implementatie van Hallo gegevenstoegangslaag (DAL) voor een toepassing met twee beschrijfbare regio's.</span><span class="sxs-lookup"><span data-stu-id="43d6c-159">Now let's look at hello implementation of hello data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="43d6c-160">Hallo DAL moet implementeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="43d6c-160">hello DAL must implement hello following steps:</span></span>

* <span data-ttu-id="43d6c-161">Maken van meerdere exemplaren van `DocumentClient` voor elke account.</span><span class="sxs-lookup"><span data-stu-id="43d6c-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="43d6c-162">Met twee regio's, elk DAL-exemplaar heeft een `writeClient` en één `readClient`.</span><span class="sxs-lookup"><span data-stu-id="43d6c-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="43d6c-163">Hallo-eindpunten voor op basis van regio van de toepassing hello Hallo geïmplementeerd, configureert `writeclient` en `readClient`.</span><span class="sxs-lookup"><span data-stu-id="43d6c-163">Based on hello deployed region of hello application, configure hello endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="43d6c-164">Bijvoorbeeld Hallo DAL geïmplementeerd `West US` gebruikt `contentpubdatabase-usa.documents.azure.com` voor het uitvoeren van schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="43d6c-164">For example, hello DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="43d6c-165">Hallo DAL geïmplementeerd in `NorthEurope` gebruikt `contentpubdatabase-europ.documents.azure.com` voor schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="43d6c-165">hello DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="43d6c-166">Met de Hallo voorafgaand aan installatie, kunnen toegangsmethoden Hallo-gegevens worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="43d6c-166">With hello preceding setup, hello data access methods can be implemented.</span></span> <span data-ttu-id="43d6c-167">Schrijven operations doorsturen Hallo schrijven toohello overeenkomt `writeClient`.</span><span class="sxs-lookup"><span data-stu-id="43d6c-167">Write operations forward hello write toohello corresponding `writeClient`.</span></span>

    public async Task CreateSubscriptionAsync(string userId, string category)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Subscriptions
        {
            UserId = userId,
            SubscriptionFilter = category
        });
    }

    public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Review
        {
            UserId = userId,
            ArticleId = articleId,
            ReviewText = reviewText,
            Rating = rating
        });
    }

<span data-ttu-id="43d6c-168">Voor het lezen van meldingen en beoordelingen, kunt u moet lezen van zowel de regio's en de resultaten union Hallo zoals weergegeven in het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="43d6c-168">For reading notifications and reviews, you must read from both regions and union hello results as shown in hello following snippet:</span></span>

    public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId)
    {
        IDocumentQuery<Notification> writeAccountNotification = (
            from notification in this.writeClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();
        
        IDocumentQuery<Notification> readAccountNotification = (
            from notification in this.readClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();

        List<Notification> notifications = new List<Notification>();

        while (writeAccountNotification.HasMoreResults || readAccountNotification.HasMoreResults)
        {
            IList<Task<FeedResponse<Notification>>> results = new List<Task<FeedResponse<Notification>>>();

            if (writeAccountNotification.HasMoreResults)
            {
                results.Add(writeAccountNotification.ExecuteNextAsync<Notification>());
            }

            if (readAccountNotification.HasMoreResults)
            {
                results.Add(readAccountNotification.ExecuteNextAsync<Notification>());
            }

            IList<FeedResponse<Notification>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Notification> feed in notificationFeedResult)
            {
                notifications.AddRange(feed);
            }
        }
        return notifications;
    }

    public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId)
    {
        IDocumentQuery<Review> writeAccountReviews = (
            from review in this.writeClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();
        
        IDocumentQuery<Review> readAccountReviews = (
            from review in this.readClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();

        List<Review> reviews = new List<Review>();
        
        while (writeAccountReviews.HasMoreResults || readAccountReviews.HasMoreResults)
        {
            IList<Task<FeedResponse<Review>>> results = new List<Task<FeedResponse<Review>>>();

            if (writeAccountReviews.HasMoreResults)
            {
                results.Add(writeAccountReviews.ExecuteNextAsync<Review>());
            }

            if (readAccountReviews.HasMoreResults)
            {
                results.Add(readAccountReviews.ExecuteNextAsync<Review>());
            }

            IList<FeedResponse<Review>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Review> feed in notificationFeedResult)
            {
                reviews.AddRange(feed);
            }
        }

        return reviews;
    }

<span data-ttu-id="43d6c-169">Dus als u een goede te nemen partitionerende sleutel en statische op basis van een account partitioneren, kunt u bereiken met meerdere regio lokale geschreven en gelezen met behulp van Azure DB die Cosmos.</span><span class="sxs-lookup"><span data-stu-id="43d6c-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="43d6c-170"><a id="NextSteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="43d6c-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="43d6c-171">In dit artikel wordt beschreven hoe u globaal gedistribueerde meerdere landen/regio lezen-schrijven patronen kunt gebruiken met Azure Cosmos DB met inhoud publiceren als een voorbeeldscenario.</span><span class="sxs-lookup"><span data-stu-id="43d6c-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="43d6c-172">Meer informatie over hoe Azure Cosmos DB ondersteunt [globale distributie](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="43d6c-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="43d6c-173">Meer informatie over [automatische en handmatige failover in Azure Cosmos-DB](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="43d6c-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="43d6c-174">Meer informatie over [globale consistentie met Azure Cosmos-DB](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="43d6c-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="43d6c-175">Ontwikkelen met meerdere regio's met behulp van Hallo [Azure DB Cosmos - DocumentDB-API](tutorial-global-distribution-documentdb.md)</span><span class="sxs-lookup"><span data-stu-id="43d6c-175">Develop with multiple regions using hello [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="43d6c-176">Ontwikkelen met meerdere regio's met behulp van Hallo [Azure DB Cosmos - MongoDB-API](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="43d6c-176">Develop with multiple regions using hello [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="43d6c-177">Ontwikkelen met meerdere regio's met behulp van Hallo [Azure DB Cosmos - tabel-API](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="43d6c-177">Develop with multiple regions using hello [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>
