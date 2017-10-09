---
title: overzicht van Event Hubs-API aaaAzure | Microsoft Docs
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
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="d10e1-103">Beschikbare Event Hubs-API 's</span><span class="sxs-lookup"><span data-stu-id="d10e1-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="d10e1-104">Runtime-API 's</span><span class="sxs-lookup"><span data-stu-id="d10e1-104">Runtime APIs</span></span>

<span data-ttu-id="d10e1-105">Hallo Hieronder volgt een beschrijving van alle beschikbare Azure Event Hubs runtime-clients.</span><span class="sxs-lookup"><span data-stu-id="d10e1-105">hello following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="d10e1-106">Sommige van deze bibliotheken ook beperkte beheerfunctionaliteit bevatten, maar er zijn ook [specifieke bibliotheken](#management-apis) toomanagement operations toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d10e1-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated toomanagement operations.</span></span> <span data-ttu-id="d10e1-107">Hallo core focus van deze bibliotheken is toosend en berichten ontvangen van een event hub.</span><span class="sxs-lookup"><span data-stu-id="d10e1-107">hello core focus of these libraries is toosend and receive messages from an event hub.</span></span>

<span data-ttu-id="d10e1-108">Zie [aanvullende informatie](#additional-information) voor meer informatie over de huidige status Hallo van elke runtime-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="d10e1-108">See [additional information](#additional-information) for more details on hello current status of each runtime library.</span></span>

| <span data-ttu-id="d10e1-109">Taal/Platform</span><span class="sxs-lookup"><span data-stu-id="d10e1-109">Language/Platform</span></span> | <span data-ttu-id="d10e1-110">Clientpakket</span><span class="sxs-lookup"><span data-stu-id="d10e1-110">Client package</span></span> | <span data-ttu-id="d10e1-111">EventProcessorHost-pakket</span><span class="sxs-lookup"><span data-stu-id="d10e1-111">EventProcessorHost package</span></span> | <span data-ttu-id="d10e1-112">Opslagplaats</span><span class="sxs-lookup"><span data-stu-id="d10e1-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d10e1-113">.NET-standaard</span><span class="sxs-lookup"><span data-stu-id="d10e1-113">.NET Standard</span></span> | [<span data-ttu-id="d10e1-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="d10e1-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="d10e1-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="d10e1-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="d10e1-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="d10e1-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="d10e1-117">.NET framework</span><span class="sxs-lookup"><span data-stu-id="d10e1-117">.NET Framework</span></span> | [<span data-ttu-id="d10e1-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="d10e1-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="d10e1-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="d10e1-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="d10e1-120">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="d10e1-120">N/A</span></span> |
| <span data-ttu-id="d10e1-121">Java</span><span class="sxs-lookup"><span data-stu-id="d10e1-121">Java</span></span> | [<span data-ttu-id="d10e1-122">Maven</span><span class="sxs-lookup"><span data-stu-id="d10e1-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="d10e1-123">Maven</span><span class="sxs-lookup"><span data-stu-id="d10e1-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="d10e1-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="d10e1-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="d10e1-125">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="d10e1-125">Node</span></span> | [<span data-ttu-id="d10e1-126">NPM</span><span class="sxs-lookup"><span data-stu-id="d10e1-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="d10e1-127">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="d10e1-127">N/A</span></span> | [<span data-ttu-id="d10e1-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="d10e1-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="d10e1-129">C</span><span class="sxs-lookup"><span data-stu-id="d10e1-129">C</span></span> | <span data-ttu-id="d10e1-130">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="d10e1-130">N/A</span></span> | <span data-ttu-id="d10e1-131">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="d10e1-131">N/A</span></span> | [<span data-ttu-id="d10e1-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="d10e1-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="d10e1-133">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="d10e1-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="d10e1-134">.NET</span><span class="sxs-lookup"><span data-stu-id="d10e1-134">.NET</span></span>
<span data-ttu-id="d10e1-135">Hallo .NET ecosysteem heeft meerdere runtimes, dus er zijn meerdere .NET-bibliotheken voor Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d10e1-135">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="d10e1-136">Hallo .NET standaardbibliotheek kan worden uitgevoerd met .NET Core of .NET Framework, Hallo Hallo .NET Framework-bibliotheek kan alleen worden uitgevoerd in een omgeving met .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d10e1-136">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="d10e1-137">Zie voor meer informatie over .NET Frameworks [framework-versies](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="d10e1-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="d10e1-138">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="d10e1-138">Node</span></span>

<span data-ttu-id="d10e1-139">Hallo Node.js-bibliotheek is momenteel in preview en als een kant-project wordt beheerd door Microsoft-werknemers en externe medewerkers.</span><span class="sxs-lookup"><span data-stu-id="d10e1-139">hello Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="d10e1-140">Alle bijdragen, met inbegrip van broncode Welkom zijn en zal worden beoordeeld.</span><span class="sxs-lookup"><span data-stu-id="d10e1-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="d10e1-141">Management-API 's</span><span class="sxs-lookup"><span data-stu-id="d10e1-141">Management APIs</span></span>

<span data-ttu-id="d10e1-142">Hallo Hieronder volgt een lijst van alle beschikbare management specifieke bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="d10e1-142">hello following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="d10e1-143">Geen van deze bibliotheken runtime bewerkingen bevatten, en zijn voor Hallo enig doel van het beheer van Event Hubs-entiteiten.</span><span class="sxs-lookup"><span data-stu-id="d10e1-143">None of these libraries contain runtime operations, and are for hello sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="d10e1-144">Taal/Platform</span><span class="sxs-lookup"><span data-stu-id="d10e1-144">Language/Platform</span></span> | <span data-ttu-id="d10e1-145">Management Pack</span><span class="sxs-lookup"><span data-stu-id="d10e1-145">Management package</span></span> | <span data-ttu-id="d10e1-146">Opslagplaats</span><span class="sxs-lookup"><span data-stu-id="d10e1-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d10e1-147">.NET-standaard</span><span class="sxs-lookup"><span data-stu-id="d10e1-147">.NET Standard</span></span> | [<span data-ttu-id="d10e1-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="d10e1-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="d10e1-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="d10e1-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="d10e1-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d10e1-150">Next steps</span></span>
<span data-ttu-id="d10e1-151">U meer informatie over Event Hubs via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d10e1-151">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="d10e1-152">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="d10e1-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="d10e1-153">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="d10e1-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="d10e1-154">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d10e1-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)