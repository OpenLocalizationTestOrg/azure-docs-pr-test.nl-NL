---
title: Microsoft Dynamics CRM en Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: a9593d5f198e05db80451a599428a296ed02e781
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="3b04e-104">Overzicht: Telemetrie voor Microsoft Dynamics CRM Online met behulp van Application Insights inschakelen</span><span class="sxs-lookup"><span data-stu-id="3b04e-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="3b04e-105">Dit artikel ziet u het ophalen van telemetriegegevens van [Microsoft Dynamics CRM Online](https://www.dynamics.com/) met [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="3b04e-105">This article shows you how to get telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="3b04e-106">We doorlopen het complete proces van het Application Insights-script toevoegen aan uw toepassing vastleggen van gegevens en gegevensvisualisatie.</span><span class="sxs-lookup"><span data-stu-id="3b04e-106">We’ll walk through the complete process of adding Application Insights script to your application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="3b04e-107">[De Voorbeeldoplossing Bladeren](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="3b04e-107">[Browse the sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-to-new-or-existing-crm-online-instance"></a><span data-ttu-id="3b04e-108">Application Insights toevoegen aan nieuwe of bestaande exemplaar van CRM Online</span><span class="sxs-lookup"><span data-stu-id="3b04e-108">Add Application Insights to new or existing CRM Online instance</span></span>
<span data-ttu-id="3b04e-109">Voor het bewaken van uw toepassing, kunt u een Application Insights-SDK toevoegen aan uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="3b04e-109">To monitor your application, you add an Application Insights SDK to your application.</span></span> <span data-ttu-id="3b04e-110">De SDK telemetrie verzendt naar de [Application Insights-portal](https://portal.azure.com), kunt u gebruik van onze krachtige analyse en diagnostische hulpprogramma's, of de gegevens naar opslag exporteren.</span><span class="sxs-lookup"><span data-stu-id="3b04e-110">The SDK sends telemetry to the [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export the data to storage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="3b04e-111">Een Application Insights-resource maken in Azure</span><span class="sxs-lookup"><span data-stu-id="3b04e-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="3b04e-112">Ophalen van [een account in Microsoft Azure](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="3b04e-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="3b04e-113">Meld u aan bij de [Azure-portal](https://portal.azure.com) en een nieuwe Application Insights-resource toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3b04e-113">Sign into the [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="3b04e-114">Dit is waar uw gegevens worden verwerkt en weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3b04e-114">This is where your data will be processed and displayed.</span></span>
   
    ![Klik op +, Ontwikkelaarsservices, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="3b04e-116">Kies ASP.NET als het toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="3b04e-116">Choose ASP.NET as the application type.</span></span>
3. <span data-ttu-id="3b04e-117">Open de pagina aan de slag en ' bewaken en onderzoeken van client-side '.</span><span class="sxs-lookup"><span data-stu-id="3b04e-117">Open the Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Codefragment voor het invoegen in uw webpagina](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="3b04e-119">**Houd de codetabel open** terwijl u de volgende stap in een ander browservenster.</span><span class="sxs-lookup"><span data-stu-id="3b04e-119">**Keep the code page open** while you do the next step in another browser window.</span></span> <span data-ttu-id="3b04e-120">U moet de code snel.</span><span class="sxs-lookup"><span data-stu-id="3b04e-120">You'll need the code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="3b04e-121">Een JavaScript-web-resource maken in Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="3b04e-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="3b04e-122">Open uw CRM Online-instantie en aanmelding met administrator-bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="3b04e-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="3b04e-123">Open Microsoft Dynamics CRM-instellingen aanpassingen, past u het systeem</span><span class="sxs-lookup"><span data-stu-id="3b04e-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize the System</span></span>
   
    ![Microsoft Dynamics CRM-instellingen](./media/app-insights-sample-mscrm/04.png)
   
    ![Instellingen > aanpassingen](./media/app-insights-sample-mscrm/05.png)

    ![De Systeemoptie aanpassen](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="3b04e-127">Maak een JavaScript-resource.</span><span class="sxs-lookup"><span data-stu-id="3b04e-127">Create a JavaScript resource.</span></span>
   
    ![Dialoogvenster nieuwe webbron](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="3b04e-129">Geef het een naam, selecteer **Script (JScript)** en open de teksteditor.</span><span class="sxs-lookup"><span data-stu-id="3b04e-129">Give it a name, select **Script (JScript)** and open the text editor.</span></span>
   
    ![Open de teksteditor](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="3b04e-131">Kopieer de code uit de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3b04e-131">Copy the code from Application Insights.</span></span> <span data-ttu-id="3b04e-132">Zorg dat u scriptlabels negeren bij het kopiëren.</span><span class="sxs-lookup"><span data-stu-id="3b04e-132">While copying make sure to ignore script tags.</span></span> <span data-ttu-id="3b04e-133">Raadpleeg de onderstaande schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="3b04e-133">Refer below screenshot:</span></span>
   
    ![De instrumentatiesleutel instellen](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="3b04e-135">De code bevat de instrumentatiesleutel die uw Application insights-resource identificeert.</span><span class="sxs-lookup"><span data-stu-id="3b04e-135">The code includes the instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="3b04e-136">Opslaan en publiceren.</span><span class="sxs-lookup"><span data-stu-id="3b04e-136">Save and publish.</span></span>
   
    ![Opslaan en publiceren](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="3b04e-138">Instrument formulieren</span><span class="sxs-lookup"><span data-stu-id="3b04e-138">Instrument Forms</span></span>
1. <span data-ttu-id="3b04e-139">Open het formulier Account in Microsoft CRM Online</span><span class="sxs-lookup"><span data-stu-id="3b04e-139">In Microsoft CRM Online, open the Account form</span></span>
   
    ![Accountformulier](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="3b04e-141">Open de eigenschappen van het formulier</span><span class="sxs-lookup"><span data-stu-id="3b04e-141">Open the form Properties</span></span>
   
    ![Eigenschappen van formulier](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="3b04e-143">De JavaScript-web-resource die u hebt gemaakt toevoegen</span><span class="sxs-lookup"><span data-stu-id="3b04e-143">Add the JavaScript web resource that you created</span></span>
   
    ![Menu toevoegen](./media/app-insights-sample-mscrm/13.png)
   
    ![De webresource toevoegen](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="3b04e-146">Opslaan en publiceren van uw aanpassingen van formulieren.</span><span class="sxs-lookup"><span data-stu-id="3b04e-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="3b04e-147">Metrische gegevens vastgelegd</span><span class="sxs-lookup"><span data-stu-id="3b04e-147">Metrics captured</span></span>
<span data-ttu-id="3b04e-148">U hebt nu het vastleggen van telemetriegegevens voor het formulier ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3b04e-148">You have now set up telemetry capture for the form.</span></span> <span data-ttu-id="3b04e-149">Wanneer deze wordt gebruikt, worden gegevens verzonden naar uw Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="3b04e-149">Whenever it is used, data will be sent to your Application Insights resource.</span></span>

<span data-ttu-id="3b04e-150">Hier vindt u voorbeelden van de gegevens die u ziet.</span><span class="sxs-lookup"><span data-stu-id="3b04e-150">Here are samples of the data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="3b04e-151">Toepassingsstatus</span><span class="sxs-lookup"><span data-stu-id="3b04e-151">Application health</span></span>
![Voorbeeld van de paginalaadtijd](./media/app-insights-sample-mscrm/15.png)

![Voorbeeld pagina weergaven grafiek](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="3b04e-154">Browseruitzonderingen:</span><span class="sxs-lookup"><span data-stu-id="3b04e-154">Browser exceptions:</span></span>

![Grafiek met serveruitzonderingen klikken](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="3b04e-156">Klik in de grafiek als u meer informatie:</span><span class="sxs-lookup"><span data-stu-id="3b04e-156">Click the chart to get more detail:</span></span>

![Lijst met uitzonderingen](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="3b04e-158">Gebruik</span><span class="sxs-lookup"><span data-stu-id="3b04e-158">Usage</span></span>
![Gebruikers, sessies en paginaweergaven](./media/app-insights-sample-mscrm/19.png)

![Sesion grafieken](./media/app-insights-sample-mscrm/20.png)

![Browserversies](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="3b04e-162">Browsers</span><span class="sxs-lookup"><span data-stu-id="3b04e-162">Browsers</span></span>
![Overzicht van de laadtijd van pagina](./media/app-insights-sample-mscrm/22.png)

![Het aantal sessies per browserversie](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="3b04e-165">Geolocatie</span><span class="sxs-lookup"><span data-stu-id="3b04e-165">Geolocation</span></span>
![Het aantal sessies per land](./media/app-insights-sample-mscrm/24.png)

![Sessies en gebruikers per land](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="3b04e-168">Inside pagina-aanvraag voor weergave</span><span class="sxs-lookup"><span data-stu-id="3b04e-168">Inside page view request</span></span>
![Overzicht van de pagina weergeven](./media/app-insights-sample-mscrm/26.png)

![Zoeken op de pagina-gebeurtenissen weergeven](./media/app-insights-sample-mscrm/27.png)

![Vergelijkbare paginaweergaven](./media/app-insights-sample-mscrm/28.png)

![Eigenschappen van paginaweergaven](./media/app-insights-sample-mscrm/29.png)

![Pagina's per sessie](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="3b04e-174">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="3b04e-174">Sample code</span></span>
<span data-ttu-id="3b04e-175">[De voorbeeldcode Bladeren](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="3b04e-175">[Browse the sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="3b04e-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="3b04e-176">Power BI</span></span>
<span data-ttu-id="3b04e-177">U kunt zelfs grondigere analyse doen als u [de gegevens exporteren naar Microsoft Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="3b04e-177">You can do even deeper analysis if you [export the data to Microsoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="3b04e-178">Voorbeeld Microsoft Dynamics CRM-oplossing</span><span class="sxs-lookup"><span data-stu-id="3b04e-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="3b04e-179">[Hier volgt de Voorbeeldoplossing geïmplementeerd in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="3b04e-179">[Here is the sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="3b04e-180">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="3b04e-180">Learn more</span></span>
* [<span data-ttu-id="3b04e-181">Wat is Application Insights?</span><span class="sxs-lookup"><span data-stu-id="3b04e-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="3b04e-182">Application Insights voor webpagina 's</span><span class="sxs-lookup"><span data-stu-id="3b04e-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="3b04e-183">Meer voorbeelden en scenario 's</span><span class="sxs-lookup"><span data-stu-id="3b04e-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
