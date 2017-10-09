---
title: aaaAzure Cosmos DB algemene distributie-zelfstudie voor tabel-API | Microsoft Docs
description: Meer informatie over hoe toosetup Azure Cosmos DB globale distributie op basis Hallo tabel-API.
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
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a><span data-ttu-id="b32e9-104">Hoe toosetup Azure Cosmos DB globale distributie op basis Hallo tabel-API</span><span class="sxs-lookup"><span data-stu-id="b32e9-104">How toosetup Azure Cosmos DB global distribution using hello Table API</span></span>

<span data-ttu-id="b32e9-105">In dit artikel, laten we zien hoe toouse hello Azure portal toosetup Azure Cosmos DB globale distributie en vervolgens verbinding maken via Hallo tabel-API (preview).</span><span class="sxs-lookup"><span data-stu-id="b32e9-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Table API (preview).</span></span>

<span data-ttu-id="b32e9-106">Dit artikel behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="b32e9-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="b32e9-107">Globale distributie op basis van hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="b32e9-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="b32e9-108">Configureren van de algemene distributie op basis van Hallo [tabel-API](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="b32e9-108">Configure global distribution using hello [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a><span data-ttu-id="b32e9-109">Verbinding maken met tooa voorkeursregio met Hallo tabel-API</span><span class="sxs-lookup"><span data-stu-id="b32e9-109">Connecting tooa preferred region using hello Table API</span></span>

<span data-ttu-id="b32e9-110">In de volgorde tootake profiteren van [globale distributie](distribute-data-globally.md), clienttoepassingen Hallo besteld voorkeur lijst met regio's toobe gebruikte tooperform document bewerkingen kunnen opgeven.</span><span class="sxs-lookup"><span data-stu-id="b32e9-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="b32e9-111">Dit kan worden gedaan door de instelling Hallo `TablePreferredLocations` configuratiewaarde in Hallo app-configuratie voor Hallo preview Azure-opslag-SDK.</span><span class="sxs-lookup"><span data-stu-id="b32e9-111">This can be done by setting hello `TablePreferredLocations` configuration value in hello app config for hello preview Azure Storage SDK.</span></span> <span data-ttu-id="b32e9-112">Op basis van hello Azure DB die Cosmos-accountconfiguratie, huidige regionale beschikbaarheid en Hallo voorkeur lijst die is opgegeven, Hallo meeste optimale eindpunt wordt gekozen door hello Azure-opslag-SDK tooperform schrijven en lees-en schrijfopdrachten.</span><span class="sxs-lookup"><span data-stu-id="b32e9-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello Azure Storage SDK tooperform write and read operations.</span></span>

<span data-ttu-id="b32e9-113">Hallo `TablePreferredLocations` moet een door komma's gescheiden lijst met aanbevolen (multihoming) locaties bevatten voor leesbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="b32e9-113">hello `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="b32e9-114">Elk clientexemplaar kunt u een subset van deze gebieden in volgorde van voorkeur Hallo voor lage latentie leesbewerkingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="b32e9-114">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="b32e9-115">Hallo-regio's moeten de namen van hun [weergavenamen](https://msdn.microsoft.com/library/azure/gg441293.aspx), bijvoorbeeld `West US`.</span><span class="sxs-lookup"><span data-stu-id="b32e9-115">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="b32e9-116">Alle leest de eerste beschikbare regio toohello verzonden in Hallo `TablePreferredLocations` lijst.</span><span class="sxs-lookup"><span data-stu-id="b32e9-116">All reads will be sent toohello first available region in hello `TablePreferredLocations` list.</span></span> <span data-ttu-id="b32e9-117">Als Hallo-aanvraag is mislukt, zal Hallo client mislukken omlaag Hallo lijst toohello volgende regio, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="b32e9-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="b32e9-118">Hallo SDK proberen enkel tooread uit Hallo regio's die zijn opgegeven in `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="b32e9-118">hello SDK will only attempt tooread from hello regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="b32e9-119">Dus bijvoorbeeld als Hallo databaseaccount beschikbaar in drie gebieden is, maar het Hallo-client alleen twee van bevat Hallo niet schrijven regio's voor `TablePreferredLocations`, en vervolgens geen leesbewerkingen buiten Hallo schrijven regio, zelfs in geval van Hallo van failover kunnen worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="b32e9-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for `TablePreferredLocations`, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="b32e9-120">Hallo SDK worden automatisch alle schrijfbewerkingen toohello huidige schrijven regio verzonden.</span><span class="sxs-lookup"><span data-stu-id="b32e9-120">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="b32e9-121">Als hello `TablePreferredLocations` eigenschap niet is ingesteld, worden alle aanvragen worden aangeboden via Hallo huidige schrijven regio.</span><span class="sxs-lookup"><span data-stu-id="b32e9-121">If hello `TablePreferredLocations` property is not set, all requests will be served from hello current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="b32e9-122">Dat is, die in deze zelfstudie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b32e9-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="b32e9-123">U leert hoe toomanage consistentie van uw account globaal gerepliceerde Hallo door te lezen [consistentieniveaus in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="b32e9-123">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="b32e9-124">En Zie voor meer informatie over hoe globale databasereplicatie in Azure Cosmos DB werkt, [gegevens globaal met Azure Cosmos DB distribueren](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="b32e9-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b32e9-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b32e9-125">Next steps</span></span>

<span data-ttu-id="b32e9-126">In deze zelfstudie hebt u Hallo volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="b32e9-126">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b32e9-127">Globale distributie op basis van hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="b32e9-127">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="b32e9-128">Globale distributie op basis van Hallo DocumentDB APIs configureren</span><span class="sxs-lookup"><span data-stu-id="b32e9-128">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="b32e9-129">U kunt nu doorgaan met de volgende zelfstudie toolearn toohello hoe toodevelop lokaal via Azure Cosmos DB lokale emulator Hallo.</span><span class="sxs-lookup"><span data-stu-id="b32e9-129">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b32e9-130">Lokaal ontwikkelen met Hallo emulator</span><span class="sxs-lookup"><span data-stu-id="b32e9-130">Develop locally with hello emulator</span></span>](local-emulator.md)
