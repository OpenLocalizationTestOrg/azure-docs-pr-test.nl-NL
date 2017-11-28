---
title: Realtime waarschuwingen van Azure CDN | Microsoft Docs
description: Realtime-waarschuwingen in Microsoft Azure CDN. Realtime waarschuwingen bevatten meldingen over de prestaties van de eindpunten in uw CDN-profiel.
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
ms.openlocfilehash: 6e66eb076ac7220823a848b5047f147d4101cd55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="59176-104">Realtime-waarschuwingen in Microsoft Azure CDN</span><span class="sxs-lookup"><span data-stu-id="59176-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="59176-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="59176-105">Overview</span></span>
<span data-ttu-id="59176-106">Dit document wordt uitgelegd in Microsoft Azure CDN realtime-waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="59176-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="59176-107">Deze functionaliteit biedt realtime meldingen over de prestaties van de eindpunten in uw CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="59176-107">This functionality provides real-time notifications about the performance of the endpoints in your CDN profile.</span></span>  <span data-ttu-id="59176-108">U kunt e-mailadres of op basis van HTTP-waarschuwingen instellen:</span><span class="sxs-lookup"><span data-stu-id="59176-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="59176-109">Bandbreedte</span><span class="sxs-lookup"><span data-stu-id="59176-109">Bandwidth</span></span>
* <span data-ttu-id="59176-110">Statuscodes</span><span class="sxs-lookup"><span data-stu-id="59176-110">Status Codes</span></span>
* <span data-ttu-id="59176-111">Cache-statussen</span><span class="sxs-lookup"><span data-stu-id="59176-111">Cache Statuses</span></span>
* <span data-ttu-id="59176-112">Verbindingen</span><span class="sxs-lookup"><span data-stu-id="59176-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="59176-113">Maken van een realtime waarschuwing</span><span class="sxs-lookup"><span data-stu-id="59176-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="59176-114">In de [Azure Portal](https://portal.azure.com), blader naar uw CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="59176-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![Blade CDN-profiel](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="59176-116">Klik in de blade CDN-profiel op de **beheren** knop.</span><span class="sxs-lookup"><span data-stu-id="59176-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Knop blade CDN-profiel beheren](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="59176-118">Hiermee opent u de CDN-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="59176-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="59176-119">Beweeg de muisaanwijzer over de **Analytics** tabblad en klik vervolgens Beweeg de muisaanwijzer over de **realtime statistieken** doel.</span><span class="sxs-lookup"><span data-stu-id="59176-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="59176-120">Klik op **realtime-waarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="59176-120">Click on **Real-Time Alerts**.</span></span>
   
    ![CDN-beheerportal](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="59176-122">De lijst met bestaande waarschuwing configuraties (indien aanwezig) wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="59176-122">The list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="59176-123">Klik op de **waarschuwing toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="59176-123">Click the **Add Alert** button.</span></span>
   
    ![Knop Waarschuwing toevoegen](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="59176-125">Een formulier voor het maken van een nieuwe waarschuwing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="59176-125">A form for creating a new alert is displayed.</span></span>
   
    ![Nieuwe waarschuwing formulier](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="59176-127">Als u wilt dat deze waarschuwing geactiveerd wanneer u klikt op **opslaan**, Controleer de **waarschuwing ingeschakeld** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="59176-127">If you want this alert to be active when you click **Save**, check the **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="59176-128">Voer een beschrijvende naam voor de waarschuwing in de **naam** veld.</span><span class="sxs-lookup"><span data-stu-id="59176-128">Enter a descriptive name for your alert in the **Name** field.</span></span>
7. <span data-ttu-id="59176-129">In de **mediatype** vervolgkeuzelijst **HTTP Large Object**.</span><span class="sxs-lookup"><span data-stu-id="59176-129">In the **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Het mediatype met HTTP-Large Object geselecteerd](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="59176-131">U moet selecteren **HTTP Large Object** als de **mediatype**.</span><span class="sxs-lookup"><span data-stu-id="59176-131">You must select **HTTP Large Object** as the **Media Type**.</span></span>  <span data-ttu-id="59176-132">De andere opties worden niet gebruikt door **Azure CDN van Verizon**.</span><span class="sxs-lookup"><span data-stu-id="59176-132">The other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="59176-133">Fout bij selecteren **HTTP Large Object** , wordt de waarschuwing nooit worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="59176-133">Failure to select **HTTP Large Object** will cause your alert to never be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="59176-134">Maak een **expressie** controleren door te selecteren een **metriek**, **Operator**, en **activeren waarde**.</span><span class="sxs-lookup"><span data-stu-id="59176-134">Create an **Expression** to monitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="59176-135">Voor **metriek**, selecteer het type van de gewenste bewaakte voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="59176-135">For **Metric**, select the type of condition you want monitored.</span></span>  <span data-ttu-id="59176-136">**Mbps bandbreedte** is de hoeveelheid bandbreedte in megabits per seconde.</span><span class="sxs-lookup"><span data-stu-id="59176-136">**Bandwidth Mbps** is the amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="59176-137">**Totaal aantal verbindingen** is het aantal gelijktijdige HTTP-verbindingen naar onze randservers.</span><span class="sxs-lookup"><span data-stu-id="59176-137">**Total Connections** is the number of concurrent HTTP connections to our edge servers.</span></span>  <span data-ttu-id="59176-138">Zie voor definities van de verschillende cache statussen en statuscodes [Azure CDN Cache statuscodes](https://msdn.microsoft.com/library/mt759237.aspx) en [Azure CDN HTTP-statuscodes](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="59176-138">For definitions of the various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="59176-139">**Operator** is de rekenkundige operator die zorgt voor de relatie tussen de metrische gegevens en de trigger-waarde.</span><span class="sxs-lookup"><span data-stu-id="59176-139">**Operator** is the mathematical operator that establishes the relationship between the metric and the trigger value.</span></span>
   * <span data-ttu-id="59176-140">**Activeren van de waarde** is de drempelwaarde in die moet worden voldaan voordat een melding wordt verzonden uit.</span><span class="sxs-lookup"><span data-stu-id="59176-140">**Trigger Value** is the threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="59176-141">In het onderstaande voorbeeld geeft de expressie die ik heb gemaakt dat ik wil worden gewaarschuwd wanneer het aantal 404 statuscodes groter dan 25 is.</span><span class="sxs-lookup"><span data-stu-id="59176-141">In the below example, the expression I have created indicates that I would like to be notified when the number of 404 status codes is greater than 25.</span></span>
     
     ![Realtime waarschuwing voorbeeldexpressie](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="59176-143">Voor **Interval**, opgeven hoe vaak u wilt de geëvalueerde expressie.</span><span class="sxs-lookup"><span data-stu-id="59176-143">For **Interval**, enter how frequently you would like the expression evaluated.</span></span>
10. <span data-ttu-id="59176-144">In de **meldingen op basis van** vervolgkeuzelijst, selecteer deze optie als u een melding krijgen wilt wanneer de expressie waar is.</span><span class="sxs-lookup"><span data-stu-id="59176-144">In the **Notify on** dropdown, select when you would like to be notified when the expression is true.</span></span>
    
    * <span data-ttu-id="59176-145">**Start-voorwaarde** geeft aan dat een melding wordt verzonden wanneer de opgegeven voorwaarde voor het eerst wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="59176-145">**Condition Start** indicates that a notification will be sent when the specified condition is first detected.</span></span>
    * <span data-ttu-id="59176-146">**End-voorwaarde** geeft aan dat een melding wordt verzonden wanneer de opgegeven voorwaarde wordt niet meer gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="59176-146">**Condition End** indicates that a notification will be sent when the specified condition is no longer detected.</span></span> <span data-ttu-id="59176-147">Deze melding kan alleen worden geactiveerd nadat ons netwerk bewakingssysteem gedetecteerd dat de opgegeven voorwaarde opgetreden.</span><span class="sxs-lookup"><span data-stu-id="59176-147">This notification can only be triggered after our network monitoring system detected that the specified condition occurred.</span></span>
    * <span data-ttu-id="59176-148">**Continue** geeft aan dat een melding wordt verzonden elke keer dat het netwerk bewakingssysteem de opgegeven voorwaarde detecteert.</span><span class="sxs-lookup"><span data-stu-id="59176-148">**Continuous** indicates that a notification will be sent each time that the network monitoring system detects the specified condition.</span></span> <span data-ttu-id="59176-149">Houd er rekening mee dat het netwerk bewakingssysteem alleen één keer per interval voor de opgegeven voorwaarde controleert.</span><span class="sxs-lookup"><span data-stu-id="59176-149">Keep in mind that the network monitoring system will only check once per interval for the specified condition.</span></span>
    * <span data-ttu-id="59176-150">**Voorwaarde begin- en** geeft aan dat een melding wordt verzonden de eerste keer dat de opgegeven voorwaarde wordt gedetecteerd en nog een keer als de voorwaarde is niet meer gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="59176-150">**Condition Start and End** indicates that a notification will be sent the first time that the specified condition is detected and once again when the condition is no longer detected.</span></span>
11. <span data-ttu-id="59176-151">Als u meldingen ontvangen via e-mail wilt, controleert u de **melden via E-mail** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="59176-151">If you want to receive notifications by email, check the **Notify by Email** checkbox.</span></span>  
    
    ![Delen per E-mail formulier](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="59176-153">In de **naar** en voer het e-mailadres dat u waar u meldingen verzonden.</span><span class="sxs-lookup"><span data-stu-id="59176-153">In the **To** field, enter the email address you where you want notifications sent.</span></span> <span data-ttu-id="59176-154">Voor **onderwerp** en **hoofdtekst**, mag u laat de standaardwaarde of kunt u aanpassen op het bericht met de **beschikbare trefwoorden** lijst dynamisch invoegen waarschuwingsgegevens wanneer het bericht Er wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="59176-154">For **Subject** and **Body**, you may leave the default, or you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="59176-155">U kunt de e-mailmelding testen door te klikken op de **testen melding** knop, maar alleen als de configuratie van de waarschuwing is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="59176-155">You can test the email notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="59176-156">Als u wilt dat meldingen worden gepubliceerd op een webserver, controleert u de **hoogte door HTTP Post** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="59176-156">If you want notifications to be posted to a web server, check the **Notify by HTTP Post** checkbox.</span></span>
    
    ![Melden door HTTP Post-formulier](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="59176-158">In de **Url** en voer de URL die u waar u het HTTP-bericht verzonden.</span><span class="sxs-lookup"><span data-stu-id="59176-158">In the **Url** field, enter the URL you where you want the HTTP message posted.</span></span> <span data-ttu-id="59176-159">In de **Headers** tekstvak de HTTP-headers worden verzonden in de aanvraag invoeren.</span><span class="sxs-lookup"><span data-stu-id="59176-159">In the **Headers** textbox, enter the HTTP headers to be sent in the request.</span></span>  <span data-ttu-id="59176-160">Voor **hoofdtekst** kunt u aanpassen op het bericht met de **beschikbare trefwoorden** lijst waarschuwingsgegevens dynamisch invoegen wanneer het bericht is verzonden.</span><span class="sxs-lookup"><span data-stu-id="59176-160">For **Body** you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>  <span data-ttu-id="59176-161">**Headers** en **hoofdtekst** standaard naar een XML-nettolading vergelijkbaar met het onderstaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="59176-161">**Headers** and **Body** default to an XML payload similar to the below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="59176-162">U kunt de melding HTTP Post testen door te klikken op de **testen melding** knop, maar alleen als de configuratie van de waarschuwing is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="59176-162">You can test the HTTP Post notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="59176-163">Klik op de **opslaan** om op te slaan van uw configuratie van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="59176-163">Click the **Save** button to save your alert configuration.</span></span>  <span data-ttu-id="59176-164">Als u dit selectievakje inschakelt **waarschuwing ingeschakeld** in stap 5, de waarschuwing is nu actief.</span><span class="sxs-lookup"><span data-stu-id="59176-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59176-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="59176-165">Next Steps</span></span>
* <span data-ttu-id="59176-166">Analyseren [realtime statistieken in Azure CDN](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="59176-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="59176-167">Meer gedetailleerde met dig [geavanceerde HTTP-rapporten](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="59176-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="59176-168">Analyseren [gebruikspatronen](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="59176-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

