---
title: partneroplossingen aaaManaging in Azure Security Center | Microsoft Docs
description: "Dit document leert u hoe Azure Security Center u monitor in een oogopslag Hallo gezondheidsstatus van de partneroplossingen die zijn geïntegreerd met uw Azure-abonnement kunt."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a>Partneroplossingen bewaken met Azure Security Center
Dit document begeleidt u bij hoe toomonitor Hallo gezondheidsstatus van uw partneroplossingen in Azure Security Center.

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie. Dit document is niet een stapsgewijze handleiding.
>
>

## <a name="monitoring-partner-solutions"></a>Partneroplossingen bewaken
Hallo **partneroplossingen** tegel op Hallo **Security Center** blade kunt u controleren in een oogopslag Hallo gezondheidsstatus van de partneroplossingen die zijn geïntegreerd met uw Azure-abonnement.

![Tegel Partneroplossingen][1]

Hallo **partneroplossingen** tegel Hallo aantal partneroplossingen die zijn geïntegreerd met uw abonnement wordt weergegeven. Als er geen oplossingen geïntegreerd, geeft Hallo tegel Hallo cijfer nul.

tooview hello status van uw partneroplossingen:

1. Selecteer Hallo **partneroplossingen** tegel. Hallo **partneroplossingen** blade wordt geopend met een lijst van uw partneroplossingen verbonden tooSecurity Center.

   ![Partneroplossingen][3]

   Hallo-status van een partneroplossing kan zijn:

   * Beveiligd (groen): er is geen probleem met de status.
   * Niet in orde (rood): er is een probleem met de status waarvoor onmiddellijke aandacht is vereist.
   * Gestopte reporting (oranje): Hallo-oplossing is gestopt melden van de status.
   * Onbekende beveiligingsstatus (oranje): Hallo-status van het Hallo-oplossing is onbekend op dit moment vanwege tooa is mislukt-proces voor het toevoegen van een nieuwe resource toohello bestaande oplossing.
   * Niet gerapporteerd (grijs) - Hallo-oplossing heeft gerapporteerd iets nog een oplossing status is mogelijk omdat als deze onlangs verbonden is en nog steeds implementeert.

2. Selecteer een partneroplossing. In dit voorbeeld kunt u selecteren Hallo **Qualys** oplossing.  Er wordt een blade geopend met de gekoppelde resources Hallo status van de partneroplossing Hallo en Hallo-oplossing. Selecteer **oplossingenconsole** tooopen Hallo partner management ervaring voor deze oplossing.

   ![Details van partneroplossingen][4]
3. Ga terug toohello **Qualys** blade en selecteer **koppeling VM**. Hallo **toepassingen koppelen** blade wordt geopend. Hier kunt u resources toohello partneroplossing.

   ![Koppeling resources toopartner oplossing][5]

## <a name="next-steps"></a>Volgende stappen
In dit document zijn u geïntroduceerd toohello **partneroplossingen** -tegel in Security Center. toolearn meer informatie over Security Center, Zie Hallo artikelen te volgen:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) : meer informatie hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) : Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) : meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) : meer informatie hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) : Hallo nieuwste Azure-beveiliging nieuws en informatie.

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
