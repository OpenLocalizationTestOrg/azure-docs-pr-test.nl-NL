---
title: aaaWindows Phone Silverlight-SDK Upgrade Procedures
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
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="24579-103">Windows Phone Silverlight-SDK upgradeprocedures</span><span class="sxs-lookup"><span data-stu-id="24579-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="24579-104">Als u hebt al een oudere versie van onze SDK geïntegreerd in uw toepassing, hebt u tooconsider Hallo volgende punten bij het upgraden van Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="24579-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="24579-105">Mogelijk hebt u toofollow verschillende procedures als u verschillende versies van Hallo SDK gemist.</span><span class="sxs-lookup"><span data-stu-id="24579-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="24579-106">Bijvoorbeeld als u migreert vanaf 0.10.1 too0.11.0 hebt toofirst Volg Hallo ' van 0.9.0 too0.10.1 ' procedure vervolgens Hallo ' van 0.10.1 too0.11.0 ' procedure.</span><span class="sxs-lookup"><span data-stu-id="24579-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-200-too330"></a><span data-ttu-id="24579-107">Van 2.0.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="24579-107">From 2.0.0 too3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="24579-108">Test-Logboeken</span><span class="sxs-lookup"><span data-stu-id="24579-108">Test logs</span></span>
<span data-ttu-id="24579-109">De logboeken van de console die wordt geproduceerd door Hallo SDK kunnen worden ingeschakeld/uitgeschakeld/gefilterd.</span><span class="sxs-lookup"><span data-stu-id="24579-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="24579-110">toocustomize deze, update Hallo eigenschap `EngagementAgent.Instance.TestLogEnabled` tooone van Hallo waarde in Hallo `EngagementTestLogLevel` opsomming, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="24579-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a><span data-ttu-id="24579-111">Van 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="24579-111">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="24579-112">Hallo hieronder wordt beschreven hoe toomigrate een SDK-integratie van Hallo Capptain service aangeboden door Capptain SAS in een app die is aangedreven door Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="24579-112">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="24579-113">Capptain en Mobile Engagement dezelfde services niet zijn Hallo en Hallo onderstaande procedure alleen illustreert hoe toomigrate Hallo client-app.</span><span class="sxs-lookup"><span data-stu-id="24579-113">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="24579-114">Uw gegevens worden niet van Hallo Capptain servers toohello Mobile Engagement servers migreren Hallo SDK in Hallo-app gemigreerd</span><span class="sxs-lookup"><span data-stu-id="24579-114">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="24579-115">Als u vanaf een eerdere versie migreert, verwijder Hallo Capptain website toomigrate too1.1.1 eerst overleggen en toepassing hello procedure te volgen</span><span class="sxs-lookup"><span data-stu-id="24579-115">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="24579-116">Nuget-pakket</span><span class="sxs-lookup"><span data-stu-id="24579-116">Nuget package</span></span>
<span data-ttu-id="24579-117">Vervang **Capptain.WindowsPhone** door **MicrosoftAzure.MobileEngagement** Nuget-pakket.</span><span class="sxs-lookup"><span data-stu-id="24579-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="24579-118">Mobile Engagement toepassen</span><span class="sxs-lookup"><span data-stu-id="24579-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="24579-119">Hallo SDK gebruikt Hallo term `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="24579-119">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="24579-120">U moet tooupdate uw project toomatch deze wijziging.</span><span class="sxs-lookup"><span data-stu-id="24579-120">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="24579-121">U moet toouninstall uw huidige Capptain nuget-pakket.</span><span class="sxs-lookup"><span data-stu-id="24579-121">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="24579-122">Houd rekening met dat uw wijzigingen in de map Capptain bronnen worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="24579-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="24579-123">Als u deze bestanden tookeep wilt maken van een kopie van deze.</span><span class="sxs-lookup"><span data-stu-id="24579-123">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="24579-124">Daarna Hallo nieuwe Microsoft Azure Engagement nuget-pakket te installeren op uw project.</span><span class="sxs-lookup"><span data-stu-id="24579-124">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="24579-125">U vindt deze op [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="24579-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="24579-126">Deze actie vervangt alle bestanden van de resources gebruikt door Engagement en voegt het nieuwe Engagement DLL tooyour Hallo project verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="24579-126">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="24579-127">U hebt uw projectverwijzingen tooclean door Capptain DLL verwijzingen te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="24579-127">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="24579-128">Als u dit niet doet, Hallo-versie van Capptain conflict veroorzaken en fouten gebeurt.</span><span class="sxs-lookup"><span data-stu-id="24579-128">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="24579-129">Als u Capptain resources hebt aangepast, wordt de inhoud van uw oude bestanden kopiëren en plak deze in Hallo nieuwe Engagement bestanden.</span><span class="sxs-lookup"><span data-stu-id="24579-129">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="24579-130">Houd er rekening mee dat zowel xaml en cs-bestanden bijgewerkt toobe hebben.</span><span class="sxs-lookup"><span data-stu-id="24579-130">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="24579-131">Wanneer deze stappen zijn voltooid. hoeft u alleen tooreplace oude Capptain verwijzingen door Hallo nieuwe Engagement verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="24579-131">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="24579-132">Alle Capptain naamruimten hebben toobe bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="24579-132">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="24579-133">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="24579-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="24579-134">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="24579-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="24579-135">Alle Capptain klassen met 'Capptain' moeten 'Engagement' bevatten.</span><span class="sxs-lookup"><span data-stu-id="24579-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="24579-136">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="24579-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="24579-137">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="24579-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="24579-138">Voor xaml-bestanden wijzigen Capptain naamruimte en kenmerken ook.</span><span class="sxs-lookup"><span data-stu-id="24579-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="24579-139">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="24579-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="24579-140">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="24579-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="24579-141">Hallo voor andere bronnen zoals Capptain afbeeldingen, houd er rekening mee dat ze ook zijn gewijzigd toouse 'Engagement'.</span><span class="sxs-lookup"><span data-stu-id="24579-141">For hello other resources like Capptain pictures, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="24579-142">Toepassings-ID / SDK-sleutel</span><span class="sxs-lookup"><span data-stu-id="24579-142">Application ID / SDK Key</span></span>
<span data-ttu-id="24579-143">Engagement maakt gebruik van een verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="24579-143">Engagement uses a connection string.</span></span> <span data-ttu-id="24579-144">U hebt geen toospecify een toepassings-ID en een met Mobile Engagement SDK-sleutel, u hoeft alleen toospecify een verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="24579-144">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="24579-145">U kunt deze functie instellen op uw EngagementConfiguration-bestand.</span><span class="sxs-lookup"><span data-stu-id="24579-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="24579-146">Hallo Engagement configuratie kan worden ingesteld in uw `Resources\EngagementConfiguration.xml` -bestand van uw project.</span><span class="sxs-lookup"><span data-stu-id="24579-146">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="24579-147">Dit bestand toospecify bewerken:</span><span class="sxs-lookup"><span data-stu-id="24579-147">Edit this file toospecify:</span></span>

* <span data-ttu-id="24579-148">De verbindingsreeks voor de toepassing tussen de tags `<connectionString>` en `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="24579-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="24579-149">Als u wilt dat deze tijdens runtime in plaats daarvan kunt u bellen Hallo volgende toospecify methode voordat de initialisatie van de agent Hallo Engagement:</span><span class="sxs-lookup"><span data-stu-id="24579-149">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="24579-150">Hallo-verbindingsreeks voor uw toepassing wordt weergegeven in de klassieke Azure-Portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="24579-150">hello connection string for your application is displayed in hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="24579-151">Wijziging van items</span><span class="sxs-lookup"><span data-stu-id="24579-151">Items name change</span></span>
<span data-ttu-id="24579-152">Alle items met de naam *capptain* naam hebt gegeven *engagement*.</span><span class="sxs-lookup"><span data-stu-id="24579-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="24579-153">Op dezelfde manier voor *Capptain* te*Engagement*.</span><span class="sxs-lookup"><span data-stu-id="24579-153">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="24579-154">Voorbeelden van veelgebruikte Capptain items:</span><span class="sxs-lookup"><span data-stu-id="24579-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="24579-155">CapptainConfiguration EngagementConfiguration nu met de naam</span><span class="sxs-lookup"><span data-stu-id="24579-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="24579-156">CapptainAgent EngagementAgent nu met de naam</span><span class="sxs-lookup"><span data-stu-id="24579-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="24579-157">CapptainReach EngagementReach nu met de naam</span><span class="sxs-lookup"><span data-stu-id="24579-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="24579-158">CapptainHttpConfig EngagementHttpConfig nu met de naam</span><span class="sxs-lookup"><span data-stu-id="24579-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="24579-159">GetCapptainPageName GetEngagementPageName nu met de naam</span><span class="sxs-lookup"><span data-stu-id="24579-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="24579-160">Houd er rekening mee dat rename ook van invloed op overschreven methoden.</span><span class="sxs-lookup"><span data-stu-id="24579-160">Note that rename also affects overridden methods.</span></span>

