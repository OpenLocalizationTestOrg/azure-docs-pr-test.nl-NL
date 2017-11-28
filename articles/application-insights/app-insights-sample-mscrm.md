---
title: aaaMicrosoft Dynamics CRM en Azure Application Insights | Microsoft Docs
description: Telemetrie ophalen uit Microsoft Dynamics CRM Online met behulp van Application Insights. Overzicht van setup ophalen van gegevens, visualisatie en exporteren.
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="22852-104">Overzicht: Telemetrie voor Microsoft Dynamics CRM Online met behulp van Application Insights inschakelen</span><span class="sxs-lookup"><span data-stu-id="22852-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="22852-105">Dit artikel ziet u hoe tooget telemetriegegevens van [Microsoft Dynamics CRM Online](https://www.dynamics.com/) met [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="22852-105">This article shows you how tooget telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="22852-106">We doorlopen Hallo complete proces van Application Insights-script tooyour toepassing toe te voegen, het vastleggen van gegevens en gegevensvisualisatie.</span><span class="sxs-lookup"><span data-stu-id="22852-106">We’ll walk through hello complete process of adding Application Insights script tooyour application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="22852-107">[Hallo Voorbeeldoplossing Bladeren](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="22852-107">[Browse hello sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a><span data-ttu-id="22852-108">Application Insights toonew of bestaande CRM Online-instantie toevoegen</span><span class="sxs-lookup"><span data-stu-id="22852-108">Add Application Insights toonew or existing CRM Online instance</span></span>
<span data-ttu-id="22852-109">toomonitor uw toepassing toevoegen van een Application Insights-SDK tooyour-toepassing.</span><span class="sxs-lookup"><span data-stu-id="22852-109">toomonitor your application, you add an Application Insights SDK tooyour application.</span></span> <span data-ttu-id="22852-110">Hallo SDK verzendt telemetrie toohello [Application Insights-portal](https://portal.azure.com), kunt u gebruik van onze krachtige analyse en diagnostische hulpprogramma's, of Hallo gegevens toostorage exporteren.</span><span class="sxs-lookup"><span data-stu-id="22852-110">hello SDK sends telemetry toohello [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export hello data toostorage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="22852-111">Een Application Insights-resource maken in Azure</span><span class="sxs-lookup"><span data-stu-id="22852-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="22852-112">Ophalen van [een account in Microsoft Azure](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="22852-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="22852-113">Meld u aan bij Hallo [Azure-portal](https://portal.azure.com) en een nieuwe Application Insights-resource toevoegen.</span><span class="sxs-lookup"><span data-stu-id="22852-113">Sign into hello [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="22852-114">Dit is waar uw gegevens worden verwerkt en weergegeven.</span><span class="sxs-lookup"><span data-stu-id="22852-114">This is where your data will be processed and displayed.</span></span>
   
    ![Klik op +, Ontwikkelaarsservices, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="22852-116">Kies ASP.NET als Hallo toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="22852-116">Choose ASP.NET as hello application type.</span></span>
3. <span data-ttu-id="22852-117">Open de pagina aan de slag Hallo en ' bewaken en onderzoeken van client-side '.</span><span class="sxs-lookup"><span data-stu-id="22852-117">Open hello Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Codefragment voor het invoegen in uw webpagina](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="22852-119">**Hallo-codetabel openhouden** terwijl u de volgende stap in een ander browservenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="22852-119">**Keep hello code page open** while you do hello next step in another browser window.</span></span> <span data-ttu-id="22852-120">U moet binnenkort Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="22852-120">You'll need hello code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="22852-121">Een JavaScript-web-resource maken in Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="22852-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="22852-122">Open uw CRM Online-instantie en aanmelding met administrator-bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="22852-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="22852-123">Open Microsoft Dynamics CRM-instellingen aanpassingen, aanpassen Hallo systeem</span><span class="sxs-lookup"><span data-stu-id="22852-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize hello System</span></span>
   
    ![Microsoft Dynamics CRM-instellingen](./media/app-insights-sample-mscrm/04.png)
   
    ![Instellingen > aanpassingen](./media/app-insights-sample-mscrm/05.png)

    ![Hallo Systeemoptie aanpassen](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="22852-127">Maak een JavaScript-resource.</span><span class="sxs-lookup"><span data-stu-id="22852-127">Create a JavaScript resource.</span></span>
   
    ![Dialoogvenster nieuwe webbron](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="22852-129">Geef het een naam, selecteer **Script (JScript)** en open Hallo teksteditor.</span><span class="sxs-lookup"><span data-stu-id="22852-129">Give it a name, select **Script (JScript)** and open hello text editor.</span></span>
   
    ![Open Hallo teksteditor](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="22852-131">Hallo-code van de Application Insights kopiëren.</span><span class="sxs-lookup"><span data-stu-id="22852-131">Copy hello code from Application Insights.</span></span> <span data-ttu-id="22852-132">Zorg ervoor dat tooignore scriptlabels tijdens het kopiëren van.</span><span class="sxs-lookup"><span data-stu-id="22852-132">While copying make sure tooignore script tags.</span></span> <span data-ttu-id="22852-133">Raadpleeg de onderstaande schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="22852-133">Refer below screenshot:</span></span>
   
    ![De instrumentatiesleutel instellen](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="22852-135">Hallo-code bevat Hallo instrumentatiesleutel die uw Application insights-resource identificeert.</span><span class="sxs-lookup"><span data-stu-id="22852-135">hello code includes hello instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="22852-136">Opslaan en publiceren.</span><span class="sxs-lookup"><span data-stu-id="22852-136">Save and publish.</span></span>
   
    ![Opslaan en publiceren](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="22852-138">Instrument formulieren</span><span class="sxs-lookup"><span data-stu-id="22852-138">Instrument Forms</span></span>
1. <span data-ttu-id="22852-139">Open in Microsoft CRM Online formulier Hallo-Account</span><span class="sxs-lookup"><span data-stu-id="22852-139">In Microsoft CRM Online, open hello Account form</span></span>
   
    ![Accountformulier](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="22852-141">Hallo formulier eigenschappen openen</span><span class="sxs-lookup"><span data-stu-id="22852-141">Open hello form Properties</span></span>
   
    ![Eigenschappen van formulier](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="22852-143">Hallo JavaScript webbron die u hebt gemaakt toevoegen</span><span class="sxs-lookup"><span data-stu-id="22852-143">Add hello JavaScript web resource that you created</span></span>
   
    ![Menu toevoegen](./media/app-insights-sample-mscrm/13.png)
   
    ![Hallo webbron toevoegen](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="22852-146">Opslaan en publiceren van uw aanpassingen van formulieren.</span><span class="sxs-lookup"><span data-stu-id="22852-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="22852-147">Metrische gegevens vastgelegd</span><span class="sxs-lookup"><span data-stu-id="22852-147">Metrics captured</span></span>
<span data-ttu-id="22852-148">U hebt nu het vastleggen van telemetriegegevens voor Hallo formulier ingesteld.</span><span class="sxs-lookup"><span data-stu-id="22852-148">You have now set up telemetry capture for hello form.</span></span> <span data-ttu-id="22852-149">Wanneer deze wordt gebruikt, worden gegevens verzonden tooyour Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="22852-149">Whenever it is used, data will be sent tooyour Application Insights resource.</span></span>

<span data-ttu-id="22852-150">Hier vindt u voorbeelden van Hallo-gegevens die u ziet.</span><span class="sxs-lookup"><span data-stu-id="22852-150">Here are samples of hello data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="22852-151">Toepassingsstatus</span><span class="sxs-lookup"><span data-stu-id="22852-151">Application health</span></span>
![Voorbeeld van de paginalaadtijd](./media/app-insights-sample-mscrm/15.png)

![Voorbeeld pagina weergaven grafiek](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="22852-154">Browseruitzonderingen:</span><span class="sxs-lookup"><span data-stu-id="22852-154">Browser exceptions:</span></span>

![Grafiek met serveruitzonderingen klikken](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="22852-156">Klik op Hallo grafiek tooget meer detail:</span><span class="sxs-lookup"><span data-stu-id="22852-156">Click hello chart tooget more detail:</span></span>

![Lijst met uitzonderingen](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="22852-158">Gebruik</span><span class="sxs-lookup"><span data-stu-id="22852-158">Usage</span></span>
![Gebruikers, sessies en paginaweergaven](./media/app-insights-sample-mscrm/19.png)

![Sesion grafieken](./media/app-insights-sample-mscrm/20.png)

![Browserversies](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="22852-162">Browsers</span><span class="sxs-lookup"><span data-stu-id="22852-162">Browsers</span></span>
![Overzicht van de laadtijd van pagina](./media/app-insights-sample-mscrm/22.png)

![Het aantal sessies per browserversie](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="22852-165">Geolocatie</span><span class="sxs-lookup"><span data-stu-id="22852-165">Geolocation</span></span>
![Het aantal sessies per land](./media/app-insights-sample-mscrm/24.png)

![Sessies en gebruikers per land](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="22852-168">Inside pagina-aanvraag voor weergave</span><span class="sxs-lookup"><span data-stu-id="22852-168">Inside page view request</span></span>
![Overzicht van de pagina weergeven](./media/app-insights-sample-mscrm/26.png)

![Zoeken op de pagina-gebeurtenissen weergeven](./media/app-insights-sample-mscrm/27.png)

![Vergelijkbare paginaweergaven](./media/app-insights-sample-mscrm/28.png)

![Eigenschappen van paginaweergaven](./media/app-insights-sample-mscrm/29.png)

![Pagina's per sessie](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="22852-174">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="22852-174">Sample code</span></span>
<span data-ttu-id="22852-175">[Hallo voorbeeldcode Bladeren](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="22852-175">[Browse hello sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="22852-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="22852-176">Power BI</span></span>
<span data-ttu-id="22852-177">U kunt zelfs grondigere analyse doen als u [exporteren Hallo gegevens tooMicrosoft Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="22852-177">You can do even deeper analysis if you [export hello data tooMicrosoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="22852-178">Voorbeeld Microsoft Dynamics CRM-oplossing</span><span class="sxs-lookup"><span data-stu-id="22852-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="22852-179">[Hier volgt Hallo Voorbeeldoplossing geïmplementeerd in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="22852-179">[Here is hello sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="22852-180">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="22852-180">Learn more</span></span>
* [<span data-ttu-id="22852-181">Wat is Application Insights?</span><span class="sxs-lookup"><span data-stu-id="22852-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="22852-182">Application Insights voor webpagina 's</span><span class="sxs-lookup"><span data-stu-id="22852-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="22852-183">Meer voorbeelden en scenario 's</span><span class="sxs-lookup"><span data-stu-id="22852-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
