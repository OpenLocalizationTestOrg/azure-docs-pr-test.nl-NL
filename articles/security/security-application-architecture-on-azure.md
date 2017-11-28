---
title: aaaIntegrate beveiliging in uw Azure architectuur ontwerpen | Microsoft Docs
description: " In dit artikel krijgt u inzicht Hallo toepassingen en services architectuur op Azure toomake deze eenvoudiger toointegrate beveiliging in het ontwerp en de implementatie. "
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
ms.openlocfilehash: cfca8a1a2766f72bc3340c4e3df0019eb8b5a1e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="05532-103">Toepassingsarchitectuur in Azure</span><span class="sxs-lookup"><span data-stu-id="05532-103">Application architecture on Azure</span></span>
<span data-ttu-id="05532-104">toohelp Beveilig uw cloud-gebaseerde oplossingen in Microsoft Azure een solide basis van de architectuur is essentieel.</span><span class="sxs-lookup"><span data-stu-id="05532-104">toohelp secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="05532-105">Architecten, ontwerpers en uitvoerders profiteren van een sterke kennis van de architectuur van toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="05532-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="05532-106">Deze fundamentele kennis helpt u begrijpen alle Hallo onderdelen van uw cloud-gebaseerde oplossingen en maken het gemakkelijker toointegrate beveiliging in alle aspecten van uw ontwerp en de implementatie.</span><span class="sxs-lookup"><span data-stu-id="05532-106">This foundational knowledge helps you understand all hello components of your cloud-based solutions and make it easier toointegrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="05532-107">We hebben Hallo na toohelp u met uw architectuur onderzoeken en ontwerpen:</span><span class="sxs-lookup"><span data-stu-id="05532-107">We have hello following toohelp you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="05532-108">Architectuur infographics</span><span class="sxs-lookup"><span data-stu-id="05532-108">Architectural infographics</span></span>
* <span data-ttu-id="05532-109">Architecturale blauwdrukken</span><span class="sxs-lookup"><span data-stu-id="05532-109">Architectural blueprints</span></span>
* <span data-ttu-id="05532-110">Cloud en enterprise is ingesteld</span><span class="sxs-lookup"><span data-stu-id="05532-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="05532-111">3D-blauwdruk Visio-sjabloon</span><span class="sxs-lookup"><span data-stu-id="05532-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="05532-112">Architectuur infographics</span><span class="sxs-lookup"><span data-stu-id="05532-112">Architectural infographics</span></span>
<span data-ttu-id="05532-113">Microsoft publiceert verschillende architectuur gerelateerde posters/infographics.</span><span class="sxs-lookup"><span data-stu-id="05532-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="05532-114">Deze omvatten:</span><span class="sxs-lookup"><span data-stu-id="05532-114">They include:</span></span>

* [<span data-ttu-id="05532-115">Echte Cloud-toepassingen maken</span><span class="sxs-lookup"><span data-stu-id="05532-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="05532-116">Schalen met Cloudservices</span><span class="sxs-lookup"><span data-stu-id="05532-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="05532-117">Architecturale blauwdrukken</span><span class="sxs-lookup"><span data-stu-id="05532-117">Architectural blueprints</span></span>
<span data-ttu-id="05532-118">Publiceert Microsoft over een set op hoog niveau [bouwkundige blauwdrukken](http://aka.ms/azblueprints) die laat zien hoe toobuild specifieke typen van systemen die Microsoft-producten.</span><span class="sxs-lookup"><span data-stu-id="05532-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how toobuild specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="05532-119">Elke blauwdruk bevat a:</span><span class="sxs-lookup"><span data-stu-id="05532-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="05532-120">Platte 2D Visio 2003-bestand dat u kunt downloaden en wijzigen</span><span class="sxs-lookup"><span data-stu-id="05532-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="05532-121">Kleur van de 3D-perspectief PDF-bestand toointroduce Hallo blauwdruk tooless technische doelgroepen</span><span class="sxs-lookup"><span data-stu-id="05532-121">Colorful 3D perspective PDF file toointroduce hello blueprint tooless technical audiences</span></span>
* <span data-ttu-id="05532-122">Video die bij het Hallo 3D-versie helpt</span><span class="sxs-lookup"><span data-stu-id="05532-122">Video that walks through hello 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="05532-123">Cloud en enterprise is ingesteld</span><span class="sxs-lookup"><span data-stu-id="05532-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="05532-124">[Hallo Visio en symbolen training video bekijken](http://aka.ms/CnESymbolsVideo) en vervolgens [downloaden van de Cloud en Enterprise symbool set Hallo](http://aka.ms/CnESymbols) toohelp technische materialen beschrijven Azure, Windows Server, SQL Server en meer maken.</span><span class="sxs-lookup"><span data-stu-id="05532-124">[View hello Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download hello Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) toohelp create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="05532-125">U kunt Hallo symbolen in architectuur diagrammen, trainingsmateriaal presentaties, gegevensbladen, infographics, whitepapers en zelfs van derden books gebruiken als Hallo adresboek treinen toouse Microsoft-producten mensen.</span><span class="sxs-lookup"><span data-stu-id="05532-125">You can use hello symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if hello book trains people toouse Microsoft products.</span></span> <span data-ttu-id="05532-126">Ze zijn echter niet bedoeld voor gebruik in gebruikersinterfaces.</span><span class="sxs-lookup"><span data-stu-id="05532-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="05532-127">3D-blauwdruk Visio-sjabloon</span><span class="sxs-lookup"><span data-stu-id="05532-127">3D blueprint Visio template</span></span>
<span data-ttu-id="05532-128">3D-versies van Hallo Hallo [Microsoft architectuur blauwdrukken](http://aka.ms/azblueprints) in eerste instantie zijn gemaakt in een niet-Microsoft-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="05532-128">hello 3D versions of hello [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="05532-129">Een nieuwe Visio 2013 (en hoger) sjabloon verzonden op 5 augustus 2015 als onderdeel van een [Microsoft Architecture certificeringsinstantie loop gedistribueerd bij EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span><span class="sxs-lookup"><span data-stu-id="05532-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="05532-130">Hallo-sjabloon is ook beschikbaar buiten Hallo loop.</span><span class="sxs-lookup"><span data-stu-id="05532-130">hello template is also available outside hello course.</span></span>

* <span data-ttu-id="05532-131">[Bekijk Hallo training video](http://aka.ms/3dBlueprintTemplateVideo) eerste zodat u weet wat u ermee kunt doen</span><span class="sxs-lookup"><span data-stu-id="05532-131">[View hello training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="05532-132">Hallo downloaden [Microsoft Visio-sjabloon voor 3D-blauwdruk](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="05532-132">Download hello [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="05532-133">Hallo downloaden [Cloud en Enterprise symbolen](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse met Hallo 3D-sjabloon</span><span class="sxs-lookup"><span data-stu-id="05532-133">Download hello [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse with hello 3D template</span></span>
