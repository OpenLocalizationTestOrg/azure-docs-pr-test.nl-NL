---
title: aaaResolve endpoint protection-status meldingen in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** Endpoint Protection oplossen health waarschuwingen **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a>Endpoint protection-status meldingen in Azure Security Center oplossen
Azure Security Center wordt aanbevolen dat u gedetecteerde endpoint protection-statuswaarschuwingen oplossen.  Security Center kunt u welke virtuele machines (VM's) endpoint protection storingen en hoeveel hebt toosee.

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie. Dit is geen stapsgewijze handleiding.
> 
> 

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren
1. In Hallo **blade aanbevelingen**, selecteer **waarschuwingen voor Endpoint Protection oplossen health**.
   ![Statusmeldingen endpoint protection oplossen][1]
2. Hiermee opent u de blade Hallo **Endpoint Protection fout** die een lijst met virtuele machines met fouten en het aantal mislukte Hallo voor elke virtuele machine. Selecteer een virtuele machine in Hallo-lijst.
   ![Endpoint protection-fout][2]
3. Een **fouten lijst** blade wordt geopend voor Hallo virtuele machine geselecteerde, een lijst met fouten worden weergegeven. Selecteer een fout in Hallo lijst toolearn meer. Dit wordt een blade geopend met informatie over de fout Hallo geselecteerd.
   ![Lijst met fouten][3]
   ![foutgebeurtenis][4]

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
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
