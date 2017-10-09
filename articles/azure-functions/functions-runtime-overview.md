---
title: Overzicht van de Runtime Functions aaaAzure | Microsoft Docs
description: Overzicht van hello Azure Functions-Runtime-Preview
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="c1c93-103">Overzicht van Azure Functions-Runtime</span><span class="sxs-lookup"><span data-stu-id="c1c93-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="c1c93-104">Hello Azure Functions-Runtime biedt een nieuwe manier voor u tootake profiteren van Hallo eenvoud en flexibiliteit van hello Azure Functions programming model lokale.</span><span class="sxs-lookup"><span data-stu-id="c1c93-104">hello Azure Functions Runtime provides a new way for you tootake advantage of hello simplicity and flexibility of hello Azure Functions programming model on-premises.</span></span> <span data-ttu-id="c1c93-105">Gebouwd op Hallo dezelfde bron hoofdmappen zoals Azure Functions, Azure Functions-Runtime geïmplementeerde lokale tooprovide een bijna identiek ontwikkeling optreden als Hallo-cloudservice is geopend.</span><span class="sxs-lookup"><span data-stu-id="c1c93-105">Built on hello same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises tooprovide a nearly identical development experience as hello cloud service.</span></span>

![Preview-Portal voor Azure Functions-Runtime][1]

<span data-ttu-id="c1c93-107">Hello Azure Functions-Runtime biedt een manier voor u tooexperience Azure Functions alvorens toohello cloud toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="c1c93-107">hello Azure Functions Runtime provides a way for you tooexperience Azure Functions before committing toohello cloud.</span></span> <span data-ttu-id="c1c93-108">Op deze manier kunnen Hallo code activa die u bouwt vervolgens worden uitgevoerd met u toohello cloud wanneer u migreert.</span><span class="sxs-lookup"><span data-stu-id="c1c93-108">In this way, hello code assets you build can then be taken with you toohello cloud when you migrate.</span></span>  <span data-ttu-id="c1c93-109">Hallo runtime worden ook nieuwe opties voor u, zoals het gebruik van Hallo spare rekencapaciteit van uw lokale computers toorun batchprocessen nacht geopend.</span><span class="sxs-lookup"><span data-stu-id="c1c93-109">hello runtime also opens up new options for you, such as using hello spare compute power of your on-premises computers toorun batch processes overnight.</span></span> <span data-ttu-id="c1c93-110">U kunt apparaten binnen uw organisatie tooconditionally verzenden tooother gegevenssystemen, zowel on-premises en in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="c1c93-110">You can also use devices within your organization tooconditionally send data tooother systems, both on-premises and in hello cloud.</span></span>

<span data-ttu-id="c1c93-111">Hello Azure Functions-Runtime bestaat uit twee onderdelen:</span><span class="sxs-lookup"><span data-stu-id="c1c93-111">hello Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="c1c93-112">Beheer van Azure Functions-Runtimerol</span><span class="sxs-lookup"><span data-stu-id="c1c93-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="c1c93-113">Azure Functions-Runtime-Werkrol</span><span class="sxs-lookup"><span data-stu-id="c1c93-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="c1c93-114">Azure Functions Beheerrol</span><span class="sxs-lookup"><span data-stu-id="c1c93-114">Azure Functions Management Role</span></span>

<span data-ttu-id="c1c93-115">Hallo Beheerrol van Azure Functions biedt een host voor het Hallo-beheer van uw functies on-premises.</span><span class="sxs-lookup"><span data-stu-id="c1c93-115">hello Azure Functions Management Role provides a host for hello management of your Functions on-premises.</span></span> <span data-ttu-id="c1c93-116">Deze rol voert Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="c1c93-116">This role performs hello following tasks:</span></span>

* <span data-ttu-id="c1c93-117">Hosting van Azure Functions-beheerportal, Hallo HALLO hallo dezelfde is als die u in Hallo ziet [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c1c93-117">Hosting of hello Azure Functions Management Portal, which is hello hello same one you see in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c1c93-118">Deze kunt ontwikkelen van uw functies in Hallo dezelfde manier als in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c1c93-118">This lets you develop your functions in hello same way as you would in hello Azure portal.</span></span>
* <span data-ttu-id="c1c93-119">Functies over meerdere functies werknemers verdeeld.</span><span class="sxs-lookup"><span data-stu-id="c1c93-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="c1c93-120">Levert een publishing eindpunt zodat u uw functies direct vanuit Microsoft Visual Studio kunt publiceren.</span><span class="sxs-lookup"><span data-stu-id="c1c93-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="c1c93-121">Azure Functions-Werkrol</span><span class="sxs-lookup"><span data-stu-id="c1c93-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="c1c93-122">Hello Azure Functions-werkrollen zijn geïmplementeerd in Windows-Containers en dit is waar uw functiecode wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c1c93-122">hello Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="c1c93-123">U kunt meerdere werkrollen implementeren binnen uw organisatie en is een belangrijke manier waarin klanten kunnen maken gebruik van ongebruikte rekenkracht.</span><span class="sxs-lookup"><span data-stu-id="c1c93-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="c1c93-124">Minimale vereisten</span><span class="sxs-lookup"><span data-stu-id="c1c93-124">Minimum Requirements</span></span>

<span data-ttu-id="c1c93-125">tooget Hello Azure Functions-Runtime moet u een machine met hebben gestart **Windows Server 2016 of Windows 10 auteurs Update** met toegang tooa **SQL Server** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c1c93-125">tooget started with hello Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access tooa **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1c93-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1c93-126">Next Steps</span></span>

<span data-ttu-id="c1c93-127">Hallo installeren [Azure Functions-Runtime-preview](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="c1c93-127">Install hello [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
