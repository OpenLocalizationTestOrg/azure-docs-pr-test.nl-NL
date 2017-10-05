---
title: Azure Mobile Engagement Troubleshooting Guide - Service
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
ms.openlocfilehash: f13fd0540b783120014b3a8d4e41f78808c7fade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="ab32a-103">Gids voor probleemoplossing voor problemen met de Service</span><span class="sxs-lookup"><span data-stu-id="ab32a-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="ab32a-104">Hieronder vindt u mogelijke problemen die optreden bij hoe Azure Mobile Engagement wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ab32a-104">The following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="ab32a-105">Serviceonderbrekingen</span><span class="sxs-lookup"><span data-stu-id="ab32a-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="ab32a-106">Probleem</span><span class="sxs-lookup"><span data-stu-id="ab32a-106">Issue</span></span>
* <span data-ttu-id="ab32a-107">Problemen die worden veroorzaakt door Azure Mobile Engagement serviceonderbrekingen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ab32a-107">Issues that appear to be caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="ab32a-108">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="ab32a-108">Causes</span></span>
* <span data-ttu-id="ab32a-109">Problemen die worden veroorzaakt door Azure Mobile Engagement serviceonderbrekingen lijken kunnen zijn veroorzaakt door verschillende andere problemen:</span><span class="sxs-lookup"><span data-stu-id="ab32a-109">Issues that appear to be caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="ab32a-110">Geïsoleerde problemen die oorspronkelijk al aan alle Azure Mobile Engagement weergegeven</span><span class="sxs-lookup"><span data-stu-id="ab32a-110">Isolated issues that originally appear systemic to all of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="ab32a-111">Bekende problemen veroorzaakt door serverstoringen (die niet altijd wordt weergegeven in de serverstatus):</span><span class="sxs-lookup"><span data-stu-id="ab32a-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="ab32a-112">Voor de planning vertragingen, fouten Targeting, problemen Badge-update, statistieken stop verzamelen, werkt niet voor Push kan niet-API's meer werken, nieuwe apps of gebruikers worden gemaakt, DNS-fouten en time-outfouten in de gebruikersinterface, API of Apps op een apparaat.</span><span class="sxs-lookup"><span data-stu-id="ab32a-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in the UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="ab32a-113">Afhankelijkheid uitval cloud [Azure servicestatus](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="ab32a-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="ab32a-114">Push Notification Services (PNS) afhankelijkheid uitval</span><span class="sxs-lookup"><span data-stu-id="ab32a-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="ab32a-115">App Store uitval</span><span class="sxs-lookup"><span data-stu-id="ab32a-115">App Store Outages</span></span>

1) <span data-ttu-id="ab32a-116">Als u wilt testen om te zien als het probleem al is kunt u dezelfde functie uit een andere testen</span><span class="sxs-lookup"><span data-stu-id="ab32a-116">To test to see if the problem is systemic you can test the same function from a different</span></span>

* <span data-ttu-id="ab32a-117">Azure Mobile Engagement geïntegreerde toepassing</span><span class="sxs-lookup"><span data-stu-id="ab32a-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="ab32a-118">Testapparaat</span><span class="sxs-lookup"><span data-stu-id="ab32a-118">Test device</span></span>
* <span data-ttu-id="ab32a-119">Testversie van het besturingssysteem van het apparaat</span><span class="sxs-lookup"><span data-stu-id="ab32a-119">Test device OS version</span></span>
* <span data-ttu-id="ab32a-120">Campagne</span><span class="sxs-lookup"><span data-stu-id="ab32a-120">Campaign</span></span>
* <span data-ttu-id="ab32a-121">Beheerdersaccount</span><span class="sxs-lookup"><span data-stu-id="ab32a-121">Administrator user account</span></span>
* <span data-ttu-id="ab32a-122">Browser (IE, Firefox, Chrome, enz.)</span><span class="sxs-lookup"><span data-stu-id="ab32a-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="ab32a-123">Computer</span><span class="sxs-lookup"><span data-stu-id="ab32a-123">Computer</span></span>

2) <span data-ttu-id="ab32a-124">Als het probleem alleen betrekking heeft op de gebruikersinterface of de API testen:</span><span class="sxs-lookup"><span data-stu-id="ab32a-124">To test if the problem only affects the UI or the API's:</span></span>

* <span data-ttu-id="ab32a-125">Dezelfde functie uit de Azure Mobile Engagement-gebruikersinterface en de Azure Mobile Engagement API testen.</span><span class="sxs-lookup"><span data-stu-id="ab32a-125">Test the same function from both the Azure Mobile Engagement UI and the Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="ab32a-126">Als het probleem met uw mobiele telefoonnetwerk is testen:</span><span class="sxs-lookup"><span data-stu-id="ab32a-126">To test if the problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="ab32a-127">Test tijdens verbinding met Internet via Wi-Fi en via uw mobiele telefoon 3G netwerk is verbonden.</span><span class="sxs-lookup"><span data-stu-id="ab32a-127">Test while connected to the Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="ab32a-128">Bevestig dat uw firewall niet worden geblokkeerd van de Azure Mobile Engagement IP-adressen of -poorten.</span><span class="sxs-lookup"><span data-stu-id="ab32a-128">Confirm that your firewall is not blocking any of the Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="ab32a-129">Als het probleem met uw apparaat is testen:</span><span class="sxs-lookup"><span data-stu-id="ab32a-129">To test if the problem is with your Device:</span></span>

* <span data-ttu-id="ab32a-130">Als het apparaat verbinding kunnen maken met Azure Mobile Engagement met een andere geïntegreerde Azure Mobile Engagement-app testen.</span><span class="sxs-lookup"><span data-stu-id="ab32a-130">Test if your Device is able to connect to Azure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="ab32a-131">Test die u kunt gebeurtenissen, taken en Crashes van uw telefoon die kan worden weergegeven in de gebruikersinterface van Azure Mobile Engagement genereren.</span><span class="sxs-lookup"><span data-stu-id="ab32a-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in the Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="ab32a-132">Testen of u pushmeldingen verzenden vanuit de Azure Mobile Engagement-gebruikersinterface op uw apparaat op basis van de apparaat-ID kunt.</span><span class="sxs-lookup"><span data-stu-id="ab32a-132">Test if you can send push notifications from the Azure Mobile Engagement UI to your device based on its Device ID.</span></span> 

5) <span data-ttu-id="ab32a-133">Als het probleem met uw App is testen:</span><span class="sxs-lookup"><span data-stu-id="ab32a-133">To test if the problem is with your App:</span></span>

* <span data-ttu-id="ab32a-134">Installeren en testen van de toepassing van een emulator in plaats van vanaf een fysiek apparaat:</span><span class="sxs-lookup"><span data-stu-id="ab32a-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="ab32a-135">Om te controleren of het probleem is met upgrades voor het besturingssysteem voor de eindgebruiker apparaten waarvoor een upgrade van de SDK om op te lossen:</span><span class="sxs-lookup"><span data-stu-id="ab32a-135">To test if the problem is with OS upgrades to end user Devices, which require an SDK upgrade to resolve:</span></span>

* <span data-ttu-id="ab32a-136">Test uw toepassing op verschillende apparaten met verschillende versies van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="ab32a-136">Test your application on different devices with different versions of the OS.</span></span>
* <span data-ttu-id="ab32a-137">Controleer of u van de meest recente versie van de SDK gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="ab32a-137">Confirm that you are using the most recent version of the SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="ab32a-138">Connectiviteit en onjuiste informatie over problemen</span><span class="sxs-lookup"><span data-stu-id="ab32a-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="ab32a-139">Probleem</span><span class="sxs-lookup"><span data-stu-id="ab32a-139">Issue</span></span>
* <span data-ttu-id="ab32a-140">Problemen bij het aanmelden bij de Azure Mobile Engagement-gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="ab32a-140">Problems logging into the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="ab32a-141">Verbindingsfouten met de Azure Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="ab32a-141">Connection errors with the Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="ab32a-142">Problemen met het uploaden van App-Info labels via de apparaat-API.</span><span class="sxs-lookup"><span data-stu-id="ab32a-142">Problems uploading App Info Tags via the Device API.</span></span>
* <span data-ttu-id="ab32a-143">Problemen bij het downloaden van Logboeken of de geëxporteerde gegevens van Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="ab32a-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="ab32a-144">Onjuiste informatie weergegeven in de gebruikersinterface van Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="ab32a-144">Incorrect information shown in the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="ab32a-145">Onjuiste informatie die wordt weergegeven in Azure Mobile Engagement-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="ab32a-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="ab32a-146">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="ab32a-146">Causes</span></span>
* <span data-ttu-id="ab32a-147">Bevestig dat uw gebruikersaccount heeft onvoldoende machtigingen om uit te voeren van de taak.</span><span class="sxs-lookup"><span data-stu-id="ab32a-147">Confirm your user account has sufficient permissions to perform the task.</span></span>
* <span data-ttu-id="ab32a-148">Bevestig dat het probleem niet geïsoleerd, zodat één computer of uw lokale netwerk is.</span><span class="sxs-lookup"><span data-stu-id="ab32a-148">Confirm that the problem is not isolated to one computer or your local network.</span></span>
* <span data-ttu-id="ab32a-149">Controleer of het uitval moet worden gemeld dat de service Azure Mobile Engagement geen heeft.</span><span class="sxs-lookup"><span data-stu-id="ab32a-149">Confirm that that the Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="ab32a-150">Bevestig dat uw App-Info label bestanden al deze regels volgen:</span><span class="sxs-lookup"><span data-stu-id="ab32a-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="ab32a-151">Gebruik alleen de UTF8-tekenset (de ANSI-tekenset wordt niet ondersteund).</span><span class="sxs-lookup"><span data-stu-id="ab32a-151">Use only the UTF8 character set (the ANSI character set is not supported).</span></span>
  * <span data-ttu-id="ab32a-152">Gebruik een komma "," als scheidingsteken (u kunt een service om aan te vragen het CSV-scheidingsteken wijzigen vanaf een door komma's openen "," naar een ander teken, zoals een puntkomma ';').</span><span class="sxs-lookup"><span data-stu-id="ab32a-152">Use a comma "," as the separator character (you can open a service request to request to change the .csv separator character from a comma "," to another character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="ab32a-153">Gebruik voor Boole-waarden alle kleine letters 'true' en 'false'.</span><span class="sxs-lookup"><span data-stu-id="ab32a-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="ab32a-154">Gebruik een bestand dat kleiner is dan de maximale bestandsgrootte van 35MB.</span><span class="sxs-lookup"><span data-stu-id="ab32a-154">Use a file that is smaller than the maximum file size of 35MB.</span></span>

