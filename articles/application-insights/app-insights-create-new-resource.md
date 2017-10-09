---
title: een nieuwe Azure Application Insights-resource aaaCreate | Microsoft Docs
description: Stel handmatig bewaking van de Application Insights voor een nieuwe live-toepassing.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="adbfb-103">Een Application Insights-resource maken</span><span class="sxs-lookup"><span data-stu-id="adbfb-103">Create an Application Insights resource</span></span>
<span data-ttu-id="adbfb-104">Azure Application Insights gegevens over uw toepassing worden weergegeven in een Microsoft Azure *resource*.</span><span class="sxs-lookup"><span data-stu-id="adbfb-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="adbfb-105">Een nieuwe resource daarom deel uitmaakt van [toomonitor Application Insights instellen met een nieuwe toepassing][start].</span><span class="sxs-lookup"><span data-stu-id="adbfb-105">Creating a new resource is therefore part of [setting up Application Insights toomonitor a new application][start].</span></span> <span data-ttu-id="adbfb-106">In veel gevallen kan maken van een resource automatisch worden gedaan door Hallo IDE.</span><span class="sxs-lookup"><span data-stu-id="adbfb-106">In many cases, creating a resource can be done automatically by hello IDE.</span></span> <span data-ttu-id="adbfb-107">Maar in sommige gevallen u Maak handmatig een resource - bijvoorbeeld afzonderlijke resources voor ontwikkeling en productie toohave builds van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="adbfb-107">But in some cases, you create a resource manually - for example, toohave separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="adbfb-108">Nadat u Hallo resource hebt gemaakt, kunt u de instrumentatiesleutel ophalen en die tooconfigure Hallo SDK in de toepassing hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="adbfb-108">After you have created hello resource, you get its instrumentation key and use that tooconfigure hello SDK in hello application.</span></span> <span data-ttu-id="adbfb-109">sleutel resourcekoppelingen Hallo Hallo telemetrie toohello resource.</span><span class="sxs-lookup"><span data-stu-id="adbfb-109">hello resource key links hello telemetry toohello resource.</span></span>

## <a name="sign-up-toomicrosoft-azure"></a><span data-ttu-id="adbfb-110">TooMicrosoft Azure registreren</span><span class="sxs-lookup"><span data-stu-id="adbfb-110">Sign up tooMicrosoft Azure</span></span>
<span data-ttu-id="adbfb-111">Als u dit nog niet hebt verkregen een [Microsoft-account, nu](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="adbfb-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="adbfb-112">(Als u gebruikmaakt van services zoals Outlook.com, OneDrive, Windows Phone of XBox Live, u hebt al een Microsoft-account.)</span><span class="sxs-lookup"><span data-stu-id="adbfb-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="adbfb-113">U moet ook een abonnement te[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="adbfb-113">You also need a subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="adbfb-114">Eigenaar als uw team of organisatie een Azure-abonnement heeft, Hallo kan u toevoegen tooit, met behulp van uw Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="adbfb-114">If your team or organization has an Azure subscription, hello owner can add you tooit, using your Windows Live ID.</span></span> <span data-ttu-id="adbfb-115">U bent alleen kosten in rekening gebracht voor wat u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="adbfb-115">You're only charged for what you use.</span></span> <span data-ttu-id="adbfb-116">Hallo standaard basisniveau kunt u een bepaalde hoeveelheid experimenteel gebruik gratis.</span><span class="sxs-lookup"><span data-stu-id="adbfb-116">hello default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="adbfb-117">Als u toegang tooa abonnement hebt, aanmelden tooApplication Insights op [http://portal.azure.com](https://portal.azure.com), en uw toologin Live ID gebruiken.</span><span class="sxs-lookup"><span data-stu-id="adbfb-117">When you've got access tooa subscription, log in tooApplication Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID toologin.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="adbfb-118">Een Application Insights-resource maken</span><span class="sxs-lookup"><span data-stu-id="adbfb-118">Create an Application Insights resource</span></span>
<span data-ttu-id="adbfb-119">In Hallo [portal.azure.com](https://portal.azure.com), een Application Insights-resource toevoegen:</span><span class="sxs-lookup"><span data-stu-id="adbfb-119">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Klik op Nieuw > Application Insights](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="adbfb-121">**Toepassingstype** is van invloed op wat er op de blade overzicht Hallo en Hallo eigenschappen beschikbaar zijn in [metrische explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="adbfb-121">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="adbfb-122">Als u uw app-type niet ziet, kiest u algemene.</span><span class="sxs-lookup"><span data-stu-id="adbfb-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="adbfb-123">**Abonnement** is uw betaling-account in Azure.</span><span class="sxs-lookup"><span data-stu-id="adbfb-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="adbfb-124">**Resourcegroep** is nuttig voor het beheren van eigenschappen zoals toegangsbeheer.</span><span class="sxs-lookup"><span data-stu-id="adbfb-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="adbfb-125">Als u andere Azure-resources al hebt gemaakt, kunt u kiezen tooput deze nieuwe bron in Hallo dezelfde groep.</span><span class="sxs-lookup"><span data-stu-id="adbfb-125">If you have already created other Azure resources, you can choose tooput this new resource in hello same group.</span></span>
* <span data-ttu-id="adbfb-126">**Locatie** is waar we uw gegevens wilt bewaren.</span><span class="sxs-lookup"><span data-stu-id="adbfb-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="adbfb-127">**Pincode toodashboard** plaatst u een snelle toegang tegel voor uw resource op de startpagina van Azure.</span><span class="sxs-lookup"><span data-stu-id="adbfb-127">**Pin toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="adbfb-128">Aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="adbfb-128">Recommended.</span></span>

<span data-ttu-id="adbfb-129">Wanneer uw app is gemaakt, wordt er een nieuwe blade geopend.</span><span class="sxs-lookup"><span data-stu-id="adbfb-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="adbfb-130">Deze blade is waar u prestatie- en gebruiksgegevens over uw app bekijken.</span><span class="sxs-lookup"><span data-stu-id="adbfb-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="adbfb-131">tooget back tooit volgende keer dat u zich aanmeldt tooAzure, zoeken naar uw app snel starten-tegel op Hallo start board (startscherm).</span><span class="sxs-lookup"><span data-stu-id="adbfb-131">tooget back tooit next time you log in tooAzure, look for your app's quick-start tile on hello start board (home screen).</span></span> <span data-ttu-id="adbfb-132">Of klik op Bladeren toofind deze.</span><span class="sxs-lookup"><span data-stu-id="adbfb-132">Or click Browse toofind it.</span></span>

## <a name="copy-hello-instrumentation-key"></a><span data-ttu-id="adbfb-133">Hallo-instrumentatiesleutel kopiëren</span><span class="sxs-lookup"><span data-stu-id="adbfb-133">Copy hello instrumentation key</span></span>
<span data-ttu-id="adbfb-134">de instrumentatiesleutel Hallo identificeert Hallo resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="adbfb-134">hello instrumentation key identifies hello resource that you created.</span></span> <span data-ttu-id="adbfb-135">U moet toogive toohello SDK.</span><span class="sxs-lookup"><span data-stu-id="adbfb-135">You need it toogive toohello SDK.</span></span>

![Klik op Essentials, Hallo Instrumentatiesleutel, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a><span data-ttu-id="adbfb-137">Hallo SDK installeren in uw app</span><span class="sxs-lookup"><span data-stu-id="adbfb-137">Install hello SDK in your app</span></span>
<span data-ttu-id="adbfb-138">Hallo Application Insights-SDK installeren in uw app.</span><span class="sxs-lookup"><span data-stu-id="adbfb-138">Install hello Application Insights SDK in your app.</span></span> <span data-ttu-id="adbfb-139">Deze stap is afhankelijk van geheugenlatentie Hallo-type van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="adbfb-139">This step depends heavily on hello type of your application.</span></span> 

<span data-ttu-id="adbfb-140">Gebruik Hallo instrumentation sleutel tooconfigure [SDK die u in uw toepassing installeert hello][start].</span><span class="sxs-lookup"><span data-stu-id="adbfb-140">Use hello instrumentation key tooconfigure [hello SDK that you install in your application][start].</span></span>

<span data-ttu-id="adbfb-141">Hallo SDK bevat standaard modules die telemetrie zonder dat u toowrite code hoeft te verzenden.</span><span class="sxs-lookup"><span data-stu-id="adbfb-141">hello SDK includes standard modules that send telemetry without you having toowrite any code.</span></span> <span data-ttu-id="adbfb-142">tootrack gebruikersacties of het analyseren van problemen in meer detail [Hallo API gebruiken] [ api] toosend uw eigen telemetrie.</span><span class="sxs-lookup"><span data-stu-id="adbfb-142">tootrack user actions or diagnose issues in more detail, [use hello API][api] toosend your own telemetry.</span></span>

## <span data-ttu-id="adbfb-143"><a name="monitor"></a>Zie telemetriegegevens</span><span class="sxs-lookup"><span data-stu-id="adbfb-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="adbfb-144">Blade tooreturn tooyour toepassing blade sluiten Hallo snel starten in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="adbfb-144">Close hello quick start blade tooreturn tooyour application blade in hello Azure portal.</span></span>

<span data-ttu-id="adbfb-145">Klik op Hallo zoeken tegel toosee [diagnostische gegevens doorzoeken][diagnostic], waarbij Hallo eerste gebeurtenissen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="adbfb-145">Click hello Search tile toosee [Diagnostic Search][diagnostic], where hello first events appear.</span></span> 

<span data-ttu-id="adbfb-146">Als u meer gegevens verwacht, klikt u op **vernieuwen** na enkele seconden.</span><span class="sxs-lookup"><span data-stu-id="adbfb-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="adbfb-147">Het automatisch maken van een resource</span><span class="sxs-lookup"><span data-stu-id="adbfb-147">Creating a resource automatically</span></span>
<span data-ttu-id="adbfb-148">U kunt schrijven een [PowerShell-script](app-insights-powershell.md) toocreate een resource automatisch.</span><span class="sxs-lookup"><span data-stu-id="adbfb-148">You can write a [PowerShell script](app-insights-powershell.md) toocreate a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adbfb-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="adbfb-149">Next steps</span></span>
* [<span data-ttu-id="adbfb-150">Een dashboard maken</span><span class="sxs-lookup"><span data-stu-id="adbfb-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="adbfb-151">Diagnostische gegevens doorzoeken</span><span class="sxs-lookup"><span data-stu-id="adbfb-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="adbfb-152">Metrische gegevens verkennen</span><span class="sxs-lookup"><span data-stu-id="adbfb-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="adbfb-153">Analytics-query's schrijven</span><span class="sxs-lookup"><span data-stu-id="adbfb-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

