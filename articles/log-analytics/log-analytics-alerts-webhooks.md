---
title: Voorbeeld van aaaWebhook meldingsactie in OMS Log Analytics | Microsoft Docs
description: "Een van de Hallo acties u kunt uitvoeren in het antwoord tooa logboekanalyse waarschuwing is een * webhook *, zodat u tooinvoke een extern proces via één HTTP-aanvraag. In dit artikel wordt een voorbeeld van het maken van een webhook actie in een waarschuwing voor logboekanalyse met Slack uitgelegd."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a>Maakt een actie waarschuwing webhook in OMS Log Analytics toosend bericht tooSlack
Een van de Hallo acties die u in het antwoord tooa uitvoeren kunt [logboekanalyse waarschuwing](log-analytics-alerts.md) is een *webhook*, waarmee u tooinvoke een extern proces via één HTTP-aanvraag.  U kunt meer informatie over de details van waarschuwingen en webhooks in [waarschuwingen in Log Analytics](log-analytics-alerts.md)

In dit artikel behandelen we een voorbeeld van het maken van een webhook actie in een waarschuwing voor logboekanalyse met Slack die een messaging-service.

> [!NOTE]
> Dit voorbeeld moet u een toegestane account toocomplete hebben.  U kunt zich aanmelden voor een gratis account bij [slack.com](http://slack.com).
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a>Stap 1 - webhooks in Slack inschakelen
1. Meld u aan tooSlack op [slack.com](http://slack.com).
2. Een kanaal selecteren in Hallo **kanalen** sectie in het linkerdeelvenster Hallo.  Dit is Hallo-kanaal dat Hallo-bericht verzonden naar.  U kunt een Hallo standaard kanalen zoals selecteren **algemene** of **willekeurige**.  In een productiescenario u wilt waarschijnlijk een speciale kanaal maken zoals **criticalservicealerts**. <br>
   
   ![Slack-kanalen](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. Klik op **toevoegen van een app of aangepaste integratie** tooopen Hallo App-map.
4. Type *webhooks* in het zoekvak Hallo en selecteer vervolgens **binnenkomende WebHooks**. <br>
   
   ![Slack-kanalen](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. Klik op **installeren** volgende tooyour Teamnaam.
6. Klik op **configuratie toevoegen**.
7. Selecteer Hallo Hallo kanaal toouse voor dit voorbeeld gaan en klik vervolgens op **binnenkomende WebHooks toevoegen integratie**.  
8. Kopiëren Hallo **Webhook-URL**.  U plakt dit in de configuratie van de waarschuwing Hallo. <br>
   
    ![Slack-kanalen](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a>Stap 2: waarschuwingsregel maken in Log Analytics
1. [Een waarschuwingsregel maakt](log-analytics-alerts.md) Hello instellingen te volgen.
   * Query:```    Type=Event EventLevelName=error ```
   * Controleer voor deze waarschuwing elke: 5 minuten
   * het aantal resultaten Hallo: groter is dan 10
   * Via dit tijdvenster: 60 minuten
   * Selecteer **Ja** voor **Webhook** en **Nee** Hallo voor andere acties.
2. Plakken Hallo Slack-URL in Hallo **Webhook-URL** veld.
3. Hallo-optie te selecteren**aangepaste JSON-nettolading opnemen**.
4. Toegestane verwacht een nettolading in JSON is geformatteerd met een parameter genaamd *tekst*.  Dit is Hallo-tekst die wordt weergegeven in het maken van het Hallo-bericht.  U kunt een of meer Waarschuwingsparameters Hallo Hallo met  *#*  zoals zoals in het volgende voorbeeld Hallo symbool.
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![Voorbeeld van de JSON-nettolading](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. Klik op **opslaan** toosave Hallo waarschuwingsregel.
6. Wacht voldoende tijd om een waarschuwing toobe gemaakt en controleer vervolgens de toegestane vertraging voor een bericht vergelijkbaar toohello volgende worden.
   
   ![Voorbeeld van de webhook in Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a>Geavanceerde webhook nettolading voor vertraging
U kunt binnenkomende berichten met Slack grote schaal aanpassen. Zie voor meer informatie [binnenkomende Webhooks](https://api.slack.com/incoming-webhooks) op Hallo toegestane website. Hieronder vindt u een complexere nettolading toocreate een uitgebreid bericht met opmaak:

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


Hierdoor zou een bericht gegenereerd in Slack vergelijkbare toohello volgende.

![Voorbeeld van de berichten in Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a>Samenvatting
Met deze waarschuwingsregel in plaats hebt u een bericht verzonden tooSlack telkens Hallo criteria wordt voldaan.  

Dit is slechts één voorbeeld van een actie die u in het antwoord tooan waarschuwing kunt maken.  U kunt een webhook-actie die een andere externe service, een runbook actie toostart een runbook in Azure Automation, of een e-mailbericht actie toosend aanroept maken een tooyourself e-mail of andere ontvangers.   

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over andere [waarschuwing acties in logboekanalyse](log-analytics-alerts-actions.md) met inbegrip van andere acties.


