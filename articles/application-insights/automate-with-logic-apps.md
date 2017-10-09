---
title: aaaAutomate Azure Application Insights verwerkt met behulp van Logic Apps.
description: Meer informatie over hoe u snel herhaalbare processen kunt automatiseren door Hallo Application Insights-connector tooyour logische app toe te voegen.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a>Application Insights-processen automatiseren met behulp van Logic Apps

Vindt u uzelf herhaaldelijk Hallo dezelfde query's uitvoeren op uw gegevens telemetrie toocheck of uw service goed werkt? Zoek tooautomate zijn deze query's voor het vinden van trends en afwijkingen en vervolgens uw eigen werkstromen omheen te bouwen? Hello Azure Application Insights-connector (preview) voor Logic Apps is de juiste hulpprogramma Hallo voor dit doel.

Met deze integratie kunt u meerdere processen automatiseren zonder een één regel code te schrijven. U kunt een logische app maken met Application Insights Hallo connector tooquickly een Application Insights-proces automatiseren. 

U kunt ook aanvullende acties toevoegen. Hallo Logic Apps-functie van Azure App Service kunt u honderden acties beschikbaar. Bijvoorbeeld, met behulp van een logische app, kunt u automatisch een e-mailmelding verzenden of maken van een bug in Visual Studio Team Services. U kunt ook een gebruiken Hallo veel beschikbaar [sjablonen](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp versnellen Hallo-proces voor het maken van uw logische app. 

## <a name="create-a-logic-app-for-application-insights"></a>Een logische app maken voor Application Insights

In deze zelfstudie leert u hoe toocreate een logische app die gebruikmaakt van Hallo Analytics autocluster algoritme toogroup kenmerken in Hallo-gegevens voor een webtoepassing. Hallo resultaten verzonden Hallo stroom automatisch via e-mail, slechts één voorbeeld van hoe u kunt Application Insights Analytics en Logic Apps samen gebruiken. 

### <a name="step-1-create-a-logic-app"></a>Stap 1: Een logische app maken
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. In Hallo **nieuw** deelvenster **Web en mobiel**, en selecteer vervolgens **logische App**.

    ![Nieuwe logische app venster](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a>Stap 2: Een trigger voor uw logische app maken
1. In Hallo **Logic App-ontwerper** venster onder **beginnen met een algemene trigger**, selecteer **terugkeerpatroon**.

    ![Logic App Designer-venster](./media/automate-with-logic-apps/logicapp2.png)

2. In Hallo **frequentie** de optie **dag** en klikt u op Hallo **Interval** in het vak **1**.

    ![Logic App-ontwerper "Recurrence" venster](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a>Stap 3: Een Application Insights-actie toevoegen
1. Klik op **nieuwe stap**, en klik vervolgens op **een actie toevoegen**.

2. In Hallo **kiest u een actie** zoekvak, type **Azure Application Insights**.

3. Onder **acties**, klikt u op **Azure Application Insights – visualiseren Analytics query Preview**.

    ![Logic App-ontwerper 'Kies een actie' venster](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Stap 4: Verbinding maken met tooan Application Insights-resource

toocomplete deze stap moet u een toepassings-ID en een API-sleutel voor uw resource. U kunt ze ophalen uit hello Azure-portal, zoals wordt weergegeven in het volgende diagram Hallo:

![Toepassings-ID in hello Azure-portal](./media/automate-with-logic-apps/appid.png) 

Geef een naam voor uw verbinding, het Hallo toepassings-ID en het Hallo-API-sleutel.

![Venster Logic App-ontwerper stroom-verbinding](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Stap 5: Hallo Analytics-query en grafiektype opgeven
In Hallo voorbeeld te volgen, Hallo query Hallo is mislukt-aanvragen in Hallo laatste dag selecteert en verbindt deze met uitzonderingen die zijn opgetreden tijdens het Hallo-bewerking. Analytics correleert Hallo kan aanvragen, op basis van Hallo operation_Id id. Hallo resultaten segmenten Hallo query vervolgens met behulp van Hallo autocluster algoritme. 

Wanneer u uw eigen query's maakt, moet u controleren of ze correct in Analytics werken voordat u deze tooyour stroom toevoegt.

1. In Hallo **Query** Voeg Hallo Analytics-query te volgen: 

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

2. In Hallo **grafiektype** de optie **HTML-tabel**.

    ![De configuratie queryvenster Analytics](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a>Stap 6: Hallo logic app toosend e-mail configureren

1. Klik op **nieuwe stap**, en selecteer vervolgens **een actie toevoegen**.

2. Typ in het zoekvak Hallo **Outlook van Office 365**.

3. Klik op **Outlook in Office 365 – stuurt u een e-mailadres**.

    ![Selectie van Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. In Hallo **e-mailbericht verzenden** venster Hallo te volgen:

   a. Typ de e-mailadres Hallo van Hallo ontvanger.

   b. Typ een onderwerp voor Hallo e-mail.

   c. Klik ergens in Hallo **hoofdtekst** vak en selecteer vervolgens op Hallo dynamische inhoud menu dat op het juiste Hallo verschijnt **hoofdtekst**.

   d. Klik op **geavanceerde opties weergeven**.

      ![Outlook-configuratie voor Office 365](./media/automate-with-logic-apps/flow5.png)

5. Hallo dynamische inhoud menu Hallo te volgen:

    a. Selecteer **Bijlagenaam**.

    b. Selecteer **bijlage inhoud**.
    
    c. In Hallo **Is HTML** de optie **Ja**.

      ![Configuratiescherm voor Office 365-e-mailadres](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a>Stap 7: Opslaan en uw logische app testen
* Klik op **opslaan** toosave uw wijzigingen.

U kunt wachten op Hallo trigger toorun Hallo logische app, of u kunt Hallo logische app onmiddellijk uitvoeren door te selecteren **uitvoeren**.

![Scherm van logische app maken](./media/automate-with-logic-apps/step7.png)

Wanneer uw logische app wordt uitgevoerd, is het Hallo ontvangers die u hebt opgegeven in de lijst met e-mailbericht Hallo ontvangt een e-mail dat op Hallo volgende lijkt:

![Logic app e-mailbericht](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over het maken van [analysequery's](app-insights-analytics-using.md).
- Meer informatie over [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).



<!--Link references-->





