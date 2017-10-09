---
title: aaaAdd next generation firewall in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbevelingen ** toevoegen een volgende generatie Firewall ** en ** Route traffice via NGFW alleen **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a>Next Generation Firewall toevoegen in Azure Security Center
Azure Security Center kan aanbevelen dat u next generation firewall (NGFW) van een Microsoft-partner tooincrease uw beveiligingsinstellingen toevoegt. Dit document vindt u via een voorbeeld van hoe toodo dit.

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.  Dit is geen stapsgewijze handleiding.
>
>

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren
1. In Hallo **aanbevelingen** blade Selecteer **Next Generation Firewall toevoegen**.
   ![Een firewall van de volgende generatie toevoegen][1]
2. In Hallo **Next Generation Firewall toevoegen** blade, selecteert u een eindpunt.
   ![Selecteer een eindpunt][2]
3. Een tweede **Next Generation Firewall toevoegen** blade wordt geopend. U kunt toouse een bestaande oplossing als beschikbaar of u kunt een nieuwe maken. In dit voorbeeld zijn er geen bestaande oplossingen beschikbaar, dus we een NGFW maken.
   ![Next Generation Firewall maken][3]
4. een oplossing toocreate een NGFW selecteren in de lijst Hallo van geïntegreerde partners. In dit voorbeeld selecteren we **Check Point**.
   ![Selecteer Next Generation Firewall-oplossing][4]
5. Hallo **Check Point** blade wordt geopend zodat u informatie over Hallo partneroplossing. Selecteer **maken** Hallo informatie blade.
   ![Firewall-informatie-blade][5]
6. Hallo **virtuele machine maken** blade wordt geopend. Hier kunt u informatie vereist toospin een virtuele machine (VM) die wordt uitgevoerd Hallo NGFW. Hallo stappen en bieden Hallo NGFW informatie vereist. Selecteer OK tooapply.
   ![Virtuele machine toorun NGFW maken][6]

## <a name="route-traffic-through-ngfw-only"></a>Het verkeer alleen via de NGFW leiden
Retourneren van toohello **aanbevelingen** blade. Een nieuwe vermelding is gegenereerd nadat u een NGFW via Security Center, aangeroepen toegevoegd **routeren van verkeer via NGFW**. Deze aanbeveling wordt alleen gemaakt als u uw NGFW door Security Center geïnstalleerd. Als u internetgerichte eindpunten hebt, raadt Security Center Netwerkbeveiligingsgroep regels waarmee binnenkomend verkeer tooyour VM via uw NGFW forceren te configureren.

1. In Hallo **blade aanbevelingen**, selecteer **routeren van verkeer via NGFW**.
   ![Verkeer alleen via NGFW sturen][7]
2. Hiermee opent u de blade Hallo **routeren van verkeer via NGFW**, die een lijst met virtuele machines die u kunt het verkeer naar versturen. Selecteer een virtuele machine in Hallo-lijst.
   ![Selecteer een virtuele machine][8]
3. Een blade voor Hallo geselecteerd VM geopend waarin gerelateerde regels voor binnenkomende verbindingen. Een beschrijving biedt u meer informatie over het mogelijk de volgende stappen. Selecteer **binnenkomende regels bewerken** tooproceed met een inkomende regel bewerken. Hallo verwachting is dat **bron** is niet ingesteld te**eventuele** voor Hallo internetgerichte eindpunten die zijn gekoppeld aan Hallo NGFW. Zie toolearn meer informatie over het Hallo-eigenschappen van inkomende hello-regel [NSG-regels](../virtual-network/virtual-networks-nsg.md#nsg-rules).
   ![Configureer regels toolimit toegang][9]
   ![binnenkomende regel bewerken][10]

## <a name="see-also"></a>Zie ook
Dit document hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling "Toevoegen Next Generation Firewall." toolearn meer informatie over NGFWs en Hallo Check Point-partneroplossing Hallo ziet:

* [Next Generation Firewall](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [Check Point vSEC](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees blogberichten over Azure-beveiliging en naleving.

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
