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
# <a name="how-toomanage-concurrency-in-azure-search"></a>Hoe toomanage gelijktijdigheid in Azure Search

Bij het beheren van Azure Search-resources, zoals indexen en gegevensbronnen, is belangrijk tooupdate resources veilig, vooral als u resources gelijktijdig worden gebruikt door verschillende onderdelen van uw toepassing. Wanneer twee clients gelijktijdig een resource zijn zonder coördinatie bijwerkt, zijn racetoestanden mogelijk. tooprevent deze, Azure Search biedt een *optimistische gelijktijdigheidsmodel*. Er zijn geen vergrendelingen voor een bron. Er is in plaats daarvan een ETag voor elke bron die u Hallo resourceversie identificeert zodat u kunt aanvragen dat per ongeluk voorkomen opgesteld worden overschreven.

> [!Tip]
> Conceptuele code in een [C#-oplossing steekproef](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) wordt uitgelegd hoe gelijktijdigheidbeheer werkt in Azure Search. Hallo code maakt voorwaarden die gelijktijdigheidbeheer aanroepen. Lezen Hallo [onderstaande codefragment](#samplecode) is waarschijnlijk voldoende voor de meeste ontwikkelaars, maar als u wilt dat toorun het, bewerken appsettings.json tooadd Hallo-servicenaam en een admin api-sleutel. Een service-URL van de opgegeven `http://myservice.search.windows.net`, Hallo servicenaam is `myservice`.

## <a name="how-it-works"></a>Hoe werkt het?

Optimistische gelijktijdigheid van taken is geïmplementeerd via access voorwaarde controleert in API-aanroepen schrijven tooindexes, indexeerfuncties gegevensbronnen en synonymMap resources. 

Alle resources hebben een [ *entiteitscode (ETag)* ](https://en.wikipedia.org/wiki/HTTP_ETag) waarmee object versie-informatie. Hallo ETag eerst inschakelt, kunt u voorkomen dat gelijktijdige wijzigingen in een typische werkstroom (ophalen, lokaal wijzigen, bijwerken) door ervoor te zorgen van Hallo resource ETag komt overeen met de lokale kopie. 

+ Hallo REST-API maakt gebruik van een [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) op Hallo aanvraag-header.
+ Hallo .NET SDK stelt Hallo ETag via een accessCondition-object instellen Hallo [If-Match | De header If-Match-geen](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) op Hallo resource. Een object dat is overgenomen van [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) heeft een accessCondition-object.

Telkens wanneer u een resource bijwerkt, wordt de ETag automatisch gewijzigd. Wanneer u gelijktijdigheid management implementeert, wordt u alleen een voorwaarde plaatsen op Hallo updateaanvraag waarvoor de externe bron Hallo toohave Hallo dezelfde ETag als Hallo kopie van Hallo-bron die u hebt gewijzigd op Hallo-client. Als een gelijktijdige proces al Hallo externe bron is gewijzigd, Hallo ETag niet overeenkomt met de voorwaarde Hallo en Hallo aanvraag mislukt met HTTP 412. Als u Hallo .NET SDK, dit zich voordoet als een `CloudException` waar Hallo `IsAccessConditionFailed()` uitbreidingsmethode ' true ' geretourneerd.

> [!Note]
> Er is slechts één mechanisme voor gelijktijdigheid van taken. Het wordt altijd gebruikt ongeacht welke API wordt gebruikt voor updates van de resource. 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a>Gebruiksvoorbeelden en voorbeeldcode

Hallo volgende code toont accessCondition sleutel updatebewerkingen controleert:

+ Een update mislukt als Hallo resource niet meer bestaat
+ Een update mislukt als de resource-versie Hallo gewijzigd

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a>Voorbeeldcode uit [DotNetETagsExplainer programma](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)

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

## <a name="design-pattern"></a>Ontwerp

Een ontwerppatroon voor de uitvoering van optimistische gelijktijdigheid bevatten een lus die pogingen Hallo voorwaarde de toegangscontrole, een test voor Hallo toegang voorwaarde, en desgewenst een bijgewerkte resource opgehaald voordat u probeert toore-Hallo wijzigingen toepassen. 

Dit codefragment illustreert Hallo toevoeging van een synonymMap tooan index die al bestaat. Deze code is van Hallo [synoniem (preview) C#-zelfstudie voor Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk). 

Hallo codefragment index Hallo "hotels" opgehaald, Hallo Objectversie op een updatebewerking controleert, genereert een uitzondering als Hallo voorwaarde mislukt en vervolgens nieuwe pogingen bewerking (omhoog toothree tijdstippen), die beginnen met een index voor het ophalen van Hallo server tooget Hallo laatste Hallo Versie.

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


## <a name="next-steps"></a>Volgende stappen

Bekijk Hallo [synoniemen C#-voorbeeld](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) voor meer context op hoe toosafely bijwerken voor een bestaande index.

Probeer te wijzigen van een van de volgende Hallo voorbeelden tooinclude ETags of AccessCondition objecten.

+ [REST-API-voorbeeld op Github](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ [Voorbeeld van de .NET SDK op Github](https://github.com/Azure-Samples/search-dotnet-getting-started). Deze oplossing bevat Hallo 'DotNetEtagsExplainer'-project met Hallo-code die in dit artikel worden gepresenteerd.

## <a name="see-also"></a>Zie ook

  [Veelvoorkomende HTTP-headers voor aanvraag en -antwoord](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)    
  [HTTP-statuscodes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index-bewerkingen (REST-API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)