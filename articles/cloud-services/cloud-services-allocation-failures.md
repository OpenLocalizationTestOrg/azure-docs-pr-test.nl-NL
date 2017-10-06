---
title: aaaTroubleshooting Cloud toewijzingsfout bij | Microsoft Docs
description: Toewijzingsfouten oplossen die zijn opgetreden bij het implementeren van Cloud Services in Azure
services: azure-service-management, cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 529157eb-e4a1-4388-aa2b-09e8b923af74
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: dfd5cc4663ccc6ed1b27ca9df579182737363b0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-allocation-failure-when-you-deploy-cloud-services-in-azure"></a>Toewijzingsfouten oplossen die zijn opgetreden bij het implementeren van Cloud Services in Azure
## <a name="summary"></a>Samenvatting
Als u exemplaren tooa Cloudservice implementeren of nieuwe web- of worker-rolexemplaren toevoegen, wijst Microsoft Azure compute-bronnen. Tijd tot tijd krijgt u fouten bij het uitvoeren van deze bewerkingen zelfs voordat u hello Azure-abonnement limieten bereiken. In dit artikel wordt uitgelegd Hallo oorzaken van een aantal algemene toewijzingsfouten Hallo en mogelijke herstel wordt voorgesteld. Hallo-informatie is mogelijk ook handig wanneer u van plan Hallo-implementatie van uw services bent.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

### <a name="background--how-allocation-works"></a>Achtergrond – de werking van toewijzing
Hallo-servers in Azure-datacenters worden in clusters gepartitioneerd. Een nieuwe toewijzingsaanvraag voor cloud-service wordt uitgevoerd in meerdere clusters. Wanneer de eerste instantie Hallo geïmplementeerde tooa cloudservice (in fasering of productie), die de cloudservice is vastgemaakt tooa cluster opgehaald. Verdere implementaties voor Hallo cloudservice in Hallo hetzelfde gebeurt cluster. In dit artikel verwijzen we toothis als 'vastgemaakt tooa cluster'. Afbeelding 1 hieronder ziet u Hallo geval van een normale toewijzing die wordt uitgevoerd in meerdere clusters; Diagram 2 ziet u Hallo geval van een toewijzing die vastgemaakt tooCluster 2 omdat die is waar Hallo bestaande CS_1 voor Cloud-Service wordt gehost.

![Diagram van toewijzing](./media/cloud-services-allocation-failure/Allocation1.png)

### <a name="why-allocation-failure-happens"></a>Waarom toewijzingsfout gebeurt
Wanneer een aanvraag voor geheugentoewijzing vastgemaakt tooa cluster is, is er een hogere kans van resources vrij voor toofind mislukken omdat Hallo beschikbaar resourcegroep beperkt tooa cluster. Bovendien, als uw aanvraag voor geheugentoewijzing vastgemaakt tooa cluster is maar Hallo type resource dat u hebt aangevraagd wordt niet ondersteund door dit cluster, uw aanvraag mislukt zelfs als Hallo cluster gratis resource heeft. Diagram 3 hieronder ziet u Hallo geval waarbij een vastgezette toewijzing mislukt, omdat Hallo alleen candidate cluster geen gratis resources heeft. Diagram 4 wordt Hallo geval waarbij een vastgezette toewijzing mislukt, omdat Hallo alleen candidate cluster biedt geen ondersteuning voor Hallo aangevraagde VM-grootte, hoewel Hallo cluster resources vrij heeft.

![Vastgemaakte geheugentoewijzing is mislukt](./media/cloud-services-allocation-failure/Allocation2.png)

## <a name="troubleshooting-allocation-failure-for-cloud-services"></a>Toewijzingsfouten voor cloudservices oplossen
### <a name="error-message"></a>Foutbericht
Hallo volgende foutbericht weergegeven:

    "Azure operation '{operation id}' failed with code Compute.ConstrainedAllocationFailed. Details: Allocation failed; unable toosatisfy constraints in request. hello requested new service deployment is bound tooan Affinity Group, or it targets a Virtual Network, or there is an existing deployment under this hosted service. Any of these conditions constrains hello new deployment toospecific Azure resources. Please retry later or try reducing hello VM size or number of role instances. Alternatively, if possible, remove hello aforementioned constraints or try deploying tooa different region."

### <a name="common-issues"></a>Algemene problemen
Hier volgen Hallo algemene toewijzing scenario's die ertoe leiden een toewijzing aanvraag toobe vastgemaakt tooa één cluster dat.

* TooStaging sleuf - implementeren als een cloudservice een implementatie in een sleuf heeft, vervolgens Hallo volledige in de cloud-service is vastgemaakt tooa specifieke cluster.  Dit betekent dat als een implementatie al in de productiesite hello bestaat, vervolgens een nieuwe implementatie van de test kan alleen worden toegewezen in hetzelfde cluster als productiesite Hallo Hallo. Als het Hallo-cluster heeft capaciteit bijna bereikt, mislukken Hallo-aanvraag.
* Schalen: het toevoegen van nieuwe exemplaren tooan bestaande cloudservice moet toewijzen in Hallo hetzelfde cluster.  Kleine schaal aanvragen kan doorgaans worden verdeeld, maar niet altijd. Als het Hallo-cluster heeft capaciteit bijna bereikt, mislukken Hallo-aanvraag.
* Affiniteitsgroep - een nieuwe implementatie tooan leeg cloudservice kan worden toegewezen door Hallo fabric in een cluster in deze regio, tenzij het Hallo-cloudservice is vastgemaakt tooan affiniteitsgroep. Implementaties toohello dezelfde affiniteitsgroep worden geprobeerd op Hallo hetzelfde cluster. Als het Hallo-cluster heeft capaciteit bijna bereikt, mislukken Hallo-aanvraag.
* Affiniteitsgroep vNet - oudere virtuele netwerken zijn gebonden tooaffinity groepen in plaats van de regio's en cloudservices in deze virtuele netwerken is vastgemaakt toohello affiniteitsgroep cluster. Implementaties toothis type virtueel netwerk wordt een poging op Hallo vastgemaakt cluster. Als het Hallo-cluster heeft capaciteit bijna bereikt, mislukken Hallo-aanvraag.

## <a name="solutions"></a>Oplossingen
1. In dat geval tooa nieuwe cloudservice - deze oplossing is waarschijnlijk toobe meest succesvolle als Hallo platform toochoose van alle clusters in deze regio kunt.

   * Hallo werkbelasting tooa nieuwe cloudservice implementeren  
   * Hallo CNAME of A record toopoint verkeer toohello nieuwe cloudservice bijwerken
   * Zodra nul verkeer de oude site toohello gaat, kunt u de oude cloudservice Hallo verwijderen. Deze oplossing moet rekening worden gebracht zonder uitvaltijd.
2. Verwijderen van de productie- en staging-sleuven: deze oplossing uw bestaande DNS-naam blijft behouden, maar zal leiden tot uitvaltijd tooyour toepassing.

   * Hallo productie- en staging-sleuven van een bestaande cloudservice zodat Hallo-cloudservice leeg is, verwijderen en vervolgens
   * Maak een nieuwe implementatie in een bestaande cloudservice Hallo. Dit wordt opnieuw geprobeerd tooallocation in alle clusters in Hallo regio. Zorg ervoor dat Hallo cloud-service is niet gebonden tooan affiniteitsgroep.
3. Gereserveerd IP - behoudt deze oplossing voor uw bestaande IP-adres, maar zal leiden tot uitvaltijd tooyour toepassing.  

   * Maken van een ReservedIP voor uw bestaande implementatie met behulp van Powershell

     ```
     New-AzureReservedIP -ReservedIPName {new reserved IP name} -Location {location} -ServiceName {existing service name}
     ```
   * Ga als volgt #2 hierboven, waardoor ervoor toospecify Hallo nieuwe ReservedIP in CSCFG Hallo-service.
4. Verwijder affiniteitsgroep voor nieuwe implementaties - Affiniteitsgroepen niet langer worden aanbevolen. Volg de stappen voor #1 hierboven toodeploy een nieuwe cloudservice. Zorg ervoor dat cloudservice is niet in een affiniteitsgroep.
5. Converteren van tooa regionaal virtueel netwerk - Zie [hoe toomigrate van Affiniteitsgroepen tooa regionaal virtueel netwerk (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
