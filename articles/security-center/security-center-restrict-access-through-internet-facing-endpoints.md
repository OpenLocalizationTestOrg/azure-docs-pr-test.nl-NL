---
title: aaaRestrict toegang via internetgerichte eindpunten in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** toegang via Internetgericht eindpunt ** beperken.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a>Beperken van toegang via internetgerichte eindpunten in Azure Security Center
Azure Security Center wordt aanbevolen dat u de toegang via internetgerichte eindpunten beperken als een van uw Netwerkbeveiligingsgroepen (nsg's) heeft een of meer regels voor binnenkomende verbindingen die toegankelijk is vanaf 'alle' IP-bronadressen. Openstellen te 'any' mogelijkheid aanvallers tooaccess uw resources. Security Center beveelt aan dat u deze regels voor binnenkomende verbindingen toorestrict toegang toosource IP-adressen die daadwerkelijk toegang nodig bewerken.

Deze aanbeveling is voor elke niet--poort dat 'een' als bron gegenereerd.

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie. Dit is geen stapsgewijze handleiding.
>
>

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren
1. In Hallo **blade aanbevelingen**, selecteer **beperken van toegang via Internetgericht eindpunt**.

   ![Toegang via een internetgericht eindpunt beperken][1]
2. Hiermee opent u de blade Hallo **beperken van toegang via Internetgericht eindpunt**. Deze blade bevat Hallo virtuele machines (VM's) met regels voor binnenkomende verbindingen die een mogelijk beveiligingsprobleem te maken. Selecteer een virtuele machine.

   ![Selecteer een virtuele machine][2]
3. Hallo **NSG** blade Netwerkbeveiligingsgroep wordt informatie weergegeven, gerelateerde binnenkomende regels en Hallo VM gekoppeld. Selecteer **binnenkomende regels bewerken** tooproceed met een inkomende regel bewerken.

   ![Netwerkbeveiligingsgroep-blade][3]
4. Op Hallo **inkomende beveiligingsregels** blade Selecteer Hallo binnenkomende regel tooedit. In dit voorbeeld gaan we selecteren **AllowWeb**.

   ![Inkomende beveiligingsregels][4]

   Opmerking: u kunt ook selecteren **regels standaard** toosee Hallo set met standaardregels die zijn opgenomen in alle nsg's. Hallo-standaardregels kunnen niet worden verwijderd, maar omdat ze een lagere prioriteit worden toegewezen, kunnen ze worden overschreven door het Hallo-regels die u maakt. Meer informatie over [regels standaard](../virtual-network/virtual-networks-nsg.md#default-rules).

   ![Standaardregels][5]
5. Op Hallo **AllowWeb** blade Hallo-eigenschappen bewerken van Hallo binnenkomende regel zodat die Hallo **bron** is een IP-adres of een blok IP-adressen. Zie toolearn meer informatie over het Hallo-eigenschappen van inkomende hello-regel [NSG-regels](../virtual-network/virtual-networks-nsg.md#nsg-rules).

   ![Regel voor binnenkomende bewerken][6]

## <a name="see-also"></a>Zie ook
In dit artikel hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling 'toegang beperken tot en met een Internetgericht eindpunt." toolearn meer informatie over het inschakelen van regels, en nsg's ziet Hallo:

* [Wat is een netwerkbeveiligingsgroep (NSG)?](../virtual-network/virtual-networks-nsg.md)
* [Hoe toomanage nsg's met behulp van Azure-portal Hallo](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md)--meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md): leer hoe aanbevelingen u helpen uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md)--meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md)--meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md)--Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/)--Hallo nieuwste Azure-beveiliging nieuws en informatie.

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
