---
title: Herstellen van de OS-beveiligingslekken in Azure Security Center | Microsoft Docs
description: Dit document ziet u hoe de aanbeveling Azure Security Center implementeren ** herstellen OS beveiligingslekken **.
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
ms.openlocfilehash: e6b251d5b97c57b3b6f79d14e53fbed5ca37ecb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a>OS-beveiligingslekken in Azure Security Center oplossen
Azure Security Center analyseert dagelijks uw virtuele machine (VM)-besturingssysteem (OS) voor configuraties die de virtuele machine kwetsbaar voor aanvallen kunnen maken en raadt aan om de configuratiewijzigingen voor deze beveiligingsproblemen te verhelpen. Security Center raadt aan dat u beveiligingsproblemen oplossen wanneer de configuratie van het besturingssysteem van de VM komt niet overeen met de aanbevolen configuratieregels.

> [!NOTE]
> Zie voor meer informatie over de specifieke configuraties die worden bewaakt de [lijst met regels van de aanbevolen configuratie](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
>
>

## <a name="implement-the-recommendation"></a>De aanbeveling implementeren

> [!NOTE]
> In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie.  Dit document is niet een stapsgewijze handleiding.
>
>

1. In de **aanbevelingen** blade Selecteer **herstellen OS beveiligingslekken**.
   ![Beveiligingsproblemen met het besturingssysteem herstellen][1]

    De **herstellen OS beveiligingslekken** blade wordt geopend en een lijst met uw virtuele machines met besturingssysteemconfiguraties die niet overeenkomen met de aanbevolen configuratie-regels.  Voor elke VM identificeert de blade:

   * **REGELS voor MISLUKTE** --het aantal regels dat configuratie van het besturingssysteem van de VM is mislukt.
   * **TIJD van laatste SCAN** --de datum en tijd dat Security Center voor het laatst gescand configuratie van het besturingssysteem van de VM.
   * **STATUS** --de huidige status van het probleem:

     * Open: De kwetsbaarheid ertoe is nog niet opgelost
     * Bezig: De kwetsbaarheid ertoe dat momenteel wordt toegepast, door u is geen actie vereist.
     * Opgelost: De kwetsbaarheid ertoe is al opgenomen in (als het probleem verholpen is, de vermelding is lichter gekleurd weergegeven)
   * **ERNST** --alle zwakke plekken zijn ingesteld op een ernst van de laag, wat betekent dat een beveiligingsprobleem moet worden opgelost, maar geen onmiddellijke aandacht vereist.

2. Selecteer een virtuele machine. Een blade voor die VM wordt geopend en de regels die niet wordt weergegeven.
   ![Van configuratieregels die zijn mislukt][2]

3. Selecteer een regel. In dit voorbeeld kunt selecteren **wachtwoorden moeten voldoen aan de complexiteitsvereisten**. Er wordt een blade geopend met een beschrijving van de regel is mislukt en de impact. Bekijk de details en houd rekening met hoe besturingssysteemconfiguraties worden toegepast.
  ![Beschrijving voor de regel is mislukt][3]

  Security Center gebruikt Common Configuration Enumeration (CCE) om de unieke id's voor configuratieregels toewijzen. De volgende informatie wordt in deze blade verstrekt:

  - --Naam van regel
  - ERNST--Waarde voor CCE ernst van kritieke, belangrijk of waarschuwingsstatus
  - CCIED--CCE unieke id voor de regel
  - Beschrijving: Beschrijving van regel
  - BEVEILIGINGSLEK--Uitleg van beveiligingslek of het risico als de regel wordt niet toegepast
  - IMPACT--Zakelijke impact als regel wordt toegepast
  - VERWACHTE waarde--Waarde verwacht wanneer Security Center uw configuratie van het besturingssysteem van de virtuele machine op basis van de regel analyseert
  - --REGEL regel-bewerking door Security Center gebruikt tijdens de analyse van de configuratie van het besturingssysteem van virtuele machine op basis van de regel
  - WERKELIJKE waarde--Waarde geretourneerd na analyse van uw besturingssysteem voor VM-configuratie op basis van de regel
  - RESULTAAT van evaluatie:-resultaat van de analyse: doorgeven, mislukken

## <a name="see-also"></a>Zie ook
In dit artikel hebt u geleerd hoe u implementeert de aanbeveling Security Center "Herstellen OS beveiligingslekken." U kunt de reeks configuratieregels bekijken [hier](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335). Security Center gebruikt CCE (algemene configuratie opsomming) om de unieke id's voor configuratieregels toewijzen. Ga naar de [CCE](https://nvd.nist.gov/cce/index.cfm) website voor meer informatie.

Zie de volgende bronnen voor meer informatie over Security Center:

* [Ondersteunde platforms in Azure Security Center](security-center-os-coverage.md) -geeft een lijst van ondersteunde Windows- en Linux-machines.
* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) -informatie over het beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen configureren.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) -Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) -informatie over het bewaken van de status van uw Azure-resources.
* [Het beheren van en reageren op beveiligingswaarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) -informatie over het beheren van en reageren op beveiligingswaarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) -informatie over het bewaken van de status van uw partneroplossingen.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) -Raadpleeg Veelgestelde vragen over het gebruik van de service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) -Lees blogberichten over Azure-beveiliging en naleving.

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
