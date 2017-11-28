---
title: Zelfstudie voor Azure DB Cosmos globale distributie voor tabel-API | Microsoft Docs
description: Informatie over het instellen van Azure DB die Cosmos globale distributie op basis van de tabel-API.
services: cosmos-db
keywords: globale distributie, tabel
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
ms.openlocfilehash: 63c9e530a4982e2e6e478fea56e015fc77851e1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-table-api"></a><span data-ttu-id="477e1-104">Het instellen van Azure DB die Cosmos globale distributie op basis van de tabel-API</span><span class="sxs-lookup"><span data-stu-id="477e1-104">How to setup Azure Cosmos DB global distribution using the Table API</span></span>

<span data-ttu-id="477e1-105">In dit artikel, laten we zien hoe de Azure portal gebruiken om setup Azure Cosmos DB globale distributie en maak verbinding met de tabel-API (preview).</span><span class="sxs-lookup"><span data-stu-id="477e1-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the Table API (preview).</span></span>

<span data-ttu-id="477e1-106">In dit artikel bevat informatie over de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="477e1-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="477e1-107">Globale distributie op basis van de Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="477e1-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="477e1-108">Configureren globale distributie met behulp van de [tabel-API](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="477e1-108">Configure global distribution using the [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-table-api"></a><span data-ttu-id="477e1-109">Verbinding maken met een voorkeursregio met behulp van de tabel-API</span><span class="sxs-lookup"><span data-stu-id="477e1-109">Connecting to a preferred region using the Table API</span></span>

<span data-ttu-id="477e1-110">Om te profiteren van [globale distributie](distribute-data-globally.md), clienttoepassingen de voorkeur geordende lijst met regio's moeten worden gebruikt voor het document bewerkingen uitvoeren kunnen opgeven.</span><span class="sxs-lookup"><span data-stu-id="477e1-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="477e1-111">Dit kan worden gedaan door het instellen van de `TablePreferredLocations` configuratiewaarde in de app-configuratie voor de preview van Azure-opslag-SDK.</span><span class="sxs-lookup"><span data-stu-id="477e1-111">This can be done by setting the `TablePreferredLocations` configuration value in the app config for the preview Azure Storage SDK.</span></span> <span data-ttu-id="477e1-112">Op basis van de Azure DB die Cosmos-accountconfiguratie, huidige regionale beschikbaarheid en de voorkeur lijst is opgegeven, wordt het meest optimale eindpunt door de Azure-opslag-SDK schrijven uitvoeren en leesbewerkingen gekozen.</span><span class="sxs-lookup"><span data-stu-id="477e1-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the Azure Storage SDK to perform write and read operations.</span></span>

<span data-ttu-id="477e1-113">De `TablePreferredLocations` moet een door komma's gescheiden lijst met aanbevolen (multihoming) locaties bevatten voor leesbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="477e1-113">The `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="477e1-114">Elk clientexemplaar kunt u een subset van deze gebieden in de gewenste volgorde voor lage latentie leesbewerkingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="477e1-114">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="477e1-115">De regio's moeten de namen van hun [weergavenamen](https://msdn.microsoft.com/library/azure/gg441293.aspx), bijvoorbeeld `West US`.</span><span class="sxs-lookup"><span data-stu-id="477e1-115">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="477e1-116">Alle leesbewerkingen wordt verzonden naar de eerste beschikbare regio in de `TablePreferredLocations` lijst.</span><span class="sxs-lookup"><span data-stu-id="477e1-116">All reads will be sent to the first available region in the `TablePreferredLocations` list.</span></span> <span data-ttu-id="477e1-117">Als de aanvraag is mislukt, zal de client mislukken omlaag in de lijst voor de volgende regio, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="477e1-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="477e1-118">De SDK wordt alleen poging tot lezen van de gebieden die zijn opgegeven `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="477e1-118">The SDK will only attempt to read from the regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="477e1-119">Ja, bijvoorbeeld of de Account van de Database is beschikbaar in drie gebieden, maar de client geeft alleen twee van de niet-schrijven regio's voor `TablePreferredLocations`, en vervolgens geen leesbewerkingen buiten de regio schrijven, zelfs wanneer een failover kunnen worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="477e1-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for `TablePreferredLocations`, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="477e1-120">Alle schrijfbewerkingen naar de huidige schrijven regio worden automatisch verzonden door de SDK.</span><span class="sxs-lookup"><span data-stu-id="477e1-120">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="477e1-121">Als de `TablePreferredLocations` eigenschap niet is ingesteld, wordt alle aanvragen van het huidige schrijven gebied kunnen worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="477e1-121">If the `TablePreferredLocations` property is not set, all requests will be served from the current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="477e1-122">Dat is, die in deze zelfstudie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="477e1-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="477e1-123">U kunt informatie over het beheren van de consistentie van uw account globaal gerepliceerde door te lezen [consistentieniveaus in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="477e1-123">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="477e1-124">En Zie voor meer informatie over hoe globale databasereplicatie in Azure Cosmos DB werkt, [gegevens globaal met Azure Cosmos DB distribueren](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="477e1-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="477e1-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="477e1-125">Next steps</span></span>

<span data-ttu-id="477e1-126">In deze zelfstudie hebt u het volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="477e1-126">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="477e1-127">Globale distributie op basis van de Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="477e1-127">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="477e1-128">Globale distributie op basis van de DocumentDB APIs configureren</span><span class="sxs-lookup"><span data-stu-id="477e1-128">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="477e1-129">U kunt nu doorgaan met de volgende zelfstudie voor meer informatie over het ontwikkelen van lokaal via de lokale Azure DB die Cosmos-emulator.</span><span class="sxs-lookup"><span data-stu-id="477e1-129">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="477e1-130">Lokaal ontwikkelen met de emulator</span><span class="sxs-lookup"><span data-stu-id="477e1-130">Develop locally with the emulator</span></span>](local-emulator.md)