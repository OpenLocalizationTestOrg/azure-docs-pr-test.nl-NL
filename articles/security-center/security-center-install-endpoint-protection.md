---
title: Endpoint Protection installeren in Azure Security Center | Microsoft Docs
description: Dit document ziet u hoe de aanbeveling Azure Security Center implementeren ** installeren Endpoint Protection **.
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
ms.openlocfilehash: efb86a0ae362c30a6772c391a499154b7ae2a697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a>Endpoint Protection installeren in Azure Security Center
Azure Security Center raadt endpoint protection op uw virtuele Azure-machines (VM's) te installeren als endpoint protection nog niet is ingeschakeld. Deze aanbeveling is alleen van toepassing op Windows-VM's.

> [!NOTE]
> Deze voorbeeldimplementatie maakt gebruik van Microsoft Antimalware. Zie [Partner-integratie in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) voor een lijst met partners die is geïntegreerd met Security Center.  
>
>

## <a name="implement-the-recommendation"></a>De aanbeveling implementeren

> [!NOTE]
> In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie.  Dit document is niet een stapsgewijze handleiding.
>
>

1. In de **aanbevelingen** blade Selecteer **Endpoint Protection installeren**.
   ![Selecteer de Endpoint Protection installeren][1]
2. De **Endpoint Protection installeren** blade wordt geopend met een lijst van virtuele machines zonder endpoint protection. Selecteer in de lijst van de virtuele machines die u wilt installeren van endpoint protection op en klik op **installeren op virtuele machines**.
   ![Selecteer de virtuele machines voor het installeren van Endpoint Protection op][2]
3. De **Selecteer Endpoint Protection** er wordt een blade geopend zodat u kunt selecteren van de endpoint protection-oplossing die u wilt gebruiken. In dit voorbeeld gaan we selecteren **Microsoft Antimalware**.
   ![Selecteer de Endpoint Protection][3]
4. Meer informatie over de oplossing voor eindpuntbeveiliging wordt weergegeven. Selecteer **Maken**.
   ![Maken van anti-malwareoplossing][4]
5. Voer de vereiste configuratie-instellingen op de **Add Extension** blade en selecteer vervolgens **OK**. Zie voor meer informatie over de configuratie-instellingen, [standaard en aangepaste Antimalware configuratie](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).

[Microsoft Antimalware](../security/azure-security-antimalware.md) is nu actief zijn op de geselecteerde virtuele machines.

## <a name="see-also"></a>Zie ook
In dit artikel hebt u geleerd hoe u implementeert de aanbeveling Security Center "Endpoint Protection installeren." Zie voor meer informatie over het inschakelen van Microsoft Antimalware in Azure, het volgende document:

* [Microsoft Antimalware voor Cloudservices en virtuele Machines](../security/azure-security-antimalware.md) --informatie over het implementeren van Microsoft Antimalware.

Zie de volgende documenten voor meer informatie over Security Center:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --informatie over het configureren van beveiligingsbeleid.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --informatie over het bewaken van de status van uw Azure-resources.
* [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) (Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center): ontdek hoe u beveiligingswaarschuwingen kunt beheren en erop kunt reageren.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md): leer hoe u de integriteitsstatus van uw partneroplossingen kunt bewaken.
* [Azure Security Center FAQ](security-center-faq.md) (Veelgestelde vragen over Azure Security Center): raadpleeg veelgestelde vragen over het gebruik van de service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees blogberichten over Azure-beveiliging en naleving.

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
