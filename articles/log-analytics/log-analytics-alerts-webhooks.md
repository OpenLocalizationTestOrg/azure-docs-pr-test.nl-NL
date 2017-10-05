---
title: Voorbeeld van de Webhook meldingsactie in OMS Log Analytics | Microsoft Docs
description: "Een van de acties die u in reactie op een waarschuwing voor logboekanalyse uitvoeren kunt is een * webhook *, zodat u kunt het aanroepen van een extern proces via één HTTP-aanvraag. In dit artikel wordt een voorbeeld van het maken van een webhook actie in een waarschuwing voor logboekanalyse met Slack uitgelegd."
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
ms.openlocfilehash: 55b66132f7ec5c26c0a7cac1ec0a5c403dbd1082
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-to-send-message-to-slack"></a><span data-ttu-id="4a39d-104">Maken van een actie waarschuwing webhook in OMS Log Analytics bericht te verzenden naar Slack</span><span class="sxs-lookup"><span data-stu-id="4a39d-104">Create an alert webhook action in OMS Log Analytics to send message to Slack</span></span>
<span data-ttu-id="4a39d-105">Een van de acties die u kunt uitvoeren in reactie op een [logboekanalyse waarschuwing](log-analytics-alerts.md) is een *webhook*, waarmee u een extern proces via één HTTP-aanvraag aanroepen.</span><span class="sxs-lookup"><span data-stu-id="4a39d-105">One of the actions you can run in response to a [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you to invoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="4a39d-106">U kunt meer informatie over de details van waarschuwingen en webhooks in [waarschuwingen in Log Analytics](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="4a39d-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="4a39d-107">In dit artikel behandelen we een voorbeeld van het maken van een webhook actie in een waarschuwing voor logboekanalyse met Slack die een messaging-service.</span><span class="sxs-lookup"><span data-stu-id="4a39d-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="4a39d-108">U moet een toegestane account te voltooien in dit voorbeeld hebben.</span><span class="sxs-lookup"><span data-stu-id="4a39d-108">You must have a Slack account to complete this sample.</span></span>  <span data-ttu-id="4a39d-109">U kunt zich aanmelden voor een gratis account bij [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="4a39d-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="4a39d-110">Stap 1 - webhooks in Slack inschakelen</span><span class="sxs-lookup"><span data-stu-id="4a39d-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="4a39d-111">Meld u aan met Slack op [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="4a39d-111">Sign in to Slack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="4a39d-112">Een kanaal selecteren in de **kanalen** sectie in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="4a39d-112">Select a channel in the **Channels** section in the left pane.</span></span>  <span data-ttu-id="4a39d-113">Dit is het kanaal dat het bericht wordt verzonden naar.</span><span class="sxs-lookup"><span data-stu-id="4a39d-113">This is the channel that the message will be sent to.</span></span>  <span data-ttu-id="4a39d-114">U kunt een van de standaard-kanalen zoals selecteren **algemene** of **willekeurige**.</span><span class="sxs-lookup"><span data-stu-id="4a39d-114">You can select one of the default channels such as **general** or **random**.</span></span>  <span data-ttu-id="4a39d-115">In een productiescenario u wilt waarschijnlijk een speciale kanaal maken zoals **criticalservicealerts**.</span><span class="sxs-lookup"><span data-stu-id="4a39d-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Slack-kanalen](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="4a39d-117">Klik op **toevoegen van een app of aangepaste integratie** om de App-map te openen.</span><span class="sxs-lookup"><span data-stu-id="4a39d-117">Click **Add an app or custom integration** to open the App Directory.</span></span>
4. <span data-ttu-id="4a39d-118">Type *webhooks* in het zoekvak en selecteer vervolgens **binnenkomende WebHooks**.</span><span class="sxs-lookup"><span data-stu-id="4a39d-118">Type *webhooks* into the search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Slack-kanalen](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="4a39d-120">Klik op **installeren** naast de teamnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="4a39d-120">Click **Install** next to your team name.</span></span>
6. <span data-ttu-id="4a39d-121">Klik op **configuratie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4a39d-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="4a39d-122">Selecteer de het kanaal dat u wilt gebruiken voor dit voorbeeld en klik vervolgens op **binnenkomende WebHooks toevoegen integratie**.</span><span class="sxs-lookup"><span data-stu-id="4a39d-122">Select the the channel that you're going to use for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="4a39d-123">Kopieer de **Webhook-URL**.</span><span class="sxs-lookup"><span data-stu-id="4a39d-123">Copy the **Webhook URL**.</span></span>  <span data-ttu-id="4a39d-124">U plakt dit in de configuratie van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="4a39d-124">You'll be pasting this into the Alert configuration.</span></span> <br>
   
    ![Slack-kanalen](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="4a39d-126">Stap 2: waarschuwingsregel maken in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4a39d-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="4a39d-127">[Een waarschuwingsregel maakt](log-analytics-alerts.md) met de volgende instellingen.</span><span class="sxs-lookup"><span data-stu-id="4a39d-127">[Create an alert rule](log-analytics-alerts.md) with the following settings.</span></span>
   * <span data-ttu-id="4a39d-128">Query:```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="4a39d-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="4a39d-129">Controleer voor deze waarschuwing elke: 5 minuten</span><span class="sxs-lookup"><span data-stu-id="4a39d-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="4a39d-130">Het aantal resultaten: groter is dan 10</span><span class="sxs-lookup"><span data-stu-id="4a39d-130">The number of results is: greater than 10</span></span>
   * <span data-ttu-id="4a39d-131">Via dit tijdvenster: 60 minuten</span><span class="sxs-lookup"><span data-stu-id="4a39d-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="4a39d-132">Selecteer **Ja** voor **Webhook** en **Nee** voor de andere acties.</span><span class="sxs-lookup"><span data-stu-id="4a39d-132">Select **Yes** for **Webhook** and **No** for the other actions.</span></span>
2. <span data-ttu-id="4a39d-133">Plak de URL van de vertraging in de **Webhook-URL** veld.</span><span class="sxs-lookup"><span data-stu-id="4a39d-133">Paste the Slack URL into the **Webhook URL** field.</span></span>
3. <span data-ttu-id="4a39d-134">Selecteer de optie voor **aangepaste JSON-nettolading opnemen**.</span><span class="sxs-lookup"><span data-stu-id="4a39d-134">Select the option to **include a custom JSON payload**.</span></span>
4. <span data-ttu-id="4a39d-135">Toegestane verwacht een nettolading in JSON is geformatteerd met een parameter genaamd *tekst*.</span><span class="sxs-lookup"><span data-stu-id="4a39d-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="4a39d-136">Dit is de tekst die wordt weergegeven in het bericht dat wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4a39d-136">This is the text that it will display in the message it creates.</span></span>  <span data-ttu-id="4a39d-137">U kunt een of meer van de waarschuwing parameters met de  *#*  symbool zoals zoals in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4a39d-137">You can use one or more of the alert parameters using the *#* symbol such as in the following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds the over threshold of #thresholdvalue ."
    }
    ```
   
    ![Voorbeeld van de JSON-nettolading](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="4a39d-139">Klik op **opslaan** om op te slaan van de waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="4a39d-139">Click **Save** to save the alert rule.</span></span>
6. <span data-ttu-id="4a39d-140">Wacht voldoende tijd om een waarschuwing te worden gemaakt en vervolgens Slack controleren op een bericht dat op het volgende lijkt.</span><span class="sxs-lookup"><span data-stu-id="4a39d-140">Wait sufficient time for an alert to be created and then check Slack for a message which will be similar to the following.</span></span>
   
   ![Voorbeeld van de webhook in Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="4a39d-142">Geavanceerde webhook nettolading voor vertraging</span><span class="sxs-lookup"><span data-stu-id="4a39d-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="4a39d-143">U kunt binnenkomende berichten met Slack grote schaal aanpassen.</span><span class="sxs-lookup"><span data-stu-id="4a39d-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="4a39d-144">Zie voor meer informatie [binnenkomende Webhooks](https://api.slack.com/incoming-webhooks) op de website van de toegestane vertraging.</span><span class="sxs-lookup"><span data-stu-id="4a39d-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on the Slack website.</span></span> <span data-ttu-id="4a39d-145">Hieronder vindt u een complexere nettolading met een uitgebreid bericht met opmaak maken:</span><span class="sxs-lookup"><span data-stu-id="4a39d-145">Following is a more complex payload to create a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link To SearchResults",
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


<span data-ttu-id="4a39d-146">Hierdoor zou een bericht gegenereerd in Slack vergelijkbaar met de volgende.</span><span class="sxs-lookup"><span data-stu-id="4a39d-146">This would generate a message in Slack similar to the following.</span></span>

![Voorbeeld van de berichten in Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="4a39d-148">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="4a39d-148">Summary</span></span>
<span data-ttu-id="4a39d-149">Met deze waarschuwingsregel in plaats hebt u een bericht verzonden met Slack telkens wanneer de criteria wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="4a39d-149">With this alert rule in place, you would have a message sent to Slack every time the criteria is met.</span></span>  

<span data-ttu-id="4a39d-150">Dit is slechts één voorbeeld van een actie die u in reactie op een waarschuwing kunt maken.</span><span class="sxs-lookup"><span data-stu-id="4a39d-150">This is only one example of an action that you can create in response to an alert.</span></span>  <span data-ttu-id="4a39d-151">U kunt een webhook-actie die een andere externe service aanroept, een runbook-actie voor het starten van een runbook in Azure Automation of een e-actie een e-mail te verzenden naar uzelf of naar andere ontvangers maken.</span><span class="sxs-lookup"><span data-stu-id="4a39d-151">You could create a webhook action that calls another external service, a runbook action to start a runbook in Azure Automation, or an email action to send a mail to yourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="4a39d-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4a39d-152">Next Steps</span></span>
* <span data-ttu-id="4a39d-153">Meer informatie over andere [waarschuwing acties in logboekanalyse](log-analytics-alerts-actions.md) met inbegrip van andere acties.</span><span class="sxs-lookup"><span data-stu-id="4a39d-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


