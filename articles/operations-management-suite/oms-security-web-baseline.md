---
title: aaaOperations Management Suite beveiligings- en Audit oplossing Web basislijn | Microsoft Docs
description: Dit document wordt uitgelegd hoe toouse OMS beveiligings- en Audit oplossing tooperform een beoordeling van de basislijn web van alle bewaakte webservers voor naleving en beveiliging doel.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Evaluatie van de webbasislijn in de oplossing voor beveiliging en controle voor Operations Management Suite
Dit document helpt u toouse [Operations Management Suite (OMS) beveiligings- en Audit oplossing](operations-management-suite-overview.md) web-basislijn assessment mogelijkheden tooaccess Hallo beveiligingsstatus van uw bewaakte resources.

## <a name="what-is-web-baseline-assessment"></a>Wat is evaluatie van de webbasislijn?
Beveiliging voor OMS biedt momenteel evaluatie van de beveiligingsbasislijn voor besturingssystemen. Wordt gescand Hallo besturingssysteeminstellingen van uw servers om de 24 uur en biedt een weergave in het potentieel kwetsbaar instellingen. Lees [Basislijnevaluatie in de oplossing voor beveiliging en controle voor Operations Management Suite](oms-security-baseline.md) voor meer informatie hierover.

Hallo-doel van Hallo web basislijn assessment is toofind kwetsbaar web server-instellingen. Hallo drie primaire bronnen voor Hallo web basislijnconfiguraties zijn: .NET, ASP.NET en IIS-configuratie.  Net zoals het operationele systeem basislijn assessment hello, OMS beveiliging gaat tooscan uw webservers elke 24hrs en bieden een overzicht van de beveiligingsstatus van deze.  Internet Information Service (IIS)-configuraties zijn zeer aanpasbare waarmee verschillende site en toepassing niveaus toobe-genegeerd. Hallo scanner controleert Hallo-instellingen op elke toepassing siteniveau in toevoeging toohello standaard hoofdniveau. Dit helpt u bij tooidentify mogelijke beveiligingsproblemen instellingen locaties en snel herstellen.


## <a name="web-security-baseline-assessment"></a>Basislijnevaluatie van de webbeveiliging
Deze functie gaat toobe toegankelijk via Hallo OMS zoekoptie voor deze preview. Hallo stappen hieronder tooperform Hallo bestemd voor toevoeging query:

1. In Hallo **Microsoft Operations Management Suite** hoofddashboard Klik **beveiligings- en Audit** tegel.
2. In Hallo **beveiligings- en Audit** dashboard, klikt u op **logboek zoeken** knop.
3. Hallo eerste query die u kunt gebruiken is Hallo **Web basislijn Assessment samenvatting**. In Hallo **Begin zoeken hier** veld, typt u deze query: Type*SecurityBaselineSummary BaselineType = web =*. Hallo scherm volgen is een voorbeeld van uitvoer:

![Overzicht van evaluatie van de webbasislijn](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> In deze query geeft elke record het evaluatieoverzicht op één server weer.

Wanneer u naar Hallo **logboek zoeken**, kunt u verschillende query's tooobtain meer informatie over Hallo web basislijn assessment typen. Bovendien toohello vorige query, u kunt ook gebruiken Hallo uitzonderingen in dit voorbeeld te volgen.

**Web Baseline Rule Assessment** (Evaluatie van webbasislijnregels): elke record vertegenwoordigt een evaluatie van één webbasislijnregel op één server. Dit omvat alle gegevens voor de regel hello, locatie, Hallo verwacht resultaat en Hallo werkelijke resultaat.

**Query**: Type*=SecurityBaseline BaselineType=web*

![Evaluatie van webbasislijnregels](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

**Weergeven van alle resultaten voor een specifieke server**: deze query geeft aan hoe toosee resultaten van een specifieke server.

**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*

![Alle resultaten](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

U kunt deze toocreate records/query's ook uw eigen dashboards, rapporten of meldingen. welkomstscherm onderstaande is een voorbeeld-UI-besturingselement dat u tooyour dashboard kunt toevoegen. U leert hoe toovisualize uw gegevens dankzij OMS-ontwerper [hier](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). welkomstscherm onderstaande is een voorbeeld van hoe Hallo tegel eruitziet nadat u deze aanpassing.

![Voorbeeld-UI](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> Als u tooknow Hallo instellingen die zijn geselecteerd voor de beoordeling van Hallo basislijn wilt, kunt u downloaden [deze Excel-spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) die deze instellingen bevat.

## <a name="see-also"></a>Zie ook
In dit document hebt u meer kunnen lezen over het evalueren van de webbasislijn met behulp van de oplossing voor beveiliging en controle voor OMS. toolearn meer informatie over OMS-beveiliging, Zie Hallo artikelen te volgen:

* [Overzicht van Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Bewaking en reageren tooSecurity waarschuwingen in de beveiliging van Operations Management Suite en Audit-oplossing](oms-security-responding-alerts.md)
* [Resources bewaken in de oplossing Beveiliging en controle van Operations Management Suite ](oms-security-monitoring-resources.md)

