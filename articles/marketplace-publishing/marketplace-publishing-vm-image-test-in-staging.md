---
title: uw virtuele machine biedt voor Hallo Marketplace aaaTest | Microsoft Docs
description: Begrijpen hoe tootest uw virtuele machine voor beelden hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a>Testen van uw VM-aanbieding voor Azure Marketplace Hallo in fasering
Fasering betekent dat het implementeren van uw SKU in een particulier 'sandbox"waar u kunt testen en valideren van de functionaliteit ervan voordat u deze toohello Marketplace implementeert. Hallo SKU wordt weergegeven in de faseringsmodus net zoals tooa klant die is geïmplementeerd. Uw VM-installatiekopie moet toostaging gecertificeerde toobe gepusht.

## <a name="step-1-push-your-offer-toostaging"></a>Stap 1: Uw aanbieding toostaging Push
1. Op Hallo **publiceren** tabblad **tooStaging Push**.
   
    ![tekenen](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. Als Hallo Publishing Portal een melding van fouten, corrigeer deze.
3. In Hallo **wie toegang heeft tot uw voorbereide aanbieding?** dialoogvenster Voer Hallo lijst met Azure-abonnementen die u toopreview uw aanbieding in Hallo gebruikt [Azure preview-portal](https://portal.azure.com).
   
   > [!NOTE]
   > In geval van virtuele Machines en oplossingssjablonen, neem **niet** geaccepteerde abonnementen van het type Cryptografieprovider DreamSpark of Azure in Open.
   > 
   > 

    > In geval van virtuele Machines, als u op de knop Hallo **PUSH tooSTAGING**, Hallo stappen uit te voeren achter Hallo scene worden uitgevoerd. U zult kunnen tooview Hallo voortgang van elke stap Hallo publiceren tabblad in Hallo portal publiceren. U moet controleren op deze pagina op een vast interval (totdat het Hallo-status geeft tijdelijke) voor alle foutinformatie die nodig correctie van uw.

    > - In eerste instantie gaat uw staging aanvraag toohello certificeringsinstantie team dat Hallo vhd valideren. Echter, als uw aanvraag is alleen marketing wijzigen, klikt u vervolgens Hallo certificeringsinstantie stap overgeslagen.
    > - Zodra de Hallo certificeringsinstantie is voltooid, Hallo replicatie van Hallo aanbieding starten voor alle Azure-datacenters. In het algemeen neemt 24-48hours voor Hallo replicatie toocomplete maar tooa week, afhankelijk van de grootte op Hallo van Hallo vhd kan duren. Als uw aanvraag is alleen marketing wijzigen, klikt u vervolgens is Hallo-replicatie echter sneller.
    > - Wanneer het Hallo-replicatie is voltooid, klikt u vervolgens Hallo aanbieding is beschikbaar in Hallo [Azure-portal](http:/portal.azure.com). Op dat moment Hallo status worden voorbereid in Hallo portal publiceren. Een gefaseerde aanbieding is zichtbaar in Hallo [Azure-portal](http:/portal.azure.com) alleen met Hallo e id('s) welke Hello aanbieding gefaseerde Hallo-abonnement gekoppeld.

1. Meld u aan toohello [Azure preview-portal](https://portal.azure.com) met behulp van een hello Azure-abonnementen die worden vermeld in de vorige stap Hallo.
2. Zoek uw aanbieding en valideren van de VM-installatiekopie punten:
   
   * Zorg ervoor dat inhoud marketing correct in Hallo Marketplace weergegeven.
   * End-to-end-implementatie van Hallo VM-installatiekopie.
     
      ![IMG-kaart-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> Uw aanbieding blijft in de faseringsmodus totdat u Microsoft via Hallo Publishing Portal waarschuwen [**publiceren** tabblad > Klik op de knop Hallo **"Aanvragen goedkeuring tooPush tooProduction"**] dat u klaar toopush bent tooproduction. Dit is een ideale tijd toohave die alle leden van uw team via alles ter voorbereiding op uw aanbieding gaat van vermelde controleren.
> 
> Hallo staging-platform is ontworpen voor testen Hallo aanbieding in een preview-modus door Hallo uitgever. We voorkomen raden dat deze platofrm gebruiken voor commerciële doeleinden.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Nu uw aanbieding 'gefaseerde' en dat u de functionaliteit en marketing van inhoud hebt getest, kunt u doorgaan met de uiteindelijke publicatie toohello fase **stap 4**: [implementeren van uw aanbieding toohello Marketplace](marketplace-publishing-push-to-production.md).

## <a name="see-also"></a>Zie ook
* [Aan de slag: hoe toopublish een aanbieding toohello Azure Marketplace](marketplace-publishing-getting-started.md)

