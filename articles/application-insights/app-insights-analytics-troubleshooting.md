---
title: aaaTroubleshoot analyses in Azure Application Insights | Microsoft Docs
description: 'Problemen met Application Insights analytics? Begin hier. '
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="12156-104">Problemen met analyses in Application Insights oplossen</span><span class="sxs-lookup"><span data-stu-id="12156-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="12156-105">Problemen met [Application Insights Analytics](app-insights-analytics.md)?</span><span class="sxs-lookup"><span data-stu-id="12156-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="12156-106">Begin hier.</span><span class="sxs-lookup"><span data-stu-id="12156-106">Start here.</span></span> <span data-ttu-id="12156-107">Analytics is een krachtige zoekfunctie Hallo van Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="12156-107">Analytics is hello powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="12156-108">Limieten</span><span class="sxs-lookup"><span data-stu-id="12156-108">Limits</span></span>
* <span data-ttu-id="12156-109">Momenteel zijn queryresultaten beperkt toojust over een week van afgelopen gegevens.</span><span class="sxs-lookup"><span data-stu-id="12156-109">At present, query results are limited toojust over a week of past data.</span></span>
* <span data-ttu-id="12156-110">We testen op browsers: meest recente edities van Chrome, rand en Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="12156-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="12156-111">Bekende incompatibele browser-extensies</span><span class="sxs-lookup"><span data-stu-id="12156-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="12156-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="12156-112">Ghostery</span></span>

<span data-ttu-id="12156-113">Hallo uitbreiding uitschakelen of een andere browser gebruikt.</span><span class="sxs-lookup"><span data-stu-id="12156-113">Disable hello extension or use a different browser.</span></span>

## <span data-ttu-id="12156-114"><a name="e-a"></a>'Fout'</span><span class="sxs-lookup"><span data-stu-id="12156-114"><a name="e-a"></a> "Unexpected error"</span></span>
![Onverwachte foutscherm](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="12156-116">Er is een interne fout opgetreden tijdens de runtime portal: niet-verwerkte uitzondering.</span><span class="sxs-lookup"><span data-stu-id="12156-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="12156-117">Hallo browsercache reinigen.</span><span class="sxs-lookup"><span data-stu-id="12156-117">Clean hello browser's cache.</span></span> 

## <span data-ttu-id="12156-118"><a name="e-b"></a>403... Probeer tooreload</span><span class="sxs-lookup"><span data-stu-id="12156-118"><a name="e-b"></a>403 ... please try tooreload</span></span>
![403... Probeer tooreload](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="12156-120">Een verificatie gerelateerde fout (tijdens de verificatie of access token genereren).</span><span class="sxs-lookup"><span data-stu-id="12156-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="12156-121">Hallo portal heeft misschien geen enkele manier te herstellen zonder browserinstellingen te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="12156-121">hello portal may have no way too recover without changing browser settings.</span></span>

* <span data-ttu-id="12156-122">Controleer of [cookies van derden zijn ingeschakeld](#cookies) in Hallo browser.</span><span class="sxs-lookup"><span data-stu-id="12156-122">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 

## <span data-ttu-id="12156-123"><a name="authentication"></a>403... beveiligingszone controleren</span><span class="sxs-lookup"><span data-stu-id="12156-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403.. .verify beveiligingszone](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="12156-125">Een verificatie gerelateerde fout (tijdens de verificatie of access token genereren).</span><span class="sxs-lookup"><span data-stu-id="12156-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="12156-126">Hallo portal heeft misschien geen enkele manier te herstellen zonder browserinstellingen te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="12156-126">hello portal may have no way too recover without changing browser settings.</span></span>

1. <span data-ttu-id="12156-127">Controleer of [cookies van derden zijn ingeschakeld](#cookies) in Hallo browser.</span><span class="sxs-lookup"><span data-stu-id="12156-127">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 
2. <span data-ttu-id="12156-128">Hebt u een favoriet, bladwijzer of opgeslagen koppeling tooopen Hallo Analytics-portal gebruikt?</span><span class="sxs-lookup"><span data-stu-id="12156-128">Did you use a favorite, bookmark or saved link tooopen hello Analytics portal?</span></span> <span data-ttu-id="12156-129">Weet u bent aangemeld met andere referenties dan u hebt gebruikt toen u Hallo koppeling opgeslagen?</span><span class="sxs-lookup"><span data-stu-id="12156-129">Are you signed in with different credentials than you used when you saved hello link?</span></span>
3. <span data-ttu-id="12156-130">Probeer het met een in-persoonlijke/incognito-browservenster (na het sluiten van alle dergelijke vensters).</span><span class="sxs-lookup"><span data-stu-id="12156-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="12156-131">Hebt u tooprovide uw referenties.</span><span class="sxs-lookup"><span data-stu-id="12156-131">You'll have tooprovide your credentials.</span></span> 
4. <span data-ttu-id="12156-132">Open een andere (gewone) browservenster en gaat u te[Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="12156-132">Open another (ordinary) browser window and go too[Azure](https://portal.azure.com).</span></span> <span data-ttu-id="12156-133">Meld u af. Open de koppeling vervolgens en meld u aan met de juiste referenties Hallo.</span><span class="sxs-lookup"><span data-stu-id="12156-133">Sign out. Then open your link and sign in with hello correct credentials.</span></span>
5. <span data-ttu-id="12156-134">Rand en Internet Explorer krijgen gebruikers kunnen ook te deze fout als vertrouwde zone-instellingen worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="12156-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="12156-135">Controleer of beide [Analytics-portal](https://analytics.applicationinsights.io) en [Azure Active Directory-portal](https://portal.azure.com) zijn in Hallo dezelfde beveiligingszone:</span><span class="sxs-lookup"><span data-stu-id="12156-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in hello same security zone:</span></span>
   
   * <span data-ttu-id="12156-136">Open in Internet Explorer, **Internetopties**, **beveiliging**, **vertrouwde websites**, **Sites**:</span><span class="sxs-lookup"><span data-stu-id="12156-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![Dialoogvenster Internet-opties, een site toe te voegen tooTrusted Sites](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="12156-138">In de lijst met Websites van hello, als een van de volgende URL's Hallo opgenomen zijn, controleert u of die Hallo anderen ook zijn opgenomen:</span><span class="sxs-lookup"><span data-stu-id="12156-138">In hello Websites list, if any of hello following URLs are included, make sure that hello others are included also:</span></span>
     
     <span data-ttu-id="12156-139">https://Analytics.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="12156-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="12156-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="12156-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="12156-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="12156-141">https://login.windows.net</span></span>

## <span data-ttu-id="12156-142"><a name="e-d"></a>404 ... Kan de resource niet vinden</span><span class="sxs-lookup"><span data-stu-id="12156-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404... bron is niet gevonden](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="12156-144">Bron van toepassing is verwijderd uit de Application Insights en is niet langer beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="12156-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="12156-145">Dit kan gebeuren als u Hallo URL toohello Analytics pagina opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="12156-145">This can happen if you saved hello URL toohello Analytics page.</span></span>

## <span data-ttu-id="12156-146"><a name="e-e"></a>403 ... Geen autorisatie</span><span class="sxs-lookup"><span data-stu-id="12156-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403... niet geautoriseerd](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="12156-148">U hebt geen machtiging tooopen deze toepassing in Analytics.</span><span class="sxs-lookup"><span data-stu-id="12156-148">You don't have permission tooopen this application in Analytics.</span></span>

* <span data-ttu-id="12156-149">Krijgt u de koppeling Hallo van iemand anders?</span><span class="sxs-lookup"><span data-stu-id="12156-149">Did you get hello link from someone else?</span></span> <span data-ttu-id="12156-150">Vraagt u ze ervoor dat u in Hallo toomake [lezers of inzenders voor deze resourcegroep](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="12156-150">Ask them toomake sure you are in hello [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="12156-151">U Hallo koppeling met andere referenties opslaan?</span><span class="sxs-lookup"><span data-stu-id="12156-151">Did you save hello link using different credentials?</span></span> <span data-ttu-id="12156-152">Open Hallo [Azure-portal](https://portal.azure.com), meldt u zich af en probeer deze koppeling opnieuw opgeven van de juiste referenties Hallo.</span><span class="sxs-lookup"><span data-stu-id="12156-152">Open hello [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing hello correct credentials.</span></span>

## <span data-ttu-id="12156-153"><a name="html-storage"></a>403 ... HTML5-opslag</span><span class="sxs-lookup"><span data-stu-id="12156-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="12156-154">Onze portal maakt gebruik van HTML5 localStorage en sessionStorage.</span><span class="sxs-lookup"><span data-stu-id="12156-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="12156-155">Chrome: Instellingen, privacy, instellingen van de inhoud.</span><span class="sxs-lookup"><span data-stu-id="12156-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="12156-156">Internet Explorer: Internet-opties, tabblad Geavanceerd, beveiliging, de DOM-opslag inschakelen</span><span class="sxs-lookup"><span data-stu-id="12156-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403... Probeer tooenable HTML5-opslag](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="12156-158"><a name="e-g"></a>404 ... Abonnement is niet gevonden</span><span class="sxs-lookup"><span data-stu-id="12156-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ... Abonnement is niet gevonden](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="12156-160">Hallo-URL is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="12156-160">hello URL is invalid.</span></span> 

* <span data-ttu-id="12156-161">Hallo app resource in openen [Application Insights-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="12156-161">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="12156-162">Gebruik vervolgens Hallo Analytics-knop.</span><span class="sxs-lookup"><span data-stu-id="12156-162">Then use hello Analytics button.</span></span>

## <span data-ttu-id="12156-163"><a name="e-h"></a>404... pagina bestaat niet</span><span class="sxs-lookup"><span data-stu-id="12156-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ... Pagina bestaat niet](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="12156-165">Hallo-URL is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="12156-165">hello URL is invalid.</span></span>

* <span data-ttu-id="12156-166">Hallo app resource in openen [Application Insights-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="12156-166">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="12156-167">Gebruik vervolgens Hallo Analytics-knop.</span><span class="sxs-lookup"><span data-stu-id="12156-167">Then use hello Analytics button.</span></span>

## <span data-ttu-id="12156-168"><a name="cookies"></a>Cookies van derden inschakelen</span><span class="sxs-lookup"><span data-stu-id="12156-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="12156-169">Zie [hoe toodisable derden cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), maar zoals u ziet, moeten we te**inschakelen** ze.</span><span class="sxs-lookup"><span data-stu-id="12156-169">See [how toodisable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need too**enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

