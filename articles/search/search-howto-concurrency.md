---
title: aaaHow toomanage gelijktijdige schrijft tooresources in Azure Search
description: Optimistische gelijktijdigheid tooavoid Force Feedback conflicten op updates of verwijderingen tooAzure zoekindexen, Indexeerfuncties en gegevensbronnen gebruiken.
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: 
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: heidist
ms.openlocfilehash: c061d2b5c4d2dbd0fd5633405b01ab2912fbc754
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-concurrency-in-azure-search"></a><span data-ttu-id="9f463-103">Hoe toomanage gelijktijdigheid in Azure Search</span><span class="sxs-lookup"><span data-stu-id="9f463-103">How toomanage concurrency in Azure Search</span></span>

<span data-ttu-id="9f463-104">Bij het beheren van Azure Search-resources, zoals indexen en gegevensbronnen, is belangrijk tooupdate resources veilig, vooral als u resources gelijktijdig worden gebruikt door verschillende onderdelen van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="9f463-104">When managing Azure Search resources such as indexes and data sources, it's important tooupdate resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="9f463-105">Wanneer twee clients gelijktijdig een resource zijn zonder coördinatie bijwerkt, zijn racetoestanden mogelijk.</span><span class="sxs-lookup"><span data-stu-id="9f463-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="9f463-106">tooprevent deze, Azure Search biedt een *optimistische gelijktijdigheidsmodel*.</span><span class="sxs-lookup"><span data-stu-id="9f463-106">tooprevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="9f463-107">Er zijn geen vergrendelingen voor een bron.</span><span class="sxs-lookup"><span data-stu-id="9f463-107">There are no locks on a resource.</span></span> <span data-ttu-id="9f463-108">Er is in plaats daarvan een ETag voor elke bron die u Hallo resourceversie identificeert zodat u kunt aanvragen dat per ongeluk voorkomen opgesteld worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="9f463-108">Instead, there is an ETag for every resource that identifies hello resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="9f463-109">Conceptuele code in een [C#-oplossing steekproef](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) wordt uitgelegd hoe gelijktijdigheidbeheer werkt in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="9f463-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="9f463-110">Hallo code maakt voorwaarden die gelijktijdigheidbeheer aanroepen.</span><span class="sxs-lookup"><span data-stu-id="9f463-110">hello code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="9f463-111">Lezen Hallo [onderstaande codefragment](#samplecode) is waarschijnlijk voldoende voor de meeste ontwikkelaars, maar als u wilt dat toorun het, bewerken appsettings.json tooadd Hallo-servicenaam en een admin api-sleutel.</span><span class="sxs-lookup"><span data-stu-id="9f463-111">Reading hello [code fragment below](#samplecode) is probably sufficient for most developers, but if you want toorun it, edit appsettings.json tooadd hello service name and an admin api-key.</span></span> <span data-ttu-id="9f463-112">Een service-URL van de opgegeven `http://myservice.search.windows.net`, Hallo servicenaam is `myservice`.</span><span class="sxs-lookup"><span data-stu-id="9f463-112">Given a service URL of `http://myservice.search.windows.net`, hello service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="9f463-113">Hoe werkt het?</span><span class="sxs-lookup"><span data-stu-id="9f463-113">How it works</span></span>

<span data-ttu-id="9f463-114">Optimistische gelijktijdigheid van taken is geïmplementeerd via access voorwaarde controleert in API-aanroepen schrijven tooindexes, indexeerfuncties gegevensbronnen en synonymMap resources.</span><span class="sxs-lookup"><span data-stu-id="9f463-114">Optimistic concurrency is implemented through access condition checks in API calls writing tooindexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="9f463-115">Alle resources hebben een [ *entiteitscode (ETag)* ](https://en.wikipedia.org/wiki/HTTP_ETag) waarmee object versie-informatie.</span><span class="sxs-lookup"><span data-stu-id="9f463-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="9f463-116">Hallo ETag eerst inschakelt, kunt u voorkomen dat gelijktijdige wijzigingen in een typische werkstroom (ophalen, lokaal wijzigen, bijwerken) door ervoor te zorgen van Hallo resource ETag komt overeen met de lokale kopie.</span><span class="sxs-lookup"><span data-stu-id="9f463-116">By checking hello ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring hello resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="9f463-117">Hallo REST-API maakt gebruik van een [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) op Hallo aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="9f463-117">hello REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello request header.</span></span>
+ <span data-ttu-id="9f463-118">Hallo .NET SDK stelt Hallo ETag via een accessCondition-object instellen Hallo [If-Match | De header If-Match-geen](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) op Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="9f463-118">hello .NET SDK sets hello ETag through an accessCondition object, setting hello [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello resource.</span></span> <span data-ttu-id="9f463-119">Een object dat is overgenomen van [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) heeft een accessCondition-object.</span><span class="sxs-lookup"><span data-stu-id="9f463-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="9f463-120">Telkens wanneer u een resource bijwerkt, wordt de ETag automatisch gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="9f463-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="9f463-121">Wanneer u gelijktijdigheid management implementeert, wordt u alleen een voorwaarde plaatsen op Hallo updateaanvraag waarvoor de externe bron Hallo toohave Hallo dezelfde ETag als Hallo kopie van Hallo-bron die u hebt gewijzigd op Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="9f463-121">When you implement concurrency management, all you're doing is putting a precondition on hello update request that requires hello remote resource toohave hello same ETag as hello copy of hello resource that you modified on hello client.</span></span> <span data-ttu-id="9f463-122">Als een gelijktijdige proces al Hallo externe bron is gewijzigd, Hallo ETag niet overeenkomt met de voorwaarde Hallo en Hallo aanvraag mislukt met HTTP 412.</span><span class="sxs-lookup"><span data-stu-id="9f463-122">If a concurrent process has changed hello remote resource already, hello ETag will not match hello precondition and hello request will fail with HTTP 412.</span></span> <span data-ttu-id="9f463-123">Als u Hallo .NET SDK, dit zich voordoet als een `CloudException` waar Hallo `IsAccessConditionFailed()` uitbreidingsmethode ' true ' geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9f463-123">If you're using hello .NET SDK, this manifests as a `CloudException` where hello `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="9f463-124">Er is slechts één mechanisme voor gelijktijdigheid van taken.</span><span class="sxs-lookup"><span data-stu-id="9f463-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="9f463-125">Het wordt altijd gebruikt ongeacht welke API wordt gebruikt voor updates van de resource.</span><span class="sxs-lookup"><span data-stu-id="9f463-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="9f463-126">Gebruiksvoorbeelden en voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="9f463-126">Use cases and sample code</span></span>

<span data-ttu-id="9f463-127">Hallo volgende code toont accessCondition sleutel updatebewerkingen controleert:</span><span class="sxs-lookup"><span data-stu-id="9f463-127">hello following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="9f463-128">Een update mislukt als Hallo resource niet meer bestaat</span><span class="sxs-lookup"><span data-stu-id="9f463-128">Fail an update if hello resource no longer exists</span></span>
+ <span data-ttu-id="9f463-129">Een update mislukt als de resource-versie Hallo gewijzigd</span><span class="sxs-lookup"><span data-stu-id="9f463-129">Fail an update if hello resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="9f463-130">Voorbeeldcode uit [DotNetETagsExplainer programma](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span><span class="sxs-lookup"><span data-stu-id="9f463-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

```
    class Program
    {
        // This sample shows how ETags work by performing conditional updates and deletes
        // on an Azure Search index.
        static void Main(string[] args)
        {
            IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
            IConfigurationRoot configuration = builder.Build();

            SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

            Console.WriteLine("Deleting index...\n");
            DeleteTestIndexIfExists(serviceClient);

            // Every top-level resource in Azure Search has an associated ETag that keeps track of which version
            // of hello resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once hello resource exists in Azure Search, its ETag will be populated. Make sure toouse hello object
            // returned by hello SearchServiceClient! Otherwise, you will still have hello old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that hello update will only
            // succeed if hello index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates toohello same resource. If another
            // client tries tooupdate hello resource, it will fail as long as all clients are using hello right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. toostart, both clients see hello same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates hello index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries tooupdate hello index, but fails, thanks toohello ETag check.
            try
            {
                indexForClient2.Fields.Add(new Field("b", DataType.Boolean));
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient2, 
                    accessCondition: AccessCondition.IfNotChanged(indexForClient2));

                Console.WriteLine("Whoops; This shouldn't happen");
                Environment.Exit(1);
            }
            catch (CloudException e) when (e.IsAccessConditionFailed())
            {
                Console.WriteLine("Client 2 failed tooupdate hello index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of hello DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using hello Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // hello resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key tooend application...\n");
            Console.ReadKey();
        }

        private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
        {
            string searchServiceName = configuration["SearchServiceName"];
            string adminApiKey = configuration["SearchServiceAdminApiKey"];

            SearchServiceClient serviceClient =
                new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
            return serviceClient;
        }

        private static void DeleteTestIndexIfExists(SearchServiceClient serviceClient)
        {
            if (serviceClient.Indexes.Exists("test"))
            {
                serviceClient.Indexes.Delete("test");
            }
        }

        private static Index DefineTestIndex() =>
            new Index()
            {
                Name = "test",
                Fields = new[] { new Field("id", DataType.String) { IsKey = true } }
            };
    }
}
```

## <a name="design-pattern"></a><span data-ttu-id="9f463-131">Ontwerp</span><span class="sxs-lookup"><span data-stu-id="9f463-131">Design pattern</span></span>

<span data-ttu-id="9f463-132">Een ontwerppatroon voor de uitvoering van optimistische gelijktijdigheid bevatten een lus die pogingen Hallo voorwaarde de toegangscontrole, een test voor Hallo toegang voorwaarde, en desgewenst een bijgewerkte resource opgehaald voordat u probeert toore-Hallo wijzigingen toepassen.</span><span class="sxs-lookup"><span data-stu-id="9f463-132">A design pattern for implementing optimistic concurrency should include a loop that retries hello access condition check, a test for hello access condition, and optionally retrieves an updated resource before attempting toore-apply hello changes.</span></span> 

<span data-ttu-id="9f463-133">Dit codefragment illustreert Hallo toevoeging van een synonymMap tooan index die al bestaat.</span><span class="sxs-lookup"><span data-stu-id="9f463-133">This code snippet illustrates hello addition of a synonymMap tooan index that already exists.</span></span> <span data-ttu-id="9f463-134">Deze code is van Hallo [synoniem (preview) C#-zelfstudie voor Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span><span class="sxs-lookup"><span data-stu-id="9f463-134">This code is from hello [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="9f463-135">Hallo codefragment index Hallo "hotels" opgehaald, Hallo Objectversie op een updatebewerking controleert, genereert een uitzondering als Hallo voorwaarde mislukt en vervolgens nieuwe pogingen bewerking (omhoog toothree tijdstippen), die beginnen met een index voor het ophalen van Hallo server tooget Hallo laatste Hallo Versie.</span><span class="sxs-lookup"><span data-stu-id="9f463-135">hello snippet gets hello "hotels" index, checks hello object version on an update operation, throws an exception if hello condition fails, and then retries hello operation (up toothree times), starting with index retrieval from hello server tooget hello latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // hello IfNotChanged condition ensures that hello index is updated only if hello ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated hello index successfully.\n");
                    break;
                }
                catch (CloudException e) when (e.IsAccessConditionFailed())
                {
                    Console.WriteLine($"Index update failed : {e.Message}. Attempt({i}/{MaxNumTries}).\n");
                }
            }
        }
        
        private static Index AddSynonymMapsToFields(Index index)
        {
            index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
            index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };
            return index;
        }


## <a name="next-steps"></a><span data-ttu-id="9f463-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9f463-136">Next steps</span></span>

<span data-ttu-id="9f463-137">Bekijk Hallo [synoniemen C#-voorbeeld](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) voor meer context op hoe toosafely bijwerken voor een bestaande index.</span><span class="sxs-lookup"><span data-stu-id="9f463-137">Review hello [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how toosafely update an existing index.</span></span>

<span data-ttu-id="9f463-138">Probeer te wijzigen van een van de volgende Hallo voorbeelden tooinclude ETags of AccessCondition objecten.</span><span class="sxs-lookup"><span data-stu-id="9f463-138">Try modifying either of hello following samples tooinclude ETags or AccessCondition objects.</span></span>

+ [<span data-ttu-id="9f463-139">REST-API-voorbeeld op Github</span><span class="sxs-lookup"><span data-stu-id="9f463-139">REST API sample on Github</span></span>](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ <span data-ttu-id="9f463-140">[Voorbeeld van de .NET SDK op Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9f463-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="9f463-141">Deze oplossing bevat Hallo 'DotNetEtagsExplainer'-project met Hallo-code die in dit artikel worden gepresenteerd.</span><span class="sxs-lookup"><span data-stu-id="9f463-141">This solution includes hello "DotNetEtagsExplainer" project containing hello code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="9f463-142">Zie ook</span><span class="sxs-lookup"><span data-stu-id="9f463-142">See also</span></span>

  <span data-ttu-id="9f463-143">[Veelvoorkomende HTTP-headers voor aanvraag en -antwoord](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span><span class="sxs-lookup"><span data-stu-id="9f463-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="9f463-144">[HTTP-statuscodes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index-bewerkingen (REST-API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span><span class="sxs-lookup"><span data-stu-id="9f463-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>