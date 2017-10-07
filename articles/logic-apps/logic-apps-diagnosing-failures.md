---
title: aaaDiagnose fouten - Azure Logic Apps | Microsoft Docs
description: Algemene manieren toounderstand waar logische apps zijn mislukt
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a>Logic app mislukte diagnoses
Als u problemen of fouten met uw logische apps optreden, er zijn enkele manieren kunt u beter te begrijpen waar Hallo fouten afkomstig zijn uit.  

## <a name="azure-portal-tools"></a>Azure portal-hulpprogramma 's
Hello Azure-portal biedt veel toodiagnose van hulpprogramma's voor elke logische app bij elke stap.

### <a name="trigger-history"></a>Geschiedenis van de trigger

Elke app logica heeft ten minste één trigger. Als u merkt dat apps worden niet geactiveerd, zoek eerst Hallo trigger geschiedenis voor meer informatie. U kunt toegang tot geschiedenis van Hallo-trigger op Hallo logica app'ss hoofdblade.

![Zoeken naar Hallo trigger geschiedenis][1]

Hallo trigger geschiedenislijsten die alle pogingen die uw logische app activeren. U kunt klikken op elke poging trigger toodrill in Hallo details specifiek, een invoer of uitvoer die Hallo trigger poging gegenereerd. Als u mislukte triggers vinden, selecteer Hallo trigger poging en kies Hallo **uitvoer** koppelen tooreview eventuele gegenereerde foutberichten, bijvoorbeeld voor FTP-referenties die ongeldig zijn.

Hallo verschillende statussen ziet u mogelijk zijn:

* **Overgeslagen**. Hallo-eindpunt polled toocheck voor gegevens is en dat er geen gegevens beschikbaar was antwoord ontvangen.
* **Geslaagd**. Hallo trigger ontvangen gegevens is beschikbaar antwoord. Deze status kan worden veroorzaakt door een handmatige trigger, een terugkeerpatroon trigger of een polling-trigger. Deze status wordt meestal vergezeld van Hallo **Fired** status, maar mogelijk niet als er een voorwaarde of SplitOn opdracht in de codeweergave die niet is voldaan.
* **Kan geen**. Er is een fout gegenereerd.

#### <a name="start-a-trigger-manually"></a>Een trigger handmatig starten

Als u wilt dat Hallo logic app toocheck voor een beschikbare trigger onmiddellijk zonder te wachten op de volgende terugkeerpatroon hello, klikt u op **Trigger selecteren** op Hallo hoofdblade tooforce een controle. Bijvoorbeeld, te klikken op deze koppeling met een trigger Dropbox zorgt ervoor dat Hallo werkstroom tooimmediately poll Dropbox voor nieuwe bestanden.

### <a name="run-history"></a>geschiedenis uitvoeren

Elke gestarte trigger resulteert in een uitvoering. U kunt informatie over openen vanaf Hallo hoofdblade, met veel details die kunnen u helpen begrijpen wat is er gebeurd tijdens het Hallo-werkstroom.

![Zoeken naar Hallo geschiedenis uitvoeren][2]

Een uitvoering geeft Hallo volgende statussen:

* **Geslaagd**. Alle acties is voltooid. Als er een fout opgetreden, is die is mislukt door een actie die is opgetreden in de werkstroom hello later verwerkt. Dat wil zeggen, werd Hallo mislukt uitgevoerd door een actie die toorun na een mislukte actie is ingesteld.
* **Kan geen**. Ten minste één actie heeft een fout die niet is verwerkt door de actie later in Hallo-werkstroom.
* **Geannuleerd**. Hallo werkstroom werd uitgevoerd, maar heeft een annuleringsaanvraag ontvangen.
* **Met**. Hallo werkstroom momenteel wordt uitgevoerd. Deze status kan optreden voor beperkte werkstromen, of vanwege Hallo huidige plan prijzen. Zie voor meer informatie [actie limieten op de pagina met prijzen Hallo](https://azure.microsoft.com/pricing/details/app-service/plans/). Configureren van diagnostische gegevens (Hallo grafieken die worden weergegeven onder Hallo geschiedenis uitvoeren) kunt bieden ook informatie over eventuele vertraging gebeurtenissen die zich voordoen.

Wanneer u een uitvoeringsgeschiedenis bekijkt, kunt u inzoomen voor meer informatie.  

#### <a name="trigger-outputs"></a>Trigger-uitvoer

Trigger voert weergeven Hallo gegevens die afkomstig zijn van het Hallo-trigger. Deze uitvoer kunt u bepalen of alle eigenschappen naar verwachting geretourneerd.

> [!NOTE]
> Als er inhoud die u niet begrijpt, informatie over hoe Azure Logic Apps [verschillende typen inhoud verwerkt](../logic-apps/logic-apps-content-type.md).
> 

![Voorbeelden van trigger-uitvoer][3]

#### <a name="action-inputs-and-outputs"></a>Actie-invoer en uitvoer

U kunt inzoomen op het Hallo-in- en uitgangen die een actie ontvangen. Deze gegevens zijn handig om te begrijpen Hallo afmeting en vorm van Hallo outputs en voor het vinden van eventuele foutberichten die mogelijk zijn gegenereerd.

![Actie-invoer en uitvoer][4]

## <a name="debug-workflow-runtime"></a>Fouten opsporen in workflowruntime

Samen met bewaking Hallo invoer, uitvoer en triggers van een reeks, kunt u sommige stappen tooa werkstroom die u helpen bij foutopsporing toevoegen. 
[RequestBin](http://requestb.in) is een krachtig hulpprogramma waarmee u als een stap in een werkstroom toevoegen kunt. U kunt met behulp van RequestBin een HTTP-aanvraag inspector toodetermine Hallo exacte grootte, vorm en indeling van een HTTP-aanvraag instellen. U kunt een RequestBin maken en plak de URL van de Hallo in een logische app HTTP POST-actie met de inhoud van de hoofdtekst is dat u wilt dat tootest, bijvoorbeeld, een expressie of een andere stap uitvoer. Na het uitvoeren van Hallo logische app, kunt u uw RequestBin toosee hoe Hallo aanvraag werd gevormd wanneer gegenereerd vanuit Logic Apps-engine Hallo vernieuwen.

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
