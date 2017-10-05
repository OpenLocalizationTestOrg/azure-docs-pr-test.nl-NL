---
title: Azure Mobile Engagement-gebruikersinterface - Reach-campagne
description: Laern hoe campagnes maken en beheren van push-bericht met behulp van Azure Mobile Engagement
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
ms.openlocfilehash: fc88db8db11d1ed12fa95c2087c9a32b21bf4de5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-push-notification-campaigns"></a><span data-ttu-id="555f5-103">Het maken en beheren van campagnes met pushmeldingen</span><span class="sxs-lookup"><span data-stu-id="555f5-103">How to create and manage push notification campaigns</span></span>
<span data-ttu-id="555f5-104">Een nieuwe pushcampagne maken met een complexe formule door te geven van alle informatie die u nodig hebt voor het verzenden van een push-melding kunt u de Reach-sectie van de gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="555f5-104">You can use the Reach section of the UI to create a new Push campaign with a complex formula by providing all the information you need to send a push notification.</span></span> <span data-ttu-id="555f5-105">De opties van een pushcampagne enigszins afwijken, afhankelijk van de soorten vier campagne: aankondigingen, Polls, gegevens-Pushes en tegels (alleen Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="555f5-105">The options of a Push campaign vary slightly depending on the four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="555f5-106">Is van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="555f5-106">Option Applies to:</span></span>
* <span data-ttu-id="555f5-107">Talen: Alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="555f5-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="555f5-108">Campagne: Alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="555f5-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="555f5-109">Melding: Aankondigingen, Polls</span><span class="sxs-lookup"><span data-stu-id="555f5-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="555f5-110">Inhoud: Uniek zijn voor elk campagnetype</span><span class="sxs-lookup"><span data-stu-id="555f5-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="555f5-111">Doelgroep: Alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="555f5-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="555f5-112">Tijdsbestek: aankondigingen, Polls, tegels</span><span class="sxs-lookup"><span data-stu-id="555f5-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="555f5-113">Test: Alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="555f5-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Reach-Campaign1][20]

## <a name="languages"></a><span data-ttu-id="555f5-115">Talen</span><span class="sxs-lookup"><span data-stu-id="555f5-115">Languages</span></span>
<span data-ttu-id="555f5-116">De vervolgkeuzelijst talen kunt u een andere versie van uw Pushmeldingen verzenden naar apparaten die zijn ingesteld op het gebruik van verschillende talen.</span><span class="sxs-lookup"><span data-stu-id="555f5-116">You can use the Languages drop-down menu to send a different version of your Push to devices that are set to use different languages.</span></span> <span data-ttu-id="555f5-117">Alle apparaten ontvangen standaard de dezelfde Push ongeacht welke taal ze zijn ingesteld om te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="555f5-117">By default, all devices will receive the same Push regardless of what language they are set to use.</span></span> <span data-ttu-id="555f5-118">De versie van de standaardtaal van de push-bewerking ontvangt de gebruiker het apparaat dat is ingesteld op een andere taal.</span><span class="sxs-lookup"><span data-stu-id="555f5-118">Users with their device set to a different language will receive the Default Language version of the Push.</span></span> <span data-ttu-id="555f5-119">Veel van de opties voor de push-campagne kunnen u alternatieve inhoud opgeven voor elk van de extra talen die u selecteert.</span><span class="sxs-lookup"><span data-stu-id="555f5-119">Many of the push campaign options allow you to specify alternate content for each of the additional languages you select.</span></span> 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="555f5-121">Taalverschillen van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="555f5-121">Language differences apply to:</span></span>
* <span data-ttu-id="555f5-122">Talen: Unieke talen kunnen naast de standaardtaal worden geselecteerd</span><span class="sxs-lookup"><span data-stu-id="555f5-122">Languages:    Unique languages may be selected in addition to the default language</span></span>
* <span data-ttu-id="555f5-123">Campagne: Gelijk voor alle talen</span><span class="sxs-lookup"><span data-stu-id="555f5-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="555f5-124">Melding: Uniek voor elke taal naast de standaardtaal</span><span class="sxs-lookup"><span data-stu-id="555f5-124">Notification:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="555f5-125">Inhoud: Uniek voor elke taal naast de standaardtaal</span><span class="sxs-lookup"><span data-stu-id="555f5-125">Content:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="555f5-126">Doelgroep: Kan worden gefilterd door het criterium van een afzonderlijke taal</span><span class="sxs-lookup"><span data-stu-id="555f5-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="555f5-127">Tijdsbestek: hetzelfde voor alle talen</span><span class="sxs-lookup"><span data-stu-id="555f5-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="555f5-128">Test: Voor elke taal tegelijk kunnen worden verzonden</span><span class="sxs-lookup"><span data-stu-id="555f5-128">Test:    May be sent to each language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="555f5-129">Ondersteunde talen:</span><span class="sxs-lookup"><span data-stu-id="555f5-129">Supported Languages:</span></span>
* <span data-ttu-id="555f5-130">Arabisch (ar)</span><span class="sxs-lookup"><span data-stu-id="555f5-130">Arabic (ar)</span></span> 
* <span data-ttu-id="555f5-131">Bulgaars (bg)</span><span class="sxs-lookup"><span data-stu-id="555f5-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="555f5-132">Catalaans (ca)</span><span class="sxs-lookup"><span data-stu-id="555f5-132">Catalan (ca)</span></span> 
* <span data-ttu-id="555f5-133">Chinees (zh)</span><span class="sxs-lookup"><span data-stu-id="555f5-133">Chinese (zh)</span></span> 
* <span data-ttu-id="555f5-134">Kroatisch (uur)</span><span class="sxs-lookup"><span data-stu-id="555f5-134">Croatian (hr)</span></span> 
* <span data-ttu-id="555f5-135">Czech (CS)</span><span class="sxs-lookup"><span data-stu-id="555f5-135">Czech (cs)</span></span> 
* <span data-ttu-id="555f5-136">Deens (da)</span><span class="sxs-lookup"><span data-stu-id="555f5-136">Danish (da)</span></span> 
* <span data-ttu-id="555f5-137">Nederlands (nl)</span><span class="sxs-lookup"><span data-stu-id="555f5-137">Dutch (nl)</span></span> 
* <span data-ttu-id="555f5-138">Engels (en)</span><span class="sxs-lookup"><span data-stu-id="555f5-138">English (en)</span></span> 
* <span data-ttu-id="555f5-139">Fins (fi)</span><span class="sxs-lookup"><span data-stu-id="555f5-139">Finnish (fi)</span></span> 
* <span data-ttu-id="555f5-140">Frans (fr)</span><span class="sxs-lookup"><span data-stu-id="555f5-140">French (fr)</span></span> 
* <span data-ttu-id="555f5-141">Duits (de)</span><span class="sxs-lookup"><span data-stu-id="555f5-141">German (de)</span></span> 
* <span data-ttu-id="555f5-142">Grieks (el)</span><span class="sxs-lookup"><span data-stu-id="555f5-142">Greek (el)</span></span> 
* <span data-ttu-id="555f5-143">Hebreeuwse (hij)</span><span class="sxs-lookup"><span data-stu-id="555f5-143">Hebrew (he)</span></span> 
* <span data-ttu-id="555f5-144">Hindi (hoog)</span><span class="sxs-lookup"><span data-stu-id="555f5-144">Hindi (hi)</span></span> 
* <span data-ttu-id="555f5-145">Hongaars (hu)</span><span class="sxs-lookup"><span data-stu-id="555f5-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="555f5-146">Indonesisch (id)</span><span class="sxs-lookup"><span data-stu-id="555f5-146">Indonesian (id)</span></span> 
* <span data-ttu-id="555f5-147">Italiaans (it)</span><span class="sxs-lookup"><span data-stu-id="555f5-147">Italian (it)</span></span> 
* <span data-ttu-id="555f5-148">Japans (ja)</span><span class="sxs-lookup"><span data-stu-id="555f5-148">Japanese (ja)</span></span> 
* <span data-ttu-id="555f5-149">Koreaans (ko)</span><span class="sxs-lookup"><span data-stu-id="555f5-149">Korean (ko)</span></span> 
* <span data-ttu-id="555f5-150">Lets (lv)</span><span class="sxs-lookup"><span data-stu-id="555f5-150">Latvian (lv)</span></span> 
* <span data-ttu-id="555f5-151">Litouws (lt)</span><span class="sxs-lookup"><span data-stu-id="555f5-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="555f5-152">Maleis (macrolanguage) (ms)</span><span class="sxs-lookup"><span data-stu-id="555f5-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="555f5-153">Noors, Bokmål (nb)</span><span class="sxs-lookup"><span data-stu-id="555f5-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="555f5-154">Pools (pl)</span><span class="sxs-lookup"><span data-stu-id="555f5-154">Polish (pl)</span></span> 
* <span data-ttu-id="555f5-155">Portugees (pt)</span><span class="sxs-lookup"><span data-stu-id="555f5-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="555f5-156">Roemeens (ro)</span><span class="sxs-lookup"><span data-stu-id="555f5-156">Romanian (ro)</span></span> 
* <span data-ttu-id="555f5-157">Russisch (ru)</span><span class="sxs-lookup"><span data-stu-id="555f5-157">Russian (ru)</span></span> 
* <span data-ttu-id="555f5-158">Servisch (sr)</span><span class="sxs-lookup"><span data-stu-id="555f5-158">Serbian (sr)</span></span> 
* <span data-ttu-id="555f5-159">Slowaaks (sk)</span><span class="sxs-lookup"><span data-stu-id="555f5-159">Slovak (sk)</span></span> 
* <span data-ttu-id="555f5-160">Sloveens (sl)</span><span class="sxs-lookup"><span data-stu-id="555f5-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="555f5-161">Spaans (es)</span><span class="sxs-lookup"><span data-stu-id="555f5-161">Spanish (es)</span></span> 
* <span data-ttu-id="555f5-162">Zweeds (sv)</span><span class="sxs-lookup"><span data-stu-id="555f5-162">Swedish (sv)</span></span> 
* <span data-ttu-id="555f5-163">Tagalog (tl)</span><span class="sxs-lookup"><span data-stu-id="555f5-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="555f5-164">Thais (e)</span><span class="sxs-lookup"><span data-stu-id="555f5-164">Thai (th)</span></span> 
* <span data-ttu-id="555f5-165">Turks (tr)</span><span class="sxs-lookup"><span data-stu-id="555f5-165">Turkish (tr)</span></span> 
* <span data-ttu-id="555f5-166">Oekraïens (GB)</span><span class="sxs-lookup"><span data-stu-id="555f5-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="555f5-167">Vietnamees (vi)</span><span class="sxs-lookup"><span data-stu-id="555f5-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="555f5-168">Campagne</span><span class="sxs-lookup"><span data-stu-id="555f5-168">Campaign</span></span>
<span data-ttu-id="555f5-169">De naam en categorie van uw campagne ook instellen als u van plan bent voor het negeren van de sectie doelgroep van een pushcampagne en verzend deze campagne via de Reach API (en een aantal elementen met de geringe Push-API) in plaats daarvan kunt u de sectie campagne.</span><span class="sxs-lookup"><span data-stu-id="555f5-169">You can use the Campaign section to set the name and category of your campaign as well as if you plan to ignore the audience section of a Push campaign and send this campaign via the Reach API (and some elements with the low level Push API) instead.</span></span> <span data-ttu-id="555f5-170">Categorieën kunnen worden gebruikt met een aangepaste meldingssjabloon op beheer in-app-meldingen op basis van vooraf gedefinieerde instellingen.</span><span class="sxs-lookup"><span data-stu-id="555f5-170">Categories can be used with a custom notification template to control in-app notifications based on predefined settings.</span></span> <span data-ttu-id="555f5-171">U kunt een lijst met uw bestaande 'categorieën' via de Reach API ophalen.</span><span class="sxs-lookup"><span data-stu-id="555f5-171">You can get a list of your existing “Categories” via the Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="555f5-172">Als u de optie 'Negeren doelgroep, push wordt naar gebruikers verzonden via de API' in de sectie "Campagne" van een Reach-campagne gebruiken, de campagne wordt niet automatisch verzenden, moet u handmatig verzenden via de Reach API.</span><span class="sxs-lookup"><span data-stu-id="555f5-172">If you use the "Ignore Audience, push will be sent to users via the API" option in the "Campaign" section of a Reach campaign, the campaign will NOT automatically send, you will need to send it manually via the Reach API.</span></span>

![Reach-Campaign3][22]

### <a name="option-applies-to"></a><span data-ttu-id="555f5-174">Is van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="555f5-174">Option Applies to:</span></span>
* <span data-ttu-id="555f5-175">Naam: alle</span><span class="sxs-lookup"><span data-stu-id="555f5-175">Name:    All</span></span>
* <span data-ttu-id="555f5-176">Categorie: Aankondigingen, Polls</span><span class="sxs-lookup"><span data-stu-id="555f5-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="555f5-177">Doelgroep negeren, push wordt verzonden naar gebruikers via de API: alle</span><span class="sxs-lookup"><span data-stu-id="555f5-177">Ignore Audience, push will be sent to users via the API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="555f5-178">Melding</span><span class="sxs-lookup"><span data-stu-id="555f5-178">Notification</span></span>
<span data-ttu-id="555f5-179">U kunt de sectie meldingen basisinstellingen voor het opnemen van uw push instellen: de titel van de push-bewerking, het bericht, de installatiekopie van een in-app, of als deze worden weggeklikt.</span><span class="sxs-lookup"><span data-stu-id="555f5-179">You can use the Notification section to set basic settings for your push including: The title of the Push, the message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="555f5-180">Instellingen voor veel meldingen zijn specifiek voor het platform van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="555f5-180">Many notification settings are specific to the platform of your device.</span></span> <span data-ttu-id="555f5-181">U kunt aangeven of uw push 'in-app' of 'out of app' worden verzonden of beide.</span><span class="sxs-lookup"><span data-stu-id="555f5-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="555f5-182">(Houd er rekening mee dat gebruikers kunnen 'opt-in' of 'opt-out' van 'buiten app' Pushes op het besturingssysteem niveau op hun apparaten en Azure Mobile Engagement kan niet worden voor deze instelling overschrijven.</span><span class="sxs-lookup"><span data-stu-id="555f5-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at the Operating System level on their devices, and Azure Mobile Engagement will not be able to override this setting.</span></span> <span data-ttu-id="555f5-183">Denk eraan dat de Reach API 'in-app verwerkt' en 'out van app' duwt.</span><span class="sxs-lookup"><span data-stu-id="555f5-183">Also remember that the Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="555f5-184">De Push-API kan worden gebruikt voor 'out of app' pushes te verwerken.) Pushes kunnen worden aangepast met afbeeldingen of HTML-inhoud, inclusief dieptekoppelingen voor het koppelen van buiten uw App of op een andere locatie in uw App (Android SDK 2.1.0 of hoger opzet categorieën vereist).</span><span class="sxs-lookup"><span data-stu-id="555f5-184">The Push API can be used to handle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or to another location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="555f5-185">U kunt de pictogram- of iOS-badge wijzigen en verzenden van tekst of web-inhoud (een pop-upvenster met de HTML-inhoud, URL koppeling naar een andere locatie binnen of buiten de app).</span><span class="sxs-lookup"><span data-stu-id="555f5-185">You can change the icon or iOS badge, and send either text or web content (a popup with html content, URL link to another location either inside or outside of the app).</span></span> <span data-ttu-id="555f5-186">U kunt ook Android-apparaten beltoon laten horen of Trillen met de push-bewerking.</span><span class="sxs-lookup"><span data-stu-id="555f5-186">You can also make Android devices ring or vibrate with the Push.</span></span> <span data-ttu-id="555f5-187">(Houd er rekening mee dat u de juiste moet machtigingen van de SDK in uw Android-manifestbestand ring of een apparaat laten trillen.) Er is momenteel geen bedrijfstak standaard voor Android 'grote afbeelding' grootten, aangezien schermgrootte verschillen op elk apparaat maar 400 x 100 afbeeldingen op bijna elke schermgrootte werken.</span><span class="sxs-lookup"><span data-stu-id="555f5-187">(Remember that you will need the correct SDK permissions in your Android manifest file to ring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="555f5-188">Levering typen:</span><span class="sxs-lookup"><span data-stu-id="555f5-188">Delivery Types:</span></span>
* <span data-ttu-id="555f5-189">Alleen buiten app: wanneer de toepassing niet wordt gebruikt door de gebruiker de melding worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="555f5-189">Out of app only: the notification will be delivered when the user does not use the application.</span></span>
* <span data-ttu-id="555f5-190">De out-of alleen appmelding vereist een certificaat van Apple of Google (APNS of GCM-certificaat).</span><span class="sxs-lookup"><span data-stu-id="555f5-190">The out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="555f5-191">In-app alleen: deze melding wordt weergegeven wanneer er op de toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="555f5-191">In-app only: The notification appears only when the application is running.</span></span>
* <span data-ttu-id="555f5-192">De melding gebruikt het Capptain levering systeem voor het bereiken van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="555f5-192">The notification uses the Capptain delivery system to reach the user.</span></span> <span data-ttu-id="555f5-193">U kunt de visuele lay-out/weergave van uw push volledig aanpassen.</span><span class="sxs-lookup"><span data-stu-id="555f5-193">You can fully customize the visual layout/display of your push.</span></span>
* <span data-ttu-id="555f5-194">Op elk gewenst moment: Deze optie zorgt ervoor dat u een melding die van de toepassing wordt uitgevoerd of niet verzenden.</span><span class="sxs-lookup"><span data-stu-id="555f5-194">Anytime: This option ensures that you send a notification either the application is running or not.</span></span>

![Reach-Campaign4][23]

### <a name="option-applies-to"></a><span data-ttu-id="555f5-196">Is van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="555f5-196">Option Applies to:</span></span>
* <span data-ttu-id="555f5-197">Melding: Aankondigingen, Polls</span><span class="sxs-lookup"><span data-stu-id="555f5-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="555f5-198">Inhoud</span><span class="sxs-lookup"><span data-stu-id="555f5-198">Content</span></span>
<span data-ttu-id="555f5-199">De sectie inhoud kunt u de inhoud van uw aankondigingen, Polls, gegevens-Pushes en tegels (alleen Windows Phone) wijzigen.</span><span class="sxs-lookup"><span data-stu-id="555f5-199">You can use the Content section to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="555f5-200">De instelling van de inhoud van pushcampagnes is specifiek voor het type campagne.</span><span class="sxs-lookup"><span data-stu-id="555f5-200">The Content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="555f5-201">Zie ook</span><span class="sxs-lookup"><span data-stu-id="555f5-201">See also</span></span>
* <span data-ttu-id="555f5-202">[UI-documentatie - bereiken - Push-inhoud][Link 29]</span><span class="sxs-lookup"><span data-stu-id="555f5-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Reach-Campaign5][24]

## <a name="audience"></a><span data-ttu-id="555f5-204">Doelgroep</span><span class="sxs-lookup"><span data-stu-id="555f5-204">Audience</span></span>
<span data-ttu-id="555f5-205">U kunt de sectie doelgroep gebruiken voor het definiëren van een standaard lijst met items om te beperken van uw campagne of limieten uw campagne op basis van aangepaste criteria.</span><span class="sxs-lookup"><span data-stu-id="555f5-205">You can use the Audience section to define a standard list of items to limit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="555f5-206">De standaard set opties voor het beperken van uw doelgroep kunt u om naar nieuwe of oude gebruikers of alleen de systeemeigen push-gebruikers te pushen.</span><span class="sxs-lookup"><span data-stu-id="555f5-206">The standard set of options to Limit your Audience allows you to push to either new or old users or native push users only.</span></span> <span data-ttu-id="555f5-207">U kunt ook een quotum om te beperken het aantal gebruikers die de push-bewerking ontvangen instellen.</span><span class="sxs-lookup"><span data-stu-id="555f5-207">You can also set a quota to limit the number of users who receive the push.</span></span> <span data-ttu-id="555f5-208">U kunt handmatig de expressie voor het filteren van uw campagne om op te nemen van een of meer criterium voor Doelgebruikers bewerken.</span><span class="sxs-lookup"><span data-stu-id="555f5-208">You can manually Edit the expression for how your campaign is filtered to include one or more criterion to target users.</span></span> <span data-ttu-id="555f5-209">U kunt handmatig een doelgroepexpressie typen.</span><span class="sxs-lookup"><span data-stu-id="555f5-209">You can manually type an audience expression.</span></span> <span data-ttu-id="555f5-210">Een dergelijke expressie moet expliciet definiëren voor de relatie tussen criteria.</span><span class="sxs-lookup"><span data-stu-id="555f5-210">Such an expression must explicitly define the relation between criteria.</span></span> <span data-ttu-id="555f5-211">Een criterium is beschreven door een id die met een hoofdletter moet beginnen en mag geen spaties bevatten.</span><span class="sxs-lookup"><span data-stu-id="555f5-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="555f5-212">De relatie tussen de criteria kan worden beschreven met behulp van 'en', 'of', 'not' operators, evenals '(',')'.</span><span class="sxs-lookup"><span data-stu-id="555f5-212">The relation between the criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="555f5-213">Voorbeeld: 'Criterion1 of (Criterion1 en niet Criterion2)'.</span><span class="sxs-lookup"><span data-stu-id="555f5-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="555f5-214">Met een grote doelgroep opgenomen in de campagnes, mag de serverzijde die gericht is op scan traag is, met name als u probeert te starten meerdere campagnes op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="555f5-214">With a large audience included in campaigns, the server side targeting scan can be slow, especially if you attempt to start multiple campaigns at the same time.</span></span>

* <span data-ttu-id="555f5-215">Alleen indien mogelijk een campagne start tegelijk.</span><span class="sxs-lookup"><span data-stu-id="555f5-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="555f5-216">Alleen de meest, vier campagnes starten op een tijdstip.</span><span class="sxs-lookup"><span data-stu-id="555f5-216">At the most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="555f5-217">Push-alleen voor uw actieve gebruikers (selectievakje ' alleen gebruikers benaderen die kunnen worden bereikt met behulp van Native Pushberichten' en 'Alleen actieve gebruikers benaderen') zodat alleen uw gebruikers die nog steeds de app hebt geïnstalleerd en deze gebruiken, moeten worden gescand.</span><span class="sxs-lookup"><span data-stu-id="555f5-217">Push only to your active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have the app installed and use it will need to be scanned.</span></span>
  <span data-ttu-id="555f5-218">Als uw doelgroep is gedefinieerd, kunt u de knop simuleren om erachter te komen hoeveel gebruikers deze Push ontvangt.</span><span class="sxs-lookup"><span data-stu-id="555f5-218">Once your audience is defined, you can use the simulate button to find out how many users will receive this Push.</span></span> <span data-ttu-id="555f5-219">Hiermee wordt het aantal bekende gebruikers mogelijk doel voor deze doelgroep (dit is een schatting op basis van een steekproef van gebruikers) berekenen.</span><span class="sxs-lookup"><span data-stu-id="555f5-219">This will compute the number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="555f5-220">Vergeet niet dat gebruikers die de toepassing hebben verwijderd eveneens deel van deze doelgroep uitmaken, maar kunnen niet worden bereikt.</span><span class="sxs-lookup"><span data-stu-id="555f5-220">Be aware that users who have uninstalled the application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="555f5-221">Zie ook</span><span class="sxs-lookup"><span data-stu-id="555f5-221">See also</span></span>
* <span data-ttu-id="555f5-222">[UI - Reach - documentatie nieuw Push criterium][Link 28]</span><span class="sxs-lookup"><span data-stu-id="555f5-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Reach-Campaign6][25]

### <a name="edit-expression"></a><span data-ttu-id="555f5-224">Expressie bewerken</span><span class="sxs-lookup"><span data-stu-id="555f5-224">Edit expression</span></span>
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="555f5-226">Limiet voor die uw doelgroep is van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="555f5-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="555f5-227">Alleen een subset van gebruikers benaderen: alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="555f5-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="555f5-228">Alleen oude gebruikers benaderen: alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="555f5-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="555f5-229">Alleen nieuwe gebruikers benaderen: alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="555f5-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="555f5-230">Alleen niet-actieve gebruikers benaderen: aankondigingen, Polls, tegels</span><span class="sxs-lookup"><span data-stu-id="555f5-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="555f5-231">Alleen actieve gebruikers benaderen: alle (aankondigingen, Polls, gegevens-Pushes, tegels)</span><span class="sxs-lookup"><span data-stu-id="555f5-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="555f5-232">Alleen gebruikers benaderen die kunnen worden bereikt via een Native Pushbericht: aankondigingen, Polls</span><span class="sxs-lookup"><span data-stu-id="555f5-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="555f5-233">Tijdsbestek</span><span class="sxs-lookup"><span data-stu-id="555f5-233">Time Frame</span></span>
<span data-ttu-id="555f5-234">U kunt de sectie tijdsbestek ingesteld wanneer de pushmelding wordt verzonden of u kunt het tijdsbestek onmiddellijk starten van de campagne leeg laten.</span><span class="sxs-lookup"><span data-stu-id="555f5-234">You can use the Time Frame section to set when the push will be sent or you can leave the time frame blank to start the campaign immediately.</span></span> <span data-ttu-id="555f5-235">Houd er rekening mee dat met behulp van de tijdzone van de eindgebruikers de campagne eerder start mogelijk dan u voor uw eindgebruikers in Azië verwacht en kleine batches van pushes tegelijkertijd verzendt totdat alle tijdzones in de hele wereld overeen met het tijdsbestek dat is ingesteld voor uw campagne een dag.</span><span class="sxs-lookup"><span data-stu-id="555f5-235">Remember that using the end-users' time zone may start the campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in the world match the time frame set for your campaign.</span></span> <span data-ttu-id="555f5-236">Met behulp van de tijdzone van de eindgebruikers kan ook vertragingen veroorzaken bij campagnes worden gestart omdat het de tijd aanvragen via de telefoon voordat u begint de push-bewerking heeft.</span><span class="sxs-lookup"><span data-stu-id="555f5-236">Using the end users' time zone can also cause delays in campaigns since it has to request the time from the phone before starting the push.</span></span>

> [!NOTE]
> <span data-ttu-id="555f5-237">Zonder een einddatum in cache campagnes pushes lokaal en nog steeds weergegeven nadat u handmatig voltooid campagnes.</span><span class="sxs-lookup"><span data-stu-id="555f5-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="555f5-238">Om te voorkomen dat dit gedrag, specifieke eindtijd voor campagnes.</span><span class="sxs-lookup"><span data-stu-id="555f5-238">To avoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="555f5-239">Zie ook</span><span class="sxs-lookup"><span data-stu-id="555f5-239">See also</span></span>
* <span data-ttu-id="555f5-240">[Bereiken - hoe Tos – plannen][Link 3]</span><span class="sxs-lookup"><span data-stu-id="555f5-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="555f5-242">Instellingen van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="555f5-242">Settings Apply to:</span></span>
* <span data-ttu-id="555f5-243">Tijdsbestek: aankondigingen, Polls, tegels</span><span class="sxs-lookup"><span data-stu-id="555f5-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="555f5-244">Test</span><span class="sxs-lookup"><span data-stu-id="555f5-244">Test</span></span>
<span data-ttu-id="555f5-245">De sectie Test kunt u deze pushmelding wordt verzonden naar uw eigen testapparaat voordat u de campagne opslaat.</span><span class="sxs-lookup"><span data-stu-id="555f5-245">You can use the Test section to send this push to your own test device before saving the campaign.</span></span> <span data-ttu-id="555f5-246">Als u de aangepaste talen voor deze campagne hebt geconfigureerd, kunt u de push-bewerking testen in elke taal.</span><span class="sxs-lookup"><span data-stu-id="555f5-246">If you have configured any custom languages for this campaign, you can test the push in each language.</span></span> <span data-ttu-id="555f5-247">U kunt een testapparaat van 'Mijn Account' instellen.</span><span class="sxs-lookup"><span data-stu-id="555f5-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="555f5-248">Er zijn geen gegevens worden geregistreerd wanneer u met de knop 'test' serverzijde pushes, gegevens alleen worden geregistreerd voor echte pushcampagnes.</span><span class="sxs-lookup"><span data-stu-id="555f5-248">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="555f5-249">Zie ook</span><span class="sxs-lookup"><span data-stu-id="555f5-249">See also</span></span>
* <span data-ttu-id="555f5-250">[UI-documentatie - Mijn Account][Link 14]</span><span class="sxs-lookup"><span data-stu-id="555f5-250">[UI Documentation - My Account][Link 14]</span></span>

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

