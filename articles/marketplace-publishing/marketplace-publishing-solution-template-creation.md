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
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a>Handleiding toocreate een oplossingssjabloon voor Azure Marketplace
Na het voltooien van stap 1, [accountaanmaking en registratie][link-acct-creation], wij u op het maken van een Azure-compatibele oplossingssjabloon op Hallo begeleide [technische vereisten voor het maken van een oplossingssjabloon](marketplace-publishing-solution-template-creation-prerequisites.md). Nu we u stapsgewijs door de stappen begeleidt voor het maken van de oplossingssjabloon van een voor meerdere virtuele machines op Hallo Hallo [Publishing Portal] [ link-pubportal] voor hello Azure Marketplace.

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a>Maken van uw oplossing sjabloon aanbieding in Hallo Publishing Portal
Ga te [https://publish.windowsazure.com](http://publish.windowsazure.com). Als u zich aanmeldt voor de eerste keer toohello hello [Publishing Portal](https://publish.windowsazure.com/), gebruik Hallo dezelfde account met de verkoper-profiel van uw bedrijf is geregistreerd. U kunt later een werknemer van uw bedrijf toevoegen als een co-beheerder in Hallo Publishing Portal.

### <a name="1-select-solution-templates"></a>1. Selecteer "Oplossingssjablonen"
  ![tekenen][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a>2. Maak een nieuwe oplossingssjabloon
  ![tekenen][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a>3. Beginnen met topologieën
Een oplossingssjabloon is een 'parent' tooall bijbehorende topologieën. U kunt meerdere topologieën definiëren in één aanbieding/oplossingssjabloon. Wanneer een aanbieding wordt doorgegeven toostaging, wordt deze doorgegeven met alle bijbehorende topologieën. Ga als volgt uw aanbieding Hallo stappen hieronder toodefine:     

* Een topologie maakt: 'Id' is doorgaans Hallo-naam van Hallo-topologie voor Hallo oplossingssjabloon. Hallo-topologie-id wordt gebruikt in Hallo-URL, zoals hieronder wordt weergegeven:

  Azure Marketplace: http://azure.microsoft.com/marketplace/partners/ {PublisherNamespace} / {OfferIdentifier} {TopologyIdentifier}

  Azure-Portal: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {TopologyIdentifier}
* Voeg een nieuwe versie toe.

### <a name="4-get-your-topology-versions-certified"></a>4. De versies van uw topologie gecertificeerd ophalen
Een zipbestand met alle vereiste bestanden tooprovision die bepaalde versie van de topologie Hallo uploaden. Dit zipbestand moet Hallo volgende bevatten:

* *mainTemplate.json* en *createUiDefinition.json* -bestand in de hoofdmap.
* Alle gekoppelde sjablonen en alle vereiste scripts.

  > [!TIP]
  > Terwijl de ontwikkelaars werken op Hallo oplossing sjabloon topologieën maken en hen gecertificeerde Hallo bedrijven, marketing en/of juridische afdelingen van uw bedrijf op Hallo marketing- en juridische inhoud werken kunnen.
  >
  >

## <a name="next-steps"></a>Volgende stappen
Nu dat u uw oplossingssjabloon gemaakt en Hallo zip-bestand wordt geüpload, volg de instructies Hallo in Hallo [Marketplace marketing inhoud handleiding](marketplace-publishing-push-to-staging.md) voordat Hallo aanbieding toostaging worden gepusht. toosee hello volledige set van marketplace publiceren artikelen, gaat u naar [aan de slag: hoe toopublish een aanbieding toohello Azure Marketplace](marketplace-publishing-getting-started.md).

U is mogelijk ook geïnteresseerd in deze verwante artikelen:

* VM-installatiekopieën: [over installatiekopieën van virtuele machines in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)
* VM-extensies: [VM-Agent en een overzicht van de VM-extensies](https://msdn.microsoft.com/library/azure/dn832621.aspx) en [Azure VM-extensies en functies](https://msdn.microsoft.com/library/azure/dn606311.aspx)
* Azure Resource Manager: [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md) en [eenvoudige sjabloon voorbeelden](https://github.com/rjmax/ArmExamples)
* Storage-account beperkt: [hoe tooMonitor voor beperking van de Storage-Account](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) en [Premium-opslag](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
