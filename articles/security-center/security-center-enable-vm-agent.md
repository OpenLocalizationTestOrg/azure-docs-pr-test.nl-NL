---
title: aaaEnable VM-Agent in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** inschakelen VM Agent **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a>VM-Agent in Azure Security Center inschakelen
Hallo VM-Agent moet worden geïnstalleerd op virtuele machines (VM's) in de volgorde te[gegevensverzameling inschakelen](security-center-enable-data-collection.md).  Hiermee schakelt u Azure Security Center u toosee waarvoor VMs Hallo VM-Agent en wordt u het beste inschakelen Hallo VM-Agent op deze virtuele machines.

Hallo VM-Agent wordt standaard geïnstalleerd voor virtuele machines die vanuit Azure Marketplace Hallo worden geïmplementeerd. Hallo artikel [VM-Agent en -extensies – deel 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) bevat informatie over hoe tooinstall Hallo VM-Agent.

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie. Dit is geen stapsgewijze handleiding.
>
>

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren
1. In Hallo **blade aanbevelingen**, selecteer **VM-Agent inschakelen**.
   ![VM-agent inschakelen][1]
2. Hiermee opent u de blade Hallo **VM-Agent ontbreekt of niet reageert**. Deze blade bevat Hallo virtuele machines waarvoor Hallo VM-Agent. Hallo instructies op Hallo blade tooinstall Hallo VM-agent.
   ![VM-Agent ontbreekt.][2]

## <a name="see-also"></a>Zie ook
toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md)--meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md): leer hoe aanbevelingen u helpen uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md)--meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md)--meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md)--Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/)--Hallo nieuwste Azure-beveiliging nieuws en informatie.

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
