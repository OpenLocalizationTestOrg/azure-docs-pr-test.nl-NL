---
title: Overzicht van Azure Event Hubs-API | Microsoft Docs
description: Overzicht van de beschikbare Azure Event Hubs-API 's
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 40cd76e1aacb68d6051cae4a3c90a8970f5449f0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="01059-103">Beschikbare Event Hubs-API 's</span><span class="sxs-lookup"><span data-stu-id="01059-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="01059-104">Runtime-API 's</span><span class="sxs-lookup"><span data-stu-id="01059-104">Runtime APIs</span></span>

<span data-ttu-id="01059-105">Hier volgt een beschrijving van alle beschikbare Azure Event Hubs runtime-clients.</span><span class="sxs-lookup"><span data-stu-id="01059-105">The following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="01059-106">Sommige van deze bibliotheken ook beperkte beheerfunctionaliteit bevatten, maar er zijn ook [specifieke bibliotheken](#management-apis) toegewezen aan beheertaken uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="01059-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated to management operations.</span></span> <span data-ttu-id="01059-107">De focus core van deze bibliotheken is verzenden en ontvangen van berichten van een event hub.</span><span class="sxs-lookup"><span data-stu-id="01059-107">The core focus of these libraries is to send and receive messages from an event hub.</span></span>

<span data-ttu-id="01059-108">Zie [aanvullende informatie](#additional-information) voor meer informatie over de huidige status van elke runtime-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="01059-108">See [additional information](#additional-information) for more details on the current status of each runtime library.</span></span>

| <span data-ttu-id="01059-109">Taal/Platform</span><span class="sxs-lookup"><span data-stu-id="01059-109">Language/Platform</span></span> | <span data-ttu-id="01059-110">Clientpakket</span><span class="sxs-lookup"><span data-stu-id="01059-110">Client package</span></span> | <span data-ttu-id="01059-111">EventProcessorHost-pakket</span><span class="sxs-lookup"><span data-stu-id="01059-111">EventProcessorHost package</span></span> | <span data-ttu-id="01059-112">Opslagplaats</span><span class="sxs-lookup"><span data-stu-id="01059-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="01059-113">.NET-standaard</span><span class="sxs-lookup"><span data-stu-id="01059-113">.NET Standard</span></span> | [<span data-ttu-id="01059-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="01059-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="01059-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="01059-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="01059-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="01059-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="01059-117">.NET framework</span><span class="sxs-lookup"><span data-stu-id="01059-117">.NET Framework</span></span> | [<span data-ttu-id="01059-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="01059-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="01059-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="01059-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="01059-120">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="01059-120">N/A</span></span> |
| <span data-ttu-id="01059-121">Java</span><span class="sxs-lookup"><span data-stu-id="01059-121">Java</span></span> | [<span data-ttu-id="01059-122">Maven</span><span class="sxs-lookup"><span data-stu-id="01059-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="01059-123">Maven</span><span class="sxs-lookup"><span data-stu-id="01059-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="01059-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="01059-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="01059-125">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="01059-125">Node</span></span> | [<span data-ttu-id="01059-126">NPM</span><span class="sxs-lookup"><span data-stu-id="01059-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="01059-127">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="01059-127">N/A</span></span> | [<span data-ttu-id="01059-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="01059-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="01059-129">C</span><span class="sxs-lookup"><span data-stu-id="01059-129">C</span></span> | <span data-ttu-id="01059-130">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="01059-130">N/A</span></span> | <span data-ttu-id="01059-131">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="01059-131">N/A</span></span> | [<span data-ttu-id="01059-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="01059-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="01059-133">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="01059-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="01059-134">.NET</span><span class="sxs-lookup"><span data-stu-id="01059-134">.NET</span></span>
<span data-ttu-id="01059-135">Het .NET-ecosysteem heeft meerdere runtimes, dus er zijn meerdere .NET-bibliotheken voor Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="01059-135">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="01059-136">De standaard .NET-bibliotheek kan worden uitgevoerd met .NET Core of de .NET Framework, terwijl de .NET Framework-bibliotheek kan alleen worden uitgevoerd in een omgeving met .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="01059-136">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="01059-137">Zie voor meer informatie over .NET Frameworks [framework-versies](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="01059-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="01059-138">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="01059-138">Node</span></span>

<span data-ttu-id="01059-139">De Node.js-bibliotheek is momenteel in preview en als een kant-project wordt beheerd door Microsoft-werknemers en externe medewerkers.</span><span class="sxs-lookup"><span data-stu-id="01059-139">The Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="01059-140">Alle bijdragen, met inbegrip van broncode Welkom zijn en zal worden beoordeeld.</span><span class="sxs-lookup"><span data-stu-id="01059-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="01059-141">Management-API 's</span><span class="sxs-lookup"><span data-stu-id="01059-141">Management APIs</span></span>

<span data-ttu-id="01059-142">Hier volgt een lijst met alle beschikbare management specifieke bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="01059-142">The following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="01059-143">Geen van deze bibliotheken runtime bewerkingen bevatten, en zijn voor enig doel van het beheer van Event Hubs-entiteiten.</span><span class="sxs-lookup"><span data-stu-id="01059-143">None of these libraries contain runtime operations, and are for the sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="01059-144">Taal/Platform</span><span class="sxs-lookup"><span data-stu-id="01059-144">Language/Platform</span></span> | <span data-ttu-id="01059-145">Management Pack</span><span class="sxs-lookup"><span data-stu-id="01059-145">Management package</span></span> | <span data-ttu-id="01059-146">Opslagplaats</span><span class="sxs-lookup"><span data-stu-id="01059-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="01059-147">.NET-standaard</span><span class="sxs-lookup"><span data-stu-id="01059-147">.NET Standard</span></span> | [<span data-ttu-id="01059-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="01059-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="01059-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="01059-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="01059-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="01059-150">Next steps</span></span>
<span data-ttu-id="01059-151">U kunt meer informatie over Event Hubs vinden via de volgende koppelingen:</span><span class="sxs-lookup"><span data-stu-id="01059-151">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="01059-152">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="01059-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="01059-153">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="01059-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="01059-154">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="01059-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)