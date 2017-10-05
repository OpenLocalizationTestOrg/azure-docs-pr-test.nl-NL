---
title: Windows Phone Silverlight-SDK upgradeprocedures
description: Windows Phone Silverlight-SDK upgradeprocedures voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f87f65788075c7f4067e77946e1bcbc8f3709317
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="14908-103">Windows Phone Silverlight-SDK upgradeprocedures</span><span class="sxs-lookup"><span data-stu-id="14908-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="14908-104">Als u hebt al een oudere versie van onze SDK geïntegreerd in uw toepassing, hebt u de volgende punten overwegen bij het upgraden van de SDK.</span><span class="sxs-lookup"><span data-stu-id="14908-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="14908-105">U moet verschillende procedures volgen als u verschillende versies van de SDK hebt gemist.</span><span class="sxs-lookup"><span data-stu-id="14908-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="14908-106">Bijvoorbeeld als u migreert van 0.10.1 naar u moet eerst Volg de procedure 'van 0.9.0 naar 0.10.1' 0.11.0 vervolgens de procedure 'van 0.10.1 naar 0.11.0'.</span><span class="sxs-lookup"><span data-stu-id="14908-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-200-to-330"></a><span data-ttu-id="14908-107">Van 2.0.0 naar 3.3.0</span><span class="sxs-lookup"><span data-stu-id="14908-107">From 2.0.0 to 3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="14908-108">Test-Logboeken</span><span class="sxs-lookup"><span data-stu-id="14908-108">Test logs</span></span>
<span data-ttu-id="14908-109">De logboeken van de console die wordt geproduceerd door de SDK kunnen worden ingeschakeld/uitgeschakeld/gefilterd.</span><span class="sxs-lookup"><span data-stu-id="14908-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="14908-110">Werk de eigenschap voor het aanpassen van dit `EngagementAgent.Instance.TestLogEnabled` op een van de waarde in de `EngagementTestLogLevel` opsomming, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="14908-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-to-200"></a><span data-ttu-id="14908-111">Van 1.1.1 naar 2.0.0</span><span class="sxs-lookup"><span data-stu-id="14908-111">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="14908-112">De volgende beschrijft het migreren van een SDK-integratie van de service van Capptain SAS Capptain in een app die is aangedreven door Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="14908-112">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="14908-113">Capptain en Mobile Engagement zijn niet dezelfde services en de procedure die hieronder wordt alleen uitgelegd hoe u voor het migreren van de client-app.</span><span class="sxs-lookup"><span data-stu-id="14908-113">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="14908-114">Migreren van de SDK in de app wordt niet uw gegevens migreren van de servers Capptain naar de Mobile Engagement-servers</span><span class="sxs-lookup"><span data-stu-id="14908-114">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="14908-115">Als u vanaf een eerdere versie migreert, raadpleegt u de Capptain-website om te migreren naar 1.1.1 eerst en vervolgens de volgende procedure toepassen</span><span class="sxs-lookup"><span data-stu-id="14908-115">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="14908-116">Nuget-pakket</span><span class="sxs-lookup"><span data-stu-id="14908-116">Nuget package</span></span>
<span data-ttu-id="14908-117">Vervang **Capptain.WindowsPhone** door **MicrosoftAzure.MobileEngagement** Nuget-pakket.</span><span class="sxs-lookup"><span data-stu-id="14908-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="14908-118">Mobile Engagement toepassen</span><span class="sxs-lookup"><span data-stu-id="14908-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="14908-119">De SDK gebruikt de term `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="14908-119">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="14908-120">U moet uw project zodat deze overeenkomt met deze wijziging bijwerken.</span><span class="sxs-lookup"><span data-stu-id="14908-120">You need to update your project to match this change.</span></span>

<span data-ttu-id="14908-121">U moet uw huidige Capptain nuget-pakket te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="14908-121">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="14908-122">Houd rekening met dat uw wijzigingen in de map Capptain bronnen worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="14908-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="14908-123">Als u wilt behouden die bestanden vervolgens een kopie maken van deze.</span><span class="sxs-lookup"><span data-stu-id="14908-123">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="14908-124">Daarna het nieuwe Microsoft Azure Engagement nuget-pakket te installeren op uw project.</span><span class="sxs-lookup"><span data-stu-id="14908-124">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="14908-125">U vindt deze op [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="14908-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="14908-126">Deze bewerking vervangt alle resources bestanden die worden gebruikt door Engagement en voegt u het nieuwe Engagement dll-bestand toe aan de projectverwijzingen.</span><span class="sxs-lookup"><span data-stu-id="14908-126">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="14908-127">U moet uw projectverwijzingen door Capptain DLL verwijzingen te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="14908-127">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="14908-128">Als u dit niet doet, wordt de versie van Capptain conflict veroorzaken en fouten gebeurt.</span><span class="sxs-lookup"><span data-stu-id="14908-128">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="14908-129">Als u Capptain resources hebt aangepast, uw oude bestanden inhoud kopiëren en plak deze in de nieuwe Engagement-bestanden.</span><span class="sxs-lookup"><span data-stu-id="14908-129">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="14908-130">Houd er rekening mee dat zowel xaml en cs-bestanden moeten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="14908-130">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="14908-131">Wanneer deze stappen zijn voltooid. hoeft u alleen oude Capptain verwijzingen door de nieuwe Engagement verwijzingen moeten worden vervangen.</span><span class="sxs-lookup"><span data-stu-id="14908-131">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="14908-132">Alle Capptain naamruimten moeten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="14908-132">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="14908-133">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="14908-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="14908-134">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="14908-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="14908-135">Alle Capptain klassen met 'Capptain' moeten 'Engagement' bevatten.</span><span class="sxs-lookup"><span data-stu-id="14908-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="14908-136">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="14908-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="14908-137">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="14908-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="14908-138">Voor xaml-bestanden wijzigen Capptain naamruimte en kenmerken ook.</span><span class="sxs-lookup"><span data-stu-id="14908-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="14908-139">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="14908-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="14908-140">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="14908-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="14908-141">Voor de andere resources zoals Capptain afbeeldingen, houd er rekening mee dat ze ook zijn gewijzigd voor het gebruik van 'Engagement'.</span><span class="sxs-lookup"><span data-stu-id="14908-141">For the other resources like Capptain pictures, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="14908-142">Toepassings-ID / SDK-sleutel</span><span class="sxs-lookup"><span data-stu-id="14908-142">Application ID / SDK Key</span></span>
<span data-ttu-id="14908-143">Engagement maakt gebruik van een verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="14908-143">Engagement uses a connection string.</span></span> <span data-ttu-id="14908-144">U hoeft niet te geven van een toepassings-ID en een SDK-sleutel met Mobile Engagement, hoeft u een verbindingsreeks opgeven.</span><span class="sxs-lookup"><span data-stu-id="14908-144">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="14908-145">U kunt deze functie instellen op uw EngagementConfiguration-bestand.</span><span class="sxs-lookup"><span data-stu-id="14908-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="14908-146">De configuratie van de Engagement kan worden ingesteld in uw `Resources\EngagementConfiguration.xml` -bestand van uw project.</span><span class="sxs-lookup"><span data-stu-id="14908-146">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="14908-147">Dit bestand op te geven bewerken:</span><span class="sxs-lookup"><span data-stu-id="14908-147">Edit this file to specify:</span></span>

* <span data-ttu-id="14908-148">De verbindingsreeks voor de toepassing tussen de tags `<connectionString>` en `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="14908-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="14908-149">Als u in plaats daarvan tijdens runtime opgeven wilt, kunt u de volgende methode voordat de initialisatie van de Engagement-agent kunt aanroepen:</span><span class="sxs-lookup"><span data-stu-id="14908-149">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="14908-150">De verbindingsreeks voor uw toepassing wordt weergegeven in de klassieke Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="14908-150">The connection string for your application is displayed in the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="14908-151">Wijziging van items</span><span class="sxs-lookup"><span data-stu-id="14908-151">Items name change</span></span>
<span data-ttu-id="14908-152">Alle items met de naam *capptain* naam hebt gegeven *engagement*.</span><span class="sxs-lookup"><span data-stu-id="14908-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="14908-153">Op dezelfde manier voor *Capptain* naar *Engagement*.</span><span class="sxs-lookup"><span data-stu-id="14908-153">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="14908-154">Voorbeelden van veelgebruikte Capptain items:</span><span class="sxs-lookup"><span data-stu-id="14908-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="14908-155">CapptainConfiguration EngagementConfiguration nu met de naam</span><span class="sxs-lookup"><span data-stu-id="14908-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="14908-156">CapptainAgent EngagementAgent nu met de naam</span><span class="sxs-lookup"><span data-stu-id="14908-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="14908-157">CapptainReach EngagementReach nu met de naam</span><span class="sxs-lookup"><span data-stu-id="14908-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="14908-158">CapptainHttpConfig EngagementHttpConfig nu met de naam</span><span class="sxs-lookup"><span data-stu-id="14908-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="14908-159">GetCapptainPageName GetEngagementPageName nu met de naam</span><span class="sxs-lookup"><span data-stu-id="14908-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="14908-160">Houd er rekening mee dat rename ook van invloed op overschreven methoden.</span><span class="sxs-lookup"><span data-stu-id="14908-160">Note that rename also affects overridden methods.</span></span>

