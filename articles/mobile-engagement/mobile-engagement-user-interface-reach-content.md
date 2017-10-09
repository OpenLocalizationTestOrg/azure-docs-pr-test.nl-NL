---
title: aaaAzure gebruikersinterface van de Mobile Engagement - inhoud bereiken
description: Meer informatie over hoe toomanage Hallo unieke inhoud van verschillende soorten push-melding Hallo campagnes in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a><span data-ttu-id="e7776-103">Hoe toomanage unieke inhoud van verschillende soorten campagnes met pushmeldingen Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="e7776-103">How toomanage hello unique content of hello different types of push notification campaigns</span></span>
<span data-ttu-id="e7776-104">U kunt Hallo inhoudsectie van een nieuwe reach campagne toomodify Hallo inhoud van uw aankondigingen, Polls, gegevens-Pushes en tegels (alleen Windows Phone) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e7776-104">You can use hello Content section of a new reach campaign toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="e7776-105">Hallo is inhoud deze instelling van pushcampagnes specifieke toohello type campagne.</span><span class="sxs-lookup"><span data-stu-id="e7776-105">hello content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="e7776-106">Typen inhoud:</span><span class="sxs-lookup"><span data-stu-id="e7776-106">Content types:</span></span>
* <span data-ttu-id="e7776-107">Aankondigingen</span><span class="sxs-lookup"><span data-stu-id="e7776-107">Announcements</span></span>
* <span data-ttu-id="e7776-108">Polls</span><span class="sxs-lookup"><span data-stu-id="e7776-108">Polls</span></span>
* <span data-ttu-id="e7776-109">Gegevens-pushes</span><span class="sxs-lookup"><span data-stu-id="e7776-109">Data pushes</span></span>
* <span data-ttu-id="e7776-110">Tegels (alleen Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="e7776-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="e7776-111">Inhoud van aankondigingen</span><span class="sxs-lookup"><span data-stu-id="e7776-111">Content of Announcements</span></span>
 ![Reach-Content1][30] 

### <a name="choose-hello-type-of-your-announcement"></a><span data-ttu-id="e7776-113">Hallo-type van uw aankondiging kiezen:</span><span class="sxs-lookup"><span data-stu-id="e7776-113">Choose hello type of your announcement:</span></span>
* <span data-ttu-id="e7776-114">Alleen melding: Er is een eenvoudige standaard melding.</span><span class="sxs-lookup"><span data-stu-id="e7776-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="e7776-115">Dit betekent dat tooit wordt uitgevoerd als een gebruiker erop, geen extra weergave wordt weergegeven, maar alleen Hallo actie die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="e7776-115">Meaning that if a user clicks on it, no additional view will appear, but only hello action associated tooit will occur.</span></span>
* <span data-ttu-id="e7776-116">Tekst-aankondiging: Er is een melding die Hallo gebruiker toohave kijken een tekstweergave stelt.</span><span class="sxs-lookup"><span data-stu-id="e7776-116">Text announcement: It is a notification that engages hello user toohave a look at a text view.</span></span>
* <span data-ttu-id="e7776-117">Web-aankondiging: Er is een melding die Hallo gebruiker toohave kijken een webweergave stelt.</span><span class="sxs-lookup"><span data-stu-id="e7776-117">Web announcement: It is a notification that engages hello user toohave a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="e7776-118">Zie ook</span><span class="sxs-lookup"><span data-stu-id="e7776-118">See also</span></span>
* <span data-ttu-id="e7776-119">[Bereiken - hoe Tos - aankondigingen][Link 3]</span><span class="sxs-lookup"><span data-stu-id="e7776-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="e7776-120">Over aankondigingen van webweergave:</span><span class="sxs-lookup"><span data-stu-id="e7776-120">About Web View Announcements:</span></span>
<span data-ttu-id="e7776-121">Instanties van Hallo patroon '{deviceid}' in hello HTML-code of JavaScript-code die u hier opgeeft, wordt automatisch worden vervangen door Hallo-id van Hallo apparaat Hallo aankondiging om weer te geven.</span><span class="sxs-lookup"><span data-stu-id="e7776-121">Occurrences of hello pattern "{deviceid}" in hello HTML code or JavaScript code you provide here will be automatically replaced by hello identifier of hello device displaying hello announcement.</span></span> <span data-ttu-id="e7776-122">Dit is een eenvoudige manier tooretrieve Azure Mobile Engagement apparaat-id's in een externe webservice die op uw back-office wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="e7776-122">This is an easy way tooretrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="e7776-123">Als u wilt dat toocreate een volledige scherm Webweergave (zonder Hallo actie en afsluiten standaardknoppen we bieden) kunt u Hallo volgende functies uit uw webweergave-aankondiging van JavaScript-code:</span><span class="sxs-lookup"><span data-stu-id="e7776-123">If you want toocreate a full screen web view (without hello default Action and Exit buttons we provide) you can use hello following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="e7776-124">Hallo aankondigingsactie uitvoeren: ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="e7776-124">perform hello announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="e7776-125">Hallo aankondiging afsluiten: ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="e7776-125">exit from hello announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="e7776-126">Kies uw actie:</span><span class="sxs-lookup"><span data-stu-id="e7776-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="e7776-127">Over het actie-URL's:</span><span class="sxs-lookup"><span data-stu-id="e7776-127">About Action URLs:</span></span>
<span data-ttu-id="e7776-128">Elke URL die kan worden geïnterpreteerd door het besturingssysteem kan worden gebruikt als een actie-URL.</span><span class="sxs-lookup"><span data-stu-id="e7776-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="e7776-129">Elke toegewezen URL die uw toepassing mogelijk ondersteuning (bijvoorbeeld gebruikers toomake tooa bepaald scherm springen) kan ook worden gebruikt als actie-URL.</span><span class="sxs-lookup"><span data-stu-id="e7776-129">Any dedicated URL that your application might support (e.g. toomake users jump tooa particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="e7776-130">Elk exemplaar van Hallo {deviceid} patroon wordt automatisch vervangen door Hallo-id van Hallo-apparaat Hallo actie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="e7776-130">Each occurrence of hello {deviceid} pattern is automatically replaced by hello identifier of hello device performing hello action.</span></span> <span data-ttu-id="e7776-131">Dit kan zijn gebruikte tooeasily Azure Mobile Engagement apparaat-id's ophalen via een externe webservice die op uw back-office wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="e7776-131">This can be used tooeasily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="e7776-132">**Android en iOS-acties**</span><span class="sxs-lookup"><span data-stu-id="e7776-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="e7776-133">Een webpagina openen</span><span class="sxs-lookup"><span data-stu-id="e7776-133">Open a web page</span></span>
  * <span data-ttu-id="e7776-134">http://\[web-site-domein\]</span><span class="sxs-lookup"><span data-stu-id="e7776-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="e7776-135">Voorbeeld: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="e7776-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="e7776-136">E-mail verzenden</span><span class="sxs-lookup"><span data-stu-id="e7776-136">Send an e-mail</span></span>
  * <span data-ttu-id="e7776-137">mailto:\[e-mail-ontvanger\]? onderwerp =\[onderwerp\]& body =\[bericht\]</span><span class="sxs-lookup"><span data-stu-id="e7776-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="e7776-138">Example:mailto:foo@example.com? onderwerp begroetingen % 20from % 20Azure % 20Mobile % 20Engagement =! & body = goede % 20stuff!</span><span class="sxs-lookup"><span data-stu-id="e7776-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="e7776-139">Sms-bericht verzenden</span><span class="sxs-lookup"><span data-stu-id="e7776-139">Send a SMS</span></span>
  * <span data-ttu-id="e7776-140">SMS:\[-telefoonnummer\]</span><span class="sxs-lookup"><span data-stu-id="e7776-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="e7776-141">Voorbeeld: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="e7776-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="e7776-142">Kies een telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="e7776-142">Dial a phone number</span></span>
  * <span data-ttu-id="e7776-143">Tel:\[-telefoonnummer\]</span><span class="sxs-lookup"><span data-stu-id="e7776-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="e7776-144">Voorbeeld: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="e7776-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="e7776-145">**Android alleen acties**</span><span class="sxs-lookup"><span data-stu-id="e7776-145">**Android only actions**</span></span>
  * <span data-ttu-id="e7776-146">Een toepassing op Hallo Play Store downloaden</span><span class="sxs-lookup"><span data-stu-id="e7776-146">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="e7776-147">market://details?id=\[app-pakket\]</span><span class="sxs-lookup"><span data-stu-id="e7776-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="e7776-148">Voorbeeld: market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="e7776-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="e7776-149">Een geografisch gelokaliseerde zoekopdracht uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e7776-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="e7776-150">geo:0, 0? q =\[zoekopdracht\]</span><span class="sxs-lookup"><span data-stu-id="e7776-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="e7776-151">Voorbeeld: geo:0, 0? q = starbucks, Parijs</span><span class="sxs-lookup"><span data-stu-id="e7776-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="e7776-152">**iOS alleen acties**</span><span class="sxs-lookup"><span data-stu-id="e7776-152">**iOS only actions**</span></span>
  * <span data-ttu-id="e7776-153">Een toepassing op Hallo App Store downloaden</span><span class="sxs-lookup"><span data-stu-id="e7776-153">Download an application on hello App Store</span></span>
  * <span data-ttu-id="e7776-154">http://iTunes.Apple.com/ [Land] /app/ [app-naam] /id [app-id]? mt = 8</span><span class="sxs-lookup"><span data-stu-id="e7776-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="e7776-155">Voorbeeld: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="e7776-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="e7776-156">Windows-acties</span><span class="sxs-lookup"><span data-stu-id="e7776-156">Windows Actions</span></span>
  * <span data-ttu-id="e7776-157">Een webpagina openen</span><span class="sxs-lookup"><span data-stu-id="e7776-157">Open a web page</span></span>
  * <span data-ttu-id="e7776-158">http://\[web-site-domein\]</span><span class="sxs-lookup"><span data-stu-id="e7776-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="e7776-159">Voorbeeld: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="e7776-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="e7776-160">E-mail verzenden</span><span class="sxs-lookup"><span data-stu-id="e7776-160">Send an e-mail</span></span>
  * <span data-ttu-id="e7776-161">mailto:\[e-mail-ontvanger\]? onderwerp =\[onderwerp\]& body =\[bericht\]</span><span class="sxs-lookup"><span data-stu-id="e7776-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="e7776-162">Example:mailto:foo@example.com? onderwerp begroetingen % 20from % 20Azure % 20Mobile % 20Engagement =! & body = goede % 20stuff!</span><span class="sxs-lookup"><span data-stu-id="e7776-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="e7776-163">Een sms-bericht verzenden (Skype Store App vereist)</span><span class="sxs-lookup"><span data-stu-id="e7776-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="e7776-164">SMS:\[-telefoonnummer\]</span><span class="sxs-lookup"><span data-stu-id="e7776-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="e7776-165">Voorbeeld: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="e7776-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="e7776-166">Een telefoonnummer kiezen (Skype Store App vereist)</span><span class="sxs-lookup"><span data-stu-id="e7776-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="e7776-167">Tel:\[-telefoonnummer\]</span><span class="sxs-lookup"><span data-stu-id="e7776-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="e7776-168">Voorbeeld: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="e7776-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="e7776-169">Een toepassing op Hallo Play Store downloaden</span><span class="sxs-lookup"><span data-stu-id="e7776-169">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="e7776-170">MS-windows-store: PDP? PFN =\[app-pakket-ID\]</span><span class="sxs-lookup"><span data-stu-id="e7776-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="e7776-171">Voorbeeld: ms-windows-store: PDP? PFN 4d91298a-07cb-40fb-aecc-4cb5615d53c1 =</span><span class="sxs-lookup"><span data-stu-id="e7776-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="e7776-172">Een bingmaps zoekopdracht starten</span><span class="sxs-lookup"><span data-stu-id="e7776-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="e7776-173">bingmaps:? q =\[zoekopdracht\]</span><span class="sxs-lookup"><span data-stu-id="e7776-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="e7776-174">Voorbeeld: bingmaps:? q = starbucks, Parijs</span><span class="sxs-lookup"><span data-stu-id="e7776-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="e7776-175">Een aangepast schema gebruiken</span><span class="sxs-lookup"><span data-stu-id="e7776-175">Use a custom scheme</span></span>
  * <span data-ttu-id="e7776-176">\[aangepaste schema\]://\[params aangepast schema\]</span><span class="sxs-lookup"><span data-stu-id="e7776-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="e7776-177">Voorbeeld: myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="e7776-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="e7776-178">Gebruik de pakketgegevens van een (Store App voor uitbreiding lezen vereist)</span><span class="sxs-lookup"><span data-stu-id="e7776-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="e7776-179">\[map\]\[gegevens\].\[ de extensie\]</span><span class="sxs-lookup"><span data-stu-id="e7776-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="e7776-180">Example:myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="e7776-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="e7776-181">Een bijhouden-URL maken:</span><span class="sxs-lookup"><span data-stu-id="e7776-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="e7776-182">Zie de sectie 'Instellingen' Hallo Hallo <UI Documentation> voor instructies over het bouwen van een URL bijhouden die gebruikers toodownload een van de andere toepassingen leiden zal.</span><span class="sxs-lookup"><span data-stu-id="e7776-182">See hello “Settings” section of hello <UI Documentation> for instruction on building a tracking URL that will allow users toodownload one of your other applications.</span></span>

### <a name="define-hello-texts-of-your-announcement"></a><span data-ttu-id="e7776-183">De tekst hello van uw aankondiging definiëren</span><span class="sxs-lookup"><span data-stu-id="e7776-183">Define hello texts of your announcement</span></span>
<span data-ttu-id="e7776-184">Vul in het Hallo-titel, de inhoud en de tekst van knop van uw aankondiging.</span><span class="sxs-lookup"><span data-stu-id="e7776-184">Fill in hello title, content, and button texts of your announcement.</span></span> <span data-ttu-id="e7776-185">U kunt een doelgroep van een toekomstige campagne op basis van feedback van reach Hallo van hoe gebruikers toothis campagne gereageerd richten.</span><span class="sxs-lookup"><span data-stu-id="e7776-185">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="e7776-186">Doelgroepen kan zijn gebaseerd op Hallo van feedback van of deze campagne zojuist, beantwoorde, ondernomen of afgesloten gepusht is.</span><span class="sxs-lookup"><span data-stu-id="e7776-186">Audience targeting can be based on hello feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="e7776-187">Zie ook</span><span class="sxs-lookup"><span data-stu-id="e7776-187">See also</span></span>
* <span data-ttu-id="e7776-188">[UI - Reach - documentatie nieuw Push criterium][Link 28]</span><span class="sxs-lookup"><span data-stu-id="e7776-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="e7776-189">Inhoud van Polls</span><span class="sxs-lookup"><span data-stu-id="e7776-189">Content of Polls</span></span>
![Reach-Content2][31] 

<span data-ttu-id="e7776-191">Vul in het Hallo-titel, beschrijving en knop tekst van uw aankondiging.</span><span class="sxs-lookup"><span data-stu-id="e7776-191">Fill in hello title, description, and button texts of your announcement.</span></span> <span data-ttu-id="e7776-192">Vervolgens voegt u vragen en opties voor Hallo antwoorden tooyour vragen.</span><span class="sxs-lookup"><span data-stu-id="e7776-192">Then, add questions and choices for hello answers tooyour questions.</span></span>
<span data-ttu-id="e7776-193">U kunt een doelgroep van een toekomstige campagne op basis van feedback van reach Hallo van hoe gebruikers toothis campagne gereageerd richten.</span><span class="sxs-lookup"><span data-stu-id="e7776-193">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="e7776-194">Doelgroepen kan zijn gebaseerd op of deze campagne zojuist, beantwoorde, ondernomen of afgesloten gepusht is.</span><span class="sxs-lookup"><span data-stu-id="e7776-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="e7776-195">Doelgroepen kan ook worden gebaseerd op Poll antwoord feedback, waar de vraag en antwoord keuze hello worden gebruikt als criteria.</span><span class="sxs-lookup"><span data-stu-id="e7776-195">Audience targeting can also be based on Poll answer feedback, where hello question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="e7776-196">Zie ook</span><span class="sxs-lookup"><span data-stu-id="e7776-196">See also</span></span>
* <span data-ttu-id="e7776-197">[UI - Reach - documentatie nieuw Push criterium][Link 28]</span><span class="sxs-lookup"><span data-stu-id="e7776-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="e7776-198">Inhoud van het gegevens-Pushes</span><span class="sxs-lookup"><span data-stu-id="e7776-198">Content of Data Pushes</span></span>
![Reach-Content3][32] 

### <a name="choose-hello-type-of-your-data"></a><span data-ttu-id="e7776-200">Hallo-type van uw gegevens kiezen:</span><span class="sxs-lookup"><span data-stu-id="e7776-200">Choose hello type of your data:</span></span>
* <span data-ttu-id="e7776-201">Tekst</span><span class="sxs-lookup"><span data-stu-id="e7776-201">Text</span></span>
* <span data-ttu-id="e7776-202">Binaire gegevens</span><span class="sxs-lookup"><span data-stu-id="e7776-202">Binary data</span></span>
* <span data-ttu-id="e7776-203">Base64-gegevens</span><span class="sxs-lookup"><span data-stu-id="e7776-203">Base64 data</span></span>

### <a name="define-hello-content-of-your-data"></a><span data-ttu-id="e7776-204">Hallo-inhoud van uw gegevens definiëren</span><span class="sxs-lookup"><span data-stu-id="e7776-204">Define hello content of your data</span></span>
* <span data-ttu-id="e7776-205">Als u tekstgegevens toopush hebt geselecteerd, tekst kopiëren en plakken Hallo in Hallo 'inhoud' vak.</span><span class="sxs-lookup"><span data-stu-id="e7776-205">If you selected toopush text data, copy and paste hello text into hello "content" box.</span></span>
* <span data-ttu-id="e7776-206">Als u toopush geselecteerd binair of base64-gegevens gebruiken Hallo 'uw bestand uploadt' knop tooupload uw bestand.</span><span class="sxs-lookup"><span data-stu-id="e7776-206">If you selected toopush either binary or base64 data, use hello "upload your file" button tooupload your file.</span></span>
* <span data-ttu-id="e7776-207">U kunt een doelgroep van een toekomstige campagne op basis van feedback van reach Hallo van hoe gebruikers toothis campagne gereageerd richten.</span><span class="sxs-lookup"><span data-stu-id="e7776-207">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="e7776-208">Doelgroepen kan zijn gebaseerd op of deze campagne zojuist, beantwoorde, ondernomen of afgesloten gepusht is.</span><span class="sxs-lookup"><span data-stu-id="e7776-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="e7776-209">Zie ook</span><span class="sxs-lookup"><span data-stu-id="e7776-209">See also</span></span>
* <span data-ttu-id="e7776-210">[UI - Reach - documentatie nieuw Push criterium][Link 28]</span><span class="sxs-lookup"><span data-stu-id="e7776-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="e7776-211">Inhoud van de tegels (alleen Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="e7776-211">Content of Tiles (Windows Phone only)</span></span>
![Reach-Content4][33]

### <a name="define-hello-content-of-your-tile"></a><span data-ttu-id="e7776-213">Hallo-inhoud van uw tegel definiëren</span><span class="sxs-lookup"><span data-stu-id="e7776-213">Define hello content of your tile</span></span>
<span data-ttu-id="e7776-214">de nettolading van de tegel Hallo is Hallo tekst toobe weergegeven in de tegel Hallo van uw app op Windows Phone-apparaten.</span><span class="sxs-lookup"><span data-stu-id="e7776-214">hello tile payload is hello text toobe displayed in hello tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="e7776-215">Een tegel push is Hallo Microsoft Push Notification Service (MPNS) versie van een native pushberichten voor Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="e7776-215">A tile push is hello Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="e7776-216">Hallo tegel push type is het enige push type hello, die geen antwoord en dus Hallo doelgroep van toekomstige campagnes van Hallo resultaten van een tegel pushcampagne kan niet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e7776-216">hello tile push type is hello only push type that does not have a response and so hello audience of future campaigns can't be built on hello results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="e7776-217">Zie ook</span><span class="sxs-lookup"><span data-stu-id="e7776-217">See also</span></span>
* <span data-ttu-id="e7776-218">[API - Reach API - documentatie Native Pushberichten][Link 4]</span><span class="sxs-lookup"><span data-stu-id="e7776-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

