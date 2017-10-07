---
title: aaaDeployment problemen voor veelgestelde vragen over Microsoft Azure Cloud Services | Microsoft Docs
description: Dit artikel worden Hallo Veelgestelde vragen over de implementatie voor Microsoft Azure Cloud Services.
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 8d67e36aa87fb5794d358e5cc235123ac7286028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemen bij de implementatie voor Azure Cloud Services: veelgestelde vragen (FAQ's)

Dit artikel bevat veelgestelde vragen over problemen bij de implementatie voor [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services). U kunt ook contact opnemen met Hallo [VM-grootte voor Cloud Services-pagina](cloud-services-sizes-specs.md) voor informatie over de grootte.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-does-deploying-a-cloud-service-toohello-staging-slot-sometimes-fail-with-a-resource-allocation-error-if-there-is-already-an-existing-deployment-in-hello-production-slot"></a>Waarom voor het implementeren van een cloud service toohello faseringssleuven soms niet met een resource toewijzingsfout als er al een bestaande implementatie in de productiesite Hallo?
Als een cloudservice een implementatie in een sleuf heeft, is Hallo volledige in de cloudservice vastgemaakt tooa specifieke cluster. Dit betekent dat als een implementatie al in de productiesite hello bestaat, een nieuwe implementatie van de test kan alleen worden toegewezen in hetzelfde cluster als productiesite Hallo Hallo.

Toewijzingsfouten optreden wanneer Hallo cluster waar uw cloudservice zich bevindt geen voldoende fysieke resources toosatisfy compute uw implementatieaanvraag.

Zie voor informatie over deze toewijzingsfouten beperkende [Service in de Cloud toewijzingsfout: oplossingen](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-scaling-up-or-scaling-out-a-cloud-service-deployment-sometimes-result-in-allocation-failure"></a>Waarom wordt omhoog schalen of buiten een cloud service-implementatie soms leiden tot toewijzingsfout schalen?
Wanneer u een cloudservice is geïmplementeerd, krijgt meestal specifieke cluster vastgemaakt tooa. Dit betekent dat het omhoog schalen/uit een bestaande cloud service nieuwe exemplaren in Hallo moet toewijzen hetzelfde cluster. Als Hallo cluster heeft capaciteit bijna of Hallo gewenste VM grootte/type is niet beschikbaar, Hallo verzoek mislukken.

Zie voor informatie over deze toewijzingsfouten beperkende [Service in de Cloud toewijzingsfout: oplossingen](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-deploying-a-cloud-service-into-an-affinity-group-sometimes-result-in-allocation-failure"></a>Waarom voor het implementeren van een cloudservice in een affiniteitsgroep is het soms resulteert in toewijzingsfout?
Een nieuwe implementatie tooan leeg cloudservice kan worden toegewezen door Hallo fabric in een cluster in deze regio, tenzij het Hallo-cloudservice is vastgemaakt tooan affiniteitsgroep. Implementaties toohello dezelfde affiniteitsgroep worden geprobeerd op Hallo hetzelfde cluster. Als het Hallo-cluster heeft capaciteit bijna bereikt, mislukken Hallo-aanvraag.

Zie voor informatie over deze toewijzingsfouten beperkende [Service in de Cloud toewijzingsfout: oplossingen](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-changing-vm-size-or-adding-a-new-vm-tooan-existing-cloud-service-sometimes-result-in-allocation-failure"></a>Waarom een nieuwe VM tooan bestaande cloudservice soms toevoegen of wijzigen van de VM-grootte resulteert in toewijzingsfout?
Hallo-clusters in een datacenter mogelijk verschillende configuraties van typen machines (bijvoorbeeld een reeks, Av2 reeks, D-reeks, Dv2 reeks, reeks G, H reeks, enzovoort). Maar niet alle Hallo clusters zou noodzakelijkerwijs Hallo allerlei virtuele machines. Bijvoorbeeld, als u een D-reeks VM tooa cloudservice dat al is geïmplementeerd in een reeks alleen-lezen cluster tooadd probeert, treden er al een geheugentoewijzing is mislukt. Dit wordt ook gebeuren als u probeert toochange VM SKU groottes (bijvoorbeeld overschakelen van een reeks van een reeks tooa D).

Zie voor informatie over deze toewijzingsfouten beperkende [Service in de Cloud toewijzingsfout: oplossingen](cloud-services-allocation-failures.md#solutions).

Zie beschikbaar toocheck Hallo grootte in uw regio [Microsoft Azure: producten die beschikbaar zijn in elke regio](https://azure.microsoft.com/regions/services).

## <a name="why-does-deploying-a-cloud-service-sometime-fail-due-toolimitsquotasconstraints-on-my-subscription-or-service"></a>Waarom het implementeren van een cloud voor service sometime mislukken vanwege toolimits/quota/beperkingen op mijn abonnement of de service?
Implementatie van een cloudservice kan mislukken als het Hallo-resources die vereist toobe toegewezen zijn Hallo standaard of maximumquotum toegestaan voor uw service op Hallo regio/datacenter niveau overschrijden. Zie voor meer informatie [Cloudservices beperkt](../azure-subscription-service-limits.md#cloud-services-limits).

U kan ook Hallo huidige/gebruiksquotum volgen voor uw abonnement op Hallo-portal: Azure Portal = > abonnementen = > \<betreffende abonnement > = > 'Gebruik + quotum'.

Gebruik/verbruik-gerelateerde resourcegegevens kan ook worden opgehaald via hello Azure Billing-API's. Zie [Azure-Resource gebruiks-API (Preview)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview).

## <a name="how-can-i-change-hello-size-of-a-deployed-cloud-service-vm-without-redeploying-it"></a>Hoe kan ik Hallo grootte van een geïmplementeerde cloudservice-VM wijzigen zonder dat dit?
U kunt Hallo VM-grootte van een geïmplementeerde cloudservice niet wijzigen zonder deze opnieuw distribueren. Hallo VM-grootte is ingebouwd in Hallo CSDEF die alleen kan worden bijgewerkt met een implementatie opnieuw uit.

Zie voor meer informatie [hoe tooupdate een cloudservice](cloud-services-update-azure-service.md).

 
