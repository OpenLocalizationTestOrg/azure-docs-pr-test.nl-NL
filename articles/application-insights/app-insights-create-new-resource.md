---
title: Maak een nieuwe Azure Application Insights-resource | Microsoft Docs
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
ms.openlocfilehash: 5f8814ee943424c1c278ab3732129d4459f83819
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="cdb1f-103">Een Application Insights-resource maken</span><span class="sxs-lookup"><span data-stu-id="cdb1f-103">Create an Application Insights resource</span></span>
<span data-ttu-id="cdb1f-104">Azure Application Insights gegevens over uw toepassing worden weergegeven in een Microsoft Azure *resource*.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="cdb1f-105">Een nieuwe resource daarom deel uitmaakt van [Application Insights instellen voor het bewaken van een nieuwe toepassing][start].</span><span class="sxs-lookup"><span data-stu-id="cdb1f-105">Creating a new resource is therefore part of [setting up Application Insights to monitor a new application][start].</span></span> <span data-ttu-id="cdb1f-106">In veel gevallen kan maken van een resource automatisch worden gedaan door de IDE.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-106">In many cases, creating a resource can be done automatically by the IDE.</span></span> <span data-ttu-id="cdb1f-107">Maar in sommige gevallen u Maak handmatig een resource - bijvoorbeeld, als u wilt dat afzonderlijke resources voor ontwikkeling en productie builds van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-107">But in some cases, you create a resource manually - for example, to have separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="cdb1f-108">Nadat u de resource hebt gemaakt, kunt u de instrumentatiesleutel ophalen en gebruiken die voor het configureren van de SDK in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-108">After you have created the resource, you get its instrumentation key and use that to configure the SDK in the application.</span></span> <span data-ttu-id="cdb1f-109">De bronsleutel koppelingen de telemetrie naar de resource.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-109">The resource key links the telemetry to the resource.</span></span>

## <a name="sign-up-to-microsoft-azure"></a><span data-ttu-id="cdb1f-110">Meld u aan Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="cdb1f-110">Sign up to Microsoft Azure</span></span>
<span data-ttu-id="cdb1f-111">Als u dit nog niet hebt verkregen een [Microsoft-account, nu](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="cdb1f-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="cdb1f-112">(Als u gebruikmaakt van services zoals Outlook.com, OneDrive, Windows Phone of XBox Live, u hebt al een Microsoft-account.)</span><span class="sxs-lookup"><span data-stu-id="cdb1f-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="cdb1f-113">U moet ook een abonnement op [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="cdb1f-113">You also need a subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="cdb1f-114">Als uw team of organisatie een Azure-abonnement heeft, de eigenaar kunt u toevoegen, met behulp van uw Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-114">If your team or organization has an Azure subscription, the owner can add you to it, using your Windows Live ID.</span></span> <span data-ttu-id="cdb1f-115">U bent alleen kosten in rekening gebracht voor wat u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-115">You're only charged for what you use.</span></span> <span data-ttu-id="cdb1f-116">Het basic standaardplan kunt u een bepaalde hoeveelheid experimenteel gebruik gratis.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-116">The default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="cdb1f-117">Wanneer u toegang tot een abonnement hebt, meld u aan bij Application Insights op [http://portal.azure.com](https://portal.azure.com), en gebruik van uw Live-ID om aan te melden.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-117">When you've got access to a subscription, log in to Application Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID to login.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="cdb1f-118">Een Application Insights-resource maken</span><span class="sxs-lookup"><span data-stu-id="cdb1f-118">Create an Application Insights resource</span></span>
<span data-ttu-id="cdb1f-119">In de [portal.azure.com](https://portal.azure.com), een Application Insights-resource toevoegen:</span><span class="sxs-lookup"><span data-stu-id="cdb1f-119">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Klik op Nieuw > Application Insights](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="cdb1f-121">**Toepassingstype** is van invloed op wat er op de overzichtsblade en de eigenschappen die beschikbaar zijn in [metrische explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="cdb1f-121">**Application type** affects what you see on the overview blade and the properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="cdb1f-122">Als u uw app-type niet ziet, kiest u algemene.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="cdb1f-123">**Abonnement** is uw betaling-account in Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="cdb1f-124">**Resourcegroep** is nuttig voor het beheren van eigenschappen zoals toegangsbeheer.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="cdb1f-125">Als u andere Azure-resources al hebt gemaakt, kunt u deze nieuwe bron plaatsen in dezelfde groep.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-125">If you have already created other Azure resources, you can choose to put this new resource in the same group.</span></span>
* <span data-ttu-id="cdb1f-126">**Locatie** is waar we uw gegevens wilt bewaren.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="cdb1f-127">**Vastmaken aan dashboard** plaatst u een snelle toegang tegel voor uw resource op de startpagina van Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-127">**Pin to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="cdb1f-128">Aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-128">Recommended.</span></span>

<span data-ttu-id="cdb1f-129">Wanneer uw app is gemaakt, wordt er een nieuwe blade geopend.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="cdb1f-130">Deze blade is waar u prestatie- en gebruiksgegevens over uw app bekijken.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="cdb1f-131">U kunt teruggaan naar het volgende keer dat u zich bij Azure aanmelden, zoekt u naar uw app snel starten-tegel in de start board (startscherm).</span><span class="sxs-lookup"><span data-stu-id="cdb1f-131">To get back to it next time you log in to Azure, look for your app's quick-start tile on the start board (home screen).</span></span> <span data-ttu-id="cdb1f-132">Of klik op Bladeren om te zoeken.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-132">Or click Browse to find it.</span></span>

## <a name="copy-the-instrumentation-key"></a><span data-ttu-id="cdb1f-133">De instrumentatiesleutel kopiëren</span><span class="sxs-lookup"><span data-stu-id="cdb1f-133">Copy the instrumentation key</span></span>
<span data-ttu-id="cdb1f-134">De instrumentatiesleutel identificeert de resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-134">The instrumentation key identifies the resource that you created.</span></span> <span data-ttu-id="cdb1f-135">U moet deze aan de SDK.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-135">You need it to give to the SDK.</span></span>

![Klik op Essentials, klik op de Instrumentatiesleutel, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-the-sdk-in-your-app"></a><span data-ttu-id="cdb1f-137">De SDK installeren in uw app</span><span class="sxs-lookup"><span data-stu-id="cdb1f-137">Install the SDK in your app</span></span>
<span data-ttu-id="cdb1f-138">De Application Insights-SDK installeren in uw app.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-138">Install the Application Insights SDK in your app.</span></span> <span data-ttu-id="cdb1f-139">Deze stap is sterk afhankelijk van het type van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-139">This step depends heavily on the type of your application.</span></span> 

<span data-ttu-id="cdb1f-140">De instrumentatiesleutel gebruiken voor het configureren van [de SDK die u in uw toepassing installeert][start].</span><span class="sxs-lookup"><span data-stu-id="cdb1f-140">Use the instrumentation key to configure [the SDK that you install in your application][start].</span></span>

<span data-ttu-id="cdb1f-141">De SDK bevat standaard modules weer die het verzenden van telemetrie zonder dat u code hoeft te schrijven.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-141">The SDK includes standard modules that send telemetry without you having to write any code.</span></span> <span data-ttu-id="cdb1f-142">Voor het bijhouden van acties van de gebruiker of het analyseren van problemen in meer detail [gebruikmaken van de API] [ api] uw eigen telemetrie verzenden.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-142">To track user actions or diagnose issues in more detail, [use the API][api] to send your own telemetry.</span></span>

## <span data-ttu-id="cdb1f-143"><a name="monitor"></a>Zie telemetriegegevens</span><span class="sxs-lookup"><span data-stu-id="cdb1f-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="cdb1f-144">Sluit de blade snel starten om terug te keren naar de blade van uw toepassing in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-144">Close the quick start blade to return to your application blade in the Azure portal.</span></span>

<span data-ttu-id="cdb1f-145">Klik op de tegel Search om te zien [diagnostische gegevens doorzoeken][diagnostic], waarbij de eerste gebeurtenissen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-145">Click the Search tile to see [Diagnostic Search][diagnostic], where the first events appear.</span></span> 

<span data-ttu-id="cdb1f-146">Als u meer gegevens verwacht, klikt u op **vernieuwen** na enkele seconden.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="cdb1f-147">Het automatisch maken van een resource</span><span class="sxs-lookup"><span data-stu-id="cdb1f-147">Creating a resource automatically</span></span>
<span data-ttu-id="cdb1f-148">U kunt schrijven een [PowerShell-script](app-insights-powershell.md) automatisch maken van een resource.</span><span class="sxs-lookup"><span data-stu-id="cdb1f-148">You can write a [PowerShell script](app-insights-powershell.md) to create a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdb1f-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cdb1f-149">Next steps</span></span>
* [<span data-ttu-id="cdb1f-150">Een dashboard maken</span><span class="sxs-lookup"><span data-stu-id="cdb1f-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="cdb1f-151">Diagnostische gegevens doorzoeken</span><span class="sxs-lookup"><span data-stu-id="cdb1f-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="cdb1f-152">Metrische gegevens verkennen</span><span class="sxs-lookup"><span data-stu-id="cdb1f-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="cdb1f-153">Analytics-query's schrijven</span><span class="sxs-lookup"><span data-stu-id="cdb1f-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

