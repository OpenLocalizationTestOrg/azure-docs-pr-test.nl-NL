---
title: Security Center threat intelligence-rapport aaaAzure | Microsoft Docs
description: Dit document helpt u toouse Azure Security Center Threat Intelligent rapporten tijdens een onderzoek toofind meer informatie over een beveiligingswaarschuwing.
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: c888cfac1dd8b057616a6b8e6c6f6b67b552f2e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a>Bedreigingsinformatierapport in Azure Security Center
In dit document wordt uitgelegd hoe bedreigingsinformatierapporten in Azure Security Center u kunnen helpen meer te weten te komen over een bedreiging die een beveiligingswaarschuwing heeft gegenereerd.

## <a name="what-is-a-threat-intelligence-report"></a>Wat is een bedreigingsinformatierapport?
Detectie van dreigingen Security Center werkt door de bewaking van de beveiligingsgegevens van uw Azure-resources, het Hallo-netwerk en de verbonden partneroplossingen. Deze informatie kunt vaak correleren van gegevens uit meerdere bronnen, tooidentify bedreigingen wordt geanalyseerd. Dit proces maakt deel uit van Hallo Security Center [detectiemogelijkheden](security-center-detection-capabilities.md).

Wanneer Security Center een bedreiging detecteert, produceert het een [beveiligingswaarschuwing](security-center-managing-and-responding-alerts.md) met gedetailleerde informatie over een specifieke gebeurtenis en suggesties om het op te lossen. tooassist respons op incidenten teams onderzoeken en bedreigingen te herstellen, Security Center bevat een bedreiging intelligence-rapport dat informatie over Hallo threat die is gedetecteerd bevat, inclusief gegevens, zoals de:

* De identiteit of associaties van de aanvaller (indien beschikbaar)
* De doelstellingen van de aanvaller
* Huidige en eerdere aanvalscampagnes (indien beschikbaar)
* De tactieken, middelen en procedures van de aanvaller
* Gekoppelde indicators of compromise (IoC) zoals URL's en bestands-hashes
* Victimology die Hallo industrie- en geografische invloed tooassist u bij het bepalen of uw Azure-resources zijn kwetsbaar voor
* Informatie over risicobeperking en herstel

> [!NOTE]
> Hallo hoeveelheid gegevens in een bepaalde lijst varieert; Hallo detailniveau is gebaseerd op de activiteit en de invloed van Hallo malware.
>
>

Security Center heeft drie soorten threat rapporten die volgens toohello aanval kunnen variëren. Hallo rapporten zijn beschikbaar:

* **Activiteitsgroeprapport**: biedt diepgaande informatie over aanvallers en hun doelstellingen en tactieken.
* **Campagnerapport**: gericht op details van een specifieke aanvalscampagne.
* **Samenvattingsrapport voor dreiging**: alle items in de vorige twee rapporten Hallo Hallo dekt.

Dit type gegevens is zeer nuttig tijdens Hallo [respons op incidenten](security-center-incident-response.md) verwerken, waarbij er een lopende onderzoek toounderstand Hallo-bron van de aanval hello, Hallo aanvaller beweegredenen en wat toodo toomitigate dit probleem u verder gaat.

## <a name="how-tooaccess-hello-threat-intelligence-report"></a>Hoe Hallo tooaccess threat intelligence-rapport?
U kunt uw huidige waarschuwingen controleren door te kijken Hallo **beveiligingswaarschuwingen** tegel. Openen hello Azure-Portal en stappen Hallo hieronder toosee meer informatie over elke waarschuwing:

1. Op Hallo Security Center-dashboard, ziet u Hallo **beveiligingswaarschuwingen** tegel.
2. Klik op Hallo tegel tooopen hello **beveiligingswaarschuwingen** -blade waarmee de bevat meer informatie over Hallo waarschuwingen en klik op in Hallo beveiligingswaarschuwing dat u wilt dat tooobtain meer informatie over.

    ![Beveiligingswaarschuwingen](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. In dit geval Hallo **verdachte proces dat wordt uitgevoerd** blade Hallo worden details weergegeven over Hallo waarschuwing zoals weergegeven in onderstaande afbeelding ziet Hallo:

    ![Details van beveiligingswaarschuwing](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. Hallo hoeveelheid gegevens beschikbaar zijn voor elke beveiligingswaarschuwing varieert volgens toohello type waarschuwing. In Hallo **rapporten** veld dat u hebt een koppeling toohello threat intelligence-rapport. Als u hierop klikt, wordt er een nieuw browservenster geopend met een PDF-bestand.

   ![Opslagselectie](./media/security-center-threat-report/security-center-threat-report-fig3.png)

U kunt hier downloaden Hallo PDF-bestand voor dit rapport en lees die meer over de beveiliging van Hallo probleem dat is gedetecteerd en acties onderneemt op basis van Hallo informatie.

## <a name="see-also"></a>Zie ook
In dit document hebt u geleerd hoe beveiligingsinformatierapporten van Azure Security Center u kunnen helpen tijdens een onderzoek naar beveiligingswaarschuwingen. toolearn meer informatie over Azure Security Center Hallo ziet:

* [Veelgestelde vragen over Azure Security Center](security-center-faq.md). Veelgestelde vragen over het gebruik van Hallo service vinden.
* [Azure Security Center gebruiken voor reacties op incidenten](security-center-incident-response.md)
* [Detectiemogelijkheden van Azure Security Center](security-center-detection-capabilities.md)
* [Plannings- en bedieningsgids voor Azure Security Center](security-center-planning-and-operations-guide.md). Meer informatie over hoe tooplan en Hallo ontwerpoverwegingen tooadopt Azure Security Center begrijpen.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md). Meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Beveiligingsincidenten afhandelen in Azure Security Center](security-center-incident.md)
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/). Raadpleeg de blogberichten over beveiliging en naleving in Azure.
