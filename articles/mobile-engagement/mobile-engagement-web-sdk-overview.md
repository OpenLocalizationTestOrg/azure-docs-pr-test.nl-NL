---
title: Overzicht van Azure Mobile Engagement Web SDK | Microsoft Docs
description: De nieuwste updates en procedures voor de webservice-SDK voor Azure Mobile Engagement
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
ms.openlocfilehash: 770a83131a3e661771db50b22ce7de25b2d541cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="8865a-103">Azure Mobile Engagement Web SDK</span><span class="sxs-lookup"><span data-stu-id="8865a-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="8865a-104">Begin hier als u de details over het integreren van Azure Mobile Engagement in een web-app.</span><span class="sxs-lookup"><span data-stu-id="8865a-104">Start here for all the details about how to integrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="8865a-105">Als u wilt u het proberen voordat het aan de slag met uw eigen web-app, raadpleegt u onze [15 minuten zelfstudie](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8865a-105">If you'd like to give it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="8865a-106">Integratie procedures</span><span class="sxs-lookup"><span data-stu-id="8865a-106">Integration procedures</span></span>
1. <span data-ttu-id="8865a-107">Meer informatie over [Mobile Engagement integreren in uw web-app](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="8865a-107">Learn [how to integrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="8865a-108">Voor implementatie van tag plan, meer [hoe u de geavanceerde Mobile Engagement tags API in uw web-app](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="8865a-108">For tag plan implementation, learn [how to use the advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="8865a-109">Releaseopmerkingen</span><span class="sxs-lookup"><span data-stu-id="8865a-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="8865a-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="8865a-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="8865a-111">Vaste crash op persoonlijke bladeren (Safari).</span><span class="sxs-lookup"><span data-stu-id="8865a-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="8865a-112">Vaste crash browsers met cookies is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8865a-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="8865a-113">Raadpleeg voor alle versies, de [voltooien releaseopmerkingen](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="8865a-113">For all versions, please see the [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="8865a-114">Upgradeprocedures</span><span class="sxs-lookup"><span data-stu-id="8865a-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-to-200"></a><span data-ttu-id="8865a-115">Upgrade uitvoeren van 1.2.1 naar 2.0.0</span><span class="sxs-lookup"><span data-stu-id="8865a-115">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="8865a-116">De volgende secties wordt beschreven hoe een Mobile Engagement Web SDK-integratie migreren vanaf de Capptain-service, die worden aangeboden door Capptain SAS, naar een Azure Mobile Engagement-app.</span><span class="sxs-lookup"><span data-stu-id="8865a-116">The following sections describe how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="8865a-117">Als u vanaf een versie ouder dan 1.2.1 migreert, neem contact op met de website Capptain om te migreren naar 1.2.1 eerst en pas de volgende procedures.</span><span class="sxs-lookup"><span data-stu-id="8865a-117">If you are migrating from a version earlier than 1.2.1, please consult the Capptain website to migrate to 1.2.1 first, and then apply the following procedures.</span></span>

<span data-ttu-id="8865a-118">Deze versie van de Mobile Engagement Web SDK biedt geen ondersteuning voor Samsung Smart TV, Opera TV, webOS of de Reach-functie.</span><span class="sxs-lookup"><span data-stu-id="8865a-118">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8865a-119">Capptain en Azure Mobile Engagement zijn niet dezelfde service en de volgende procedures Markeer alleen het migreren van de client-app.</span><span class="sxs-lookup"><span data-stu-id="8865a-119">Capptain and Azure Mobile Engagement are not the same service, and the following procedures highlight only how to migrate the client app.</span></span> <span data-ttu-id="8865a-120">Migreren van de Mobile Engagement Web SDK in de app wordt niet uw gegevens migreren vanaf een server Capptain met een Mobile Engagement-server.</span><span class="sxs-lookup"><span data-stu-id="8865a-120">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="8865a-121">JavaScript-bestanden</span><span class="sxs-lookup"><span data-stu-id="8865a-121">JavaScript files</span></span>
<span data-ttu-id="8865a-122">Het bestand capptain-sdk.js vervangen door de azure-engagement.js bestand, en werk vervolgens de invoer van uw script dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="8865a-122">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="8865a-123">Capptain Reach verwijderen</span><span class="sxs-lookup"><span data-stu-id="8865a-123">Remove Capptain Reach</span></span>
<span data-ttu-id="8865a-124">Deze versie van de Mobile Engagement Web SDK biedt geen ondersteuning voor de Reach-functie.</span><span class="sxs-lookup"><span data-stu-id="8865a-124">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="8865a-125">Als u hebt Capptain Reach geïntegreerd in uw toepassing, moet u om deze te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8865a-125">If you have integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="8865a-126">Het importeren van CSS bereiken verwijderen vanaf de pagina en verwijderen van het gerelateerde CSS-bestand (capptain-reach.css, standaard).</span><span class="sxs-lookup"><span data-stu-id="8865a-126">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="8865a-127">Verwijderen van de volgende Reach-resources: de installatiekopie van het sluiten (capptain-close.png, standaard) en het merk-pictogram (standaard capptain-melding-pictogram).</span><span class="sxs-lookup"><span data-stu-id="8865a-127">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="8865a-128">Verwijder de gebruikersinterface bereiken voor in-app-meldingen.</span><span class="sxs-lookup"><span data-stu-id="8865a-128">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="8865a-129">De standaardindeling ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="8865a-129">The default layout looks like this:</span></span>

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

<span data-ttu-id="8865a-130">Verwijder de gebruikersinterface bereiken voor tekst- en aankondigingen van web- en polls.</span><span class="sxs-lookup"><span data-stu-id="8865a-130">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="8865a-131">De standaardindeling ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="8865a-131">The default layout looks like this:</span></span>

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

<span data-ttu-id="8865a-132">Verwijder de `reach` object uit uw configuratie, indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="8865a-132">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="8865a-133">Als volgt uitziet:</span><span class="sxs-lookup"><span data-stu-id="8865a-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="8865a-134">Verwijder eventuele andere Reach-aanpassing, zoals categorieën.</span><span class="sxs-lookup"><span data-stu-id="8865a-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="8865a-135">Afgeschafte API's verwijderen</span><span class="sxs-lookup"><span data-stu-id="8865a-135">Remove deprecated APIs</span></span>
<span data-ttu-id="8865a-136">Sommige-API's van Capptain zijn afgeschaft in de Mobile Engagement Web SDK.</span><span class="sxs-lookup"><span data-stu-id="8865a-136">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="8865a-137">Verwijder alle aanroepen naar de volgende API's: `agent.connect`, `agent.disconnect`, `agent.pause`, en `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="8865a-137">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="8865a-138">Verwijder een van de volgende callbacks van uw configuratie Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, en `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="8865a-138">Remove any of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="8865a-139">Configuratie</span><span class="sxs-lookup"><span data-stu-id="8865a-139">Configuration</span></span>
<span data-ttu-id="8865a-140">Mobile Engagement gebruikt een verbindingsreeks voor het configureren van de SDK-id's, bijvoorbeeld de toepassings-id.</span><span class="sxs-lookup"><span data-stu-id="8865a-140">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="8865a-141">Vervang de toepassings-ID door de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="8865a-141">Replace the application ID with your connection string.</span></span> <span data-ttu-id="8865a-142">Let op het globale object voor de SDK-configuratie wordt gewijzigd van `capptain` naar `azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="8865a-142">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="8865a-143">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="8865a-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="8865a-144">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="8865a-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="8865a-145">De verbindingsreeks voor uw toepassing wordt weergegeven in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8865a-145">The connection string for your application is displayed in the Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="8865a-146">JavaScript-API 's</span><span class="sxs-lookup"><span data-stu-id="8865a-146">JavaScript APIs</span></span>
<span data-ttu-id="8865a-147">Het globale JavaScript-object `window.capptain` heeft gekregen `window.azureEngagement`, maar u kunt de `window.engagement` alias voor de API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="8865a-147">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="8865a-148">U kunt deze alias niet gebruiken voor het definiëren van de configuratie van de SDK.</span><span class="sxs-lookup"><span data-stu-id="8865a-148">You can't use this alias to define the SDK configuration.</span></span>

<span data-ttu-id="8865a-149">Bijvoorbeeld: `capptain.deviceId` wordt `engagement.deviceId`, `capptain.agent.startActivity` wordt `engagement.agent.startActivity`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="8865a-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="8865a-150">Als u hebt al een eerdere versie van Azure Mobile Engagement Web SDK geïntegreerd in uw toepassing, leest u over [procedures upgrade](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="8865a-150">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

