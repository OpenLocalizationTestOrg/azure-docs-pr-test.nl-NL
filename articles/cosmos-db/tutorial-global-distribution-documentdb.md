---
title: aaaAzure Cosmos DB algemene distributie-zelfstudie voor DocumentDB-API | Microsoft Docs
description: Meer informatie over hoe toosetup Azure Cosmos DB globale distributie op basis Hallo DocumentDB-API.
services: cosmos-db
keywords: globale distributie, documentdb
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a><span data-ttu-id="2b2cc-104">Hoe toosetup Azure Cosmos DB globale distributie op basis Hallo DocumentDB-API</span><span class="sxs-lookup"><span data-stu-id="2b2cc-104">How toosetup Azure Cosmos DB global distribution using hello DocumentDB API</span></span>

<span data-ttu-id="2b2cc-105">In dit artikel, laten we zien hoe toouse hello Azure portal toosetup Azure Cosmos DB globale distributie en vervolgens verbinding maken via Hallo DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello DocumentDB API.</span></span>

<span data-ttu-id="2b2cc-106">Dit artikel behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="2b2cc-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="2b2cc-107">Globale distributie op basis van hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="2b2cc-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="2b2cc-108">Configureren van de algemene distributie op basis van Hallo [DocumentDB APIs](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="2b2cc-108">Configure global distribution using hello [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a><span data-ttu-id="2b2cc-109">De voorkeursregio tooa hello DocumentDB API met verbinding te maken</span><span class="sxs-lookup"><span data-stu-id="2b2cc-109">Connecting tooa preferred region using hello DocumentDB API</span></span>

<span data-ttu-id="2b2cc-110">In de volgorde tootake profiteren van [globale distributie](distribute-data-globally.md), clienttoepassingen Hallo besteld voorkeur lijst met regio's toobe gebruikte tooperform document bewerkingen kunnen opgeven.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="2b2cc-111">Dit kan worden gedaan door in te stellen Hallo verbindingsbeleid.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-111">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="2b2cc-112">Op basis van hello Azure DB die Cosmos-accountconfiguratie, huidige regionale beschikbaarheid en Hallo voorkeur lijst opgegeven, Hallo meeste optimale eindpunt wordt gekozen door Hallo DocumentDB SDK tooperform operations lezen en schrijven.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello DocumentDB SDK tooperform write and read operations.</span></span>

<span data-ttu-id="2b2cc-113">Deze lijst voorkeur is opgegeven bij het initialiseren van een verbinding met de Hallo DocumentDB SDK's.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-113">This preference list is specified when initializing a connection using hello DocumentDB SDKs.</span></span> <span data-ttu-id="2b2cc-114">Hallo SDK's accepteren een optionele parameter 'PreferredLocations' is een geordende lijst met Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-114">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="2b2cc-115">Hallo SDK worden automatisch alle schrijfbewerkingen toohello huidige schrijven regio verzonden.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-115">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="2b2cc-116">De eerste beschikbare regio toohello wordt alle leesbewerkingen verzonden in Hallo PreferredLocations lijst.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-116">All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="2b2cc-117">Als Hallo-aanvraag is mislukt, zal Hallo client mislukken omlaag Hallo lijst toohello volgende regio, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="2b2cc-118">Hallo SDK's proberen enkel tooread uit Hallo regio's die zijn opgegeven in PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-118">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="2b2cc-119">Dus bijvoorbeeld kunnen als Hallo databaseaccount beschikbaar in drie gebieden is, maar het Hallo-client alleen twee Hallo niet schrijven regio's voor PreferredLocations bevat, klikt u vervolgens geen leesbewerkingen worden geleverd buiten Hallo schrijven regio, zelfs in geval van Hallo van failover.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="2b2cc-120">Hallo-toepassing kunt Hallo huidige schrijven endpoint controleren en lezen eindpunt gekozen door Hallo SDK door te controleren of twee eigenschappen WriteEndpoint en ReadEndpoint beschikbaar in de SDK-versie 1.8 en hoger.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-120">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="2b2cc-121">Als Hallo PreferredLocations-eigenschap niet is ingesteld, worden alle aanvragen worden aangeboden via Hallo huidige schrijven regio.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-121">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="2b2cc-122">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="2b2cc-122">.NET SDK</span></span>
<span data-ttu-id="2b2cc-123">Hallo SDK kan worden gebruikt zonder codewijzigingen.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-123">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="2b2cc-124">In dit geval Hallo SDK automatisch wordt verwezen beide leest en schrijft toohello huidige schrijven regio.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-124">In this case, hello SDK automatically directs both reads and writes toohello current write region.</span></span>

<span data-ttu-id="2b2cc-125">In versie 1.8 en hoger van .NET SDK hello heeft Hallo ConnectionPolicy parameter voor Hallo DocumentClient constructor de eigenschap Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-125">In version 1.8 and later of hello .NET SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="2b2cc-126">Deze eigenschap is van het type verzameling `<string>` en een lijst met regionamen moeten bevatten.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="2b2cc-127">Hallo tekenreekswaarden zijn geformatteerd per Hallo regionaam kolom op Hallo [Azure-gebieden] [ regions] pagina, zonder spaties vóór of na Hallo eerste en laatste teken respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-127">hello string values are formatted per hello Region Name column on hello [Azure Regions][regions] page, with no spaces before or after hello first and last character respectively.</span></span>

<span data-ttu-id="2b2cc-128">Hallo huidige schrijven en lezen eindpunten zijn respectievelijk beschikbaar in DocumentClient.WriteEndpoint en DocumentClient.ReadEndpoint.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-128">hello current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="2b2cc-129">Hallo-URL's voor eindpunten Hallo moeten niet worden beschouwd als lange levensduur constanten.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-129">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="2b2cc-130">Hallo-service kan deze op elk gewenst moment bijwerken.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-130">hello service may update these at any point.</span></span> <span data-ttu-id="2b2cc-131">Hallo SDK verwerkt deze wijziging automatisch.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-131">hello SDK handles this change automatically.</span></span>
>
>

```csharp
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;
  
ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="2b2cc-132">NodeJS, JavaScript en Python SDK 's</span><span class="sxs-lookup"><span data-stu-id="2b2cc-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="2b2cc-133">Hallo SDK kan worden gebruikt zonder codewijzigingen.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-133">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="2b2cc-134">In dit geval Hallo die SDK automatisch wordt doorverwezen zowel leest en schrijft toohello huidige schrijven regio.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-134">In this case, hello SDK will automatically direct both reads and writes toohello current write region.</span></span>

<span data-ttu-id="2b2cc-135">In versie 1.8 en hoger van elke SDK Hallo ConnectionPolicy parameter voor Hallo DocumentClient constructor een nieuwe eigenschap DocumentClient.ConnectionPolicy.PreferredLocations aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-135">In version 1.8 and later of each SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="2b2cc-136">Dit is de parameter is een matrix met tekenreeksen die een lijst met regionamen neemt.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="2b2cc-137">Hallo-namen zijn geformatteerd per Hallo regionaam kolom in Hallo [Azure-gebieden] [ regions] pagina.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-137">hello names are formatted per hello Region Name column in hello [Azure Regions][regions] page.</span></span> <span data-ttu-id="2b2cc-138">U kunt ook vooraf gedefinieerde Hallo constanten in Hallo gemak object AzureDocuments.Regions gebruiken</span><span class="sxs-lookup"><span data-stu-id="2b2cc-138">You can also use hello predefined constants in hello convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="2b2cc-139">Hallo huidige schrijven en lezen eindpunten zijn respectievelijk beschikbaar in DocumentClient.getWriteEndpoint en DocumentClient.getReadEndpoint.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-139">hello current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="2b2cc-140">Hallo-URL's voor eindpunten Hallo moeten niet worden beschouwd als lange levensduur constanten.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-140">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="2b2cc-141">Hallo-service kan deze op elk gewenst moment bijwerken.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-141">hello service may update these at any point.</span></span> <span data-ttu-id="2b2cc-142">Hallo SDK wordt deze wijziging automatisch verwerkt.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-142">hello SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="2b2cc-143">Hieronder volgt een voorbeeld van code voor NodeJS/Javascript.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="2b2cc-144">Python en Java Hallo volgen hetzelfde patroon.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-144">Python and Java will follow hello same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="2b2cc-145">REST</span><span class="sxs-lookup"><span data-stu-id="2b2cc-145">REST</span></span>
<span data-ttu-id="2b2cc-146">Zodra een databaseaccount beschikbaar is gesteld in meerdere regio's, kunnen clients de beschikbaarheid opvragen door het uitvoeren van een aanvraag voor ophalen op Hallo URI te volgen.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on hello following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="2b2cc-147">Hallo-service retourneert een lijst met regio's en hun bijbehorende Azure DB die Cosmos-eindpunt URI's voor Hallo replica's.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-147">hello service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for hello replicas.</span></span> <span data-ttu-id="2b2cc-148">Hallo huidige schrijven regio wordt aangegeven in het Hallo-antwoord.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-148">hello current write region will be indicated in hello response.</span></span> <span data-ttu-id="2b2cc-149">Hallo-client kan vervolgens als volgt selecteren Hallo juiste eindpunt voor alle verdere REST-API-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-149">hello client can then select hello appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="2b2cc-150">Voorbeeld van een antwoord</span><span class="sxs-lookup"><span data-stu-id="2b2cc-150">Example response</span></span>

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* <span data-ttu-id="2b2cc-151">PUT, POST en DELETE-aanvragen moeten gaan toohello aangegeven schrijven URI</span><span class="sxs-lookup"><span data-stu-id="2b2cc-151">All PUT, POST and DELETE requests must go toohello indicated write URI</span></span>
* <span data-ttu-id="2b2cc-152">Alle opgehaald en andere aanvragen (bijvoorbeeld query's) met het kenmerk alleen-lezen gaat tooany eindpunt van de keuze van Hallo client</span><span class="sxs-lookup"><span data-stu-id="2b2cc-152">All GETs and other read-only requests (for example queries) may go tooany endpoint of hello client’s choice</span></span>

<span data-ttu-id="2b2cc-153">Schrijven tooread alleen-lezen regio's aanvragen mislukt met foutcode HTTP 403 ('verboden').</span><span class="sxs-lookup"><span data-stu-id="2b2cc-153">Write requests tooread-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="2b2cc-154">Als Hallo schrijven regio wordt gewijzigd na schrijft Hallo-client de initiële detectie fase daaropvolgende toohello vorige schrijven regio mislukt met foutcode HTTP 403 ('verboden').</span><span class="sxs-lookup"><span data-stu-id="2b2cc-154">If hello write region changes after hello client’s initial discovery phase, subsequent writes toohello previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="2b2cc-155">Hallo-client vervolgens krijgt Hallo lijst met regio's opnieuw tooget Hallo bijgewerkte schrijven regio.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-155">hello client should then GET hello list of regions again tooget hello updated write region.</span></span>

<span data-ttu-id="2b2cc-156">Dat is, die in deze zelfstudie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="2b2cc-157">U leert hoe toomanage consistentie van uw account globaal gerepliceerde Hallo door te lezen [consistentieniveaus in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="2b2cc-157">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="2b2cc-158">En Zie voor meer informatie over hoe globale databasereplicatie in Azure Cosmos DB werkt, [gegevens globaal met Azure Cosmos DB distribueren](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="2b2cc-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b2cc-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2b2cc-159">Next steps</span></span>

<span data-ttu-id="2b2cc-160">In deze zelfstudie hebt u Hallo volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="2b2cc-160">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2b2cc-161">Globale distributie op basis van hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="2b2cc-161">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="2b2cc-162">Globale distributie op basis van Hallo DocumentDB APIs configureren</span><span class="sxs-lookup"><span data-stu-id="2b2cc-162">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="2b2cc-163">U kunt nu doorgaan met de volgende zelfstudie toolearn toohello hoe toodevelop lokaal via Azure Cosmos DB lokale emulator Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b2cc-163">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b2cc-164">Lokaal ontwikkelen met Hallo emulator</span><span class="sxs-lookup"><span data-stu-id="2b2cc-164">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

