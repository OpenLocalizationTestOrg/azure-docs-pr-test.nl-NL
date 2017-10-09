---
title: aaaAzure Mobile Engagement Troubleshooting Guide - Service
description: Troubleshooting Guide voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="e349d-103">Gids voor probleemoplossing voor problemen met de Service</span><span class="sxs-lookup"><span data-stu-id="e349d-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="e349d-104">Hallo volgen mogelijke problemen die optreden bij hoe Azure Mobile Engagement wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e349d-104">hello following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="e349d-105">Serviceonderbrekingen</span><span class="sxs-lookup"><span data-stu-id="e349d-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="e349d-106">Probleem</span><span class="sxs-lookup"><span data-stu-id="e349d-106">Issue</span></span>
* <span data-ttu-id="e349d-107">Problemen die worden veroorzaakt door Azure Mobile Engagement serviceonderbrekingen toobe weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e349d-107">Issues that appear toobe caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="e349d-108">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="e349d-108">Causes</span></span>
* <span data-ttu-id="e349d-109">Problemen die worden veroorzaakt door Azure Mobile Engagement serviceonderbrekingen toobe weergegeven kunnen zijn veroorzaakt door verschillende andere problemen:</span><span class="sxs-lookup"><span data-stu-id="e349d-109">Issues that appear toobe caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="e349d-110">Geïsoleerde problemen die oorspronkelijk al tooall van Azure Mobile Engagement weergegeven</span><span class="sxs-lookup"><span data-stu-id="e349d-110">Isolated issues that originally appear systemic tooall of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="e349d-111">Bekende problemen veroorzaakt door serverstoringen (die niet altijd wordt weergegeven in de serverstatus):</span><span class="sxs-lookup"><span data-stu-id="e349d-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="e349d-112">Voor de planning vertragingen, fouten Targeting, problemen Badge-update, statistieken stop verzamelen, werkt niet voor Push kan niet-API's meer werken, nieuwe apps of gebruikers worden gemaakt, DNS-fouten en time-outfouten in Hallo UI of API-Apps op een apparaat.</span><span class="sxs-lookup"><span data-stu-id="e349d-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in hello UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="e349d-113">Afhankelijkheid uitval cloud [Azure servicestatus](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="e349d-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="e349d-114">Push Notification Services (PNS) afhankelijkheid uitval</span><span class="sxs-lookup"><span data-stu-id="e349d-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="e349d-115">App Store uitval</span><span class="sxs-lookup"><span data-stu-id="e349d-115">App Store Outages</span></span>

1) <span data-ttu-id="e349d-116">tootest toosee als Hallo probleem al kunt u dezelfde functie uit een andere Hallo testen</span><span class="sxs-lookup"><span data-stu-id="e349d-116">tootest toosee if hello problem is systemic you can test hello same function from a different</span></span>

* <span data-ttu-id="e349d-117">Azure Mobile Engagement geïntegreerde toepassing</span><span class="sxs-lookup"><span data-stu-id="e349d-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="e349d-118">Testapparaat</span><span class="sxs-lookup"><span data-stu-id="e349d-118">Test device</span></span>
* <span data-ttu-id="e349d-119">Testversie van het besturingssysteem van het apparaat</span><span class="sxs-lookup"><span data-stu-id="e349d-119">Test device OS version</span></span>
* <span data-ttu-id="e349d-120">Campagne</span><span class="sxs-lookup"><span data-stu-id="e349d-120">Campaign</span></span>
* <span data-ttu-id="e349d-121">Beheerdersaccount</span><span class="sxs-lookup"><span data-stu-id="e349d-121">Administrator user account</span></span>
* <span data-ttu-id="e349d-122">Browser (IE, Firefox, Chrome, enz.)</span><span class="sxs-lookup"><span data-stu-id="e349d-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="e349d-123">Computer</span><span class="sxs-lookup"><span data-stu-id="e349d-123">Computer</span></span>

2) <span data-ttu-id="e349d-124">tootest als Hallo probleem alleen betrekking heeft op Hallo UI of Hallo-API's:</span><span class="sxs-lookup"><span data-stu-id="e349d-124">tootest if hello problem only affects hello UI or hello API's:</span></span>

* <span data-ttu-id="e349d-125">Test hello dezelfde functioneren van beide hello Azure Mobile Engagement-UI en hello Azure Mobile Engagement-API's.</span><span class="sxs-lookup"><span data-stu-id="e349d-125">Test hello same function from both hello Azure Mobile Engagement UI and hello Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="e349d-126">tootest als Hallo probleem met het netwerk van uw mobiele telefoon is:</span><span class="sxs-lookup"><span data-stu-id="e349d-126">tootest if hello problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="e349d-127">Tijdens het verbonden toohello Internet via Wi-Fi en verbonden via het netwerk van de mobiele telefoon 3G testen.</span><span class="sxs-lookup"><span data-stu-id="e349d-127">Test while connected toohello Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="e349d-128">Controleer of de firewall niet hello Azure Mobile Engagement IP-adressen of poorten blokkeert.</span><span class="sxs-lookup"><span data-stu-id="e349d-128">Confirm that your firewall is not blocking any of hello Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="e349d-129">tootest als Hallo probleem met uw apparaat is:</span><span class="sxs-lookup"><span data-stu-id="e349d-129">tootest if hello problem is with your Device:</span></span>

* <span data-ttu-id="e349d-130">Als het apparaat kunnen tooconnect tooAzure Mobile Engagement met een andere geïntegreerde Azure Mobile Engagement-app testen.</span><span class="sxs-lookup"><span data-stu-id="e349d-130">Test if your Device is able tooconnect tooAzure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="e349d-131">Test die u kunt gebeurtenissen, taken en Crashes van uw telefoon die kan worden bekeken in hello Azure Mobile Engagement UI genereren.</span><span class="sxs-lookup"><span data-stu-id="e349d-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in hello Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="e349d-132">Testen of u pushmeldingen verzenden vanuit hello Azure Mobile Engagement UI tooyour apparaat op basis van de apparaat-ID kunt.</span><span class="sxs-lookup"><span data-stu-id="e349d-132">Test if you can send push notifications from hello Azure Mobile Engagement UI tooyour device based on its Device ID.</span></span> 

5) <span data-ttu-id="e349d-133">tootest als Hallo probleem met uw App is:</span><span class="sxs-lookup"><span data-stu-id="e349d-133">tootest if hello problem is with your App:</span></span>

* <span data-ttu-id="e349d-134">Installeren en testen van de toepassing van een emulator in plaats van vanaf een fysiek apparaat:</span><span class="sxs-lookup"><span data-stu-id="e349d-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="e349d-135">tootest als Hallo probleem is met upgrades tooend besturingssysteemgebruiker apparaten waarvoor een upgrade tooresolve SDK:</span><span class="sxs-lookup"><span data-stu-id="e349d-135">tootest if hello problem is with OS upgrades tooend user Devices, which require an SDK upgrade tooresolve:</span></span>

* <span data-ttu-id="e349d-136">Test uw toepassing op verschillende apparaten met verschillende versies van Hallo OS.</span><span class="sxs-lookup"><span data-stu-id="e349d-136">Test your application on different devices with different versions of hello OS.</span></span>
* <span data-ttu-id="e349d-137">Bevestig dat u van de meest recente versie Hallo Hallo SDK gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="e349d-137">Confirm that you are using hello most recent version of hello SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="e349d-138">Connectiviteit en onjuiste informatie over problemen</span><span class="sxs-lookup"><span data-stu-id="e349d-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="e349d-139">Probleem</span><span class="sxs-lookup"><span data-stu-id="e349d-139">Issue</span></span>
* <span data-ttu-id="e349d-140">Problemen met aanmelden bij hello Azure Mobile Engagement-gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="e349d-140">Problems logging into hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="e349d-141">Verbindingsfouten Hello Azure Mobile Engagement-API van.</span><span class="sxs-lookup"><span data-stu-id="e349d-141">Connection errors with hello Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="e349d-142">Problemen met het App-Info labels uploaden via Hallo apparaat-API.</span><span class="sxs-lookup"><span data-stu-id="e349d-142">Problems uploading App Info Tags via hello Device API.</span></span>
* <span data-ttu-id="e349d-143">Problemen bij het downloaden van Logboeken of de geëxporteerde gegevens van Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e349d-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="e349d-144">Onjuiste gegevens in hello Azure Mobile Engagement-gebruikersinterface wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e349d-144">Incorrect information shown in hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="e349d-145">Onjuiste informatie die wordt weergegeven in Azure Mobile Engagement-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="e349d-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="e349d-146">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="e349d-146">Causes</span></span>
* <span data-ttu-id="e349d-147">Bevestig dat uw gebruikersaccount heeft onvoldoende machtigingen tooperform Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="e349d-147">Confirm your user account has sufficient permissions tooperform hello task.</span></span>
* <span data-ttu-id="e349d-148">Bevestig dat Hallo-probleem is niet geïsoleerd tooone computer of uw lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="e349d-148">Confirm that hello problem is not isolated tooone computer or your local network.</span></span>
* <span data-ttu-id="e349d-149">Controleer of deze hello Azure Mobile Engagement-service geen gemelde storingen heeft.</span><span class="sxs-lookup"><span data-stu-id="e349d-149">Confirm that that hello Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="e349d-150">Bevestig dat uw App-Info label bestanden al deze regels volgen:</span><span class="sxs-lookup"><span data-stu-id="e349d-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="e349d-151">Gebruik alleen Hallo UTF8-tekenset (Hallo ANSI-tekenset wordt niet ondersteund).</span><span class="sxs-lookup"><span data-stu-id="e349d-151">Use only hello UTF8 character set (hello ANSI character set is not supported).</span></span>
  * <span data-ttu-id="e349d-152">Gebruik een komma "," als scheidingsteken hello (u kunt een scheidingsteken van service aanvraag toorequest toochange Hallo CSV openen vanuit een komma "," tooanother teken, zoals een puntkomma ';').</span><span class="sxs-lookup"><span data-stu-id="e349d-152">Use a comma "," as hello separator character (you can open a service request toorequest toochange hello .csv separator character from a comma "," tooanother character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="e349d-153">Gebruik voor Boole-waarden alle kleine letters 'true' en 'false'.</span><span class="sxs-lookup"><span data-stu-id="e349d-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="e349d-154">Gebruik een bestand dat kleiner is dan de maximale bestandsgrootte Hallo van 35MB.</span><span class="sxs-lookup"><span data-stu-id="e349d-154">Use a file that is smaller than hello maximum file size of 35MB.</span></span>

