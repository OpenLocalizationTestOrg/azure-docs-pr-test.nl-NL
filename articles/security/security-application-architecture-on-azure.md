---
title: Beveiliging integreren in uw Azure architectuur ontwerpen | Microsoft Docs
description: " Dit artikel helpt u een overzicht van de architectuur voor toepassingen en services in Azure om het gemakkelijker om te integreren met beveiliging ontwerpen en implementeren. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 4f2d9386-bda3-4ec8-8b1a-cd0c11242ffc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 91e46d690d3e7c298bc3b4020cc383ca99c43c4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="8fb14-103">Toepassingsarchitectuur in Azure</span><span class="sxs-lookup"><span data-stu-id="8fb14-103">Application architecture on Azure</span></span>
<span data-ttu-id="8fb14-104">Als u wilt beveiligen van uw cloud-gebaseerde oplossingen in Microsoft Azure een solide basis van de architectuur is essentieel.</span><span class="sxs-lookup"><span data-stu-id="8fb14-104">To help secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="8fb14-105">Architecten, ontwerpers en uitvoerders profiteren van een sterke kennis van de architectuur van toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="8fb14-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="8fb14-106">Deze fundamentele kennis helpt u inzicht in de onderdelen van uw cloud-gebaseerde oplossingen en makkelijker te beveiliging integreren in alle aspecten van uw ontwerp en de implementatie.</span><span class="sxs-lookup"><span data-stu-id="8fb14-106">This foundational knowledge helps you understand all the components of your cloud-based solutions and make it easier to integrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="8fb14-107">We hebben het volgende om u te helpen uw architectuur onderzoeken en ontwerpen:</span><span class="sxs-lookup"><span data-stu-id="8fb14-107">We have the following to help you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="8fb14-108">Architectuur infographics</span><span class="sxs-lookup"><span data-stu-id="8fb14-108">Architectural infographics</span></span>
* <span data-ttu-id="8fb14-109">Architecturale blauwdrukken</span><span class="sxs-lookup"><span data-stu-id="8fb14-109">Architectural blueprints</span></span>
* <span data-ttu-id="8fb14-110">Cloud en enterprise is ingesteld</span><span class="sxs-lookup"><span data-stu-id="8fb14-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="8fb14-111">3D-blauwdruk Visio-sjabloon</span><span class="sxs-lookup"><span data-stu-id="8fb14-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="8fb14-112">Architectuur infographics</span><span class="sxs-lookup"><span data-stu-id="8fb14-112">Architectural infographics</span></span>
<span data-ttu-id="8fb14-113">Microsoft publiceert verschillende architectuur gerelateerde posters/infographics.</span><span class="sxs-lookup"><span data-stu-id="8fb14-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="8fb14-114">Deze omvatten:</span><span class="sxs-lookup"><span data-stu-id="8fb14-114">They include:</span></span>

* [<span data-ttu-id="8fb14-115">Echte Cloud-toepassingen maken</span><span class="sxs-lookup"><span data-stu-id="8fb14-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="8fb14-116">Schalen met Cloudservices</span><span class="sxs-lookup"><span data-stu-id="8fb14-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="8fb14-117">Architecturale blauwdrukken</span><span class="sxs-lookup"><span data-stu-id="8fb14-117">Architectural blueprints</span></span>
<span data-ttu-id="8fb14-118">Publiceert Microsoft over een set op hoog niveau [bouwkundige blauwdrukken](http://aka.ms/azblueprints) die laat zien hoe u specifieke typen van systemen die Microsoft-producten.</span><span class="sxs-lookup"><span data-stu-id="8fb14-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how to build specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="8fb14-119">Elke blauwdruk bevat a:</span><span class="sxs-lookup"><span data-stu-id="8fb14-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="8fb14-120">Platte 2D Visio 2003-bestand dat u kunt downloaden en wijzigen</span><span class="sxs-lookup"><span data-stu-id="8fb14-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="8fb14-121">Kleur van de 3D-perspectief PDF-bestand in te voeren van de blauwdruk voor minder technische doelgroepen</span><span class="sxs-lookup"><span data-stu-id="8fb14-121">Colorful 3D perspective PDF file to introduce the blueprint to less technical audiences</span></span>
* <span data-ttu-id="8fb14-122">Video die bij de 3D-versie helpt</span><span class="sxs-lookup"><span data-stu-id="8fb14-122">Video that walks through the 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="8fb14-123">Cloud en enterprise is ingesteld</span><span class="sxs-lookup"><span data-stu-id="8fb14-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="8fb14-124">[De Visio en symbolen training video bekijken](http://aka.ms/CnESymbolsVideo) en vervolgens [downloaden van de Cloud en Enterprise symbool instellen](http://aka.ms/CnESymbols) om te beschrijven van Azure, Windows Server, SQL Server en meer technische materialen maken.</span><span class="sxs-lookup"><span data-stu-id="8fb14-124">[View the Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download the Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) to help create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="8fb14-125">U kunt de symbolen in architectuur diagrammen, trainingsmateriaal presentaties, gegevensbladen, infographics, whitepapers en zelfs van derden books gebruiken als het rapport mensen traint te gebruiken Microsoft-producten.</span><span class="sxs-lookup"><span data-stu-id="8fb14-125">You can use the symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if the book trains people to use Microsoft products.</span></span> <span data-ttu-id="8fb14-126">Ze zijn echter niet bedoeld voor gebruik in gebruikersinterfaces.</span><span class="sxs-lookup"><span data-stu-id="8fb14-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="8fb14-127">3D-blauwdruk Visio-sjabloon</span><span class="sxs-lookup"><span data-stu-id="8fb14-127">3D blueprint Visio template</span></span>
<span data-ttu-id="8fb14-128">De 3D-versies van de [Microsoft architectuur blauwdrukken](http://aka.ms/azblueprints) in eerste instantie zijn gemaakt in een niet-Microsoft-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="8fb14-128">The 3D versions of the [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="8fb14-129">Een nieuwe Visio 2013 (en hoger) sjabloon verzonden op 5 augustus 2015 als onderdeel van een [Microsoft Architecture certificeringsinstantie loop gedistribueerd bij EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span><span class="sxs-lookup"><span data-stu-id="8fb14-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="8fb14-130">De sjabloon is ook beschikbaar is buiten het verloop.</span><span class="sxs-lookup"><span data-stu-id="8fb14-130">The template is also available outside the course.</span></span>

* <span data-ttu-id="8fb14-131">[Bekijk de video training](http://aka.ms/3dBlueprintTemplateVideo) eerste zodat u weet wat u ermee kunt doen</span><span class="sxs-lookup"><span data-stu-id="8fb14-131">[View the training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="8fb14-132">Download de [Microsoft Visio-sjabloon voor 3D-blauwdruk](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="8fb14-132">Download the [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="8fb14-133">Download de [Cloud en Enterprise symbolen](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) voor gebruik met de 3D-sjabloon</span><span class="sxs-lookup"><span data-stu-id="8fb14-133">Download the [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) to use with the 3D template</span></span>
