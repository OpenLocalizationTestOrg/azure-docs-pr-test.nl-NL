---
title: aaaRespond toosecurity incidenten met Azure Security Center | Microsoft Docs
description: Dit document wordt uitgelegd hoe toouse Azure Security Center voor een respons op incidenten scenario.
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 8af12f1c-4dce-4212-8ac4-170d4313492d
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: aaf50c0c7e774d03d517c3fd11686dbae48dd29b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-security-center-for-an-incident-response"></a>Azure Security Center gebruiken voor reacties op incidenten
Veel organisaties ontdekken hoe toorespond toosecurity incidenten alleen nadat ze zijn een aanval. het is belangrijk toohave een respons op incidenten plannen voldaan voordat een aanval plaatsvindt tooreduce kosten en schade. U kunt Azure Security Center gebruiken in verschillende fasen tijdens een reactie op een incident.

## <a name="incident-response-planning"></a>Planning voor het reageren op incidenten
Een doeltreffend plan is afhankelijk van drie belangrijkste mogelijkheden: kunnen tooprotect enkel, detecteren en toothreats reageren. Beveiliging is over het voorkomen van incidenten, detectie is over het identificeren van bedreigingen vroeg en reactie over Hallo aanvaller onbeschikbaar maken en herstellen van systemen toomitigate Hallo gevolgen van een inbreuk.

In dit artikel gebruikt Hallo beveiliging respons op incidenten stadia van Hallo [reactie van Microsoft Azure-beveiliging in Hallo Cloud](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678) artikel, zoals wordt weergegeven in het volgende diagram Hallo:

![Levenscyclus van reacties op incidenten](./media/security-center-incident-response/security-center-incident-response-fig1.png)

Security Center kunt u tijdens het Hallo-analyse, beoordeling en spoor fasen. Hier volgen enkele voorbeelden van hoe Security Center nuttig tijdens het Hallo drie initiële respons op incidenten fasen zijn kan:

* **Detecteren**: Bekijk Hallo eerste indicatie van een gebeurtenis onderzoek.
  * Voorbeeld: Bekijk Hallo initiële verificatie dat een beveiligingswaarschuwing met hoge prioriteit in Security Center-dashboard Hallo is gegenereerd.
* **Beoordelen**: Hallo eerste beoordeling tooobtain meer informatie over Hallo verdachte activiteiten uitvoeren.
  * Voorbeeld: meer informatie over de beveiligingswaarschuwing Hallo verkrijgen.
* **Diagnose stellen**: een technisch onderzoek uitvoeren, en strategieën voor beheersing, risicobeperking en tijdelijke oplossingen in kaart brengen.
  * Voorbeeld: stappen Hallo herstel door Security Center in die bepaalde Beveiligingswaarschuwing beschreven.

Hallo-scenario dat volgt op ziet u hoe tooleverage Security Center tijdens Hallo detecteren, beoordeling en spoor/reageren fasen van een beveiligingsincident voordoet. In Security Center is een [beveiligingsincident](security-center-incident.md) een samenloop van alle waarschuwingen voor een resource die overeenstemt met [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/)-patronen. Incidenten verschijnen in Hallo [beveiligingswaarschuwingen](security-center-managing-and-responding-alerts.md) tegel en blade. Een incident blijkt Hallo lijst met verwante waarschuwingen, waarmee u tooobtain meer informatie over elk exemplaar. Security Center geeft ook zelfstandige beveiligingswaarschuwingen die ook gebruikt tootrack omlaag een verdachte activiteit worden kunnen.

## <a name="scenario"></a>Scenario
Contoso onlangs gemigreerd enkele van hun tooAzure lokale bronnen, met inbegrip van sommige line-of-business-werkbelastingen op basis van een virtuele machine en de SQL-databases. Het Contoso Core Computer Security Incident Response Team (CSIRT) heeft een probleem met het onderzoeken van mogelijke beveiligingskwesties. De oorzaak hiervan is dat het bedrijf geen beveiligingsintelligence heeft die is geïntegreerd in de aanwezige hulpmiddelen voor het reageren op incidenten. Dit gebrek aan integratie introduceert een probleem opgetreden tijdens het Hallo detecteren fase (te veel valse positieven), evenals tijdens Hallo schatten en spoor fasen. Als onderdeel van deze migratie ze tooopt beslist in voor het Beveiligingscentrum toohelp ze Verhelp het probleem.

eerste fase van deze voltooide migratie Hallo nadat ze vrijgegeven alle resources en verholpen alle Hallo beveiligingsaanbevelingen vanuit Security Center. Contoso CSIRT is Hallo centrale punt voor het omgaan met beveiligingsincidenten computer. Hallo-team bestaat uit een groep personen die verantwoordelijk zijn voor het omgaan met een beveiligingsincident voordoet. Hallo teamleden beschikken over rechten tooensure die geen antwoord-gebied is achtergebleven gesignaleerde duidelijk gedefinieerde.

Voor Hallo doel van dit scenario gaan we toofocus op Hallo functies Hallo Persona's die deel van Contoso CSIRT uitmaken te volgen:

![Levenscyclus van reacties op incidenten](./media/security-center-incident-response/security-center-incident-response-fig2.png)

Judy houdt zich bezig met beveiligingsbewerkingen. Haar verantwoordelijkheden zijn onder andere:

* Controleren en bedreigingen toosecurity rond Hallo klok reageren.
* Escaleren toohello cloud werkbelasting eigenaar of beveiligingsanalist indien nodig.

Sam is een beveiligingsanalist en zijn verantwoordelijkheden omvatten:

* Het onderzoeken van aanvallen.
* Het oplossen van problemen die worden vermeld in beveiligingswaarschuwingen.
* Werken met werkbelasting eigenaars toodetermine en beperkingen van toepassing.

Zoals u ziet, Judith en Sam hebben verschillende verantwoordelijkheden en moeten werken ze samen tooshare Security Center informatie.

## <a name="recommended-solution"></a>Aanbevolen oplossing
Aangezien Judith en Sam verschillende rollen hebben, moeten ze gebruikmaken van verschillende gebieden van Security Center tooobtain relevante informatie voor hun dagelijkse activiteiten. Judy gebruikt **beveiligingswaarschuwingen** als onderdeel van haar dagelijkse bewakingswerkzaamheden.

![Beveiligingswaarschuwingen](./media/security-center-incident-response/security-center-incident-response-fig3.png)

Judy gebruikt beveiligingswaarschuwingen tijdens Hallo detecteren en schatten fasen. Nadat Judith is voltooid de eerste beoordeling hello, mogelijk ze Hallo probleem tooSam escaleren als extra onderzoek vereist is. Op dit moment gebruikt Sam Hallo-informatie die is opgegeven door Security Center soms in combinatie met andere gegevensbronnen toomove toohello spoor fase.

## <a name="how-tooimplement-this-solution"></a>Hoe tooimplement deze oplossing
toosee hoe u Azure Security Center in een respons op incidenten scenario gebruikt, we stappen van Judith in Hallo analyse en evaluatie fasen en vervolgens zien wat Sam doet toodiagnose Hallo probleem.

### <a name="detect-and-assess-incident-response-stages"></a>Detectie- en beoordelingsfase van de reactie op incidenten
Judy toohello aangemeld met Azure-portal en werkt in Hallo Security Center-console. Als onderdeel van haar dagelijks bewakingsactiviteiten gestart ze hoge prioriteit beveiliging waarschuwingen door te voeren Hallo stappen te volgen beoordelen:

1. Klik op Hallo **beveiligingswaarschuwingen** tegel en toegang Hallo **beveiligingswaarschuwingen** blade.
    ![Blade Beveiligingswaarschuwing](./media/security-center-incident-response/security-center-incident-response-fig4.png)

   > [!NOTE]
   > Judy is gaat tooperform een beoordeling op Hallo schadelijke SQL activiteit waarschuwing voor Hallo doel van dit scenario, zoals in de voorgaande afbeelding Hallo.
   >
   >
2. Klik op Hallo **schadelijke SQL-activiteit** waarschuwing en bekijk Hallo aangevallen resources in Hallo **schadelijke SQL-activiteit** blade: ![details Incident](./media/security-center-incident-response/security-center-incident-response-fig5.png)

    In deze blade Judy kunt notities met betrekking tot Hallo aangevallen resources, hoe vaak deze aanval is uitgevoerd en wanneer deze is gedetecteerd.
3. Klik op Hallo **aangevallen resource** tooobtain meer informatie over deze aanval.

Na het lezen van Hallo beschrijving Judy ervan overtuigd dat dit geen fout-positief is en dat ze deze case tooSam moet escaleren.

### <a name="diagnose-incident-response-stage"></a>Diagnosefase van reactie op incidenten
SAM Hallo geval ontvangt van Judy en begint met het Hallo-herstelstappen die Security Center voorgesteld controleren.

![Levenscyclus van reacties op incidenten](./media/security-center-incident-response/security-center-incident-response-fig6.png)

### <a name="additional-resources"></a>Aanvullende bronnen
Hallo respons op incidenten team kan ook profiteren van Hallo [Security Center Power BI](security-center-powerbi.md) mogelijkheid toosee verschillende soorten rapporten. Deze rapporten kunnen sneller worden tijdens verder onderzoek toovisualize, analyseren en filteren van aanbevelingen en beveiligingswaarschuwingen. Voor de bedrijven die gebruikmaken van hun security information en event-beheeroplossing (SIEM) tijdens het onderzoek van hello, kunnen ze ook [Security Center integreren in hun oplossing](security-center-integrating-alerts-with-log-integration.md). U kunt ook Azure controlelogboeken en -virtuele machine (VM) beveiligingsgebeurtenissen integreren met behulp van Hallo [Azure-logboekanalyse integratie hulpprogramma](https://blogs.msdn.microsoft.com/azuresecurity/2016/07/21/microsoft-azure-log-integration-preview/). een aanval tooinvestigate, kunt u deze informatie gebruiken in combinatie met Hallo-informatie die door Security Center biedt.

## <a name="conclusion"></a>Conclusie
Een team is samengesteld voordat er een incident voordoet, is erg belangrijk tooyour organisatie en positief van invloed zijn op hoe incidenten moeten worden verwerkt. Die Hallo juiste hulpmiddelen toomonitor bronnen, kunt u dit team tootake nauwkeurige stappen tooremediate een beveiligingsincident voordoet. Security Center [detectiemogelijkheden](security-center-detection-capabilities.md) kunt helpen IT tooquickly reageren toosecurity incidenten en beveiligingsproblemen herstellen.
