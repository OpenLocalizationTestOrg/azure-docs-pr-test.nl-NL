---
title: Azure Mobile Engagement-gebruikersinterface - Reach criterium
description: Informatie over het gebruik van criteria gerichte campagnes met pushmeldingen verzenden naar een specifieke subset van uw gebruikers met behulp van Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 803b44721d0ab1ac7b5a8074e18857fc57adb724
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-targeting-criteria-to-send-push-campaigns-to-a-select-subset-of-your-users"></a><span data-ttu-id="1e623-103">Het gebruik van criteria gerichte pushcampagnes verzenden naar een specifieke subset van uw gebruikers</span><span class="sxs-lookup"><span data-stu-id="1e623-103">How to use targeting criteria to send push campaigns to a select subset of your users</span></span>
<span data-ttu-id="1e623-104">Uw doelgroep gericht op specifieke criteria met de knop "Nieuw criterium" is een van de meest krachtige concepten in Azure Mobile Engagement helpt u relevante verzenden pushmeldingen dat klanten reageren zullen op in plaats van spam iedereen.</span><span class="sxs-lookup"><span data-stu-id="1e623-104">Targeting your audience by specific criteria with the "New Criteria" button is one of the most powerful concepts in Azure Mobile Engagement that helps you send relevant push notifications that the customers will respond to instead of Spamming everyone.</span></span> <span data-ttu-id="1e623-105">U kunt uw doelgroep op basis van criteria standaard beperken en simuleren pushes om te bepalen hoeveel mensen de melding wilt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="1e623-105">You can limit your audience based on standard criteria and simulate pushes to determine how many people will receive the notification.</span></span>

<span data-ttu-id="1e623-106">**Zie ook:**</span><span class="sxs-lookup"><span data-stu-id="1e623-106">**See also:**</span></span>

* <span data-ttu-id="1e623-107">[Nieuwe Pushcampagne van UI - Reach - documentatie][Link 27]</span><span class="sxs-lookup"><span data-stu-id="1e623-107">[UI Documentation - Reach - New Push Campaign][Link 27]</span></span>

## <a name="audience-criteria-can-include"></a><span data-ttu-id="1e623-108">Doelgroep criteria kunnen opnemen:</span><span class="sxs-lookup"><span data-stu-id="1e623-108">Audience criteria can include:</span></span>
* <span data-ttu-id="1e623-109">** Technicals: ** kunt u zich richten op basis van de dezelfde technische informatie die u in de secties Analytics en Monitor zien kunt.</span><span class="sxs-lookup"><span data-stu-id="1e623-109">**Technicals: ** You can target based on the same technical information you can see in the Analytics and Monitor sections.</span></span> <span data-ttu-id="1e623-110">**Zie ook:** [UI-documentatie - Analytics][Link 15], [UI-documentatie - Monitor][Link 16]</span><span class="sxs-lookup"><span data-stu-id="1e623-110">**See also:** [UI Documentation - Analytics][Link 15],  [UI Documentation - Monitor][Link 16]</span></span>
* <span data-ttu-id="1e623-111">**Locatie:** toepassingen die gebruikmaken van "realtime locatie rapportage" met Geofencing kunnen geografische locatie gebruiken als een criterium toe te passen van een doelgroep van de GPS-locatie.</span><span class="sxs-lookup"><span data-stu-id="1e623-111">**Location:** Applications that use "Real time location reporting" with Geo-Fencing can use Geo-Location as a criteria to target an audience from the GPS location.</span></span> <span data-ttu-id="1e623-112">'Vertraagde gebied locatie rapportage' aanroep ook worden gebruikt voor het doel van een doelgroep vanaf de locatie van de mobiele telefoon ("realtime locatie rapportage" en 'Vertraagde Locatiemelding' moet worden geactiveerd uit de SDK).</span><span class="sxs-lookup"><span data-stu-id="1e623-112">"Lazy Area Location Reporting" call also be used to target an audience from the cell phone location ("Real time location reporting" and "Lazy Area Location Reporting" must be activated from the SDK).</span></span> <span data-ttu-id="1e623-113">**Zie ook:** [SDK-documentatie - iOS - integratie][Link 5], [SDK-documentatie - Android - integratie][Link 5]</span><span class="sxs-lookup"><span data-stu-id="1e623-113">**See also:** [SDK Documentation - iOS -  Integration][Link 5], [SDK Documentation - Android -  Integration][Link 5]</span></span>
* <span data-ttu-id="1e623-114">**Reach Feedback:** kunt u uw doelgroep op basis van hun feedback van eerdere reach-meldingen via reach feedback van aankondigingen, Polls en gegevens-Pushes richten.</span><span class="sxs-lookup"><span data-stu-id="1e623-114">**Reach Feedback:** You can target your audience based on their feedback from previous reach notifications through reach feedback from Announcements, Polls, and Data Pushes.</span></span> <span data-ttu-id="1e623-115">Hiermee kunt u met betere doel uw doelgroep na twee of drie campagnes bereiken dan mogelijk is de eerste keer.</span><span class="sxs-lookup"><span data-stu-id="1e623-115">This enables you to better target your audience after two or three reach campaigns than you could the first time.</span></span> <span data-ttu-id="1e623-116">Het kan ook worden gebruikt voor het filteren van gebruikers die al een melding met vergelijkbare inhoud ontvangen door een campagne niet worden verzonden naar gebruikers die een specifieke vorige campagne al ontvangen.</span><span class="sxs-lookup"><span data-stu-id="1e623-116">It can also be used to filter out users who already received a notification with similar content, by setting a campaign to NOT be sent to users who already received a specific previous campaign.</span></span> <span data-ttu-id="1e623-117">U kunt zelfs voorkomen dat gebruikers een bepaalde campagne die nog steeds actief nieuwe Pushes ontvangen die zijn opgenomen.</span><span class="sxs-lookup"><span data-stu-id="1e623-117">You can even exclude users who are included a specific campaign that is still active from receiving new Pushes.</span></span> <span data-ttu-id="1e623-118">**Zie ook:** [inhoud van de gebruikersinterface Documentation - Reach - Push][Link 29]</span><span class="sxs-lookup"><span data-stu-id="1e623-118">**See also:** [UI Documentation -  Reach - Push Content][Link 29]</span></span>
* <span data-ttu-id="1e623-119">**Installeren bijhouden:** kunt u gegevens op basis van waar uw gebruikers geïnstalleerd in uw App bijhouden.</span><span class="sxs-lookup"><span data-stu-id="1e623-119">**Install Tracking:** You can track information based on where your users installed your App.</span></span> <span data-ttu-id="1e623-120">**Zie ook:** [UI-documentatie - instellingen][Link 20]</span><span class="sxs-lookup"><span data-stu-id="1e623-120">**See also:** [UI Documentation -  Settings][Link 20]</span></span>
* <span data-ttu-id="1e623-121">**Gebruikersprofiel:** u doel op basis van informatie van de standaardgebruiker kunt en u kunt doel op basis van de aangepaste app-gegevens die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1e623-121">**User Profile:** You can target based on standard user information and you can target based on the custom app info that you have created.</span></span> <span data-ttu-id="1e623-122">Dit omvat gebruikers die u momenteel bent aangemeld en gebruikers die specifieke vragen die u hebt aangegeven dat ze worden ingesteld in de app zelf in plaats van alleen hoe ze hebben gereageerd op vorige campagnes beantwoord.</span><span class="sxs-lookup"><span data-stu-id="1e623-122">This includes users who are currently logged in and users that have answered specific questions you have asked them to set in the app itself instead of just how they have responded to previous campaigns.</span></span> <span data-ttu-id="1e623-123">Al je App-gegevens voor uw app weergegeven op deze lijst gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="1e623-123">All of your App Info's defined for your app show up on this list.</span></span>
* <span data-ttu-id="1e623-124">Segmenten: U kunt ook doel op basis van segmenten die u hebt gemaakt op basis van specifieke gebruikersgedrag met meerdere criteria.</span><span class="sxs-lookup"><span data-stu-id="1e623-124">Segments: You can also target based on segments that you have created based on specific user behavior containing multiple criteria.</span></span> <span data-ttu-id="1e623-125">Alle van de segmenten die zijn gedefinieerd voor uw app weergegeven op deze lijst.</span><span class="sxs-lookup"><span data-stu-id="1e623-125">All of your segments defined for your app show up on this list.</span></span> <span data-ttu-id="1e623-126">**Zie ook:** [UI-documentatie - segmenten][Link 18]</span><span class="sxs-lookup"><span data-stu-id="1e623-126">**See also:** [UI Documentation -  Segments][Link 18]</span></span>
* <span data-ttu-id="1e623-127">**App-Info:** aangepaste App Info labels kan worden gemaakt vanuit 'Instellingen' voor het bijhouden van gebruikersgedrag.</span><span class="sxs-lookup"><span data-stu-id="1e623-127">**App Info:** Custom App Info Tags can be created from “Settings” to track user behavior.</span></span> <span data-ttu-id="1e623-128">**Zie ook:** [UI-documentatie - instellingen][Link 20]</span><span class="sxs-lookup"><span data-stu-id="1e623-128">**See also:** [UI Documentation -  Settings][Link 20]</span></span>

## <a name="example"></a><span data-ttu-id="1e623-129">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1e623-129">Example:</span></span>
<span data-ttu-id="1e623-130">Als u een aankondiging push alleen naar de submap reeks gebruikers die u hebt een actie aankopen binnen Apps uitgevoerd wilt.</span><span class="sxs-lookup"><span data-stu-id="1e623-130">If you want to push an announcement only to the sub-set of your users that have performed an in-app purchase action.</span></span>

1. <span data-ttu-id="1e623-131">Ga naar de instellingenpagina van uw toepassing, selecteert u het menu 'App-info' en 'Nieuwe app-info' selecteren</span><span class="sxs-lookup"><span data-stu-id="1e623-131">Go to your application settings page, select the "App info" menu and select "New app info"</span></span>
2. <span data-ttu-id="1e623-132">Registreren van een nieuwe Booleaanse app-info 'inAppPurchase' genoemd</span><span class="sxs-lookup"><span data-stu-id="1e623-132">Register a new Boolean app info called "inAppPurchase"</span></span>
3. <span data-ttu-id="1e623-133">Ervoor dat uw toepassing ingesteld op 'true' wanneer de gebruiker met succes een aankopen binnen Apps uitvoert deze app-gegevens (met behulp van de sendAppInfo ('inAppPurchase',...) functie)</span><span class="sxs-lookup"><span data-stu-id="1e623-133">Make your application set this app info to "true" when the user successfully performs an in-app purchase (by using the sendAppInfo("inAppPurchase", ...) function)</span></span>
4. <span data-ttu-id="1e623-134">Als u niet wilt u dit doet in uw toepassing, kunt u dit doen vanuit uw back-end via de API van het apparaat)</span><span class="sxs-lookup"><span data-stu-id="1e623-134">If you don't want to do this from your application, you can do it from your backend by using the device API)</span></span>
5. <span data-ttu-id="1e623-135">En, hoeft u alleen uw aankondiging maken met een criterium voor het beperken van uw doelgroep naar gebruikers met de 'inAppPurchase' is ingesteld op 'true')</span><span class="sxs-lookup"><span data-stu-id="1e623-135">Then, you just need to create your announcement, with a criterion limiting your audience to users having "inAppPurchase" set to "true")</span></span>

> [!NOTE]
> <span data-ttu-id="1e623-136">Azure Mobile Engagement voor het verzamelen van informatie van de apparaten van gebruikers voordat de pushmelding wordt verzonden, en dus kan leiden tot een vertraging die gericht is op basis van criteria dan app info tags is vereist.</span><span class="sxs-lookup"><span data-stu-id="1e623-136">Targeting based on criteria other than app info tags requires Azure Mobile Engagement to gather information from your users' devices before the push is sent and so can cause a delay.</span></span> <span data-ttu-id="1e623-137">Configuratie van complexe push opties (zoals het bijwerken van badges) kunnen ook worden vertraagd duwt.</span><span class="sxs-lookup"><span data-stu-id="1e623-137">Complex push configuration options (like updating badges) can also delay pushes.</span></span> <span data-ttu-id="1e623-138">Met behulp van een campagne 'één keer' van de Push-API is de absolute snelste pushmethode in Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="1e623-138">Using a "one shot" campaign from the Push API is the absolute fastest push method in Azure Mobile Engagement.</span></span> <span data-ttu-id="1e623-139">Gebruik alleen de labels van app-info als push criteria voor een Reach-campagne (zowel via de Reach API of de gebruikersinterface) is de volgende snelste methode omdat tags van app-gegevens worden opgeslagen op de server.</span><span class="sxs-lookup"><span data-stu-id="1e623-139">Using only app info tags as push criteria for a Reach campaign (either from the Reach API or the UI) is the next fastest method since app info tags are stored on the server side.</span></span> <span data-ttu-id="1e623-140">Gebruik van andere doelitems criteria voor een pushcampagne is de meest flexibele maar traagste pushmethode omdat Azure Mobile Engagement query uitvoeren op de apparaten om te verzenden van de campagne.</span><span class="sxs-lookup"><span data-stu-id="1e623-140">Using other targeting criteria for a push campaign is the most flexible but slowest push method since Azure Mobile Engagement has to query the devices in order to send the campaign.</span></span>

![Reach-Criterion1][29] 

## <a name="criterion-options-apply-to"></a><span data-ttu-id="1e623-142">Opties voor criterium van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="1e623-142">Criterion Options Apply to:</span></span>
* <span data-ttu-id="1e623-143">**Technicals**</span><span class="sxs-lookup"><span data-stu-id="1e623-143">**Technicals**</span></span>     
* <span data-ttu-id="1e623-144">De naam van de firmware: de naam van de Firmware</span><span class="sxs-lookup"><span data-stu-id="1e623-144">Firmware name:    Firmware name</span></span>
* <span data-ttu-id="1e623-145">Firmwareversie: firmwareversie</span><span class="sxs-lookup"><span data-stu-id="1e623-145">Firmware version:    Firmware version</span></span>
* <span data-ttu-id="1e623-146">Apparaatmodel: Apparaatmodel</span><span class="sxs-lookup"><span data-stu-id="1e623-146">Device model:    Device model</span></span>
* <span data-ttu-id="1e623-147">De fabrikant van apparaat: de fabrikant van apparaat</span><span class="sxs-lookup"><span data-stu-id="1e623-147">Device manufacturer:    Device manufacturer</span></span>
* <span data-ttu-id="1e623-148">Toepassingsversie: toepassingsversie</span><span class="sxs-lookup"><span data-stu-id="1e623-148">Application version:    Application version</span></span>
* <span data-ttu-id="1e623-149">Provider name: naam van de provider, niet gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="1e623-149">Carrier name:    Carrier name, undefined</span></span>
* <span data-ttu-id="1e623-150">Carrier land: Carrier land, niet gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="1e623-150">Carrier country:    Carrier country, undefined</span></span>
* <span data-ttu-id="1e623-151">Netwerktype: type netwerk</span><span class="sxs-lookup"><span data-stu-id="1e623-151">Network type:    Network type</span></span>
* <span data-ttu-id="1e623-152">Landinstellingen: landinstelling</span><span class="sxs-lookup"><span data-stu-id="1e623-152">Locale:    Locale</span></span>
* <span data-ttu-id="1e623-153">Grootte van het scherm: grootte van het scherm</span><span class="sxs-lookup"><span data-stu-id="1e623-153">Screen size:    Screen size</span></span>
* <span data-ttu-id="1e623-154">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="1e623-154">**Location**</span></span>      
* <span data-ttu-id="1e623-155">Laatste bekende gebied: land, regio, plaats</span><span class="sxs-lookup"><span data-stu-id="1e623-155">Last known area:    Country, Region, Locality</span></span>
* <span data-ttu-id="1e623-156">Realtime geofencing: lijst van en nuttige locaties (naam, acties), circulaire POI (naam, breedtegraad, lengtegraad, Radius in meter)</span><span class="sxs-lookup"><span data-stu-id="1e623-156">Real time geo-fencing:    List of POIs (Name, Actions), Circular POI (Name, Latitude, Longitude, Radius in meters)</span></span>
* <span data-ttu-id="1e623-157">**Feedback bereiken**</span><span class="sxs-lookup"><span data-stu-id="1e623-157">**Reach feedback**</span></span>     
* <span data-ttu-id="1e623-158">Aankondiging feedback: aankondiging, feedback</span><span class="sxs-lookup"><span data-stu-id="1e623-158">Announcement feedback:    Announcement, feedback</span></span>
* <span data-ttu-id="1e623-159">Feedback pollen: Poll, feedback</span><span class="sxs-lookup"><span data-stu-id="1e623-159">Poll feedback:    Poll, feedback</span></span>
* <span data-ttu-id="1e623-160">Antwoord feedback pollen: pollen antwoord feedback, vraag en keuze</span><span class="sxs-lookup"><span data-stu-id="1e623-160">Poll answer feedback:    Poll answer feedback, question, choice</span></span>
* <span data-ttu-id="1e623-161">Gegevens-Push feedback: gegevens-Push, feedback</span><span class="sxs-lookup"><span data-stu-id="1e623-161">Data Push feedback:    Data Push, feedback</span></span>
* <span data-ttu-id="1e623-162">**Installeer bijhouden**</span><span class="sxs-lookup"><span data-stu-id="1e623-162">**Install Tracking**</span></span>     
* <span data-ttu-id="1e623-163">Opslag: Opslag, niet gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="1e623-163">Store:    Store, Undefined</span></span>
* <span data-ttu-id="1e623-164">Bron: Bron, niet gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="1e623-164">Source:    Source, Undefined</span></span>
* <span data-ttu-id="1e623-165">**Gebruikersprofiel**</span><span class="sxs-lookup"><span data-stu-id="1e623-165">**User profile**</span></span>     
* <span data-ttu-id="1e623-166">Geslacht: man of vrouwelijk, niet gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="1e623-166">Gender:    male or female, undefined</span></span>
* <span data-ttu-id="1e623-167">Datum geboren: operator, datum is niet gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="1e623-167">Birth date:    operator, date, undefined</span></span>
* <span data-ttu-id="1e623-168">Aanmelden: true of false, niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="1e623-168">Opt-in:    true or false, undefined</span></span>
* <span data-ttu-id="1e623-169">**App-gegevens**</span><span class="sxs-lookup"><span data-stu-id="1e623-169">**App Info**</span></span>      
* <span data-ttu-id="1e623-170">Tekenreeks: Tekenreeks is niet gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="1e623-170">String:    String, undefined</span></span>
* <span data-ttu-id="1e623-171">Datum: de operator, datum, niet-gedefinieerde</span><span class="sxs-lookup"><span data-stu-id="1e623-171">Date:    operator, date, undefined</span></span>
* <span data-ttu-id="1e623-172">Geheel getal: de operator, getal, niet-gedefinieerde</span><span class="sxs-lookup"><span data-stu-id="1e623-172">Integer:    operator, number, undefined</span></span>
* <span data-ttu-id="1e623-173">Booleaanse waarde: true of false, wordt niet gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="1e623-173">Boolean:    true or false, undefined</span></span>
* <span data-ttu-id="1e623-174">**Segment**</span><span class="sxs-lookup"><span data-stu-id="1e623-174">**Segment**</span></span>    
* <span data-ttu-id="1e623-175">Naam van de segmenten (in de vervolgkeuzelijst), uitsluiten (Doelgebruikers die geen deel uit van dit segment).</span><span class="sxs-lookup"><span data-stu-id="1e623-175">Name of Segments (from dropdown list), Exclusion (target users that are not a part of this segment).</span></span>

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

