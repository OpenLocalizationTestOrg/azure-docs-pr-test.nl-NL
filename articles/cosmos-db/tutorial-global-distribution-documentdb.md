---
title: Azure DB Cosmos globale distributie-zelfstudie voor DocumentDB-API | Microsoft Docs
description: Informatie over het instellen van Azure DB die Cosmos globale distributie op basis van de DocumentDB-API.
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
ms.openlocfilehash: f4d8efe9814bd28bb902567a23b541bc9b5414a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-documentdb-api"></a><span data-ttu-id="b4ac7-104">Het instellen van Azure DB die Cosmos globale distributie op basis van de DocumentDB-API</span><span class="sxs-lookup"><span data-stu-id="b4ac7-104">How to setup Azure Cosmos DB global distribution using the DocumentDB API</span></span>

<span data-ttu-id="b4ac7-105">In dit artikel, laten we zien hoe de Azure portal instellen van Azure DB die Cosmos globale distributie en vervolgens verbinding met de DocumentDB-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the DocumentDB API.</span></span>

<span data-ttu-id="b4ac7-106">In dit artikel bevat informatie over de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="b4ac7-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="b4ac7-107">Globale distributie op basis van de Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="b4ac7-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="b4ac7-108">Configureren globale distributie met behulp van de [DocumentDB APIs](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="b4ac7-108">Configure global distribution using the [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-documentdb-api"></a><span data-ttu-id="b4ac7-109">Verbinding maken met een voorkeursregio met de DocumentDB-API</span><span class="sxs-lookup"><span data-stu-id="b4ac7-109">Connecting to a preferred region using the DocumentDB API</span></span>

<span data-ttu-id="b4ac7-110">Om te profiteren van [globale distributie](distribute-data-globally.md), clienttoepassingen de voorkeur geordende lijst met regio's moeten worden gebruikt voor het document bewerkingen uitvoeren kunnen opgeven.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="b4ac7-111">Dit kan worden gedaan door het instellen van het verbindingsbeleid voor de.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-111">This can be done by setting the connection policy.</span></span> <span data-ttu-id="b4ac7-112">Op basis van de Azure DB die Cosmos-accountconfiguratie, huidige regionale beschikbaarheid en de voorkeur lijst is opgegeven, wordt het meest optimale eindpunt door de DocumentDB SDK schrijven uitvoeren en leesbewerkingen gekozen.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the DocumentDB SDK to perform write and read operations.</span></span>

<span data-ttu-id="b4ac7-113">Deze lijst voorkeur is opgegeven bij het initialiseren van een verbinding met de DocumentDB SDK's.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-113">This preference list is specified when initializing a connection using the DocumentDB SDKs.</span></span> <span data-ttu-id="b4ac7-114">De SDK's accepteren een optionele parameter 'PreferredLocations' is een geordende lijst met Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-114">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="b4ac7-115">Alle schrijfbewerkingen naar de huidige schrijven regio worden automatisch verzonden door de SDK.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-115">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="b4ac7-116">Alle leesbewerkingen wordt verzonden naar de eerste beschikbare regio in de lijst PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-116">All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="b4ac7-117">Als de aanvraag is mislukt, zal de client mislukken omlaag in de lijst voor de volgende regio, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="b4ac7-118">De SDK's wordt alleen poging tot lezen van de gebieden die zijn opgegeven in PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-118">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="b4ac7-119">Dus bijvoorbeeld kunnen als het databaseaccount beschikbaar in drie gebieden is, maar de client alleen twee van de niet-schrijven regio's voor PreferredLocations bevat, klikt u vervolgens geen leesbewerkingen worden geleverd buiten de regio schrijven, zelfs in het geval van failover.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="b4ac7-120">De toepassing kunt controleren of de huidige schrijven endpoint en lezen eindpunt gekozen door de SDK door het controleren van de twee eigenschappen, WriteEndpoint en ReadEndpoint beschikbaar in de SDK-versie 1.8 en hoger.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-120">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="b4ac7-121">Als de eigenschap PreferredLocations niet is ingesteld, worden alle aanvragen van de huidige schrijven regio worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-121">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="b4ac7-122">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="b4ac7-122">.NET SDK</span></span>
<span data-ttu-id="b4ac7-123">De SDK kan worden gebruikt zonder codewijzigingen.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-123">The SDK can be used without any code changes.</span></span> <span data-ttu-id="b4ac7-124">In dit geval de SDK automatisch wordt verwezen beide leest en schrijft naar het huidige schrijven gebied.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-124">In this case, the SDK automatically directs both reads and writes to the current write region.</span></span>

<span data-ttu-id="b4ac7-125">In versie 1.8 en hoger van de .NET SDK heeft de ConnectionPolicy-parameter voor de DocumentClient-constructor de eigenschap Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-125">In version 1.8 and later of the .NET SDK, the ConnectionPolicy parameter for the DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="b4ac7-126">Deze eigenschap is van het type verzameling `<string>` en een lijst met regionamen moeten bevatten.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="b4ac7-127">De string-waarden zijn geformatteerd per regio-naamkolom op de [Azure-gebieden] [ regions] pagina, zonder spaties vóór of na de eerste en laatste teken respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-127">The string values are formatted per the Region Name column on the [Azure Regions][regions] page, with no spaces before or after the first and last character respectively.</span></span>

<span data-ttu-id="b4ac7-128">De huidige geschreven en gelezen eindpunten zijn respectievelijk beschikbaar in DocumentClient.WriteEndpoint en DocumentClient.ReadEndpoint.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-128">The current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="b4ac7-129">De URL's voor de eindpunten niet beschouwd als lange levensduur constanten.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-129">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="b4ac7-130">De service kan deze op elk gewenst moment bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-130">The service may update these at any point.</span></span> <span data-ttu-id="b4ac7-131">De SDK verwerkt deze wijziging automatisch.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-131">The SDK handles this change automatically.</span></span>
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

// connect to DocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="b4ac7-132">NodeJS, JavaScript en Python SDK 's</span><span class="sxs-lookup"><span data-stu-id="b4ac7-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="b4ac7-133">De SDK kan worden gebruikt zonder codewijzigingen.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-133">The SDK can be used without any code changes.</span></span> <span data-ttu-id="b4ac7-134">De SDK wordt in dit geval automatisch doorverwezen zowel lees- en schrijfbewerkingen naar de huidige regio schrijven.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-134">In this case, the SDK will automatically direct both reads and writes to the current write region.</span></span>

<span data-ttu-id="b4ac7-135">In versie 1.8 en hoger van elke SDK, de ConnectionPolicy-parameter voor de constructor DocumentClient een nieuwe eigenschap aangeroepen DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-135">In version 1.8 and later of each SDK, the ConnectionPolicy parameter for the DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="b4ac7-136">Dit is de parameter is een matrix met tekenreeksen die een lijst met regionamen neemt.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="b4ac7-137">De namen zijn geformatteerd per de regionaam kolom in de [Azure-gebieden] [ regions] pagina.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-137">The names are formatted per the Region Name column in the [Azure Regions][regions] page.</span></span> <span data-ttu-id="b4ac7-138">U kunt ook de vooraf gedefinieerde constanten gebruiken in het gemak object AzureDocuments.Regions</span><span class="sxs-lookup"><span data-stu-id="b4ac7-138">You can also use the predefined constants in the convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="b4ac7-139">De huidige geschreven en gelezen eindpunten zijn respectievelijk beschikbaar in DocumentClient.getWriteEndpoint en DocumentClient.getReadEndpoint.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-139">The current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="b4ac7-140">De URL's voor de eindpunten niet beschouwd als lange levensduur constanten.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-140">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="b4ac7-141">De service kan deze op elk gewenst moment bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-141">The service may update these at any point.</span></span> <span data-ttu-id="b4ac7-142">De SDK is, wordt deze wijziging automatisch verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-142">The SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="b4ac7-143">Hieronder volgt een voorbeeld van code voor NodeJS/Javascript.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="b4ac7-144">Python en Java volgen hetzelfde patroon.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-144">Python and Java will follow the same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in the following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize the connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="b4ac7-145">REST</span><span class="sxs-lookup"><span data-stu-id="b4ac7-145">REST</span></span>
<span data-ttu-id="b4ac7-146">Zodra een databaseaccount beschikbaar is gesteld in meerdere regio's, kunnen clients de beschikbaarheid opvragen door het uitvoeren van een aanvraag voor ophalen naar de volgende URI.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on the following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="b4ac7-147">De service retourneert een lijst met regio's en hun bijbehorende Azure DB die Cosmos-eindpunt URI's voor de replica's.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-147">The service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for the replicas.</span></span> <span data-ttu-id="b4ac7-148">De huidige schrijven regio wordt aangegeven in het antwoord.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-148">The current write region will be indicated in the response.</span></span> <span data-ttu-id="b4ac7-149">De client kan vervolgens als volgt selecteren het juiste eindpunt voor alle verdere REST-API-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-149">The client can then select the appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="b4ac7-150">Voorbeeld van een antwoord</span><span class="sxs-lookup"><span data-stu-id="b4ac7-150">Example response</span></span>

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


* <span data-ttu-id="b4ac7-151">PUT, POST en DELETE-aanvragen, moeten verwijzen naar de opgegeven URI voor schrijven</span><span class="sxs-lookup"><span data-stu-id="b4ac7-151">All PUT, POST and DELETE requests must go to the indicated write URI</span></span>
* <span data-ttu-id="b4ac7-152">Alle opgehaald en andere aanvragen (bijvoorbeeld query's) met het kenmerk alleen-lezen mag verwijzen naar een willekeurig eindpunt van de keuze van de client</span><span class="sxs-lookup"><span data-stu-id="b4ac7-152">All GETs and other read-only requests (for example queries) may go to any endpoint of the client’s choice</span></span>

<span data-ttu-id="b4ac7-153">Schrijven naar aanvragen voor alleen-lezen gebieden mislukt met foutcode HTTP 403 ('verboden').</span><span class="sxs-lookup"><span data-stu-id="b4ac7-153">Write requests to read-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="b4ac7-154">Als de regio schrijven gewijzigd na de initiële detectie-fase van de client, mislukt schrijft naar de vorige schrijven regio met foutcode HTTP 403 ('verboden').</span><span class="sxs-lookup"><span data-stu-id="b4ac7-154">If the write region changes after the client’s initial discovery phase, subsequent writes to the previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="b4ac7-155">De client moet vervolgens de lijst met regio's om opnieuw op te halen van de bijgewerkte schrijven regio ophalen.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-155">The client should then GET the list of regions again to get the updated write region.</span></span>

<span data-ttu-id="b4ac7-156">Dat is, die in deze zelfstudie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="b4ac7-157">U kunt informatie over het beheren van de consistentie van uw account globaal gerepliceerde door te lezen [consistentieniveaus in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="b4ac7-157">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="b4ac7-158">En Zie voor meer informatie over hoe globale databasereplicatie in Azure Cosmos DB werkt, [gegevens globaal met Azure Cosmos DB distribueren](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="b4ac7-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4ac7-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b4ac7-159">Next steps</span></span>

<span data-ttu-id="b4ac7-160">In deze zelfstudie hebt u het volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="b4ac7-160">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b4ac7-161">Globale distributie op basis van de Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="b4ac7-161">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="b4ac7-162">Globale distributie op basis van de DocumentDB APIs configureren</span><span class="sxs-lookup"><span data-stu-id="b4ac7-162">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="b4ac7-163">U kunt nu doorgaan met de volgende zelfstudie voor meer informatie over het ontwikkelen van lokaal via de lokale Azure DB die Cosmos-emulator.</span><span class="sxs-lookup"><span data-stu-id="b4ac7-163">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b4ac7-164">Lokaal ontwikkelen met de emulator</span><span class="sxs-lookup"><span data-stu-id="b4ac7-164">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

