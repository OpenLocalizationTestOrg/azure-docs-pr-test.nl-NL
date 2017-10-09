---
title: Overzicht van Mobile Engagement Web SDK aaaAzure | Microsoft Docs
description: meest recente updates en procedures voor het Hallo Web SDK voor Azure Mobile Engagement Hallo
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 5bbc2fda-0f3f-43d0-a73d-0f2c0f8dc25b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 10/18/2016
ms.author: piyushjo
ms.openlocfilehash: 9e60a232b5eb2c41c405041a88e09d7137563513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="80d3e-103">Azure Mobile Engagement Web SDK</span><span class="sxs-lookup"><span data-stu-id="80d3e-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="80d3e-104">Hier wordt gestart voor alle informatie over het Hallo toointegrate Azure Mobile Engagement in een web-app.</span><span class="sxs-lookup"><span data-stu-id="80d3e-104">Start here for all hello details about how toointegrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="80d3e-105">Als u toogive wilt deze een try voordat het aan de slag met uw eigen web-app, Zie onze [15 minuten zelfstudie](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="80d3e-105">If you'd like toogive it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="80d3e-106">Integratie procedures</span><span class="sxs-lookup"><span data-stu-id="80d3e-106">Integration procedures</span></span>
1. <span data-ttu-id="80d3e-107">Meer informatie over [hoe toointegrate Mobile Engagement in uw web-app](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="80d3e-107">Learn [how toointegrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="80d3e-108">Voor implementatie van tag plan, meer [hoe toouse Hallo Mobile Engagement tags API in uw web-app geavanceerde](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="80d3e-108">For tag plan implementation, learn [how toouse hello advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="80d3e-109">Releaseopmerkingen</span><span class="sxs-lookup"><span data-stu-id="80d3e-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="80d3e-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="80d3e-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="80d3e-111">Vaste crash op persoonlijke bladeren (Safari).</span><span class="sxs-lookup"><span data-stu-id="80d3e-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="80d3e-112">Vaste crash browsers met cookies is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="80d3e-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="80d3e-113">Zie voor alle versies Hallo [voltooien releaseopmerkingen](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="80d3e-113">For all versions, please see hello [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="80d3e-114">Upgradeprocedures</span><span class="sxs-lookup"><span data-stu-id="80d3e-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-too200"></a><span data-ttu-id="80d3e-115">Upgrade van 1.2.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="80d3e-115">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="80d3e-116">Hallo volgende secties wordt beschreven hoe toomigrate een Mobile Engagement Web SDK-integratie van Hallo Capptain service, die worden aangeboden door Capptain SAS, tooan Azure Mobile Engagement-app.</span><span class="sxs-lookup"><span data-stu-id="80d3e-116">hello following sections describe how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="80d3e-117">Als u migreert vanaf een eerdere versie dan 1.2.1, Raadpleeg Hallo Capptain website toomigrate too1.2.1 eerst en vervolgens toepassen Hallo procedures te volgen.</span><span class="sxs-lookup"><span data-stu-id="80d3e-117">If you are migrating from a version earlier than 1.2.1, please consult hello Capptain website toomigrate too1.2.1 first, and then apply hello following procedures.</span></span>

<span data-ttu-id="80d3e-118">Deze versie van Hallo Mobile Engagement Web SDK biedt geen ondersteuning voor Samsung Smart TV, Opera TV, webOS of Hallo Reach-functie.</span><span class="sxs-lookup"><span data-stu-id="80d3e-118">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80d3e-119">Capptain en Azure Mobile Engagement zijn niet dezelfde service Hallo en Hallo procedures te volgen Markeer alleen toomigrate Hallo client-app.</span><span class="sxs-lookup"><span data-stu-id="80d3e-119">Capptain and Azure Mobile Engagement are not hello same service, and hello following procedures highlight only how toomigrate hello client app.</span></span> <span data-ttu-id="80d3e-120">Migreren Hallo Mobile Engagement Web SDK in Hallo-app wordt niet uw gegevens migreren vanaf een Capptain tooa Mobile Engagement-server.</span><span class="sxs-lookup"><span data-stu-id="80d3e-120">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="80d3e-121">JavaScript-bestanden</span><span class="sxs-lookup"><span data-stu-id="80d3e-121">JavaScript files</span></span>
<span data-ttu-id="80d3e-122">Vervangen Hallo bestand capptain-sdk.js Hello azure engagement.js bestand, en werk uw invoer script vervolgens dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="80d3e-122">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="80d3e-123">Capptain Reach verwijderen</span><span class="sxs-lookup"><span data-stu-id="80d3e-123">Remove Capptain Reach</span></span>
<span data-ttu-id="80d3e-124">Deze versie van Hallo Mobile Engagement Web SDK biedt geen ondersteuning voor Hallo Reach-functie.</span><span class="sxs-lookup"><span data-stu-id="80d3e-124">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="80d3e-125">Als u hebt Capptain Reach geïntegreerd in uw toepassing, moet u tooremove deze.</span><span class="sxs-lookup"><span data-stu-id="80d3e-125">If you have integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="80d3e-126">Hallo bereiken CSS importeren uit uw pagina verwijderen en verwijder Hallo gerelateerde CSS-bestand (capptain-reach.css, standaard).</span><span class="sxs-lookup"><span data-stu-id="80d3e-126">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="80d3e-127">Verwijderen van Hallo Reach-resources te volgen: Hallo Hallo merk-pictogram (standaard capptain-melding-pictogram) en sluiten afbeelding (capptain-close.png, standaard).</span><span class="sxs-lookup"><span data-stu-id="80d3e-127">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="80d3e-128">Verwijder Hallo UI bereiken voor in-app-meldingen.</span><span class="sxs-lookup"><span data-stu-id="80d3e-128">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="80d3e-129">Hallo-standaardindeling ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="80d3e-129">hello default layout looks like this:</span></span>

    <!-- capptain notification -->
    <div id="capptain_notification_area" class="capptain_category_default">
      <div class="icon">
        <img src="capptain-notification-icon.png" alt="icon" />
      </div>
      <div class="content">
        <div class="title" id="capptain_notification_title"></div>
        <div class="message" id="capptain_notification_message"></div>
      </div>
      <div id="capptain_notification_image"></div>
      <div>
        <button id="capptain_notification_close">Close</button>
      </div>
    </div>

<span data-ttu-id="80d3e-130">Hallo UI bereiken voor tekst- en aankondigingen en polls verwijderen.</span><span class="sxs-lookup"><span data-stu-id="80d3e-130">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="80d3e-131">Hallo-standaardindeling ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="80d3e-131">hello default layout looks like this:</span></span>

    <div id="capptain_overlay" class="capptain_category_default">
      <button id="capptain_overlay_close">x</button>
      <div id="capptain_overlay_title"></div>
      <div id="capptain_overlay_body"></div>
      <div id="capptain_overlay_poll"></div>
      <div id="capptain_overlay_buttons">
        <button id="capptain_overlay_exit"></button>
        <button id="capptain_overlay_action"></button>
      </div>
    </div>

<span data-ttu-id="80d3e-132">Hallo verwijderen `reach` object uit uw configuratie, indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="80d3e-132">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="80d3e-133">Als volgt uitziet:</span><span class="sxs-lookup"><span data-stu-id="80d3e-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="80d3e-134">Verwijder eventuele andere Reach-aanpassing, zoals categorieën.</span><span class="sxs-lookup"><span data-stu-id="80d3e-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="80d3e-135">Afgeschafte API's verwijderen</span><span class="sxs-lookup"><span data-stu-id="80d3e-135">Remove deprecated APIs</span></span>
<span data-ttu-id="80d3e-136">Sommige-API's van Capptain zijn afgeschaft in Hallo Mobile Engagement Web SDK.</span><span class="sxs-lookup"><span data-stu-id="80d3e-136">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="80d3e-137">Verwijder alle aanroepen toohello API's te volgen: `agent.connect`, `agent.disconnect`, `agent.pause`, en `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="80d3e-137">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="80d3e-138">Verwijder een van volgende retouraanroepen uit de configuratie van uw Capptain Hallo: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, en `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="80d3e-138">Remove any of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="80d3e-139">Configuratie</span><span class="sxs-lookup"><span data-stu-id="80d3e-139">Configuration</span></span>
<span data-ttu-id="80d3e-140">Mobile Engagement maakt gebruik van een verbinding tekenreeks tooconfigure SDK-id's, bijvoorbeeld Hallo toepassings-id.</span><span class="sxs-lookup"><span data-stu-id="80d3e-140">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="80d3e-141">Hallo toepassings-ID vervangen door de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="80d3e-141">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="80d3e-142">Houd er rekening mee dat globale Hallo-object voor Hallo SDK-configuratie wordt gewijzigd van `capptain` te`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="80d3e-142">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="80d3e-143">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="80d3e-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="80d3e-144">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="80d3e-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="80d3e-145">Hallo-verbindingsreeks voor uw toepassing wordt weergegeven in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="80d3e-145">hello connection string for your application is displayed in hello Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="80d3e-146">JavaScript-API 's</span><span class="sxs-lookup"><span data-stu-id="80d3e-146">JavaScript APIs</span></span>
<span data-ttu-id="80d3e-147">Hallo globale JavaScript-object `window.capptain` heeft gekregen `window.azureEngagement`, maar u kunt Hallo `window.engagement` alias voor de API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="80d3e-147">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="80d3e-148">U kunt deze alias toodefine Hallo SDK-configuratie niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="80d3e-148">You can't use this alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="80d3e-149">Bijvoorbeeld: `capptain.deviceId` wordt `engagement.deviceId`, `capptain.agent.startActivity` wordt `engagement.agent.startActivity`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="80d3e-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="80d3e-150">Als u hebt al een eerdere versie van Azure Mobile Engagement Web SDK Hallo geïntegreerd in uw toepassing, leest u over [procedures upgrade](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="80d3e-150">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

