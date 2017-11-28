---
title: aaaAzure AD v2 JS SPA begeleide Setup - Test | Microsoft Docs
description: Hoe een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen in JavaScript SPA-toepassingen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="80127-103">Testen van uw code</span><span class="sxs-lookup"><span data-stu-id="80127-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="80127-104">Testen met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="80127-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="80127-105">Als u van Visual Studio gebruikmaakt, drukt u op `F5` toorun uw project: Hallo browser wordt geopend en stuurt u te*http://localhost: {poort}* waarin u zien hoe Hallo *Microsoft Graph-API aanroepen* knop.</span><span class="sxs-lookup"><span data-stu-id="80127-105">If you are using Visual Studio, press `F5` toorun your project: hello browser opens and directs you too*http://localhost:{port}* where you see hello *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="80127-106">Testen met Python of een andere webserver</span><span class="sxs-lookup"><span data-stu-id="80127-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="80127-107">Als u Visual Studio niet gebruikt, zorg er dan de webserver wordt gestart en deze is geconfigureerd toolisten tooa TCP-poort op basis van het Hallo-map met uw *index.html* bestand.</span><span class="sxs-lookup"><span data-stu-id="80127-107">If you are not using Visual Studio, make sure your web server is started and it is configured toolisten tooa TCP port based on hello folder containing your *index.html* file.</span></span> <span data-ttu-id="80127-108">Voor Python, u kunt beginnen met luisteren toohello poort door te voeren in Hallo opdracht vragen / terminal, vanuit de map van de app Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="80127-108">For Python, you can start listening toohello port by running hello in hello command prompt/ terminal, from hello app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="80127-109">Open de browser Hallo en het type *http://localhost: 8080* of *http://localhost: {poort}* - hello *poort* overeenkomt met toohello-poort die uw webserver controleert op.</span><span class="sxs-lookup"><span data-stu-id="80127-109">Then, open hello browser and type *http://localhost:8080* or *http://localhost:{port}* - where hello *port* corresponds toohello port that your web server is listening to.</span></span> <span data-ttu-id="80127-110">U ziet Hallo-inhoud van uw pagina index.html Hello *Microsoft Graph-API aanroepen* knop.</span><span class="sxs-lookup"><span data-stu-id="80127-110">You should see hello contents of your index.html page with hello *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="80127-111">Uw toepassing testen</span><span class="sxs-lookup"><span data-stu-id="80127-111">Test your application</span></span>

<span data-ttu-id="80127-112">Na het Hallo-browser laadt uw *index.html*, klikt u op Hallo *Microsoft Graph-API aanroepen* knop.</span><span class="sxs-lookup"><span data-stu-id="80127-112">After hello browser loads your *index.html*, click hello *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="80127-113">Als dit Hallo eerst, Hallo browser stuurt u toohello Microsoft Azure Active Directory-v2-eindpunt, waar u zich gevraagd toosign in.</span><span class="sxs-lookup"><span data-stu-id="80127-113">If this is hello first time, hello browser redirects you toohello Microsoft Azure Active Directory v2 endpoint, where you are  prompted toosign in.</span></span>
 
![Schermopname van een steekproef](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="80127-115">Toestemming</span><span class="sxs-lookup"><span data-stu-id="80127-115">Consent</span></span>
<span data-ttu-id="80127-116">Hallo eerste keer tooyour toepassing aanmeldt, krijgt u een toestemming scherm vergelijkbare toohello volgende, waarbij u tooaccept moet:</span><span class="sxs-lookup"><span data-stu-id="80127-116">hello very first time you sign in tooyour application, you are presented with a consent screen similar toohello following, where you need tooaccept:</span></span>

 ![Toestemming scherm](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="80127-118">Verwachte resultaten</span><span class="sxs-lookup"><span data-stu-id="80127-118">Expected results</span></span>
<span data-ttu-id="80127-119">U ziet gebruikersprofielgegevens door Hallo Microsoft Graph API-aanroep antwoord geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="80127-119">You should see user profile information returned by hello Microsoft Graph API call response.</span></span>
 
 ![Resultaten](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="80127-121">Zie ook basisinformatie over Hallo token verkregen in Hallo *Access Token* en *Token ID-Claims* vakken.</span><span class="sxs-lookup"><span data-stu-id="80127-121">You also see basic information about hello token acquired in hello *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="80127-122">Meer informatie over bereikwaarden en gedelegeerde machtigingen</span><span class="sxs-lookup"><span data-stu-id="80127-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="80127-123">Hallo Microsoft Graph API vereist Hallo `user.read` tooread Hallo gebruikersprofiel bereik.</span><span class="sxs-lookup"><span data-stu-id="80127-123">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="80127-124">Deze scope wordt automatisch toegevoegd standaard in elke toepassing die wordt geregistreerd op onze portal voor wachtwoordregistratie.</span><span class="sxs-lookup"><span data-stu-id="80127-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="80127-125">Sommige andere API's voor Microsoft Graph evenals aangepaste API's voor uw back-endserver moet mogelijk extra scopes.</span><span class="sxs-lookup"><span data-stu-id="80127-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="80127-126">Bijvoorbeeld: voor Microsoft Graph Hallo bereik `Calendars.Read` agenda's van vereiste toolist Hallo gebruikers is.</span><span class="sxs-lookup"><span data-stu-id="80127-126">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="80127-127">In volgorde Hallo tooaccess kalender van de gebruiker in de context van een toepassing hello, moet u tooadd hello `Calendars.Read` registratiegegevens van machtiging toohello toepassing gedelegeerd en voeg vervolgens Hallo `Calendars.Read` bereik toohello `acquireTokenSilent` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="80127-127">In order tooaccess hello user’s calendar in hello context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="80127-128">Hallo gebruiker mogelijk gevraagd om extra toestemmingen als u het aantal scopes Hallo verhogen.</span><span class="sxs-lookup"><span data-stu-id="80127-128">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<span data-ttu-id="80127-129">Als u een back-end API niet vereist een bereik (niet aanbevolen), kunt u Hallo `clientId` als bereik in Hallo Hallo `acquireTokenSilent` en/of `acquireTokenRedirect` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="80127-129">If a backend API does not require a scope (not recommended), you can use hello `clientId` as hello scope in hello `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
