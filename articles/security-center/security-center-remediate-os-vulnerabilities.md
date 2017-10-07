---
title: aaaRemediate OS beveiligingslekken in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** herstellen OS beveiligingslekken **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a>OS-beveiligingslekken in Azure Security Center oplossen
Azure Security Center analyseert dagelijks uw virtuele machine (VM)-besturingssysteem (OS) voor configuraties die kunnen Hallo VM kwetsbaarder tooattack en raadt configuratiewijzigingen tooaddress beveiligingslekken. Security Center adviseert u beveiligingsproblemen oplossen wanneer de configuratie van het besturingssysteem van de VM komt niet overeen met de Hallo configuratieregels aanbevolen.

> [!NOTE]
> Zie voor meer informatie over Hallo specifieke configuraties die worden bewaakt Hallo [lijst met regels van de aanbevolen configuratie](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
>
>

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.  Dit document is niet een stapsgewijze handleiding.
>
>

1. In Hallo **aanbevelingen** blade Selecteer **herstellen OS beveiligingslekken**.
   ![Beveiligingsproblemen met het besturingssysteem herstellen][1]

    Hallo **herstellen OS beveiligingslekken** blade wordt geopend en een lijst met uw virtuele machines met besturingssysteemconfiguraties die niet overeenkomen met de Hallo configuratieregels aanbevolen.  Voor elke VM identificeert Hallo blade:

   * **REGELS voor MISLUKTE** --Hallo aantal regels dat Hallo configuratie van het besturingssysteem van de virtuele machine is mislukt.
   * **TIJD van laatste SCAN** --Hallo datum en tijd dat Security Center voor het laatst gescand configuratie van het besturingssysteem Hallo van de virtuele machine.
   * **STATUS** --Hallo van de huidige status van Hallo beveiligingslek:

     * Open: Hallo beveiligingslek is nog niet opgelost
     * Bezig: Hallo beveiligingslek momenteel wordt toegepast, door u is geen actie vereist.
     * Opgelost: Hallo beveiligingslek is al opgenomen (wanneer het Hallo-probleem is opgelost, Hallo vermelding is lichter gekleurd weergegeven)
   * **ERNST** --alle zwakke plekken zijn ingesteld van tooa ernst van de laag, wat betekent dat een beveiligingsprobleem moet worden opgelost, maar geen onmiddellijke aandacht vereist.

2. Selecteer een virtuele machine. Een blade voor die VM wordt geopend en geeft weer Hallo-regels die zijn mislukt.
   ![Van configuratieregels die zijn mislukt][2]

3. Selecteer een regel. In dit voorbeeld kunt selecteren **wachtwoorden moeten voldoen aan de complexiteitsvereisten**. Er wordt een blade geopend met een beschrijving regel en Hallo impact van Hallo is mislukt. Bekijk de details van Hallo en houd rekening met hoe besturingssysteemconfiguraties worden toegepast.
  ![Beschrijving voor Hallo is mislukt voor regel][3]

  Security Center gebruikt Common Configuration Enumeration (CCE) tooassign unieke id's voor van configuratieregels. Hallo volgende informatie is beschikbaar op deze blade:

  - --Naam van regel
  - ERNST--Waarde voor CCE ernst van kritieke, belangrijk of waarschuwingsstatus
  - CCIED--CCE unieke id voor de regel Hallo
  - Beschrijving: Beschrijving van regel
  - BEVEILIGINGSLEK--Uitleg van beveiligingslek of het risico als de regel wordt niet toegepast
  - IMPACT--Zakelijke impact als regel wordt toegepast
  - VERWACHTE waarde--Waarde verwacht wanneer Security Center de configuratie van uw VM besturingssysteem tegen Hallo regel analyseert
  - --REGEL regel-bewerking door Security Center gebruikt tijdens de analyse van de configuratie van het besturingssysteem van virtuele machine tegen Hallo regel
  - WERKELIJKE waarde--Waarde geretourneerd na analyse van de configuratie van het besturingssysteem van virtuele machine tegen Hallo regel
  - RESULTAAT van evaluatie:-resultaat van de analyse: doorgeven, mislukken

## <a name="see-also"></a>Zie ook
In dit artikel hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling 'herstellen OS beveiligingslekken." Kunt u bekijken Hallo set configuratieregels [hier](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335). Unieke id's (Common Configuration opsomming) CCE tooassign Security Center gebruikt voor van configuratieregels. Ga naar Hallo [CCE](https://nvd.nist.gov/cce/index.cfm) website voor meer informatie.

toolearn meer informatie over Security Center, Zie Hallo resources te volgen:

* [Ondersteunde platforms in Azure Security Center](security-center-os-coverage.md) -geeft een lijst van ondersteunde Windows- en Linux-machines.
* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) -informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) -Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) -informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) -informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) -informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) -Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) -Lees blogberichten over Azure-beveiliging en naleving.

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
