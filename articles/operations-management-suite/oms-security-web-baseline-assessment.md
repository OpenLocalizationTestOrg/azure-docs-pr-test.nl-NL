---
title: aaaWeb basislijn beoordeling in de beveiliging van Operations Management Suite en Audit oplossing basislijn | Microsoft Docs
description: Dit document wordt uitgelegd hoe toouse web-basislijn assessment in OMS beveiligings- en Audit oplossing tooperform een basislijn beoordeling van alle bewaakte webservers voor naleving en beveiliging doel.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: dafa9d3d93fae31748306b60ee40b285dd59c802
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Evaluatie van de webbasislijn in de oplossing voor beveiliging en controle voor Operations Management Suite
Dit document helpt u OMS-beveiliging gebruiken en Audit web basislijn assessment mogelijkheden tooaccess Hallo beveiligingsstatus van uw bewaakte resources.

## <a name="what-is-web-baseline-assessment"></a>Wat is evaluatie van de webbasislijn?
Beveiliging voor OMS biedt momenteel evaluatie van de beveiligingsbasislijn voor besturingssystemen. Wordt gescand Hallo OS-instellingen van uw servers om de 24 uur, en biedt een weergave in het potentieel kwetsbaar instellingen. Lees [Basislijnevaluatie in de oplossing voor beveiliging en controle voor Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/oms-security-baseline) voor meer informatie hierover.

Hallo-doel van Hallo Web basislijn assessment is toofind kwetsbaar web server-instellingen. Hallo drie primaire bronnen voor Hallo web basislijnconfiguraties zijn: .NET, ASP.NET en IIS-configuratie.  Net zoals het operationele systeem basislijn assessment hello, OMS beveiliging gaat tooscan uw webservers elke 24hrs en bieden een overzicht van de beveiligingsstatus van deze.  Internet Information Service (IIS)-configuraties zijn zeer aanpasbare waarmee verschillende site en toepassing niveaus toobe-genegeerd. Hallo scanner controleert Hallo-instellingen op elke toepassing siteniveau in toevoeging toohello standaard hoofdniveau. Dit helpt u bij tooidentify kwetsbaar instellingen en snel herstellen, samen met onze aanbevelingen voor deze instellingen.

>[!NOTE] 
>U kunt downloaden Hallo algemene configuratie-ID's en Basislijnregels gebruikt door de OMS-beveiliging in deze [pagina](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335?redir=0).


## <a name="web-security-baseline-assessment"></a>Basislijnevaluatie van de webbeveiliging

Voor deze preview Hallo functie toegankelijk via Hallo OMS-zoekoptie en Hallo OMS-beveiliging en Audit-Dashboard. Hallo stappen hieronder tooperform Hallo bestemd voor toevoeging query:

1. In Hallo **Microsoft Operations Management Suite** hoofddashboard, klikt u op **beveiligings- en Audit** tegel.
2. In Hallo **beveiligings- en Audit** dashboard ziet u Hallo Web basislijn perspectief volgende toohello OS basislijn perspectief.
   
    ![Basislijnevaluatie webbeveiliging in Beveiliging en controle in OMS](./media/oms-security-web-baseline/oms-security-web-baseline-fig5.png)

3. Hallo linkerdeelvenster ziet u het aantal webservers vergeleken toohello basislijn Hallo gemiddelde percentage van de regels die zijn geslaagd op alle servers van Hallo geëvalueerd en Hallo-lijst met Servers die beoordeeld werden Hallo.
4. Hallo rechter deelvenster geeft een lijst van unieke Hallo regels die niet door *ernst*, en *RuleType*. Te klikken op Hallo rechterdeelvenster regels wordt Hallo details weergeven van die regel. Een voorbeeld is weergegeven in Hallo onder afbeelding. Hallo-regel die wordt geëvalueerd wordt vermeld onder *instelling van regel*. Hallo *AzId* veld dat de unieke id voor elke regel die door Microsoft worden gebruikt is voor het bijhouden van Hallo basislijnregels. Bovendien kunnen gebruikers toothat Hallo zien *resultaat verwacht* (van Microsoft aanbevolen waarde), en andere details met betrekking tot Hallo beveiliging gevolgen van het Hallo-regel.
    
    ![Query’s uitvoeren](./media/oms-security-web-baseline/oms-security-web-baseline-fig6.png)

5. U kunt uw eigen query's maken tooreview Hallo resultaten. 

Hallo eerste query die u kunt gebruiken is Hallo **Web basislijn Assessment samenvatting**. In Hallo **Begin zoeken hier** veld, typt u deze query: *Type = SecurityBaselineSummary BaselineType Web =*. Hallo Hier volgt een voorbeeld van uitvoer:

![Queryresultaat](./media/oms-security-web-baseline/oms-security-web-baseline-fig7.png)

>[!NOTE] 
>In deze query geeft elke record het evaluatieoverzicht op één server weer.

Wanneer u naar Hallo **logboek zoeken**, kunt u verschillende query's tooobtain meer informatie over Hallo web basislijn assessment typen. Bovendien toohello vorige query, u kunt ook gebruiken Hallo uitzonderingen in dit voorbeeld te volgen:

**Web Baseline Rule Assessment** (Evaluatie van webbasislijnregels): elke record vertegenwoordigt een evaluatie van één webbasislijnregel op één server. Dit omvat alle gegevens voor een mislukte regel hello *SitePath* op welke Hallo regel is geëvalueerd, hello *resultaat verwacht*, en Hallo *werkelijke resultaat*.

Query: *Type=SecurityBaseline BaselineType=Web AnalyzeResult=Failed*

![Queryresultaat 2](./media/oms-security-web-baseline/oms-security-web-baseline-fig8.png)

**Weergeven van alle resultaten voor een specifieke server**: deze query geeft aan hoe toosee resultaten van een specifieke server: Query: *Type = SecurityBaseline BaselineType = Web Computer BaselineTestVM1 =*

![Queryresultaat 3](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

U kunt deze records/query's toocreate uw eigen dashboards, rapporten of meldingen. Hier volgt een voorbeeld-UI-besturingselement dat u tooyour dashboard kunt toevoegen. U leert hoe toovisualize uw gegevens dankzij OMS-ontwerper [hier](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). welkomstscherm onderstaande is een voorbeeld van hoe Hallo tegel eruitziet nadat u deze aanpassing.

![dashboard](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

## <a name="see-also"></a>Zie ook
In dit document hebt u meer kunnen lezen over het evalueren van de webbasislijn met behulp van de oplossing voor beveiliging en controle voor OMS. toolearn meer informatie over OMS-beveiliging, Zie Hallo artikelen te volgen:

* [Overzicht van Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Bewaking en reageren tooSecurity waarschuwingen in de beveiliging van Operations Management Suite en Audit-oplossing](oms-security-responding-alerts.md)
* [Resources bewaken in de oplossing Beveiliging en controle van Operations Management Suite ](oms-security-monitoring-resources.md)

