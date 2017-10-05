---
title: Meerdere hoofddatabase architecturen met Azure Cosmos DB | Microsoft Docs
description: Meer informatie over het ontwerpen van toepassingsarchitecturen met lokale lees- en schrijfbewerkingen over meerdere geografische regio's met Azure Cosmos DB.
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
ms.openlocfilehash: cf1482ae7b1070023703f5dbe861d151f5d64fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="1d60a-103">Meerdere master gerepliceerd globaal database architecturen met Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="1d60a-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="1d60a-104">Azure Cosmos DB ondersteunt klare [globale replicatie](distribute-data-globally.md), waarmee u gegevens naar meerdere regio's met lage latentie toegang overal in de werklast verdelen.</span><span class="sxs-lookup"><span data-stu-id="1d60a-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you to distribute data to multiple regions with low latency access anywhere in the workload.</span></span> <span data-ttu-id="1d60a-105">Dit model wordt meestal gebruikt voor publisher/consumer werkbelastingen wanneer er een schrijver in één geografische regio en globaal gedistribueerde lezers in andere regio (lezen).</span><span class="sxs-lookup"><span data-stu-id="1d60a-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="1d60a-106">U kunt ook Azure Cosmos DB globale Replicatieondersteuning gebruiken om toepassingen waarin schrijvers en lezers worden globaal gedistribueerd te bouwen.</span><span class="sxs-lookup"><span data-stu-id="1d60a-106">You can also use Azure Cosmos DB's global replication support to build applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="1d60a-107">Dit document bevat een patroon waarmee lokale schrijf- en lokale leestoegang voor gedistribueerde schrijvers met behulp van Azure DB die Cosmos bereiken.</span><span class="sxs-lookup"><span data-stu-id="1d60a-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="1d60a-108"><a id="ExampleScenario"></a>Publicatie - een voorbeeldscenario</span><span class="sxs-lookup"><span data-stu-id="1d60a-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="1d60a-109">We bekijken een werkelijk scenario te beschrijven hoe u globaal gedistribueerde meerdere-region/meerdere-pre-master lezen schrijven patronen kunt gebruiken met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1d60a-109">Let's look at a real world scenario to describe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="1d60a-110">U kunt een content publishing platform gebouwd op Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1d60a-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="1d60a-111">Hier volgen enkele vereisten waaraan dit platform voor consumenten en uitgevers voor een goede gebruikerservaring moet voldoen.</span><span class="sxs-lookup"><span data-stu-id="1d60a-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="1d60a-112">Zowel auteurs en abonnees verdeeld over de hele wereld</span><span class="sxs-lookup"><span data-stu-id="1d60a-112">Both authors and subscribers are spread over the world</span></span> 
* <span data-ttu-id="1d60a-113">Auteurs moeten (schrijven) artikelen publiceren naar de lokale regio (dichtst)</span><span class="sxs-lookup"><span data-stu-id="1d60a-113">Authors must publish (write) articles to their local (closest) region</span></span>
* <span data-ttu-id="1d60a-114">Auteurs hebben lezers/abonnees van hun artikelen die zijn verdeeld over de hele wereld.</span><span class="sxs-lookup"><span data-stu-id="1d60a-114">Authors have readers/subscribers of their articles who are distributed across the globe.</span></span> 
* <span data-ttu-id="1d60a-115">Abonnees moeten een melding krijgen wanneer nieuwe artikelen worden gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="1d60a-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="1d60a-116">Abonnees moet leesrechten artikelen hun lokale regio.</span><span class="sxs-lookup"><span data-stu-id="1d60a-116">Subscribers must be able to read articles from their local region.</span></span> <span data-ttu-id="1d60a-117">Ze moeten ook worden kunnen beoordelingen toevoegen aan deze artikelen.</span><span class="sxs-lookup"><span data-stu-id="1d60a-117">They should also be able to add reviews to these articles.</span></span> 
* <span data-ttu-id="1d60a-118">Iedereen met inbegrip van de auteur van de artikelen moet kunnen weergeven, alle beoordelingen zijn verbonden met artikelen vanaf een lokale regio.</span><span class="sxs-lookup"><span data-stu-id="1d60a-118">Anyone including the author of the articles should be able view all the reviews attached to articles from a local region.</span></span> 

<span data-ttu-id="1d60a-119">Miljoenen consumenten en uitgevers miljarden artikelen, ervan uitgaande dat we hebben snel pakt u de problemen van de schaal samen met garanderen plaats van toegang.</span><span class="sxs-lookup"><span data-stu-id="1d60a-119">Assuming millions of consumers and publishers with billions of articles, soon we have to confront the problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="1d60a-120">Net als bij de meeste schaalbaarheidsproblemen, ligt de oplossing in de strategie voor een goede partitionering.</span><span class="sxs-lookup"><span data-stu-id="1d60a-120">As with most scalability problems, the solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="1d60a-121">Daarna bekijken we het model artikelen, controleren en meldingen als documenten, Azure DB die Cosmos-accounts configureren en implementeren van een gegevenstoegangslaag.</span><span class="sxs-lookup"><span data-stu-id="1d60a-121">Next, let's look at how to model articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="1d60a-122">Als u weten over partitioneren en partitiesleutels wilt, Zie [partitionerings- en schalen in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="1d60a-122">If you would like to learn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="1d60a-123"><a id="ModelingNotifications"></a>Modellering meldingen</span><span class="sxs-lookup"><span data-stu-id="1d60a-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="1d60a-124">Meldingen zijn gegevensfeeds specifiek voor een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1d60a-124">Notifications are data feeds specific to a user.</span></span> <span data-ttu-id="1d60a-125">Daarom zijn de toegangspatronen voor meldingen documenten altijd in de context van één gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1d60a-125">Therefore, the access patterns for notifications documents are always in the context of single user.</span></span> <span data-ttu-id="1d60a-126">U zou bijvoorbeeld 'een melding naar een gebruiker boeken' of 'alle meldingen voor een bepaalde gebruiker ophalen'.</span><span class="sxs-lookup"><span data-stu-id="1d60a-126">For example, you would "post a notification to a user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="1d60a-127">Ja, de beste keuze van de partitiesleutel voor dit type zou worden `UserId`.</span><span class="sxs-lookup"><span data-stu-id="1d60a-127">So, the optimal choice of partitioning key for this type would be `UserId`.</span></span>

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // The user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // The partition Key for the resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of the notification. 
        public string ArticleId { get; set; } 
    }

## <span data-ttu-id="1d60a-128"><a id="ModelingSubscriptions"></a>Modellering abonnementen</span><span class="sxs-lookup"><span data-stu-id="1d60a-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="1d60a-129">Abonnementen kunnen worden gemaakt voor de verschillende criteria zoals een specifieke categorie artikelen interessegebied of een bepaalde uitgever.</span><span class="sxs-lookup"><span data-stu-id="1d60a-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="1d60a-130">Daarom de `SubscriptionFilter` een goede keuze voor de partitiesleutel is.</span><span class="sxs-lookup"><span data-stu-id="1d60a-130">Hence the `SubscriptionFilter` is a good choice for partition key.</span></span>

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

## <span data-ttu-id="1d60a-131"><a id="ModelingArticles"></a>Vormgeven aan artikelen</span><span class="sxs-lookup"><span data-stu-id="1d60a-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="1d60a-132">Zodra een artikel wordt geïdentificeerd door meldingen, de volgende query's doorgaans zijn gebaseerd op de `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="1d60a-132">Once an article is identified through notifications, subsequent queries are typically based on the `Article.Id`.</span></span> <span data-ttu-id="1d60a-133">Kiezen `Article.Id` als partitie biedt de sleutel dus het beste distributiepunt voor het opslaan van de artikelen in een verzameling Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1d60a-133">Choosing `Article.Id` as partition the key thus provides the best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

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
        
        // Author of the article
        public string Author { get; set; }

        // Category/genre of the article
        public string Category { get; set; }

        // Tags associated with the article
        public string[] Tags { get; set; }

        // Title of the article
        public string Title { get; set; }
        
        //... 
    }

## <span data-ttu-id="1d60a-134"><a id="ModelingReviews"></a>Modellering beoordelingen</span><span class="sxs-lookup"><span data-stu-id="1d60a-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="1d60a-135">Beoordelingen zijn voornamelijk zoals artikelen, geschreven en gelezen in de context van het artikel.</span><span class="sxs-lookup"><span data-stu-id="1d60a-135">Like articles, reviews are mostly written and read in the context of article.</span></span> <span data-ttu-id="1d60a-136">Kiezen `ArticleId` een partitie sleutel biedt aanbevolen distributie en efficiënte toegang van revisies die zijn gekoppeld aan het artikel.</span><span class="sxs-lookup"><span data-stu-id="1d60a-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of the review 
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

## <span data-ttu-id="1d60a-137"><a id="DataAccessMethods"></a>Methoden voor gegevenstoegang laag</span><span class="sxs-lookup"><span data-stu-id="1d60a-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="1d60a-138">Nu we kijken naar de belangrijkste gegevens toegangsmethoden we moet implementeren.</span><span class="sxs-lookup"><span data-stu-id="1d60a-138">Now let's look at the main data access methods we need to implement.</span></span> <span data-ttu-id="1d60a-139">Hier volgt een lijst met methoden die de `ContentPublishDatabase` moet:</span><span class="sxs-lookup"><span data-stu-id="1d60a-139">Here's the list of methods that the `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="1d60a-140"><a id="Architecture"></a>Configuratie van Azure DB Cosmos-account</span><span class="sxs-lookup"><span data-stu-id="1d60a-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="1d60a-141">Als u wilt garanderen lokale leest en schrijft, we moet partitie-alleen gegevens niet op partitie sleutel, maar ook op basis van het toegangspatroon geografische in regio's.</span><span class="sxs-lookup"><span data-stu-id="1d60a-141">To guarantee local reads and writes, we must partition data not just on partition key, but also based on the geographical access pattern into regions.</span></span> <span data-ttu-id="1d60a-142">Het model afhankelijk is van een account Azure Cosmos DB database geo-replicatie voor elke regio.</span><span class="sxs-lookup"><span data-stu-id="1d60a-142">The model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="1d60a-143">Bijvoorbeeld, met twee gebieden is hier een instelling voor schrijfacties voor meerdere landen/regio:</span><span class="sxs-lookup"><span data-stu-id="1d60a-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="1d60a-144">Accountnaam</span><span class="sxs-lookup"><span data-stu-id="1d60a-144">Account Name</span></span> | <span data-ttu-id="1d60a-145">Regio schrijven</span><span class="sxs-lookup"><span data-stu-id="1d60a-145">Write Region</span></span> | <span data-ttu-id="1d60a-146">Lees de regio</span><span class="sxs-lookup"><span data-stu-id="1d60a-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="1d60a-147">Het volgende diagram toont hoe lees- en schrijfbewerkingen worden uitgevoerd in een typische toepassing met deze instellingen:</span><span class="sxs-lookup"><span data-stu-id="1d60a-147">The following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Azure meerdere masters Cosmos-DB-architectuur](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="1d60a-149">Hier volgt een codefragment met het initialiseren van de clients in een DAL uitgevoerd in de `West US` regio.</span><span class="sxs-lookup"><span data-stu-id="1d60a-149">Here is a code snippet showing how to initialize the clients in a DAL running in the `West US` region.</span></span>
    
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

<span data-ttu-id="1d60a-150">Met de voorgaande setup kan de gegevenstoegangslaag doorsturen alle schrijfbewerkingen naar het lokale account op basis van waarop deze wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="1d60a-150">With the preceding setup, the data access layer can forward all writes to the local account based on where it is deployed.</span></span> <span data-ttu-id="1d60a-151">Leesbewerkingen worden uitgevoerd door bij het lezen van beide accounts voor de globale weergave van gegevens.</span><span class="sxs-lookup"><span data-stu-id="1d60a-151">Reads are performed by reading from both accounts to get the global view of data.</span></span> <span data-ttu-id="1d60a-152">Deze methode kan worden uitgebreid met zoveel regio's waar nodig.</span><span class="sxs-lookup"><span data-stu-id="1d60a-152">This approach can be extended to as many regions as required.</span></span> <span data-ttu-id="1d60a-153">Dit is bijvoorbeeld een installatie met drie geografische regio's:</span><span class="sxs-lookup"><span data-stu-id="1d60a-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="1d60a-154">Accountnaam</span><span class="sxs-lookup"><span data-stu-id="1d60a-154">Account Name</span></span> | <span data-ttu-id="1d60a-155">Regio schrijven</span><span class="sxs-lookup"><span data-stu-id="1d60a-155">Write Region</span></span> | <span data-ttu-id="1d60a-156">Regio 1 lezen</span><span class="sxs-lookup"><span data-stu-id="1d60a-156">Read Region 1</span></span> | <span data-ttu-id="1d60a-157">Regio 2 lezen</span><span class="sxs-lookup"><span data-stu-id="1d60a-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="1d60a-158"><a id="DataAccessImplementation"></a>Data access-laag implementatie</span><span class="sxs-lookup"><span data-stu-id="1d60a-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="1d60a-159">Nu we bekijken de uitvoering van de gegevenstoegangslaag (DAL) voor een toepassing met twee beschrijfbare regio's.</span><span class="sxs-lookup"><span data-stu-id="1d60a-159">Now let's look at the implementation of the data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="1d60a-160">De DAL moet implementeren de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1d60a-160">The DAL must implement the following steps:</span></span>

* <span data-ttu-id="1d60a-161">Maken van meerdere exemplaren van `DocumentClient` voor elke account.</span><span class="sxs-lookup"><span data-stu-id="1d60a-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="1d60a-162">Met twee regio's, elk DAL-exemplaar heeft een `writeClient` en één `readClient`.</span><span class="sxs-lookup"><span data-stu-id="1d60a-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="1d60a-163">Op basis van de geïmplementeerde regio van de toepassing, configureren van de eindpunten voor `writeclient` en `readClient`.</span><span class="sxs-lookup"><span data-stu-id="1d60a-163">Based on the deployed region of the application, configure the endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="1d60a-164">Bijvoorbeeld, de DAL worden geïmplementeerd in `West US` gebruikt `contentpubdatabase-usa.documents.azure.com` voor het uitvoeren van schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="1d60a-164">For example, the DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="1d60a-165">De DAL geïmplementeerd in `NorthEurope` gebruikt `contentpubdatabase-europ.documents.azure.com` voor schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="1d60a-165">The DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="1d60a-166">Met de voorgaande setup kunnen de data access-methoden worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="1d60a-166">With the preceding setup, the data access methods can be implemented.</span></span> <span data-ttu-id="1d60a-167">Schrijven operations doorsturen van het schrijven naar de bijbehorende `writeClient`.</span><span class="sxs-lookup"><span data-stu-id="1d60a-167">Write operations forward the write to the corresponding `writeClient`.</span></span>

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

<span data-ttu-id="1d60a-168">Voor het lezen van meldingen en beoordelingen, moet u lezen van zowel regio's en union de resultaten zoals weergegeven in het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="1d60a-168">For reading notifications and reviews, you must read from both regions and union the results as shown in the following snippet:</span></span>

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

<span data-ttu-id="1d60a-169">Dus als u een goede te nemen partitionerende sleutel en statische op basis van een account partitioneren, kunt u bereiken met meerdere regio lokale geschreven en gelezen met behulp van Azure DB die Cosmos.</span><span class="sxs-lookup"><span data-stu-id="1d60a-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="1d60a-170"><a id="NextSteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1d60a-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="1d60a-171">In dit artikel wordt beschreven hoe u globaal gedistribueerde meerdere landen/regio lezen-schrijven patronen kunt gebruiken met Azure Cosmos DB met inhoud publiceren als een voorbeeldscenario.</span><span class="sxs-lookup"><span data-stu-id="1d60a-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="1d60a-172">Meer informatie over hoe Azure Cosmos DB ondersteunt [globale distributie](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="1d60a-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="1d60a-173">Meer informatie over [automatische en handmatige failover in Azure Cosmos-DB](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="1d60a-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="1d60a-174">Meer informatie over [globale consistentie met Azure Cosmos-DB](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="1d60a-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="1d60a-175">Ontwikkelen met meerdere regio's met behulp van de [Azure DB Cosmos - DocumentDB-API](tutorial-global-distribution-documentdb.md)</span><span class="sxs-lookup"><span data-stu-id="1d60a-175">Develop with multiple regions using the [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="1d60a-176">Ontwikkelen met meerdere regio's met behulp van de [Azure DB Cosmos - MongoDB-API](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="1d60a-176">Develop with multiple regions using the [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="1d60a-177">Ontwikkelen met meerdere regio's met behulp van de [Azure DB Cosmos - tabel-API](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="1d60a-177">Develop with multiple regions using the [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>
