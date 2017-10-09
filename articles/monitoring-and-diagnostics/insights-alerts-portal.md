---
title: waarschuwingen voor Azure-services - aaaCreate Azure-portal | Microsoft Docs
description: Trigger e-mailberichten, meldingen, worden URL's van websites (webhooks) of automation aanroepen wanneer Hallo door u opgegeven voorwaarden wordt voldaan.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="9517f-103">Metrische waarschuwingen in de Azure-Monitor maken voor Azure-services - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9517f-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9517f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="9517f-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="9517f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9517f-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="9517f-106">CLI</span><span class="sxs-lookup"><span data-stu-id="9517f-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="9517f-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="9517f-107">Overview</span></span>
<span data-ttu-id="9517f-108">Dit artikel laat zien hoe tooset Azure metrische waarschuwingen met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9517f-108">This article shows you how tooset up Azure metric alerts using hello Azure portal.</span></span>   

<span data-ttu-id="9517f-109">U kunt een waarschuwing op basis van bewaking metrische gegevens voor of gebeurtenissen op uw Azure-services kunt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="9517f-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="9517f-110">**Metrische waarden** - hello triggers waarschuwen wanneer Hallo-waarde van een opgegeven metriek overschrijdt de drempelwaarde die u in beide richtingen toewijst.</span><span class="sxs-lookup"><span data-stu-id="9517f-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="9517f-111">Dat wil zeggen, deze beide wordt geactiveerd wanneer eerst aan Hallo voorwaarde wordt voldaan en vervolgens later wanneer die voorwaarde wordt niet langer wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="9517f-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="9517f-112">**Activiteit logboekgebeurtenissen** -een waarschuwing kunt activeren voor *elke* gebeurtenis of alleen wanneer een bepaalde gebeurtenissen optreden.</span><span class="sxs-lookup"><span data-stu-id="9517f-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="9517f-113">meer informatie over de activiteit logboek waarschuwingen toolearn [Klik hier](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="9517f-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="9517f-114">Een metriek waarschuwing toodo Hallo volgen wanneer deze wordt geactiveerd, kunt u configureren:</span><span class="sxs-lookup"><span data-stu-id="9517f-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="9517f-115">verzenden van e-mailmeldingen toohello servicebeheerder en medebeheerders</span><span class="sxs-lookup"><span data-stu-id="9517f-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="9517f-116">e-mail verzenden tooadditional e-mails die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="9517f-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="9517f-117">een webhook aanroepen</span><span class="sxs-lookup"><span data-stu-id="9517f-117">call a webhook</span></span>
* <span data-ttu-id="9517f-118">starten van de uitvoering van een Azure-runbook (alleen van hello Azure-portal)</span><span class="sxs-lookup"><span data-stu-id="9517f-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="9517f-119">U kunt configureren en ophalen van informatie over metrische waarschuwingsregels met</span><span class="sxs-lookup"><span data-stu-id="9517f-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="9517f-120">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9517f-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="9517f-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9517f-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="9517f-122">opdrachtregelinterface (CLI)</span><span class="sxs-lookup"><span data-stu-id="9517f-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="9517f-123">Monitor voor Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="9517f-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a><span data-ttu-id="9517f-124">Een waarschuwingsregel maken op een metriek Hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9517f-124">Create an alert rule on a metric with hello Azure portal</span></span>
1. <span data-ttu-id="9517f-125">In Hallo [portal](https://portal.azure.com/), zoekt Hallo resource u geïnteresseerd bent in de bewaking en selecteert u deze.</span><span class="sxs-lookup"><span data-stu-id="9517f-125">In hello [portal](https://portal.azure.com/), locate hello resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="9517f-126">Selecteer **waarschuwingen** of **waarschuwing regels** onder Hallo sectie bewaking.</span><span class="sxs-lookup"><span data-stu-id="9517f-126">Select **Alerts** or **Alert rules** under hello MONITORING section.</span></span> <span data-ttu-id="9517f-127">tekst Hello en pictogram kunnen enigszins verschillen voor verschillende resources.</span><span class="sxs-lookup"><span data-stu-id="9517f-127">hello text and icon may vary slightly for different resources.</span></span>  

    ![Bewaking](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="9517f-129">Selecteer Hallo **waarschuwing toevoegen** opdracht en Hallo invullen.</span><span class="sxs-lookup"><span data-stu-id="9517f-129">Select hello **Add alert** command and fill in hello fields.</span></span>

    ![Waarschuwing toevoegen](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="9517f-131">**Naam** uw Waarschuwing regel en kies een **beschrijving**, die ook weergegeven in e-mailmeldingen.</span><span class="sxs-lookup"><span data-stu-id="9517f-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="9517f-132">Selecteer Hallo **metriek** u wilt dat toomonitor en kies vervolgens een **voorwaarde** en **drempelwaarde** waarde voor metriek Hallo.</span><span class="sxs-lookup"><span data-stu-id="9517f-132">Select hello **Metric** you want toomonitor, then choose a **Condition** and **Threshold** value for hello metric.</span></span> <span data-ttu-id="9517f-133">Hallo hebt gekozen **periode** hoelang Hallo metriek regel moet worden voldaan voordat de waarschuwing Hallo-triggers.</span><span class="sxs-lookup"><span data-stu-id="9517f-133">Also chose hello **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span> <span data-ttu-id="9517f-134">Dus bijvoorbeeld, als u Hallo periode 'PT5M' en de waarschuwing CPU dan 80 zoekt %, Hallo waarschuwing wordt geactiveerd wanneer Hallo CPU is al consistent bovenstaande 80% 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="9517f-134">So for example, if you use hello period "PT5M" and your alert looks for CPU above 80%, hello alert triggers when hello CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="9517f-135">Zodra de eerste trigger Hallo plaatsvindt, deze opnieuw wordt geactiveerd wanneer Hallo CPU onder 80% gedurende vijf minuten blijft.</span><span class="sxs-lookup"><span data-stu-id="9517f-135">Once hello first trigger occurs, it again triggers when hello CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="9517f-136">Hallo meting van CPU doet zich voor elke 1 minuut.</span><span class="sxs-lookup"><span data-stu-id="9517f-136">hello CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="9517f-137">Controleer **e-eigenaars...**  als u wilt dat beheerders en medebeheerders toobe per e-mail verzonden wanneer Hallo waarschuwing wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="9517f-137">Check **Email owners...** if you want administrators and co-administrators toobe emailed when hello alert fires.</span></span>

7. <span data-ttu-id="9517f-138">Als u aanvullende e-mailberichten tooreceive een melding wanneer hello wilt waarschuwing wordt geactiveerd, toe te voegen in Hallo **aanvullende beheerder email(s)** veld.</span><span class="sxs-lookup"><span data-stu-id="9517f-138">If you want additional emails tooreceive a notification when hello alert fires, add them in hello **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="9517f-139">Scheid meerdere e-mailberichten met puntkomma's -  *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="9517f-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="9517f-140">In een geldige URI in Hallo plaatsen **Webhook** veld als u wilt dat deze wordt aangeroepen wanneer Hallo waarschuwing wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="9517f-140">Put in a valid URI in hello **Webhook** field if you want it called when hello alert fires.</span></span>

9. <span data-ttu-id="9517f-141">Als u Azure Automation gebruikt, kunt u een Runbook toobe uitgevoerd wanneer het Hallo-waarschuwing wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="9517f-141">If you use Azure Automation, you can select a Runbook toobe run when hello alert fires.</span></span>

10. <span data-ttu-id="9517f-142">Selecteer **OK** wanneer gereed toocreate Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="9517f-142">Select **OK** when done toocreate hello alert.</span></span>   

<span data-ttu-id="9517f-143">Binnen een paar minuten Hallo waarschuwing actief is en wordt geactiveerd als eerder beschreven.</span><span class="sxs-lookup"><span data-stu-id="9517f-143">Within a few minutes, hello alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="9517f-144">Uw waarschuwingen beheren</span><span class="sxs-lookup"><span data-stu-id="9517f-144">Managing your alerts</span></span>
<span data-ttu-id="9517f-145">Wanneer u een waarschuwing hebt gemaakt, kunt u deze selecteren en:</span><span class="sxs-lookup"><span data-stu-id="9517f-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="9517f-146">Een grafiek weer met Hallo metrische drempel en de werkelijke waarden van Hallo Hallo vorige dag weergeven.</span><span class="sxs-lookup"><span data-stu-id="9517f-146">View a graph showing hello metric threshold and hello actual values from hello previous day.</span></span>
* <span data-ttu-id="9517f-147">Bewerk of verwijder deze.</span><span class="sxs-lookup"><span data-stu-id="9517f-147">Edit or delete it.</span></span>
* <span data-ttu-id="9517f-148">**Schakel** of **inschakelen** als u wilt dat tootemporarily stoppen of te hervatten ontvangen van meldingen voor deze waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="9517f-148">**Disable** or **Enable** it if you want tootemporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9517f-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9517f-149">Next steps</span></span>
* <span data-ttu-id="9517f-150">[Een overzicht van Azure monitoring](monitoring-overview.md) inclusief Hallo typen gegevens u kunt verzamelen en controleren.</span><span class="sxs-lookup"><span data-stu-id="9517f-150">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="9517f-151">Meer informatie over [configureren van webhooks in waarschuwingen](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="9517f-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="9517f-152">Meer informatie over [waarschuwingen configureren op activiteit logboekgebeurtenissen](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="9517f-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="9517f-153">Meer informatie over [Azure Automation-Runbooks](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="9517f-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="9517f-154">Ophalen van een [overzicht van diagnostische logboeken](monitoring-overview-of-diagnostic-logs.md) en gedetailleerde hoge frequentie metrische gegevens verzamelen over uw service.</span><span class="sxs-lookup"><span data-stu-id="9517f-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="9517f-155">Ophalen van een [overzicht van metrische gegevens verzameling](insights-how-to-customize-monitoring.md) toomake ervoor dat uw service beschikbaar is en reageert.</span><span class="sxs-lookup"><span data-stu-id="9517f-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
