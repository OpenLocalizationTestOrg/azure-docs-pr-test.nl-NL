---
title: aaaScale quota en limieten in uw lab in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe tooscale een lab in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a>Schaal quota en limieten in DevTest Labs
Als u in DevTest Labs werkt, kunt u wellicht opgevallen dat er zijn bepaalde limieten standaard toosome Azure-resources, die Hallo DevTest Labs service kunnen beïnvloeden. Deze limieten zijn waarnaar wordt verwezen tooas **quota**.

> [!NOTE]
> Hallo DevTest Labs service kan geen quota's niet opleggen. Quota's die u kunt tegenkomen zijn standaardbeperkingen Hallo algemene Azure-abonnement.

U kunt elke Azure-resource gebruiken totdat u het quotum bereikt. Elk abonnement heeft een afzonderlijke quota's en gebruik per abonnement wordt bijgehouden.

Elk abonnement heeft bijvoorbeeld een standaardquotum van 20 kernen. Dus als u virtuele machines in uw testomgeving met vier cores maakt, kunt klikt u vervolgens u alleen maken vijf virtuele machines. 

[Azure-abonnement en Servicelimieten](https://docs.microsoft.com/azure/azure-subscription-service-limits) vindt u enkele van de meest voorkomende quota Hallo voor Azure-resources. Hallo bronnen meestal gebruikt in een testomgeving en voor die u kunt tegenkomen quota, VM kernen, openbare IP-adressen, netwerkinterface, beheerde schijven, RBAC roltoewijzing en ExpressRoute-circuits bevatten.

## <a name="view-your-usage-and-quotas"></a>Uw gebruik en quota's weergeven
Deze stappen ziet u hoe de tooview Hallo huidige quota's in uw abonnement voor specifieke Azure-resources en toosee welk percentage van elke quota die u hebt gebruikt.

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecteer **meer Services**, en selecteer vervolgens **facturering** uit Hallo-lijst.
1. Selecteer in de blade facturering hello, een abonnement.
4. Selecteer **gebruik + quota**.

   ![Knop voor informatie over het gebruik en quota 's](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   Gebruik + quota Hallo blade wordt weergegeven, met verschillende bronnen beschikbaar zijn in het desbetreffende abonnement en Hallo percentage Hallo quota die per resource wordt gebruikt.

   ![Quota's en gebruik](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a>Aanvragen meer resources in uw abonnement
Als u een quotum-limiet bereikt, de standaardlimiet Hallo van een resource in een abonnement kan worden verhoogd van tooa maximumlimiet, zoals beschreven in [Azure-abonnement en Servicelimieten](https://docs.microsoft.com/azure/azure-subscription-service-limits).

Deze stappen ziet u hoe toorequest een quotum verhogen door Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecteer **meer Services**, selecteer **facturering**, en selecteer vervolgens **gebruik + quota**.
1. Selecteer in het Hallo gebruik + quota blade Hallo **aanvragen verhogen** knop.

   ![Knop voor toename van aanvragen](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. toocomplete en Hallo aanvraag indienen, vul Hallo vereist op alle drie tabbladen Hallo **nieuw ondersteuningsverzoek** formulier.

   ![Toename aanvraagformulier](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

[Wat Azure limieten en toeneemt](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) vindt u meer informatie over het contact opnemen met ondersteuning van Azure toorequest een quotum verhogen.



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Volgende stappen
* Hallo verkennen [DevTest Labs Azure Resource Manager QuickStart sjablonengalerie](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
