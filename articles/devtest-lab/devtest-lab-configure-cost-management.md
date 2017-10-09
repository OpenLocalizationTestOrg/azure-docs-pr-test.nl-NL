---
title: aaaView hello maandelijkse lab geschatte kosten trend in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hello Azure DevTest Labs maandelijkse geschatte kosten trend van grafiek.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a>Weergave Hallo maandelijkse lab geschatte kosten trend in Azure DevTest Labs
Hallo kostenbeheer functie van DevTest Labs kunt u bijhouden Hallo kosten van uw testomgeving. Dit artikel wordt beschreven hoe toouse hello **maandelijkse geschatte kosten Trend** grafiek tooview Hallo van het huidige kalendermaand geschatte kosten-to-date en de kosten van het verwachte einde van de maand voor Hallo Hallo huidige kalendermaand. In dit artikel leert u hoe tooview Hallo maandelijkse geschatte kosten trend grafiek in hello Azure-portal.

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a>Hallo maandelijkse geschatte kosten Trend grafiek weergeven
tooview hello maandelijkse geschatte kosten Trend grafiek, als volgt te werk: 

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
3. Selecteer de gewenste lab Hallo in lijst Hallo van labs.   
4. Selecteer op Hallo van labblade, **instellingen**.
5. Op de Hallo lab **instellingen** blade Selecteer **Lab kosten trend**.
6. Hallo toont volgende schermafbeelding een voorbeeld van een grafiek kosten. 
   
    ![Kosten grafiek](./media/devtest-lab-configure-cost-management/graph.png)

Hallo **geschatte kosten** waarde is van het huidige kalendermaand geschatte kosten-to-date Hallo. Hallo **geschatte kosten** hello geschatte kosten voor de hele Hallo huidige kalendermaand berekend met behulp van Hallo labkosten voor Hallo vorige vijf dagen.

Hallo-kosten zijn toohello dichtstbijzijnde gehele getal afgerond. Bijvoorbeeld: 

* 5.01 rondt af too6 naar boven 
* 5.50 rondt af too6 naar boven
* 5.99 rondt af too6 naar boven

Stelt boven Hallo diagram, u in de grafiek Hallo ziet Hallo-kosten zijn *geschatte* via [betalen naar gebruik](https://azure.microsoft.com/offers/ms-azr-0003p/) tarieven aanbieden.
Bovendien Hallo volgen *niet* opgenomen in Hallo kostenberekening:

* CSP en Dreamspark abonnementen worden momenteel niet ondersteund als Hallo maakt gebruik van Azure DevTest Labs [Azure facturering API's](../billing/billing-usage-rate-card-overview.md) toocalculate Hallo lab kosten, die geen ondersteuning biedt voor CSP of Dreamspark abonnementen.
* De tarieven van de aanbieding. Er zijn momenteel niet kunnen toouse de tarieven van de aanbieding (die wordt weergegeven onder uw abonnement) dat u hebt onderhandeld met Microsoft of Microsoft partners. We gebruiken de tarieven voor betalen per gebruik.
* Uw belastingen
* Uw kortingen
* Uw factureringsvaluta. Op dit moment wordt Hallo labkosten alleen weergegeven in valuta USD.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Verwante blogberichten
* [Twee meer dingen tookeep uw kosten op bijhouden in DevTest Labs](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [Waarom kosten drempelwaarden?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a>Volgende stappen
Hier volgen enkele dingen tootry vervolgens:

* [Labbeleidsregels definiëren](devtest-lab-set-lab-policy.md) -informatie over hoe tooset verschillende beleidsregels gebruikt Hallo toogovern hoe uw lab en bijbehorende virtuele machines worden gebruikt. 
* [Maken van aangepaste installatiekopie](devtest-lab-create-template.md) : wanneer u een virtuele machine, maakt u een basis, kan dit een aangepaste installatiekopie of een Marketplace-installatiekopie opgeven. In dit artikel ziet u hoe toocreate een aangepaste installatiekopie van een VHD-bestand.
* [Configureren van installatiekopieën van Marketplace](devtest-lab-configure-marketplace-images.md) - DevTest Labs ondersteunt het maken van virtuele machines op basis van Azure Marketplace-installatiekopieën. Dit artikel wordt beschreven hoe toospecify die, indien aanwezig, Azure Marketplace-installatiekopieën kunnen worden gebruikt bij het maken van virtuele machines in een testomgeving.
* [Een virtuele machine maken in een testomgeving](devtest-lab-add-vm-with-artifacts.md) -ziet u hoe een virtuele machine uit een basisinstallatiekopie toocreate (ofwel aangepaste of Marketplace), en hoe toowork met artefacten in uw virtuele machine.

