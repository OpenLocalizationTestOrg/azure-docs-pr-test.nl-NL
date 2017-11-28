---
title: aaaAzure Mobile Engagement Troubleshooting Guide - API 's
description: Troubleshooting Guide voor Azure Mobile Engagement - API 's
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3efc8a52-2b74-4917-b887-815ae8277474
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: piyushjo
ms.openlocfilehash: 5656b6f0f1aaf3e496a168c7cf09b307b9ab2a4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-api-issues"></a><span data-ttu-id="193ee-103">Gids voor probleemoplossing voor problemen die API</span><span class="sxs-lookup"><span data-stu-id="193ee-103">Troubleshooting guide for API issues</span></span>
<span data-ttu-id="193ee-104">Hallo volgen mogelijke problemen die optreden bij hoe beheerders kunnen met Azure Mobile Engagement via Hallo API's communiceren.</span><span class="sxs-lookup"><span data-stu-id="193ee-104">hello following are possible issues you may encounter with how administrators interact with Azure Mobile Engagement via hello APIs.</span></span>

## <a name="syntax-issues"></a><span data-ttu-id="193ee-105">Syntaxis problemen</span><span class="sxs-lookup"><span data-stu-id="193ee-105">Syntax issues</span></span>
### <a name="issue"></a><span data-ttu-id="193ee-106">Probleem</span><span class="sxs-lookup"><span data-stu-id="193ee-106">Issue</span></span>
* <span data-ttu-id="193ee-107">Syntaxisfouten met behulp van API hello (of onverwacht gedrag).</span><span class="sxs-lookup"><span data-stu-id="193ee-107">Syntax Errors using hello API (or unexpected behavior).</span></span>

### <a name="causes"></a><span data-ttu-id="193ee-108">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="193ee-108">Causes</span></span>
* <span data-ttu-id="193ee-109">Problemen met de syntaxis:</span><span class="sxs-lookup"><span data-stu-id="193ee-109">Syntax issues:</span></span>
  * <span data-ttu-id="193ee-110">Zorg ervoor dat toocheck Hallo syntaxis van de specifieke API Hallo u tooconfirm die Hallo optie beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="193ee-110">Make sure toocheck hello Syntax of hello specific API you are using tooconfirm that hello option is available.</span></span>
  * <span data-ttu-id="193ee-111">Een veelvoorkomend probleem met het gebruik van de API is tooconfuse Hallo Reach API en Hallo Push-API (de meeste taken moeten worden uitgevoerd met Hallo Reach API in plaats van Hallo Push-API).</span><span class="sxs-lookup"><span data-stu-id="193ee-111">A common issue with API usage is tooconfuse hello Reach API and hello Push API (most tasks should be performed with hello Reach API instead of hello Push API).</span></span> 
  * <span data-ttu-id="193ee-112">Een andere veel voorkomende problemen met de SDK-integratie en het gebruik van de API is tooconfuse Hallo SDK-sleutel en Hallo API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="193ee-112">Another common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>
  * <span data-ttu-id="193ee-113">Scripts die verbinding maken met API's toohello moeten toosend gegevens ten minste elke 10 minuten of Hallo verbinding time-out (met name voor Monitor API scripts luisteren naar gegevens).</span><span class="sxs-lookup"><span data-stu-id="193ee-113">Scripts that connect toohello APIs need toosend data at least every 10 minutes or hello connection will time out (especially common in Monitor API scripts listening for data).</span></span> <span data-ttu-id="193ee-114">Time-outs voor tooprevent hebben uw script verzenden een ping XMPP elke 10 minuten tookeep Hallo sessie-alive met Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="193ee-114">tooprevent timeouts, have your script send an XMPP ping every 10 minutes tookeep hello session alive with hello server.</span></span>

### <a name="see-also"></a><span data-ttu-id="193ee-115">Zie ook</span><span class="sxs-lookup"><span data-stu-id="193ee-115">See also</span></span>
* <span data-ttu-id="193ee-116">[API-documentatie][Link 4]</span><span class="sxs-lookup"><span data-stu-id="193ee-116">[API Documentation][Link 4]</span></span>
* [<span data-ttu-id="193ee-117">XMPP Protocol Info</span><span class="sxs-lookup"><span data-stu-id="193ee-117">XMPP Protocol Info</span></span>](http://xmpp.org/extensions/xep-0199.html)

## <a name="unable-toouse-hello-api-tooperform-hello-same-action-available-in-hello-azure-mobile-engagement-ui"></a><span data-ttu-id="193ee-118">Kan geen toouse Hallo API tooperform Hallo dezelfde actie beschikbaar is in hello Azure Mobile Engagement-gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="193ee-118">Unable toouse hello API tooperform hello same action available in hello Azure Mobile Engagement UI</span></span>
### <a name="issue"></a><span data-ttu-id="193ee-119">Probleem</span><span class="sxs-lookup"><span data-stu-id="193ee-119">Issue</span></span>
* <span data-ttu-id="193ee-120">Een actie die werkt van Azure Mobile Engagement-UI niet van Hallo werkt Hallo gerelateerde Azure Mobile Engagement-API.</span><span class="sxs-lookup"><span data-stu-id="193ee-120">An action that works from hello Azure Mobile Engagement UI doesn't work from hello related Azure Mobile Engagement API.</span></span>

### <a name="causes"></a><span data-ttu-id="193ee-121">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="193ee-121">Causes</span></span>
* <span data-ttu-id="193ee-122">Bevestigen dat u dezelfde actie van hello Azure Mobile Engagement UI ziet u dat u deze functie van Azure Mobile Engagement met correct hebt geïntegreerd Hallo kunt doen Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="193ee-122">Confirming that you can perform hello same action from hello Azure Mobile Engagement UI shows that you have correctly integrated this feature of Azure Mobile Engagement with hello SDK.</span></span>

### <a name="see-also"></a><span data-ttu-id="193ee-123">Zie ook</span><span class="sxs-lookup"><span data-stu-id="193ee-123">See also</span></span>
* <span data-ttu-id="193ee-124">[UI-documentatie][Link 1]</span><span class="sxs-lookup"><span data-stu-id="193ee-124">[UI Documentation][Link 1]</span></span>

## <a name="error-messages"></a><span data-ttu-id="193ee-125">Foutberichten</span><span class="sxs-lookup"><span data-stu-id="193ee-125">Error Messages</span></span>
### <a name="issue"></a><span data-ttu-id="193ee-126">Probleem</span><span class="sxs-lookup"><span data-stu-id="193ee-126">Issue</span></span>
* <span data-ttu-id="193ee-127">Foutcodes met Hallo API weergegeven tijdens runtime, of in Logboeken.</span><span class="sxs-lookup"><span data-stu-id="193ee-127">Error codes using hello API displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="193ee-128">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="193ee-128">Causes</span></span>
* <span data-ttu-id="193ee-129">Dit is een samengestelde lijst met algemene API status codes getallen voor verwijzing en voorlopige probleemoplossing:</span><span class="sxs-lookup"><span data-stu-id="193ee-129">Here is a composite list of common API status codes numbers for reference and preliminary troubleshooting:</span></span>
  
        200        Success.
        200        Account updated: device registered, associated, updated, or removed from hello current account.
        200        Returns a list of projects as a JSON object or an authentication token generated and returned in hello response’s body.
        201        Account created.
        400        Invalid parameter or validation exception (check payload for details). hello parameters provided toohello API or service are invalid. In this case, hello HTTP response will embed more details. Make sure tootest for hello MIME type of hello response as hello payload can either be plain text or a JSON object.
        401        Authentication error. No user is currently authenticated or connected (check hello AppID and SDK key).
        402        Billing lock. hello application is either off its quotas or is currently in a bad billing state.
        403        hello application is not enabled or hello specific API is disabled for this application.
        403        Unauthorized access toohello project or application, invalid access key (hello key must match hello one provided when created).
        403        Campaign specific errors: campaign must be finished (or has already been activated), hello suspend action can only be performed on an scheduled campaign, cannot finish a campaign that is not currently “in progress”, campaign must be “in progress” and hello campaign’s property named, manual Push must be set tootrue.
        403        hello email address is already associated tooanother account (a super user for instance). No authentication token will be generated.
        404        Application, device, campaign, or project identifier not found.
        404        Query parameter is invalid JSON or has a field with an unexpected value.
        404        hello email address is not associated with an account. Please create or update hello account first.
        405        Invalid HTTP method (GET, POST, etc.) or trying tooedit a read only segment (i.e. add or update or delete a criterion). A segment becomes read only after it has been computed for hello first time.
        409        Name already associated tooa different device ID or campaign.
        413        Too many device identifiers (current limit is 1,000), POST URL encoded entity is over 2MB, or hello period is too large toobe displayed (hello server didn’t retrieve hello analytics because hello user request is for a period that is too large).
        503        Analytics not available yet (hello requested information is not computed yet for an application).
        504        hello server was not able toohandle your request in a reasonable time (if you make multiple calls tooan API very quickly, try toomake one call at a time and spread hello calls out over time).

### <a name="see-also"></a><span data-ttu-id="193ee-130">Zie ook</span><span class="sxs-lookup"><span data-stu-id="193ee-130">See also</span></span>
* <span data-ttu-id="193ee-131">[API-documentatie - voor gedetailleerde fouten op elke specifieke API][Link 4]</span><span class="sxs-lookup"><span data-stu-id="193ee-131">[API Documentation - for detailed errors on each specific API][Link 4]</span></span>

## <a name="silent-failures"></a><span data-ttu-id="193ee-132">Achtergrond fouten</span><span class="sxs-lookup"><span data-stu-id="193ee-132">Silent failures</span></span>
### <a name="issue"></a><span data-ttu-id="193ee-133">Probleem</span><span class="sxs-lookup"><span data-stu-id="193ee-133">Issue</span></span>
* <span data-ttu-id="193ee-134">API-actie is mislukt met er is geen foutbericht weergegeven tijdens runtime, of in Logboeken.</span><span class="sxs-lookup"><span data-stu-id="193ee-134">API action fails with no error message displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="193ee-135">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="193ee-135">Causes</span></span>
* <span data-ttu-id="193ee-136">Aantal items wordt uitgeschakeld in Azure Mobile Engagement gebruikersinterface als ze zijn niet correct worden geïntegreerd, maar mislukken achtergrond van Hallo API, dus onthouden Hallo tootest Hallo dezelfde functionaliteit van Hallo UI toosee als het werkt.</span><span class="sxs-lookup"><span data-stu-id="193ee-136">Many items will be disabled in hello Azure Mobile Engagement UI if they aren't integrated correctly, but will fail silently from hello API, so remember tootest hello same functionality from hello UI toosee if it works.</span></span>
* <span data-ttu-id="193ee-137">Azure Mobile Engagement en veel geavanceerde functies van Azure Mobile Engagement u toouse, moeten toobe afzonderlijk geïntegreerd in uw app Hello SDK als afzonderlijke stappen probeert voordat u ze kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="193ee-137">Azure Mobile Engagement, and many advanced features of Azure Mobile Engagement you are attempting toouse, need toobe individually integrated into your app with hello SDK as separate steps before you can use them.</span></span>

### <a name="see-also"></a><span data-ttu-id="193ee-138">Zie ook</span><span class="sxs-lookup"><span data-stu-id="193ee-138">See also</span></span>
* <span data-ttu-id="193ee-139">[Troubleshooting Guide - SDK][Link 25]</span><span class="sxs-lookup"><span data-stu-id="193ee-139">[Troubleshooting Guide - SDK][Link 25]</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface-home.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
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

