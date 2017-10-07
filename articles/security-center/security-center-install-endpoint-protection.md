---
title: aaaInstall Endpoint Protection in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** installeren Endpoint Protection **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a>Endpoint Protection installeren in Azure Security Center
Azure Security Center raadt endpoint protection op uw virtuele Azure-machines (VM's) te installeren als endpoint protection nog niet is ingeschakeld. Deze aanbeveling is van toepassing tooWindows virtuele machines alleen.

> [!NOTE]
> Deze voorbeeldimplementatie maakt gebruik van Microsoft Antimalware. Zie [Partner-integratie in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) voor een lijst met partners die is geïntegreerd met Security Center.  
>
>

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.  Dit document is niet een stapsgewijze handleiding.
>
>

1. In Hallo **aanbevelingen** blade Selecteer **Endpoint Protection installeren**.
   ![Selecteer de Endpoint Protection installeren][1]
2. Hallo **Endpoint Protection installeren** blade wordt geopend met een lijst van virtuele machines zonder endpoint protection. Selecteer een van de Hallo lijst Hallo virtuele machines die u wilt tooinstall endpoint protection op en klik op **installeren op virtuele machines**.
   ![Selecteer VMs tooinstall Endpoint Protection op][2]
3. Hallo **Selecteer Endpoint Protection** wordt een blade geopend tooallow u tooselect Hallo oplossing voor eindpuntbeveiliging gewenste toouse. In dit voorbeeld gaan we selecteren **Microsoft Antimalware**.
   ![Selecteer de Endpoint Protection][3]
4. Meer informatie over de oplossing voor eindpuntbeveiliging hello wordt weergegeven. Selecteer **Maken**.
   ![Maken van anti-malwareoplossing][4]
5. Voer Hallo vereiste configuratie-instellingen op Hallo **Add Extension** blade en selecteer vervolgens **OK**. toolearn meer informatie over het Hallo-configuratie-instellingen, Zie [standaard en aangepaste Antimalware configuratie](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).

[Microsoft Antimalware](../security/azure-security-antimalware.md) is nu actief op Hallo VMs geselecteerd.

## <a name="see-also"></a>Zie ook
In dit artikel hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling "Endpoint Protection installeren." toolearn meer informatie over het inschakelen van Microsoft Antimalware in Azure, Zie Hallo document te volgen:

* [Microsoft Antimalware voor Cloudservices en virtuele Machines](../security/azure-security-antimalware.md) --meer informatie over hoe Microsoft Antimalware toodeploy.

toolearn meer informatie over Security Center, Zie Hallo documenten te volgen:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees blogberichten over Azure-beveiliging en naleving.

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
