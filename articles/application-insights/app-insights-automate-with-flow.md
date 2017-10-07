---
title: aaaAutomate Azure Application Insights verwerkt met Microsoft-Flow
description: Meer informatie over hoe u kunt Microsoft Flow tooquickly herhaalbare processen automatiseren met behulp van Hallo Application Insights-connector.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a>Azure Application Insights-processen met Hallo-connector voor Microsoft-Flow automatiseren

Vindt u uzelf herhaaldelijk uitgevoerd Hallo dezelfde query's op uw telemetrie gegevens toocheck die uw service goed werkt? Zoek tooautomate zijn deze query's voor het vinden van trends en afwijkingen en vervolgens uw eigen werkstromen omheen te bouwen? Hello Azure Application Insights-connector (preview) voor Microsoft-Flow is de juiste hulpprogramma Hallo voor deze doeleinden.

Met deze integratie kunt u nu meerdere processen automatiseren zonder een één regel code te schrijven. Nadat u een stroom met behulp van een actie Application Insights hebt gemaakt, wordt uw Application Insights Analytics query automatisch uitgevoerd door Hallo-stroom. 

U kunt ook aanvullende acties toevoegen. Microsoft-Flow maakt honderden acties beschikbaar. U kunt bijvoorbeeld Microsoft Flow tooautomatically verzenden een e-mailmelding gebruiken of maken van een bug in Visual Studio Team Services. U kunt ook een gebruiken Hallo veel [sjablonen](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) die beschikbaar zijn voor het Hallo-connector voor Microsoft-Flow. Deze sjablonen versnellen Hallo van het maken van een stroom. 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a>Maken van een stroom voor Application Insights

In deze zelfstudie leert u hoe toocreate een stroom die gebruikmaakt van Hallo Analytics automatisch cluster algoritme toogroup kenmerken in Hallo-gegevens voor een webtoepassing. Hallo resultaten verzonden Hallo stroom automatisch via e-mail, slechts één voorbeeld van hoe u kunt Microsoft Flow en Application Insights Analytics samen gebruiken. 

### <a name="step-1-create-a-flow"></a>Stap 1: Een stroom maken
1. Aanmelden te[Microsoft Flow](http://flow.microsoft.com), en selecteer vervolgens **mijn loopt**.
2. Klik op **maken van een stroom van leeg**.

### <a name="step-2-create-a-trigger-for-your-flow"></a>Stap 2: Maak een trigger voor uw flow
1. Selecteer **planning**, en selecteer vervolgens **schema - terugkeerpatroon**.
2. In Hallo **frequentie** de optie **dag**, en in Hallo **Interval** Voer **1**.

    ![Dialoogvenster voor Microsoft-Flow-trigger](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a>Stap 3: Een Application Insights-actie toevoegen
1. Klik op **nieuwe stap**, en klik vervolgens op **een actie toevoegen**.
2. Zoeken naar **Azure Application Insights**.
3. Klik op **Azure Application Insights – visualiseren Analytics query Preview**.

    ![Analytics query-venster uitvoeren](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Stap 4: Verbinding maken met tooan Application Insights-resource

toocomplete deze stap moet u een toepassings-ID en een API-sleutel voor uw resource. U kunt ze ophalen uit hello Azure-portal, zoals wordt weergegeven in het volgende diagram Hallo:

![Toepassings-ID in hello Azure-portal](./media/app-insights-automate-with-flow/appid.png) 

- Geef een naam voor de verbinding, samen met de Hallo-toepassing-ID en API-sleutel.

    ![Venster van de verbinding met Microsoft-Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Stap 5: Hallo Analytics-query en grafiektype opgeven
Deze voorbeeldquery Hallo is mislukt-aanvragen in Hallo laatste dag selecteert en verbindt deze met uitzonderingen die zijn opgetreden tijdens het Hallo-bewerking. Analytics correleert toe op basis van Hallo operation_Id id. Hallo resultaten segmenten Hallo query vervolgens met behulp van Hallo autocluster algoritme. 

Wanneer u uw eigen query's maakt, moet u controleren of ze correct in Analytics werken voordat u deze tooyour stroom toevoegt.

- Hallo na Analytics query toevoegen en selecteer vervolgens Hallo HTML tabeltype grafiek. 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```
    
    ![De configuratie queryvenster Analytics](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a>Stap 6: Hallo stroom toosend e-mail configureren

1. Klik op **nieuwe stap**, en klik vervolgens op **een actie toevoegen**.
2. Zoeken naar **OfficeOutlook 365**.
3. Klik op **Outlook in Office 365 – stuurt u een e-mailadres**.

    ![Selectievenster voor Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. In Hallo **e-mailbericht verzenden** venster Hallo te volgen:

   a. Typ de e-mailadres Hallo van Hallo ontvanger.

   b. Typ een onderwerp voor Hallo e-mail.

   c. Klik ergens in Hallo **hoofdtekst** vak en selecteer vervolgens op Hallo dynamische inhoud menu dat op het juiste Hallo verschijnt **hoofdtekst**.

   d. Klik op **geavanceerde opties weergeven**.

    ![Outlook-configuratie voor Office 365](./media/app-insights-automate-with-flow/flow5.png)

5. Hallo dynamische inhoud menu Hallo te volgen:

    a. Selecteer **Bijlagenaam**.

    b. Selecteer **bijlage inhoud**.
    
    c. In Hallo **Is HTML** de optie **Ja**.

    ![Venster van Office 365 e-configuratie](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a>Stap 7: Opslaan en testen van uw flow
- In Hallo **stroom naam** vak en klik vervolgens op toevoegen van een naam voor uw flow **stroom maken**.

    ![Venster van de stroom maken](./media/app-insights-automate-with-flow/flow8.png)

U kunt wachten om deze actie op Hallo trigger toorun of kunt u meteen via Hallo stroom uitvoeren [actieve Hallo-trigger op aanvraag](https://flow.microsoft.com/blog/run-now-and-six-more-services/).

Wanneer Hallo stroom wordt uitgevoerd, wordt Hallo ontvangers die u hebt opgegeven in de lijst met e-mailbericht Hallo een e-mailbericht dat op Hallo volgende lijkt:

![Voorbeeldbericht](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a>Volgende stappen

- Meer informatie over het maken van [analysequery's](app-insights-analytics-using.md).
- Meer informatie over [Microsoft Flow](https://ms.flow.microsoft.com).



<!--Link references-->





