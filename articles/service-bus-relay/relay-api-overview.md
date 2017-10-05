---
title: Overzicht van Azure Relay-API | Microsoft Docs
description: Overzicht van de beschikbare Azure Relay-API 's
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 8d93a0344adc3b0b7617f3a7d85124142d7a7555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="9c577-103">Beschikbare Relay-API 's</span><span class="sxs-lookup"><span data-stu-id="9c577-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="9c577-104">Runtime-API 's</span><span class="sxs-lookup"><span data-stu-id="9c577-104">Runtime APIs</span></span>

<span data-ttu-id="9c577-105">De volgende tabel geeft een lijst met alle beschikbare Relay runtime-clients.</span><span class="sxs-lookup"><span data-stu-id="9c577-105">The following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="9c577-106">De [aanvullende informatie](#additional-information) sectie bevat meer informatie over de status van elke runtime-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="9c577-106">The [additional information](#additional-information) section contains more information about the status of each runtime library.</span></span>

| <span data-ttu-id="9c577-107">Taal/Platform</span><span class="sxs-lookup"><span data-stu-id="9c577-107">Language/Platform</span></span> | <span data-ttu-id="9c577-108">Beschikbare functie</span><span class="sxs-lookup"><span data-stu-id="9c577-108">Available feature</span></span> | <span data-ttu-id="9c577-109">Clientpakket</span><span class="sxs-lookup"><span data-stu-id="9c577-109">Client package</span></span> | <span data-ttu-id="9c577-110">Opslagplaats</span><span class="sxs-lookup"><span data-stu-id="9c577-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9c577-111">.NET-standaard</span><span class="sxs-lookup"><span data-stu-id="9c577-111">.NET Standard</span></span> | <span data-ttu-id="9c577-112">Hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="9c577-112">Hybrid Connections</span></span> | [<span data-ttu-id="9c577-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="9c577-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="9c577-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="9c577-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="9c577-115">.NET framework</span><span class="sxs-lookup"><span data-stu-id="9c577-115">.NET Framework</span></span> | <span data-ttu-id="9c577-116">WCF-relay</span><span class="sxs-lookup"><span data-stu-id="9c577-116">WCF Relay</span></span> | [<span data-ttu-id="9c577-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="9c577-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="9c577-118">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="9c577-118">N/A</span></span> |
| <span data-ttu-id="9c577-119">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="9c577-119">Node</span></span> | <span data-ttu-id="9c577-120">Hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="9c577-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="9c577-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="9c577-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="9c577-122">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="9c577-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="9c577-123">.NET</span><span class="sxs-lookup"><span data-stu-id="9c577-123">.NET</span></span>
<span data-ttu-id="9c577-124">Het .NET-ecosysteem heeft meerdere runtimes, dus er zijn meerdere .NET-bibliotheken voor Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="9c577-124">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="9c577-125">De standaard .NET-bibliotheek kan worden uitgevoerd met .NET Core of de .NET Framework, terwijl de .NET Framework-bibliotheek kan alleen worden uitgevoerd in een omgeving met .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="9c577-125">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="9c577-126">Zie voor meer informatie over .NET Frameworks [framework-versies](/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="9c577-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c577-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9c577-127">Next steps</span></span>
<span data-ttu-id="9c577-128">Volg deze koppelingen voor meer informatie over Azure Relay:</span><span class="sxs-lookup"><span data-stu-id="9c577-128">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="9c577-129">Wat is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="9c577-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="9c577-130">Veelgestelde vragen over Relay</span><span class="sxs-lookup"><span data-stu-id="9c577-130">Relay FAQ</span></span>](relay-faq.md)