---
title: aaaWebJobs in Azure App Service
description: Meer informatie over hoe toobuild WebJobs toorun achtergrond test, communiceren met services zoals opslag en Service Bus en geplande taken maken.
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="4ed42-103">WebJobs in Azure App Service gebruiken</span><span class="sxs-lookup"><span data-stu-id="4ed42-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="4ed42-104">In dit artikel koppelingen toodocumentation resources over het toouse Azure WebJobs en hello Azure WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="4ed42-104">This article links toodocumentation resources about how toouse Azure WebJobs and hello Azure WebJobs SDK.</span></span> <span data-ttu-id="4ed42-105">Azure WebJobs bieden een eenvoudige manier toorun scripts of programma's als achtergrond processen op [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="4ed42-105">Azure WebJobs provide an easy way toorun scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="4ed42-106">U kunt uploaden en uitvoeren van een uitvoerbaar bestand zoals als cmd bat, exe (.NET) ps1, servicel, php, py, js en jar.</span><span class="sxs-lookup"><span data-stu-id="4ed42-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="4ed42-107">Deze programma's uitvoeren als WebJobs volgens een schema (cron) of continu.</span><span class="sxs-lookup"><span data-stu-id="4ed42-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="4ed42-108">Hallo WebJobs SDK kunt u gemakkelijker toouse Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4ed42-108">hello WebJobs SDK makes it easier toouse Azure Storage.</span></span> <span data-ttu-id="4ed42-109">Hallo WebJobs SDK is een binding en de trigger-systeem dat met Microsoft Azure Storage-Blobs, wachtrijen en tabellen, evenals Service Bus-wachtrijen werkt.</span><span class="sxs-lookup"><span data-stu-id="4ed42-109">hello WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="4ed42-110">Maken, implementeren en beheren van WebJobs is naadloos met geïntegreerde tooling in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4ed42-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="4ed42-111">WebJobs van sjablonen maken, publiceren en beheren (uitvoeren/stop/monitor/debug) ze.</span><span class="sxs-lookup"><span data-stu-id="4ed42-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="4ed42-112">Hallo WebJobs-dashboard in hello Azure-portal biedt krachtige beheermogelijkheden die u u volledige controle over Hallo uitvoering van WebJobs hebt, met inbegrip van Hallo mogelijkheid tooinvoke afzonderlijke functies binnen WebJobs.</span><span class="sxs-lookup"><span data-stu-id="4ed42-112">hello WebJobs dashboard in hello Azure portal provides powerful management capabilities that give you full control over hello execution of WebJobs, including hello ability tooinvoke individual functions within WebJobs.</span></span> <span data-ttu-id="4ed42-113">Hallo dashboard worden ook de functie runtimes en logboekregistratie uitvoer weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4ed42-113">hello dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

