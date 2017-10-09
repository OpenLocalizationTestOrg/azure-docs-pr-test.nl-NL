---
title: aaaAzure Cosmos DB algemene distributie-zelfstudie voor Graph API | Microsoft Docs
description: Meer informatie over hoe toosetup Azure Cosmos DB globale distributie op basis Hallo Graph API.
services: cosmos-db
keywords: globale distributie, grafiek, gremlin
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a><span data-ttu-id="bcdd9-104">Hoe toosetup Azure Cosmos DB globale distributie op basis Hallo Graph API</span><span class="sxs-lookup"><span data-stu-id="bcdd9-104">How toosetup Azure Cosmos DB global distribution using hello Graph API</span></span>

<span data-ttu-id="bcdd9-105">In dit artikel, laten we zien hoe toouse hello Azure portal toosetup Azure Cosmos DB globale distributie en vervolgens verbinding maken via Hallo Graph API (preview).</span><span class="sxs-lookup"><span data-stu-id="bcdd9-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Graph API (preview).</span></span>

<span data-ttu-id="bcdd9-106">Dit artikel behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="bcdd9-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="bcdd9-107">Globale distributie op basis van hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="bcdd9-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="bcdd9-108">Configureren van de algemene distributie op basis van Hallo [Graph API's](graph-introduction.md) (preview)</span><span class="sxs-lookup"><span data-stu-id="bcdd9-108">Configure global distribution using hello [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a><span data-ttu-id="bcdd9-109">Verbinding maken met Hallo Graph API Hallo .NET SDK met de voorkeursregio tooa</span><span class="sxs-lookup"><span data-stu-id="bcdd9-109">Connecting tooa preferred region using hello Graph API using hello .NET SDK</span></span>

<span data-ttu-id="bcdd9-110">Hallo Graph API wordt weergegeven als een extensiebibliotheek boven op Hallo DocumentDB SDK.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-110">hello Graph API is exposed as an extension library on top of hello DocumentDB SDK.</span></span>

<span data-ttu-id="bcdd9-111">In de volgorde tootake profiteren van [globale distributie](distribute-data-globally.md), clienttoepassingen Hallo besteld voorkeur lijst met regio's toobe gebruikte tooperform document bewerkingen kunnen opgeven.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-111">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="bcdd9-112">Dit kan worden gedaan door in te stellen Hallo verbindingsbeleid.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-112">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="bcdd9-113">Op basis van hello Azure DB die Cosmos-accountconfiguratie, huidige regionale beschikbaarheid en Hallo voorkeur lijst opgegeven, Hallo meeste optimale eindpunt wordt gekozen door Hallo SDK tooperform schrijven en lees-en schrijfopdrachten.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-113">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello SDK tooperform write and read operations.</span></span>

<span data-ttu-id="bcdd9-114">Deze lijst voorkeur is opgegeven bij het initialiseren van een verbinding met de Hallo SDK's.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-114">This preference list is specified when initializing a connection using hello SDKs.</span></span> <span data-ttu-id="bcdd9-115">Hallo SDK's accepteren een optionele parameter 'PreferredLocations' is een geordende lijst met Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-115">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="bcdd9-116">**Schrijft**: Hallo SDK automatisch naar alle verzonden wordt schrijft toohello huidige schrijven regio.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-116">**Writes**: hello SDK will automatically send all writes toohello current write region.</span></span>
* <span data-ttu-id="bcdd9-117">**Leest**: alle leesbewerkingen worden de eerste beschikbare regio toohello in Hallo PreferredLocations lijst verzonden.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-117">**Reads**: All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="bcdd9-118">Als Hallo-aanvraag is mislukt, zal Hallo client mislukken omlaag Hallo lijst toohello volgende regio, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-118">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span> <span data-ttu-id="bcdd9-119">Hallo SDK's proberen enkel tooread uit Hallo regio's die zijn opgegeven in PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-119">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="bcdd9-120">Dus bijvoorbeeld kunnen als Hallo Cosmos-DB-account beschikbaar in drie gebieden is, maar het Hallo-client alleen twee Hallo niet schrijven regio's voor PreferredLocations bevat, klikt u vervolgens geen leesbewerkingen worden geleverd buiten Hallo schrijven regio, zelfs in geval van Hallo van failover.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-120">So, for example, if hello Cosmos DB account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="bcdd9-121">Hallo-toepassing kunt Hallo huidige schrijven endpoint controleren en lezen eindpunt gekozen door Hallo SDK door te controleren of twee eigenschappen WriteEndpoint en ReadEndpoint beschikbaar in de SDK-versie 1.8 en hoger.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-121">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="bcdd9-122">Als Hallo PreferredLocations-eigenschap niet is ingesteld, worden alle aanvragen worden aangeboden via Hallo huidige schrijven regio.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-122">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

### <a name="using-hello-sdk"></a><span data-ttu-id="bcdd9-123">Met behulp van Hallo SDK</span><span class="sxs-lookup"><span data-stu-id="bcdd9-123">Using hello SDK</span></span>

<span data-ttu-id="bcdd9-124">Bijvoorbeeld in Hallo .NET SDK, Hallo `ConnectionPolicy` parameter voor Hallo `DocumentClient` constructor heeft een eigenschap genaamd `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-124">For example, in hello .NET SDK, hello `ConnectionPolicy` parameter for hello `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="bcdd9-125">Deze eigenschap kan worden ingesteld als tooa lijst met regionamen.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-125">This property can be set tooa list of region names.</span></span> <span data-ttu-id="bcdd9-126">Hallo weergeven voor de namen van [Azure-gebieden] [ regions] kan worden opgegeven als onderdeel van `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-126">hello display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="bcdd9-127">Hallo-URL's voor eindpunten Hallo moeten niet worden beschouwd als lange levensduur constanten.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-127">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="bcdd9-128">Hallo-service kan deze op elk gewenst moment bijwerken.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-128">hello service may update these at any point.</span></span> <span data-ttu-id="bcdd9-129">Hallo SDK verwerkt deze wijziging automatisch.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-129">hello SDK handles this change automatically.</span></span>
>
>

```cs
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

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="bcdd9-130">Dat is, die in deze zelfstudie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="bcdd9-131">U leert hoe toomanage consistentie van uw account globaal gerepliceerde Hallo door te lezen [consistentieniveaus in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="bcdd9-131">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="bcdd9-132">En Zie voor meer informatie over hoe globale databasereplicatie in Azure Cosmos DB werkt, [gegevens globaal met Azure Cosmos DB distribueren](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="bcdd9-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcdd9-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bcdd9-133">Next steps</span></span>

<span data-ttu-id="bcdd9-134">In deze zelfstudie hebt u Hallo volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="bcdd9-134">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bcdd9-135">Globale distributie op basis van hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="bcdd9-135">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="bcdd9-136">Globale distributie op basis van Hallo DocumentDB APIs configureren</span><span class="sxs-lookup"><span data-stu-id="bcdd9-136">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="bcdd9-137">U kunt nu doorgaan met de volgende zelfstudie toolearn toohello hoe toodevelop lokaal via Azure Cosmos DB lokale emulator Hallo.</span><span class="sxs-lookup"><span data-stu-id="bcdd9-137">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bcdd9-138">Lokaal ontwikkelen met Hallo emulator</span><span class="sxs-lookup"><span data-stu-id="bcdd9-138">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

