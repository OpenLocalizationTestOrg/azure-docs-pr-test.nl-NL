---
title: aaaGuide toocreating een oplossingssjabloon voor Hallo Marketplace | Microsoft Docs
description: Gedetailleerde instructies waarmee toocreate, certificeren en implementeren van een Multi-VM-installatiekopie oplossingssjabloon voor de aankoop op Hallo Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="10496-103">Handleiding toocreate een oplossingssjabloon voor Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="10496-103">Guide toocreate a solution template for Azure Marketplace</span></span>
<span data-ttu-id="10496-104">Na het voltooien van stap 1, [accountaanmaking en registratie][link-acct-creation], wij u op het maken van een Azure-compatibele oplossingssjabloon op Hallo begeleide [technische vereisten voor het maken van een oplossingssjabloon](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="10496-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on hello creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="10496-105">Nu we u stapsgewijs door de stappen begeleidt voor het maken van de oplossingssjabloon van een voor meerdere virtuele machines op Hallo Hallo [Publishing Portal] [ link-pubportal] voor hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="10496-105">Now we will walk you through hello steps for creating a solution template for multiple VMs on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a><span data-ttu-id="10496-106">Maken van uw oplossing sjabloon aanbieding in Hallo Publishing Portal</span><span class="sxs-lookup"><span data-stu-id="10496-106">Create your solution template offer in hello Publishing Portal</span></span>
<span data-ttu-id="10496-107">Ga te [https://publish.windowsazure.com](http://publish.windowsazure.com). Als u zich aanmeldt voor de eerste keer toohello hello [Publishing Portal](https://publish.windowsazure.com/), gebruik Hallo dezelfde account met de verkoper-profiel van uw bedrijf is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="10496-107">Go too [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for hello first time toohello [Publishing Portal](https://publish.windowsazure.com/), use hello same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="10496-108">U kunt later een werknemer van uw bedrijf toevoegen als een co-beheerder in Hallo Publishing Portal.</span><span class="sxs-lookup"><span data-stu-id="10496-108">Later, you can add any employee of your company as a co-admin in hello Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="10496-109">1. Selecteer "Oplossingssjablonen"</span><span class="sxs-lookup"><span data-stu-id="10496-109">1. Select "Solution templates"</span></span>
  ![tekenen][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="10496-111">2. Maak een nieuwe oplossingssjabloon</span><span class="sxs-lookup"><span data-stu-id="10496-111">2. Create a new solution template</span></span>
  ![tekenen][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="10496-113">3. Beginnen met topologieën</span><span class="sxs-lookup"><span data-stu-id="10496-113">3. Start with topologies</span></span>
<span data-ttu-id="10496-114">Een oplossingssjabloon is een 'parent' tooall bijbehorende topologieën.</span><span class="sxs-lookup"><span data-stu-id="10496-114">A solution template is a "parent" tooall of its topologies.</span></span> <span data-ttu-id="10496-115">U kunt meerdere topologieën definiëren in één aanbieding/oplossingssjabloon.</span><span class="sxs-lookup"><span data-stu-id="10496-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="10496-116">Wanneer een aanbieding wordt doorgegeven toostaging, wordt deze doorgegeven met alle bijbehorende topologieën.</span><span class="sxs-lookup"><span data-stu-id="10496-116">When an offer is pushed toostaging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="10496-117">Ga als volgt uw aanbieding Hallo stappen hieronder toodefine:</span><span class="sxs-lookup"><span data-stu-id="10496-117">Follow hello steps below toodefine your offer:</span></span>     

* <span data-ttu-id="10496-118">Een topologie maakt: 'Id' is doorgaans Hallo-naam van Hallo-topologie voor Hallo oplossingssjabloon.</span><span class="sxs-lookup"><span data-stu-id="10496-118">Create a Topology: “Topology Identifier” is typically hello name of hello topology for hello solution template.</span></span> <span data-ttu-id="10496-119">Hallo-topologie-id wordt gebruikt in Hallo-URL, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="10496-119">hello topology identifier is used in hello URL as shown below:</span></span>

  <span data-ttu-id="10496-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/ {PublisherNamespace} / {OfferIdentifier} {TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="10496-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="10496-121">Azure-Portal: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="10496-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="10496-122">Voeg een nieuwe versie toe.</span><span class="sxs-lookup"><span data-stu-id="10496-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="10496-123">4. De versies van uw topologie gecertificeerd ophalen</span><span class="sxs-lookup"><span data-stu-id="10496-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="10496-124">Een zipbestand met alle vereiste bestanden tooprovision die bepaalde versie van de topologie Hallo uploaden.</span><span class="sxs-lookup"><span data-stu-id="10496-124">Upload a zip file that contains all required files tooprovision that particular version of hello topology.</span></span> <span data-ttu-id="10496-125">Dit zipbestand moet Hallo volgende bevatten:</span><span class="sxs-lookup"><span data-stu-id="10496-125">This zip file must contain hello following:</span></span>

* <span data-ttu-id="10496-126">*mainTemplate.json* en *createUiDefinition.json* -bestand in de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="10496-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="10496-127">Alle gekoppelde sjablonen en alle vereiste scripts.</span><span class="sxs-lookup"><span data-stu-id="10496-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="10496-128">Terwijl de ontwikkelaars werken op Hallo oplossing sjabloon topologieën maken en hen gecertificeerde Hallo bedrijven, marketing en/of juridische afdelingen van uw bedrijf op Hallo marketing- en juridische inhoud werken kunnen.</span><span class="sxs-lookup"><span data-stu-id="10496-128">While your developers work on creating hello solution template topologies and getting them certified, hello business, marketing, and/or legal departments of your company can work on hello marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="10496-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="10496-129">Next steps</span></span>
<span data-ttu-id="10496-130">Nu dat u uw oplossingssjabloon gemaakt en Hallo zip-bestand wordt geüpload, volg de instructies Hallo in Hallo [Marketplace marketing inhoud handleiding](marketplace-publishing-push-to-staging.md) voordat Hallo aanbieding toostaging worden gepusht.</span><span class="sxs-lookup"><span data-stu-id="10496-130">Now that you created your solution template and uploaded hello zip file, please follow hello instructions in hello [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing hello offer toostaging.</span></span> <span data-ttu-id="10496-131">toosee hello volledige set van marketplace publiceren artikelen, gaat u naar [aan de slag: hoe toopublish een aanbieding toohello Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="10496-131">toosee hello full set of marketplace publishing articles, visit [Getting started: How toopublish an offer toohello Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="10496-132">U is mogelijk ook geïnteresseerd in deze verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="10496-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="10496-133">VM-installatiekopieën: [over installatiekopieën van virtuele machines in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="10496-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="10496-134">VM-extensies: [VM-Agent en een overzicht van de VM-extensies](https://msdn.microsoft.com/library/azure/dn832621.aspx) en [Azure VM-extensies en functies](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="10496-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="10496-135">Azure Resource Manager: [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md) en [eenvoudige sjabloon voorbeelden](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="10496-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="10496-136">Storage-account beperkt: [hoe tooMonitor voor beperking van de Storage-Account](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) en [Premium-opslag](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="10496-136">Storage account throttles: [How tooMonitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
