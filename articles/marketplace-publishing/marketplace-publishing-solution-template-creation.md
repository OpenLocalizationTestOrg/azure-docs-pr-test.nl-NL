---
title: Handleiding voor het maken van een oplossingssjabloon voor de Marketplace | Microsoft Docs
description: Gedetailleerde instructies voor het maken, certificeren en implementeren van een oplossingssjabloon Multi-VM-installatiekopie voor aanschaffen op Azure Marketplace.
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
ms.openlocfilehash: b753bfb4bd69bd9aacf4eebd8999397394c28bc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="guide-to-create-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="6e92a-103">Handleiding voor het maken van een oplossingssjabloon voor Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6e92a-103">Guide to create a solution template for Azure Marketplace</span></span>
<span data-ttu-id="6e92a-104">Na het voltooien van stap 1, [accountaanmaking en registratie][link-acct-creation], wij u op het maken van een Azure-compatibele oplossingssjabloon op begeleide [technische vereisten voor het maken van een oplossingssjabloon](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="6e92a-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on the creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="6e92a-105">Nu we u stapsgewijs door de stappen begeleidt voor het maken van een oplossingssjabloon voor meerdere virtuele machines op de [Publishing Portal] [ link-pubportal] voor Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6e92a-105">Now we will walk you through the steps for creating a solution template for multiple VMs on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-the-publishing-portal"></a><span data-ttu-id="6e92a-106">Maken van uw oplossing sjabloon aanbieding in de Portal publiceren</span><span class="sxs-lookup"><span data-stu-id="6e92a-106">Create your solution template offer in the Publishing Portal</span></span>
<span data-ttu-id="6e92a-107">Ga naar [https://publish.windowsazure.com](http://publish.windowsazure.com). Als u zich aanmeldt voor het eerst naar de [Publishing Portal](https://publish.windowsazure.com/), gebruik hetzelfde account gebruiken met de verkoper-profiel van uw bedrijf is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="6e92a-107">Go to  [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for the first time to the [Publishing Portal](https://publish.windowsazure.com/), use the same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="6e92a-108">Later kunt u alle werknemers van uw bedrijf toevoegen als een co-beheerder in de Portal voor publiceren.</span><span class="sxs-lookup"><span data-stu-id="6e92a-108">Later, you can add any employee of your company as a co-admin in the Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="6e92a-109">1. Selecteer "Oplossingssjablonen"</span><span class="sxs-lookup"><span data-stu-id="6e92a-109">1. Select "Solution templates"</span></span>
  ![tekenen][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="6e92a-111">2. Maak een nieuwe oplossingssjabloon</span><span class="sxs-lookup"><span data-stu-id="6e92a-111">2. Create a new solution template</span></span>
  ![tekenen][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="6e92a-113">3. Beginnen met topologieën</span><span class="sxs-lookup"><span data-stu-id="6e92a-113">3. Start with topologies</span></span>
<span data-ttu-id="6e92a-114">Een oplossingssjabloon is een bovenliggende topologie voor alle bijbehorende topologieën.</span><span class="sxs-lookup"><span data-stu-id="6e92a-114">A solution template is a "parent" to all of its topologies.</span></span> <span data-ttu-id="6e92a-115">U kunt meerdere topologieën definiëren in één aanbieding/oplossingssjabloon.</span><span class="sxs-lookup"><span data-stu-id="6e92a-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="6e92a-116">Wanneer een aanbieding wordt doorgegeven voor fasering, wordt deze doorgegeven met alle bijbehorende topologieën.</span><span class="sxs-lookup"><span data-stu-id="6e92a-116">When an offer is pushed to staging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="6e92a-117">Volg onderstaande stappen voor het definiëren van uw aanbieding:</span><span class="sxs-lookup"><span data-stu-id="6e92a-117">Follow the steps below to define your offer:</span></span>     

* <span data-ttu-id="6e92a-118">Een topologie maakt: "Topologie id" is doorgaans de naam van de topologie voor de oplossingssjabloon.</span><span class="sxs-lookup"><span data-stu-id="6e92a-118">Create a Topology: “Topology Identifier” is typically the name of the topology for the solution template.</span></span> <span data-ttu-id="6e92a-119">De topologie-id wordt gebruikt in de URL, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="6e92a-119">The topology identifier is used in the URL as shown below:</span></span>

  <span data-ttu-id="6e92a-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/ {PublisherNamespace} / {OfferIdentifier} {TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="6e92a-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="6e92a-121">Azure-Portal: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="6e92a-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="6e92a-122">Voeg een nieuwe versie toe.</span><span class="sxs-lookup"><span data-stu-id="6e92a-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="6e92a-123">4. De versies van uw topologie gecertificeerd ophalen</span><span class="sxs-lookup"><span data-stu-id="6e92a-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="6e92a-124">Upload een zipbestand dat alle vereiste bestanden voor het inrichten van die bepaalde versie van de topologie bevat.</span><span class="sxs-lookup"><span data-stu-id="6e92a-124">Upload a zip file that contains all required files to provision that particular version of the topology.</span></span> <span data-ttu-id="6e92a-125">Dit zipbestand moet bevatten het volgende:</span><span class="sxs-lookup"><span data-stu-id="6e92a-125">This zip file must contain the following:</span></span>

* <span data-ttu-id="6e92a-126">*mainTemplate.json* en *createUiDefinition.json* -bestand in de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="6e92a-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="6e92a-127">Alle gekoppelde sjablonen en alle vereiste scripts.</span><span class="sxs-lookup"><span data-stu-id="6e92a-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="6e92a-128">Terwijl de ontwikkelaars werkt over het maken van de oplossing sjabloon topologieën en hen gecertificeerd, het bedrijf zijn, kunnen de inhoud marketing- en juridische marketing en/of juridische afdelingen van uw bedrijf werken.</span><span class="sxs-lookup"><span data-stu-id="6e92a-128">While your developers work on creating the solution template topologies and getting them certified, the business, marketing, and/or legal departments of your company can work on the marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="6e92a-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e92a-129">Next steps</span></span>
<span data-ttu-id="6e92a-130">Nu u uw oplossingssjabloon gemaakt en dat het zip-bestand wordt geüpload, volg de instructies in de [Marketplace marketing inhoud handleiding](marketplace-publishing-push-to-staging.md) voordat u de aanbieding voor fasering.</span><span class="sxs-lookup"><span data-stu-id="6e92a-130">Now that you created your solution template and uploaded the zip file, please follow the instructions in the [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing the offer to staging.</span></span> <span data-ttu-id="6e92a-131">De volledige set van marketplace artikelen publiceren, Ga naar [aan de slag: hoe een aanbieding publiceren in Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6e92a-131">To see the full set of marketplace publishing articles, visit [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="6e92a-132">U is mogelijk ook geïnteresseerd in deze verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="6e92a-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="6e92a-133">VM-installatiekopieën: [over installatiekopieën van virtuele machines in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="6e92a-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="6e92a-134">VM-extensies: [VM-Agent en een overzicht van de VM-extensies](https://msdn.microsoft.com/library/azure/dn832621.aspx) en [Azure VM-extensies en functies](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="6e92a-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="6e92a-135">Azure Resource Manager: [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md) en [eenvoudige sjabloon voorbeelden](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="6e92a-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="6e92a-136">Storage-account beperkt: [bewaken voor beperking van de Storage-Account](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) en [Premium-opslag](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="6e92a-136">Storage account throttles: [How to Monitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
