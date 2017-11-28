---
title: Runtime-overzicht van Azure Functions | Microsoft Docs
description: Overzicht van de Azure Functions-Runtime-Preview
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
ms.openlocfilehash: cb98d5f2aaa526555820c15ba5a32fb7e78ffc5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="3e3a6-103">Overzicht van Azure Functions-Runtime</span><span class="sxs-lookup"><span data-stu-id="3e3a6-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="3e3a6-104">De Azure Functions-Runtime biedt een nieuwe manier om te profiteren van de eenvoud en flexibiliteit van de Azure Functions programming model lokale.</span><span class="sxs-lookup"><span data-stu-id="3e3a6-104">The Azure Functions Runtime provides a new way for you to take advantage of the simplicity and flexibility of the Azure Functions programming model on-premises.</span></span> <span data-ttu-id="3e3a6-105">Gebouwd op de dezelfde open-source hoofdmappen als Azure Functions, is Azure Functions-Runtime geïmplementeerde on-premises naar bieden een bijna identiek ontwikkeling biedt als de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="3e3a6-105">Built on the same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises to provide a nearly identical development experience as the cloud service.</span></span>

![Preview-Portal voor Azure Functions-Runtime][1]

<span data-ttu-id="3e3a6-107">De Azure Functions-Runtime biedt een manier om de ervaring van Azure Functions alvorens toe te wijzen aan de cloud.</span><span class="sxs-lookup"><span data-stu-id="3e3a6-107">The Azure Functions Runtime provides a way for you to experience Azure Functions before committing to the cloud.</span></span> <span data-ttu-id="3e3a6-108">Op deze manier kunnen kunnen de code-elementen die u bouwt vervolgens worden uitgevoerd met u naar de cloud wanneer u migreert.</span><span class="sxs-lookup"><span data-stu-id="3e3a6-108">In this way, the code assets you build can then be taken with you to the cloud when you migrate.</span></span>  <span data-ttu-id="3e3a6-109">De runtime ook wordt geopend nieuwe opties voor u, zoals het gebruik van de ongebruikte rekencapaciteit van uw lokale computers batchprocessen 's nachts uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3e3a6-109">The runtime also opens up new options for you, such as using the spare compute power of your on-premises computers to run batch processes overnight.</span></span> <span data-ttu-id="3e3a6-110">U kunt ook apparaten binnen uw organisatie gebruiken voorwaardelijk om gegevens te verzenden met andere systemen, zowel on-premises en in de cloud.</span><span class="sxs-lookup"><span data-stu-id="3e3a6-110">You can also use devices within your organization to conditionally send data to other systems, both on-premises and in the cloud.</span></span>

<span data-ttu-id="3e3a6-111">De Azure Functions-Runtime bestaat uit twee onderdelen:</span><span class="sxs-lookup"><span data-stu-id="3e3a6-111">The Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="3e3a6-112">Beheer van Azure Functions-Runtimerol</span><span class="sxs-lookup"><span data-stu-id="3e3a6-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="3e3a6-113">Azure Functions-Runtime-Werkrol</span><span class="sxs-lookup"><span data-stu-id="3e3a6-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="3e3a6-114">Azure Functions Beheerrol</span><span class="sxs-lookup"><span data-stu-id="3e3a6-114">Azure Functions Management Role</span></span>

<span data-ttu-id="3e3a6-115">De Azure Functions rol biedt een host voor het beheer van uw functies on-premises.</span><span class="sxs-lookup"><span data-stu-id="3e3a6-115">The Azure Functions Management Role provides a host for the management of your Functions on-premises.</span></span> <span data-ttu-id="3e3a6-116">Deze rol voert de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="3e3a6-116">This role performs the following tasks:</span></span>

* <span data-ttu-id="3e3a6-117">Hosting van de Azure Functions-beheerportal, dit is de hetzelfde account dat u ziet in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3e3a6-117">Hosting of the Azure Functions Management Portal, which is the the same one you see in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3e3a6-118">Hiermee kunt u het ontwikkelen van uw functies op dezelfde manier als in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3e3a6-118">This lets you develop your functions in the same way as you would in the Azure portal.</span></span>
* <span data-ttu-id="3e3a6-119">Functies over meerdere functies werknemers verdeeld.</span><span class="sxs-lookup"><span data-stu-id="3e3a6-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="3e3a6-120">Levert een publishing eindpunt zodat u uw functies direct vanuit Microsoft Visual Studio kunt publiceren.</span><span class="sxs-lookup"><span data-stu-id="3e3a6-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="3e3a6-121">Azure Functions-Werkrol</span><span class="sxs-lookup"><span data-stu-id="3e3a6-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="3e3a6-122">De Azure Functions-werkrollen zijn geïmplementeerd in Windows-Containers en dit is waar uw functiecode wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3e3a6-122">The Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="3e3a6-123">U kunt meerdere werkrollen implementeren binnen uw organisatie en is een belangrijke manier waarin klanten kunnen maken gebruik van ongebruikte rekenkracht.</span><span class="sxs-lookup"><span data-stu-id="3e3a6-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="3e3a6-124">Minimale vereisten</span><span class="sxs-lookup"><span data-stu-id="3e3a6-124">Minimum Requirements</span></span>

<span data-ttu-id="3e3a6-125">Aan de slag met de Azure Functions-Runtime moet u een machine met hebben **Windows Server 2016 of Windows 10 auteurs Update** met toegang tot een **SQL Server** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="3e3a6-125">To get started with the Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access to a **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e3a6-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3e3a6-126">Next Steps</span></span>

<span data-ttu-id="3e3a6-127">Installeer de [Azure Functions-Runtime-preview](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="3e3a6-127">Install the [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
