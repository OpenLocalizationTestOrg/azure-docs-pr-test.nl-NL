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
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a><span data-ttu-id="5137b-104">Maakt een actie waarschuwing webhook in OMS Log Analytics toosend bericht tooSlack</span><span class="sxs-lookup"><span data-stu-id="5137b-104">Create an alert webhook action in OMS Log Analytics toosend message tooSlack</span></span>
<span data-ttu-id="5137b-105">Een van de Hallo acties die u in het antwoord tooa uitvoeren kunt [logboekanalyse waarschuwing](log-analytics-alerts.md) is een *webhook*, waarmee u tooinvoke een extern proces via één HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="5137b-105">One of hello actions you can run in response tooa [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you tooinvoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="5137b-106">U kunt meer informatie over de details van waarschuwingen en webhooks in [waarschuwingen in Log Analytics](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="5137b-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="5137b-107">In dit artikel behandelen we een voorbeeld van het maken van een webhook actie in een waarschuwing voor logboekanalyse met Slack die een messaging-service.</span><span class="sxs-lookup"><span data-stu-id="5137b-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="5137b-108">Dit voorbeeld moet u een toegestane account toocomplete hebben.</span><span class="sxs-lookup"><span data-stu-id="5137b-108">You must have a Slack account toocomplete this sample.</span></span>  <span data-ttu-id="5137b-109">U kunt zich aanmelden voor een gratis account bij [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="5137b-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="5137b-110">Stap 1 - webhooks in Slack inschakelen</span><span class="sxs-lookup"><span data-stu-id="5137b-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="5137b-111">Meld u aan tooSlack op [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="5137b-111">Sign in tooSlack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="5137b-112">Een kanaal selecteren in Hallo **kanalen** sectie in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="5137b-112">Select a channel in hello **Channels** section in hello left pane.</span></span>  <span data-ttu-id="5137b-113">Dit is Hallo-kanaal dat Hallo-bericht verzonden naar.</span><span class="sxs-lookup"><span data-stu-id="5137b-113">This is hello channel that hello message will be sent to.</span></span>  <span data-ttu-id="5137b-114">U kunt een Hallo standaard kanalen zoals selecteren **algemene** of **willekeurige**.</span><span class="sxs-lookup"><span data-stu-id="5137b-114">You can select one of hello default channels such as **general** or **random**.</span></span>  <span data-ttu-id="5137b-115">In een productiescenario u wilt waarschijnlijk een speciale kanaal maken zoals **criticalservicealerts**.</span><span class="sxs-lookup"><span data-stu-id="5137b-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Slack-kanalen](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="5137b-117">Klik op **toevoegen van een app of aangepaste integratie** tooopen Hallo App-map.</span><span class="sxs-lookup"><span data-stu-id="5137b-117">Click **Add an app or custom integration** tooopen hello App Directory.</span></span>
4. <span data-ttu-id="5137b-118">Type *webhooks* in het zoekvak Hallo en selecteer vervolgens **binnenkomende WebHooks**.</span><span class="sxs-lookup"><span data-stu-id="5137b-118">Type *webhooks* into hello search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Slack-kanalen](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="5137b-120">Klik op **installeren** volgende tooyour Teamnaam.</span><span class="sxs-lookup"><span data-stu-id="5137b-120">Click **Install** next tooyour team name.</span></span>
6. <span data-ttu-id="5137b-121">Klik op **configuratie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5137b-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="5137b-122">Selecteer Hallo Hallo kanaal toouse voor dit voorbeeld gaan en klik vervolgens op **binnenkomende WebHooks toevoegen integratie**.</span><span class="sxs-lookup"><span data-stu-id="5137b-122">Select hello hello channel that you're going toouse for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="5137b-123">Kopiëren Hallo **Webhook-URL**.</span><span class="sxs-lookup"><span data-stu-id="5137b-123">Copy hello **Webhook URL**.</span></span>  <span data-ttu-id="5137b-124">U plakt dit in de configuratie van de waarschuwing Hallo.</span><span class="sxs-lookup"><span data-stu-id="5137b-124">You'll be pasting this into hello Alert configuration.</span></span> <br>
   
    ![Slack-kanalen](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="5137b-126">Stap 2: waarschuwingsregel maken in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="5137b-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="5137b-127">[Een waarschuwingsregel maakt](log-analytics-alerts.md) Hello instellingen te volgen.</span><span class="sxs-lookup"><span data-stu-id="5137b-127">[Create an alert rule](log-analytics-alerts.md) with hello following settings.</span></span>
   * <span data-ttu-id="5137b-128">Query:```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="5137b-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="5137b-129">Controleer voor deze waarschuwing elke: 5 minuten</span><span class="sxs-lookup"><span data-stu-id="5137b-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="5137b-130">het aantal resultaten Hallo: groter is dan 10</span><span class="sxs-lookup"><span data-stu-id="5137b-130">hello number of results is: greater than 10</span></span>
   * <span data-ttu-id="5137b-131">Via dit tijdvenster: 60 minuten</span><span class="sxs-lookup"><span data-stu-id="5137b-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="5137b-132">Selecteer **Ja** voor **Webhook** en **Nee** Hallo voor andere acties.</span><span class="sxs-lookup"><span data-stu-id="5137b-132">Select **Yes** for **Webhook** and **No** for hello other actions.</span></span>
2. <span data-ttu-id="5137b-133">Plakken Hallo Slack-URL in Hallo **Webhook-URL** veld.</span><span class="sxs-lookup"><span data-stu-id="5137b-133">Paste hello Slack URL into hello **Webhook URL** field.</span></span>
3. <span data-ttu-id="5137b-134">Hallo-optie te selecteren**aangepaste JSON-nettolading opnemen**.</span><span class="sxs-lookup"><span data-stu-id="5137b-134">Select hello option too**include a custom JSON payload**.</span></span>
4. <span data-ttu-id="5137b-135">Toegestane verwacht een nettolading in JSON is geformatteerd met een parameter genaamd *tekst*.</span><span class="sxs-lookup"><span data-stu-id="5137b-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="5137b-136">Dit is Hallo-tekst die wordt weergegeven in het maken van het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="5137b-136">This is hello text that it will display in hello message it creates.</span></span>  <span data-ttu-id="5137b-137">U kunt een of meer Waarschuwingsparameters Hallo Hallo met  *#*  zoals zoals in het volgende voorbeeld Hallo symbool.</span><span class="sxs-lookup"><span data-stu-id="5137b-137">You can use one or more of hello alert parameters using hello *#* symbol such as in hello following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![Voorbeeld van de JSON-nettolading](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="5137b-139">Klik op **opslaan** toosave Hallo waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="5137b-139">Click **Save** toosave hello alert rule.</span></span>
6. <span data-ttu-id="5137b-140">Wacht voldoende tijd om een waarschuwing toobe gemaakt en controleer vervolgens de toegestane vertraging voor een bericht vergelijkbaar toohello volgende worden.</span><span class="sxs-lookup"><span data-stu-id="5137b-140">Wait sufficient time for an alert toobe created and then check Slack for a message which will be similar toohello following.</span></span>
   
   ![Voorbeeld van de webhook in Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="5137b-142">Geavanceerde webhook nettolading voor vertraging</span><span class="sxs-lookup"><span data-stu-id="5137b-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="5137b-143">U kunt binnenkomende berichten met Slack grote schaal aanpassen.</span><span class="sxs-lookup"><span data-stu-id="5137b-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="5137b-144">Zie voor meer informatie [binnenkomende Webhooks](https://api.slack.com/incoming-webhooks) op Hallo toegestane website.</span><span class="sxs-lookup"><span data-stu-id="5137b-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on hello Slack website.</span></span> <span data-ttu-id="5137b-145">Hieronder vindt u een complexere nettolading toocreate een uitgebreid bericht met opmaak:</span><span class="sxs-lookup"><span data-stu-id="5137b-145">Following is a more complex payload toocreate a rich message with formatting:</span></span>

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


<span data-ttu-id="5137b-146">Hierdoor zou een bericht gegenereerd in Slack vergelijkbare toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="5137b-146">This would generate a message in Slack similar toohello following.</span></span>

![Voorbeeld van de berichten in Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="5137b-148">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="5137b-148">Summary</span></span>
<span data-ttu-id="5137b-149">Met deze waarschuwingsregel in plaats hebt u een bericht verzonden tooSlack telkens Hallo criteria wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="5137b-149">With this alert rule in place, you would have a message sent tooSlack every time hello criteria is met.</span></span>  

<span data-ttu-id="5137b-150">Dit is slechts één voorbeeld van een actie die u in het antwoord tooan waarschuwing kunt maken.</span><span class="sxs-lookup"><span data-stu-id="5137b-150">This is only one example of an action that you can create in response tooan alert.</span></span>  <span data-ttu-id="5137b-151">U kunt een webhook-actie die een andere externe service, een runbook actie toostart een runbook in Azure Automation, of een e-mailbericht actie toosend aanroept maken een tooyourself e-mail of andere ontvangers.</span><span class="sxs-lookup"><span data-stu-id="5137b-151">You could create a webhook action that calls another external service, a runbook action toostart a runbook in Azure Automation, or an email action toosend a mail tooyourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="5137b-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5137b-152">Next Steps</span></span>
* <span data-ttu-id="5137b-153">Meer informatie over andere [waarschuwing acties in logboekanalyse](log-analytics-alerts-actions.md) met inbegrip van andere acties.</span><span class="sxs-lookup"><span data-stu-id="5137b-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


