---
title: aaaAutomate Azure Log Analytics verwerkt met Microsoft-Flow
description: Meer informatie over hoe u kunt Microsoft Flow tooquickly herhaalbare processen automatiseren met behulp van hello Azure Log Analytics-connector.
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a>Log Analytics-processen met Hallo-connector voor Microsoft-Flow automatiseren
[Microsoft-Flow](https://ms.flow.microsoft.com) kunt u toocreate geautomatiseerde werkstromen met honderden acties voor diverse services. De uitvoer van een actie kan worden gebruikt als invoer tooanother zodat u toocreate integratie tussen verschillende services.  Hello Azure Log Analytics-connector voor Microsoft-Flow kunt u toobuild werkstromen die door het logboek van zoekopdrachten in logboekanalyse opgehaalde gegevens bevatten.

U kunt bijvoorbeeld Microsoft Flow toouse Log Analytics-gegevens in een e-mailmelding vanuit Office 365 gebruiken, maakt een bug in Visual Studio Team Services of een toegestane bericht.  Door een eenvoudige planning of van een bepaalde actie in een gekoppelde service, zoals wanneer een e-mailbericht of een tweet wordt ontvangen, kunt u een werkstroom activeren.  


> [!NOTE]
> Hello Azure Log Analytics-connector voor Microsoft-Flow vereist uw werkruimte toobe bijgewerkt toohello nieuwe logboekanalyse querytaal. U kunt meer informatie over de nieuwe taal Hallo en uw werkruimte op Hallo procedure tooupgrade ophalen [Upgrade van uw Azure-logboekanalyse werkruimte toonew logboek zoekopdracht](log-analytics-log-search-upgrade.md).  

Hallo-zelfstudie in dit artikel leert u hoe toocreate een stroom die automatisch verzonden resultaten van een zoekopdracht Log Analytics-logboek Hallo via e-mail, slechts één voorbeeld van hoe u Log Analytics in Microsoft Flow kunt gebruiken. 


## <a name="step-1-create-a-flow"></a>Stap 1: Een stroom maken
1. Aanmelden te[Microsoft Flow](http://flow.microsoft.com), en selecteer **mijn loopt**.
2. Klik op **+ maken van leeg**.

## <a name="step-2-create-a-trigger-for-your-flow"></a>Stap 2: Maak een trigger voor uw flow
1. Klik op **zoeken honderden connectors en triggers**.
2. Type **planning** in het zoekvak Hallo.
3. Selecteer **planning**, en selecteer vervolgens **schema - terugkeerpatroon**.
4. In Hallo **frequentie** vak Selecteer **dag** en in Hallo **Interval** Voer **1**.<br><br>![Dialoogvenster voor Microsoft-Flow-trigger](media/log-analytics-flow-tutorial/flow01.png)


## <a name="step-3-add-a-log-analytics-action"></a>Stap 3: Een actie logboekanalyse toevoegen
1. Klik op **+ een nieuwe stap**, en klik vervolgens op **een actie toevoegen**.
2. Zoeken naar **Meld Analytics**.
3. Klik op **Azure Log Analytics-query uitvoeren en visualiseren resultaten**.<br><br>![Log Analytics query-venster uitvoeren](media/log-analytics-flow-tutorial/flow02.png)

## <a name="step-4-configure-hello-log-analytics-action"></a>Stap 4: Configureer Hallo logboekanalyse actie

1. Geef details op Hallo voor uw werkruimte inclusief Hallo abonnement-ID, resourcegroep, en de naam van de werkruimte.
2. Log Analytics query toohello na Hallo toevoegen **Query** venster.  Dit is alleen een voorbeeldquery en u kunt vervangen door een andere waarmee gegevens worden geretourneerd.
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. Selecteer **HTML-tabel** voor Hallo **grafiektype**.<br><br>![Log Analytics actie](media/log-analytics-flow-tutorial/flow03.png)

## <a name="step-5-configure-hello-flow-toosend-email"></a>Stap 5: Hallo stroom toosend e-mail configureren

1. Klik op **nieuwe stap**, en klik vervolgens op **+ een actie toevoegen**.
2. Zoeken naar **OfficeOutlook 365**.
3. Klik op **Outlook in Office 365 – stuurt u een e-mailadres**.<br><br>![Selectievenster voor Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)

4. Hallo e-mailadres van een ontvanger opgeven in Hallo **naar** venster en een onderwerp in voor Hallo e-mailadres in **onderwerp**.
5. Klik ergens in Hallo **hoofdtekst** vak.  Een **dynamische inhoud** venster wordt geopend met waarden uit de vorige acties.  
6. Selecteer **hoofdtekst**.  Dit is Hallo resultaten van Hallo-query in Hallo Log Analytics-actie.
6. Klik op **geavanceerde opties weergeven**.
7. In Hallo **Is HTML** de optie **Ja**.<br><br>![Venster van Office 365 e-configuratie](media/log-analytics-flow-tutorial/flow05.png)

## <a name="step-6-save-and-test-your-flow"></a>Stap 6: Opslaan en testen van uw flow
1. In Hallo **stroom naam** vak en klik vervolgens op toevoegen van een naam voor uw flow **stroom maken**.<br><br>![Stroom opslaan](media/log-analytics-flow-tutorial/flow06.png)
2. Hallo-stroom wordt nu gemaakt en wordt uitgevoerd na een dag is Hallo planning die u hebt opgegeven. 
3. tooimmediately test Hallo flow, klikt u op **nu uitvoeren** en vervolgens **uitvoeren stroom**.<br><br>![Stroom uitvoeren](media/log-analytics-flow-tutorial/flow07.png)
3. Wanneer het Hallo-stroom is voltooid, controleert u Hallo mail van Hallo-ontvanger die u hebt opgegeven.  U moet een e-mailbericht met een hoofdtekst vergelijkbare toohello volgende hebt ontvangen:<br><br>![Voorbeeldbericht](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-search-new.md).
- Meer informatie over [Microsoft Flow](https://ms.flow.microsoft.com).



