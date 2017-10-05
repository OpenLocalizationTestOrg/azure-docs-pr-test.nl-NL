---
title: Azure AD v2 Windows Desktop aan de slag - testen | Microsoft Docs
description: Hoe Windows Desktop .NET (XAML) toepassingen een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 972cc48057c13271d725b0c973c3ccf651ad27c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="db4ca-103">Testen van uw code</span><span class="sxs-lookup"><span data-stu-id="db4ca-103">Test your code</span></span>

<span data-ttu-id="db4ca-104">Testen van uw toepassing, drukt u op `F5` uw project in Visual Studio wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="db4ca-104">In order to test your application, press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="db4ca-105">Het hoofdvenster moet worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="db4ca-105">Your Main Window should appear:</span></span>

![Schermopname van een steekproef](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="db4ca-107">Wanneer u klaar bent om te testen, klikt u op *Microsoft Graph-API aanroepen* en gebruik van een Microsoft Azure Active Directory (organisatieaccount) of een Microsoft-Account (live.com, outlook.com)-account aan te melden.</span><span class="sxs-lookup"><span data-stu-id="db4ca-107">When you're ready to test, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> <span data-ttu-id="db4ca-108">Dit is de eerste keer, ziet u een venster waarin de gebruiker die zich aanmeldt:</span><span class="sxs-lookup"><span data-stu-id="db4ca-108">It it is the first time, you will see a window asking user to sign in:</span></span>

![Aanmelden](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="db4ca-110">Toestemming</span><span class="sxs-lookup"><span data-stu-id="db4ca-110">Consent</span></span>
<span data-ttu-id="db4ca-111">De eerste keer dat u zich aanmeldt bij uw toepassing worden weergegeven met een scherm toestemming vergelijkbaar met de waarin u wilt accepteren expliciet hieronder:</span><span class="sxs-lookup"><span data-stu-id="db4ca-111">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![Toestemming scherm](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="db4ca-113">Verwachte resultaten</span><span class="sxs-lookup"><span data-stu-id="db4ca-113">Expected results</span></span>
<span data-ttu-id="db4ca-114">U ziet gebruikersprofielgegevens geretourneerd door de Microsoft Graph API-aanroep op het scherm API aanroepen resultaten.</span><span class="sxs-lookup"><span data-stu-id="db4ca-114">You should see user profile information returned by the Microsoft Graph API call on the API Call Results screen.</span></span>

<span data-ttu-id="db4ca-115">U ziet ook basisinformatie over het token dat is verkregen `AcquireTokenAsync` of `AcquireTokenSilentAsync` in het vak Token Info:</span><span class="sxs-lookup"><span data-stu-id="db4ca-115">You  should also see basic information about the token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in the Token Info box:</span></span>

|<span data-ttu-id="db4ca-116">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="db4ca-116">Property</span></span>  |<span data-ttu-id="db4ca-117">Indeling</span><span class="sxs-lookup"><span data-stu-id="db4ca-117">Format</span></span>  |<span data-ttu-id="db4ca-118">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="db4ca-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="db4ca-119">Naam</span><span class="sxs-lookup"><span data-stu-id="db4ca-119">Name</span></span> | <span data-ttu-id="db4ca-120">{De volledige gebruikersnaam}</span><span class="sxs-lookup"><span data-stu-id="db4ca-120">{User Full name}</span></span> |<span data-ttu-id="db4ca-121">De voor- en achternaam van de gebruiker</span><span class="sxs-lookup"><span data-stu-id="db4ca-121">The user’s first and last name</span></span>|
|<span data-ttu-id="db4ca-122">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="db4ca-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="db4ca-123">De gebruikersnaam die wordt gebruikt voor het identificeren van de gebruiker</span><span class="sxs-lookup"><span data-stu-id="db4ca-123">The username used to identify the user</span></span>|
|<span data-ttu-id="db4ca-124">Token is verlopen</span><span class="sxs-lookup"><span data-stu-id="db4ca-124">Token Expires</span></span> |<span data-ttu-id="db4ca-125">{Datum-/}</span><span class="sxs-lookup"><span data-stu-id="db4ca-125">{DateTime}</span></span>         |<span data-ttu-id="db4ca-126">De tijd waarop het token verloopt.</span><span class="sxs-lookup"><span data-stu-id="db4ca-126">The time on which the token expires.</span></span> <span data-ttu-id="db4ca-127">MSAL wordt de verloopdatum u door het vernieuwen van het token indien nodig</span><span class="sxs-lookup"><span data-stu-id="db4ca-127">MSAL will extend the expiration date for you by renewing the token when necessary</span></span>|
|<span data-ttu-id="db4ca-128">Toegangstoken</span><span class="sxs-lookup"><span data-stu-id="db4ca-128">Access token</span></span> |<span data-ttu-id="db4ca-129">{Tekenreeks}</span><span class="sxs-lookup"><span data-stu-id="db4ca-129">{String}</span></span>         |<span data-ttu-id="db4ca-130">De tokentekenreeks verzonden die worden verzonden naar HTTP-aanvragen waarvoor de autorisatie-header</span><span class="sxs-lookup"><span data-stu-id="db4ca-130">The token string sent that will be sent to HTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="db4ca-131">Meer informatie over bereikwaarden en gedelegeerde machtigingen</span><span class="sxs-lookup"><span data-stu-id="db4ca-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="db4ca-132">Graph API kan alleen de `user.read` bereik gebruikersprofiel lezen.</span><span class="sxs-lookup"><span data-stu-id="db4ca-132">Graph API requires the `user.read` scope to read user profile.</span></span> <span data-ttu-id="db4ca-133">Deze scope wordt automatisch toegevoegd standaard in elke toepassing die wordt geregistreerd op onze portal voor wachtwoordregistratie.</span><span class="sxs-lookup"><span data-stu-id="db4ca-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="db4ca-134">Vereist extra scopes sommige andere Graph API's, evenals aangepaste API's voor uw back-endserver.</span><span class="sxs-lookup"><span data-stu-id="db4ca-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="db4ca-135">Bijvoorbeeld: voor de grafiek, `Calendars.Read` is vereist tot agenda's van de gebruiker van de lijst.</span><span class="sxs-lookup"><span data-stu-id="db4ca-135">For example, for Graph, `Calendars.Read` is required to list user’s calendars.</span></span> <span data-ttu-id="db4ca-136">Voor toegang tot de agenda van de gebruiker in een context van een toepassing, moet u toevoegen `Calendars.Read` toepassing registratiegegevens gedelegeerd en voeg vervolgens `Calendars.Read` naar de `AcquireTokenAsync` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="db4ca-136">In order to access the user’s calendar in a context of an application, you need to add `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` to the `AcquireTokenAsync` call.</span></span> <span data-ttu-id="db4ca-137">Gebruiker kan worden gevraagd om extra toestemmingen verhogen van het aantal scopes.</span><span class="sxs-lookup"><span data-stu-id="db4ca-137">User may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



