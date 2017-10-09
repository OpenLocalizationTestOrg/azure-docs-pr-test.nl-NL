---
title: aaaEnable Netwerkbeveiligingsgroepen in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** inschakelen netwerk beveiliging groepen **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a>Inschakelen van Netwerkbeveiligingsgroepen in Azure Security Center
Azure Security Center raadt aan dat u een netwerkbeveiligingsgroep (NSG) inschakelen als een nog niet is ingeschakeld. Nsg's bevatten een lijst met regels voor lijst ACL (Access Control) toestaan of weigeren netwerkverkeer tooyour VM-exemplaren in een virtueel netwerk. NSG's kunnen worden gekoppeld aan subnetten of afzonderlijke VM-exemplaren in dat subnet. Wanneer een NSG gekoppeld aan een subnet is, toepassing hello ACL-regels tooall Hallo VM-exemplaren in dat subnet. Bovendien verkeer tooan afzonderlijke VM kan worden beperkt door een NSG koppelen verdere rechtstreeks toothat VM. toolearn Zie meer [wat is er een Netwerkbeveiligingsgroep (NSG)?](../virtual-network/virtual-networks-nsg.md)

Als u geen nsg's is ingeschakeld, Security Center geeft twee aanbevelingen tooyou: schakelen van Netwerkbeveiligingsgroepen op subnetten en inschakelen van Netwerkbeveiligingsgroepen op virtuele machines. U kiezen welke niveau, subnet of virtuele machine, tooapply nsg's.

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.  Dit is geen stapsgewijze handleiding.
>
>

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren
1. In Hallo **aanbevelingen** blade Selecteer **Netwerkbeveiligingsgroepen inschakelen** op subnetten of op virtuele machines.
   ![Netwerkbeveiligingsgroepen inschakelen][1]
2. Hiermee opent u de blade Hallo **ontbrekende Netwerkbeveiligingsgroepen configureren** voor subnetten of voor virtuele machines, afhankelijk van het Hallo-aanbeveling die u hebt geselecteerd. Selecteer een subnet of een virtuele machine tooconfigure een NSG op.

   ![NSG voor subnet configureren][2]

   ![NSG voor de virtuele machine configureren][3]
3. Op Hallo **netwerkbeveiligingsgroep kiezen** blade, selecteer een bestaande NSG of **nieuw** toocreate een NSG.

   ![Netwerkbeveiligingsgroep kiezen][4]

Als u een NSG maakt, stappen Hallo in [hoe toomanage nsg's met behulp van Azure-portal Hallo](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate een NSG en stel de beveiligingsregels voor verbindingen.

## <a name="see-also"></a>Zie ook
In dit artikel hebt u gezien hoe tooimplement Hallo Security Center aanbeveling "inschakelen Netwerkbeveiligingsgroepen' voor subnetten of virtuele machines. toolearn meer informatie over het inschakelen van NSGs, Zie de volgende Hallo:

* [Wat is een netwerkbeveiligingsgroep (NSG)?](../virtual-network/virtual-networks-nsg.md)
* [Hoe toomanage nsg's met behulp van Azure-portal Hallo](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Hallo nieuwste Azure-beveiliging nieuws en informatie.

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
