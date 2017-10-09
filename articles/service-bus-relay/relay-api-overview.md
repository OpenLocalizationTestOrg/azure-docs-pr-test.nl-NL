---
title: overzicht van de Relay-API aaaAzure | Microsoft Docs
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
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="799a6-103">Beschikbare Relay-API 's</span><span class="sxs-lookup"><span data-stu-id="799a6-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="799a6-104">Runtime-API 's</span><span class="sxs-lookup"><span data-stu-id="799a6-104">Runtime APIs</span></span>

<span data-ttu-id="799a6-105">Hallo bevat volgende tabel alle beschikbare Relay runtime-clients.</span><span class="sxs-lookup"><span data-stu-id="799a6-105">hello following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="799a6-106">Hallo [aanvullende informatie](#additional-information) sectie vindt u meer informatie over Hallo status van elke runtime-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="799a6-106">hello [additional information](#additional-information) section contains more information about hello status of each runtime library.</span></span>

| <span data-ttu-id="799a6-107">Taal/Platform</span><span class="sxs-lookup"><span data-stu-id="799a6-107">Language/Platform</span></span> | <span data-ttu-id="799a6-108">Beschikbare functie</span><span class="sxs-lookup"><span data-stu-id="799a6-108">Available feature</span></span> | <span data-ttu-id="799a6-109">Clientpakket</span><span class="sxs-lookup"><span data-stu-id="799a6-109">Client package</span></span> | <span data-ttu-id="799a6-110">Opslagplaats</span><span class="sxs-lookup"><span data-stu-id="799a6-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="799a6-111">.NET-standaard</span><span class="sxs-lookup"><span data-stu-id="799a6-111">.NET Standard</span></span> | <span data-ttu-id="799a6-112">Hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="799a6-112">Hybrid Connections</span></span> | [<span data-ttu-id="799a6-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="799a6-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="799a6-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="799a6-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="799a6-115">.NET framework</span><span class="sxs-lookup"><span data-stu-id="799a6-115">.NET Framework</span></span> | <span data-ttu-id="799a6-116">WCF-relay</span><span class="sxs-lookup"><span data-stu-id="799a6-116">WCF Relay</span></span> | [<span data-ttu-id="799a6-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="799a6-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="799a6-118">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="799a6-118">N/A</span></span> |
| <span data-ttu-id="799a6-119">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="799a6-119">Node</span></span> | <span data-ttu-id="799a6-120">Hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="799a6-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="799a6-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="799a6-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="799a6-122">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="799a6-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="799a6-123">.NET</span><span class="sxs-lookup"><span data-stu-id="799a6-123">.NET</span></span>
<span data-ttu-id="799a6-124">Hallo .NET ecosysteem heeft meerdere runtimes, dus er zijn meerdere .NET-bibliotheken voor Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="799a6-124">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="799a6-125">Hallo .NET standaardbibliotheek kan worden uitgevoerd met .NET Core of .NET Framework, Hallo Hallo .NET Framework-bibliotheek kan alleen worden uitgevoerd in een omgeving met .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="799a6-125">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="799a6-126">Zie voor meer informatie over .NET Frameworks [framework-versies](/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="799a6-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="799a6-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="799a6-127">Next steps</span></span>
<span data-ttu-id="799a6-128">toolearn meer informatie over Azure-Relay, gaat u naar deze koppelingen:</span><span class="sxs-lookup"><span data-stu-id="799a6-128">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="799a6-129">Wat is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="799a6-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="799a6-130">Veelgestelde vragen over Relay</span><span class="sxs-lookup"><span data-stu-id="799a6-130">Relay FAQ</span></span>](relay-faq.md)