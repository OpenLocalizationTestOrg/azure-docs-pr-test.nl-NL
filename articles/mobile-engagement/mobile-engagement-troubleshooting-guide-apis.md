---
title: Azure Mobile Engagement Troubleshooting Guide - API 's
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
ms.openlocfilehash: a7ae0a83046f2d67b790f672dcd3ae261987357a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-api-issues"></a><span data-ttu-id="c53c1-103">Gids voor probleemoplossing voor problemen die API</span><span class="sxs-lookup"><span data-stu-id="c53c1-103">Troubleshooting guide for API issues</span></span>
<span data-ttu-id="c53c1-104">Hieronder vindt u mogelijke problemen die optreden bij de wisselwerking tussen beheerders met Azure Mobile Engagement via de API's.</span><span class="sxs-lookup"><span data-stu-id="c53c1-104">The following are possible issues you may encounter with how administrators interact with Azure Mobile Engagement via the APIs.</span></span>

## <a name="syntax-issues"></a><span data-ttu-id="c53c1-105">Syntaxis problemen</span><span class="sxs-lookup"><span data-stu-id="c53c1-105">Syntax issues</span></span>
### <a name="issue"></a><span data-ttu-id="c53c1-106">Probleem</span><span class="sxs-lookup"><span data-stu-id="c53c1-106">Issue</span></span>
* <span data-ttu-id="c53c1-107">Syntaxisfouten met behulp van de API (of onverwacht gedrag).</span><span class="sxs-lookup"><span data-stu-id="c53c1-107">Syntax Errors using the API (or unexpected behavior).</span></span>

### <a name="causes"></a><span data-ttu-id="c53c1-108">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="c53c1-108">Causes</span></span>
* <span data-ttu-id="c53c1-109">Problemen met de syntaxis:</span><span class="sxs-lookup"><span data-stu-id="c53c1-109">Syntax issues:</span></span>
  * <span data-ttu-id="c53c1-110">Controleer of de syntaxis van de specifieke API die u gebruikt om te bevestigen dat de optie beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="c53c1-110">Make sure to check the Syntax of the specific API you are using to confirm that the option is available.</span></span>
  * <span data-ttu-id="c53c1-111">Een veelvoorkomend probleem met het gebruik van de API is gehaald de Reach API en de Push-API (de meeste taken moeten worden uitgevoerd met de Reach API in plaats van de Push-API).</span><span class="sxs-lookup"><span data-stu-id="c53c1-111">A common issue with API usage is to confuse the Reach API and the Push API (most tasks should be performed with the Reach API instead of the Push API).</span></span> 
  * <span data-ttu-id="c53c1-112">Een andere veel voorkomende problemen met de SDK-integratie en het gebruik van de API is gehaald de SDK-sleutel en de API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="c53c1-112">Another common issue with SDK integration and API usage is to confuse the SDK Key and the API Key.</span></span>
  * <span data-ttu-id="c53c1-113">Scripts die verbinding met de API's maken nodig om gegevens te verzenden ten minste elke 10 minuten of de verbinding wordt time-out (met name voor Monitor API scripts luisteren naar gegevens).</span><span class="sxs-lookup"><span data-stu-id="c53c1-113">Scripts that connect to the APIs need to send data at least every 10 minutes or the connection will time out (especially common in Monitor API scripts listening for data).</span></span> <span data-ttu-id="c53c1-114">Om te voorkomen dat time-outs, hebt u uw script een ping XMPP elke 10 minuten aan de sessie keepalive met de server verzenden.</span><span class="sxs-lookup"><span data-stu-id="c53c1-114">To prevent timeouts, have your script send an XMPP ping every 10 minutes to keep the session alive with the server.</span></span>

### <a name="see-also"></a><span data-ttu-id="c53c1-115">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c53c1-115">See also</span></span>
* <span data-ttu-id="c53c1-116">[API-documentatie][Link 4]</span><span class="sxs-lookup"><span data-stu-id="c53c1-116">[API Documentation][Link 4]</span></span>
* [<span data-ttu-id="c53c1-117">XMPP Protocol Info</span><span class="sxs-lookup"><span data-stu-id="c53c1-117">XMPP Protocol Info</span></span>](http://xmpp.org/extensions/xep-0199.html)

## <a name="unable-to-use-the-api-to-perform-the-same-action-available-in-the-azure-mobile-engagement-ui"></a><span data-ttu-id="c53c1-118">Kan de API gebruiken om uit te voeren dezelfde actie beschikbaar is in de gebruikersinterface van Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c53c1-118">Unable to use the API to perform the same action available in the Azure Mobile Engagement UI</span></span>
### <a name="issue"></a><span data-ttu-id="c53c1-119">Probleem</span><span class="sxs-lookup"><span data-stu-id="c53c1-119">Issue</span></span>
* <span data-ttu-id="c53c1-120">Een actie die van de Azure Mobile Engagement-gebruikersinterface werkt werkt van de gerelateerde Azure Mobile Engagement API niet.</span><span class="sxs-lookup"><span data-stu-id="c53c1-120">An action that works from the Azure Mobile Engagement UI doesn't work from the related Azure Mobile Engagement API.</span></span>

### <a name="causes"></a><span data-ttu-id="c53c1-121">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="c53c1-121">Causes</span></span>
* <span data-ttu-id="c53c1-122">Bevestigen dat u dezelfde actie vanaf de Azure Mobile Engagement-gebruikersinterface uitvoeren kunt, ziet u dat u deze functie van Azure Mobile Engagement correct hebt geïntegreerd met de SDK.</span><span class="sxs-lookup"><span data-stu-id="c53c1-122">Confirming that you can perform the same action from the Azure Mobile Engagement UI shows that you have correctly integrated this feature of Azure Mobile Engagement with the SDK.</span></span>

### <a name="see-also"></a><span data-ttu-id="c53c1-123">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c53c1-123">See also</span></span>
* <span data-ttu-id="c53c1-124">[UI-documentatie][Link 1]</span><span class="sxs-lookup"><span data-stu-id="c53c1-124">[UI Documentation][Link 1]</span></span>

## <a name="error-messages"></a><span data-ttu-id="c53c1-125">Foutberichten</span><span class="sxs-lookup"><span data-stu-id="c53c1-125">Error Messages</span></span>
### <a name="issue"></a><span data-ttu-id="c53c1-126">Probleem</span><span class="sxs-lookup"><span data-stu-id="c53c1-126">Issue</span></span>
* <span data-ttu-id="c53c1-127">Foutcodes met behulp van de API weergegeven tijdens runtime, of in Logboeken.</span><span class="sxs-lookup"><span data-stu-id="c53c1-127">Error codes using the API displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="c53c1-128">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="c53c1-128">Causes</span></span>
* <span data-ttu-id="c53c1-129">Dit is een samengestelde lijst met algemene API status codes getallen voor verwijzing en voorlopige probleemoplossing:</span><span class="sxs-lookup"><span data-stu-id="c53c1-129">Here is a composite list of common API status codes numbers for reference and preliminary troubleshooting:</span></span>
  
        200        Success.
        200        Account updated: device registered, associated, updated, or removed from the current account.
        200        Returns a list of projects as a JSON object or an authentication token generated and returned in the response’s body.
        201        Account created.
        400        Invalid parameter or validation exception (check payload for details). The parameters provided to the API or service are invalid. In this case, the HTTP response will embed more details. Make sure to test for the MIME type of the response as the payload can either be plain text or a JSON object.
        401        Authentication error. No user is currently authenticated or connected (check the AppID and SDK key).
        402        Billing lock. The application is either off its quotas or is currently in a bad billing state.
        403        The application is not enabled or the specific API is disabled for this application.
        403        Unauthorized access to the project or application, invalid access key (the key must match the one provided when created).
        403        Campaign specific errors: campaign must be finished (or has already been activated), the suspend action can only be performed on an scheduled campaign, cannot finish a campaign that is not currently “in progress”, campaign must be “in progress” and the campaign’s property named, manual Push must be set to true.
        403        The email address is already associated to another account (a super user for instance). No authentication token will be generated.
        404        Application, device, campaign, or project identifier not found.
        404        Query parameter is invalid JSON or has a field with an unexpected value.
        404        The email address is not associated with an account. Please create or update the account first.
        405        Invalid HTTP method (GET, POST, etc.) or trying to edit a read only segment (i.e. add or update or delete a criterion). A segment becomes read only after it has been computed for the first time.
        409        Name already associated to a different device ID or campaign.
        413        Too many device identifiers (current limit is 1,000), POST URL encoded entity is over 2MB, or the period is too large to be displayed (the server didn’t retrieve the analytics because the user request is for a period that is too large).
        503        Analytics not available yet (the requested information is not computed yet for an application).
        504        The server was not able to handle your request in a reasonable time (if you make multiple calls to an API very quickly, try to make one call at a time and spread the calls out over time).

### <a name="see-also"></a><span data-ttu-id="c53c1-130">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c53c1-130">See also</span></span>
* <span data-ttu-id="c53c1-131">[API-documentatie - voor gedetailleerde fouten op elke specifieke API][Link 4]</span><span class="sxs-lookup"><span data-stu-id="c53c1-131">[API Documentation - for detailed errors on each specific API][Link 4]</span></span>

## <a name="silent-failures"></a><span data-ttu-id="c53c1-132">Achtergrond fouten</span><span class="sxs-lookup"><span data-stu-id="c53c1-132">Silent failures</span></span>
### <a name="issue"></a><span data-ttu-id="c53c1-133">Probleem</span><span class="sxs-lookup"><span data-stu-id="c53c1-133">Issue</span></span>
* <span data-ttu-id="c53c1-134">API-actie is mislukt met er is geen foutbericht weergegeven tijdens runtime, of in Logboeken.</span><span class="sxs-lookup"><span data-stu-id="c53c1-134">API action fails with no error message displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="c53c1-135">Oorzaken</span><span class="sxs-lookup"><span data-stu-id="c53c1-135">Causes</span></span>
* <span data-ttu-id="c53c1-136">Aantal items wordt in de Azure Mobile Engagement-gebruikersinterface wordt uitgeschakeld als ze zijn niet correct geïntegreerd maar achtergrond mislukken van de API, dus moet u dezelfde functionaliteit van de gebruikersinterface om te zien als werkt testen.</span><span class="sxs-lookup"><span data-stu-id="c53c1-136">Many items will be disabled in the Azure Mobile Engagement UI if they aren't integrated correctly, but will fail silently from the API, so remember to test the same functionality from the UI to see if it works.</span></span>
* <span data-ttu-id="c53c1-137">Azure Mobile Engagement en veel geavanceerde functies van Azure Mobile Engagement u probeert te gebruiken, moeten afzonderlijk integreren in uw app met de SDK als afzonderlijke stappen voordat u ze kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c53c1-137">Azure Mobile Engagement, and many advanced features of Azure Mobile Engagement you are attempting to use, need to be individually integrated into your app with the SDK as separate steps before you can use them.</span></span>

### <a name="see-also"></a><span data-ttu-id="c53c1-138">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c53c1-138">See also</span></span>
* <span data-ttu-id="c53c1-139">[Troubleshooting Guide - SDK][Link 25]</span><span class="sxs-lookup"><span data-stu-id="c53c1-139">[Troubleshooting Guide - SDK][Link 25]</span></span>

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

