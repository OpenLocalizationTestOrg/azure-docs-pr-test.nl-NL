---
title: aaaAzure Mobile Engagement Web SDK upgradeprocedures | Microsoft Docs
description: meest recente updates en procedures voor het Hallo Web SDK voor Azure Mobile Engagement Hallo
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a20529b4-ec8d-4503-8ae9-09b5f0846d5b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: a2df65904c6b56584ce6588ed26a9b79f3aa27ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="9d1f0-103">Azure Mobile Engagement Web SDK upgradeprocedures</span><span class="sxs-lookup"><span data-stu-id="9d1f0-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="9d1f0-104">Als u hebt al een eerdere versie van Azure Mobile Engagement Web SDK Hallo geïntegreerd in uw webtoepassing, moet u tooconsider Hallo volgende punten wanneer u een upgrade uitvoert van Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-104">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your web application, you need tooconsider hello following points when you upgrade hello SDK.</span></span>

<span data-ttu-id="9d1f0-105">Als u meerdere versies van Mobile Engagement Web SDK Hallo overgeslagen, moet u mogelijk toocomplete verschillende procedures tijdens het upgradeproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-105">If you skipped multiple versions of hello Mobile Engagement Web SDK, you might need toocomplete several procedures during hello upgrade process.</span></span> <span data-ttu-id="9d1f0-106">Bijvoorbeeld, als u migreert vanaf 1.4.0 too1.6.0, eerste Volg Hallo procedures tooupgrade van 1.4.0 too1.5.0.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-106">For example, if you migrate from 1.4.0 too1.6.0, first follow hello procedures tooupgrade from 1.4.0 too1.5.0.</span></span> <span data-ttu-id="9d1f0-107">Volg daarna Hallo procedures tooupgrade van 1.5.0 too1.6.0.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-107">Then, follow hello procedures tooupgrade from 1.5.0 too1.6.0.</span></span>

<span data-ttu-id="9d1f0-108">Welke versie u een van upgrade, vervangen door een eerdere versie van Hallo bestand azure-engagement.js Hallo meest recente versie van Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-108">Whichever version you upgrade from, replace any earlier version of hello file azure-engagement.js with hello latest version of hello file.</span></span>

## <a name="upgrade-from-121-too200"></a><span data-ttu-id="9d1f0-109">Upgrade van 1.2.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="9d1f0-109">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="9d1f0-110">Deze sectie beschrijft hoe toomigrate een Mobile Engagement Web SDK-integratie van Hallo Capptain service, die worden aangeboden door Capptain SAS, tooan Azure Mobile Engagement-app.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-110">This section describes how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="9d1f0-111">Als u vanaf een eerdere versie, neem Raadpleeg Hallo Capptain website toofirst migreert too1.2.1 migreren en vervolgens toepassen Hallo procedures te volgen.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-111">If you are migrating from an earlier version, please consult hello Capptain website toofirst migrate too1.2.1, and then apply hello following procedures.</span></span>

<span data-ttu-id="9d1f0-112">Deze versie van Hallo Mobile Engagement Web SDK biedt geen ondersteuning voor Samsung Smart TV, Opera TV, webOS of Hallo Reach-functie.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-112">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d1f0-113">Capptain en Azure Mobile Engagement zijn niet dezelfde service Hallo.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-113">Capptain and Azure Mobile Engagement are not hello same service.</span></span> <span data-ttu-id="9d1f0-114">Hallo na procedure licht alleen toomigrate Hallo client-app.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-114">hello following procedure highlights only how toomigrate hello client app.</span></span> <span data-ttu-id="9d1f0-115">Migreren Hallo Mobile Engagement Web SDK in Hallo-app wordt niet uw gegevens migreren vanaf een Capptain tooa Mobile Engagement-server.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-115">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="9d1f0-116">JavaScript-bestanden</span><span class="sxs-lookup"><span data-stu-id="9d1f0-116">JavaScript files</span></span>
<span data-ttu-id="9d1f0-117">Vervangen Hallo bestand capptain-sdk.js Hello azure engagement.js bestand, en werk uw invoer script vervolgens dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-117">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="9d1f0-118">Capptain Reach verwijderen</span><span class="sxs-lookup"><span data-stu-id="9d1f0-118">Remove Capptain Reach</span></span>
<span data-ttu-id="9d1f0-119">Deze versie van Hallo Mobile Engagement Web SDK biedt geen ondersteuning voor Hallo Reach-functie.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-119">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="9d1f0-120">Als u Capptain Reach geïntegreerd in uw toepassing, moet u tooremove deze.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-120">If you integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="9d1f0-121">Hallo bereiken CSS importeren uit uw pagina verwijderen en verwijder Hallo gerelateerde CSS-bestand (capptain-reach.css, standaard).</span><span class="sxs-lookup"><span data-stu-id="9d1f0-121">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="9d1f0-122">Verwijderen van Hallo Reach-resources te volgen: Hallo Hallo merk-pictogram (standaard capptain-melding-pictogram) en sluiten afbeelding (capptain-close.png, standaard).</span><span class="sxs-lookup"><span data-stu-id="9d1f0-122">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="9d1f0-123">Verwijder Hallo UI bereiken voor in-app-meldingen.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-123">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="9d1f0-124">Hallo-standaardindeling ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="9d1f0-124">hello default layout looks like this:</span></span>

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

<span data-ttu-id="9d1f0-125">Hallo UI bereiken voor tekst- en aankondigingen en polls verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-125">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="9d1f0-126">Hallo-standaardindeling ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="9d1f0-126">hello default layout looks like this:</span></span>

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

<span data-ttu-id="9d1f0-127">Hallo verwijderen `reach` object uit uw configuratie, indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-127">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="9d1f0-128">Als volgt uitziet:</span><span class="sxs-lookup"><span data-stu-id="9d1f0-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="9d1f0-129">Verwijder eventuele andere Reach-aanpassing, zoals categorieën.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="9d1f0-130">Afgeschafte API's verwijderen</span><span class="sxs-lookup"><span data-stu-id="9d1f0-130">Remove deprecated APIs</span></span>
<span data-ttu-id="9d1f0-131">Sommige-API's van Capptain zijn afgeschaft in Hallo Mobile Engagement Web SDK.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-131">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="9d1f0-132">Verwijder alle aanroepen toohello API's te volgen: `agent.connect`, `agent.disconnect`, `agent.pause`, en `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-132">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="9d1f0-133">Verwijder alle exemplaren van de volgende retouraanroepen uit de configuratie van uw Capptain Hallo: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, en `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-133">Remove any instances of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="9d1f0-134">Configuratie</span><span class="sxs-lookup"><span data-stu-id="9d1f0-134">Configuration</span></span>
<span data-ttu-id="9d1f0-135">Mobile Engagement maakt gebruik van een verbinding tekenreeks tooconfigure SDK-id's, bijvoorbeeld Hallo toepassings-id.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-135">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="9d1f0-136">Hallo toepassings-ID vervangen door de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-136">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="9d1f0-137">Houd er rekening mee dat globale Hallo-object voor Hallo SDK-configuratie wordt gewijzigd van `capptain` te`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-137">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="9d1f0-138">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="9d1f0-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="9d1f0-139">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="9d1f0-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="9d1f0-140">Hallo-verbindingsreeks voor uw toepassing wordt weergegeven in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-140">hello connection string for your application is displayed in hello Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="9d1f0-141">JavaScript-API 's</span><span class="sxs-lookup"><span data-stu-id="9d1f0-141">JavaScript APIs</span></span>
<span data-ttu-id="9d1f0-142">Hallo globale JavaScript-object `window.capptain` heeft gekregen `window.azureEngagement` , maar u kunt Hallo `window.engagement` alias voor de API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-142">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="9d1f0-143">U kunt Hallo alias toodefine Hallo SDK configuratie niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-143">You can't use hello alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="9d1f0-144">Bijvoorbeeld: `capptain.deviceId` wordt `engagement.deviceId`, `capptain.agent.startActivity` wordt `engagement.agent.startActivity`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="9d1f0-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

