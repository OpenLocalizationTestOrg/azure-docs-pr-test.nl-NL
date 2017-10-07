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
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a>Meerdere master gerepliceerd globaal database architecturen met Azure Cosmos-DB
Azure Cosmos DB ondersteunt klare [globale replicatie](distribute-data-globally.md), waarmee u toodistribute gegevensgebieden toomultiple met lage latentie toegang overal in Hallo werkbelasting. Dit model wordt meestal gebruikt voor publisher/consumer werkbelastingen wanneer er een schrijver in één geografische regio en globaal gedistribueerde lezers in andere regio (lezen). 

U kunt ook Azure Cosmos DB globale replicatie ondersteuning toobuild toepassingen waarin schrijvers en lezers worden globaal gedistribueerd. Dit document bevat een patroon waarmee lokale schrijf- en lokale leestoegang voor gedistribueerde schrijvers met behulp van Azure DB die Cosmos bereiken.

## <a id="ExampleScenario"></a>Publicatie - een voorbeeldscenario
Bekijk een werkelijk scenario toodescribe hoe u globaal gedistribueerde meerdere-region/meerdere-pre-master lezen schrijven patronen kunt gebruiken met Azure Cosmos DB. U kunt een content publishing platform gebouwd op Azure Cosmos DB. Hier volgen enkele vereisten waaraan dit platform voor consumenten en uitgevers voor een goede gebruikerservaring moet voldoen.

* Zowel auteurs en abonnees verdeeld over Hallo wereld 
* Auteurs moeten (schrijven) artikelen tootheir lokale (dichtst) regio publiceren
* Auteurs hebben lezers/abonnees van hun artikelen die zijn verdeeld over de hele wereld Hallo. 
* Abonnees moeten een melding krijgen wanneer nieuwe artikelen worden gepubliceerd.
* Abonnees moet kunnen tooread artikelen van hun lokale regio. Ze moeten ook worden kunnen tooadd beoordelingen toothese artikelen. 
* Iedereen inclusief Hallo auteur Hallo artikelen moet kunnen weergeven, dat alle gekoppelde tooarticles beoordelingen van een lokale regio Hallo. 

Ervan uitgaande dat miljoenen consumenten en uitgevers miljarden artikelen, snel hebben we tooconfront Hallo problemen van de schaal samen met plaats van toegang te garanderen. Net als bij de meeste schaalbaarheidsproblemen, ligt Hallo oplossing in de strategie voor een goede partitionering. Vervolgens laten we kijken hoe toomodel artikelen, controleren en meldingen als documenten, Azure DB die Cosmos-accounts configureren en implementeren van een gegevenstoegangslaag. 

Als u meer informatie over partitioneren en partitiesleutels toolearn, Zie [partitionerings- en schalen in Azure Cosmos DB](partition-data.md).

## <a id="ModelingNotifications"></a>Modellering meldingen
Meldingen zijn gegevens feeds tooa specifieke gebruiker. Hallo toegangspatronen voor meldingen documenten zijn daarom altijd in de context Hallo van één gebruiker. U zou bijvoorbeeld 'posten een tooa meldingsgebruiker' of 'alle meldingen voor een bepaalde gebruiker ophalen'. Beste keuze van de partitiesleutel voor dit type zou worden dus Hallo `UserId`.

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

## <a id="ModelingSubscriptions"></a>Modellering abonnementen
Abonnementen kunnen worden gemaakt voor de verschillende criteria zoals een specifieke categorie artikelen interessegebied of een bepaalde uitgever. Daarom Hallo `SubscriptionFilter` een goede keuze voor de partitiesleutel is.

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

## <a id="ModelingArticles"></a>Vormgeven aan artikelen
Zodra een artikel wordt geïdentificeerd door meldingen, de volgende query's doorgaans zijn gebaseerd op Hallo `Article.Id`. Kiezen `Article.Id` als partitie biedt Hallo sleutel dus Hallo best distributiepunten voor het opslaan van de artikelen in een verzameling Azure Cosmos DB. 

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

## <a id="ModelingReviews"></a>Modellering beoordelingen
Beoordelingen zijn voornamelijk zoals artikelen, geschreven en gelezen in Hallo context van het artikel. Kiezen `ArticleId` een partitie sleutel biedt aanbevolen distributie en efficiënte toegang van revisies die zijn gekoppeld aan het artikel. 

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

## <a id="DataAccessMethods"></a>Methoden voor gegevenstoegang laag
Nu we kijken naar de belangrijkste gegevens Hallo toegangsmethoden moeten we tooimplement. Hier volgt de lijst Hallo van methoden die Hallo `ContentPublishDatabase` moet:

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <a id="Architecture"></a>Configuratie van Azure DB Cosmos-account
lokale tooguarantee leest en schrijft, we gegevens niet alleen op partitiesleutel moet partitioneren, maar ook op basis van de geografische toegangspatroon Hallo in regio's. Hallo model afhankelijk is van een account Azure Cosmos DB database geo-replicatie voor elke regio. Bijvoorbeeld, met twee gebieden is hier een instelling voor schrijfacties voor meerdere landen/regio:

| Accountnaam | Regio schrijven | Lees de regio |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

Hallo volgende diagram ziet u hoe lees- en schrijfbewerkingen worden uitgevoerd in een typische toepassing met deze instellingen:

![Azure meerdere masters Cosmos-DB-architectuur](./media/multi-region-writers/multi-master.png)

Hier volgt een codefragment met hoe tooinitialize clients in een DAL uitgevoerd in de Hallo Hallo `West US` regio.
    
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

Met de Hallo voorafgaand aan installatie, kan Hallo gegevenstoegangslaag doorsturen alle schrijfbewerkingen toohello lokale account op basis van waarop deze wordt geïmplementeerd. Leesbewerkingen worden uitgevoerd door bij het lezen van beide accounts tooget Hallo globale weergave van gegevens. Deze methode kan worden uitgebreid tooas veel regio's waar nodig. Dit is bijvoorbeeld een installatie met drie geografische regio's:

| Accountnaam | Regio schrijven | Regio 1 lezen | Regio 2 lezen |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <a id="DataAccessImplementation"></a>Data access-laag implementatie
Nu we bekijken Hallo-implementatie van Hallo gegevenstoegangslaag (DAL) voor een toepassing met twee beschrijfbare regio's. Hallo DAL moet implementeren Hallo stappen te volgen:

* Maken van meerdere exemplaren van `DocumentClient` voor elke account. Met twee regio's, elk DAL-exemplaar heeft een `writeClient` en één `readClient`. 
* Hallo-eindpunten voor op basis van regio van de toepassing hello Hallo geïmplementeerd, configureert `writeclient` en `readClient`. Bijvoorbeeld Hallo DAL geïmplementeerd `West US` gebruikt `contentpubdatabase-usa.documents.azure.com` voor het uitvoeren van schrijfbewerkingen. Hallo DAL geïmplementeerd in `NorthEurope` gebruikt `contentpubdatabase-europ.documents.azure.com` voor schrijfbewerkingen.

Met de Hallo voorafgaand aan installatie, kunnen toegangsmethoden Hallo-gegevens worden geïmplementeerd. Schrijven operations doorsturen Hallo schrijven toohello overeenkomt `writeClient`.

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

Voor het lezen van meldingen en beoordelingen, kunt u moet lezen van zowel de regio's en de resultaten union Hallo zoals weergegeven in het volgende codefragment Hallo:

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

Dus als u een goede te nemen partitionerende sleutel en statische op basis van een account partitioneren, kunt u bereiken met meerdere regio lokale geschreven en gelezen met behulp van Azure DB die Cosmos.

## <a id="NextSteps"></a>Volgende stappen
In dit artikel wordt beschreven hoe u globaal gedistribueerde meerdere landen/regio lezen-schrijven patronen kunt gebruiken met Azure Cosmos DB met inhoud publiceren als een voorbeeldscenario.

* Meer informatie over hoe Azure Cosmos DB ondersteunt [globale distributie](distribute-data-globally.md)
* Meer informatie over [automatische en handmatige failover in Azure Cosmos-DB](regional-failover.md)
* Meer informatie over [globale consistentie met Azure Cosmos-DB](consistency-levels.md)
* Ontwikkelen met meerdere regio's met behulp van Hallo [Azure DB Cosmos - DocumentDB-API](tutorial-global-distribution-documentdb.md)
* Ontwikkelen met meerdere regio's met behulp van Hallo [Azure DB Cosmos - MongoDB-API](tutorial-global-distribution-MongoDB.md)
* Ontwikkelen met meerdere regio's met behulp van Hallo [Azure DB Cosmos - tabel-API](tutorial-global-distribution-table.md)
