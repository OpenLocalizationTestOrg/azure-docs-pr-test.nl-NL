---
title: Azure DB Cosmos algemene distributie-zelfstudie voor Graph API | Microsoft Docs
description: Informatie over het instellen van Azure DB die Cosmos globale distributie op basis van de Graph API.
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
ms.openlocfilehash: 3c8794fe33c2ff5aa79559ea2c323cf8d92b426a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-graph-api"></a><span data-ttu-id="6b342-104">Het instellen van Azure DB die Cosmos globale distributie op basis van de Graph API</span><span class="sxs-lookup"><span data-stu-id="6b342-104">How to setup Azure Cosmos DB global distribution using the Graph API</span></span>

<span data-ttu-id="6b342-105">In dit artikel, laten we zien hoe de Azure portal gebruiken om setup Azure Cosmos DB globale distributie en maak verbinding met de Graph-API (preview).</span><span class="sxs-lookup"><span data-stu-id="6b342-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the Graph API (preview).</span></span>

<span data-ttu-id="6b342-106">In dit artikel bevat informatie over de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="6b342-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="6b342-107">Globale distributie op basis van de Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="6b342-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="6b342-108">Configureren globale distributie met behulp van de [Graph API's](graph-introduction.md) (preview)</span><span class="sxs-lookup"><span data-stu-id="6b342-108">Configure global distribution using the [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-graph-api-using-the-net-sdk"></a><span data-ttu-id="6b342-109">Verbinding maken met een voorkeursregio met behulp van de API van de grafiek met de .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6b342-109">Connecting to a preferred region using the Graph API using the .NET SDK</span></span>

<span data-ttu-id="6b342-110">De Graph API wordt weergegeven als een extensiebibliotheek boven op de DocumentDB SDK.</span><span class="sxs-lookup"><span data-stu-id="6b342-110">The Graph API is exposed as an extension library on top of the DocumentDB SDK.</span></span>

<span data-ttu-id="6b342-111">Om te profiteren van [globale distributie](distribute-data-globally.md), clienttoepassingen de voorkeur geordende lijst met regio's moeten worden gebruikt voor het document bewerkingen uitvoeren kunnen opgeven.</span><span class="sxs-lookup"><span data-stu-id="6b342-111">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="6b342-112">Dit kan worden gedaan door het instellen van het verbindingsbeleid voor de.</span><span class="sxs-lookup"><span data-stu-id="6b342-112">This can be done by setting the connection policy.</span></span> <span data-ttu-id="6b342-113">Op basis van de Azure DB die Cosmos-accountconfiguratie, huidige regionale beschikbaarheid en de voorkeur lijst is opgegeven, wordt het meest optimale eindpunt door de SDK schrijven uitvoeren en leesbewerkingen gekozen.</span><span class="sxs-lookup"><span data-stu-id="6b342-113">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the SDK to perform write and read operations.</span></span>

<span data-ttu-id="6b342-114">Deze lijst voorkeur is opgegeven bij het initialiseren van een verbinding met de SDK's.</span><span class="sxs-lookup"><span data-stu-id="6b342-114">This preference list is specified when initializing a connection using the SDKs.</span></span> <span data-ttu-id="6b342-115">De SDK's accepteren een optionele parameter 'PreferredLocations' is een geordende lijst met Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="6b342-115">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="6b342-116">**Schrijft**: de SDK wordt automatisch verzonden naar alle schrijfbewerkingen naar de huidige regio schrijven.</span><span class="sxs-lookup"><span data-stu-id="6b342-116">**Writes**: The SDK will automatically send all writes to the current write region.</span></span>
* <span data-ttu-id="6b342-117">**Leest**: alle leesbewerkingen wordt verzonden naar de eerste beschikbare regio in de lijst PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="6b342-117">**Reads**: All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="6b342-118">Als de aanvraag is mislukt, zal de client mislukken omlaag in de lijst voor de volgende regio, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="6b342-118">If the request fails, the client will fail down the list to the next region, and so on.</span></span> <span data-ttu-id="6b342-119">De SDK's wordt alleen poging tot lezen van de gebieden die zijn opgegeven in PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="6b342-119">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="6b342-120">Dus bijvoorbeeld kunnen als de Cosmos-DB-account beschikbaar in drie gebieden is, maar de client alleen twee van de niet-schrijven regio's voor PreferredLocations bevat, klikt u vervolgens geen leesbewerkingen worden geleverd buiten de regio schrijven, zelfs in het geval van failover.</span><span class="sxs-lookup"><span data-stu-id="6b342-120">So, for example, if the Cosmos DB account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="6b342-121">De toepassing kunt controleren of de huidige schrijven endpoint en lezen eindpunt gekozen door de SDK door het controleren van de twee eigenschappen, WriteEndpoint en ReadEndpoint beschikbaar in de SDK-versie 1.8 en hoger.</span><span class="sxs-lookup"><span data-stu-id="6b342-121">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="6b342-122">Als de eigenschap PreferredLocations niet is ingesteld, worden alle aanvragen van de huidige schrijven regio worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="6b342-122">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

### <a name="using-the-sdk"></a><span data-ttu-id="6b342-123">Met behulp van de SDK</span><span class="sxs-lookup"><span data-stu-id="6b342-123">Using the SDK</span></span>

<span data-ttu-id="6b342-124">In de .NET SDK, bijvoorbeeld de `ConnectionPolicy` parameter voor de `DocumentClient` constructor heeft een eigenschap genaamd `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="6b342-124">For example, in the .NET SDK, the `ConnectionPolicy` parameter for the `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="6b342-125">Deze eigenschap kan worden ingesteld op een lijst met regionamen.</span><span class="sxs-lookup"><span data-stu-id="6b342-125">This property can be set to a list of region names.</span></span> <span data-ttu-id="6b342-126">De namen van de weergave voor [Azure-gebieden] [ regions] kan worden opgegeven als onderdeel van `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="6b342-126">The display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="6b342-127">De URL's voor de eindpunten niet beschouwd als lange levensduur constanten.</span><span class="sxs-lookup"><span data-stu-id="6b342-127">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="6b342-128">De service kan deze op elk gewenst moment bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6b342-128">The service may update these at any point.</span></span> <span data-ttu-id="6b342-129">De SDK verwerkt deze wijziging automatisch.</span><span class="sxs-lookup"><span data-stu-id="6b342-129">The SDK handles this change automatically.</span></span>
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

// connect to Azure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="6b342-130">Dat is, die in deze zelfstudie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6b342-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="6b342-131">U kunt informatie over het beheren van de consistentie van uw account globaal gerepliceerde door te lezen [consistentieniveaus in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="6b342-131">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="6b342-132">En Zie voor meer informatie over hoe globale databasereplicatie in Azure Cosmos DB werkt, [gegevens globaal met Azure Cosmos DB distribueren](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="6b342-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b342-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6b342-133">Next steps</span></span>

<span data-ttu-id="6b342-134">In deze zelfstudie hebt u het volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="6b342-134">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b342-135">Globale distributie op basis van de Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="6b342-135">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="6b342-136">Globale distributie op basis van de DocumentDB APIs configureren</span><span class="sxs-lookup"><span data-stu-id="6b342-136">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="6b342-137">U kunt nu doorgaan met de volgende zelfstudie voor meer informatie over het ontwikkelen van lokaal via de lokale Azure DB die Cosmos-emulator.</span><span class="sxs-lookup"><span data-stu-id="6b342-137">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b342-138">Lokaal ontwikkelen met de emulator</span><span class="sxs-lookup"><span data-stu-id="6b342-138">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

