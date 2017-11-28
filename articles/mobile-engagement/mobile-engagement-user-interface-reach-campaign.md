---
title: aaaAzure gebruikersinterface van de Mobile Engagement - Reach-campagne
description: Laern hoe toocreate en beheren met behulp van Azure Mobile Engagement campagnes met pushmeldingen
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a><span data-ttu-id="24c46-103">Hoe toocreate en beheren van campagnes met pushmeldingen</span><span class="sxs-lookup"><span data-stu-id="24c46-103">How toocreate and manage push notification campaigns</span></span>
<span data-ttu-id="24c46-104">Hallo Reach-sectie van Hallo UI toocreate een nieuwe pushcampagne kunt u met een complexe formule door te geven van alle benodigde toosend een push-melding Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="24c46-104">You can use hello Reach section of hello UI toocreate a new Push campaign with a complex formula by providing all hello information you need toosend a push notification.</span></span> <span data-ttu-id="24c46-105">Hallo opties van een pushcampagne enigszins afwijken, afhankelijk van Hallo vier campagne soorten: aankondigingen, Polls, gegevens-Pushes en tegels (alleen Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="24c46-105">hello options of a Push campaign vary slightly depending on hello four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="24c46-106">Is van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="24c46-106">Option Applies to:</span></span>
* <span data-ttu-id="24c46-107">Talen: Alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="24c46-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="24c46-108">Campagne: Alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="24c46-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="24c46-109">Melding: Aankondigingen, Polls</span><span class="sxs-lookup"><span data-stu-id="24c46-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="24c46-110">Inhoud: Uniek zijn voor elk campagnetype</span><span class="sxs-lookup"><span data-stu-id="24c46-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="24c46-111">Doelgroep: Alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="24c46-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="24c46-112">Tijdsbestek: aankondigingen, Polls, tegels</span><span class="sxs-lookup"><span data-stu-id="24c46-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="24c46-113">Test: Alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="24c46-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Reach-Campaign1][20]

## <a name="languages"></a><span data-ttu-id="24c46-115">Talen</span><span class="sxs-lookup"><span data-stu-id="24c46-115">Languages</span></span>
<span data-ttu-id="24c46-116">U kunt Hallo talen vervolgkeuzelijst menu toosend een andere versie van de Push-toodevices die zijn ingesteld in verschillende talen toouse gebruiken.</span><span class="sxs-lookup"><span data-stu-id="24c46-116">You can use hello Languages drop-down menu toosend a different version of your Push toodevices that are set toouse different languages.</span></span> <span data-ttu-id="24c46-117">Alle apparaten ontvangen standaard Hallo dezelfde Push ongeacht welke taal zijn ze toouse ingesteld.</span><span class="sxs-lookup"><span data-stu-id="24c46-117">By default, all devices will receive hello same Push regardless of what language they are set toouse.</span></span> <span data-ttu-id="24c46-118">Hallo standaard taalversie van Hallo Push ontvangen gebruikers met hun apparaat set tooa andere taal.</span><span class="sxs-lookup"><span data-stu-id="24c46-118">Users with their device set tooa different language will receive hello Default Language version of hello Push.</span></span> <span data-ttu-id="24c46-119">Veel van Hallo push campagne opties kunnen u alternatieve toospecify-inhoud voor elke Hallo extra talen die u selecteert.</span><span class="sxs-lookup"><span data-stu-id="24c46-119">Many of hello push campaign options allow you toospecify alternate content for each of hello additional languages you select.</span></span> 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="24c46-121">Taalverschillen van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="24c46-121">Language differences apply to:</span></span>
* <span data-ttu-id="24c46-122">Talen: Unieke talen worden geselecteerd in de standaardtaal voor toevoeging toohello</span><span class="sxs-lookup"><span data-stu-id="24c46-122">Languages:    Unique languages may be selected in addition toohello default language</span></span>
* <span data-ttu-id="24c46-123">Campagne: Gelijk voor alle talen</span><span class="sxs-lookup"><span data-stu-id="24c46-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="24c46-124">Melding: Uniek voor elke taal bovendien toohello standaardtaal</span><span class="sxs-lookup"><span data-stu-id="24c46-124">Notification:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="24c46-125">Inhoud: Uniek voor elke taal bovendien toohello standaardtaal</span><span class="sxs-lookup"><span data-stu-id="24c46-125">Content:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="24c46-126">Doelgroep: Kan worden gefilterd door het criterium van een afzonderlijke taal</span><span class="sxs-lookup"><span data-stu-id="24c46-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="24c46-127">Tijdsbestek: hetzelfde voor alle talen</span><span class="sxs-lookup"><span data-stu-id="24c46-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="24c46-128">Test: Kunnen tooeach taal worden verzonden op een tijdstip</span><span class="sxs-lookup"><span data-stu-id="24c46-128">Test:    May be sent tooeach language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="24c46-129">Ondersteunde talen:</span><span class="sxs-lookup"><span data-stu-id="24c46-129">Supported Languages:</span></span>
* <span data-ttu-id="24c46-130">Arabisch (ar)</span><span class="sxs-lookup"><span data-stu-id="24c46-130">Arabic (ar)</span></span> 
* <span data-ttu-id="24c46-131">Bulgaars (bg)</span><span class="sxs-lookup"><span data-stu-id="24c46-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="24c46-132">Catalaans (ca)</span><span class="sxs-lookup"><span data-stu-id="24c46-132">Catalan (ca)</span></span> 
* <span data-ttu-id="24c46-133">Chinees (zh)</span><span class="sxs-lookup"><span data-stu-id="24c46-133">Chinese (zh)</span></span> 
* <span data-ttu-id="24c46-134">Kroatisch (uur)</span><span class="sxs-lookup"><span data-stu-id="24c46-134">Croatian (hr)</span></span> 
* <span data-ttu-id="24c46-135">Czech (CS)</span><span class="sxs-lookup"><span data-stu-id="24c46-135">Czech (cs)</span></span> 
* <span data-ttu-id="24c46-136">Deens (da)</span><span class="sxs-lookup"><span data-stu-id="24c46-136">Danish (da)</span></span> 
* <span data-ttu-id="24c46-137">Nederlands (nl)</span><span class="sxs-lookup"><span data-stu-id="24c46-137">Dutch (nl)</span></span> 
* <span data-ttu-id="24c46-138">Engels (en)</span><span class="sxs-lookup"><span data-stu-id="24c46-138">English (en)</span></span> 
* <span data-ttu-id="24c46-139">Fins (fi)</span><span class="sxs-lookup"><span data-stu-id="24c46-139">Finnish (fi)</span></span> 
* <span data-ttu-id="24c46-140">Frans (fr)</span><span class="sxs-lookup"><span data-stu-id="24c46-140">French (fr)</span></span> 
* <span data-ttu-id="24c46-141">Duits (de)</span><span class="sxs-lookup"><span data-stu-id="24c46-141">German (de)</span></span> 
* <span data-ttu-id="24c46-142">Grieks (el)</span><span class="sxs-lookup"><span data-stu-id="24c46-142">Greek (el)</span></span> 
* <span data-ttu-id="24c46-143">Hebreeuwse (hij)</span><span class="sxs-lookup"><span data-stu-id="24c46-143">Hebrew (he)</span></span> 
* <span data-ttu-id="24c46-144">Hindi (hoog)</span><span class="sxs-lookup"><span data-stu-id="24c46-144">Hindi (hi)</span></span> 
* <span data-ttu-id="24c46-145">Hongaars (hu)</span><span class="sxs-lookup"><span data-stu-id="24c46-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="24c46-146">Indonesisch (id)</span><span class="sxs-lookup"><span data-stu-id="24c46-146">Indonesian (id)</span></span> 
* <span data-ttu-id="24c46-147">Italiaans (it)</span><span class="sxs-lookup"><span data-stu-id="24c46-147">Italian (it)</span></span> 
* <span data-ttu-id="24c46-148">Japans (ja)</span><span class="sxs-lookup"><span data-stu-id="24c46-148">Japanese (ja)</span></span> 
* <span data-ttu-id="24c46-149">Koreaans (ko)</span><span class="sxs-lookup"><span data-stu-id="24c46-149">Korean (ko)</span></span> 
* <span data-ttu-id="24c46-150">Lets (lv)</span><span class="sxs-lookup"><span data-stu-id="24c46-150">Latvian (lv)</span></span> 
* <span data-ttu-id="24c46-151">Litouws (lt)</span><span class="sxs-lookup"><span data-stu-id="24c46-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="24c46-152">Maleis (macrolanguage) (ms)</span><span class="sxs-lookup"><span data-stu-id="24c46-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="24c46-153">Noors, Bokmål (nb)</span><span class="sxs-lookup"><span data-stu-id="24c46-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="24c46-154">Pools (pl)</span><span class="sxs-lookup"><span data-stu-id="24c46-154">Polish (pl)</span></span> 
* <span data-ttu-id="24c46-155">Portugees (pt)</span><span class="sxs-lookup"><span data-stu-id="24c46-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="24c46-156">Roemeens (ro)</span><span class="sxs-lookup"><span data-stu-id="24c46-156">Romanian (ro)</span></span> 
* <span data-ttu-id="24c46-157">Russisch (ru)</span><span class="sxs-lookup"><span data-stu-id="24c46-157">Russian (ru)</span></span> 
* <span data-ttu-id="24c46-158">Servisch (sr)</span><span class="sxs-lookup"><span data-stu-id="24c46-158">Serbian (sr)</span></span> 
* <span data-ttu-id="24c46-159">Slowaaks (sk)</span><span class="sxs-lookup"><span data-stu-id="24c46-159">Slovak (sk)</span></span> 
* <span data-ttu-id="24c46-160">Sloveens (sl)</span><span class="sxs-lookup"><span data-stu-id="24c46-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="24c46-161">Spaans (es)</span><span class="sxs-lookup"><span data-stu-id="24c46-161">Spanish (es)</span></span> 
* <span data-ttu-id="24c46-162">Zweeds (sv)</span><span class="sxs-lookup"><span data-stu-id="24c46-162">Swedish (sv)</span></span> 
* <span data-ttu-id="24c46-163">Tagalog (tl)</span><span class="sxs-lookup"><span data-stu-id="24c46-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="24c46-164">Thais (e)</span><span class="sxs-lookup"><span data-stu-id="24c46-164">Thai (th)</span></span> 
* <span data-ttu-id="24c46-165">Turks (tr)</span><span class="sxs-lookup"><span data-stu-id="24c46-165">Turkish (tr)</span></span> 
* <span data-ttu-id="24c46-166">Oekraïens (GB)</span><span class="sxs-lookup"><span data-stu-id="24c46-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="24c46-167">Vietnamees (vi)</span><span class="sxs-lookup"><span data-stu-id="24c46-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="24c46-168">Campagne</span><span class="sxs-lookup"><span data-stu-id="24c46-168">Campaign</span></span>
<span data-ttu-id="24c46-169">U kunt gebruiken Hallo campagne tooset Hallo sectienaam en categorie van uw campagne ook als tooignore Hallo doelgroep sectie van een pushcampagne te plannen en verzenden van deze campagne via Hallo Reach API (en een aantal elementen met geringe Hallo Push-API) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="24c46-169">You can use hello Campaign section tooset hello name and category of your campaign as well as if you plan tooignore hello audience section of a Push campaign and send this campaign via hello Reach API (and some elements with hello low level Push API) instead.</span></span> <span data-ttu-id="24c46-170">Categorieën kunnen worden gebruikt met een aangepaste melding sjabloon toocontrol in-app-meldingen op basis van vooraf gedefinieerde instellingen.</span><span class="sxs-lookup"><span data-stu-id="24c46-170">Categories can be used with a custom notification template toocontrol in-app notifications based on predefined settings.</span></span> <span data-ttu-id="24c46-171">U kunt een lijst met uw bestaande 'categorieën' via Hallo Reach API ophalen.</span><span class="sxs-lookup"><span data-stu-id="24c46-171">You can get a list of your existing “Categories” via hello Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="24c46-172">Als u 'Doelgroep negeren, push wordt verzonden toousers via API Hallo' Hallo-optie gebruikt in 'Campagne' Hallo-sectie van een Reach-campagne Hallo campagne wordt niet automatisch verzenden, moet u toosend handmatig via Hallo Reach API.</span><span class="sxs-lookup"><span data-stu-id="24c46-172">If you use hello "Ignore Audience, push will be sent toousers via hello API" option in hello "Campaign" section of a Reach campaign, hello campaign will NOT automatically send, you will need toosend it manually via hello Reach API.</span></span>

![Reach-Campaign3][22]

### <a name="option-applies-to"></a><span data-ttu-id="24c46-174">Is van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="24c46-174">Option Applies to:</span></span>
* <span data-ttu-id="24c46-175">Naam: alle</span><span class="sxs-lookup"><span data-stu-id="24c46-175">Name:    All</span></span>
* <span data-ttu-id="24c46-176">Categorie: Aankondigingen, Polls</span><span class="sxs-lookup"><span data-stu-id="24c46-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="24c46-177">Doelgroep negeren, push toousers via Hallo API worden verzonden: alle</span><span class="sxs-lookup"><span data-stu-id="24c46-177">Ignore Audience, push will be sent toousers via hello API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="24c46-178">Melding</span><span class="sxs-lookup"><span data-stu-id="24c46-178">Notification</span></span>
<span data-ttu-id="24c46-179">U kunt Hallo melding sectie tooset basisinstellingen voor het opnemen van uw push: Hallo titel Hallo-Push, het Hallo-bericht, de installatiekopie van een in-app of als deze worden weggeklikt.</span><span class="sxs-lookup"><span data-stu-id="24c46-179">You can use hello Notification section tooset basic settings for your push including: hello title of hello Push, hello message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="24c46-180">Veel meldingsinstellingen zijn platform-specifieke toohello van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="24c46-180">Many notification settings are specific toohello platform of your device.</span></span> <span data-ttu-id="24c46-181">U kunt aangeven of uw push 'in-app' of 'out of app' worden verzonden of beide.</span><span class="sxs-lookup"><span data-stu-id="24c46-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="24c46-182">(Houd er rekening mee dat gebruikers kunnen 'opt-in' of 'opt-out' van 'buiten app' Pushes op Hallo besturingssysteem niveau op hun apparaten en Azure Mobile Engagement niet wordt kunnen toooverride worden deze instelling.</span><span class="sxs-lookup"><span data-stu-id="24c46-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at hello Operating System level on their devices, and Azure Mobile Engagement will not be able toooverride this setting.</span></span> <span data-ttu-id="24c46-183">Denk eraan dat Hallo Reach API 'in-app verwerkt' en 'out van app' duwt.</span><span class="sxs-lookup"><span data-stu-id="24c46-183">Also remember that hello Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="24c46-184">Hallo Push API kan gebruikte toohandle 'buiten app' pushes te zijn.) Pushes kunnen worden aangepast met afbeeldingen of HTML-inhoud, inclusief dieptekoppelingen voor het koppelen van buiten uw App of tooanother locatie in uw App (Android SDK 2.1.0 of hoger opzet categorieën vereist).</span><span class="sxs-lookup"><span data-stu-id="24c46-184">hello Push API can be used toohandle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or tooanother location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="24c46-185">U kunt wijzigen Hallo-pictogram of iOS-badge en -tekst of web-inhoud (een pop-up met HTML-inhoud, URL koppeling tooanother locatie binnen of buiten de app Hallo) kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="24c46-185">You can change hello icon or iOS badge, and send either text or web content (a popup with html content, URL link tooanother location either inside or outside of hello app).</span></span> <span data-ttu-id="24c46-186">U kunt ook Android-apparaten beltoon laten horen of Trillen Hello Push.</span><span class="sxs-lookup"><span data-stu-id="24c46-186">You can also make Android devices ring or vibrate with hello Push.</span></span> <span data-ttu-id="24c46-187">(Vergeet niet dat u juist SDK machtigingen in uw Android manifest tooring bestand of een apparaat laten Trillen Hallo wordt nodig.) Er is momenteel geen bedrijfstak standaard voor Android 'grote afbeelding' grootten, aangezien schermgrootte verschillen op elk apparaat maar 400 x 100 afbeeldingen op bijna elke schermgrootte werken.</span><span class="sxs-lookup"><span data-stu-id="24c46-187">(Remember that you will need hello correct SDK permissions in your Android manifest file tooring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="24c46-188">Levering typen:</span><span class="sxs-lookup"><span data-stu-id="24c46-188">Delivery Types:</span></span>
* <span data-ttu-id="24c46-189">Alleen buiten app: Hallo-melding worden geleverd wanneer gebruiker Hallo Hallo toepassing niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="24c46-189">Out of app only: hello notification will be delivered when hello user does not use hello application.</span></span>
* <span data-ttu-id="24c46-190">Hallo buiten alleen appmelding vereist een certificaat van Apple of Google (APNS of GCM-certificaat).</span><span class="sxs-lookup"><span data-stu-id="24c46-190">hello out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="24c46-191">In-app alleen: Hallo melding wordt weergegeven wanneer er op Hallo-toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="24c46-191">In-app only: hello notification appears only when hello application is running.</span></span>
* <span data-ttu-id="24c46-192">Hallo melding Hallo Capptain levering tooreach Hallo systeemgebruiker gebruikt.</span><span class="sxs-lookup"><span data-stu-id="24c46-192">hello notification uses hello Capptain delivery system tooreach hello user.</span></span> <span data-ttu-id="24c46-193">U kunt volledig Hallo visuele lay-out/weergave van uw push aanpassen.</span><span class="sxs-lookup"><span data-stu-id="24c46-193">You can fully customize hello visual layout/display of your push.</span></span>
* <span data-ttu-id="24c46-194">Op elk gewenst moment: Deze optie zorgt ervoor dat u een melding dat de toepassing hello wordt uitgevoerd of niet verzenden.</span><span class="sxs-lookup"><span data-stu-id="24c46-194">Anytime: This option ensures that you send a notification either hello application is running or not.</span></span>

![Reach-Campaign4][23]

### <a name="option-applies-to"></a><span data-ttu-id="24c46-196">Is van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="24c46-196">Option Applies to:</span></span>
* <span data-ttu-id="24c46-197">Melding: Aankondigingen, Polls</span><span class="sxs-lookup"><span data-stu-id="24c46-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="24c46-198">Inhoud</span><span class="sxs-lookup"><span data-stu-id="24c46-198">Content</span></span>
<span data-ttu-id="24c46-199">U kunt Hallo sectie inhoud toomodify Hallo inhoud van uw aankondigingen, Polls, gegevens-Pushes en tegels (alleen Windows Phone) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="24c46-199">You can use hello Content section toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="24c46-200">Hallo is inhoud deze instelling van pushcampagnes specifieke toohello type campagne.</span><span class="sxs-lookup"><span data-stu-id="24c46-200">hello Content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="24c46-201">Zie ook</span><span class="sxs-lookup"><span data-stu-id="24c46-201">See also</span></span>
* <span data-ttu-id="24c46-202">[UI-documentatie - bereiken - Push-inhoud][Link 29]</span><span class="sxs-lookup"><span data-stu-id="24c46-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Reach-Campaign5][24]

## <a name="audience"></a><span data-ttu-id="24c46-204">Doelgroep</span><span class="sxs-lookup"><span data-stu-id="24c46-204">Audience</span></span>
<span data-ttu-id="24c46-205">U kunt Hallo doelgroep sectie toodefine een standaard lijst met items toolimit uw campagne of limieten uw campagne op basis van aangepaste criteria.</span><span class="sxs-lookup"><span data-stu-id="24c46-205">You can use hello Audience section toodefine a standard list of items toolimit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="24c46-206">Hallo standaardset opties tooLimit uw doelgroep kunt u toopush tooeither nieuwe of oude gebruikers of alleen voor gebruikers van native pushberichten.</span><span class="sxs-lookup"><span data-stu-id="24c46-206">hello standard set of options tooLimit your Audience allows you toopush tooeither new or old users or native push users only.</span></span> <span data-ttu-id="24c46-207">U kunt ook een quotum toolimit Hallo aantal gebruikers die Hallo push ontvangen instellen.</span><span class="sxs-lookup"><span data-stu-id="24c46-207">You can also set a quota toolimit hello number of users who receive hello push.</span></span> <span data-ttu-id="24c46-208">U kunt handmatig bewerken Hallo-expressie voor hoe uw campagne gefilterde tooinclude is een of meer criterium tootarget gebruikers.</span><span class="sxs-lookup"><span data-stu-id="24c46-208">You can manually Edit hello expression for how your campaign is filtered tooinclude one or more criterion tootarget users.</span></span> <span data-ttu-id="24c46-209">U kunt handmatig een doelgroepexpressie typen.</span><span class="sxs-lookup"><span data-stu-id="24c46-209">You can manually type an audience expression.</span></span> <span data-ttu-id="24c46-210">Een dergelijke expressie moet expliciet Hallo relatie tussen criteria definiëren.</span><span class="sxs-lookup"><span data-stu-id="24c46-210">Such an expression must explicitly define hello relation between criteria.</span></span> <span data-ttu-id="24c46-211">Een criterium is beschreven door een id die met een hoofdletter moet beginnen en mag geen spaties bevatten.</span><span class="sxs-lookup"><span data-stu-id="24c46-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="24c46-212">relatie tussen criteria Hallo Hallo kan worden beschreven met behulp van 'en', 'of', 'not' operators, evenals '(',')'.</span><span class="sxs-lookup"><span data-stu-id="24c46-212">hello relation between hello criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="24c46-213">Voorbeeld: 'Criterion1 of (Criterion1 en niet Criterion2)'.</span><span class="sxs-lookup"><span data-stu-id="24c46-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="24c46-214">Met een grote doelgroep opgenomen in de campagnes, Hallo serverzijde die gericht is op scan kan traag zijn, met name als u probeert toostart Hallo meerdere campagnes op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="24c46-214">With a large audience included in campaigns, hello server side targeting scan can be slow, especially if you attempt toostart multiple campaigns at hello same time.</span></span>

* <span data-ttu-id="24c46-215">Alleen indien mogelijk een campagne start tegelijk.</span><span class="sxs-lookup"><span data-stu-id="24c46-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="24c46-216">Hallo maximaal vier campagnes alleen start op een tijdstip op.</span><span class="sxs-lookup"><span data-stu-id="24c46-216">At hello most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="24c46-217">Alleen actieve gebruikers met tooyour push (selectievakje ' alleen gebruikers benaderen die kunnen worden bereikt met behulp van Native Pushberichten' en 'Alleen actieve gebruikers benaderen') zodat alleen gebruikers die nog steeds Hallo-app hebt geïnstalleerd en deze gebruiken toobe gescand moet.</span><span class="sxs-lookup"><span data-stu-id="24c46-217">Push only tooyour active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have hello app installed and use it will need toobe scanned.</span></span>
  <span data-ttu-id="24c46-218">Als uw doelgroep is gedefinieerd, kunt u Hallo knop toofind uit hoeveel gebruikers deze Push ontvangt simuleren.</span><span class="sxs-lookup"><span data-stu-id="24c46-218">Once your audience is defined, you can use hello simulate button toofind out how many users will receive this Push.</span></span> <span data-ttu-id="24c46-219">Dit wilt aantal bekende gebruikers mogelijk doel voor deze doelgroep (dit is een schatting op basis van een steekproef van gebruikers) Hallo berekenen.</span><span class="sxs-lookup"><span data-stu-id="24c46-219">This will compute hello number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="24c46-220">Vergeet niet dat gebruikers die u hebt verwijderd van de toepassing hello eveneens deel van deze doelgroep uitmaken, maar kunnen niet worden bereikt.</span><span class="sxs-lookup"><span data-stu-id="24c46-220">Be aware that users who have uninstalled hello application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="24c46-221">Zie ook</span><span class="sxs-lookup"><span data-stu-id="24c46-221">See also</span></span>
* <span data-ttu-id="24c46-222">[UI - Reach - documentatie nieuw Push criterium][Link 28]</span><span class="sxs-lookup"><span data-stu-id="24c46-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Reach-Campaign6][25]

### <a name="edit-expression"></a><span data-ttu-id="24c46-224">Expressie bewerken</span><span class="sxs-lookup"><span data-stu-id="24c46-224">Edit expression</span></span>
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="24c46-226">Limiet voor die uw doelgroep is van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="24c46-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="24c46-227">Alleen een subset van gebruikers benaderen: alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="24c46-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="24c46-228">Alleen oude gebruikers benaderen: alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="24c46-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="24c46-229">Alleen nieuwe gebruikers benaderen: alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="24c46-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="24c46-230">Alleen niet-actieve gebruikers benaderen: aankondigingen, Polls, tegels</span><span class="sxs-lookup"><span data-stu-id="24c46-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="24c46-231">Alleen actieve gebruikers benaderen: alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="24c46-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="24c46-232">Alleen gebruikers benaderen die kunnen worden bereikt via een Native Pushbericht: aankondigingen, Polls</span><span class="sxs-lookup"><span data-stu-id="24c46-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="24c46-233">Tijdsbestek</span><span class="sxs-lookup"><span data-stu-id="24c46-233">Time Frame</span></span>
<span data-ttu-id="24c46-234">U kunt Hallo tijdsbestek sectie tooset Hallo push wordt verzonden of u kunt Hallo tijdsbestek leeg toostart Hallo campagne onmiddellijk laten.</span><span class="sxs-lookup"><span data-stu-id="24c46-234">You can use hello Time Frame section tooset when hello push will be sent or you can leave hello time frame blank toostart hello campaign immediately.</span></span> <span data-ttu-id="24c46-235">Houd er rekening mee dat met behulp van de tijdzone Hallo eindgebruikers mogelijk Hallo campagne start een dag eerder dan u voor uw eindgebruikers in Azië verwacht en klein batches van pushes tegelijkertijd totdat alle tijdzones in hello world overeen Hallo-periode is ingesteld voor uw campagne te verzenden.</span><span class="sxs-lookup"><span data-stu-id="24c46-235">Remember that using hello end-users' time zone may start hello campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in hello world match hello time frame set for your campaign.</span></span> <span data-ttu-id="24c46-236">Met behulp van de tijdzone Hallo eindgebruikers kan ook vertragingen veroorzaken bij campagnes omdat het toorequest Hallo actief zijn op Hallo telefoon voordat Hallo push heeft.</span><span class="sxs-lookup"><span data-stu-id="24c46-236">Using hello end users' time zone can also cause delays in campaigns since it has toorequest hello time from hello phone before starting hello push.</span></span>

> [!NOTE]
> <span data-ttu-id="24c46-237">Zonder een einddatum in cache campagnes pushes lokaal en nog steeds weergegeven nadat u handmatig voltooid campagnes.</span><span class="sxs-lookup"><span data-stu-id="24c46-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="24c46-238">tooavoid dit gedrag, de specifieke eindtijd voor campagnes.</span><span class="sxs-lookup"><span data-stu-id="24c46-238">tooavoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="24c46-239">Zie ook</span><span class="sxs-lookup"><span data-stu-id="24c46-239">See also</span></span>
* <span data-ttu-id="24c46-240">[Bereiken - hoe Tos – plannen][Link 3]</span><span class="sxs-lookup"><span data-stu-id="24c46-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="24c46-242">Instellingen van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="24c46-242">Settings Apply to:</span></span>
* <span data-ttu-id="24c46-243">Tijdsbestek: aankondigingen, Polls, tegels</span><span class="sxs-lookup"><span data-stu-id="24c46-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="24c46-244">Test</span><span class="sxs-lookup"><span data-stu-id="24c46-244">Test</span></span>
<span data-ttu-id="24c46-245">Kunt u Hallo Test sectie toosend dit apparaat push tooyour eigen test voordat u opslaat Hallo campagne.</span><span class="sxs-lookup"><span data-stu-id="24c46-245">You can use hello Test section toosend this push tooyour own test device before saving hello campaign.</span></span> <span data-ttu-id="24c46-246">Als u de aangepaste talen voor deze campagne hebt geconfigureerd, kunt u Hallo push testen in elke taal.</span><span class="sxs-lookup"><span data-stu-id="24c46-246">If you have configured any custom languages for this campaign, you can test hello push in each language.</span></span> <span data-ttu-id="24c46-247">U kunt een testapparaat van 'Mijn Account' instellen.</span><span class="sxs-lookup"><span data-stu-id="24c46-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="24c46-248">Er zijn geen gegevens worden geregistreerd wanneer u de knop Hallo serverzijde te 'test' pushes, gegevens alleen worden geregistreerd voor echte pushcampagnes.</span><span class="sxs-lookup"><span data-stu-id="24c46-248">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="24c46-249">Zie ook</span><span class="sxs-lookup"><span data-stu-id="24c46-249">See also</span></span>
* <span data-ttu-id="24c46-250">[UI-documentatie - Mijn Account][Link 14]</span><span class="sxs-lookup"><span data-stu-id="24c46-250">[UI Documentation - My Account][Link 14]</span></span>

![Reach-Campaign9][28]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

