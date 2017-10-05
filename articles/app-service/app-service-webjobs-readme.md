---
title: WebJobs in Azure App Service
description: Informatie over het bouwen van WebJobs achtergrond tests uitvoeren, communiceren met services zoals opslag en Service Bus en geplande taken maken.
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
ms.openlocfilehash: 1ca6d2eabe9781a8bb09fc5948ed306e3e8b013c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="cc5a9-103">WebJobs in Azure App Service gebruiken</span><span class="sxs-lookup"><span data-stu-id="cc5a9-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="cc5a9-104">Dit artikel bevat koppelingen naar documentatie over het gebruik van Azure WebJobs en de Azure WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-104">This article links to documentation resources about how to use Azure WebJobs and the Azure WebJobs SDK.</span></span> <span data-ttu-id="cc5a9-105">Azure WebJobs bieden een eenvoudige manier om het uitvoeren van scripts of programma's als achtergrondprocessen op [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="cc5a9-105">Azure WebJobs provide an easy way to run scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="cc5a9-106">U kunt uploaden en uitvoeren van een uitvoerbaar bestand zoals als cmd bat, exe (.NET) ps1, servicel, php, py, js en jar.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="cc5a9-107">Deze programma's uitvoeren als WebJobs volgens een schema (cron) of continu.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="cc5a9-108">De WebJobs SDK kunt gemakkelijker Azure Storage gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-108">The WebJobs SDK makes it easier to use Azure Storage.</span></span> <span data-ttu-id="cc5a9-109">De WebJobs SDK is een binding en de trigger-systeem dat met Microsoft Azure Storage-Blobs, wachtrijen en tabellen, evenals Service Bus-wachtrijen werkt.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-109">The WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="cc5a9-110">Maken, implementeren en beheren van WebJobs is naadloos met geïntegreerde tooling in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="cc5a9-111">WebJobs van sjablonen maken, publiceren en beheren (uitvoeren/stop/monitor/debug) ze.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="cc5a9-112">Het WebJobs-dashboard in de Azure portal biedt krachtige beheermogelijkheden die u volledige controle over de uitvoering van WebJobs zodat, inclusief de mogelijkheid om aan te roepen afzonderlijke functies binnen WebJobs.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-112">The WebJobs dashboard in the Azure portal provides powerful management capabilities that give you full control over the execution of WebJobs, including the ability to invoke individual functions within WebJobs.</span></span> <span data-ttu-id="cc5a9-113">Het dashboard worden bovendien de functie runtimes en logboekregistratie uitvoer weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-113">The dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

