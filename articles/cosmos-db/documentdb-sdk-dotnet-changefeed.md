---
title: aaaAzure DocumentDB .NET wijziging Feed Processor SDK & Resources | Microsoft Docs
description: Meer informatie over Hallo wijziging Feed Processor API en de SDK, inclusief release datums, buiten gebruik stellen datums en wijzigingen die zijn aangebracht tussen elke versie van Hallo DocumentDB .NET wijziging Feed Processor SDK.
services: cosmos-db
documentationcenter: .net
author: ealsur
manager: kirillg
editor: mimig1
ms.assetid: f2dd9438-8879-4f74-bb6c-e1efc2cd0157
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: maquaran
ms.openlocfilehash: 7c001cc77f41c01445fb53328e9d99fd3d312c58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="75b38-103">DocumentDB .NET wijziging Feed Processor SDK: Downloaden en release-opmerkingen</span><span class="sxs-lookup"><span data-stu-id="75b38-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="75b38-104">.NET</span><span class="sxs-lookup"><span data-stu-id="75b38-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="75b38-105">.NET-Feed van wijzigen</span><span class="sxs-lookup"><span data-stu-id="75b38-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="75b38-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="75b38-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="75b38-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="75b38-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="75b38-108">Java</span><span class="sxs-lookup"><span data-stu-id="75b38-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="75b38-109">Python</span><span class="sxs-lookup"><span data-stu-id="75b38-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="75b38-110">REST</span><span class="sxs-lookup"><span data-stu-id="75b38-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="75b38-111">REST-resourceprovider</span><span class="sxs-lookup"><span data-stu-id="75b38-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="75b38-112">SQL</span><span class="sxs-lookup"><span data-stu-id="75b38-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="75b38-113">**SDK downloaden**</span><span class="sxs-lookup"><span data-stu-id="75b38-113">**SDK download**</span></span></td><td>[<span data-ttu-id="75b38-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="75b38-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="75b38-115">**API-documentatie**</span><span class="sxs-lookup"><span data-stu-id="75b38-115">**API documentation**</span></span></td><td>[<span data-ttu-id="75b38-116">API-naslagdocumentatie voor Processor Feed bibliotheek wijzigen</span><span class="sxs-lookup"><span data-stu-id="75b38-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="75b38-117">**Aan de slag**</span><span class="sxs-lookup"><span data-stu-id="75b38-117">**Get started**</span></span></td><td>[<span data-ttu-id="75b38-118">Aan de slag met Hallo DocumentDB wijziging Feed Processor .NET SDK</span><span class="sxs-lookup"><span data-stu-id="75b38-118">Get started with hello DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="75b38-119">**Huidige ondersteunde framework**</span><span class="sxs-lookup"><span data-stu-id="75b38-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="75b38-120">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="75b38-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="75b38-121">Releaseopmerkingen</span><span class="sxs-lookup"><span data-stu-id="75b38-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="75b38-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="75b38-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="75b38-123">Een methode tooobtain een schatting van de resterende werk toobe verwerkt in Hallo wijziging Feed toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="75b38-123">Added a method tooobtain an estimate of remaining work toobe processed in hello Change Feed.</span></span>
* <span data-ttu-id="75b38-124">Compatibel met [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) 1.13.2 versies en hoger.</span><span class="sxs-lookup"><span data-stu-id="75b38-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="75b38-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="75b38-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="75b38-126">GA SDK</span><span class="sxs-lookup"><span data-stu-id="75b38-126">GA SDK</span></span>
* <span data-ttu-id="75b38-127">Compatibel met [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versies 1.14.1 en lager.</span><span class="sxs-lookup"><span data-stu-id="75b38-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="75b38-128">Release & buiten gebruik stellen datums</span><span class="sxs-lookup"><span data-stu-id="75b38-128">Release & Retirement dates</span></span>
<span data-ttu-id="75b38-129">Microsoft biedt melding ten minste **12 maanden** voordat het buiten gebruik stellen van een SDK in de volgorde toosmooth Hallo overgang tooa nieuwere/ondersteunde versie.</span><span class="sxs-lookup"><span data-stu-id="75b38-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="75b38-130">Nieuwe functies en functionaliteit en optimalisaties worden alleen toegevoegd toohello huidige SDK, omdat het wordt aanbevolen dat u altijd upgrade toohello nieuwste SDK-versie zo spoedig mogelijk.</span><span class="sxs-lookup"><span data-stu-id="75b38-130">New features and functionality and optimizations are only added toohello current SDK, as such it is recommended that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="75b38-131">Een aanvraag tooCosmos DB met een buiten gebruik gestelde SDK worden geweigerd door Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="75b38-131">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="75b38-132">Versie</span><span class="sxs-lookup"><span data-stu-id="75b38-132">Version</span></span> | <span data-ttu-id="75b38-133">Releasedatum</span><span class="sxs-lookup"><span data-stu-id="75b38-133">Release Date</span></span> | <span data-ttu-id="75b38-134">Vervaldatum</span><span class="sxs-lookup"><span data-stu-id="75b38-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="75b38-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="75b38-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="75b38-136">13 augustus 2017</span><span class="sxs-lookup"><span data-stu-id="75b38-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="75b38-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="75b38-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="75b38-138">07 juli 2017</span><span class="sxs-lookup"><span data-stu-id="75b38-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="75b38-139">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="75b38-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="75b38-140">Zie ook</span><span class="sxs-lookup"><span data-stu-id="75b38-140">See also</span></span>
<span data-ttu-id="75b38-141">Zie toolearn meer informatie over de Cosmos-DB [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) pagina van de service.</span><span class="sxs-lookup"><span data-stu-id="75b38-141">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

