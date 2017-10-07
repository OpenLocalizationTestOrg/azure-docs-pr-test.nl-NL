---
title: waarschuwingen voor Azure-services - platformoverschrijdende CLI aaaCreate | Microsoft Docs
description: Trigger e-mailberichten, meldingen, worden URL's van websites (webhooks) of automation aanroepen wanneer Hallo door u opgegeven voorwaarden wordt voldaan.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="ee4cb-103">Metrische waarschuwingen maken in de Azure-Monitor voor Azure-services - platformoverschrijdende CLI</span><span class="sxs-lookup"><span data-stu-id="ee4cb-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee4cb-104">Portal</span><span class="sxs-lookup"><span data-stu-id="ee4cb-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="ee4cb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee4cb-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="ee4cb-106">CLI</span><span class="sxs-lookup"><span data-stu-id="ee4cb-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="ee4cb-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ee4cb-107">Overview</span></span>
<span data-ttu-id="ee4cb-108">Dit artikel laat zien hoe tooset Azure metrische waarschuwingen met behulp van Hallo platformoverschrijdende opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="ee4cb-108">This article shows you how tooset up Azure metric alerts using hello cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="ee4cb-109">Nieuwe naam op voor het zogenoemde 'Azure Insights' hello is Azure Monitor tot 25 september 2016.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-109">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="ee4cb-110">Echter bevatten Hallo naamruimten, en daarom onderstaande Hallo-opdrachten nog steeds Hallo 'insights'.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-110">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
>
>

<span data-ttu-id="ee4cb-111">U kunt een waarschuwing op basis van bewaking metrische gegevens voor of gebeurtenissen op uw Azure-services kunt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="ee4cb-112">**Metrische waarden** - hello triggers waarschuwen wanneer Hallo-waarde van een opgegeven metriek overschrijdt de drempelwaarde die u in beide richtingen toewijst.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-112">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="ee4cb-113">Dat wil zeggen, deze beide wordt geactiveerd wanneer eerst aan Hallo voorwaarde wordt voldaan en vervolgens later wanneer die voorwaarde wordt niet langer wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-113">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="ee4cb-114">**Activiteit logboekgebeurtenissen** -een waarschuwing kunt activeren voor *elke* gebeurtenis of alleen wanneer een bepaalde gebeurtenissen optreden.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="ee4cb-115">meer informatie over de activiteit logboek waarschuwingen toolearn [Klik hier](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="ee4cb-115">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="ee4cb-116">Een metriek waarschuwing toodo Hallo volgen wanneer deze wordt geactiveerd, kunt u configureren:</span><span class="sxs-lookup"><span data-stu-id="ee4cb-116">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="ee4cb-117">verzenden van e-mailmeldingen toohello servicebeheerder en medebeheerders</span><span class="sxs-lookup"><span data-stu-id="ee4cb-117">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="ee4cb-118">e-mail verzenden tooadditional e-mails die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-118">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="ee4cb-119">een webhook aanroepen</span><span class="sxs-lookup"><span data-stu-id="ee4cb-119">call a webhook</span></span>
* <span data-ttu-id="ee4cb-120">uitvoering van een Azure-runbook (alleen van hello Azure-portal op dit moment) starten</span><span class="sxs-lookup"><span data-stu-id="ee4cb-120">start execution of an Azure runbook (only from hello Azure portal at this time)</span></span>

<span data-ttu-id="ee4cb-121">U kunt configureren en ophalen van informatie over metrische waarschuwingsregels met</span><span class="sxs-lookup"><span data-stu-id="ee4cb-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="ee4cb-122">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ee4cb-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="ee4cb-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee4cb-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="ee4cb-124">opdrachtregelinterface (CLI)</span><span class="sxs-lookup"><span data-stu-id="ee4cb-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="ee4cb-125">Monitor voor Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="ee4cb-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="ee4cb-126">U kunt altijd help voor opdrachten ontvangen door een opdracht te typen en stellen - help aan Hallo einde.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-126">You can always receive help for commands by typing a command and putting -help at hello end.</span></span> <span data-ttu-id="ee4cb-127">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ee4cb-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a><span data-ttu-id="ee4cb-128">Waarschuwingsregels met Hallo CLI maken</span><span class="sxs-lookup"><span data-stu-id="ee4cb-128">Create alert rules using hello CLI</span></span>
1. <span data-ttu-id="ee4cb-129">Hallo-vereisten en aanmelding tooAzure uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-129">Perform hello Prerequisites and login tooAzure.</span></span> <span data-ttu-id="ee4cb-130">Zie [Azure Monitor CLI voorbeelden](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ee4cb-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="ee4cb-131">Kort gezegd: Hallo CLI installeren en voer deze opdrachten.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-131">In short, install hello CLI and run these commands.</span></span> <span data-ttu-id="ee4cb-132">Ze u aangemeld, welk abonnement u gebruikt en u zich voorbereiden toorun Azure Monitor opdrachten weergeven.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-132">They get you logged in, show what subscription you are using, and prepare you toorun Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="ee4cb-133">toolist bestaande regels voor een resourcegroep gebruiken Hallo formulier na **inzicht van azure waarschuwingen regel lijst** *[opties] &lt;resourceGroup&gt;*</span><span class="sxs-lookup"><span data-stu-id="ee4cb-133">toolist existing rules on a resource group, use hello following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="ee4cb-134">toocreate een regel, moet u toohave belangrijke stukjes informatie eerst.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-134">toocreate a rule, you need toohave several important pieces of information first.</span></span>
  * <span data-ttu-id="ee4cb-135">Hallo **Resource-ID** voor Hallo resource gewenste tooset een waarschuwing voor</span><span class="sxs-lookup"><span data-stu-id="ee4cb-135">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="ee4cb-136">Hallo **metrische definities** beschikbaar voor die bron</span><span class="sxs-lookup"><span data-stu-id="ee4cb-136">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="ee4cb-137">Eenzijdige tooget Hallo Resource-ID is toouse hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-137">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="ee4cb-138">Hallo-bron ervan uitgaande dat al is gemaakt, selecteert u deze in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-138">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="ee4cb-139">Selecteer in de volgende blade Hallo *eigenschappen* onder Hallo *instellingen* sectie.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-139">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="ee4cb-140">Hallo *RESOURCE-ID* is een veld in de volgende Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-140">hello *RESOURCE ID* is a field in hello next blade.</span></span> <span data-ttu-id="ee4cb-141">Een andere manier is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ee4cb-141">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="ee4cb-142">Een voorbeeld van de resource-id voor een web-app is</span><span class="sxs-lookup"><span data-stu-id="ee4cb-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="ee4cb-143">tooget een lijst met beschikbare metrische gegevens Hallo en eenheden voor deze metrische gegevens bijvoorbeeld Hallo vorige resource gebruik Hallo CLI-opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="ee4cb-143">tooget a list of hello available metrics and units for those metrics for hello previous resource example, use hello following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="ee4cb-144">*PT1M* Hallo granulatie van Hallo beschikbaar meting (1 minuut intervallen) is.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-144">*PT1M* is hello granularity of hello available measurement (1-minute intervals).</span></span> <span data-ttu-id="ee4cb-145">Met andere granulaties hebt u verschillende metrische opties.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="ee4cb-146">toocreate een metriek gebaseerde waarschuwingsregel, gebruikt u een opdracht Hallo formulier te volgen:</span><span class="sxs-lookup"><span data-stu-id="ee4cb-146">toocreate a metric-based alert rule, use a command of hello following form:</span></span>

    <span data-ttu-id="ee4cb-147">**inzicht van Azure waarschuwingen metrische regelset** *[opties] &lt;ruleName&gt; &lt;locatie&gt; &lt;resourceGroup&gt; &lt;venstergrootte &gt; &lt;operator&gt; &lt;drempelwaarde&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt; timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="ee4cb-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="ee4cb-148">Hallo volgende voorbeeld wordt u een waarschuwing voor een bron voor de website.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-148">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="ee4cb-149">Hallo waarschuwing activeert wanneer het consistent verkeer ontvangt voor 5 minuten en opnieuw wanneer er geen verkeer ontvangen gedurende vijf minuten.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-149">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="ee4cb-150">toocreate webhook verzenden e-mailadres of wanneer een waarschuwing voor metrische wordt gestart, maakt u eerst Hallo e-mailadres en/of webhooks.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-150">toocreate webhook or send email when a metric alert fires, first create hello email and/or webhooks.</span></span> <span data-ttu-id="ee4cb-151">Vervolgens maakt u de regel Hallo onmiddellijk daarna.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-151">Then create hello rule immediately afterwards.</span></span> <span data-ttu-id="ee4cb-152">Kan geen koppelt u webhook of e-mailberichten met regels die gebruikmaken van Hallo CLI al is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-152">You cannot associate webhook or emails with already created rules using hello CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="ee4cb-153">U kunt controleren of uw waarschuwingen correct zijn gemaakt door te kijken op een afzonderlijke regel.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="ee4cb-154">toodelete regels, gebruikt u een opdracht Hallo vorm:</span><span class="sxs-lookup"><span data-stu-id="ee4cb-154">toodelete rules, use a command of hello form:</span></span>

    <span data-ttu-id="ee4cb-155">**Waarschuwingen regel verwijderen Insights** [opties] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="ee4cb-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="ee4cb-156">Deze opdrachten Verwijder Hallo-regels die eerder in dit artikel hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-156">These commands delete hello rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="ee4cb-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ee4cb-157">Next steps</span></span>
* <span data-ttu-id="ee4cb-158">[Een overzicht van Azure monitoring](monitoring-overview.md) inclusief Hallo typen gegevens u kunt verzamelen en controleren.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-158">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="ee4cb-159">Meer informatie over [configureren van webhooks in waarschuwingen](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="ee4cb-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="ee4cb-160">Meer informatie over [waarschuwingen configureren op activiteit logboekgebeurtenissen](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="ee4cb-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="ee4cb-161">Meer informatie over [Azure Automation-Runbooks](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="ee4cb-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="ee4cb-162">Ophalen van een [overzicht van het verzamelen van diagnostische logboeken](monitoring-overview-of-diagnostic-logs.md) toocollect gedetailleerde hoge frequentie metrische gegevens over uw service.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="ee4cb-163">Ophalen van een [overzicht van metrische gegevens verzameling](insights-how-to-customize-monitoring.md) toomake ervoor dat uw service beschikbaar is en reageert.</span><span class="sxs-lookup"><span data-stu-id="ee4cb-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
