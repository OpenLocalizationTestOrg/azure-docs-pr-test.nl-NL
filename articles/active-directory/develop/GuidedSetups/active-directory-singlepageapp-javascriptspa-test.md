---
title: Azure AD v2 JS SPA begeleide Setup - Test | Microsoft Docs
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
ms.openlocfilehash: c888760ab311e8ac08b1e625bb837f91047db645
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
## <a name="test-your-code"></a><span data-ttu-id="b5f61-103">Testen van uw code</span><span class="sxs-lookup"><span data-stu-id="b5f61-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="b5f61-104">Testen met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b5f61-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="b5f61-105">Als u van Visual Studio gebruikmaakt, drukt u op `F5` aan uw project uitvoeren: de browser wordt geopend en wordt u verwezen *http://localhost: {poort}* waarin u zien hoe de *Microsoft Graph-API aanroepen* knop.</span><span class="sxs-lookup"><span data-stu-id="b5f61-105">If you are using Visual Studio, press `F5` to run your project: the browser opens and directs you to *http://localhost:{port}* where you see the *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="b5f61-106">Testen met Python of een andere webserver</span><span class="sxs-lookup"><span data-stu-id="b5f61-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="b5f61-107">Als u Visual Studio niet gebruikt, zorg er dan de webserver wordt gestart en deze is geconfigureerd om te luisteren naar een TCP-poort op basis van de map met uw *index.html* bestand.</span><span class="sxs-lookup"><span data-stu-id="b5f61-107">If you are not using Visual Studio, make sure your web server is started and it is configured to listen to a TCP port based on the folder containing your *index.html* file.</span></span> <span data-ttu-id="b5f61-108">Voor Python, u kunt beginnen met luisteren op poort door het uitvoeren van de in de opdracht vragen / terminal, vanuit de map van de app:</span><span class="sxs-lookup"><span data-stu-id="b5f61-108">For Python, you can start listening to the port by running the in the command prompt/ terminal, from the app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="b5f61-109">Open de browser en typ vervolgens *http://localhost: 8080* of *http://localhost: {poort}* - waar de *poort* komt overeen met de poort die uw webserver luistert.</span><span class="sxs-lookup"><span data-stu-id="b5f61-109">Then, open the browser and type *http://localhost:8080* or *http://localhost:{port}* - where the *port* corresponds to the port that your web server is listening to.</span></span> <span data-ttu-id="b5f61-110">Ziet u de inhoud van uw pagina index.html met de *Microsoft Graph-API aanroepen* knop.</span><span class="sxs-lookup"><span data-stu-id="b5f61-110">You should see the contents of your index.html page with the *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="b5f61-111">Uw toepassing testen</span><span class="sxs-lookup"><span data-stu-id="b5f61-111">Test your application</span></span>

<span data-ttu-id="b5f61-112">Nadat de browser wordt geladen uw *index.html*, klikt u op de *Microsoft Graph-API aanroepen* knop.</span><span class="sxs-lookup"><span data-stu-id="b5f61-112">After the browser loads your *index.html*, click the *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="b5f61-113">Als dit de eerste keer, de browser wordt doorgestuurd naar het Microsoft Azure Active Directory v2 eindpunt, waarbij u wordt gevraagd aan te melden.</span><span class="sxs-lookup"><span data-stu-id="b5f61-113">If this is the first time, the browser redirects you to the Microsoft Azure Active Directory v2 endpoint, where you are  prompted to sign in.</span></span>
 
![Schermopname van een steekproef](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="b5f61-115">Toestemming</span><span class="sxs-lookup"><span data-stu-id="b5f61-115">Consent</span></span>
<span data-ttu-id="b5f61-116">De eerste keer dat u zich aanmeldt bij uw toepassing krijgt u een toestemming van de volgende strekking scherm waarin u wilt accepteren:</span><span class="sxs-lookup"><span data-stu-id="b5f61-116">The very first time you sign in to your application, you are presented with a consent screen similar to the following, where you need to accept:</span></span>

 ![Toestemming scherm](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="b5f61-118">Verwachte resultaten</span><span class="sxs-lookup"><span data-stu-id="b5f61-118">Expected results</span></span>
<span data-ttu-id="b5f61-119">U ziet gebruikersprofielgegevens geretourneerd door de reactie van Microsoft Graph API-aanroep.</span><span class="sxs-lookup"><span data-stu-id="b5f61-119">You should see user profile information returned by the Microsoft Graph API call response.</span></span>
 
 ![Resultaten](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="b5f61-121">Zie ook basisinformatie over het token dat is verkregen de *Access Token* en *Token ID-Claims* vakken.</span><span class="sxs-lookup"><span data-stu-id="b5f61-121">You also see basic information about the token acquired in the *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="b5f61-122">Meer informatie over bereikwaarden en gedelegeerde machtigingen</span><span class="sxs-lookup"><span data-stu-id="b5f61-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="b5f61-123">De Microsoft Graph API vereist de `user.read` bereik van het gebruikersprofiel lezen.</span><span class="sxs-lookup"><span data-stu-id="b5f61-123">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="b5f61-124">Deze scope wordt automatisch toegevoegd standaard in elke toepassing die wordt geregistreerd op onze portal voor wachtwoordregistratie.</span><span class="sxs-lookup"><span data-stu-id="b5f61-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="b5f61-125">Sommige andere API's voor Microsoft Graph evenals aangepaste API's voor uw back-endserver moet mogelijk extra scopes.</span><span class="sxs-lookup"><span data-stu-id="b5f61-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="b5f61-126">Bijvoorbeeld: voor het bereik van Microsoft Graph `Calendars.Read` is vereist voor een lijst met agenda's van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b5f61-126">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="b5f61-127">Voor toegang tot de agenda van de gebruiker in de context van een toepassing, moet u toevoegen de `Calendars.Read` overgedragen machtigingen voor de toepassingsregistratie-informatie en voeg vervolgens de `Calendars.Read` bereik voor de `acquireTokenSilent` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="b5f61-127">In order to access the user’s calendar in the context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilent` call.</span></span> <span data-ttu-id="b5f61-128">De gebruiker kan gevraagd om extra toestemmingen als u het aantal scopes verhogen.</span><span class="sxs-lookup"><span data-stu-id="b5f61-128">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<span data-ttu-id="b5f61-129">Als u een back-end API niet vereist een bereik (niet aanbevolen), kunt u de `clientId` als het bereik in de `acquireTokenSilent` en/of `acquireTokenRedirect` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="b5f61-129">If a backend API does not require a scope (not recommended), you can use the `clientId` as the scope in the `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
