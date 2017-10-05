---
title: Aantekeningen voor Application Insights release | Microsoft Docs
description: Implementatie toevoegen of markeringen om uw metrics explorer-grafieken in Application Insights te bouwen.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: f7eb2f3cba535eb64db5544c498289c9e895987a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="b35e1-103">Aantekeningen voor metrische grafieken in Application Insights</span><span class="sxs-lookup"><span data-stu-id="b35e1-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="b35e1-104">Aantekeningen op [Metrics Explorer](app-insights-metrics-explorer.md) grafieken weergegeven waarin u een nieuwe build, of een andere belangrijke gebeurtenis geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b35e1-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="b35e1-105">Ze maakt het eenvoudig om te zien of uw wijzigingen invloed zijn op de prestaties van de toepassing hadden.</span><span class="sxs-lookup"><span data-stu-id="b35e1-105">They make it easy to see whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="b35e1-106">Ze kunnen automatisch gemaakt door de [Visual Studio Team Services bouwen system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="b35e1-106">They can be automatically created by the [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="b35e1-107">U kunt ook aantekeningen voor een gebeurtenis die u met wilt vlag maken [ze worden gemaakt vanuit PowerShell](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="b35e1-107">You can also create annotations to flag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Voorbeeld van aantekeningen met zichtbaar correlatie met serverreactietijd](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="b35e1-109">Release aantekeningen met VSTS build</span><span class="sxs-lookup"><span data-stu-id="b35e1-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="b35e1-110">Release aantekeningen zijn een functie van de cloud-gebaseerde build en release van service van het Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="b35e1-110">Release annotations are a feature of the cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-the-annotations-extension-one-time"></a><span data-ttu-id="b35e1-111">De uitbreiding voor de aantekeningen (eenmaal) installeren</span><span class="sxs-lookup"><span data-stu-id="b35e1-111">Install the Annotations extension (one time)</span></span>
<span data-ttu-id="b35e1-112">Om te kunnen maken van aantekeningen release, moet u een van de vele Team Service-extensies in de Visual Studio Marketplace te installeren.</span><span class="sxs-lookup"><span data-stu-id="b35e1-112">To be able to create release annotations, you'll need to install one of the many Team Service extensions available in the Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="b35e1-113">Aanmelden bij uw [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span><span class="sxs-lookup"><span data-stu-id="b35e1-113">Sign in to your [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="b35e1-114">In Visual Studio Marketplace, [de uitbreiding Release aantekeningen](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), en voeg deze toe aan uw Team Services-account.</span><span class="sxs-lookup"><span data-stu-id="b35e1-114">In Visual Studio Marketplace, [get the Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it to your Team Services account.</span></span>

![AT top rechts van de webpagina Team Services, open Marketplace.](./media/app-insights-annotations/10.png)

<span data-ttu-id="b35e1-117">U hoeft hiervoor eenmaal voor uw Visual Studio Team Services-account.</span><span class="sxs-lookup"><span data-stu-id="b35e1-117">You only need to do this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="b35e1-118">Release aantekeningen kunnen nu worden geconfigureerd voor elk project in uw account.</span><span class="sxs-lookup"><span data-stu-id="b35e1-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="b35e1-119">Release aantekeningen configureren</span><span class="sxs-lookup"><span data-stu-id="b35e1-119">Configure release annotations</span></span>

<span data-ttu-id="b35e1-120">U moet een afzonderlijke API-sleutel voor elke release VSTS sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b35e1-120">You need to get a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="b35e1-121">Aanmelden bij de [Microsoft Azure Portal](https://portal.azure.com) en open de Application Insights-resource die uw toepassing wordt bewaakt.</span><span class="sxs-lookup"><span data-stu-id="b35e1-121">Sign in to the [Microsoft Azure Portal](https://portal.azure.com) and open the Application Insights resource that monitors your application.</span></span> <span data-ttu-id="b35e1-122">(Of [er nu een maken](app-insights-overview.md), als u dit nog niet hebt gedaan.)</span><span class="sxs-lookup"><span data-stu-id="b35e1-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="b35e1-123">Open **API-toegang**, **Application Insights-Id**.</span><span class="sxs-lookup"><span data-stu-id="b35e1-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![Open uw Application Insights-resource in portal.azure.com en instellingen kiezen.](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="b35e1-127">Open (of maak) op de releasesjabloon die u uw implementaties van Visual Studio Team Services beheert in een apart browservenster.</span><span class="sxs-lookup"><span data-stu-id="b35e1-127">In a separate browser window, open (or create) the release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="b35e1-128">Een taak toevoegen en selecteer de Application Insights Release aantekening-taak in het menu.</span><span class="sxs-lookup"><span data-stu-id="b35e1-128">Add a task, and select the Application Insights Release Annotation task from the menu.</span></span>
   
    <span data-ttu-id="b35e1-129">Plak de **toepassings-Id** die u hebt gekopieerd uit de blade API-toegang.</span><span class="sxs-lookup"><span data-stu-id="b35e1-129">Paste the **Application Id** that you copied from the API Access blade.</span></span>
   
    ![Release openen in Visual Studio Team Services, selecteert u de definitie van een release en kies bewerken.](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="b35e1-133">Stel de **APIKey** veld aan een variabele `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="b35e1-133">Set the **APIKey** field to a variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="b35e1-134">Maak een nieuwe API-sleutel en een kopie van deze weer in het venster Azure.</span><span class="sxs-lookup"><span data-stu-id="b35e1-134">Back in the Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![Klik in de blade API-toegang in het venster Azure API-sleutel maken.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="b35e1-138">Open het tabblad configuratie van de releasesjabloon.</span><span class="sxs-lookup"><span data-stu-id="b35e1-138">Open the Configuration tab of the release template.</span></span>
   
    <span data-ttu-id="b35e1-139">Maken van een variabele definitie voor `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="b35e1-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="b35e1-140">Uw API-sleutel voor de definitie van de ApiKey plakken.</span><span class="sxs-lookup"><span data-stu-id="b35e1-140">Paste your API key to the ApiKey variable definition.</span></span>
   
    ![In het venster Team Services, selecteer het tabblad configuratie en klik variabele toevoegen.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="b35e1-143">Ten slotte **opslaan** de release-definitie.</span><span class="sxs-lookup"><span data-stu-id="b35e1-143">Finally, **Save** the release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="b35e1-144">Weergave aantekeningen</span><span class="sxs-lookup"><span data-stu-id="b35e1-144">View annotations</span></span>
<span data-ttu-id="b35e1-145">Wanneer u de sjabloon voor het implementeren van een nieuwe release hebt gebruikt, wordt nu een aantekening verzonden naar Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b35e1-145">Now, whenever you use the release template to deploy a new release, an annotation will be sent to Application Insights.</span></span> <span data-ttu-id="b35e1-146">De aantekeningen worden weergegeven op de grafieken in Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="b35e1-146">The annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="b35e1-147">Klik op de markering van een aantekening details over de release, met inbegrip van de aanvrager, bron besturingselement vertakking openen, vrijgeven definitie en omgeving.</span><span class="sxs-lookup"><span data-stu-id="b35e1-147">Click on any annotation marker to open details about the release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Klik op een markering van de aantekening release.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="b35e1-149">Aangepaste aantekeningen maken vanuit PowerShell</span><span class="sxs-lookup"><span data-stu-id="b35e1-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="b35e1-150">U kunt ook aantekeningen maken van een proces gewenste (zonder tegenover Team System).</span><span class="sxs-lookup"><span data-stu-id="b35e1-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="b35e1-151">Maak een lokale kopie van de [Powershell-script uit GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="b35e1-151">Make a local copy of the [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="b35e1-152">De toepassings-ID ophalen en maak een API-sleutel vanuit de blade API-toegang.</span><span class="sxs-lookup"><span data-stu-id="b35e1-152">Get the Application ID and create an API key from the API Access blade.</span></span>

3. <span data-ttu-id="b35e1-153">Roept het script als volgt:</span><span class="sxs-lookup"><span data-stu-id="b35e1-153">Call the script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="b35e1-154">Het is gemakkelijk om het script, bijvoorbeeld om aantekeningen te maken voor het verleden.</span><span class="sxs-lookup"><span data-stu-id="b35e1-154">It's easy to modify the script, for example to create annotations for the past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b35e1-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b35e1-155">Next steps</span></span>

* [<span data-ttu-id="b35e1-156">Werkitems maken</span><span class="sxs-lookup"><span data-stu-id="b35e1-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="b35e1-157">Automatisering met PowerShell</span><span class="sxs-lookup"><span data-stu-id="b35e1-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
