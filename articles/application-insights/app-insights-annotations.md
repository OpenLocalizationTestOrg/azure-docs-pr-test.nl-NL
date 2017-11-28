---
title: aaaRelease aantekeningen voor Application Insights | Microsoft Docs
description: Implementatie toevoegen of bouwen markeringen tooyour metrics explorer-grafieken in Application Insights.
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
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="60e8d-103">Aantekeningen voor metrische grafieken in Application Insights</span><span class="sxs-lookup"><span data-stu-id="60e8d-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="60e8d-104">Aantekeningen op [Metrics Explorer](app-insights-metrics-explorer.md) grafieken weergegeven waarin u een nieuwe build, of een andere belangrijke gebeurtenis geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="60e8d-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="60e8d-105">Ze maken het gemakkelijk toosee of uw wijzigingen geen effect op de prestaties van uw toepassing heeft.</span><span class="sxs-lookup"><span data-stu-id="60e8d-105">They make it easy toosee whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="60e8d-106">Ze kunnen automatisch gemaakt door Hallo [Visual Studio Team Services bouwen system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="60e8d-106">They can be automatically created by hello [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="60e8d-107">U kunt aantekeningen tooflag ook maken een gebeurtenis die u met wilt [ze worden gemaakt vanuit PowerShell](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="60e8d-107">You can also create annotations tooflag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Voorbeeld van aantekeningen met zichtbaar correlatie met serverreactietijd](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="60e8d-109">Release aantekeningen met VSTS build</span><span class="sxs-lookup"><span data-stu-id="60e8d-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="60e8d-110">Release aantekeningen zijn een functie van cloud-gebaseerde Hallo-build en release van service van het Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="60e8d-110">Release annotations are a feature of hello cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-hello-annotations-extension-one-time"></a><span data-ttu-id="60e8d-111">Hallo aantekeningen uitbreiding (eenmaal) installeren</span><span class="sxs-lookup"><span data-stu-id="60e8d-111">Install hello Annotations extension (one time)</span></span>
<span data-ttu-id="60e8d-112">toobe kunnen toocreate release aantekeningen, moet u tooinstall een Hallo Hallo veel Team extensies beschikbaar zijn in Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="60e8d-112">toobe able toocreate release annotations, you'll need tooinstall one of hello many Team Service extensions available in hello Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="60e8d-113">Meld u aan tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span><span class="sxs-lookup"><span data-stu-id="60e8d-113">Sign in tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="60e8d-114">In Visual Studio Marketplace, [Hallo Release aantekeningen uitbreiding](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), en voeg deze tooyour Team Services-account.</span><span class="sxs-lookup"><span data-stu-id="60e8d-114">In Visual Studio Marketplace, [get hello Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it tooyour Team Services account.</span></span>

![AT top rechts van de webpagina Team Services, open Marketplace.](./media/app-insights-annotations/10.png)

<span data-ttu-id="60e8d-117">U hoeft alleen toodo dit eenmaal voor uw Visual Studio Team Services-account.</span><span class="sxs-lookup"><span data-stu-id="60e8d-117">You only need toodo this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="60e8d-118">Release aantekeningen kunnen nu worden geconfigureerd voor elk project in uw account.</span><span class="sxs-lookup"><span data-stu-id="60e8d-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="60e8d-119">Release aantekeningen configureren</span><span class="sxs-lookup"><span data-stu-id="60e8d-119">Configure release annotations</span></span>

<span data-ttu-id="60e8d-120">Tooget een afzonderlijke API-sleutel moet u voor elke release VSTS sjabloon.</span><span class="sxs-lookup"><span data-stu-id="60e8d-120">You need tooget a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="60e8d-121">Meld u aan toohello [Microsoft Azure Portal](https://portal.azure.com) en open Hallo Application Insights-resource die wordt uw toepassing bewaakt.</span><span class="sxs-lookup"><span data-stu-id="60e8d-121">Sign in toohello [Microsoft Azure Portal](https://portal.azure.com) and open hello Application Insights resource that monitors your application.</span></span> <span data-ttu-id="60e8d-122">(Of [er nu een maken](app-insights-overview.md), als u dit nog niet hebt gedaan.)</span><span class="sxs-lookup"><span data-stu-id="60e8d-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="60e8d-123">Open **API-toegang**, **Application Insights-Id**.</span><span class="sxs-lookup"><span data-stu-id="60e8d-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![Open uw Application Insights-resource in portal.azure.com en instellingen kiezen.](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="60e8d-127">Open (of maak) in een nieuw browservenster op Hallo releasesjabloon die u uw implementaties van Visual Studio Team Services beheert.</span><span class="sxs-lookup"><span data-stu-id="60e8d-127">In a separate browser window, open (or create) hello release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="60e8d-128">Een taak toevoegen en selecteer Hallo Application Insights Release aantekening taak in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="60e8d-128">Add a task, and select hello Application Insights Release Annotation task from hello menu.</span></span>
   
    <span data-ttu-id="60e8d-129">Plakken Hallo **toepassings-Id** die u hebt gekopieerd uit Hallo blade API-toegang.</span><span class="sxs-lookup"><span data-stu-id="60e8d-129">Paste hello **Application Id** that you copied from hello API Access blade.</span></span>
   
    ![Release openen in Visual Studio Team Services, selecteert u de definitie van een release en kies bewerken.](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="60e8d-133">Set Hallo **APIKey** veld tooa variabele `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="60e8d-133">Set hello **APIKey** field tooa variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="60e8d-134">Terug in Azure venster hello, maak een nieuwe API-sleutel en een kopie van deze.</span><span class="sxs-lookup"><span data-stu-id="60e8d-134">Back in hello Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![Klik in de blade API-toegang in hello Azure venster Hallo, API-sleutel maken.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="60e8d-138">Open Hallo tabblad van de configuratie van Hallo releasesjabloon.</span><span class="sxs-lookup"><span data-stu-id="60e8d-138">Open hello Configuration tab of hello release template.</span></span>
   
    <span data-ttu-id="60e8d-139">Maken van een variabele definitie voor `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="60e8d-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="60e8d-140">Plak uw API-sleutel toohello ApiKey variabele-definitie.</span><span class="sxs-lookup"><span data-stu-id="60e8d-140">Paste your API key toohello ApiKey variable definition.</span></span>
   
    ![Hallo-teamservices venster, selecteer Hallo configuratie tabblad en klik op variabele toevoegen.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="60e8d-143">Ten slotte **opslaan** Hallo release definitie.</span><span class="sxs-lookup"><span data-stu-id="60e8d-143">Finally, **Save** hello release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="60e8d-144">Weergave aantekeningen</span><span class="sxs-lookup"><span data-stu-id="60e8d-144">View annotations</span></span>
<span data-ttu-id="60e8d-145">Nu, wanneer u Hallo release sjabloon toodeploy een nieuwe release, van een aantekening wordt verzonden tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="60e8d-145">Now, whenever you use hello release template toodeploy a new release, an annotation will be sent tooApplication Insights.</span></span> <span data-ttu-id="60e8d-146">Hallo aantekeningen worden weergegeven op de grafieken in Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="60e8d-146">hello annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="60e8d-147">Klik op de aantekening markering tooopen details over Hallo introductie, met inbegrip van de aanvrager, bron besturingselement vertakking, release-definitie, omgeving en meer.</span><span class="sxs-lookup"><span data-stu-id="60e8d-147">Click on any annotation marker tooopen details about hello release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Klik op een markering van de aantekening release.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="60e8d-149">Aangepaste aantekeningen maken vanuit PowerShell</span><span class="sxs-lookup"><span data-stu-id="60e8d-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="60e8d-150">U kunt ook aantekeningen maken van een proces gewenste (zonder tegenover Team System).</span><span class="sxs-lookup"><span data-stu-id="60e8d-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="60e8d-151">Maak een lokale kopie van Hallo [Powershell-script uit GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="60e8d-151">Make a local copy of hello [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="60e8d-152">Hallo toepassings-ID ophalen en maak een API-sleutel vanuit Hallo blade API-toegang.</span><span class="sxs-lookup"><span data-stu-id="60e8d-152">Get hello Application ID and create an API key from hello API Access blade.</span></span>

3. <span data-ttu-id="60e8d-153">Roep Hallo script als volgt:</span><span class="sxs-lookup"><span data-stu-id="60e8d-153">Call hello script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="60e8d-154">Het is gemakkelijk toomodify Hallo script, bijvoorbeeld toocreate aantekeningen voor Hallo afgelopen.</span><span class="sxs-lookup"><span data-stu-id="60e8d-154">It's easy toomodify hello script, for example toocreate annotations for hello past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60e8d-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="60e8d-155">Next steps</span></span>

* [<span data-ttu-id="60e8d-156">Werkitems maken</span><span class="sxs-lookup"><span data-stu-id="60e8d-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="60e8d-157">Automatisering met PowerShell</span><span class="sxs-lookup"><span data-stu-id="60e8d-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
