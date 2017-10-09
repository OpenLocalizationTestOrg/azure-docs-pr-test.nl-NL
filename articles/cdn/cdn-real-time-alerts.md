---
title: aaaAzure CDN realtime-waarschuwingen | Microsoft Docs
description: Realtime-waarschuwingen in Microsoft Azure CDN. Realtime waarschuwingen bevatten meldingen over de prestaties van Hallo van Hallo-eindpunten in uw CDN-profiel.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="05446-104">Realtime-waarschuwingen in Microsoft Azure CDN</span><span class="sxs-lookup"><span data-stu-id="05446-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="05446-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="05446-105">Overview</span></span>
<span data-ttu-id="05446-106">Dit document wordt uitgelegd in Microsoft Azure CDN realtime-waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="05446-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="05446-107">Deze functionaliteit biedt realtime meldingen over de prestaties van Hallo van Hallo-eindpunten in uw CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="05446-107">This functionality provides real-time notifications about hello performance of hello endpoints in your CDN profile.</span></span>  <span data-ttu-id="05446-108">U kunt e-mailadres of op basis van HTTP-waarschuwingen instellen:</span><span class="sxs-lookup"><span data-stu-id="05446-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="05446-109">Bandbreedte</span><span class="sxs-lookup"><span data-stu-id="05446-109">Bandwidth</span></span>
* <span data-ttu-id="05446-110">Statuscodes</span><span class="sxs-lookup"><span data-stu-id="05446-110">Status Codes</span></span>
* <span data-ttu-id="05446-111">Cache-statussen</span><span class="sxs-lookup"><span data-stu-id="05446-111">Cache Statuses</span></span>
* <span data-ttu-id="05446-112">Verbindingen</span><span class="sxs-lookup"><span data-stu-id="05446-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="05446-113">Maken van een realtime waarschuwing</span><span class="sxs-lookup"><span data-stu-id="05446-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="05446-114">In Hallo [Azure Portal](https://portal.azure.com), bladeren tooyour CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="05446-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![Blade CDN-profiel](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="05446-116">Blade voor Hallo CDN-profiel, klik op Hallo **beheren** knop.</span><span class="sxs-lookup"><span data-stu-id="05446-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Knop blade CDN-profiel beheren](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="05446-118">Hallo CDN-beheerportal geopend.</span><span class="sxs-lookup"><span data-stu-id="05446-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="05446-119">Houd de muis boven Hallo **Analytics** tabblad en houd de muis boven Hallo **realtime statistieken** doel.</span><span class="sxs-lookup"><span data-stu-id="05446-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="05446-120">Klik op **realtime-waarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="05446-120">Click on **Real-Time Alerts**.</span></span>
   
    ![CDN-beheerportal](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="05446-122">Hallo-lijst met bestaande waarschuwing configuraties (indien aanwezig) wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="05446-122">hello list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="05446-123">Klik op Hallo **waarschuwing toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="05446-123">Click hello **Add Alert** button.</span></span>
   
    ![Knop Waarschuwing toevoegen](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="05446-125">Een formulier voor het maken van een nieuwe waarschuwing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="05446-125">A form for creating a new alert is displayed.</span></span>
   
    ![Nieuwe waarschuwing formulier](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="05446-127">Als u wilt dat deze waarschuwing toobe active wanneer u klikt op **opslaan**, Controleer Hallo **waarschuwing ingeschakeld** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="05446-127">If you want this alert toobe active when you click **Save**, check hello **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="05446-128">Voer een beschrijvende naam voor de waarschuwing in Hallo **naam** veld.</span><span class="sxs-lookup"><span data-stu-id="05446-128">Enter a descriptive name for your alert in hello **Name** field.</span></span>
7. <span data-ttu-id="05446-129">In Hallo **mediatype** vervolgkeuzelijst **HTTP Large Object**.</span><span class="sxs-lookup"><span data-stu-id="05446-129">In hello **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Het mediatype met HTTP-Large Object geselecteerd](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="05446-131">U moet selecteren **HTTP Large Object** als Hallo **mediatype**.</span><span class="sxs-lookup"><span data-stu-id="05446-131">You must select **HTTP Large Object** as hello **Media Type**.</span></span>  <span data-ttu-id="05446-132">Hallo andere opties worden niet gebruikt door **Azure CDN van Verizon**.</span><span class="sxs-lookup"><span data-stu-id="05446-132">hello other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="05446-133">Fout tooselect **HTTP Large Object** , wordt de waarschuwing toonever worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="05446-133">Failure tooselect **HTTP Large Object** will cause your alert toonever be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="05446-134">Maakt een **expressie** toomonitor door het selecteren van een **metriek**, **Operator**, en **activeren waarde**.</span><span class="sxs-lookup"><span data-stu-id="05446-134">Create an **Expression** toomonitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="05446-135">Voor **metriek**, Hallo type bewaakte gewenste voorwaarde selecteren.</span><span class="sxs-lookup"><span data-stu-id="05446-135">For **Metric**, select hello type of condition you want monitored.</span></span>  <span data-ttu-id="05446-136">**Mbps bandbreedte** is Hallo hoeveelheid bandbreedtegebruik in megabits per seconde.</span><span class="sxs-lookup"><span data-stu-id="05446-136">**Bandwidth Mbps** is hello amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="05446-137">**Totaal aantal verbindingen** is het aantal gelijktijdige HTTP-verbindingen tooour Hallo edge-servers.</span><span class="sxs-lookup"><span data-stu-id="05446-137">**Total Connections** is hello number of concurrent HTTP connections tooour edge servers.</span></span>  <span data-ttu-id="05446-138">Zie voor definities van Hallo verschillende cache statussen en statuscodes, [Azure CDN Cache statuscodes](https://msdn.microsoft.com/library/mt759237.aspx) en [Azure CDN HTTP-statuscodes](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="05446-138">For definitions of hello various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="05446-139">**Operator** Hallo rekenkundige operator die zorgt voor de relatie tussen Hallo metriek en Hallo trigger waarde Hallo is.</span><span class="sxs-lookup"><span data-stu-id="05446-139">**Operator** is hello mathematical operator that establishes hello relationship between hello metric and hello trigger value.</span></span>
   * <span data-ttu-id="05446-140">**Activeren van de waarde** is Hallo drempelwaarde in die moet worden voldaan voordat een melding wordt verzonden uit.</span><span class="sxs-lookup"><span data-stu-id="05446-140">**Trigger Value** is hello threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="05446-141">Hallo onderstaand voorbeeld wijst Hallo expressie die ik heb gemaakt dat ik wil een melding krijgen wanneer Hallo 404 statuscodes aantal groter dan 25 is toobe.</span><span class="sxs-lookup"><span data-stu-id="05446-141">In hello below example, hello expression I have created indicates that I would like toobe notified when hello number of 404 status codes is greater than 25.</span></span>
     
     ![Realtime waarschuwing voorbeeldexpressie](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="05446-143">Voor **Interval**, opgeven hoe vaak u graag Hallo expressie, geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="05446-143">For **Interval**, enter how frequently you would like hello expression evaluated.</span></span>
10. <span data-ttu-id="05446-144">In Hallo **meldingen op basis van** vervolgkeuzelijst, selecteer deze optie als u wilt toobe een melding krijgen wanneer hello expressie waar is.</span><span class="sxs-lookup"><span data-stu-id="05446-144">In hello **Notify on** dropdown, select when you would like toobe notified when hello expression is true.</span></span>
    
    * <span data-ttu-id="05446-145">**Start-voorwaarde** geeft aan dat een melding wordt verzonden wanneer Hallo opgegeven voorwaarde voor het eerst wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="05446-145">**Condition Start** indicates that a notification will be sent when hello specified condition is first detected.</span></span>
    * <span data-ttu-id="05446-146">**End-voorwaarde** geeft aan dat een melding wordt verzonden wanneer Hallo opgegeven voorwaarde wordt niet meer gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="05446-146">**Condition End** indicates that a notification will be sent when hello specified condition is no longer detected.</span></span> <span data-ttu-id="05446-147">Deze melding kan alleen worden geactiveerd nadat ons netwerk bewakingssysteem gedetecteerd die Hallo opgegeven veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="05446-147">This notification can only be triggered after our network monitoring system detected that hello specified condition occurred.</span></span>
    * <span data-ttu-id="05446-148">**Continue** geeft aan dat een melding wordt verzonden elke keer dat netwerk bewakingssysteem Hallo detecteert Hallo opgegeven voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="05446-148">**Continuous** indicates that a notification will be sent each time that hello network monitoring system detects hello specified condition.</span></span> <span data-ttu-id="05446-149">Houd er rekening mee dat Hallo netwerk bewaking van systeem wordt alleen controle eenmaal per interval voor Hallo voorwaarde opgegeven.</span><span class="sxs-lookup"><span data-stu-id="05446-149">Keep in mind that hello network monitoring system will only check once per interval for hello specified condition.</span></span>
    * <span data-ttu-id="05446-150">**Voorwaarde begin- en** geeft aan dat een melding wordt verzonden hello eerste keer is dat Hallo opgegeven voorwaarde wordt gedetecteerd en nog een keer wanneer Hallo voorwaarde wordt niet meer gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="05446-150">**Condition Start and End** indicates that a notification will be sent hello first time that hello specified condition is detected and once again when hello condition is no longer detected.</span></span>
11. <span data-ttu-id="05446-151">Als u wilt dat tooreceive meldingen via e-mail, controleert u Hallo **melden via E-mail** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="05446-151">If you want tooreceive notifications by email, check hello **Notify by Email** checkbox.</span></span>  
    
    ![Delen per E-mail formulier](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="05446-153">In Hallo **naar** Voer Hallo e-mailadres u waar u meldingen verzonden.</span><span class="sxs-lookup"><span data-stu-id="05446-153">In hello **To** field, enter hello email address you where you want notifications sent.</span></span> <span data-ttu-id="05446-154">Voor **onderwerp** en **hoofdtekst**, u Hallo standaard laten of kunt u aanpassen op het Hallo-bericht met Hallo **beschikbare trefwoorden** lijst toodynamically invoegen waarschuwingsgegevens wanneer Hallo-bericht is verzonden.</span><span class="sxs-lookup"><span data-stu-id="05446-154">For **Subject** and **Body**, you may leave hello default, or you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="05446-155">U kunt e-mailmelding Hallo testen door te klikken op Hallo **testen melding** knop, maar alleen als Hallo configuratie van de waarschuwing is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="05446-155">You can test hello email notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="05446-156">Als u wilt dat meldingen toobe geboekt tooa webserver, controleert u Hallo **hoogte door HTTP Post** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="05446-156">If you want notifications toobe posted tooa web server, check hello **Notify by HTTP Post** checkbox.</span></span>
    
    ![Melden door HTTP Post-formulier](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="05446-158">In Hallo **Url** Voer Hallo-URL die u waar u het Hallo HTTP-bericht verzonden.</span><span class="sxs-lookup"><span data-stu-id="05446-158">In hello **Url** field, enter hello URL you where you want hello HTTP message posted.</span></span> <span data-ttu-id="05446-159">In Hallo **Headers** textbox Voer Hallo HTTP-headers toobe in Hallo-aanvraag verzonden.</span><span class="sxs-lookup"><span data-stu-id="05446-159">In hello **Headers** textbox, enter hello HTTP headers toobe sent in hello request.</span></span>  <span data-ttu-id="05446-160">Voor **hoofdtekst** kunt u aanpassen op het Hallo-bericht met Hallo **beschikbare trefwoorden** lijst toodynamically invoegen waarschuwingsgegevens wanneer het Hallo-bericht wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="05446-160">For **Body** you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>  <span data-ttu-id="05446-161">**Headers** en **hoofdtekst** standaard tooan XML-nettolading vergelijkbare toohello onderstaand voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="05446-161">**Headers** and **Body** default tooan XML payload similar toohello below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="05446-162">U kunt Hallo HTTP Post-melding testen door te klikken op Hallo **testen melding** knop, maar alleen als Hallo configuratie van de waarschuwing is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="05446-162">You can test hello HTTP Post notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="05446-163">Klik op Hallo **opslaan** knop toosave uw configuratie van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="05446-163">Click hello **Save** button toosave your alert configuration.</span></span>  <span data-ttu-id="05446-164">Als u dit selectievakje inschakelt **waarschuwing ingeschakeld** in stap 5, de waarschuwing is nu actief.</span><span class="sxs-lookup"><span data-stu-id="05446-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05446-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="05446-165">Next Steps</span></span>
* <span data-ttu-id="05446-166">Analyseren [realtime statistieken in Azure CDN](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="05446-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="05446-167">Meer gedetailleerde met dig [geavanceerde HTTP-rapporten](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="05446-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="05446-168">Analyseren [gebruikspatronen](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="05446-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

